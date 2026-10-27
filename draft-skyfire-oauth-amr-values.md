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
area: Security
workgroup: Web Authorization Protocol
updates: 8176
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
-
  name: Nash Ali
  organization: Experian
  email: nash.ali@experian.com
-
  name: Srinivasa Thumma
  organization: Akamai
  email: sthumma@akamai.com

normative:
  RFC8176:

informative:
  RFC4226:
  RFC4949:
  RFC6238:
  RFC7519:
  I-D.skyfire-oauth-kyapay-token:
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
    - org: IANA
    target: https://www.iana.org/assignments/authentication-method-reference-values
    title: Authentication Method Reference Values
    date: false
  WebAuthn:
    target: https://www.w3.org/TR/2026/REC-webauthn-3-20260825/
    title: "Web Authentication: An API for accessing Public Key Credentials - Level 3"
    author:
      - name: Tim Cappalli
      - name: Akshay Kumar
      - name: Emil Lundberg
      - name: Matthew Miller
      - name: Pascoe
      - name: Nina Satragno
    date: 2026-08-25
    seriesinfo:
      W3C: Recommendation
  ISO30107-1:
    target: https://www.iso.org/standard/83828.html
    title: "Information technology - Biometric presentation attack detection - Part 1: Framework"
    author:
      - org: International Organization for Standardization
    date: 2023
    seriesinfo:
      "ISO/IEC": "30107-1:2023"
  NIST.SP.800-63B-4:
    target: https://pages.nist.gov/800-63-4/sp800-63b.html
    title: "Digital Identity Guidelines: Authentication and Authenticator Management"
    author:
      - org: National Institute of Standards and Technology
    date: 2025-08
    seriesinfo:
      "NIST Special Publication": "800-63B-4"
  CAMARA.NumberVerification:
    target: https://github.com/camaraproject/NumberVerification
    title: "Number Verification API, version 2.1.0"
    author:
      - org: CAMARA Project
    date: 2025

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
one use case for them is use in KYAPay tokens {{I-D.skyfire-oauth-kyapay-token}}.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Authentication Method Reference Values {#amrValues}

The following Authentication Method Reference values
are defined by this specification:

## "app" (Authenticator App) Method {#appMethod}

{:vspace}
app:
: Use of an authenticator application on a device held by the user.
  An issuer includes this value where it knows that an authenticator application was used.
  Where a code is produced from a shared secret
  and the issuer cannot determine what produced it,
  this value is omitted.

  An authenticator application commonly acts as an OTP authenticator
  or as an out-of-band authenticator,
  as described in Sections 3.1.3 to 3.1.5 of {{NIST.SP.800-63B-4}}.

## "bg" (Background Authentication) Method {#bgMethod}

{:vspace}
bg:
: Background Authentication (Silent network authentication of phone number, device recognition, geo-location, etc.)

  The "sna" value ({{snaMethod}}) identifies one specific background method
  and is a subset of this value.
  Geo-location is separately registered as "geo"
  and device recognition is within the scope of "rba",
  both in {{RFC8176}}.

## "sna" (Silent Network Authentication) Method {#snaMethod}

{:vspace}
sna:
: Silent Network Authentication.
  Confirmation by the mobile network operator that the device making the request
  holds the subscriber identity associated with a given telephone number,
  performed without any interaction with the user.
  An example is the Number Verification API {{CAMARA.NumberVerification}}.

## "email" (E-mail Channel) Method {#emailMethod}

{:vspace}
email:
: Use of e-mail as the channel by which an authentication interaction reached the user.
  What was delivered over the channel is described by an accompanying value
  such as "code" or "url".
  See {{composing}}.

  E-mail is not an acceptable channel for out-of-band authentication
  under Section 3.1.3.1 of {{NIST.SP.800-63B-4}}.
  See {{security}}.

## "code" (Code provided to and entered by user) Method {#codeMethod}

{:vspace}
code:
: Code provided to and entered by user

  For example, a secret received on an out-of-band device
  and entered into the authentication session,
  as described in Section 3.1.3 of {{NIST.SP.800-63B-4}}.

## "url" (URL provided to and clicked on by user) Method {#urlMethod}

{:vspace}
url:
: URL provided to and clicked on by user

## "push" (Push notification to mobile phone) Method {#pushMethod}

{:vspace}
push:
: Push notification to mobile phone

  An out-of-band authentication interaction in which the verifier reaches
  an application on the user's device over a secondary channel,
  as described in Section 3.1.3 of {{NIST.SP.800-63B-4}}.

## "facliv" (Facial Liveness Check) Method {#faclivMethod}

{:vspace}
facliv:
: Determination that a facial image or video presented for authentication
  is of a live person rather than an artifact
  such as a photograph, mask, or synthetic rendering.
  This is a presentation attack detection measure {{ISO30107-1}}.

  The "facliv" and "face" {{RFC8176}} values describe different determinations
  and are not alternatives:
  "face" is a comparison of a presented face against a reference,
  and "facliv" is a determination that the presented face is live.
  Where both were performed, both values are included.

## "passkey" (Passkey) Method {#passkeyMethod}

{:vspace}
passkey:
: A passkey, that is, a client-side discoverable credential as defined by {{WebAuthn}}.

## "mdc" (Multi-Device Credential) Method {#mdcMethod}

{:vspace}
mdc:
: Use of a multi-device credential as defined by {{WebAuthn}},
  that is, a backup-eligible credential,
  which may be backed up and synchronized to other devices.
  Multi-device credentials are commonly referred to as synced passkeys.
  A WebAuthn Relying Party learns whether a credential is backup eligible
  from the flags in the authenticator data.

  This value describes whether a credential may be replicated.
  It is independent of how the key is protected on any one device,
  which "hwk" and "swk" {{RFC8176}} describe.
  Where both are known, both are included.

  The absence of this value does not indicate that a credential is a single-device credential.

## "uv" (User Verification) Method {#uvMethod}

{:vspace}
uv:
: User verification.
  Local authorization of the authenticator by an authorization gesture
  capable of distinguishing individual users,
  such as a PIN, a password, or biometric recognition {{WebAuthn}}.

  This is distinct from "user" {{RFC8176}}, which is a test of user presence.
  As {{WebAuthn}} states, a user presence test
  "is not capable of biometric recognition,
  nor does it involve the presentation of a shared secret such as a password or PIN".

  This value does not identify which modality the authenticator used.


# Updated Authentication Method Reference Value {#amrUpdates}

The following Authentication Method Reference value
is updated by this specification:

## "tel" (Telephone Call) Method {#telMethod}

{:vspace}
tel:
: Telephone call to the user at a registered number.
  The call may be used to provide information to the user, such as a code, that is then used in another channel.
  The call may be used for the user to provide information that the caller uses in the authentication.

This definition replaces the one in {{RFC8176}}, which is
"Confirmation by telephone call to the user at a registered number.
This authentication technique is sometimes also referred to as
'call back' {{RFC4949}}."


# Composing Authentication Method Reference Values {#composing}

The "amr" claim value is an array, and as described in {{RFC8176}},
all the applicable values may be returned.
A single authentication event is frequently described by more than one value,
because the registered values describe different aspects of it.

The "email" and "push" values registered by this specification describe the channel by which an authentication interaction reached the person.
{{RFC8176}} registers "sms" and "tel" in the same sense,
and uses the term "channel" in this sense in its definition of "mca".

The "code" and "url" values describe challenges delivered over such a channel, which the person must return to the verifier to complete authentication.
The person may return it directly, as when a code is read and typed in,
or indirectly, as when following a link causes the value to be sent.
The "otp" value {{RFC8176}} is related but narrower:
it identifies a one-time password produced by an algorithm
such as HOTP {{RFC4226}} or TOTP {{RFC6238}},
typically generated by an authenticator rather than delivered over a channel.
A code not produced by such an algorithm is described by "code".

A channel value alone does not say what the person did.
A challenge value alone does not say how it reached them.
An issuer that knows both will typically return both.
{{examples}} gives examples, and {{compositions}} maps terms in common industry use
onto the corresponding sets of values.

The "sms" value registered by {{RFC8176}} predates this distinction.
Its definition describes both a channel and the interaction carried over it,
and is unchanged by this specification.
An issuer wishing to be explicit about what was delivered over the SMS channel
may return a challenge value alongside it.


# Security Considerations {#security}

The security considerations defined in
Authentication Method Reference Values {{RFC8176}}
apply to this specification.

E-mail is not an acceptable channel for out-of-band authentication
under Section 3.1.3.1 of {{NIST.SP.800-63B-4}},
because an e-mail account may be accessible with only a password
and messages may be intercepted or rerouted.
A relying party evaluating an "amr" claim that includes "email"
may wish to take this into account.

{{NIST.SP.800-63B-4}} also no longer accepts out-of-band authentication
in which the user approves a request on the secondary channel
without transferring a secret between the channels,
because of authentication fatigue attacks.
The "push" value alone does not indicate whether a secret was transferred.
An issuer that knows a code was transferred returns "code" alongside it.


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
* Specification Document(s): {{appMethod}} of this specification

### "bg" Method

* Authentication Method Reference Name: bg
* Authentication Method Reference Description: Background Authentication
* Change Controller: IETF
* Specification Document(s): {{bgMethod}} of this specification

### "sna" Method

* Authentication Method Reference Name: sna
* Authentication Method Reference Description: Silent Network Authentication
* Change Controller: IETF
* Specification Document(s): {{snaMethod}} of this specification

### "email" Method

* Authentication Method Reference Name: email
* Authentication Method Reference Description: Use of e-mail as the channel for an authentication interaction
* Change Controller: IETF
* Specification Document(s): {{emailMethod}} of this specification

### "code" Method

* Authentication Method Reference Name: code
* Authentication Method Reference Description: Code provided to and entered by user
* Change Controller: IETF
* Specification Document(s): {{codeMethod}} of this specification

### "url" Method

* Authentication Method Reference Name: url
* Authentication Method Reference Description: URL provided to and clicked on by user
* Change Controller: IETF
* Specification Document(s): {{urlMethod}} of this specification

### "push" Method

* Authentication Method Reference Name: push
* Authentication Method Reference Description: Push notification to mobile phone
* Change Controller: IETF
* Specification Document(s): {{pushMethod}} of this specification

### "facliv" Method

* Authentication Method Reference Name: facliv
* Authentication Method Reference Description: Facial Liveness Check
* Change Controller: IETF
* Specification Document(s): {{faclivMethod}} of this specification

### "passkey" Method

* Authentication Method Reference Name: passkey
* Authentication Method Reference Description: Passkey
* Change Controller: IETF
* Specification Document(s): {{passkeyMethod}} of this specification

### "mdc" Method

* Authentication Method Reference Name: mdc
* Authentication Method Reference Description: Multi-Device Credential
* Change Controller: IETF
* Specification Document(s): {{mdcMethod}} of this specification

### "uv" Method

* Authentication Method Reference Name: uv
* Authentication Method Reference Description: User Verification
* Change Controller: IETF
* Specification Document(s): {{uvMethod}} of this specification

### "tel" Method

* Authentication Method Reference Name: tel
* Authentication Method Reference Description: Telephone call to the user at a registered number
* Change Controller: IETF
* Specification Document(s): {{telMethod}} of this specification


--- back

# Examples {#examples}

The following "amr" claim value indicates that a code
was sent to the user over the e-mail channel and entered by the user:

~~~
"amr": ["email", "code"]
~~~

The following "amr" claim value indicates that a link
was sent to the user over the e-mail channel and followed by the user:

~~~
"amr": ["email", "url"]
~~~

The following "amr" claim value indicates that a one-time password
was generated by an authenticator application and entered by the user:

~~~
"amr": ["app", "otp"]
~~~

The following "amr" claim value indicates that a password was used
together with a code sent over the e-mail channel,
and that the issuer considers the combination to be multiple-factor authentication:

~~~
"amr": ["pwd", "email", "code", "mfa"]
~~~

# Common Compositions {#compositions}

The terms below are names in common industry use for authentication arrangements
that this specification describes using more than one value.
This mapping is non-normative.
It is provided so that implementers of the same arrangement emit the same set of values.

{:vspace}
Email one-time code, also called email OTP:
: `["email", "code"]`

Magic link, also called e-mail link sign-in:
: `["email", "url"]`

SMS one-time code:
: `["sms", "code"]`.
  As noted in {{composing}}, "sms" predates the channel and challenge distinction,
  and `["sms"]` remains correct.

Voice one-time code, where a call conveys a code that the user then enters:
: `["tel", "code"]`

Call-back confirmation, where the user confirms during the call itself:
: `["tel"]`

Authenticator application one-time password:
: `["app", "otp"]`

Push approval:
: `["push"]`

Push approval with number matching:
: `["push", "code"]`

Silent network authentication:
: `["sna"]`

Facial recognition with a liveness check:
: `["face", "facliv"]`

Device-bound passkey held in hardware, such as on a security key:
: `["passkey", "hwk"]`

Synced passkey:
: `["passkey", "mdc"]`.
  "hwk" or "swk" is added where the issuer knows how the key is protected.

# Acknowledgments
{: numbered="false"}

We would like to thank
Jean Diaconu,
Max Gerber,
and
Rob Zagarella
for their contributions to the specification.


# Document History
{: numbered="false"}

[[ to be removed by the RFC Editor before publication as an RFC ]]

-03

* Added "sna" for silent network authentication, a specific case of the background authentication described by "bg".
* Added "mdc" for multi-device credentials, commonly called synced passkeys, which composes with "hwk" and "swk" {{RFC8176}}.
* Added "uv" for user verification, distinct from the user presence test described by "user" {{RFC8176}}.
* Redefined "app" by the property it describes rather than by product examples, and stated when an issuer can assert it.
* Narrowed "email" to the channel, with what was delivered over it described by an accompanying value.
* Stated that "facliv" and "face" {{RFC8176}} describe different determinations and are included together where both were performed, and added a reference to {{ISO30107-1}}.
* Added a reference for "passkey" to {{WebAuthn}}.
* Added references to {{NIST.SP.800-63B-4}} for "app", "code", "push", and "email", and to {{CAMARA.NumberVerification}} for "sna".
* Added Security Considerations on e-mail as an authentication channel and on push approval without a transferred secret.
* Added a section on composing values, and appendices giving examples and common compositions.
* Removed "sqa". Current NIST guidance treats knowledge-based authentication and security questions as the same family, and "kba" {{RFC8176}} already covers it.
* Removed the Security Considerations note on security questions, which applied to "sqa".
* Added Max Gerber to the acknowledgments.

-02

* Updated the definition of "tel" to incorporate calls to provide information such as codes and removed "call".
* Renamed "psk" to "passkey" because of the potential confusion with pre-shared key.
* Added warning in Security Considerations that security questions are not acceptable authentication secrets under current NIST guidance.
* Added {:vspace} syntax to definition list entries.

-01

* Moved "inp" and "vid" methods to the ID Verification spec.
* Added "call", "code", "url", "facliv", "sqa", and "psk" methods.
* Added Nash Ali and Srinivasa Thumma as authors.

-00

* Initial draft.
