---
title: "Additional Authentication Method Reference Values"
abbrev: "Additional AMR Values"
category: std

docname: draft-skyfire-oauth-amr-values-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
#number:
date:
consensus: true
v: 3
# area: AREA
# workgroup: TODO
keyword:
 - agent
 - identity
 - agentic
 - payment
 - commerce
venue:
  github: "skyfire-xyz/draft-skyfire-oauth-amr-values"
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  latest: "https://skyfire-xyz.github.io/draft-skyfire-oauth-amr-values/draft-skyfire-oauth-amr-values.html"

author:
-
  name: Ankit Agarwal
  organization: Skyfire Systems Inc.
  email: ankit_agarwal@yahoo.com
  uri: https://skyfire.xyz
-
  ins: M. Jones
  name: Michael B. Jones
  organization: Self-Issued Consulting
  email: michael_b_jones@hotmail.com
  uri: https://self-issued.info/

normative:
  RFC8176:

informative:
  RFC7519:
  OpenID.Core:
    target: https://openid.net/specs/openid-connect-core-1_0.html
    title: "OpenID Connect Core 1.0 incorporating errata set 2"
    date: 2023-12-15
    author:
      - name: Nat Sakimura
      - name: John Bradley
      - name: Michael B. Jones
      - name: Breno de Medeiros
      - name: Chuck Mortimore
  IANA.AMR:
    author:
    - name: IANA
    target: https://www.iana.org/assignments/authentication-method-reference-values
    title: Authentication Method Reference Values

...

--- abstract

The JWT "amr" (Authentication Methods References) claim
contains values conveying authentication methods used in the authentication.
This specification defines additional Authentication Method Reference values
beyond those already registered to represent additional
authentication methods in use today.

--- middle

# Introduction

The JWT {{RFC7519}} "amr" (Authentication Methods References) claim {{OpenID.Core}}
contains values conveying authentication methods used in the authentication.
They are registered in the
IANA "Authentication Method Reference Values" registry {{IANA.AMR}}.

Since the Authentication Method Reference Values {{RFC8176}}
specification was published, several new authentication methods have been developed
and/or come into widespread use.
This specification defines additional Authentication Method Reference values
to represent these additional
authentication methods in use today.

While these Authentication Method Reference values are general purpose
and can be used in any JSON Web Token (JWT) {{RFC7519}},
one use case for them is use in KYAPay tokens {{?I-D.skyfire-oauth-kyapay-token}}.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Authentication Method Reference Values {#amrValues}

The following Authentication Method Reference values
are defined by this specification:

## "app" (Authenticator App) Method {#appMethod}

app:
: Authenticator App (e.g., Okta Verify, Google Authenticator, Microsoft Authenticator)

## "inp" (In-person Authentication) Method {#inpMethod}

inp:
: In-person Authentication

## "vid" (Video Authentication) Method {#vidMethod}

vid:
: Video Authentication (live video interview)

## "bg" (Background Authentication) Method {#bgMethod}

bg:
: Background Authentication (Silent network authentication of phone number, device recognition, geo-location, etc.)

## "email" (Code or link sent to e-mail) Method {#emailMethod}

email:
: Use of code or link sent to e-mail

## "push" (Push notification to mobile phone) Method {#pushMethod}

push:
: Push notification to mobile phone


# Security Considerations

The security considerations defined in
Authentication Method Reference Values {{RFC8176}}
apply to this specification.


# Privacy Considerations

The privacy considerations defined in
Authentication Method Reference Values {{RFC8176}}
apply to this specification.


# IANA Considerations

## Authentication Method References Registry {#ivmRegistry}

This specification registers the following
Authentication Method Reference values in the
IANA "Authentication Method Reference Values" registry {{IANA.AMR}}
established by {{RFC8176}}.

### "app" Method

* Authentication Method Reference Name: app
* Authentication Method Reference Description: Authenticator App
* Change Controller: IETF
* Specification Document(s): (#appMethod) of this specification

### "inp" Method

* Authentication Method Reference Name: inp
* Authentication Method Reference Description: In-person Authentication
* Change Controller: IETF
* Specification Document(s): (#inpMethod) of this specification

### "vid" Method

* Authentication Method Reference Name: vid
* Authentication Method Reference Description: Video Authentication
* Change Controller: IETF
* Specification Document(s): (#vidMethod) of this specification

### "bg" Method

* Authentication Method Reference Name: bg
* Authentication Method Reference Description: Background Authentication
* Change Controller: IETF
* Specification Document(s): (#bgMethod) of this specification

### "email" Method

* Authentication Method Reference Name: email
* Authentication Method Reference Description: Code or link sent to e-mail
* Change Controller: IETF
* Specification Document(s): (#emailMethod) of this specification

### "push" Method

* Authentication Method Reference Name: push
* Authentication Method Reference Description: Push notification to mobile phone
* Change Controller: IETF
* Specification Document(s): (#pushMethod) of this specification


--- back

# Document History
{: numbered="false"}

[[ to be removed by the RFC Editor before publication as an RFC ]]

-00

* Initial draft.
