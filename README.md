# MOSS
Media Object Storage System

## Purpose
Innovate UK https://www.gov.uk/government/organisations/innovate-uk funded project to research and develop object-based ‘blob’ storage systems that are optimised for the network-based processing, distribution and archiving of very large collections of media files or scientific data. 


The project demonstrates ways of combining object-based storage and functional programming to archive, store, process and distribute professional media data across networks and in the Cloud. 


The aim is to  provide far greater data resilience, permanence and ease of network delivery than current systems, and resolve problems of versioning. 


The project leader is a SME solutions provider (Ovation), working with a large creative media facilities company (Smoke & Mirrors), and a research group at Imperial College that has pioneered functional programming, parallel and distributed software development frameworks



##  Walkthrough of a use of the Subtitling Workflow 
[![MOSS Subtitle Walkthrough](http://i.imgur.com/9dWxseG.png)](https://www.youtube.com/watch?v=_6Ks8P8MuIs "MOSS Subs Walkthrough")


## Architecture Diagram
![Architecture](http://i.imgur.com/N4fdZvZ.jpg)

## Conceptual Diagram
![Conceptual](http://i.imgur.com/bECn8xF.jpg)

## Repository Interface Definition

```javascript
interface Repository {
  function getLicenses() { return ['license1', 'license2'] }

  function getOrganisations() { return [{ name: '', licenses: [] }]; }
  function getUsers() { return { name: '', organisation: 'icl' }; }
  function getMachines() {}
  
  function getAbstractMethods() {
    return [
      { name: 'reduce', implementation: ['reduceS', 'reduceP'] }
    ];
  }
}
````

## Changesets

A changeset is a JSON array containing the change objects:

```
[
{ 
  action: addition || removal , 
  s: subjectUri, 
  p: propertyName, 
  o: valueOfProperty, 
  o_type: resource || literal 
}
]

```

- `addition` indicates a subject's property value is being added
- `removal` indicates a subject's property value is being removed
- `s` is the `uri` of the resource being updated
- `p` is the property being updated
- `o` is the value being updated
- `o_type` denotes whether `o` should be interpreted as a `uri` or a `literal` value
- `resource` indicates that the value is the uri of another object/resource in the system
- `literal` indicates that the value is a text, boolean, or numeric value

eg:

```
[
  {  
     action: "addition", 
     s: "openshare:user/john", 
     p: "name", 
     o: "John", 
     o_type: "literal"
  },
  { 
     action: "addition", 
     s: "openshare:user/john", 
     p: "organisation", 
     o: "openshare:org/acme", 
     o_type: "resource"
  },
]
```



