# About 
Homepage: https://www.link2.ca/

# Agile Documentation
[Agile manifesto](https://www.agilealliance.org/agile101/the-agile-manifesto/)

# Ontology Docs 
[Structured Data](https://docs.inrupt.com/developer-tools/javascript/client-libraries/structured-data/)

# Solid Documentation 
Documentation of solid development is messy, I've attempted to organize what I think is most useful below

## App dev
- Recommended: [solid-ui-react Github](https://github.com/inrupt/solid-ui-react#development)
  - Good for authentication in [React](https://solid-ui-react.docs.inrupt.com/?path=/docs/usage--page), beyound that not too great
  - **Note**: their [example app](https://github.com/inrupt/solid-ui-react-demo) has dependency issues, and is deprecated. Here's a [working one](https://github.com/link2pod/NextAppExample)
  - **Note**: their [online storybook](https://solid-ui-react.docs.inrupt.com/) is also kindof broken, and data components aren't documented
- [Inrupt JS Library Usage Examples](https://docs.inrupt.com/developer-tools/javascript/client-libraries/using-libraries/)
  - Provides good introduction to RDF modelling
  - Strong tools for [reading+writing data](https://docs.inrupt.com/developer-tools/javascript/client-libraries/tutorial/read-write-data/)
- [Solidproject first-app tutorial](https://solidproject.org/developers/tutorials/first-app) 
  - Parcel issues, would not recommend

## Solid Servers (Optional reading)
Not too important, so just go the recommended
- Recommended: [Github Repo Docs - Getting started](https://github.com/CommunitySolidServer/tutorials/blob/main/getting-started.md)
  - Great introduction, goes over concepts at good level. (30-45 mins)
- [Solidproject server hosting](https://solidproject.org//self-hosting/css)
  - Useful for seeing all the options and quickstarting 
  - insufficient details for anything useful
- [Github Repo Docs](https://github.com/CommunitySolidServer/CommunitySolidServer/tree/main/documentation/markdown)
  - More details, but useful tutorials and links to references

### Authentication
Overview of authentication flow: https://solidproject.org/TR/oidc#basic-flow
For solid authentication, there's many protocols being considered. The 2 main ones are WAC and ACP. 

#### Web Access Control (WAC) 
Server side: when server receives GET request for resource (say http://example.ttl) then it looks for corresponding acl file (default is http://example.ttl.acl, but could be different) 
- If no acl file exists, permissions on the parent will be used (i.e. look for http://dir1/dir2/file.ttl.acl, then http://dir1/dir2/.acl, then http://dir1/.acl)
- There's 4 permission modes: read, write, append, control, each with [corresponding representations](https://solid.github.io/web-access-control-spec/#authorization-rule) 
  - control permission refers to ability to change the acl for the resource 
- the acl file is a RDF file with [these requirements](https://solid.github.io/web-access-control-spec/#authorization-conformance). 

Client side: client must send HEAD request for resource, then follow the "Link: rel=acl <url>" header to locate the required ACL resource, then GET it 
- inrupt's [solid-client JS library](https://docs.inrupt.com/developer-tools/javascript/client-libraries/tutorial/manage-wac/#change-access-to-a-resource) has helpful functions

#### ACP 
Server side: similar recursive permission inheritance 
- 3 permissions: read, write, append 
Client side: [inrupt library](https://docs.inrupt.com/developer-tools/javascript/client-libraries/tutorial/manage-acp/)

