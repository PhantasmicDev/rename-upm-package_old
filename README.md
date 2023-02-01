# Rename UPM Package
An action that will edit and rename files to reflect a name change in your [custom upm package](https://docs.unity3d.com/Manual/CustomPackages.html). Changing the name of a upm package can be tedious and this action can automate editting the package.json and assembly definition files to match your package's new name.

**This action will:**
- package.json
  - Edit 'name' entry.
  - Edit 'displayName' entry.
- Assembly Definition Files
  - Rename Assembly Definition Files to match 'Company.Package' naming convention.
  - Edit 'name' entry.
  - Update 'references' to other asembly definition files that were renamed, if the assembly definition's 'Use GUID' option is unchecked.
  
  ### Notice
  This action assumes that your package follows Unity's [recommended package layout](https://docs.unity3d.com/Manual/cus-layout.html) to correctly find all the assembly definitions files to rename.
