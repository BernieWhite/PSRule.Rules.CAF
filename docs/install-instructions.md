---
author: BernieWhite
---

# Installation

PSRule for CAF supports running within continuous integration (CI) systems or locally.
It is shipped as a PowerShell module which makes it easy to install and distribute updates.

!!! Tip
    PSRule for CAF provides native integration to popular CI systems such as GitHub Actions and Azure Pipelines.
    If you are using a different CI system you can use the local install to run on MacOS,
    Linux, and Windows worker nodes.

## With GitHub Actions

[:octicons-workflow-24: GitHub Action][1]

Install and use PSRule for CAF with GitHub Actions by referencing the `microsoft/ps-rule` action.

=== "Stable"

    Install the latest stable version of PSRule for CAF.

    ```yaml
    - name: Analyze Azure template files
      uses: microsoft/ps-rule@v2.0.0
      with:
        modules: 'PSRule.Rules.CAF'
    ```

=== "Pre-release"

    Install the latest stable or pre-release version of PSRule for CAF.

    ```yaml
    - name: Analyze Azure template files
      uses: microsoft/ps-rule@v2.0.0
      with:
        modules: 'PSRule.Rules.CAF'
        prerelease: true
    ```

This will automatically install compatible versions of all dependencies.

  [1]: https://github.com/marketplace/actions/psrule

## With Azure Pipelines

[:octicons-workflow-24: Extension][2]

Install and use PSRule for CAF with Azure Pipeline by using extension tasks.
Install the extension from the marketplace, then use the `ps-rule-assert` task in pipeline steps.

=== "Stable"

    Install the latest stable version of PSRule for CAF.

    ```yaml
    - task: ps-rule-assert@1
      displayName: Analyze Azure template files
      inputs:
        modules: 'PSRule.Rules.CAF'
    ```

=== "Pre-release"

    Install the latest stable or pre-release version of PSRule for CAF.

    ```yaml
    - task: ps-rule-install@1
      displayName: Install PSRule for CAF (pre-release)
      inputs:
        module: PSRule.Rules.CAF
        prerelease: true

    - task: ps-rule-assert@1
      displayName: Analyze Azure template files
      inputs:
        modules: 'PSRule.Rules.CAF'
    ```

This will automatically install compatible versions of all dependencies.

  [2]: https://marketplace.visualstudio.com/items?itemName=bewhite.ps-rule

## Installing locally

PSRule for CAF can be installed locally from the PowerShell Gallery using PowerShell.
You can also use this option to install on CI workers that are not natively supported.

The following platforms are supported:

- Windows PowerShell 5.1 with .NET Framework 4.7.2 or greater.
- PowerShell 7.1 or greater on MacOS, Linux, and Windows.

The following modules are required for PSRule for CAF:

- PSRule
- PSRule.Rules.Azure
- Az.Accounts
- Az.Resources

The required version of each module will automatically be installed along-side PSRule for CAF.

### Installing PowerShell

PowerShell 7.x can be installed on MacOS, Linux, and Windows but is not installed by default.
For a list of platforms that PowerShell 7.1 is supported on and install instructions see [Get PowerShell][3].

  [3]: https://github.com/PowerShell/PowerShell#get-powershell

### Getting the modules

[:octicons-download-24: Module][module]

PSRule for CAF can be installed or updated from the PowerShell Gallery.
Use the following command line examples from a PowerShell terminal to install or update PSRule for CAF.

=== "For the current user"
    To install PSRule for CAF for the current user use:

    ```powershell
    Install-Module -Name 'PSRule.Rules.CAF' -Repository PSGallery -Scope CurrentUser
    ```

    To update PSRule for CAF for the current user use:

    ```powershell
    Update-Module -Name 'PSRule.Rules.CAF' -Scope CurrentUser
    ```

    This will automatically install compatible versions of all dependencies.

=== "For all users"
    To install PSRule for CAF for all users (requires admin/ root permissions) use:

    ```powershell
    Install-Module -Name 'PSRule.Rules.CAF' -Repository PSGallery -Scope AllUsers
    ```

    To update PSRule for CAF for all users (requires admin/ root permissions) use:

    ```powershell
    Update-Module -Name 'PSRule.Rules.CAF' -Scope AllUsers
    ```

    This will automatically install compatible versions of all dependencies.

### Pre-release versions

To use a pre-release version of PSRule for CAF add the `-AllowPrerelease` switch when calling `Install-Module`,
`Update-Module`, or `Save-Module` cmdlets.

!!! tip
    To install pre-release module versions, the latest version of _PowerShellGet_ may be required.

    ```powershell
    # Install the latest PowerShellGet version
    Install-Module -Name PowerShellGet -Repository PSGallery -Scope CurrentUser -Force
    ```

### Building from source

[:octicons-file-code-24: Source][5]

PSRule for CAF is provided as open source on GitHub.
To build PSRule for CAF from source code:

1. Clone the GitHub [repository][5].
2. Run `./build.ps1` from a PowerShell terminal in the cloned path.

This build script will compile the module and documentation then output the result into `out/modules/PSRule.Rules.CAF`.

  [5]: https://github.com/microsoft/PSRule.Rules.CAF.git

#### Development dependencies

The following dependencies will be automatically installed if the required versions are not present:

- PowerShell modules:
  - PlatyPS
  - Pester
  - PSScriptAnalyzer
  - PowerShellGet
  - PackageManagement
  - InvokeBuild
- Bicep CLI

These dependencies are only required for building and running tests for PSRule for CAF.

Additionally .NET Core SDK v3.1 is required.
.NET Core will not be automatically downloaded and installed.
To download and install the latest SDK see [Download .NET Core 3.1][dotnet].

### Limited access networks

If you are on a network that does not permit Internet access to the PowerShell Gallery,
download the required PowerShell modules on an alternative device that has access.
PowerShell provides the `Save-Module` cmdlet that can be run from a PowerShell terminal to do this.

The following command lines can be used to download the required modules using a PowerShell terminal.
After downloading the modules, copy the module directories to devices with restricted Internet access.

=== "Runtime modules"
    To save PSRule for CAF for offline use:

    ```powershell
    $modules = @('PSRule', 'PSRule.Rules.Azure', 'PSRule.Rules.CAF', 'Az.Accounts', 'Az.Resources')
    Save-Module -Name $modules -Path '.\modules'
    ```

    This will save PSRule for CAF and all dependencies into the `modules` sub-directory.

=== "Development modules"
    To save PSRule for CAF development module dependencies for offline use:

    ```powershell
    $modules = @('PSRule', 'PSRule.Rules.Azure', 'Az.Accounts', 'Az.Resources', 'PlatyPS', 'Pester',
      'PSScriptAnalyzer', 'PowerShellGet', 'PackageManagement', 'InvokeBuild')
    Save-Module -Name $modules -Repository PSGallery -Path '.\modules';
    ```

    This will save required developments dependencies into the `modules` sub-directory.

*[CI]: continuous integration

[module]: https://www.powershellgallery.com/packages/PSRule.Rules.CAF
[dotnet]: https://dotnet.microsoft.com/download/dotnet-core/3.1
