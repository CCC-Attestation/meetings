# Workload Identity and Remote Attestation

The evolving regulatory environment coupled with a steady stream of high-profile and costly breaches is leading enterprises and regulators alike to focus on securing and governing deployed workloads. An increasingly pressing need in enterprise IT is being able to securely authenticate workloads to each other and controlling which workloads can access what data. This need has been recognized and a variety of approaches are competing for adoption and viability, such as the [SPIFFE/SPIRE architecture](https://spiffe.io/docs/latest/architecture/), the [WIMSE working group at the IETF](https://www.ietf.org/blog/wimse-working-group/) and others.

While it is quite clear that for the foreseeable future this need is not going to be met by Confidential Computing alone, the security features related to workload identification and isolation offered by Confidential Computing eclipse other approaches. Confidential Computing will not be first to market, and thus will need to evolve to fit within, and ideally serve as the North Star of workload identity as it becomes a foundational pillar of trustworthy and governable enterprise computing. Remote Attestation plays a key role in workload identification in Confidential Computing and it is thus critically important to architect it in a way that best fits within the workload identity space.

The workload identity problem space can be defined by the following set of key scenarios and requirements:

1. Any two workloads, WA and WB, should be able to obtain identities WIA and WIB, use these identities to obtain credentials WCA and WCB, and authenticate each other using these credentials. The identities, credentials and authentication/authorization mechanisms in question must all be portable, standards-based, and capable of supporting transport-level and application-level scenarios, as well as federation.
2. There has to exist a strong binding between an identity of a workload and its lineage, such that one workload cannot impersonate another.
   * In case of workloads developed in-house, integration of workload identity with CI/CD mechanisms is highly desirable
   * In case of managed workloads or workloads obtained from trusted sources, other forms of lineage establishment can be used, with automation and accountability remaining key features
   * Both code identity and the configuration/environment in which the code is deployed are important in workload identity establishment; the environment may include attributes such as whether the code is deployed in test or production, what physical location the computation takes place in, and others
3. The credentials, once issued to a workload, must be strongly bound to the workload’s instance in order to minimize the chances of a credential being leaked and repurposed.
   * For this to work, the use of bearer tokens must be strongly discouraged
   * Obtaining cryptographic keys for identity or credential establishment from secret stores comes with the need for workload key management, and is thus less desirable than having each workload generate and certify its own short-lived keys
4. The workloads can be deployed in a variety of environments:
   * On-premises
   * In the public cloud
   * On remotely managed IoT devices
   * On users’ personal devices
5. The workloads can take a wide variety of shapes:
   * Virtual machines, including but not limited to confidential virtual machines
   * Various incarnations of container-based workloads (in AWS that might include Fargate, EKS and ECS)
   * Confidential Computing enclaves
   * Serverless computing
   * Cloud and on-premises services such as database services, queueing services and the like
   * Managed services, including SaaS products
6. Workloads might be standalone or compound (compound workloads being those consisting of multiple components that share the same lifetime from deployment through to decommissioning and potentially spanning devices or having components residing on the same physical device)
7. A workload may have multiple distinct credentials issued to it, e.g., for purposes of inbound, outbound and internal (component-to-component for compound workloads) authentication
8. Workloads might be short- or long-lived with different requirements applied to each kind:
   * For short-lived workloads, typified by container and serverless workloads, it may be important to issue credentials quickly and reliably so as not to introduce performance and reliability penalties related to multiple and/or expensive round-trips involved in credential issuance
   * For long-lived workloads, the lifetime of a workload is likely to exceed that of the credentials issued to it, requiring ability to renew and/or revoke credentials in response to governance requirements and/or emerging threats without compromising overall system reliability
9. Governance of workload identities and credentials must include some of the following capabilities:
   * Maintaining control over and a history of all policies and decisions involved in issuing and evaluating identities and credentials
   * Ability to identify, isolate and remedy vulnerable workloads in production quickly, such as when new threats are discovered or new attacks detected
	
So what does all that mean to Confidential Computing style Remote Attestation?

1. There must be a set of easy to adopt mechanisms and patterns that use Remote Attestation in workload credential issuance, where the issued Workload Credentials are interoperable with those utilized by the rest of the workload identity ecosystem. As such, the interplay between RATS-style Remote Attestation and industry standard identity providers and credential issuance mechanisms has to be investigated, documented and supported — across all Verifier implementations.
2. While Remote Attestation mechanisms have access to the information needed to establish the lineage of attesting workloads, the mechanisms for binding this lineage to issued workload credentials need to be defined.
3. Workloads ought to be able to both generate and certify their own keys, or obtain keys/credentials from secret key stores. The role of Remote Attestation in both of those cases has to be precisely defined and widely supported.
4. Remote Attestation-based workload credential issuance has to be supported on a wide variety of computing platforms and mechanisms, including serverless and managed workloads, as well as solutions that do not strictly follow Confidential Computing “hardware-based” tenets, such as AWS Nitro.
5. Remote Attestation mechanisms for compound workloads must be defined, including both compound workloads deployed on a single device (e.g., CPU + GPU + Smart NIC) and multiple devices (K8S pods/services, auto-scaling compute instances behind a load balancer, compound workloads spanning devices yet sharing a lifetime, etc.)
6. Credential issuance, re-issuance and revocation mechanisms may need to be optimized differently for short-lived and long-lived workloads.
7. Governance of Remote Attestation and workloads themselves must follow the governance patterns being defined by (and in collaboration with) the Governance SIG.
	
