Information Stored 
*******************

The MetaRelate project contains an informaiton repository, called MetOcean.  This may be joined by other repositories in the future.

These repositories store semi-structured information as `RDF`_.

.. _RDF: http://www.w3.org/RDF/


The structure of the RDF enables queries to be run on the contained data, usiong `SPARQL1.1`_.

.. _SPARQL1.1: http://www.w3.org/TR/sparql11-query/


The information structure is extensible, the structure is not fixed, but this description representsa minimum set which is required for the current set of queries used in the mapping manager.

.. _information_structure:

Information structure  
======================

.. graphviz:: shards.dot


Editing is Adding
=================

All editing of the informaiton in the repository is additive.  Any edits made in a branch which delete content will not be merged into the main repository. 

.. _allowed-states:

State
=====

A number of States are allowed for Mapping shard instances.  One of the allowable edit operations is to replace a mapping shard with an up-versioned shard with a different state.  This is a state transtition operation.

.. graphviz:: state.dot
