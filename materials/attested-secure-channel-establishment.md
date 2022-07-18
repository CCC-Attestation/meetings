# Attested Secure Channel Establishment

When establishing secure channels, attestation evidence can be used to enhance
the *quality* of authentication of the protocol principals' by providing their
peers information about:

* The identity and security state of the environment in which the principal
  executes;
* The security of the identity key used in the authenticated key
  exchange -- e.g., whether it is HW protected, kept in the TEE, or in insecure
  memory.

In our survey of "attested" secure channel establishment (SCE) implementation,
we have identified four different design patterns.  These patterns can be
categorised based on the different layering of the attestation, SCE and
application channels.

The four approaches are as follows:

1. Extend the SCE protocol by introducing attestation-related information
elements to the base vocabulary, creating an "attested" version of the base SCE.
Examples include EKEP and TLS+CWT.

```
     ------------------------------

 app

     ------------------------------
            .-------------.   
 SCE        | attestation |
            '-------------'
     ------------------------------
```


1. First establish a secure channel using an unmodified SCE protocol, then
export the negotiated session key material to the layer on top and use it to
protect an attestation protocol session.  There is typically some binding
between the two layers, for example STET uses the exported key material to feed
the attestation challenge.

```
     ------------------------------
            .-------------.   
 app        | attestation |
            '------o------'
     --------------|---------------
                   |
 SCE              sek

     ------------------------------
```

1. Tunnel attestation evidence through the same X.509 credentials that are used
to authenticate the secure channel.  The advantage of this approach is that
X.509 is ubiquitous and extensible.  Besides, since it tends to be orthogonal to
the core key agreement mechanics of the SCE, there are usually well-defined callback
points that can be (re)used to inject validation logics that are
attestation-specific.  Examples of this category include RA-TLS, OpenEnclave
attested TLS and .  Another example is DICE - both its TCG and Open variants.

```
     ------------------------------

 app

     ------------------------------
          .=================.
          | .-------------. | 
 SCE      | | attestation | |
          | '-------------' |
          '======X.509======'
     ------------------------------
```

1. A variant of the X.509 tunnelling approach described above is the one used by
Veracruz and Cloudproxy, which mint attested identities and embed them,
alongside the attestation evidence that was use in support of the enrolment, in
X.509 certs extensions.  These can be seen as a special form of attestation
results that morphs into a usable identity.

```
     ------------------------------

 app

     ------------------------------
          .=================.
          | .-------------. | 
 SCE      | | attested ID | |
          | '-------------' |
          '======X.509======'
     ------------------------------
```
