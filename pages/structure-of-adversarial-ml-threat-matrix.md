## Structure of Adversarial ML Threat Matrix
Because it is fashioned after [ATT&CK Enterprise](https://attack.mitre.org/matrices/enterprise/), the Adversarial ML Threat Matrix retains the terminologies: for instance, the column heads of the Threat Matrix are called "Tactics" and the individual entities are called "Techniques".

However, there are two main differences:

1.  ATT&CK Enterprise is generally designed for corporate network which is composed of many sub components like workstation, bastion hosts, database, network gear,         active directory, cloud component and so on. The tactics of ATT&CK enterprise (initial access, persistence, etc) are really a short hand of saying initial access       to *corporate network;* persistence *in corporate network.* In Adversarial ML Threat Matrix, we acknowledge that ML systems are part of corporate network but           wanted to highlight the uniqueness of the attacks.

    **Difference:** In the Adversarial ML Threat Matrix, the "Tactics" should be read as "reconnaissance of ML subsystem", "persistence in ML subsystem", "evading the      ML subsystem"

2.  When we analyzed real-world attacks on ML systems, we found out that attackers can pursue different strategies: Rely on traditional cybersecurity technique only;       Rely on Adversarial ML techniques only; or Employ a combination of traditional cybersecurity techniques and ML techniques.
  
    **Difference:** In Adversarial ML Threat Matrix, "Techniques" come in two flavors:
        -   Techniques in orange are specific to ML systems
        -   Techniques in white are applicable to both ML and non-ML systems and come directly from Enterprise ATT&CK

        Note: The Adversarial ML Threat Matrix is not yet part of the ATT&CK matrix.


