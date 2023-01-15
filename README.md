# Keycloak SPID providers configuration client
A NodeJS client to automatically configure a Keycloak instance already setup with [keycloak-spid-provider plugin](https://github.com/italia/keycloak-spid-provider)

* downloads metadata for [all 10 official SPID IdPs](https://registry.spid.gov.it/assets/data/idp.json) and creates related Keycloak configuration along with [mappers](https://github.com/italia/spid-keycloak-provider/wiki/Mapping-SPID-attributes)
* creates Keycloak configuration for AgID SPID Demo Validator (https://demo.spid.gov.it/validator)
* creates Keycloak configuration for AgID SPID Validator (for accreditamento) (https://validator.spid.gov.it)
* creates Keycloak configuration for a local [spid-saml-check](https://github.com/italia/spid-saml-check) instance
<img width="1179" alt="image" src="https://user-images.githubusercontent.com/2743637/212466689-d32dd3a6-7374-46c3-9bf5-ac5e33fe467c.png">

<img width="1169" alt="image" src="https://user-images.githubusercontent.com/2743637/212466914-c59f9ba1-bf89-4cd6-86d1-809b45b76f53.png">

## Requirements
Docker or `node` and `npm`

## Configuration
```
npm install
```

copy `.env-example` to `.env`, configure it and wipe out the comments then

## Running the tool
```
npm run create-idps
```

If you want to have official AgID SPID Demo Validator (https://demo.spid.gov.it/validator) enabled, set the following `.env` file properties

```
createSpidDemoIdP = true 
```

If you want to have official AgID SPID Validator (https://validator.spid.gov.it) enabled, set the following `.env` file properties

```
createSpidValidatorIdP = true 
``` 

If you have a local [spid-saml-check](https://github.com/italia/spid-saml-check) instance, set the following `.env` file properties

```
createSpidTestIdP = true 
spidTestIdPAlias = spid-saml-check
spidTestIdPMetadataURL = https://localhost:8443/metadata.xml
```

## Authentication flow
By default, the new IdPs are created with a SPID-specific Authentication Flow, as per https://github.com/italia/spid-keycloak-provider/wiki/Configuring-the-Authentication-Flow - this is named `First Broker Login (SPID)` (ref. [idpmodel.json#L11](https://github.com/nicolabeghin/keycloak-spid-provider-configuration-client/blob/master/template/idpmodel.json#L11)) and must be created before running the client.

<img width="1455" alt="image" src="https://user-images.githubusercontent.com/2743637/212534098-d6add32d-db1b-4c63-b203-f37f78fee8f9.png">


## Credits
* forked from https://github.com/GermanoGiudici/keycloak-spid-provider-configuration-client (kudos to @GermanoGiudici)
* this project is released under the Apache License 2.0, same as the main Keycloak package.
