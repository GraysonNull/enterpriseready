+++
date = "2016-10-25T00:00:00Z"
title = "Change Management"
featuresslug = "change-management"
type = "feature"
hero = "/images/change-management.svg"
+++

The operational procedures of many large enterprise organizations generally encourage adherence to written change management policies. For SaaS vendors embracing these procedures means integrating with change controls. There are two different layers to change management SaaS vendors should consider from a product perspective: 1) application level updates to product made by the SaaS vendor 2) account level updates to settings and configurations.

## Application level change management
Enterprises will often set up workflows around your product. When you introduce your latest & greatest features or redesign of your product you need to give the time, tools and collateral to roll out those changes on their end users.

1. Change log - Create and maintain a detailed change log of when new features are released or functionality is removed.
1. Advanced notice - depending on the depth of change, customers may need weeks or months of advanced communication so they have time to relay to their users.
1. Feature enablement - feature flags are quickly becoming a common practice to prevent beta features from reaching customers too early. However, by putting this power into the hands of account admins they can toggle the changes on their account when they’re ready.
1. Provide collateral - enable your customers to deliver the message to their end users by using templates that you create, else each customer will be completing the same work.
**Examples:** Gmail has been doing this for a long time with their Labs features. Dropbox does this with their Early Access features.

## Account level change management
Many modern SaaS applications are moving out of the back office productivity tool suite and are becoming critical to production systems. For these applications, changes to the account settings can impact end users or external systems.

1. Support customer environments - In order to ensure that critical SaaS applications integrate with the upcoming release of the customer’s software, it is important that these applications have support for multiple environments per customer (ie Prod, Staging & Dev).
1. Enable sandbox & canary environments - In the same respect, if an account level settings change is going to be made by the customer, it should be made in a sandbox environment first & then promoted to production (just like we do with our configuration management for servers).
1. Implement approval flows - Most developers won’t commit code to master without a code review from a peer. Most security conscious companies implement this policy with approval flows because there is risk that a rouge actor could inflict harm if able to act independently. In a similar way, it is useful if admins can enable approval flows for application configuration settings.

### Advanced Sandbox functionality
1. Duplicated account settings into a new environment.
1. Save and test sandbox environments
1. Apply changes to production systems
1. Rollback changes to production systems

## Examples:
<DIV style="float:left">
<a href="/zendesk/change-management"><img src="/zendesk/images/example.png" width="300px" align="left" style="margin:0;"/></a>
<DIV class="clearfix"></DIV>
### [Zendesk Change Management](/zendesk/change-management)
</DIV>
