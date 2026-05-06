# Standards & API Reference

> Project: Product Information Management (PIM) · Generated: 2026-05-03

## Industry Standards & Specifications

### ISO Standards

**ISO 22745 — Open Technical Dictionaries and Their Application to Master Data**
- URL: https://www.iso.org/standard/44191.html
- Multi-part standard (Parts 1, 10, 13, 14, 20, 30, 40) covering dictionary representation, query interfaces, concept identification, and master data exchange. Part 40 specifies the exchange file format for product catalogues where records are expressed as property-value pairs keyed to concepts in an open technical dictionary. Foundational for interoperability between PIM and procurement systems; used alongside ETIM and eClass to formalise attribute semantics.

**ISO 8000 — Data Quality**
- URL: https://www.iso.org/standard/81745.html (Part 1 overview); https://www.iso.org/standard/78501.html (Part 110)
- The definitive international standard for data quality in master data. Part 100 defines fundamentals of master data quality. Part 110 specifies requirements for the exchange of messages containing characteristic data (product attributes) in a computer-checkable format. Part 150 addresses data quality management roles and responsibilities. PIM systems should align quality scoring and validation rules with ISO 8000 definitions. Directly cited in EU Digital Product Passport regulation as a baseline for product data quality.

**ISO/IEC 15459 — Unique Identifiers for Transport Units, Returnable Transport Items, and Product Packaging**
- URL: https://www.iso.org/standard/54779.html
- Specifies globally unique identifier schemes for physical items in supply chains. Referenced in EU DPP technical specifications as the traceability identifier standard. PIM systems storing item-level data should support ISO 15459-compliant identifiers alongside GS1 keys.

### W3C & IETF Standards

**Schema.org — Product Type and Offer Vocabulary**
- URL: https://schema.org/Product
- W3C community-maintained structured data vocabulary used to mark up product pages for search engine rich snippets (name, description, image, identifiers, pricing, availability). JSON-LD is the recommended implementation format. A PIM that generates web-facing product data should produce Schema.org-compliant output. The GS1 Web Vocabulary is an official Schema.org external extension, adding supply-chain-specific properties.

**GS1 Web Vocabulary**
- URL: https://ref.gs1.org/voc/ and https://www.gs1.org/gs1-web-vocabulary
- Schema.org-aligned RDF vocabulary that extends product structured data with supply-chain properties (GTIN, batch/lot, expiry date, net content, GS1 Digital Link URI). Available in RDF/Turtle and JSON-LD. Enables machine-readable product data on the web, linking physical GS1 identifiers to digital product information pages. PIM systems exposing public product data APIs should support this vocabulary for semantic interoperability.

**GS1 Digital Link (URI Syntax Standard)**
- URL: https://www.gs1.org/standards/gs1-digital-link
- Defines how GS1 keys (GTIN, GLN, SSCC) are expressed as web URIs, enabling product barcodes and QR codes to resolve to structured data endpoints. The DPP data carrier mechanism uses GS1 Digital Link. PIM systems need to generate and resolve Digital Link URIs to meet DPP compliance requirements.

**RFC 6749 — OAuth 2.0 Authorization Framework**
- URL: https://datatracker.ietf.org/doc/html/rfc6749
- The de-facto standard for delegated API authorization. All major PIM platforms use OAuth 2.0 for API access. PIM APIs exposing product data to external systems, channels, and integrations must implement OAuth 2.0 bearer token flows (client credentials for server-to-server; authorization code for user-delegated access).

**RFC 7519 — JSON Web Token (JWT)**
- URL: https://datatracker.ietf.org/doc/html/rfc7519
- Specifies the JWT format used as access and ID tokens in OAuth 2.0 and OpenID Connect flows. PIM API authentication tokens are typically JWTs carrying scopes, roles, and tenant identifiers.

**OpenID Connect 1.0**
- URL: https://openid.net/specs/openid-connect-core-1_0.html
- Authentication layer built on OAuth 2.0. Standard for user identity in web-based PIM applications. Enables SSO integration with enterprise identity providers (Azure AD, Okta, etc.). Relevant for PIM platforms offering multi-tenant SaaS access.

### Data Model & API Specifications

**OpenAPI Specification (OAS) 3.1**
- URL: https://spec.openapis.org/oas/v3.1.0.html and https://www.openapis.org/
- The dominant standard for describing RESTful APIs. Akeneo's API is documented via OAS 3.1 (swagger). Any AI-native PIM should publish an OpenAPI spec for its REST API, enabling auto-generated client SDKs, Postman collections, and third-party integration tooling. OAS 3.1 aligns fully with JSON Schema 2020-12.

