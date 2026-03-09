# EOSC Profiles

This package defines the EOSC Profiles data model, a shared and interoperable 
data model that Nodes of the EOSC Federation can use to exchange information 
about the resources in their catalogues. 
It ensures that every Node describes services, data sources, training materials, 
interoperability guidelines, deployable applications, and organisations 
using a common, machine‑readable structure.

Figure 1 gives an overview of the data model. Relationships among entities are 
semantically labelled. The label 'isA' denotes a hierarchical relationship ('super-class'). 
For example: Datasource is a sub-class ('isA') of Service, Service is a sub-class ('isA') of Resource.
Sub-classes inherit all the properties of their super-class.

![img/model-overview.png][model-overview]

[model-overview]: img/model-overview.png "Figure 1. Overview of the EOSC profiles data model"


## EOSC Resource

EOSC Resource is the super-class that defines properties shared among the different sub-classes.

| Field | Description | Type | Multiplicity | Mandatory | Vocabulary |
|---|---|---|---|---|---|
| id | A persistent identifier, a unique reference to the Resource | String | 1 | M |  |
| alternativePIDs | Other persistent identifiers | List of Objects | 1 | O |  |
| pid | PID value | String | 1 | M |  |
| pidSchema | PID schema | String | 1 | O |  |
| url | URLs resolving to the resource | URL | N | O |  |
| name | Name or title of the resource | String | 1 | M |  |
| description | A high-level description in fairly non-technical terms of a) what the Resource does, functionality it provides and Resources it enables to access, b) the benefit to a user/customer delivered by a Resource; benefits are usually related to alleviating pains (e.g., eliminate undesired outcomes, obstacles or risks) or producing gains (e.g. increased performance, social gains, positive emotions or cost saving), c) list of customers, communities, users, etc. using the Resource. | String | 1 | M |  |
| publishingDate | date in which the resource was made available for discovery and access to others | Date (ISO 8601) | 1 | M |  |
| type | Type of the resource. One among: Service, DataSource, Adapter, InteroperabilityGuidelines, TrainingMaterial, DeployableApplication | String | 1 | M |  |
| nodePID | Node the resource belongs to | String | 1 | M |  |
| resourceOwner | PID of the organization that manages or delivers the Resource | String | 1 | O |  |
| publicContact | Email to contact for the resource | email | N | M |  |


## Service

A Service is an EOSC Resource. As such, it inherits all its fields.
In addition, a Service has the following properties:

| Field | Description | Type | Multiplicity | Mandatory | Vocabulary |
|---|---|---|---|---|---|
| serviceProviders | The name(s) (or abbreviation(s)) of Provider(s) that manage or deliver the Service in federated scenarios. | array of Strings | 1 | R |  |
| webpage | Webpage with information about the Service usually hosted and maintained by the Provider. | URL | 1 | M |  |
| logo | Link to the logo/visual identity of the Service. The logo will be visible at the Portal. If there is no specific logo for the Service the logo of the Provider may be used. | URL | 1 | R |  |
| scientificDomains | The branch of science, scientific discipline that is related to the Service. | Object | 1 | R |  |
| scientificDomain | nan | string Vocabulary ScientificDomains | 1 | M |  |
| scientificSubdomain | nan | string Vocabulary ScientificSubDomains | 1 | M |  |
| categories | nan | list of objects | 1 | R |  |
| category | nan | string Vocabulary ServiceCategory | 1 | M |  |
| subcategory | nan | string Vocabulary Service SubCategory | 1 | M |  |
| tags | free text Keywords associated to the Service to simplify search by relevant keywords. | array of string | 1 | R |  |
| accessType | Type of access to the service (e.g. physical, virtual) | string Vocabulary AccessType | 1 | R |  |
| jurisdiction | The property defines the jurisdiction of the users of the service, based on the vocabulary for this property | string Vocabulary Jurisdiction | 1 | M |  |
| trl | The Technology Readiness Level of the Service | string Vocabulary TRL | 1 | M |  |
| termsOfUse | Webpage describing the rules, Service conditions and usage policy which one must agree to abide by in order to use the Service. | URL | 1 | O |  |
| privacyPolicy | Link to the privacy policy applicable to the Service. | URL | 1 | O |  |
| accessPolicy | Information about the access policies that apply. | URL | 1 | O |  |
| orderType | Information on the order type: if the service is open access of if an order is required. | string Vocabulary OrderType | 1 | O |  |
| order | Webpage through which an order for the Service can be placed. | URL | 1 | O |  |

## Data Source

A Data Source is a specific type of Service. As such, it inherits all its fields.
In addition, a Data Source has the following properties:

