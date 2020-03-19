# Hardware Process Documentation

## Introduction 
This document details the revamped hardware process template, encapsulating the conventions we expect all our hardware projects to follow.

This process comprises:
* The structure of a hardware project repo
* The standard procedure for updating files in a hardware project
* The outputs of the hardware projects

A hardware project can be segmented into a set of sub-assemblies of components. Each sub-assembly may have further sub-assemblies. If a component can not be decomposed into further sub-assemblies, it is considered a 'primitive'. Each 'primitive' will exist within a separate repo, and projects involing additional components will be assembled from these primitives and other assemblies.

This segmentation of designs encourages re-use of components, and allows for simler management of projects - for example if a component used in multiple projects is changed, it only has to be changed in one repo, and the changes will propogate to all assemblies using it.

If a component comprises multiple parts, but all parts use the same process to manufacture and will always be used together, it will be treated as a single component and thus share the same repo. 

### Why use a standard process template?
Previously, hardware projoect files were spread across different storage locations such as google drive, github and local machines. There was no standard set of guidelines regarding what files should be stored, or in what structure. Updating files was done ad-hoc, and involved more manual work than necessary. It was difficult for collaborators to keep track of changes to files, and was difficult to find specific relevant files, especially for newcomers to the project. 

## Outputs of the Repo
The contents of the repo are packaged into a 'release' upon the merging of a PR. This is a package of files that are forwarded to the manufacturing lab. Based on the contents of this release, the manufacturing lab can manufacture the project either in house or externally.

The release should include:
* All necessary output files needed to build the product
* Test procedures and inputs
* A JSON file describing additional manufacturing parameters not found in the other files


## Repo Structure and contents
A hardware project will be contained within a github repo. The master branch will contain all relevant files for the current version, detailed below:

### Types of repo
While there will a standard template followed by all hardware projects, variants of this repo will be used for different project types. 

#### Electronics
The electronics type is used for PCB projects.
The content of the repo should follow this structure:

* testing
    * test procedure
    * test inputs
* documentation
* source
    * specification
    * Altium source files
* outputs
    * NC_Drill
    * Pick_place
    * BOM
    * gerber files
    * schematic
* Readme.md

#### Mechanical 
The mechanical type is for non-pcb type components - items such as cases and heatsinks:
The content of the repo should follow this structure:

* testing
    * test procedure
    * test inputs
* documentation
* source
    * specification
    * Fusion3D files
* outputs
    * step files
    * stl files
    * dxf files
* Readme.md



### Testing
Each hardware repo should contain a set of test documents.
* The test procedure. This contains details about the tests that a design must pass in order to be merged to the main branch. This includes detailed and easy to follow testing instructions, any parameters that make up the test configuration (e.g. the temperatures that a device must be tested at, the hardware configuration etc.), and the pass conditions for the test.
* The test report. This contains the results of any testing carried out. It should be in a seperate file to the test procedure. This could eventually be in a standard format.

#### Testing utilities
The device repo should only contain the testing intructions and parameters relating to specific tests used in the project. Any test utilities such as test software utilites or hardware rigs should be contained in a seperate repo to simplify re-use across different projects.

### Documentation
This folder contains any documentation to be consumed by a user of the product, for example usage instructions. Any files not intended for an end user should not be here.

### Source
This folder contains source files for the project. These are files that are modifed when changing the design. 

### Outputs
This folder contains any files generated from the files in the source folder.

### Specification
This should be a json file that captures any information about the product that cannot be extracted from the source files. For example, the material or surface finish.

This file should use a standard language and format across all hardware projects.


## Updating the Repo
Updating files within a hardware project repo must follow this process. 

* Check out the master branch. All changes are made to this branch. This ensures that you are working with the most recent version of the project. The modified branch can be pushed to github so others can see and collaborate.
* Create a pull request (PR) on the project repo once all changes have been made. The PR must be titled [major], [minor], or [patch], depending on the changes proposed. This PR will contain:
    - The changed files
    - Any required changes to the specification based on these changes
    - Any required changes to the test procedure
    - Any required changes to any other documentation
* Once a PR has been created, a draft release is generated and passed to the manufactuing lab. Based on this, a new prototype is built, and run through the test procedure. 
* The pass conditions for the tests are detailed within the test procedure.
* If the testing is passed, two or more approvals must be secured by authorized personell. There may be additional discussion and analysis carried out to determine if the changes should be merged. While this happens, the changes remain in the PR.
* Once there is a definitive consensus that the PR should be approved, the PR can be merged to the main branch. Do not approve a PR if you are not completely certain it should be merged. Assume that if you approve a PR, it will be merged. 
* A merged PR should be considered FINAL and IRREVOCABLE. DO NOT MERGE THINGS IF YOU DO NOT WISH TO SEE THEM BEING SOLD TO USERS FOR MONEY.
* Only AFTER the merge is done does the device get a version number. THIS IS ALSO VERY IMPORTANT. Do NOT give a version number to the work before it’s merged.
* The merge also creates a new “release” of the product that the HW operations team must take and bring to production as soon as possible.

