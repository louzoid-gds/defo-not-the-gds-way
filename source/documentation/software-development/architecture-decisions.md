# Documenting architecture decisions

You should record decisions that affect the architecture of your service, in
order to preserve the context of your choices.

As agile projects age, it is sometimes hard to keep track of the reasoning
behind the decisions made. This is especially true as new people join
the projects when those involved in the early stages are no longer around.

It is important to preserve the reasoning so the current team can
include it as context when making their own decisions about changes they need to
make. For example, understanding whether a particular choice was made for the 
sake of expediency and can therefore be changed with little impact, or whether
there were external reasons behind that decision that need to be factored in.

### How to document decisions

Architecture decisions should be stored in version control so there is a
record of what was changed, who by, and when. Decisions that affect a specific
application should be in that application's code repository. You may also want
to store larger-scale decisions in a central documentation repository.

A suggested format is the Architecture Decision Record, proposed by Michael
Nygard in [a blog post](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions)
and since adopted widely. That post describes the format in full, but as a
summary it consists of the following sections:

**Title** A description of the decision (not the problem)

**Status** eg Proposed, Accepted, Superseded

**Context** The facts behind the need to make the decision

**Decision** What the team has decided to do

**Consequences** Both positive and negative consequences of the decision