---
pillar: Operational Excellence
category: Resource naming
online version: https://github.com/microsoft/PSRule.Rules.CAF/blob/main/docs/rules/en/CAF.Name.VM.md
---

# Use standard VM names

## SYNOPSIS

Virtual machine names should use a standard prefix.

## DESCRIPTION

An effective naming convention allows operators to quickly identify resource type, associated workload,
deployment environment and Azure region.

For VMs, the Cloud Adoption Framework recommends using the `vm` prefix.

Requirements for VM names:

- For Windows, at least 1 character, but no more than 15.
- For Linux, at least 1 character, but no more than 64.
- Can include alphanumeric and hyphen characters.
- Can only start with a letter or number, and end with a letter or number.
- VM names must be unique within a resource group.

## RECOMMENDATION

Consider creating VMs with a standard name.
Additionally consider using Azure Policy to only permit creation using a standard naming convention.

## NOTES

This rule does not check if VM names are unique.

To configure this rule:

- Override the `CAF_VirtualMachinePrefix` configuration value with an array of allowed prefixes.
- Override `CAF_UseLowerNames` with `false` to allow mixed case in resource names.
By default only lower-case letters and other supported characters are allowed.
This option affects all resource name rules.

## LINKS

- [Recommended abbreviations for Azure resource types](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations)
- [Azure Well-Architected Framework](https://docs.microsoft.com/en-gb/azure/architecture/framework/devops/app-design#tagging-and-resource-naming)
- [Naming rules and restrictions for Azure resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/resource-name-rules)
