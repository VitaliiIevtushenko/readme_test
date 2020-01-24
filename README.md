# Finance Manager
Provides a mechanism for digitally managing invoices, PODs and payment in one place.

* Reduced paper-based management of invoices and PODs
* Reduction in outstanding payments due to delay in reconciliation of documents
* Simplified and improved workflow for users
* Improved visibility of bookings missing documents

## Prerequisites

* JDK 8
* Redis
* Kafka broker
* PostgreSQL
* Apache Maven
* Git
* Docker ([installation instruction for Ubuntu](https://www.digitalocean.com/community/tutorials/docker-ubuntu-16-04-ru))

## Getting Started

```
git clone https://github.com/transport-exchange-group/cx-financial-manager.git
```

#### Create Database
```
sudo -u postgres psql
create database "cxfinancialmanagerdb";
\q
```
or
```
CREATE DATABASE cxfinancialmanagerdb WITH ENCODING='UTF8' OWNER=postgres CONNECTION LIMIT=-1;
```
#### Configure properties

```properties
# Database
spring.datasource.url=jdbc:postgresql://[host]:[port]/[dbname]
spring.datasource.username=[username]
spring.datasource.password=[password]

# Certificates location
auth.publicKeyPath=[path/name].der
auth.privateKeyPath=[path/name].der

# Redis
spring.redis.host=[host]
spring.redis.port=[port]
spring.redis.password=[password]

# Kafka
spring.cloud.stream.kafka.binder.brokers=[host]:[port]

# System email
communication.email=[email]
communication.email.password=[password]

# Attachments service private API
attachments-service.private.api.url=[url]
attachments-service.private.api.username=[username]
attachments-service.private.api.password=[password]

# CX-REST service private API
cx-rest.private.api.url=[url]
cx-rest.private.api.username=[username]
cx-rest.private.api.password=[password]

# PDF-converter private API
pdf-converter.private.api.url=[url]
pdf-converter.private.api.username=[username]
pdf-converter.private.api.password=[password]
```
 
 ## API
 
 * [Private API documentation](http://stage-cx.transportexchange.co.uk/fm/doc/swagger-ui.html)
 * [Public API documentation](https://app.ardas.ua/wiki/display/TEGCXNA/Finance+Manager#FinanceManager-API)

## Versioning

For the versions available, see the [tags on Docker Hub](https://hub.docker.com/repository/docker/tegr/cx-financial-manager). 

* [Get current version (Stage)](https://dev-cx.transportexchange.co.uk/fm/version)
* [Get current version (Live)](https://live-us.transportexchangegroup.com/fm/version)

## Authors

* Natallia Osaula (BA)
* Vitaliy Evtushenko
* Dmitriy Zhadenov

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## Links

* [TEG documentation](https://transportexchangegroup.atlassian.net/wiki/spaces/TPD/pages/287965217/Finance+Application)
* [Ardas documentation](https://app.ardas.ua/wiki/display/TEGCXNA/Finance+Manager)
* [Web site (Stage)](https://dev-productportal.transportexchange.co.uk/finance/overview)
* [Web site (Live)](https://productportal.transportexchangegroup.com/finance/overview)

## Donations
This [contributors](https://github.com/your/project/contributors) have been already paid. But if you really enjoy this project or would like to say thanks for this one, you are always welcome)))
