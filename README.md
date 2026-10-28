# pkfare-api-schema

Java 25 bindings for the PKFARE SEARCH API, generated from
`src/main/resources/SEARCH_SCHEMA.yaml` using the existing OpenAPI Generator
7.14.0 Maven setup and Jackson serialization.

## Build

Use JDK 25 and Maven (or `./mvnw`):

```shell
mvn clean install
```

Generation runs during `generate-sources`. Sources are written to
`target/generated-sources/openapi/src/main/java/com/verteil/schema/pkfare` and
compiled into `target/pkfare-api-schema-1.2.0-SNAPSHOT.jar`. Generated sources
stay under `target/`; edit the schema rather than the generated Java files.

## Use from another repository

After local installation, add:

```xml
<dependency>
    <groupId>com.verteil.schema</groupId>
    <artifactId>pkfare-api-schema</artifactId>
    <version>1.2.0-SNAPSHOT</version>
</dependency>
```

The entry models are `com.verteil.schema.pkfare.SearchRequest` and
`com.verteil.schema.pkfare.SearchResponse`. Nested models have explicit names
such as `SearchFlight`, `SearchTicket`, and `SearchPrice`.
Jackson dependencies are supplied transitively. Consumers need Java 25 or later.
For other machines, publish with the existing CodeArtifact deployment workflow
and configure the consumer's repository access and credentials. A GitHub push
alone does not publish a Maven dependency. Deployment settings are unchanged.

## Schema notes

The vendor's JSON fields, required lists, types, and examples are preserved.
Inline schema titles provide stable Java model names without changing JSON.
OpenAPI validation is enabled during generation. Monetary `number` properties
use the generator's existing `BigDecimal` mapping; date strings retain PKFARE's
specified string representation.

The supplied request descriptions for `tag` and `returnTagPrice` appear reversed
relative to the introductory documentation and example. Confirm their semantics
with PKFARE before integration; neither field has been changed here.

Release tags use `pkfare-api-schema-<version>` and the existing release/deploy
workflow publishes to the configured CodeArtifact repositories.
