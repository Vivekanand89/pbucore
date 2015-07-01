# Handling 'pbcoreRelation'

EBUCore: hasRelatedResource, hasRelatedBusinessObject, hasRelatedEvent, isRelatedTo, hasRelatedMediaFragment

DublinCore object properties: hasFormat, isFormatOf, isPartOf, isReferencedBy, isReplacedBy, isRequiredBy, isVersionOf, hasVersion, requires, replaces, references, hasPart

properties to add to EBUCore: clonedTo/isClonedFrom, dubbedTo/isDubbedFrom, derivedTo/IsDerivedFrom 

**NOTE: in our previous analysis, we thought followsInSequence was a dc property, but now that I'm looking for it I can't find it?  Does this also need to be added?**

So, a couple different examples!

**To relate an Asset and an Instantiation**

```xml
<pbcoreDescriptionDocument>
  <pbcoreIdentifier source="MCU">MCU_a0567</pbcoreIdentifier>
  <pbcoreTitle>Death Is A Poor Man's Doctor</pbcoreTitle>
  <pbcoreDescription>Interviews from Detroit musicians</pbcoreDescription>
  <pbcoreInstantiation>
    <instantiationIdentifier source="McHale University">MCU_v0123_01</instantiationIdentifier>
    <instantiationLocation>McHale University</instantiationLocation>
  </pbcoreInstantiation>
</pbcoreDescriptionDocument>

```

```xml
<rdf:Description about="MCU_a0567">
  <rdf:type rdf:resource="ebucore:EditorialObject" />
  <ebucore:title>Death Is A Poor Man's Doctor</ebucore:title>
  <ebucore:description>Interviews from Detroit musicians</a>
  <dc:hasFormat>MCU_v0123_01</dc:hasFormat>
</rdf:Description>

<rdf:Description about="MCU_v0123_01">
  <rdf:type rdf:resource="ebucore:MediaResource" />
  <dc:isFormatOf>MCU_a0567</dc:hasFormat>
  <ebucore:locator>McHale University</ebucore:locator>
</rdf:Description>
```

**To relate two instantiations where one is dubbed from another**

```xml
<pbcoreDescriptionDocument>
  <pbcoreIdentifier source="MCU">MCU_a0567</pbcoreIdentifier>
  <pbcoreTitle>Death Is A Poor Man's Doctor</pbcoreTitle>
  <pbcoreDescription>Interviews from Detroit musicians</pbcoreDescription>
  <pbcoreInstantiation>
    <instantiationIdentifier source="McHale University">MCU_v0123_01</instantiationIdentifier>
    <instantiationLocation>McHale University</instantiationLocation>
    <instantiationRelation>
      <instantiationRelationType>Dubbed to</instantiationRelationType>
      <instantiationRelationIdentifier>MCU_v0123_02<instantiationRelationIdentifier>
    </instantiationRelation>
  </pbcoreInstantiation>
  <pbcoreInstantiation>
    <instantiationIdentifier source="McHale University">MCU_v0123_02</instantiationIdentifier>
    <instantiationLocation>McHale University</instantiationLocation>
    <instantiationRelation>
      <instantiationRelationType>Is Dub of</instantiationRelationType>
      <instantiationRelationIdentifier>MCU_v0123_01<instantiationRelationIdentifier>
    </instantiationRelation>
  </pbcoreInstantiation>
</pbcoreDescriptionDocument>

```

```xml
<rdf:Description about="MCU_a0567">
  <rdf:type rdf:resource="ebucore:EditorialObject" />
  <ebucore:title>Death Is A Poor Man's Doctor</ebucore:title>
  <ebucore:description>Interviews from Detroit musicians</a>
  <dc:hasFormat>MCU_v0123_01</dc:hasFormat>
</rdf:Description>

<rdf:Description about="MCU_v0123_01">
  <rdf:type rdf:resource="ebucore:MediaResource" />
  <dc:isFormatOf>MCU_a0567</dc:hasFormat>
  <ebucore:locator>McHale University</ebucore:locator>
  <ebucore:dubbedTo>MCU_v0123_02</ebucore:dubbedTo>
</rdf:Description>

<rdf:Description about="MCU_v0123_02">
  <rdf:type rdf:resource="ebucore:MediaResource" />
  <dc:isFormatOf>MCU_a0567</dc:hasFormat>
  <ebucore:locator>McHale University</ebucore:locator>
  <ebucore:isDubbedFrom>MCU_v0123_01</ebucore:isDubbedFrom>
</rdf:Description>
```