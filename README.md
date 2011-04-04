
Spoc API Specification
======================

add(s, p, o, c)
---------------
Adds one or more triples to the graph. The interpretation of each argument is as follows:

* s: if a string value then this is interpreted as the subject of a triple. 
    If s starts with _: then it is treated as a blank node. Otherwise it is parsed as a Qname or a URI.
    If an array then this is interpreted as an array of (s, p, o, c). Remaining arguments are ignored
  
* p: if a string value then this is interpreted as the property of a triple. It is parsed as a Qname or a URI.
    if an array then it is interpreted as an array of (p, o, c) all with the same subject s
  
* o:  if a string value then this is interprered as the object of a triple.
    if the value parses as a qname or URI then it is treated as a resource unless x has a value of rdfs:Literal
    otherwise it is treated as a literal.
    if an array then it is interpreted as an array of (o,c), i.e. triples with subject s, predicate p
  
* c:  must either be omitted, have a null value or be a string value. if the value matches the regex [a-zA-Z]+(-[a-zA-Z0-9])* then it is interpreted as a language code and
    the value of o is a plain literal with this language code
    Otherwise the value is parsed as a Qname or a URI and the value of o is a typed literal with this datatype

remove(s, p, o, c)
------------------
