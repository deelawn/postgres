# Group by all



# ALLBUT
### Description
* allow users to specify ALLBUT, followed by a list of columns when selecting from a table
* this will select all columns from the table except those specified
* iterations
    * first, only column names will be supported
    * next, keywords first and last will be added
        * first and last are followed by integers, so all but the first x or last x columns are selected
    * next, add support for <table_name>.ALLBUT for selecting from a table in a join query
    * finally, create syntax that allows for multiple ALLBUT selections

### Changes Needed
* src/include/parser/kwlist.h
    * add allbut keyword
    * needs to be in alphabetical order
* src/backend/parser/gram.y
    * add symbol for allbut that defines it as a node: %type <node>
    * add allbut in alphabetical order to the %token <keyword> section
    * define allbut syntax
* src/include/nodes/nodes.h
    * add node for allbut under the parsetreenodes section
* src/include/nodes/parsenodes.h
    * define struct for allbut node

### Notes
* parsing SELECT * should ultimately end up in src/backend/parser/parse_relation.c:expandTupleDesc
    * set breakpoint here to debug and see how the names are resolved and structs are built
