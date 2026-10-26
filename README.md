# vietjet-api-schema

This repository contains the Schema bindings for VietJet APIs, generated from the VietJet API Gateway OpenAPI specification.

You can find the schema in **_`src/main/resources`_**.

## Prerequisites

* Java 25
* Maven 3.5.0 or later

## Build

To build the VietJet API Schema, run the following command:

```shell

mvn clean install

```

## Usage

To use the VietJet API Schema, add the following dependency to your project:

### Gradle

```groovy

implementation 'com.verteil.schema:vietjet-api-schema:artifact-version^'

```

### Maven

```xml

<dependency>
    <groupId>com.verteil.schema</groupId>
    <artifactId>vietjet-api-schema</artifactId>
    <version>artifact-version^</version>
</dependency>

```

###### ** ^ Replace with latest artifact version**

## Schema Customizations

`src/main/resources/SEARCH_SCHEMA.yaml` is VietJet's API Gateway OpenAPI spec, with the changes below.
VietJet's spec leaves several properties untyped (`type: object`) or typed incorrectly, so the generated
models expose `Object` / the wrong type. These changes give them proper types.
When updating the spec from VietJet, check whether each change is still needed and re-apply it.

| Ticket | Model | Property | Original | Changed to | Reason |
|--------|-------|----------|----------|------------|--------|
| POD-38395 | `ReservationPassengerModel` | `infants` | array of `type: object` | array of `ReservationPassengerInfantModel` | Typed infant details on passengers |
| POD-38389 | `ReservationModel` | `charges` | array of `type: object` | array of `ReservationChargeModel` | Typed reservation charges (fare/tax breakdown) |
| POD-38389 | `AncillaryOptionsModel` | `ancillaryCharges` | single `AncillaryChargesModel` | array of `AncillaryChargesModel` | VJ returns a list, not a single object |
| POD-38389 | `AncillaryChargesModel` | `description` | `type: object` | `type: string` | VJ returns a plain string |
| POD-38389 | `ReservationPassengerJourneyDetailModel` | `cabinClass` | _(missing)_ | `CabinClassModel` | Property returned by VJ but missing from the spec |
