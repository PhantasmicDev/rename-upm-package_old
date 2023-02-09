# Rename UPM Package
An action that will edit and rename files to reflect a name change in your [custom upm package](https://docs.unity3d.com/Manual/CustomPackages.html). Changing the name of a upm package can be tedious and this action can automate editing the package.json and assembly definition files to match your package's new name.

**This action will:**
- Edit package.json
  - Edit 'name' entry.
  - Edit 'displayName' entry.
- Edit Assembly Definition files
  - Rename Assembly Definition files to match 'Company.Package' naming convention.
  - Edit 'name' entry.
  - Update 'references' entries to other asembly definition files that were renamed, if the assembly definition's 'Use GUID' option is unchecked in the Unity editor.
  
  ### Notice
  This action assumes that your package follows Unity's [recommended package layout](https://docs.unity3d.com/Manual/cus-layout.html) to correctly find all the assembly definitions files to rename.
  
  ## Usage
  
  ```yaml
  steps:
    - uses: PhantasmicDev/rename-upm-package@main
      with:
        # The name of the company or organization developing the package.
        # Required
        company-name: ''
        
        # The diplay name for the package.
        # Required
        package-name: ''
        
        # The domain name to use when generating the full package name 
        # if 'full-name' input is not provided.
        # Default: 'com'
        domain-extension: ''
        
        # The full name for the package with the naming convetion 
        # of 'com.mycompany.mypackage'. If it isn't provided, it will be generated
        # using the provided 'domain-extension', 'company-name' and 'package-name'.
        full-name: ''
        
        # The path to the root folder of your package.
        # Default: ${{ github.workspace }}
        package-root-path: ''
  ```
  
  ### Example
  A workflow dispatch example that renames the package and commits back to the remote repo. This example assumes that the root of the repo is the root of the package so 'package-root-path' input is not required.
  ```yaml
  name: Rename Package
  on:
    # To manually call from 'Actions' tab.
    workflow_dispatch:
      inputs:
        company-name:
          description: Company Name
          type: string
          required: true
        package-name:
          description: Package Name
          type: string
          required: true
  
  # Required to give 'add-and-commit' action permission to write to the remote repo.
  permissions:
    contents: write
  
  jobs:
    Rename:
      runs-on: ubuntu-latest
      steps:
        - uses: actions/checkout@v3
        
        - uses: PhantasmicDev/rename-upm-package@main
          with:
            company-name: "${{ inputs.company-name }}"
            package-name: "${{ inputs.package-name }}"
        
        - name: Commit and Push
          uses: EndBug/add-and-commit@v9.1.1
          with:
            message: Renamed Package
            committer_name: GitHub Actions
            committer_email: 41898282+github-actions[bot]@users.noreply.github.com
  ```
