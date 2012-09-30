Query Relationships
*******************

This is description of the logical relationship between the data model
and the SPARQL queries used in the Mapping-Manager application.

Data Model
==========

The current data model is about to change so this description will be covering the existing
layout as well as the forthcoming.

There are five permissible states that data is categorised as, within the application:
 * Draft
 * Proposed
 * Approved
 * Deprecated
 * Broken

along with a series of permissible transitions between states, 
shown in the diagram at :ref:`allowed-states`.

Current Data Layout
===================

There are various kinds of data loaded:

(1) user end-point data

    All data representing user endpoints (STASH, Grib, Nimrod etc) is, 
    at initialisation of the triple-store, loaded into a TDB 'NAMED GRAPH'
    titled as a catenation of the state it represents and its filename e.g.

    ``http://draft/stash.version.vn4.7.ttl``

    and when a state is changed, data shard is moved from its existing named graph to
    a new named graph representing its new state.
    
(2) linkage data

    This is the mapping between the user data (STASH, Grib etc) and CF Standard Name data.
    
(3) CF Standard Name data
    
    This is a local copy of the CF Standard Name data, drawn from the original XML file 
    and converted into Turtle.


Proposed Data Layout
====================

The new data layout is going to do away with named graphs altogether and store all
of the data in the root 'default' graph, which is unnamed and available to all queries.

This will mean that the existing queries and view workflow will also change, in that
the named graphs will no longer identify the 'status' and 'type' of the Shard, rather
this information will be held in the Mapping shard linking to it (see :ref:`information_structure`).

In addition, the current use of a local copy of the CF Standard Name XML file
will be replaced with one of the following:

* live HTTP queries to the Vocab NERC site at BODC

* downloading of the CF Standard Name data to a local cache upon initialisation.

Current and Future Workflow
===========================

This workflow is likely to change dependent upon changes in the data layout within the triple store.

tasks
_____

The current top-level view, this displays the number of shards existing within each 
group of named graphs within the triple store that fall into one of the accepted 5 'states'.

Using the aggregators 'COUNT' and 'GROUP BY', 
efficient totals are calculated for all
graphs residing within a given 'state'.

The proposed workflow is described in Issue (I), View Flow under Mapping-manager,
with a new top level page providing three options:

1) the existing Status -> Format view as described here in 'tasks'.
2) a view directly accessing the Release data.
3) a view directly accessing the Format data.

list
_____

The second-level view is designed to query all graphs within a given 'state' and display counts
of each graph, by performing a GROUP BY and COUNT with a FILTER on the graph URL
to match the given 'status'

When the data model layout changes, the query will need to check the Mapping 'hasStatus'
attribute to determine each Linkage shards status. Again GROUP BY and COUNT will provide
efficient counts of each type.

listtype
________

This the current third-level view giving a detailed listing of every Mapping/Linkage shard within
named graph.

When the data model layout changes, the query will need to find each explicit Mapping shard,
using Provenance chain lookup sub-query, and thence find each Linkage shard.

edit
____

The is the current lowest level view, which lists out a view of both Mapping and of Linkage shard
combined, as a Django ModelForm.

The query operates by stepping backwards from the explicit Linkage shard name and acquiring all siblings attributes,
then stepping backwards again to find its parent Mapping shard and acquiring all
of its attributes as well. The OPTIONAL clause is to attempt to acquire the 'canonical unit'
if it exists.

When the data model layout changes, the query will need to find the explicit Mapping shard,
using Provenance chain lookup sub-query, and acquire all required attributes for
populating the ModelForm.

new
___

This query merely pre-populates a Django ModelForm with useful defaults
and generates data from the submitted form for feeding into the triple-store
via INSERT clauses. 

mapdisplay
__________

A basic view that returns direct RDF/XML or Turtle of a given Mapping shard from
its unique URL ID identifier. It relies on CONSTRUCT using an explicit Subject URI
to access and render the data, its return format being governed by the 'output' type 
flag passed into the Fuseki query: 'txt' returns Turtle, 'xml' returns RDF/XML.
into

