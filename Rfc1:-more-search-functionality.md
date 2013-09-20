# Overview
The current search functionality enables the user to search through an ArcGIS generated geocoder and an OpenLS geocoder. To enlarge the possibilities for searching, I submit the following changes.
# Functional changes
There changes will consist of several new functionalities.
## More ways of searching
There will be more searchentries:  
1. A manual list  
2. Based on a featuresource (it can be configured on which attributes the query must be done)

## Active layers
At each search entry the admin can determine which layers **must** be active (if it's not active, it will be activated). This goes two ways: a dataset can only be searched when the layers is switched on.
## Layout of results
Via a textfield the result of the searchaction can be determined.

## Unified searching
The goal for this functionality is to provide the admin a way to configure a searchfunctionality with only one input, but on the backend it searches through multiple datasets. Combined with this is the possibility to provide auto-suggest when the users types it's search query.
## Indexing
In the viewer-admin it will be possible to manage datasets through which can be searched. Of each source (ie. WFS service, JDBC source, etc.) the admin must configure what the fields are which must be queried, and which fields are the result fields. The viewer-admin will create a index based on the configuration of the admin. This index can be updated manually or it can be configured to update automatically on a regular interval.

# Technical changes
The changes needed for the completion of this functionality are described here.
## Affected modules
The modules which are affected by these changes are split in the viewer and viewer-admin
### Viewer
* In the viewer, the search component must be changed to honour the new layout configured at the viewer-admin.
* For the new possibilities, the search component must be able to execute the new ways of searching. 
* For auto-suggest the input box must be able to handle suggestions  

### Viewer-admin  

Building an index and the possibility to use auto-suggest requires the use of a third-party component: Solr. This is a indexing and searching application. It will be configured and managed via the viewer-admin.
* In the viewer-admin there will be menu item for managing the datasets for searching:  
       Adding and removing datasets  
       Manual updating of the index  
       Automatic updating of the index  
* In the layoutmanager it must be possible to configure the searchcomponent with all the new options  

## Backwards compatibility
We foresee no incompatibility with older version. All the old configurations will be kept and remain functional.  
# Voting history