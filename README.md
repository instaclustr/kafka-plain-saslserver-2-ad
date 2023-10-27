# kafka-ldap-integration

[![Gradle build](https://github.com/ultratendency/kafka-ldap-integration/actions/workflows/gradle.yml/badge.svg)](https://github.com/ultratendency/kafka-ldap-integration/actions/workflows/gradle.yml)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=ultratendency_kafka-ldap-integration&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=ultratendency_kafka-ldap-integration)

Enhancing kafka 3.x with
- customized SimpleLDAPAuthentication using LDAPS simple bind for authentication
- In release 1.1.0 we have had support for authorization which is compatible to Kafka 2.8.1 
- The authorization feature was removed due to incompatibilites with latest Kafka versions (3.0 onwards) starting with release 1.2.0.

Thus, moving authentication from user and passwords in JAAS context file on kafka brokers to LDAP server

Binding and group membership information is cached (limited lifetime after write),
giving minor performance penalty and reduced LDAPS traffic.

## Tools
- Kotlin
- Gradle build tool
- Spek test framework

## Components

1. Unboundid LDAP SDK for LDAPS interaction
2. Caffeine Cache
3. YAML Configuration for LDAP baseDN for users, groups and more. See `src/test/resources/ldapconfig.yaml` for details

**N.B.** that the directory hosting yaml configuration file must be in CLASSPATH.

## Quickstart

A tutorial with configuration examples is available in the [User Guide](docs/index.md).

## Build

```shell
./gradlew clean build shadowJar
```

### Build without unit tests

```shell
./gradlew clean build shadowJar -x test
```

The result is `build/libs/kafka-ldap-integration-<version>.jar`, which contains the authentication classes, along with all of their dependencies.

**N.B.** This jar must be added to the classpath for the Kafka broker. The easist way to do that is to copy the jar into the directory `$KAFKA_HOME/libs`.

### Contact us

#### Credit to original authors

Maintainers of the GitHub project [kafka-ldap-integration](https://github.com/instaclustr/kafka-ldap-integration):
* Joe Schmetzer, `joe.schmetzer@instaclustr.com`
* Zeke Dean, `zeke.dean@instaclustr.com`

Maintainers of the GitHub project [kafka-plain-saslserver-2-ad](https://github.com/navikt/kafka-plain-saslserver-2-ad):
* Torstein Nesby, `torstein.nesby@nav.no`
* Trong Huu Nguyen, `trong.huu.nguyen@nav.no`
