---
v: 3

title: Fair Share Cost Token
abbrev: Fair Share Cost Token
docname: draft-bransky-scitt-fsct-latest
category: std
consensus: true
submissionType: IETF

area: "Security"
workgroup: "Supply Chain Integrity, Transparency, and Trust"
keyword: [ evidence, attestation results, endorsements, reference values ]


author:
 - name: Gregor Bransky
   organization: Please fill in
   email: Please fill in
 - name: Henk Birkholz
   organization: Fraunhofer SIT
   email: henk.birkholz@ietf.contact

contributor:
 - name: Carsten Bormann
   contribution: Carsten supplied some text and helped with the kramdown-rfc mechanics.

# This will be thinned considerably in the next round:

normative:
  RFC3986: uri
  RFC4648: base64
  RFC5280: pkix
  RFC5912: pkix-mods
  RFC6268: more-pkix-mods
  RFC6838: media-types
  STD90: json # RFC8259
  RFC8610: cddl
  RFC9165: cddlplus
  RFC9741: cddlplusplus
  RFC9277:
  RFC9334: rats-arch
  STD94: cbor # RFC8949
  IANA.cwt:
  IANA.jwt:
  BCP26: ianacons # RFC8126
  X.680: CCITT.X680.2002
  X.690: CCITT.X690.2002

informative:
  RFC3647: pkix-cps
  RFC7942: impl-status
  RFC9193: senml-cf
  STD96: cose # RFC9052
  RFC9711: rats-eat
  RFC9782: rats-eat-mt
  I-D.ietf-rats-ear: rats-ear
  RFC9781: rats-uccs
  I-D.fossati-tls-attestation: tls-a1
  I-D.fossati-seat-expat: tls-a2
  I-D.ietf-lamps-csr-attestation: csr-a
  I-D.ietf-rats-corim: rats-corim
  DICE-arch:
    author:
      org: "Trusted Computing Group"
    title: "DICE Attestation Architecture"
    target: https://trustedcomputinggroup.org/wp-content/uploads/DICE-Attestation-Architecture-Version-1.1-Revision-18_pub.pdf
    date: January, 2024
  RFC8792:

entity:
  SELF: "RFCthis"

--- abstract

Software suppliers often use hundreds, if not thousands of open source
packages in their products.
To ensure that there is a well-defined supply chain, suppliers often
want to create a working relationship with the creators of each of
the open source packages.
To enable donations, the transaction cost must be very low, which may be
supported using a solution based on Supply Chain Integrity,
Transparency, and Trust (scitt) tokens.
Specifically, Fair Share Cost Tokens (FSCT) provide some forensic
readiness in case there is a dispute about whether the supplier bore
their fair share of the cost of keeping the open source product safe
and secure.

--- middle

# Introduction

[^intro]

[^intro]: An intro giving a very high level, informal overview of that
    FSCTs do.  This will employ images like this one:

~~~ aasvg
                            .------------.
                            |  Verifier  |
                            '------------'
                                ^
                                | EAT
                                | over
                                | REST API
.------------.              .---|--------.
|  Attester  +------------->|--'      RP |
'------------' EAT over TLS '------------'
~~~
{: #topo-1 artwork-align="center"}

## Conventions and Definitions

{::boilerplate bcp14-tagged}

In this document, CDDL {{-cddl}} {{-cddlplus}} {{-cddlplusplus}} is used to describe the
data formats.

The reader is assumed to be familiar with the vocabulary and concepts
defined in {{-rats-arch}}.

# Actors and Objectives

# Secure Realizations of Process

# Implementation Status
{:removeinrfc}

[^rfced] Please remove the entire section before publication, as well as the reference to RFC 7942.

This section records the status of known implementations of the protocol
defined by this specification at the time of posting of this Internet-Draft,
and is based on a proposal described in {{-impl-status}}.
The description of implementations in this section is intended to assist the
IETF in its decision processes in progressing drafts to RFCs.
Please note that the listing of any individual implementation here does not
imply endorsement by the IETF.
Furthermore, no effort has been spent to verify the information presented here
that was supplied by IETF contributors.
This is not intended as, and must not be construed to be, a catalog of
available implementations or their features.
Readers are advised to note that other implementations may exist.

According to {{-impl-status}}, "this will allow reviewers and working groups to
assign due consideration to documents that have the benefit of running code,
which may serve as evidence of valuable experimentation and feedback that have
made the implemented protocols more mature.
It is up to the individual working groups to use this information as they see
fit".

## (To be added)

# Privacy Considerations {#privcons}


[^discuss]

The privacy considerations outlined in {{Section 11 of -rats-arch}} are fully applicable.
In particular, ...

# Security Considerations {#seccons}

The security considerations discussed in {{Section 12.2 of -rats-arch}} concerning the protection of individual messages are fully applicable.
The following subsections provide further elaboration ...

# IANA Considerations

[^rfced] Please replace "{{&SELF}}" with the RFC number assigned to this document.

[^rfced] This document uses the CPA (code point allocation) convention described in {{?I-D.bormann-cbor-draft-numbers}}. For each usage of the term "CPA", please remove the prefix "CPA" from the indicated value and replace the residue with the value assigned by IANA; perform an analogous substitution for all other occurrences of the prefix "CPA" in the document. Finally, please remove this note.

## CWT Claim Registrations {#iana-cwt}

## Media Types {#iana-mt}

--- back

# Registering and Using FSCTs

[^appendix]

[^appendix]: Possible appendices with explanatory (non-normative)
    information, with more nice figures.


~~~ aasvg
     .---------------.   .---------.
    | Reuse EAT/CoRIM | | Register  |
    | media type(s)   | | new media |
    | + profile       | | type      |
     `---+----+------'   `-+----+--'
         |    |            |    |
         |  .-+------------+-.  |
         | |  |  Register  |  | |
       .-(-+-'   new CoAP   `-+-(-.
      |  | |  Content-Format  | |  |
      |  |  `-------+--------'  |  |
      |  |          |           |  |
      |  |          v           |  |
      |  |   .--------------.   |  |
      |  |  | Automatically  |  |  |
      |  |  | derive CBOR    |  |  |
      |  |  | tag [RFC9277]  |  |  |
      |  |   `------+-------'   |  |
      |  |          |           |  |
      |  |          |           |  |
      |  |          |           |  |
      |  |          v           |  |
      |  |   .----------------. |  |
      |  |  /    Tag CMW     /  |  |
      v  v `----------------'   v  v
  .--------------------------------------.
 /             Record CMW               /
`--------------------------------------'
~~~
{: #fig-howto-cmw artwork-align="center"
   title="How To Create a CMW"}

# Open Issues
{: removeinrfc}

The list of currently open issues for this document can be found at
[](https://github.com/cabo/fsct/issues).

# Acknowledgments
{: unnumbered}

The authors would like to thank
{{{Lots o. Names}}},
{{{We n. to find}}}
and
{{{Someone Else}}}
for their reviews and suggestions.

[^note]: Note:
[^issue]: Open issue:
[^rfced]: RFC Editor:

[^discuss]: Discuss.
