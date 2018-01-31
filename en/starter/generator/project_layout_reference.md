---
### TRANSLATION INSTRUCTIONS FOR THIS SECTION:
### TRANSLATE THE VALUE OF THE title ATTRIBUTE AND UPDATE THE VALUE OF THE lang ATTRIBUTE.
### DO NOT CHANGE ANY OTHER TEXT.
layout: page
title: Swift Server Generator project layout reference
menu: starter
lang: en
redirect_from: "/starter/generator/project_layout_reference.html"
### END HEADER BLOCK - BEGIN GENERAL TRANSLATION
---
[info]: ../../../assets/info-blue.png
[tip]: ../../../assets/lightbulb-yellow.png
[warning]: ../../../assets/warning-red.png

<div class="titleBlock">
	<h1>Swift Server Generator project layout reference</h1>
</div>

Swift Server Generator generates applications in a layout compatible with [Swift Package Manager](https://swift.org/package-manager/).
The files that populate the application directory depend on the [project type](core_concepts.html#project-type),
[capabilities](core_concepts.html#capabilities) and [services](core_concepts.html#services) selected during creation.

## Common files

The following structure is common to all generated applications:

```
├── LICENSE                           - MIT license for the generated code
├── Sources/                          - Swift source code for the project
│   ├── Application/                  - Swift module for application logic
│   │   └── Application.swift         - Swift code for application logic
│   │   └── InitializationError.swift - Swift code for initialization error
│   └── <application_name>/           - Swift module for executable
│       └── main.swift                - Swift code for executable
├── Tests/                            - Swift source code for the tests
│   ├── ApplicationTests/             - Swift test module
│   │   └── RouteTests.swift          - Swift code for the test implementation
│   └── LinuxMain.swift               - Swift test definition for Linux
├── Package.swift                     - Swift Package Manager configuration file
├── Package.resolved                  - Swift Package Manager resolved packages
├── spec.json                         - Generator specification file for the project
```

There are also a number of hidden files included in all generated applications:

```
├── .gitignore                      - Defines files that should not be added to Git
├── .swift-version                  - Defines the Swift version for this project
├── .swiftservergenerator-project   - Marks this as a Swift Server Generator project
├── .yo-rc.json                     - Yeoman generator configuration file
```

> ![info] Note: `.swiftservergenerator-project` and `.yo-rc.json` are files used by the generator to know where the root of your project is and what kind of project you have. If you don’t need to do any further modifications after initial project generation (such as using the [model generator](command_line_tools.html#model-generator)), use the [single shot option](command_line_tools.html#application-generator).

## Build files

The following are created when the application is built (by `swift build`):

```
├── Packages/                       - Swift source code for resolved dependencies
├── .build/                         - Build metadata, libraries and executables
├── <application_name>.xcodeproj    - Xcode project file
```

## Scaffolded project

The following subsections apply to the [scaffold project type](core_concepts.html#scaffold).
All scaffolded projects will have the following files included:

```
├── README.md                       - Default documentation for the generated project
├── Sources/
│   └── Application/
│       └── Routes/                 - Directory for organising route handler code
```

### README
The `README.md` file contains customized documentation about the contents of the generated
application including selected capabilities and services.

### Swift Metrics

If you select the [embedded metrics dashboard](core_concepts.html#metrics-dashboard-capability) then the following
file will be included in the scaffolded project:

```
├── Sources/                          - Swift source code for the project
│   └── Application/                  - Swift module for application logic
│       └── Metrics.swift             - Swift code for Swift Metrics logic
```

### Web capability

If you select the [web capability](core_concepts.html#web-capability) then the following
files will be included in the scaffolded project:

```
├── public/                         - Directory whose contents is served on /
```

### OpenAPI / Swagger endpoint capability

If you select the [Swagger endpoint capability](core_concepts.html#swagger-fileserving-endpoint-capability) then the following
files will be included in the scaffolded project:

```
├── Sources/
│   └── Application/
│       └── Routes/
│           └── SwaggerRoute.swift  - Swift code for OpenAPI definition endpoint
```

### Example endpoints capability

If you select the [example endpoints capability](core_concepts.html#example-endpoints-capability) then the following
files will be included in the scaffolded project:

```
├── Sources/
│   └── Application/
│       └── Routes/
│           └── ProductRoutes.swift - Swift code for example endpoints
├── definitions/
│   └── <application_name>.yaml     - Swagger definition for example API
```

### Endpoints from swagger file

If you select [endpoints from swagger file](core_concepts.html#endpoints-from-swagger-file) then the following
files will be included in the scaffolded project:

```
├── Sources/
│   └── Application/
│       └── Routes/
│           └── <route_name>Routes.swift - Swift code for generated API endpoints
├── definitions/
│   └── <application_name>.yaml          - Swagger definition for generated API
```


### Both Web capability and Example endpoints capability

If both [web capability](core_concepts.html#web_capability) and
[example endpoints capability](core_concepts.html#example-endpoints-capability) are
selected then [SwaggerUI](http://swagger.io/swagger-ui/) will be added to the project
in the following location:

```
├── public/
│   └── explorer/                   - SwaggerUI
```

### Docker capability

If you select the [docker capability](core_concepts.html#docker-capability) then the following
files will be included in the scaffolded project:

```
├── Dockerfile                      - Docker spec for an image to run the application
├── Dockerfile-tools                - Docker spec for an image to build the application
├── .dockerignore                   - Defined files to ignore for building images
├── chart/
│   └── <application_name>/
│       ├── Chart.yaml              - A Helm chart for Kubernetes
│       ├── values.yaml             - IBM Cloud values for Kubernetes
│       └── templates/
│           ├── deployment.yaml     - Kubernetes deployment configuration
│           ├── hpa.yaml            - Kubernetes scaling configuration
│           └── service.yaml        - Kubernetes service configuration
```

### Server SDK generation

If you select the [Server SDK generation](core_concepts.html#server-sdk-generation) then the following
files will be included in the scaffolded project:

```
├── Sources/
│   └── <generated_name>_API_ServerSDK/
│       └── Routes/
│           ├── <generated_name>_API_ServerSDKUtility.swift - Swift server SDK helper methods
│           ├── <generated_name>API.swift                   - Swift server SDK API code
│           └── <generated_name>.swift                      - Swift server SDK object wrapper
```

### IBM Cloud

[IBM Cloud](core_concepts#services) core files are included by default. The following files are common to all generated applications:

```
├── manifest.yml                      - CloudFoundry deployment manifest file
├── cli-config.yml                    - IBM Cloud Dev Tools CLI configuration file
├── .cfignore                         - Defines files to be ignored for deployment
├── .bluemix/                         - IBM Cloud pipeline and toolchain files
│   ├── toolchain.yml                 - IBM Cloud toolchain configuration file
│   ├── pipeline.yml                  - IBM Cloud pipeline configuration file
│   ├── deploy.json                   - IBM Cloud toolchain UI configuration file
│   └── scripts/                      - Scripts for Kubernetes
│        ├── container_build.sh       - Script to build a Kubernetes container
│        └── kube_deploy.sh           - Script to deploy to a Kubernetes container
```

### Cloud Services

If you select an [IBM Cloud service](core_concepts#services), then the following files will be included in the scaffolded project:

```
├── Sources/
│   └── Application/
│       └── Services/
│            └── <service_name>.swift - Swift connector to an IBM Cloud Service
├── config/
│   ├── localdev-config.json          - IBM Cloud service configuration file
│   └── mappings.json                 - Service configuration mappings file
```

## CRUD project

The following section applies to the [CRUD project type](core_concepts.html#crud).
CRUD projects will have the following files included:

```
├── Sources/
│   ├── Application/
│   │   └── Routes/
│   │       └── SwaggerRoute.swift  - Swift code for OpenAPI definition endpoint
│   └── Generated/                  - Generated Swift code for CRUD API logic
│       ├── AdapterFactory.swift    - Swift code to select CRUD data store adapter
│       ├── AdapterError.swift      - Swift code for the store adapter error types
│       ├── ModelError.swift        - Swift code for the model error types
│       └── CRUDResources.swift     - Swift code to organise CRUD model logic
├── definitions/
│   └── <application_name>.yaml     - Swagger definition for CRUD API
├── models/                         - Data model metadata files
```

> ![warning] Files inside the `Sources/Generated` directory should not be modified as
they are regenerated regularly and any modifications will be lost.

### Models

For each model created using the [model generator](command_line_tools.html#model-generator)
the following files will be included:

```
├── Sources/
│   └── Generated/
│       ├── <Model_name>.swift                   - Swift code for defining the model
│       ├── <Model_name>Resource.swift           - Swift code for model endpoints
│       ├── <Model_name>Adapter.swift            - Swift protocol for model storage
│       └── <Model_name><StoreType>Adapter.swift - Swift code for model storage
├── models/
│   └── <model_name>.json                        - Model metadata file
```

> ![info] Model names entered into the model generator are used in a number of places in the generated project. They are used verbatim as filenames for the `.json` model files, and as endpoint paths in the application router and API definition. In the generated Swift code, Model names are converted to Swift classnames, using a simple transform that attempts to make them comply with the [Swift specifications for Identifiers](https://developer.apple.com/library/content/documentation/Swift/Conceptual/Swift_Programming_Language/LexicalStructure.html#//apple_ref/doc/uid/TP40014097-CH30-ID410). In addition, the convention that Swift class names start with an uppercase letter is applied, unless the model name starts with an underscore character (`_`).

