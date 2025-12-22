# Email Security Baseline — redavalanche.io

## Scope
Defines the minimum authentication, alignment, and reporting posture for mail that uses redavalanche.io in the From header. Applies to first-party infrastructure and any third-party sender asserting the domain.

## Baseline Controls
### SPF (Sender Policy Framework)
SPF records in DNS declare the authorized sending infrastructure for redavalanche.io. Evaluation uses the envelope identity (MAIL FROM/HELO) to determine whether the source is permitted to transmit on behalf of the domain.

### DKIM (DomainKeys Identified Mail)
DKIM provides cryptographic signing of outbound messages. Selectors identify key material published in DNS, and signatures attest to message integrity and authorized use of the signing domain. All legitimate senders are expected to sign with a domain aligned to redavalanche.io.

### DMARC (Domain-based Message Authentication, Reporting, and Conformance)
DMARC defines receiver handling based on SPF/DKIM alignment with the From domain and provides aggregate/forensic reporting for visibility into legitimate and abusive sources.

## DMARC Observation Posture
The initial DMARC policy is configured as p=none to enable monitoring without impacting delivery. This observation window allows enumeration of legitimate sources, identification of alignment gaps, and measurement of spoofing activity prior to enforcement.

## Validation
Baseline validation is met when authorized mail demonstrates SPF and/or DKIM pass with alignment to redavalanche.io, DMARC evaluates to pass for legitimate flows, and successful delivery/authentication is observed in Microsoft Outlook headers and user experience.

## Operational Notes
Authorized senders must be represented by aligned SPF and/or DKIM. DMARC reporting is treated as security telemetry for Purple Team and CTI analysis of unauthorized sources, misalignment, and spoofing trends.
