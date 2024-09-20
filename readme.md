# Introduction

The current repository defines the configuration of the [GeoJSON validator](https://www.itb.ec.europa.eu/json/geojson/upload) provided by the [Interoperability Test Bed](https://joinup.ec.europa.eu/collection/interoperability-test-bed-repository/solution/interoperability-test-bed),
that allows validation of JSON objects against the [GeoJSON specification](https://geojson.org/). This validator is a configuration of the Test Bed's [JSON validator](https://github.com/ISAITB/json-validator).

The service is accessible:
* Via UI at https://www.itb.ec.europa.eu/json/geojson/upload
* Via REST API at https://www.itb.ec.europa.eu/json/swagger-ui/index.html (use "geojson" when prompted for a "domain")
* Via SOAP API at https://www.itb.ec.europa.eu/json/soap/geojson/validation?wsdl

# Configuration

The validator's configuration is located under `resources`, and specifically within file `config.properties`. Any changes merged to this repository result in the live service being updated within 1-2 minutes.

Note that the JSON Schemas responsible for the validation are provided as remote references. These are refreshed automatically every hour without
requiring a validator restart.

# Running your own validator

You can replicate this validator on your own environment by following these steps:
1. Clone the current repository (in e.g. `MY_LOCAL_REPO`).
2. Start a new JSON validator instance by using the [isaitb/json-validator](https://hub.docker.com/r/isaitb/json-validator) Docker image, and providing the `resources` folder as the validator's resource root.

```
docker run -d --name my-validator -p 8080:8080 \
             -v /MY_LOCAL_REPO/resources:/validator/resources/ \
             -e validator.resourceRoot=/validator/resources/  \
             -e validator.domainName.resources=geojson
             isaitb/json-validator
```

Using the above command your validator will be available:
* Via UI at http://localhost:8080/json/geojson/upload
* Via REST API: http://localhost:8080/json/swagger-ui/index.html (use "geojson" when prompted for a "domain")
* Via SOAP API: http://localhost:8080/json/soap/geojson/validation?wsdl

# Licence

This configuration is shared using the [European Union Public Licence (EUPL) version 1.2](https://joinup.ec.europa.eu/sites/default/files/custom-page/attachment/eupl_v1.2_en.pdf).

# Legal notice

The authors of this repository and the resulting validator waive any and all liability linked to its usage or the interpretation of its results. In terms of data, the resulting validator does not harvest, collect or process in any way data that could be linked to the user or 
workstation.

# Contact

To get in touch for feedback or questions please send an email to [DIGIT-ITB@ec.europa.eu](mailto:DIGIT-ITB@ec.europa.eu).

