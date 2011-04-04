
Spoc API Specification
======================
Noodling around an extremely simple, non-object based API for RDF that could be implemented in many different languages




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

### Examples

To add:
    <rdf:Description rdf:about="http://example.com/foo">
       <rdfs:label>Summat</rdfs:label>
    </rdf:Desciption>
Use:  
    add("http://example.com/foo", "rdfs:label", "Summat")

To add:
    <rdf:Description rdf:about="http://example.com/foo">
       <rdfs:seeAlso rdf:resource="http://example.com/other" />
    </rdf:Desciption>
Use:  
    add("http://example.com/foo", "rdfs:seeAlso", "http://example.com/other")



To add:
    <rdf:Description rdf:about="http://example.com/foo">
       <rdfs:comment>http://example.com/other</rdfs:comment>
    </rdf:Desciption>
Use:  
    add("http://example.com/foo", "rdfs:label", "http://example.com/other", "rdfs:Literal")



remove(s, p, o, c)
------------------

find(s, p, o, c, u)
-------------------


* u: boolean, indicates whether results returned should be unique (true) or not (false). Default is false, i.e. non-unique matches


Default Namespace Bindings
--------------------------
The following namespace bindings are always available for use as qnames:

<table>
<tr><th>prefix</th><th>Namespace URI</th></tr>
<tr><td>rdf</td><td>http://www.w3.org/1999/02/22-rdf-syntax-ns#</td></tr>
<tr><td>rdfs</td><td>http://www.w3.org/2000/01/rdf-schema#</td></tr>
<tr><td>owl</td><td>http://www.w3.org/2002/07/owl#</td></tr>
<tr><td>dc</td><td>http://purl.org/dc/terms/</td></tr>
<tr><td>foaf</td><td>http://xmlns.com/foaf/0.1/</td></tr>
<tr><td>geo</td><td>http://www.w3.org/2003/01/geo/wgs84_pos#</td></tr>
<tr><td>skos</td><td>http://www.w3.org/2004/02/skos/core#</td></tr>
<tr><td>ov</td><td>http://open.vocab.org/terms/</td></tr>
</table>
