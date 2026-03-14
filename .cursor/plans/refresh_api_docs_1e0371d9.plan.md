---
name: Refresh API docs
overview: Restructure the DiHub docs around the current canonical root `openapi.json`, replace the stale `openapi.yaml`-driven API reference wiring, normalize the public API contract shown across docs, and add or reconcile the supporting pages for billing rules and certificates.
todos:
  - id: audit-openapi-structure
    content: Confirm `openapi.json` as the canonical source and identify all stale OpenAPI-derived files and navigation references
    status: completed
  - id: normalize-api-contract
    content: Reconcile auth header, server/base URL, versioning, language, and endpoint path naming so all docs describe the same public contract from `openapi.json`
    status: completed
  - id: fix-openapi-delivery
    content: Rewire Mintlify so the API reference is generated from root `openapi.json` instead of `openapi.yaml`, and ensure the raw asset route resolves correctly
    status: completed
  - id: upgrade-openapi-spec
    content: Refine root `openapi.json` so it is richer, cleaner, and better organized for API reference rendering without treating `openapi.yaml` as source of truth
    status: completed
  - id: add-reference-mdx-pages
    content: Reconcile existing MDX reference pages under `api-reference/` with the AbacatePay-inspired structure, removing or merging duplicate pages where necessary
    status: completed
  - id: decide-webhooks-treatment
    content: Either document webhooks properly or remove/hide the placeholder page until the feature is ready to publish, based on the current branch content
    status: completed
  - id: sanitize-auth-examples
    content: Replace token-like examples and outdated execute-api URLs with safe placeholders aligned to the final contract
    status: completed
  - id: add-credit-disclaimer
    content: Add or reconcile a clear page or section documenting credit consumption rules and disclaimer language
    status: completed
  - id: add-certificates-page
    content: Add or reconcile the 'Todas as certidões' page using the provided JSON source, with the final presentation order defined explicitly
    status: completed
  - id: wire-navigation
    content: Update navigation so the existing and new pages fit the final Guide/API structure without duplicate or stale API-reference entries
    status: completed
  - id: verify-published-output
    content: Verify the final docs through Mintlify output and MCP discoverability so the refreshed content is actually reachable
    status: completed
isProject: false
---

# Refresh API Docs

## Scope

Update the Mintlify docs so the API section feels closer to AbacatePay's structure, while staying simpler and more direct for DiHub users. The work must use the current root [openapi.json](/Users/clcostaf/dihub/api-docs/openapi.json) as the canonical API contract, replace stale branch assumptions tied to [openapi.yaml](/Users/clcostaf/dihub/api-docs/openapi.yaml), and make the published API reference actually usable.

## What I will change

- Treat root [openapi.json](/Users/clcostaf/dihub/api-docs/openapi.json) as the canonical contract and stop treating [openapi.yaml](/Users/clcostaf/dihub/api-docs/openapi.yaml) as the active source for Mintlify generation.
- Reconcile the existing branch state: [api-reference/openapi.json](/Users/clcostaf/dihub/api-docs/api-reference/openapi.json), [openapi.yaml](/Users/clcostaf/dihub/api-docs/openapi.yaml), and the already-generated MDX pages under [api-reference](/Users/clcostaf/dihub/api-docs/api-reference) must either be updated from root `openapi.json` or removed if stale/duplicative.
- Normalize the public contract described by the docs: one auth header, one base URL strategy, one endpoint naming style, one language strategy, and one versioning approach across OpenAPI, guide pages, and examples.
- Refactor [openapi.json](/Users/clcostaf/dihub/api-docs/openapi.json) to be more presentation-friendly for Mintlify: clearer `info`, explicit `servers`, correct auth metadata, grouped tags, improved operation summaries/descriptions, richer request/response examples, and reusable schemas/responses modeled after the better-structured parts of AbacatePay.
- Explicitly verify that the final Mintlify API reference route renders from root `openapi.json` and that the raw OpenAPI asset can be fetched without `404`/`500` failures.
- Reconcile the existing MDX reference content already present in [api-reference/overview.mdx](/Users/clcostaf/dihub/api-docs/api-reference/overview.mdx), [api-reference/credits/balance.mdx](/Users/clcostaf/dihub/api-docs/api-reference/credits/balance.mdx), and [api-reference/diligences/emit.mdx](/Users/clcostaf/dihub/api-docs/api-reference/diligences/emit.mdx), keeping the structure inspired by AbacatePay but simple and direct.
- Replace token-like sample credentials and outdated execute-api URLs with safe placeholders and the final canonical base URL.
- Add or reconcile the credit-consumption disclaimer so it matches the billing rules you provided in a scannable way.
- Add or reconcile a page titled `Todas as certidões` with a table built from [Nome das certidões.json](/Users/clcostaf/dihub/api-docs/Nome%20das%20certido%CC%83es.json), listing certificate name and issuing authority, with a defined sorting/presentation rule.
- Update [docs.json](/Users/clcostaf/dihub/api-docs/docs.json) navigation so the API area points to the final canonical OpenAPI setup and avoids duplicate manual/generated API pages.
- Review existing intro/auth/webhooks pages and make the level of change explicit: small consistency fixes for intro/auth, plus a real decision for webhooks (publish proper docs or remove the placeholder from navigation).