**JSON Schema 2020-12**
- URL: https://json-schema.org/specification
- Standard for validating and annotating JSON data. Used by ETIM xChange (the new JSON-based product data exchange format) and by OAS 3.1 for API request/response schema validation. A PIM's internal product attribute schema and API payloads should be expressible as JSON Schema for portable validation.

**GraphQL Specification (June 2018 Edition)**
- URL: https://spec.graphql.org/June2018/
- Query language for APIs; preferred for flexible, client-driven data fetching. Akeneo (via SaaS GraphQL API) and Pimcore (via DataHub) both support GraphQL. An AI-native PIM serving headless storefronts, composable commerce, and DXP architectures should offer a GraphQL endpoint alongside REST.

**BMEcat 2005**
- URL: https://www.bmecat.org/ (standard maintained by BME e.V.)
- XML-based B2B product catalogue exchange standard widely used in DACH markets and supported by most European ERP and procurement systems. PIM systems targeting European manufacturing and B2B distribution must support BMEcat export. Latest version (BMEcat 2005) supports multilingual content, technical attributes, price structures, and multimedia data. Free and open; no licence fees.

### Classification Standards

**GS1 Standards (GTIN / GLN / GPC / GDD)**
- URL: https://www.gs1.org/standards and https://www.gs1us.org/tools/gs1-us-data-hub/gs1-us-apis
- GS1 is the globally dominant product identification framework. Key identifiers: GTIN (product), GLN (location/organisation), SSCC (shipping unit). GS1 Global Product Classification (GPC) provides a standardised product taxonomy. The GS1 Global Data Dictionary (GDD) defines attribute semantics. GS1 Registry Platform APIs (REST/OData) allow programmatic lookup and validation of GTINs and company prefixes. PIM must support GTIN as a primary product identifier and GPC for classification.

**ETIM International — Electrotechnical Information Model**
- URL: https://www.etim-international.com/ and https://www.etim-international.com/classification/exchange-format/
- The leading classification standard for technical products in electrical, HVAC, plumbing, construction, and manufacturing sectors. Maintained by ETIM International with 70+ national member organisations. The ETIM model defines product classes, technical features, and allowed values. **ETIM xChange** (released February 2024) is a new JSON-based exchange format replacing BMEcat as the recommended ETIM data carrier. The ETIM API (REST) provides direct access to the full classification model. PIM targeting technical manufacturing/B2B must natively support ETIM class mapping and ETIM xChange export.

**ECLASS — International Product and Service Classification**
- URL: https://eclass.eu/en/ and https://eclass.eu/support/technical-specification/data-model/-eclass-webservice
- ISO-compliant classification standard providing 45,000 product classes and 19,000 described features, each with an 8-digit code and unique IRDI (International Registration Data Identifier). Prevalent in German manufacturing, automotive, and procurement. ECLASS provides a RESTful JSON API (documented on SwaggerHub) and a Download API for batch retrieval of class and property data. Technical specification TS-48 covers item data retrieval. PIM systems in industrial sectors should support ECLASS code assignment and ECLASS API integration for automated taxonomy mapping.

**EU Digital Product Passport (DPP) / Ecodesign for Sustainable Products Regulation (ESPR)**
- URL: https://www.gs1.org/standards/standards-emerging-regulations/DPP and https://en.wikipedia.org/wiki/EU_Digital_Product_Passport
- EU regulatory mandate under ESPR requiring a machine-readable digital record for products sold in the EU covering identity, compliance, sustainability, repairability, and circularity data. Rollout by product category: batteries (2026), textiles (2027), electronics (2028–2030). Data is attached via QR code, NFC, or RFID resolving to a DPP record in a standardised format. Technical data model based on Asset Administration Shell (AAS), JSON-LD aligned with Schema.org, and ISO 15459 traceability identifiers. Harmonised CEN/CENELEC standards in development; GS1 has published a Provisional Standard for DPP data carriers. PIM is the natural system of record for DPP data assembly. EU manufacturers and importers with European customers are directly affected.

### Security & Authentication Standards

**OAuth 2.0 (RFC 6749) and OpenID Connect 1.0**
- See entries above under W3C & IETF Standards. All major PIM platforms (Akeneo, Pimcore, inRiver, Salsify) use OAuth 2.0 for API authentication, typically via client credentials grant for server integrations.

