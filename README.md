# Meeting Materials

| Date | Track | Presentation | Presenter | Materials |
| --- | --- | --- | --- | --- |
| 2022-04-26 | <button class="l tls">secure channel establishment</button> | HTTPA | Hans Wang | <ul><li>MISSREF slides</li><li>[APNIC blog](https://blog.apnic.net/2022/01/17/httpa-seeks-to-improve-https-trust-issues/)</li><li>[paper](https://arxiv.org/pdf/2110.07954.pdf)</li></ul> |
| 2022-04-26 | <button class="l tls">secure channel establishment</button> | TLS + CWT | [Hannes Tschofenig](@hannestschofenig) | <ul><li>[slides](materials/HannesTschofenig_TLS-CWT.pdf)</li><li>[IETF draft](https://datatracker.ietf.org/doc/draft-tschofenig-tls-cwt/)</li></ul> |
| 2022-04-12 | <button class="l tls">secure channel establishment</button> | Veracruz Attestation | [Derek Miller](@dreemkiller) | <ul><li>MISSREF slides</li></ul> |
| 2022-04-12 | <button class="l tls">secure channel establishment</button> | CloudProxy | [Tom Roeder](@tmroeder) | <ul><li>[original technical report for CloudProxy](https://www2.eecs.berkeley.edu/Pubs/TechRpts/2013/EECS-2013-135.html)</li><li>[datalog-based guard code](https://github.com/jlmucb/cloudproxy/blob/master/go/tao/datalog_guard.go#L40)</li><li>[listener code](https://github.com/jlmucb/cloudproxy/blob/master/go/tao/listener.go#L27)</li></ul> |
| 2022-03-29 | <button class="l tls">secure channel establishment</button> | OpenEnclave Attested TLS | Andy Chen | <ul><li>MISSREF slides</li><li>[sample code](https://github.com/openenclave/openenclave/tree/master/samples/attested_tls)</li></ul> |
| 2022-03-29 | <button class="l tls">secure channel establishment</button> | Formal analysis of Enclave Key Exchange Protocol (EKEP) | [Tom Roeder](@tmroeder) | <ul><li>[ProVerif model](https://github.com/google/ekep-analysis)</li><li>[protocol spec](https://asylo.dev/docs/concepts/ekep.html)</li></ul> |
| 2022-03-15 | <button class="l tls">secure channel establishment</button> | RA-TLS & Gramine | [Dmitrii Kuvaiskii](@dimakuv) | <ul><li>MISSREF slides</li><li>[docs](https://graminereadthedocs.io/en/latest/attestation.html#mid-level-ra-tls-interface)</li></ul> |
| 2022-03-15 | <button class="l tls">secure channel establishment</button> | STET: Split-Trust Encryption Tool | [Keith Moyer](@KeithMoyer) | <ul><li>[code](https://github.com/GoogleCloudPlatform/stet)</li></ul> |
| 2021-10-26 | <button class="l std">emerging standards</button> | CoRIM update | [Thomas Fossati](@thomas-fossati) | <ul><li>[slides](materials/ThomasFossati_CoRIM_update.pdf)</li></ul> |
| 2021-06-22 | <button class="l std">emerging standards</button> | Entity Attestation Token (EAT) | [Laurence Lundblade](@laurencelundblade) | <ul><li>[slides](materials/LaurenceLundblade_EAT.pdf)</li></ul> |
| 2021-06-08 | <button class="l std">emerging standards</button> | Concise Reference Integrity Manifests (CoRIM) | [Thomas Fossati](@thomas-fossati) | <ul><li>[slides](materials/ThomasFossati_CoRIM.pdf)</li></ul> |
| 2021-05-25 | <button class="l oss">open source components</button> | Veraison intro | [Simon Frost](@SimonFrost-Arm) | <ul><li>[slides](materials/SimonFrost_Veraison.pdf)</li></ul> |
| 2021-04-27 | <button class="l std">emerging standards</button> | Attestation Results for Secure Interactions (AR4SI)| [Eric Voit](@ericvoit) | <ul><li>[slides](materials/EricVoit_AttestationResults.pdf)</li></ul> |


<style>
.l {
  border: none;
  color: white;
  text-align: center;
  margin: 4px 2px;
}

.std { background-color: #E99872; }
.oss { background-color: #008CBA; }
.tls { background-color: #4CAF50; }
</style>