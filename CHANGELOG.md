# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]
### Added
- Created initial rename-package.sh script where the action's logic lives.
  - Renames 'package.json's 'name' entry.
  - Renames and edits 'name' entry for assembly definition files in Runtime, Editor, Tests/Runtime and Tests/Editor to reflect the package's new name.
  - Of the renamed assembly definition files, references to renamed assembly definition files are updated.
