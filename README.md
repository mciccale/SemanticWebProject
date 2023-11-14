# Semantic Web Project

## Table of contents:

- [Project Overview](#project-overview)
- [Project Workflow](#project-workflow)
- [Application Setup](#applicacion-setup)
- [Contributors](#contributors)
- [License](#license)

## Project Overview

This project englobes all the necessary steps to transform a simple CSV file into Linked Data in order to take leverage of all the Linked Data that is available on the web. We started with a simple CSV about energy consumption of public buildings in Madrid and transformed it into a RDF graph that is consumed by a simple application that showcases the power of Linked Data.

## Project Workflow

### Data Selection

#### Data Source

As mentioned before, a dataset containing information on the energy consumption of each public building in Madrid was selected. The source dataset can be found at this [website](https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=d6fe4f894ef31710VgnVCM1000001d4a900aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default) under a [public license](https://datos.madrid.es/portal/site/egob/menuitem.3efdb29b813ad8241e830cc2a8a409a0/?vgnextoid=108804d4aab90410VgnVCM100000171f5a0aRCRD&vgnextchannel=b4c412b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default).

### Data Cleaning with OpenRefine

#### Data Analysis

The data were analyzed to identify the format of the data and the types of each column.

#### Data Cleaning

OpenRefine was used for data cleaning, identifying and correcting inconsistencies, missing or erroneous data.

### Data Reconciliation

#### Wikidata Reconciliation

Before defining the mapping process, a reconciliation step with Wikidata entities was performed. This step enhanced the value of the linked data by aligning our dataset with standardized Wikidata entities and having direct access from our RDF graph to the vast Linked Data available from WikiData.

### Ontology Generation

#### Ontology Development

A lightweight ontology specific to the data domain was created, defining relationships and characteristics of the dataset elements (such as buildings, districts, neighbourhoods, measures and sensors).

### Mapping with YARRRML

#### Data Transformation

YARRRML (Yet Another RDF Rules Mapping Language) was used to define the mapping rules for our dataset. We used Matey, a tool that allows transforming YARRRML files into rml.io files. The rml.io file was then used to generate the RDF graph using morph, a powerful tool to transform regular data into Linked Data using a mapping definition.

### Knowledge Graph Publication

#### Endpoint Setup

The knowledge graph was published on an endpoint using Helio Publisher. This allowed us to make queries to retrieve the data from our graph and then use it in our application.

#### SPARQL Queries

Enabled the ability to perform SPARQL queries on the knowledge graph, allowing for information extraction from our RDF graph but also the Wikidata graph.

### RDF Graph Validation

#### SHACL Validation

To ensure the consistency of our Knowledge Graph (KG), we thought about validating it using a set of SHACL rules. To keep it simple, we used a tool named Astrea that auto-generates some basic SHACL rules from our ontology. We then validated our KG before the last step.

### Application Development

#### Interactive Application

After all these steps, we developed a simple React.js application to test the quality and power of our KG.

The application lists all the neighbourhoods and districts of Madrid in the main page. The user can select any of these locations and access some statistics about the consumption of energy of all the buildings in that location; the population of that location, an interactive map of the location and a simple image that shows where it is located inside Madrid.

All the data that is obtained from our KG and from the links with Wikidata that we defined in the [reconciliation](#data-reconciliation) section.

## Application Setup

In order to make the app work, here are some guidelines:

1. Install dependencies of the app:

```bash
cd app
npm install
```

2. Publish the RDF file:
   You will need to publish the `rdf/result-with-links.ttl` in your host machine under the `http://localhost:9000/api/sparql` endpoint so the app can acces the data. You can use [Helio Publisher](https://github.com/oeg-upm/helio-publisher) to do so.

3. Start the app:

```bash
cd app
npm run dev
```

_Note: Due to browsers CORS policy, the access to the data will be blocked (endpoint and app have the same hostname). In order to test it, it is not possible to configure CORS in Helio, so you would need to disable CORS in the browser tab where you accesed the app. (ONLY FOR TESTING)_

## Contributors

- [Ramiro Lopez Cento](https://github.com/ramirolc02)
- [Guillermo Izquierdo Cabo](https://github.com/GuilleIzk)
- [Marco Ciccalè Baztán](https://github.com/mciccale)

We'd also like to thanks the [OEG](https://oeg.fi.upm.es) for teaching and guiding us on this project.

## License

This work is licensed under Attribution 4.0 International
