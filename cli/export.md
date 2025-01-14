---
layout: default
title: export
parent: Structurizr CLI
nav_order: 5
permalink: /cli/export
---

# export

The ```export``` command allows you to export the views within a Structurizr workspace to a number of different formats.
Files will be created one per view that has been exported.
If output directory is not specified, files will be created in the same directory as the workspace.
Please note that the export formats do not support all of the available shapes/features when compared to
the [Structurizr cloud service/on-premises installation/Lite](https://structurizr.com).

Exporting PNG/SVG diagrams from the Structurizr cloud service/on-premises installation/Lite is not supported from the CLI.
This is because the CLI is a Java application, whereas the PNG/SVG diagrams are rendered in your web browser.
PNG/SVG diagram exports can instead be automated using headless Chrome and Puppeteer -
please see [https://github.com/structurizr/puppeteer](https://github.com/structurizr/puppeteer) for some example scripts.

## Options

- -workspace: The path or URL to the workspace JSON/DSL file (required)
- -format (required):
  - plantuml: the same as `plantuml/structurizr`
  - plantuml/structurizr: exports views to PlantUML using the [StructurizrPlantUMLExporter](https://github.com/structurizr/export/tree/main/src/main/java/com/structurizr/export/plantuml#structurizrplantumlexporter)
  - plantuml/c4plantuml: exports views to PlantUML using the [C4PlantUMLExporter](https://github.com/structurizr/export/tree/main/src/main/java/com/structurizr/export/plantuml#c4plantumlexporter)
  - mermaid: exports views to Mermaid using the [MermaidExporter](https://github.com/structurizr/export/tree/main/src/main/java/com/structurizr/export/mermaid) (your Mermaid configuration will need to include `"securityLevel": "loose"` to render the diagrams correctly. See [Mermaid - Configuration - securityLevel](https://mermaid-js.github.io/mermaid/#/./Setup?id=securitylevel) for more details)
  - websequencediagrams: exports dynamic views to WebSequenceDiagrams using the [WebSequenceDiagramsExporter](https://github.com/structurizr/export/tree/main/src/main/java/com/structurizr/export/websequencediagrams)
  - dot: exports views to DOT format (for use with Graphviz) using the [DOTExporter](https://github.com/structurizr/export/tree/main/src/main/java/com/structurizr/export/dot)
  - ilograph: exports the workspace to a YAML format for use with Ilograph using the [IlographExporter](https://github.com/structurizr/export/tree/main/src/main/java/com/structurizr/export/ilograph)
  - d2: export views to D2 format using the [D2Exporter](https://github.com/goto1134/structurizr-d2-exporter)
  - json: exports the workspace to the Structurizr JSON format
  - theme: creates a JSON theme based upon the styles and tags defined in the workspace
  - fully qualified class name: provides a way to use a custom exporter; this needs to implement [WorkspaceExporter](https://github.com/structurizr/export/blob/main/src/main/java/com/structurizr/export/WorkspaceExporter.java) or [DiagramExporter](https://github.com/structurizr/export/blob/main/src/main/java/com/structurizr/export/DiagramExporter.java), with the compiled class(es) being available on the CLI classpath or packaged as a JAR file in a directory named `plugins` next to your workspace file
- -output: Relative or absolute path to an output directory (optional)

## Examples

To export all views in a JSON workspace to PlantUML format under folder named `diagrams`:

```
./structurizr.sh export -workspace workspace.json -format plantuml -output diagrams
```

To export all views in a JSON workspace to PlantUML format, using C4-PlantUML, under folder named `diagrams`:

```
./structurizr.sh export -workspace workspace.json -format plantuml/c4plantuml -output diagrams
```

To export all views in a JSON workspace to Mermaid format:

```
./structurizr.sh export -workspace workspace.json -format mermaid
```

To export all dynamic views in a DSL workspace to WebSequenceDiagrams format:

```
./structurizr.sh export -workspace workspace.dsl -format websequencediagrams
```

To export a DSL workspace to the JSON workspace format:

```
./structurizr.sh export -workspace workspace.dsl -format json
```

To export all views in a DSL workspace using a custom exporter:

```
./structurizr.sh export -workspace workspace.dsl -format com.example.MyCustomDiagramExporter
```
