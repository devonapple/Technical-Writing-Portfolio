# Team Style Guide

A collection of style guidelines and workflows for the team's documentation push.

- [Who needs this style guide](#who-needs-this-style-guide)   
- [Workflow overview](#workflow-overview)   
- [What does the documentation work look like](#what-does-the-documentation-work-look-like)   
   - [APIs and repositories](#apis-and-repositories)   
   - [Object library](#object-library)   

## Who needs this style guide

This guide is for technical writers supporting the documentation effort to bring existing API content up to standard for publication. This guide focuses on the specific workflows unique to this project, and includes outlines of the overall publication process.

This document assumes that you are a technical writer familiar with ReSTful API documentation, git, GitHub, Postman, file directory structures, Markdown, JSON, and programming capitalization schemes. Familiarity with Excel, Word, regular expressions, and mind-mapping can also mitigate some of the more repetitive tasks.

This document won't cover the basics of technical writing. The company has a resource that explains the documentation standards for the platform. The Team Style Guide does not replace the company's documentation standards.

## Workflow overview

This is an outline of the documentation workflow for this project.

**Scoping**
1. Get the assignment details.
1. Check repository for remediation opportunities and assign to engineering team.
1. Fork and clone a local copy of the API repository.
1. Identify the source Simple Hashing Algorithm (SHA) and publication date that will serve as the baseline for the documentation assignment.
1. Map out the assigned API endpoints by following the JSON files and their $ref links to common repositories.
1. Make a list of the objects and enumerator assets used by the API.
1. Identify new objects and enumerator assets that the docs team hasn't already processed.

**JSON objects**
1. Edit descriptions and related content in the JSON objects that are used in the API.
1. Edit descriptions and related content in the swagger file.
1. Test your working branch in the development environment to identify and resolve linter errors.
    1. Correct linter errors in your working branch.
    1. Make a list of linter errors from common repositories and submit tickets to the designated engineering team for remediation.
    1. Identify other fixes needed and submit tickets to the designated engineering team for remediation.
1. Submit a pull request (PR) to publish edited swagger and other JSON assets to the target repository. Edit per PR review.
1. Once the PR has been approved, translate the JSON assets to Markdown tables.

**Sample code**
1. Catalogue the existing API code samples. Assess their age and identify opportunities to update the samples.
1. Request updates to existing samples that exceed our freshness threshold.
1. Request new samples as needed to match new and updated use cases.
1. Edit the titles and descriptions to match sample code standards.
1. Submit a PR to publish edited code samples. Edit per PR review.
1. Preview the approved samples in the production environment.
1. Use the Inspect tool in your browser to view and copy the HTML code for each sample request and response.
1. Save the HTML copies to include in the user guide.

**User guide**
1. Add Markdown tables to the object library.
1. Add infrastructure for each endpoint using the [Markdown Endpoint Template](#markdown-endpoint-template).
1. Incorporate Markdown tables into the user guide.
1. Add request and response tables for each endpoint.
1. Integrate the HTML copies of the code samples for each endpoint into the user guide.
1. Create diagrams and add supporting content as needed for each endpoint.
1. Add the source SHA and publication date to the introduction of each endpoint.
1. Complete the draft user guide.
1. Submit the draft user guide for review. Edit per review.
1. Submit a PR to publish the user guide to the target repository. Edit per PR review.
1. Identify changes to parameter tables and update JSON files and Markdown tables as needed.

## What does the documentation work look like

You need to interact with several different systems to support the documentation push. 

### APIs and repositories

Developers create application program interfaces (APIs) that support operations. The technical writing team uses the company's development environment to locate and update the needed documentation.

The API documentation is organized as follows:

*Table redacted*

### Object library

A critical element of the documentation is producing a user guide that contains a complete inventory of all of the parameters used by that API. The team reframes existing parameter information into a more easily consumable and searchable developer resource. To make that work easier and ensure consistency, we transcribe the parameter tables for the JSON objects and enumerators into a Markdown file that we can easily paste into the user guide. Each object needs a unique filename. The filename matches the original JSON file unless that name is already taken by another resource. When a JSON file has one or more nested elements, we need to break these down into their own parameter tables and link them together in the user guide.

*Additional content redacted*

<a name="markdown-endpoint-template"></a>