| Field | Description | Type | Multiplicity | Mandatory | Vocabulary |
|---|---|---|---|---|---|
| submissionPolicyUrl | This policy provides a comprehensive framework for the contribution of research products. Criteria for submitting content to the repository as well as product preparation guidelines can be stated. Concepts for quality assurance may be provided. | URL | 1 | R |  |
| preservationPolicyUrl | This policy provides a comprehensive framework for the long-term preservation of the research products. Principles aims and responsibilities must be clarified. An important aspect is the description of preservation concepts to ensure the technical and conceptual utility of the content | URL | 1 | R |  |
| versionControl | If data versioning is supported: the data source explicitly allows the deposition of different versions of the same object | Boolean | 1 | O |  |
| persistentIdentitySystems | The persistent identifier systems that are used by the Data Source to identify the ProductType it supports | lis of objects | 1 | R |  |
| persistentIdentityProductType | Specify the ProductType to which the persistent identifier is referring to. | Vocabulary: Research Product Type | 1 | M |  |
| persistentIdentityProductTypeScheme | Specify the list of persistent identifier schemes used to refer to other research-related entities (e.g., authors, organizations, etc.) | List. each value from Vocabulary: Persistent Identity Scheme | N | M |  |
| dataSourceClassification | The specific type of the data source based on the vocabulary defined for this property | Vocabulary: Data Source Classification | 1 | M |  |
| researchProductTypes | The types of OpenAIRE products managed by the data source, based on the vocabulary for this property | array of strings
Vocabulary: Research Product Type | 1 | M |  |
| thematic | Boolean value specifying if the data source is dedicated to a given discipline or is instead discipline agnostic | Boolean | 1 | M |  |
| metadataLicense | License of metadata about the data hosted by the source. It specifies under which license all metadata in the repository can be accessed, used, and repurposed. | LicenseType. Object values from the SPDX vocabulary | 1 | R |  |
| licenseName | Name of the license | string | 1 | R |  |
| licenseURL | URL of the license | URL | 1 | R |  |

## Adapter

An Adapter is an EOSC Resource. As such, it inherits all its fields.
In addition, a Adapter has the following properties:

| Field | Description | Type | Multiplicity | Mandatory | Vocabulary |
|---|---|---|---|---|---|
| linkedResource | EOSC Service or Guideline reference | Object | 1 | M |  |
| type | Type of resource linked | String. One among: Service, InteroperabilityGuidelines | 1 | M |  |
| id | Unique ID of the resource linked | String | 1 | M |  |
| tagline | Short (one-sentence) description | String | 1 | O |  |
| logo | URL to the logo of the adapter | URL | 1 | O |  |
| documentation | Documentation webpage (eg, read-the-docs page) | URL | 1 | M |  |
| repository | Code repository webpage (eg, Github repository) | URL | 1 | M |  |
| package | Software package releases webpage | URL | 1 | M |  |
| programmingLanguage | Programming language | String Vocabulary ProgrammingLanguages | 1 | M |  |
| license | License of the source code of the adapter | LicenseType. Object values from the SPDX vocabulary | 1 | M |  |
| licenseName | Name of the license | String | 1 | M |  |
| icenseURL | URL of the license | URL | 1 | M |  |
| version | Software version | String | 1 | M |  |
| changeLog | Changes in the latest version | String | 1 | M |  |
| lastUpdate | Latest update date | Date (ISO 8601) | 1 | M |  |
| creator | nan | PersonType | N | M |  |
| firstName | First Name of the person | string | 1 | M |  |
| lastName | Last Name of the person | string | 1 | M |  |
| email | Email of the person | string | 1 | M |  |
| pids | persistent ids of the person | List of objects | 1 | O |  |
| pid | pid | string | 1 | M |  |
| pidScheme | PID scheme | string | 1 | M |  |
| affiliations | The organizational or institutional affiliation of the person. | List of objects | 1 | O |  |
| affiliationName | Name of the organisation | string | 1 | M |  |
| affiliationIdentifiers | Uniquely identifies the organizational affiliation of the person. | List of objects | 1 | O |  |
| id | PID of the organisation | string | 1 | M |  |
| type | Type of the PID of the organisation | string | 1 | M |  |
| role | Role of the person in the context of this entity | String Vocabulary Credit Taxonomy | 1 | O |  |
| notes | Notes: for optional attributes. | Object | 1 | O |  |
| sqa | URL to the software quality scores/badges | URL | 1 | O |  |

## InteroperabilityGuideline

An InteroperabilityGuideline is an EOSC Resource. As such, it inherits all its fields.
In addition, an InteroperabilityGuideline has the following properties:


