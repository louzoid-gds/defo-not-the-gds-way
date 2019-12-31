# How to track technical debt

While planning for the technical work we do in GDS, we need a common language
between technologists and product people to describe the scale and scope of
technical debt.

The language should enable communication of the benefits of individual pieces
of work that pay down tech debt. It should also enable us to be clearer about
the consequences of not doing something, or leaving a piece of work in a
certain state, and should allow us to track the reduction or accumulation of
technical debt over time.

The process used for tracking debt should not add significant overhead to
planning, and assigning a rating to a piece of technical debt should be quick
and simple.

### Example consequences of tech debt

- Harder to patch security vulnerabilities
- Harder to implement new features
- Harder to onboard new developers
- Consumes too many compute resources
- Too closely coupled to an architecture
- Causes too many support tickets
- Creates too much chore work
- Difficult to debug issues
- Inconsistent architecture

### Example causes of tech debt

- Out of date dependencies
- Hardcoded configuration
- Component has too many responsibilities
- Long running test suite
- Manual deployment task
- Missing documentation
- No admin interface
- Not using lessons learnt since build

### Classifying and measuring

Classifying tech debt uses two factors: the current impact of the consequence
and the effort required to remove the cause. Both are subjectively measured as
high (red), medium (amber) or low (green) with a justification and explanation
of the cause and consequence.

These are subjectively combined into an overall high/medium/low risk rating,
with the reason for the relative weighting also recorded. This rating signifies
the risk and associated cost with not dealing with the item right now. In some
circumstances (such as an upcoming planned rewrite or retirement) we would
accept a high risk as the item would go away naturally anyway. For this reason,
the risks don't necessarily map directly to priorities.

This is similar to how risks are recorded in a Risk Register. High, medium and
low ratings are given for impact and likelihood along with a combined overall
rating based on a decision about the relative importance of the impact and
likelihood. The higher the overall rating, the more the programme should be
concerned about it.

The impact of a piece of technical debt, and the effort required to remove the
cause of it, will change over time. Review recorded items of technical debt at
appropriate periods. For example: if a problematic system was not being
actively worked on at the time a piece of debt was originally recorded, it may
have a low impact rating; if it subsequently becomes worked on again, you
should review the impact.

### Process

Items of Technical Debt should be recorded on a Trello board per product. See
[GOV.UK's board](https://trello.com/b/oPnw6v3r/gov-uk-tech-debt) as an example.
The product's technical leadership will triage these on a fortnightly basis,
agree the assigned ratings and add them to the correct category. They should
also review each item every 3 months.

The product's technical leadership (Technical Architects, Technical Leads, Lead
Developers etc) should use these lists during conversations with Product and
Delivery Managers when prioritising work. Technical debt existing on the
register doesn’t necessarily mean it will be paid down at any point, only that
GOV.UK is conscious of its existence and will take it into account in product
decisions.

Tracking debt as it gets created will follow the same process, with a link to a
Trello card on a team’s backlog for the story that created it. The debt review
process doesn’t make decisions on whether the creation of the debt is the
correct thing to do, that decision stays with the product team.

If something is too small in scope to be included on the board, it should be
recorded in the relevant repository's Github issues. Tech leads should review
these regularly as part of prioritisation.

### Example

> #### Whitehall has its own upload management system
>
> **Cause**: Whitehall’s system for handling uploads of PDFs, CSVs and images
> from publishing users is different to the Asset Manager application used by
> Specialist Publisher and others. This is due to it being developed in
> isolation from another system.
>
> **Consequences**:
>
> - Inconsistent architecture
> - Too closely coupled to physical disk
> - Causes support tickets due to delay in processing attachments
>
> Impact of debt: **High** due to confusion, operational restrictions and
> support burden.
>
> Effort to pay down: **High** due to the technical effort involved in changing
> Whitehall to talk to Asset Manager, implementing missing features in Asset
> Manager and migrating existing assets.
>
> Overall rating: **High**
