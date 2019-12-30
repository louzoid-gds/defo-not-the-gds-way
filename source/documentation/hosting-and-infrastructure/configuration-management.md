# Use configuration management

Use [configuration management][] to manage, automate and standardise your infrastructure. When using configuration management you store your [infrastructure as code][] in a version control system such as Git.

### Puppet

Use [Puppet][] to configure servers and virtual machines. Puppet is widely used within GDS. It is suitable for most systems and scaleable from the simplest to more complex systems.

If your environment consists of a simple deployment artefact like an [Amazon Machine Image (AMI)][], Puppet may not be necessary, but the process for building that artefact must still be codified and version controlled.

### Terraform

Use [Terraform][] to configure third party cloud infrastructure like Amazon Web Services (AWS) or [Fastly][].

Terraform supports a [large number of providers][], and you can configure it to support multiple environments with different parameters. See the [govuk-aws][] repository as an example.

### Further reading

Find out more about configuration management in the [Service Manual][].

[configuration management]: https://www.digitalocean.com/community/tutorials/an-introduction-to-configuration-management
[infrastructure as code]: https://www.gov.uk/service-manual/technology/manage-your-software-configuration#use-infrastructure-as-code
[Amazon Elastic Compute Cloud (Amazon EC2)]: https://aws.amazon.com/ec2/
[Amazon Machine Image (AMI)]: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html
[Terraform]: https://www.terraform.io/
[Puppet]: https://puppet.com/
[Service Manual]: https://www.gov.uk/service-manual/technology/manage-your-software-configuration#using-configuration-management-tools
[Fastly]: https://www.fastly.com/
[govuk-aws]: https://github.com/alphagov/govuk-aws
[large number of providers]: https://www.terraform.io/docs/providers/
[service domains and DNS]: https://www.gov.uk/service-manual/technology/get-a-domain-name