| Field | Description | Type | Multiplicity | Mandatory | Vocabulary |
|---|---|---|---|---|---|
| resourceTypesInfo | Interoperability Guideline type. | object | 1 | M |  |
| resourceTypeGeneral | Type of the resource. Default value, not editable: "Guideline" | string('Guideline') | 1 | M |  |
| resourceType | Specific type of the guideline. | string | 1 | M |  |
| license | License of the source code of the adapter | LicenseType. Object values from the SPDX vocabulary | 1 | M |  |
| License Name | Name of the license | String | 1 | M |  |
| License URL | URL of the license | URL | 1 | M |  |
| relatedStandards | Standards related to the guideline This should point out to related standards only when it is a prerequisitite/dependency, and likely to influence a Provider’s design towards interoperability based on the guideline. | list of objects | 1 | O |  |
| relatedStandardURI | The URI of the related standard. | URL | 1 | M |  |
| relatedStandardIdentifier | The name of the related standard. | string | 1 | M |  |
| creator | nan | PersonType | N | M |  |
| firstName | First Name of the person | string | 1 | M |  |
| lastName | Last Name of the person | string | 1 | M |  |
| email | Email of the person | string | 1 | M |  |
| pids | persistent ids of the person | List of objects | 1 | O |  |
| pid | pid | string | 1 | M |  |
| pidScheme | PID scheme | string | 1 | M |  |
| affiliations | The organizational or institutional affiliation of the person. | List of objects | 1 | O |  |
| affiliationName | Name of the organisation | string | 1 | M |  |
| affiliationIdentifiers | Uniquely identifies the organizational affiliation of the person. | List of objects | 1 | O |  |
| id | PID of the organisation | string | 1 | M |  |
| type | Type of the PID of the organisation | string | 1 | M |  |
| role | Role of the person in the context of this entity | String Vocabulary Credit Taxonomy | 1 | O |  |

## DeployableApplication


A DeployableApplication is an EOSC Resource. As such, it inherits all its fields.
In addition, a DeployableApplication has the following properties:

| Field | Description | Type | Multiplicity | Mandatory | Vocabulary |
|---|---|---|---|---|---|
| acronym | Acronym of the Application | string | 1 | M |  |
| tagline | Short catch-phrase for marketing and advertising purposes. It will be usually displayed close to the Resource name and should refer to the main value or purpose of the Resource. | string | 1 | O |  |
| logo | Link to the logo of the deployable application. | URL | 1 | O |  |
| version | Version of the Resource. | string | 1 | M |  |
| lastUpdate | Date of the latest update of the Resource. | date | 1 | O |  |
| license | License of the deployable application | LicenseType. Object values from the SPDX vocabulary | 1 | R |  |
| licenseURL | URL of the license | URL | 1 | R |  |
| licenseName | Name of the license | string | 1 | R |  |
| scientificDomains | The branch of science, scientific discipline that is related to the Service. | list of Objects | 1 | R |  |
| scientificDomain | nan | string Vocabulary ScientificDomains | 1 | M |  |
| scientificSubdomain | nan | string Vocabulary ScientificSubDomains | 1 | M |  |
| tags | Keywords associated to the Resource to simplify search by relevant keywords. | list of string | 1 | O |  |
| creator | nan | PersonType | N | M |  |
| firstName | First Name of the person | string | 1 | M |  |
| lastName | Last Name of the person | string | 1 | M |  |
| email | Email of the person | string | 1 | M |  |
| pids | persistent ids of the person | list of objects | 1 | O |  |
| pid | pid | string | 1 | M |  |
| pidScheme | PID scheme | string | 1 | M |  |
| affiliations | The organizational or institutional affiliation of the person. | list of objects | 1 | O |  |
| affiliationName | Name of the organisation | string | 1 | M |  |
| affiliationIdentifiers | Uniquely identifies the organizational affiliation of the person. | list of objects | 1 | O |  |
| id | PID of the organisation | string | 1 | M |  |
| type | Type of the PID of the organisation | string | 1 | M |  |
| role | Role of the person in the context of this entity | String Vocabulary Credit Taxonomy | 1 | O |  |

## TrainingResource

A TrainingResource is an EOSC Resource. As such, it inherits all its fields.
In addition, a TrainingResource has the following properties:


| Field | Description | Type | Multiplicity | Mandatory | Vocabulary |
|---|---|---|---|---|---|
| eoscRelatedServices | PIDs of services related to this training resource | list of string | 1 | M |  |
| keywords | The keyword(s) or tag(s) used to describe the resource. | nan | 1 | M |  |
| license | License of the training resource | LicenseType | 1 | M |  |
| licenseURL | URL of the license | String | 1 | M |  |
| licenseName | Name of the license | string | 1 | M |  |
| accessRights | The access status of a resource (open, restricted, paid). | string Vocabulary TR_ACCESS_RIGHTS | 1 | M |  |
| versionDate | The date of the latest version of the training resource | Date (ISO 8601) | 1 | M |  |
| targetGroups | The principal users(s) for which the learning resource was designed. | list of string Vocabulary TARGET_USER | 1 | M |  |
| learningResourceTypes | The predominant type or kind that characterizes the learning resource. | list of string Vocabulary TR_DCMI_TYPE | 1 | M |  |
| learningOutcomes | The descriptions of what knowledge, skills or abilities students should acquire on completion of the resource. | list of string | 1 | M |  |
| expertiseLevel | Target skill level in the topic being taught. | string Vocabulary TR_EXPERTISE_LEVEL | N | M |  |
| contentResourceTypes | The predominant content type of the learning resource (video, game, diagram, slides, etc.). | list of string Vocabulary TR_CONTENT_RESOURCE_TYPE | 1 | M |  |
| qualifications | Identification of certification, accreditation or badge obtained with course or learning resource. | string Vocabulary TR_QUALIFICATION | 1 | R |  |
| duration | Approximate or typical time it takes to work with or through the learning resource for the typical intended target audience. | string | N | M |  |
| languages | The language in which the resource was originally published or made available. | list of string Vocabulary Language (ISO 2-letter codes) | 1 | O |  |
| scientificDomains | The branch of science, scientific discipline that is related to the Service. | list of Objects | 1 | R |  |
| scientificDomain | nan | string Vocabulary ScientificDomains | 1 | M |  |
| scientificSubdomain | nan | string Vocabulary ScientificSubDomains | 1 | M |  |
| creator | nan | PersonType | N | M |  |
| firstName | First Name of the person | string | 1 | M |  |
| lastName | Last Name of the person | string | 1 | M |  |
| email | Email of the person | string | 1 | M |  |
| pids | persistent ids of the person | list of objects | 1 | O |  |
| pid | pid | string | 1 | M |  |
| pidScheme | PID scheme | string | 1 | M |  |
| affiliations | The organizational or institutional affiliation of the person. | list of objects | 1 | O |  |
| affiliationName | Name of the organisation | string | 1 | M |  |
| affiliationIdentifiers | Uniquely identifies the organizational affiliation of the person. | list of obejcts | 1 | O |  |
| id | PID of the organisation | string | 1 | M |  |
| type | Type of the PID of the organisation | string | 1 | M |  |
| role | Role of the person in the context of this entity | String Vocabulary Credit Taxonomy | 1 | O |  |

## Organization

| Field | Description | Type | Multiplicity | Mandatory | Vocabulary |
|---|---|---|---|---|---|
| id | A persistent identifier, a unique reference to the organisation | String | 1 | M |  |
| alternativePIDs | Other persistent identifiers | list of Objects | 1 | O |  |
| pid | PID value | String | 1 | M |  |
| pidSchema | PID schema | String | 1 | O |  |
| name | Name of the organisation | String | 1 | M |  |
| abbreviation | Acronym or short name of the organisation | String | 1 | M |  |
| website | Website of the organisation | URL | 1 | M |  |
| country | Country of incorporation or Physical location of the organisation or its coordinating centre in the case of distributed, virtual, and mobile providers. | string (Vocabulary COUNTRY) | 1 | M |  |
| legalEntity | Yes if the organisation is a legal entity. False if it is not (e.g. a project consortium) | boolean | 1 | M |  |
| legalStatus | Legal status of the Organisation. The legal status is usually noted in the registration act/statutes. For independent legal entities (1) - legal status of the Provider. For embedded organisations (2) - legal status of the hosting legal entity. | string (Vocabulary PROVIDER_LEGAL_STATUS) | 1 | R |  |
| hostingLegalEntity | Name of the organisation/institution legally hosting (housing) the provider/research infrastructure or its coordinating centre. A distinction is made between: (1) research infrastructures that are self-standing and have a defined and distinct legal entity, (2) research infrastructures that are embedded into another institution which is a legal entity (such as a university, a research organisation, etc.). If (1) - name of the research infrastructure, If (2) - name of the hosting organisation. | string (Vocabulary) | 1 | R |  |
| description | A high-level description of the Organisation in fairly non-technical terms, with the vision, mission, objectives, background, experience. | String | 1 | M |  |
| logo | Link to the logo/visual identity of the Organisation. | URL | 1 | M |  |
| multimedia | Link to video, slideshow, photos, screenshots with details of the Organisation. | List of objects | 1 | O |  |
| multimediaURL | URL to the multimedia resource. | URL | 1 | M |  |
| multimediaName | Name of the multimedia resource. | String | 1 | M |  |
| publicContact | Email to contact the organisation | email | N | M |  |
| nodePID | Node the organisation is contributing to | PID | 1 | M |  |
