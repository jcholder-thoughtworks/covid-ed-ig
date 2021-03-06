# Emergency Department COVID-19 Severity Classification

This repository houses the source for building a CPG-on-FHIR content implementation guide for an Emergency Department COVID-19 Severity Classification. This logic represents an initial Minimum Viable Product (MVP) that implements a subset of the logic defined by the American College of Emergency Physicians (ACEP).  Refer to the [ACEP Guideline](https://www.acep.org/globalassets/sites/acep/media/covid-19-main/acep_evidencecare_covid19severitytool.pdf).

This MVP implementation is intended to align with, and eventually be replaced by, an equivalent logic library with substantially expanded functionality that is generated from OMG Business Process Modeling (BPM+) decision and case models, using an automated toolchain. Refer to the [Open Clinical Practice Guidelines](https://github.com/OpenCPG) GitHub project.

The contents of this repository are licensed under an Apache 2.0 License with an additional healthcare related disclaimer and limitation of warranty. See the [LICENSE](LICENSE) page for details.

## Content IG Walkthrough: Setup and Build

This repository provides a walkthrough of building a FHIR content implementation guide (content IG). A content IG is a FHIR implementation guide that primarily contains knowledge artifacts such as decision support rules and quality measures. By using the FHIR publication toolchain, these artifacts are made available as FHIR resources, published within websites for documentation and dissemination, and distributed as part of NPM packages for implementation.

This walkthrough consists of 5 main steps:

1. [**Setup**](#basic-setup): Setting up the IG and getting a basic build
2. [**Library**](#adding-a-library): Including a simple Library for a specific recommendation
3. [**PlanDefinition**](#adding-a-plandefinition): Adding a PlanDefinition to surface the recommendation as a decision support rule
4. [**Test Cases**](#adding-test-cases): Adding test cases to test the rule
5. [**Validation**](#validation-with-cqf-ruler-and-cds-hooks): Validating the content works as expected via the CDS Hooks Sandbox


## Basic Setup

The first step is to get a local [clone](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/cloning-a-repository) of the walkthrough repository.

Once you have a local clone, you'll need to build:

### Dependencies

Before you're able to build this IG you'll need to install several dependencies

#### Java / IG Publisher

Go to [https://adoptopenjdk.net/](https://adoptopenjdk.net/) and download the latest (version 8 or higher) JDK for your platform, and install it.

There are scripts in this repository that will download and run the latest HL7 IG Publisher.

Please make sure that the Java bin directory is added to your path.

This project includes scripts that will automatically download the correct version of the IG-Publisher.

Documentation for the IG-Publisher is available at [https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation](https://confluence.hl7.org/display/FHIR/IG+Publisher+Documentation).

#### Ruby / Jekyll

Jekyll requires Ruby version 2.1 or greater. Depending on your operating system, you may already have Ruby bundled with it. Otherwise, or if you need a newer version, go to [https://www.ruby-lang.org/en/downloads/](https://www.ruby-lang.org/en/downloads/) for directions.

Jekyll

Go to [https://jekyllrb.com](https://jekyllrb.com) and follow the instructions there, for example gem install jekyll bundler. The end result of this should be that the binary "jekyll" is now in your path.

### Build

Once you have the dependencies installed, you can build the IG by first updating the publisher:

```
_updatePublisher
```

Once the publisher has been downloaded to your local environment, you can build the IG:

```
_genonce
```

Whenever you make changes to the source content, just rerun the `_genonce` script to rebuild the IG. The IG output will be in the output folder. Using a browser, open the `index.html` page to see the IG.

NOTE: This walkthrough uses "contentig" as the name of the implementation guide. The source ImplementationGuide resource is in the [contentig.xml](input/contentig.xml) file, and the [ig.ini](ig.ini) file refers to it. To change the name of the ig, be sure to update all references to `contentig` within the ImplementationGuide resource. Note that this name serves as part of the basis for the canonical URL for your IG, which is used to uniquely identify the implementation guide and all the resources published within it, so it's important to choose your canonical URL appropriately. For more information see the [Canonical URLs](https://www.hl7.org/fhir/references.html#canonical) discussion topic in the FHIR specification.

## Adding a Library

The next step in this walkthrough is to build the recommendation logic as expressions of [Clinical Quality Language](http://cql.hl7.org) (CQL). CQL is a high-level, author-friendly language that is used to express clinical reasoning artifacts such as decision support rules, quality measurement population criteria, and public health reporting criteria.

### Atom CQL Support

To validate and test CQL, use the [Atom CQL Plugin](https://github.com/cqframework/atom_cql_support). Follow the instructions there to install the plugin, then open Atom on the root folder of this  content IG walkthrough.
