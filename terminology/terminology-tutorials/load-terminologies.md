---
description: In this post we will see how load popular terminologies into aidbox.
---

# Load ICD-10 terminology into Aidbox

With a next version of Aidbox we provide you with set of terminology packages like ICD-10 and LOINC and special bulk operation to import this code systems into your box.

You can read more about how Aidbox terminology service designed in a our CTO blog post - [Two-phase terminology](https://medium.com/@niquola/two-phase-fhir-terminology-e52e1b105f6d). 

In this tutorial we will load ICD-10 deceases codes into Aidbox and see how we can lookup codes using Concept resource Search API.

Aidbox team prepared terminology packages with popular code systems for your. This packages are essentially ndjson files with set of concept resources and they are available by public url in our cloud.

Here is the few packages you can start with:

* ICD-10 - [https://storage.googleapis.com/aidbox-public/icd10/icd10cm.ndjson.gz](https://storage.googleapis.com/aidbox-public/icd10/icd10cm.ndjson.gz)
* LOINC - [https://storage.googleapis.com/aidbox-public/loinc/loinc-concepts-2.65.ndjson.gz](https://storage.googleapis.com/aidbox-public/loinc/loinc-concepts-2.65.ndjson.gz)

Rx-Norm, SNOMED-CT and basic FHIR CodeSystems/ValueSets packages are in progress. If you need something specific - ping us in a [Aidbox Community Chat](https://community.aidbox.app).

To load this terminology packs you can use  `terminology/$import` operation. Let's load ICD-10 \(Classification of Deceases\) - just copy-paste following snippet into REST console in Aidbox UI:

{% code-tabs %}
{% code-tabs-item title="request.yalm" %}
```yaml
POST /terminology/$import

url: 'https://storage.googleapis.com/aidbox-public/icd10/icd10cm.ndjson.gz'
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You will get response with numbers of resources loaded:

{% code-tabs %}
{% code-tabs-item title="response.yaml" %}
```yaml
status: 200
result: {CodeSystem: 1, ValueSet: 1, Concept: 44487}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

As you can see package consists of one CodeSystem, one ValueSet and about 40K concepts with decease codes.

Let's go to REST console and see what do we have:

```yaml
GET /CodeSystem

# response 200

resourceType: Bundle
type: searchset
entry:
- resource:
    url: ICD-10
    id: icd-10
    name: ICD-10-CM
    status: active
    content: complete
    version: '2019'
    date: '2019'
    resourceType: CodeSystem
    description: International Classification of Diseases
```

```yaml
GET /ValueSet

# response 200

resourceType: Bundle
type: searchset
entry:
- resource:
    url: icd-10
    id: icd-10
    name: ICD-10
    status: active
    compose:
      include:
      - {system: ICD-10}
    version: 0.0.1
    date: '2019-01-01'
    resourceType: ValueSet
    description: This value set includes all ICD-10 codes.
```

Now we can search diagnoses with for example [\_ilike](../../api/search.md#_ilike-search-non-fhir) parameter:

```yaml
GET /Concept?system=ICD-10&_ilike=flue

# response 200
resourceType: Bundle
type: searchset
entry:
- resource:
    code: A08
    system: ICD-10
    display: Viral and other specified intestinal infections
    property:
      icd10:
        excludes1: ['influenza with involvement of gastrointestinal tract (J09.X3, 10.2, J11.2)']
    valueset: [icd-10]
    id: ICD-10-A08
    resourceType: Concept
- resource:
    code: A41.3
    system: ICD-10
    display: Sepsis due to Hemophilus influenzae
    valueset: [icd-10]
    id: ICD-10-A41-3
    resourceType: Concept
...
```

Or  inspect concepts in Aidbox Console UI:

![](../../.gitbook/assets/screen-shot-2019-05-14-at-17.23.53.png)

### Clean up

To clean up all terminology you can truncate all related tables from db console:

```sql
truncate concept;
truncate codesystem;
truncate valueset;
```
