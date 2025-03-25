---
author: BernieWhite
---

# Features

The following sections describe key features of PSRule for Cloud Adoption Framework (CAF).

- [Ready to go](#ready-to-go)
- [DevOps](#devops)
- [Cross-platform](#cross-platform)

## Ready to go

The CAF is a set of opinionated recommendations for implementing Azure that can scale to large organizations.
PSRule for CAF provides rules to validate resources and infrastructure as code (IaC) against these recommendations.
Currently PSRule for CAF includes rules for:

- [Recommended naming and tagging conventions][caf-naming-guidance]

Use the built-in rules to start enforcing release processes quickly.
Configure built-in rules to align to organization requirements.
Then layer on your own rules as your organization's requirements mature.
Custom rules can be implemented quickly and work side-by-side with built-in rules.

As new built-in rules are added and improved, download the latest PowerShell module to start using them.

## DevOps

Azure resources can be validated throughout their lifecycle to support a DevOps culture.

From as early as authoring a Azure Resource Manager (ARM) template, resources can be validated offline.
Pre-flight validation can be integrated into a continuous integration (CI) processes to:

- **Shift-left:** Identify configuration issues and provide fast feedback in pull requests.
- **Add quality gates:** Implement quality gates between environments such as development, test and production.
- **Monitor continuously:** Perform ongoing checks for configuration optimization opportunities.

## Cross-platform

PSRule uses modern PowerShell libraries at its core, allowing it to go anywhere PowerShell can go.
PSRule runs on MacOS, Linux and Windows.

To install PSRule for CAF use the `Install-Module` cmdlet within PowerShell.

```powershell
Install-Module -Name PSRule.Rules.CAF -Scope CurrentUser;
```

For additional installation options see [install instructions](install-instructions.md).

[caf-naming-guidance]: https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging
