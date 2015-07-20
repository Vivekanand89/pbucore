# Handling 'instantiationStandard'

Proposal to add 'hasStandard' as an EBUCore property

```xml
<pbcoreDescriptionDocument>
  <instantiationStandard source="PBCore instantiationStandard/video" ref="http://metadataregistry.org/concept/show/id/3248.html">NTSC</instantiationStandard>
</pbcoreDescriptionDocument>
```


```xml
<rdf:Description about="http://example.com#12345">
  <rdf:type rdf:resource="ebucore:MediaResource" />
  <ebucore:hasStandard rdf:resource="http://metadataregistry.org/concept/show/id/3248.html" />
</rdf:Description>
```