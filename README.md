# Data Enrichment

The common data-enrichment vocabulary -- the person profiles and company profiles returned when you look someone or something up, and the email lookups that find and verify an address -- distilled from the APIs that already exist. These are results, not records you own: CRM owns the contacts and companies you keep. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Data Enrichment, Lead Generation, B2B Data, People Data, Company Data, Firmographics, Contact Data, Email Finder, Email Verification in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| person_profile | 26 | 22 | name 55% | people 9, enrich 7, person 7, persons 4 |
| company_profile | 35 | 31 | name 71%, domain 61%, description 55%, id 55% | companies 19, company 11, organizations 8, enrich 5 |
| email_lookup | 7 | 6 | email 100%, result 83%, catch_all 67%, domain 67%, first_name 50%, last_name 50%, linkedin_url 50%, score 50% | email-finder 4, email-verifier 3, email-verification 2, find 1 |

Cohort: 137 providers with harvested OpenAPI, 47 crosswalks. Of the providers exposing a person_profile: 62% create, 54% list, 31% fetch, 4% update, 4% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A company profile agrees on name, domain, description and id -- the domain is the join key of B2B data, and every enrichment provider returns it.
- A person profile agrees only on a name: email, title, company and LinkedIn URL are each returned by a minority, because people data is sold field by field and each vendor's coverage differs.
- An email lookup agrees on the email, a result and a confidence score, and whether the domain is catch-all -- verification is the most uniform enrichment product.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Enrichment returns results about people and companies; CRM owns the contacts and companies you keep. Profiles are `/person-profiles` and `/company-profiles`, lookups `/email-lookups`.
- Prospects, and people or contacts beneath an enrich or search path, are person profiles; organizations and firmographics are company profiles.
- Duplicates merged: Apollo, Golden, Parallel, Windfall.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
