# Splunk

- [Splunk](#splunk)
  - [Notes from Training](#notes-from-training)
    - [Functions of Splunk](#functions-of-splunk)
      - [Indexer](#indexer)
    - [Web UI](#web-ui)
      - [Apps](#apps)
      - [Enterprise Web UI](#enterprise-web-ui)
        - [Search tab](#search-tab)
        - [Search Modes](#search-modes)
    - [Knowledge Objects](#knowledge-objects)

## Notes from Training

### Functions of Splunk

- Index Data
- Search and Investigate
- Add Knowledge
- Monitor and Alert
- Report and Analyze

#### Indexer

Receives info from exterior, normalizes formats based on source type, extracts the timestamps and organizes into a searchable index

### Web UI

#### Apps

Apps are workspaces. 2 defaults, Home and Search & Report.
Admin role can install new Apps, Power user can create knowledge objects and share them.

SplunkBase - repo of many example Apps.

#### Enterprise Web UI

- Splunk bar - user settings, activity etc.
- App bar - search,dashboards etc.

##### Search tab

- Can search using an index and time limit + query options
  - Search history also listing previous searches
  - **Best Practice for Search - LIMIT time, use OR or IN to avoid wildcards**
  - search will automatically look for patterns - see under tab
  - events tab has raw events
  - Visualization + Statistics if your search generates them
  - Can share a search by link
  - Search job remains active for 10mins by default
  - Shared search job remains active for 7 days by default
- Data Summary (when available) - breakdown of 
  - Host - e.g. microservice
  - Source - e.g. file or log
  - SourceType - e.g. access_combined, cisco_firewall
- Table view 
  - Allows creating views of the data without using SPL (Splunk - search processing language)

##### Search Modes

- Fast - no field discovery
- Verbose - every possible field
- Smart - some field discovery 

TODO - need to understand some more with examples

- Search results have a timeline also - can zoom to particular parts
- Can highlight text in results and add to search + reruns automatically
- Search terms NOT case sensitive
- can negate by NOT - e.g. fail NOT password -> all fail events apart from fail password
- escape characters with backslash

- Splunk Search Language - 5 parts
  - Search Terms - basis of getting the information
  - Commands - tell what we want to do with the results
    - Creating charts, compute stats, formatting
  - Functions - explain how to chart, compute and evaluate results
  - Arguments - variables to apply to the function
  - Clauses - how to group results

- Best Practices
  - TIME IS CRITICAL 
  - use OR or IN to avoid wildcards
  - Filter as early as possible
  - Default indexed fields - index, source, host, hosttype - use these to get the fastest results
  - Give as much info as possible to the query
  - Inclusion better than exclusion - e.g access denied better than NOT access granted

### Knowledge Objects

