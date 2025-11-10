# TheProtocols 4.0

**Editor’s Draft — Work in Progress**

**This version:** 4.0<br>
**Latest published version:** 4.0<br>
**Previous version:** 3.1<br>
**Editor:** Cagan Mert ISLEK [hello@islekcaganmert.me](mailto:hello@islekcaganmert.me)

**Contributors:**
Cagan Mert ISLEK [hello@islekcaganmert.me](mailto:hello@islekcaganmert.me)

**Status:** *Draft*<br>
**Publication Date:** --/--/----<br>
**Version:** 4.0<br>
**Test Suite:** *Not yet available*<br>
**Implementation Report:** *Not yet available*<br>

## Abstract

*TheProtocols* defines a federated communication and computation framework designed to **decentralize super applications** by enabling users to select both the network and the client of their preference. TheProtocols provides an extensible base for identity, session, data, and app management across independently administered networks, supporting both consumer-grade and enterprise-level applications.

The protocol defines interoperable object formats and transport mechanisms, intended to support the core functionality that a typical user requires in daily digital activity.

## Status of This Document

This section describes the status of this document at the time of its publication. Other documents, as published officially by the TheProtocols Foundation, may supersede this document.

This document is an **Editor’s Draft** of *TheProtocols 4.0*. It is under active development and subject to substantial change. Implementers **MUST NOT** rely on this version for production systems without providing a compatible fallback mechanism.

All interested parties are invited to submit implementation reports, issues, and suggestions via the public issue tracker, the Fediverse, or email at [hello@islekcaganmert.me](mailto:hello@islekcaganmert.me).

Future updates will reflect implementer feedback and formal testing.

## Introduction

TheProtocols defines a federated, extensible standard for building and interconnecting modular super applications. Its goal is to offer the interoperability and openness while enabling rich and secure app-level communication without a centralized authority.

TheProtocols consists of a Remote Procedure Call standard and multiple submodules under the `org.theprotocols` namespace, each addressing a distinct area.

## Dependencies

This specification relies on the following technologies and formats:

* **JSON [RFC8259]**
* **URI [RFC3986]**
* **HTTPS [RFC2818]**
* **ISO 8601** for date and time formats

All timestamps and durations defined in this specification **MUST** be expressed in **UTC**.

## Terminology

The key words **MUST**, **MUST NOT**, **REQUIRED**, **SHOULD**, **SHOULD NOT**, **RECOMMENDED**, **MAY**, and **OPTIONAL** in this document are to be interpreted as described in [RFC2119].

## Conformance

A conformant implementation of TheProtocols:

* **MUST** fully implement all required behaviors described by its corresponding module (`org.theprotocols.*`).
* **MAY** extend the base specification through additional namespaces, provided extensions do not alter core semantics.
* **MUST** ensure interoperability across federated deployments through correct use of identifiers and activity types.
* **SHOULD** maintain backward compatibility with prior stable releases where applicable.
* **MUST** represent all temporal data in **UTC**.

Conformance requirements apply equally to both servers and clients unless otherwise specified.

## Definitions

* **Word** — Definition

## Table of Contents

* [0.1. URI Format](a_00_core/01_uri_format.md)
* [0.2. Permissions](a_00_core/02_permissions.md)
* [0.3. Remote Procedure Calls](a_00_core/03_rpc.md)
* [1. Network](a_01_network/README.md)
* [2. Session](a_02_session/README.md)
* [3. Apps](a_03_apps/README.md)


## External Namespaces

TheProtocols allows different namespaces to be introduced by third party implementers. Any external namespace **MAY** have their documentation added **IF** the namespace is intended for network-side federation. However, implementers **MUST NOT** expect these namespaces to exist in all networks even though all networks **SHOULD** implement as much namespaces as possible.

- `net.*`
  - [HereUS SDK (`net.hereus.sdk.*`)](e_net.hereus.sdk/README.md)
