---
title: "Router Solicitation Option for Manufacturer Usage Description (MUD) URLs"
abbrev: "MUD NDP Option"
category: std

docname: draft-romann-mud-ndp-latest
submissiontype: IETF
consensus: true
v: 3
keyword: Internet-Draft
author:
 -
    fullname: Jan Romann
    organization: University of Bremen
    email: jan.romann@uni-bremen.de
    country: Germany

normative:

informative:


--- abstract

The document specifies a new IPv6 Router Solicitation option
for emitting Manufacturer Usage Descriptions (MUDs, RFC 8520) URLs.
This simplifies the integration of MUD into environments that primarily use
IPv6.

--- middle

# Introduction

Note: Everything here is still WIP.

Manufacturer Usage Descriptions (MUDs) {{!RFC8520}} can be used to describe
the kind of network access a device needs in order to properly function.
This information can be used to reduce the attack surface of a network, e.g.
by applying a corresponding firewall configuration that prohibits all traffic.
MUD nodes are supposed to indicate which MUD file describes them by emitting
a URL that is processed by a so-called MUD manager.

Devices that operate in Internet of Things (IoT) primarily rely on IPv6 due to
the scarcity of IPv4 addresses vis-à-vis a rapidly growing number of devices
and the use of IPv6 in constrained environments via protocols such as 6LoWPAN.
Although {{!RFC8520}} specifies a DHCPv6 {{?RFC8415}} option that can be used by
IPv6 devices for emitting their MUD URL, IPv6 addresses are most commonly
assigned via Stateless Address Autoconfiguration (SLAAC) {{?RFC4862}} using the
Neighbor Discovery Protocol (NDP) {{!RFC4861}} and not via DHCPv6.
This renders many IoT devices uncapable of using a standardized way for
emitting MUD URLs if they are not employing an out-of-band solution such as the
emission via a QR code {{?RFC9238}}.
<!-- TODO: Also mention LLDP and X.509 certificates -->

To potentially close this gap, this document proposes a new NDP option which
can be used in Router Solicitation (RS) messages.
This enables IPv6 nodes to emit their MUD URLs more easily when using SLAAC.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

This document makes use of the terms defined in {{!RFC8520}}]. The
   following additional terms are used: TBD

# Option Format

~~~~
0                   1
0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|      Type     |    Length   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             |
+          MUDstring          |
|                             |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+

Fields:

Type:                   TBD1

Length:                 8-bit unsigned integer. Contains the
                        length of the MUDstring in octets.

MUDstring:              String containing a MUD URL as defined
                        in section 10 of RFC 8520.
                        MUST NOT exceed 254 Bytes.
~~~~
{: #fig-ndp-mud title='MUD URL Option' align="left"}


# Security Considerations

TODO Security


# IANA Considerations

IANA is requested to assign the following new IPv6 Neighbor Discovery Option
type in the "IPv6 Neighbor Discovery Option Formats" sub-registry under the
"Internet Control Message Protocol version 6 (ICMPv6) Parameters" registry.

| Type |   Description  |    Reference   |
|:----:|:--------------:|:--------------:|
| TBA1 | MUD URL Option | [ThisDocument] |

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
