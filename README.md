# Portfolio1
Rebeccas 1st portfolio

#Programmes Service
Overview
The programmes service is used to return the list of available loyalty programmes and to validate any programme numbers entered for a specific loyalty programme.

Some programmes have more extensive checksum validation, but most are only validated against a regex pattern.

Web clients
Web clients will use this new service.

Mobile Clients
Mobile clients will use the existing endpoints for now.

Documentation
Full Documentation is available on Confluence

Service Endpoints
Name	Method	URL
getLoyaltyProgrammes	GET	/api/loyalty/v1/programmes
validateProgrammeNumber	POST	/api/loyalty/v1/programmes/{code}/{ffn}/validate
actuator health	GET	/api/loyalty/v1/programmes/actuator/health
actuator info	GET	/api/loyalty/v1/programmes/actuator/info
Error Codes
422 (UNPROCESSABLE ENTITY) HTTP code is sent to the client if provided FFN is invalid

Error code	Message
001	Unrecognized loyalty programme
002	Invalid loyalty programme number
003	This is not a recognized Frequent Flyer Number
004	The guest name does not match the account member name
005	Generic error code (for unexpected exceptions)
Error meaning are described here

Swagger
The swagger json file can be found in /swagger/schema/swagger.json
This should be updated whenever changes are made to the service contract.
Online Swagger documentation can be found at - http://localhost:9002/swagger-ui/ (Note: the last / is important)

Deployments
Please see Deployment scripts for Programmes Service to create an environment for the programmes service.

Monitoring
AWS CloudWatch is used to monitor this service.

The log streams, log groups, metrics, dashboards and alerts for the programmes service are all created from terraform scripts in the infrastructure-modules repo so they should be consistent across all dev and prod environments.

The documentation for CloudWatch Monitoring can be found here

Source Control
BitBucket

programmes - Contains the programmes service code and packer scripts
infrastructure-modules - Terraform scripts to build the infrastructure for the programmes services and parameter store values
infrastructure-environments - Atlantis scripts to deploy the infrastructure to different environments.
Branching Strategy
This service uses the Scaled Trunk Based Development Branching Strategy

Versions
Version	Description
1.0.0	Initial release
1.0.1	updated publish plugin version
1.0.2	checkstyle and pmd fixes
1.0.3	README update
Environments
Environment	Service Endpoint	Mobile API Gateway Service Endpoint	Health Endpoint	Info Endpoint
Local	http://localhost:9002/api/loyalty/v1/programmes	N/A	http://localhost:9002/api/loyalty/v1/programmes/actuator/health	http://localhost:9002/api/loyalty/v1/programmes/actuator/info
DEV J1	https://www-devj1.aerlingus.com/api/loyalty/v1/programmes		https://www-devj1.aerlingus.com/api/loyalty/v1/programmes/actuator/health	https://www-devj1.aerlingus.com/api/loyalty/v1/programmes/actuator/info
UAT	https://www-uatx2.aerlingus.com/api/loyalty/v1/programmes		https://www-uatx2.aerlingus.com/api/loyalty/v1/programmes/actuator/health	https://www-uatx2.aerlingus.com/api/loyalty/v1/programmes/actuator/info
STG	https://www-stg.aerlingus.com/api/loyalty/v1/programmes		https://www-stg.aerlingus.com/api/loyalty/v1/programmes/actuator/health	https://www-stg.aerlingus.com/api/loyalty/v1/programmes/actuator/info
PROD	https://www.aerlingus.com/api/loyalty/v1/programmes		https://www.aerlingus.com/api/loyalty/v1/programmes/actuator/health	https://www.aerlingus.com/api/loyalty/v1/programmes/actuator/info
Build Information
Requirements
Java 11
Gradle 6+
Springboot 2.2.5.RELEASE
Jenkins
The Jenkins job can be found here

Sonar
Sonar Analysis is available here

Artifactory
The snapshot artefacts can be found on Artifactory here, and the release artefacts here

Coding Standards
The following tools are implemented as part of the coding standards for this service.

Checkstyle
Checkstyle rules are applied to this service.
No Checkstyle violations are permitted

PMD
PMD rules are applied to this service.
No PMD violations are permitted

JaCoCo
Java Code Coverage rules are applied to this service.
The minimum coverage must be 80%

Testing
Automated Tests
The automated tests for loyalty can be found here

SoapUI
N/A