**OWASP API Security Top 10**
- URL: https://owasp.org/www-project-api-security/
- The OWASP API Security Top 10 identifies critical API security risks (broken object-level authorisation, broken authentication, excessive data exposure, rate limiting, etc.). PIM APIs exposing product data externally must be designed against this checklist. Particularly relevant for multi-tenant SaaS PIM where tenant data isolation is critical.

**GDPR (General Data Protection Regulation)**
- URL: https://gdpr-info.eu/
- Applies where PIM stores personal data linked to products (e.g., customer-facing personalization or supplier contact data). Relevant for PIM platforms that combine product and customer data domains (MDM scope). Data residency and right-to-erasure requirements apply.

### MCP Server Specifications

**Model Context Protocol (MCP)**
- URL: https://modelcontextprotocol.io/
- Anthropic's open protocol for connecting AI models to external data sources and tools. An AI-native PIM could expose product data, taxonomy structures, and enrichment workflows as MCP servers, enabling LLM agents to query product information, trigger enrichment tasks, and validate data quality rules programmatically. Relevant for the AI enrichment layer of an AI-native PIM.

---

## Similar Products — Developer Documentation & APIs

### Akeneo Product Cloud

- **Description:** Leading purpose-built PIM/PXM platform for mid-market and enterprise. API-first architecture; the REST API is the primary integration surface.
- **API Documentation:** https://api.akeneo.com/
- **API Reference:** https://api.akeneo.com/api-reference-index.html
- **OpenAPI Spec:** Available as JSON/YAML download from api.akeneo.com (OpenAPI 3.1 for SaaS)
- **SDKs/Libraries:** Official PHP client; community JavaScript/Python/Ruby clients via GitHub (akeneo/pim-api-docs)
- **Developer Guide:** https://api.akeneo.com/documentation/introduction.html
- **Standards:** REST/JSON; OpenAPI 3.1; OAuth 2.0 (client credentials); webhook events
- **Authentication:** OAuth 2.0 client credentials grant; API key for legacy CE

### Pimcore

- **Description:** Open-source PIM/MDM/DAM/CDP/CMS platform. GraphQL via DataHub is the primary headless integration surface; REST endpoints for custom development.
- **API Documentation:** https://docs.pimcore.com/platform/Datahub/
- **GraphQL Documentation:** https://docs.pimcore.com/platform/Datahub/GraphQL/
- **REST API Guide:** https://docs.pimcore.com/platform/2024.2/Pimcore/Best_Practice/Building_Custom_Rest_APIs/
- **SDKs/Libraries:** Community PHP SDK; third-party connectors; pimcore/data-hub GitHub repository
- **Developer Guide:** https://pimcore.com/docs
- **Standards:** GraphQL (webonyx/graphql-php); REST/JSON; OAuth 2.0; AGPL core licence
- **Authentication:** API key; OAuth 2.0 for SaaS; session-based for admin UI

### Salsify

- **Description:** Product experience management (PXM) platform with direct syndication to 1,500+ retail partners. Developer API enables product, record, and workflow integrations.
- **API Documentation:** https://developers.salsify.com/
- **SDKs/Libraries:** MuleSoft Certified Salsify Connector; community integrations
- **Developer Guide:** https://developers.salsify.com/
- **Standards:** REST/JSON; webhook events; OpenAPI spec available; microservices architecture
- **Authentication:** OAuth 2.0; API key scoped per organisation

### inRiver

- **Description:** B2B and manufacturing-focused PIM with strong supplier onboarding. REST API v2 exposes the full iPMC data model and business logic.
- **API Documentation:** https://community.inriver.com/hc/en-us/articles/360023123453-Inriver-REST-API-overview
- **Developer Docs:** https://community.inriver.com/hc/en-us/categories/360003079079-developer-docs
- **SDKs/Libraries:** Official .NET SDK (strongly typed); Swagger documentation per tenant
- **Developer Guide:** inRiver Community Portal (community.inriver.com)
- **Standards:** REST/JSON; Swagger/OpenAPI; webhooks; REST API v2 (v1 deprecated as of STEP 9.2)
- **Authentication:** API key with granular permission scopes

### Stibo Systems STEP

