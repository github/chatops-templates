# dte-templates

Contains templates that can be used by [Dynamic-Template-Engine](https://github.com/github/Dynamic-Template-Engine) node module. This repository showcases how the templates are need to be structured for ensuring proper loading and rendering of the templates.

# About

This repository houses templates utilized by Teams + Github integration code, moreover it showcases how templates can be used with [Dynamic-Template-Engine](https://github.com/github/Dynamic-Template-Engine) node module. 

# Table of contents

- [How to use?](#how-to-use)
- [Using a public repo vs local copy?](#using-a-public-repo-vs-local-copy)
- [Understanding the TransformerConfig](#understanding-the-transformerConfig)
- [Setup](#setup)

## How to use?

The templates can be loaded by [Dynamic-Template-Engine](https://github.com/github/Dynamic-Template-Engine) node module at runtime from either the local copies of templates or from a public github repository. The only requirement for the repository and/or from the local version is to adhere to the pre defined template directory structure with a Transformer Config json file. 

The structure of the template directory either the local or the cloud version should be as follows: 

```
| -> CardTemplate ------------> [CLIENT_NAME] (currently only Teams supported) ------->  [TEMPLATE_ENGINE_NAME] (ex. Liquid, HandleBars)  -------------> Template files
| -> EventTemplate -----------> [TEMPLATE_ENGINE_NAME] (ex. Liquid, HandleBars)  -------------> Template files
| -> TransformerConfig.json (this should have all the template registered for successful loading by the engine. 
```
An example of the above structure: 
```
CardTemplate ---> Teams ---> HandleBars ---> Hello.handlebars 
EventTemplate ---> Liquid ---> World.liquid
```

More Info of how to use the templates with [Dynamic-Template-Engine](https://github.com/github/Dynamic-Template-Engine) can be found [here](https://github.com/github/Dynamic-Template-Engine/tree/master#template-directory-structure)

> :warning: **NOTE**: The names of the folders are case sensitive

## Using a public repo vs local copy?

If the templates you use are generic or do not contain any internal data then having those templates in a public repo allows you to share your templates with the world, helping get user contributions and suggestions. 
If the templates being used have content you wish to keep private, then having the templates as a local copy is the recommended way.

## Understanding the TransformerConfig

The TransformerConfig.json is the file that allows you to load different templates for different tasks. Following is an example TransformConfig.json
```
{
  "cardRenderer":[
    {
      "SourceType": "IssueOpened", // Source type can be any string 
      "ClientType": "Teams", // Has to be an ClientType value currently only Teams is supported
      "TemplateType": "HandleBars", // Has to be TemplateType enum value, currently HandleBars and Liquid are the two supported 
      "TemplateName": "issue_opened.handlebars" // name of the template file 
    },
    {
      "SourceType": "IssueReopened",
      "ClientType": "Teams",
      "TemplateType": "HandleBars",
      "TemplateName": "issue_reopened.handlebars"
    }
  ],
  "partials":[],
  "eventTransformer":[
    {
      "SourceType":"IssueOpened",// Source type can be any string
      "TemplateType":"HandleBars",// Has to be TemplateType enum value, currently HandleBars and Liquid are the two supported 
      "TemplateName":"issue_opened.handlebars" // name of the template file 
    }
  ]
}
```

## Setup

For setting up the dynamic-template-engine to work with a repo follow the [setup instructions of dynamic-template-engine](https://github.com/github/Dynamic-Template-Engine#setup)