## Key repo facts informing the plan

- [docs.json](/Users/clcostaf/dihub/api-docs/docs.json) currently points the API Reference tab to [openapi.yaml](/Users/clcostaf/dihub/api-docs/openapi.yaml), but you confirmed the correct API version is root [openapi.json](/Users/clcostaf/dihub/api-docs/openapi.json).
- The repo currently has at least three OpenAPI representations in play: [openapi.json](/Users/clcostaf/dihub/api-docs/openapi.json), [openapi.yaml](/Users/clcostaf/dihub/api-docs/openapi.yaml), and [api-reference/openapi.json](/Users/clcostaf/dihub/api-docs/api-reference/openapi.json). These are not aligned and must not all remain authoritative.
- The current `api-reference` folder already contains endpoint MDX pages such as [api-reference/overview.mdx](/Users/clcostaf/dihub/api-docs/api-reference/overview.mdx), [api-reference/credits/balance.mdx](/Users/clcostaf/dihub/api-docs/api-reference/credits/balance.mdx), and [api-reference/diligences/emit.mdx](/Users/clcostaf/dihub/api-docs/api-reference/diligences/emit.mdx), so the work is now partly a cleanup/reconciliation task, not just new page creation.
- The current generated/manual API pages still reference an outdated execute-api host instead of the canonical public base URL and contain token-like sample values that should not be published.
- The current root [openapi.json](/Users/clcostaf/dihub/api-docs/openapi.json) still conflicts with repo rules on key contract details, including auth header naming (`X-Api-Key` in the schema vs `X-Api-Token` in the docs/rules) and missing server metadata.
- The current webhooks page is still a placeholder, so it cannot be treated as a minor consistency-only touch unless the decision is to hide it for now.
- The certificates source is available in [Nome das certidões.json](/Users/clcostaf/dihub/api-docs/Nome%20das%20certido%CC%83es.json), so the `Todas as certidões` table can be generated from real data instead of guesswork.

## Planned file touch points

- [docs.json](/Users/clcostaf/dihub/api-docs/docs.json)
- [openapi.json](/Users/clcostaf/dihub/api-docs/openapi.json)
- [openapi.yaml](/Users/clcostaf/dihub/api-docs/openapi.yaml)
- [api-reference/openapi.json](/Users/clcostaf/dihub/api-docs/api-reference/openapi.json)
- [index.mdx](/Users/clcostaf/dihub/api-docs/index.mdx)
- [introduction/authentication.mdx](/Users/clcostaf/dihub/api-docs/introduction/authentication.mdx)
- [webhooks/webhooks.mdx](/Users/clcostaf/dihub/api-docs/webhooks/webhooks.mdx)
- Existing MDX files under [api-reference](/Users/clcostaf/dihub/api-docs/api-reference), including [api-reference/overview.mdx](/Users/clcostaf/dihub/api-docs/api-reference/overview.mdx), [api-reference/credits/balance.mdx](/Users/clcostaf/dihub/api-docs/api-reference/credits/balance.mdx), and [api-reference/diligences/emit.mdx](/Users/clcostaf/dihub/api-docs/api-reference/diligences/emit.mdx)
- New page for credit consumption under a guide/reference section
- New page for all certificates, using [Nome das certidões.json](/Users/clcostaf/dihub/api-docs/Nome%20das%20certido%CC%83es.json)

## Content direction

- Keep all text in pt-BR to match the repository rules.
- Use AbacatePay as inspiration for structure, not for visual or textual copying.
- Keep pages short, direct, and task-oriented.
- Avoid duplicating endpoint details in MDX when OpenAPI already covers them.
- Prefer root `openapi.json` over YAML or generated JSON copies whenever a source-of-truth decision is required.
- Prefer explicit acceptance checks over implicit assumptions when Mintlify rendering behavior is part of the success criteria.

## Acceptance target

After implementation, the docs should have:

- a single coherent OpenAPI spec,
- root `openapi.json` used as the canonical source for the published API reference,
- one normalized public API contract across OpenAPI, guide pages, and examples,
- a cleaner API navigation structure,
- a working Mintlify API reference route,
- a raw OpenAPI asset that can be fetched successfully,
- simple MDX reference pages for context with no stale duplicates or outdated generated content left in place,
- authentication examples that use safe placeholders and the correct header name,
- removal of outdated execute-api URLs from public documentation,
- an explicit outcome for webhooks documentation instead of a placeholder page left unresolved,
- a clear credit billing disclaimer,
- a complete `Todas as certidões` table page based on your provided source,
- and MCP/search-visible documentation that reflects the refreshed structure after publish.