- **Description:** Enterprise MDM/PIM platform. Exposes REST, SOAP, and GraphQL APIs across multiple API product families (STEP Web API, PDX Channel API, Extension API).
- **API Documentation:** https://doc.stibosystems.com/ and https://channel-docs.pdx.stibosystems.com/
- **SDKs/Libraries:** STEP.py (community Python client); MuleSoft STEP API connector; Extension API (Java plugin framework)
- **Developer Guide:** https://doc.stibosystems.com/doc/version/2025.2/web/
- **Standards:** REST/JSON; SOAP; GraphQL; OpenAPI; MuleSoft AnyPoint compatible
- **Authentication:** OAuth 2.0; API key; SAML for enterprise SSO

### Contentserv

- **Description:** Cloud-native PIM/PXM platform for omnichannel publishing. REST API with inbound and outbound channel endpoints.
- **API Documentation:** https://api.contentserv.com/ and https://help.contentserv.com/documentation/api-documentation
- **SDKs/Libraries:** MuleSoft Contentserv connector (works.integration/contentserv-api)
- **Developer Guide:** https://api.contentserv.com/documentation/general
- **Standards:** REST/JSON; REST Webservice Manager for custom endpoint configuration
- **Authentication:** OAuth 2.0; API key

### GS1 US Data Hub APIs

- **Description:** The GS1 US API suite allows programmatic lookup and management of GTIN, GLN, and company prefix data against the global GS1 registry. Eight APIs: Product, Location, Company, GRP GetAll, Licenses GetAll, MyProduct, Unlimited (Solution Partners), and Order (Channel Partners).
- **API Documentation:** https://www.help.gs1us.org/api-documentation
- **Developer Portal Guide:** https://documents.gs1us.org/adobe/assets/deliver/urn:aaid:aem:b91e282f-2d95-4e37-b9db-05e31cd263bc/gs1-us-data-hub-api-developer-portal-user-guide.pdf
- **Standards:** REST; OData; OpenAPI
- **Authentication:** API key subscription (flat fee of USD 6,500/year add-on); "Try It" sandbox in Developer Portal

### ECLASS Web API

- **Description:** RESTful JSON API for retrieving ECLASS classification classes, properties, and IRDI-keyed concepts. Enables automated product classification and attribute mapping in PIM integrations.
- **API Documentation:** https://eclass.eu/support/technical-specification/data-model/-eclass-webservice
- **Technical Specification:** https://eclass.eu/fileadmin/Redaktion/pdf-Dateien/Wiki/ECLASS-Technica-Specification_ItemDataRetrieval-by-RESTful_Web_API_-_V2.0.pdf (TS-48)
- **SwaggerHub:** Published at SwaggerHub (linked from eclass.eu developer documentation)
- **Standards:** REST/JSON; JSON Schema validation; RDF (TS-110 for linked data output)
- **Authentication:** API key (ECLASS membership required for full access)

### ETIM International API

- **Description:** REST API providing direct access to the full ETIM classification model (product classes, features, allowed values). Complemented by ETIM xChange, the new JSON-based file exchange format (released February 2024).
- **API Documentation:** https://www.etim-international.com/classification/exchange-format/
- **ETIM xChange Spec:** https://www.etim-international.com/classification/exchange-format/ (JSON schema included)
- **Standards:** REST/JSON; JSON Schema (ETIM xChange); BMEcat XML (legacy)
- **Authentication:** ETIM membership access

---

## Notes

**Emerging Standard: Asset Administration Shell (AAS)**
The AAS is the digital twin data model underpinning the EU DPP and the German Plattform Industrie 4.0 initiative. While not yet mainstream in PIM tooling, PIM platforms targeting heavy manufacturing and DPP compliance will need to support AAS serialisation (XML, JSON, or RDF) as DPP mandates take effect from 2026 onwards. The AAS specification is maintained by the Industrial Digital Twin Association (IDTA) at https://www.idtaconsortium.com/.

**Convergence of JSON Formats**
ETIM xChange (2024), ECLASS JSON API, GS1 Web Vocabulary (JSON-LD), and OAS 3.1 (JSON Schema 2020-12) all converge on JSON as the canonical exchange format for product data. A modern AI-native PIM should adopt JSON as its internal data model and external API format, with JSON Schema for attribute validation and JSON-LD for semantic interoperability.

**MCP Integration Opportunity**
No existing PIM platform exposes an MCP server interface. An AI-native PIM that exposes product search, enrichment triggers, and data quality APIs as MCP tools would enable LLM-driven autonomous enrichment agents — a differentiated capability not yet available in any incumbent product.
