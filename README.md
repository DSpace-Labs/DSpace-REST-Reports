# DSpace-REST-Reports
Add-on Reporting Tools for Collection Managers built on the REST API

# DSpace-Rest-Reports
This is a sample javaScript application that uses the DSpace REST API to perform quality control reporting.

[Report Screenshots](https://github.com/DSpace-Labs/DSpace-REST-Reports/wiki)

## Pre-requisites
* Determine the access that you will grant to your REST api since these reporting tools can be configured to run without authentication.
* These tools can use *sorttable.js* which can be found at http://www.kryogenix.org/code/browser/sorttable/
* If you enable sorttable, uncomment sorttable.makeSortable(...) in the js files 
* Install this code into dspace/modules/xmlui/src/main/webapp/static/rest
* Update the dspace/config/modules/rest.cfg 

### rest.cfg: Enable the reporting tools to report on all items (regardless of authorization)
_Do not enable this feature if your REST API has not been secured_

```
# require authentication for filtered-items and filtered-collections (de
rest-reporting-authenticate = false
```

### rest.cfg: Configure the reporting tools of interest to run out of /static/rest

```
# return report tool html by name
rest-report-url.collections = ../static/rest/index.html
rest-report-url.item-query = ../static/rest/query.html
```

## Optional Configuration

#### Configure the list of filters that are useful to your repository managers.
```
# configurable filters for filter-collections and filtered-items
plugin.sequence.org.dspace.rest.filter.ItemFilterList = \
        org.dspace.rest.filter.ItemFilterDefs,\
        org.dspace.rest.filter.ItemFilterDefsMisc,\
        org.dspace.rest.filter.ItemFilterDefsPerm
```
#### Configure properties and regular expression filters
```
# comma separated list of supported bundles
rest-report-supp-bundles = ORIGINAL,THUMBNAIL,TEXT,LICENSE

# comma separated list of mime types for "document" type bitstreams
rest-report-mime-document = text/plain,application/pdf,text/html,application/msword,text/xml,application/vnd.openxmlformats-officedocument.wordprocessingml.document,application/vnd.ms-powerpoint,application/vnd.openxmlformats-officedocument.presentationml.presentation,application/vnd.ms-excel,application/vnd.openxmlformats-officedocument.spreadsheetml.sheet

# comma separated list of supported document types
rest-report-mime-document-supported = application/pdf

# comma separated list of supported document types
rest-report-mime-document-image = image/jpeg,image/jp2

# Minimum size for a supported PDF in the repository
rest-report-pdf-min-size = 20000

# Maximum size for a typical PDF in the repository
rest-report-pdf-max-size = 25000000

# Minimum size for a thumbnail - could indicate a corrupted original
rest-report-thumbnail-min-size = 400

# bitstream descriptor to identify generated thumbnails
rest-report-gen-thumbnail-desc = LIT Thumbnail,Generated Thumbnail

# Used by org.dspace.rest.filter.ItemFilterDefsMeta
# -----------------------------------

# regex to detect compound subjects
rest-report-regex-compound-subject = .*;.*

# regex to detect compound authors
rest-report-regex-compound-author = .* and .*

# regex to detect unbreaking metadata
rest-report-regex-unbreaking = ^.*[^ ]{50,50}.*$

# regex to detect url in description
rest-report-regex-url = ^.*(http://|https://|mailto:).*$

# regex to identify full text content from the provenance field
rest-report-regex-fulltext = ^.*No\\. of bitstreams(.|\\r|\\n|\\r\\n)*\\.(PDF|pdf|DOC|doc|PPT|ppt|DOCX|docx|PPTX|pptx).*$

# regex to identify very long metadata field
rest-report-regex-long = ^[\\s\\S]{6000,}$

# regex to identify XML entities 
rest-report-regex-xml-entity = ^.*&#.*$

# regex to identify non ascii characters 
rest-report-regex-non-ascii = ^.*[^\\p{ASCII}].*$

```

