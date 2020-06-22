# Actian AvalancheConnect Templates

## Overview
[Actian DataConnect](https://www.actian.com/data-integration/dataconnect-integration/) Templates allow users to quickly get started with pre-built, runnable integration process designs. These functional templates are process designs that perform operations such as loading data into database/warehouses from different sources or more complex integration workflow patterns involving multiple systems. This repository contains pre-built DataConnect Template packages that can be deployed on Actian Integration Manager or can be executed using an Actian DataConnect Engine. 

## Usage
To run the templates from Avalanche:
 - Download the latest version of the djar from the respective project folder in the repository. For example, you can download latest version of **Avalanche DataLoading Templates** from [here](Templates/2.0/Avalanche/)
 - Create a new configuration from the Integrations tab in Avalanche. Provide a name for your configuration and click create.
 - From the summary page, click the Package Uploaded field. When the Upload Packages & Files dialog appears, drag and drop the desired package (djar) from the templates zip file into the upload files dialog when prompted, then click done. 
 - Now click the Entry Point field and select the process.rtc file associated with your template
 - Select the Macros tab in the upper right hand corner then click add Macro. Drag and drop the macrodef.json file that coresponds to your template into the add macros dialog. Click continue.
   > Macros are symbolic name-value pairs that allow you to provide the input parameters such as URLs, user names and passwords required at runtime without making any changes to the integration. More information about specific macros applicable for the template can be found in the respective template's documentation.
 - Configure the macros applicable for the template.
 - Click on the Details tab in upper right hand corner. This will take you back to the summary page where you will find the Run Configuration button in the upper right hand corner. This button will execute your job. 
 
To run the templates from Integration Manager:
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
