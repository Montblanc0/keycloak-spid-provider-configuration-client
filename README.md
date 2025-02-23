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
Copy `.env-example` to `.env`, configure it and wipe out the comments
If you want to have official AgID SPID Demo Validator (https://demo.spid.gov.it/validator) enabled, set the following `.env` file properties

```
createSpidDemoIdP = true 
```

If you want to have official AgID SPID Validator (https://validator.spid.gov.it) enabled, set the following `.env` file properties

```
createSpidValidatorIdP = true 
``` 

If you have a local [spid-saml-check](https://github.com/italia/spid-saml-check) instance, set the following `.env` file properties (make sure that Keycloak can reach the `spidTestIdPMetadataURL` and is trusting its PEM certificate)

```
createSpidTestIdP = true 
spidTestIdPAlias = spid-saml-check
spidTestIdPMetadataURL = https://localhost:8443/metadata.xml
```

If you also want to import the demo validator idp from your local spid-saml-check instance, set the following `.env` file properties (make sure that Keycloak can reach the `spidTestDemoIdPMetadataURL` and is trusting its PEM certificate)

```
createSpidTestDemoIdP = true
spidTestDemoIdpMetadataURL = https://localhost:8443/demo/metadata.xml
```

## Running the tool
### Docker
Easiest way by leveraging Docker:

    make

### Without Docker
If you have NodeJS installed 
```
npm install
npm run create-idps
```

## Authentication flow
By default, the new IdPs are created with a SPID-specific Authentication Flow, as per https://github.com/italia/spid-keycloak-provider/wiki/Configuring-the-Authentication-Flow - which should be named `first broker login - SPID` (ref. [idpmodel.json#L11](https://github.com/Montblanc0/keycloak-spid-provider-configuration-client/blob/master/template/idpmodel.json#L11)) and must be created before running the client.

<img width="1455" alt="image" src="https://i.ibb.co/NgYbZ2Dv/first-broker-login-SPID-config.png">

## SPID access button integrated in Keycloak theme
https://github.com/nicolabeghin/keycloak-spid-provider-configuration-client/wiki/SPID-access-button-integrated-in-Keycloak-theme
<img width="285" alt="image" src="https://user-images.githubusercontent.com/2743637/212535193-aae9e8ce-b4f1-4411-9811-def46419bacf.png">

## Credits
* forked from https://github.com/nicolabeghin/keycloak-spid-provider-configuration-client (kudos to @nicolabeghin and @GermanoGiudici)
* this project is released under the Apache License 2.0, same as the main Keycloak package.
