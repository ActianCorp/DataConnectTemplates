# Actian DataConnect Templates

## Overview
[Actian DataConnect](https://www.actian.com/data-integration/dataconnect-integration/) Templates allow users to quickly get started with pre-built, runnable integration process designs. These functional templates are process designs that perform operations such as loading data into database/warehouses from different sources or more complex integration workflow patterns involving multiple systems. This repository contains pre-built DataConnect Template packages that can be deployed on Actian Integration Manager or can be executed using an Actian DataConnect Engine. 

## Usage
To run the templates,
 - Download the latest version of the djar from the respective project folder in the repository. For example, you can download latest version of **Avalanche DataLoading Templates** from [here](Templates/2.0/Avalanche/)
 - Create a configuration on Actian Integration Manager instance using the downloaded djar. This step doesn't apply if you will directly run the template with Actian DataConnect Engine.
 - Configure the macros applicable for the template and run it.
   > Macros are symbolic name-value pairs that allow you to provide the input parameters such as URLs, user names and passwords required at runtime without making any changes to the integration. More information about specific macros applicable for the template can be found in the respective template's documentation.
    
    

## Versions

| Template Version              | DataConnect Version|
| ------------------------------|--------------------|
| [1.0](Templates/1.0)          | >= 11.5.2-46       |
| [2.0 (latest)](Templates/2.0) | >= 11.5.2-65       |

## Project Structure
```
README.md
Templates
    1.0 (version)
        Avalanche (project)
            Packages
                Package1.1.0.djar
                Package2.1.0.djar
            Macros
                Macros1.1.0.json
                Macros2.1.0.json
            README.md
        XYZ (project)
            Packages
                ...
            Macros
                ...
    2.0 (version)
        Avalanche (project)
            ...
        XYZ (project)
            ...
    ...
```
## Links
- [Actian Avalanche](https://www.actian.com/analytic-database/avalanche/)
- [Actian DataConnect](https://www.actian.com/data-integration/dataconnect-integration/)
- [Actian Downloads](https://esd.actian.com/)
- [Actian Documentation Portal](https://docs.actian.com/)
