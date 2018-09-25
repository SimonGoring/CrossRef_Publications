# CrossRef_Publications

The objective of this project is to generate a list of papers within Neotoma that are not currently assigned DOIs, or have had DOIs assigned programmatically.  This project is intended to provide an interface that will support the collection of publication information using the CrossRef API, possibly extending current information recorded within Neotoma and also to provide human support to check existing Neotoma records, to validate reported DOIs, validate information about papers (abstracts, titles, authors) and to assign this information back into the Database.

## Contributions

This project is a part of the Neotoma Paleoecology Database, and work is supported in part through grants from the National Science Foundation.  This work is also associated with the project [api_nodetest](http://github.com/neotomadb/api_nodetest), part of the development of a more flexible API for the Neotoma Paleoecology Database.

### Contributors

Contributions to this project are guided by the [Code of Conduct](code_of_conduct.md).  All contributors are expected to follow the guidelines and expectations for this community.

* [Simon Goring](http://goring.org)

## Project Components

The project has three key elements:

* Validating existing DOIs
* Searching for missing DOIs
* Validating 'discovered' DOIs

### Validating Existing DOIs

For all Neotoma publications with reported DOI fields, call the CrossRef API and obtain full bibliographic information.  For each record compare Neotoma fields with the reported CrossRef fields.

CrossRef returns:  
```
publisher, issue, published-print, DOI, type, title, page, volume, author, container-title, URL, ISSN, subject
```

Neotoma uses:
```
```

For each record with a DOI we will issue a call to CrossRef, ingest the data return, compare results and score the difference between the DOI call and the Neotoma reference.  The output, along with the CrossRef record will be stored in a JSON file in `data/output` with a filename `crossrefout-yyyy-mm-dd.json`.  This file can then be used, either to help manage future changes to the records, or for other applications.

### Searching for DOIs

For Neotoma publications without DOIs we will search CrossRef, returning parsed title strings and near matches.  For each of these we will store only the DOI of close matches (according to CrossRef).  This will result in a document to be saved in `data/output` with the file format `missing-yyyy-mm-dd.json`.

### Validating DOIs

With the missing DOIs, we will build a small app that can `INSERT` into the Neotoma-dev database, in a Publications-dev table.

## TODO

**If you'd like to contribute, there are several tasks that would be useful:**

1. Much of the workflow is currently included in the [Importing_pubs.Rmd]() file, but this file is somewhat unweildy for day-to-day execution.  Rewriting the core Validation engine would be helpful, in either R or Python.  Ingesting from the Neotoma API and exporting to a JSON file.
2. File re-organization needs to happen.  There are a number of supporting files (csv and RData files) that are here for legacy reasons.  Having these files moved or removed would be helpful.
3. Paper writing and editing.  We invite the contribution of multiple authors and can support the development of a paper for publication (a data paper likely).  If you wish to contribute to coding, writing and revisions we welcome your contribution.  Please contact us directly if you would like to be listed as an author on a paper coming from this work.