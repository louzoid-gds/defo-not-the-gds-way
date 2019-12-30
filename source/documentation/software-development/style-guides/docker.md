# Docker

The purpose of this style guide is to provide some conventions for creating
production ready Dockerfiles at GDS. It supplements the official [Dockerfile
reference](https://docs.docker.com/engine/reference/builder/).

### FROM

The `FROM` directive specifies the starting image for your Docker image build.

You should specify your base image using a digest rather than a tag.

i.e. instead of

    FROM alpine:3.9

where `alpine` refers to the image name, and `3.9` refers to the "tag", a short
label used to refer to a particular variant of an image, use

    FROM alpine@sha256:769fddc7cc2f0a1c35abb2f91432e8beecf83916c421420e6a6da9f8975464b6

where "sha256@769fddc7cc2f0a1c35abb2f91432e8beecf83916c421420e6a6da9f8975464b6`
refers to a unique hash representing the particular variant of the image.

The reason for this is the non-immutability of tags. The image referenced by a
tag can be changed, reducing the repeatability of builds. `alpine:3.9` today
may not be the same as `alpine:3.9` tomorrow.

This also provides some protection from a malicious compromise of container
registries - if a malicious actor replaces third party containers _en-masse_,
your image builds will be unaffected.

To obtain the digest, run `docker pull <tag>` e.g.

    $ docker pull alpine:3.9
    3.9: Pulling from library/alpine
    Digest: sha256:769fddc7cc2f0a1c35abb2f91432e8beecf83916c421420e6a6da9f8975464b6
    Status: Image is up to date for alpine:3.9

[Dependabot](https://dependabot.com) has [support for updating `FROM` lines
which use digests](https://github.com/dependabot/dependabot-core/pull/100), so
you can still use Dependabot to keep your images up to date.

One disadvantage of using digests rather than tags is that it makes it harder
to tell which base image is being referenced. It is tempting to add a comment
to the `Dockerfile` explaining which tag the digest refers to but these
comments will rapidly become out of date if you are relying on automated tools
to update your container sources. Instead, when changing the `FROM` line you
should explain what the digest refers to in the corresponding git commit
message.

Also, not all tools fully support referencing images by digest.

### Subshells

Depending on how you specify your directives, Docker may run commands in a
subshell which can lead to loose or unexpected behaviour.

This applies to directives such as `RUN`, `CMD` and `ENTRYPOINT`.

These all have two forms - one taking freeform text and one taking an
array-style syntax. Commands specified via the array-style syntax will be
directly executed via an `execve`-style call, without an enclosing subshell.
This means that shell parameter expansion, pipes and other shell syntax will
not apply. This is more efficient and removes any ambiguity over how the
commands will be interpreted (shells can differ between systems).

In the case of `ENTRYPOINT` (or, if there is no `ENTRYPOINT`, `CMD`), invoking
the command via a subshell means that the shell becomes process ID 1 within the
container and therefore receives signals sent to the container.

Therefore you should try to use the array syntax where possible.

### Process ID (PID) 1

PID 1 is a special process ID in UNIX-like systems. It is responsible for
reaping orphaned child processes, whose parent has exited but haven't been
`waitpid()`'d on. These show up as zombie processes (state `Z`).

It is also the process which will receive signals sent to the container and
whose exit status will be the exit status of the container.

Most programs are therefore unsuitable to be PID 1 within a container, for
example:

- `bash` will not pass signals through to its children, so e.g. `SIGTERM` will
  not lead to the container being shut down. Container orchestration systems
  will usually send the container a `SIGTERM` and if it does not exit in a timely
  manner follow this up with a `SIGKILL` which can lead to slower and unclean
  shutdowns of your software.
- `java` exits with an exit status of 143 when sent a SIGTERM, even if it shuts
  down cleanly.
- `node` does not reap orphaned child processes whose parent has exited.

As a result, projects such as [tini](https://github.com/krallin/tini) exist,
which provide basic `init(1)` functionality. `tini` is now included with the
Docker runtime.

You can make use of `tini` by passing the `--init` option to docker when
running your container which in e.g. AWS ECS can be triggered using the
`initProcessEnabled` task definition parameter. It is also included in Alpine
Linux as the `tini` package, allowing it to be explicitly specified as the
`ENTRYPOINT` for a container.

To avoid users of your container needing to know about `tini`, it is
recommended that you use `tini` to supervise your container processes via this
directive in your `Dockerfile`:

    ENTRYPOINT ["tini", "--"]

or for Java programs, to map an exit status of 143 to 0

    ENTRYPOINT ["tini", "-e", "143", "--"]

This will ensure `tini` is always used regardless of how your container is run,
as `ENTRYPOINT` is part of the [OCI specification](https://github.com/opencontainers/image-spec/blob/master/config.md#image-json).

For further reading see:

* [Avoid running NodeJS as PID 1 under Docker images](https://www.elastic.io/nodejs-as-pid-1-under-docker-images/)
* [docker-node best practices - Handling Kernel Signals](https://github.com/nodejs/docker-node/blob/master/docs/BestPractices.md#handling-kernel-signals)
* [Docker and the PID 1 zombie reaping problem](https://blog.phusion.nl/2015/01/20/docker-and-the-pid-1-zombie-reaping-problem/)
