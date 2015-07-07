# MOSS
Media Object Storage System

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



