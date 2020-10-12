

# Table of Contents
1. [Adversarial ML 101](/adversarial-ml-101.md)
2. [Why Adversarial ML Threat Matrix?](#why-adversarial-ml-threat-matrix)
3. [Structure of Adversarial ML Threat Matrix](#structure-of-adversarial-ml-threat-matrix)
4. [Things to keep in mind before you use the framework](#things-to-keep-in-mind-before-you-use-the-framework)
5. [Contributors](#contributors)
6. [Feedback and Contact Information](#feedback)
7. [Adversarial ML Threat Matrix](#adversarial-ml-threat-matrix)
8. [Case Studies Page](#case-studies-page)
    - [ClearviewAI Misconfiguration](#clearviewai-misconfiguration)
    - [GPT-2 Model Replication](#gpt-2-model-replication)
    - [ProofPoint Evasion](#proofpoint-evasion)
    - [Tay Poisoning](#tay-poisoning)
    - [Microsoft Red Team Exercise](#microsoft-red-team-exercise)
    - [Bosch Team Experience with EdgeAI ](#bosch-team-experience-with-edgeai)
    - [MITRE -- Physical Adversarial Examples -- TBD](#mitre-physical-adversarial-examples-tbd)
---- 

The goal of this project is to position attacks on ML systems in an ATT&CK-style framework so that security analysts can orient themselves
in this new and upcoming threats.

## Why Adversarial ML Threat Matrix? 
1.  In the last three years, major companies such as [Google](https://www.zdnet.com/article/googles-best-image-recognition-system-flummoxed-by-fakes/), [Amazon]           (https://www.fastcompany.com/90240975/alexa-can-be-hacked-by-chirping-birds), [Microsoft](https://www.theguardian.com/technology/2016/mar/24/tay-microsofts-ai-         chatbot-gets-a-crash-course-in-racism-from-twitter), and [Tesla](https://spectrum.ieee.org/cars-that-think/transportation/self-driving/three-small-stickers-on-         road-can-steer-tesla-autopilot-into-oncoming-lane), have had their ML systems tricked, evaded, or misled.
2.  This trend is only set to rise: According to [Gartner report](https://www.gartner.com/doc/3939991). 30% of cyberattacks by 2022 will involve data poisoning, model     theft or adversarial examples.
3.  However, industry is underprepared. In a [survey](https://arxiv.org/pdf/2002.05646.pdf) of 28 organizations spanning small as well as large organizations, 25           organizations did not know how to secure their ML systems.

Unlike traditional cybersecurity vulnerabilities that are tied to specific software and hardware systems, adversarial ML vulnerabilities are enabled by inherent limitations underlying ML algorithms. As a result, data can now be weaponized in new ways requiring that we extend the way we model cyber adversary behavior, reflecting emerging threat vectors and the rapidly evolving adversarial machine learning attack lifecycle.

This threat matrix came out of partnership with 12 industry and academic research groups with the goal of empowering security analysts to orient themselves in this new and upcoming threats. **We are seeding this framework with a curated set of vulnerabilities and adversary behaviors that Microsoft and MITRE have vetted to be effective against production ML systems** Since the primary audience is security analysts, we used ATT&CK as template to position attacks on ML systems given its popularity and wide adoption in the industry.

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

## Things to keep in mind before you use the framework:
1.  This is a **first cut attempt** at collating known adversary techniques against ML Systems. We plan to iterate on the framework based on feedback from the security     and adversarial machine learning community (please engage with us and help make the matrix better!). Net-Net: This is a *living document* that will be routinely       updated.
2.  Only known bad is listed in the Matrix. Adversarial ML is an active area of research with new classes constantly being discovered. If you find a technique that is     not listed, please enlist it in the framework (see section on Feedback)
3.  We are not prescribing definitive defenses at this point - The world of adversarial. We are already in conversations to add best practices in future revisions such     as adversarial training for adversarial examples, restricting the number of significant digits in confidence score for model stealing.
4.  This is not a risk prioritization framework - The Threat Matrix only collates the known techniques; it does not provide a means to prioritize the risks.

## Contributors

Want to get involved? See [Feedback and Contact Information](#feedback)

| **Organization**    | **Contributors**    |
| :---                | :---                |
| Microsoft           | Ram Shankar Siva Kumar, Hyrum Anderson, Will Pearce, Suzy Shapperle, Blake Strom, Madeline Carmichael, Matt Swann, Nick Beede, Kathy Vu, Andi Comissioneru, Sharon Xia, Mario Goertzel, Jeffrey Snover, Abhishek Gupta  |
| MITRE               | Mikel D. Rodriguez, Christina E Liaghati, Keith R. Manville, Michael R Krumdick |
| Bosch               | Manojkumar Parmar |
| IBM                 | Pin-Yu Chen       |
| NVIDIA              | David Reber Jr., Keith Kozo, Christopher Cottrell, Daniel Rohrer |
| Airbus              | Adam Wedgbury     |
| Deep Instinct       | Nadav Maman       |
| TwoSix              | David Slater      |
| University of Toronto | Adelin Travers, Jonas Guan, Nicolas Papernot |
| Cardiff University  | Pete Burnap |
| Software Engineering Institute/Carnegie Mellon University | Nathan M. VanHoudnos | 
| Berryville Institute of Machine Learning | Gary McGraw, Harold Figueroa, Victor Shepardson, Richie Bonett|

## Feedback and Contact Information
The Adversarial ML Threat Matrix is a first-cut attempt at collating a knowledge base of how ML systems can be attacked. We need your help to make it holistic and fill in the missing gaps!

Please submit a Pull Request with suggested changes! We are excited to make this system better with you!

**Join our Adversarial ML Threat Matrix Google Group**

- For discussions around Adversarial ML Threat Matrix, we invite everyone to join our Google Group [here](https://groups.google.com/forum/#!forum/advmlthreatmatrix/join)
- If you want to access this forum using your corporate email (as opposed to your gmail)
  - Open your browser in Incognito mode.
  - Once you sign up with your corporate, and complete captcha, you may
  - Get an error, ignore it!
-   Also note, emails from Google Forums generally go to "Other"/"Spam"
    folder. So, you may want to create a rule to go into your inbox
    instead

**Want to work with us on the next iteration of the framework?**
- We are partnering with Defcon's AI Village to open up the framework to all community members to get feedback and make it better. Current thinking is to have this event circa
- Jan/Feb 2021.
    -   Please register here for the workshop for more hands on feedback
        session
 
 **Contact Information**
-   If you have questions/comments that you'd like to discuss privately,
    please email: <Ram.Shankar@microsoft.com> and <Mikel@mitre.org>

## Adversarial ML Threat Matrix 
Interactive Version to be built by MITRE. For Editable version, contact <Ramk@Microsoft.com>

## Case Studies Page
We chose **real world attacks on production ML systems** based on:
1.  Range of Attacks: evasion, poisoning, model replication and exploiting traditional software flaws.
2.  Range of Personas: Average user, Security researchers, ML Researchers and Fully equipped Red team
3.  Range of ML Paradigms: Attacks on MLaaS, ML models hosted on cloud, hosted on- presmise, ML models on edge
4.  Range of Use case: Attacks on ML systems used in both "security-sensitive" applications like cybersecurity and non-security-sensitive applications like chatbots

### ClearviewAI Misconfiguration 
**Summary of Incident:** Clearview AI's source code repository, though password protected, was misconfigured. This allowed an external researcher to register as a new user to the code repository and gain access to Clearview AI's credentials, keys to cloud storage buckets containing 70K video samples, copies of its applications and Slack tokens.
**Reported by:** Mossab Hussein (@mossab_hussein)

**Source:**
    - https://techcrunch.com/2020/04/16/clearview-source-code-lapse/amp/
    
**Mapping to Adversarial Threat Matrix :**
- In this scenario, a security researcher gained initial access to via a "Valid Account" that was created through a misconfiguration. No Adversarial ML techniques were used.
- these kinds of attacks illustrate that any attempt to secure ML system should be on top of "traditional" good cybersecurity hygiene such as locking down the system with least privileges, multi factor authentication and monitoring and auditing.

### GPT-2 Model Replication 
**Summary of Incident:** : OpenAI built GPT-2, a powerful natural language model and calling it "too dangerous to release" adopted a staged-release process to incrementally release 1.5 Billion parameter model. Before the 1.5B parameter model could be released by OpenAI, two ML researchers replicated the model and released it to the public. *Note this is a model replication attack: Here, attacker is able to recover functionally equivalent model (but generally with lower fidelity), perhaps to do reconnaissance (See proof point attack). In Model stealing, the fidelity of the model is comparable to the original, victim model.*

**Reported by:** Vanya Cohen (@VanyaCohen), Aaron Gokaslan (@SkyLi0n) , Ellie Pavlick, Stefanie Tellex

**Source:**
    - https://blog.usejournal.com/opengpt-2-we-replicated-gpt-2-because-you-can-too-45e34e6d36dc
    - https://www.wired.com/story/dangerous-ai-open-source/

**Mapping to Adversarial Threat Matrix :**
-   Using public documentation about GPT-2, ML researchers gathered similar datasets used during the original GPT-2 training.
-   Next, they used a different publicly available NLP model (called Grover) and modified Grover's objective function to reflect
    GPT-2's objective function,
-   The researchers then trained the modified Grover on the dataset they curated, using Grover's initial hyperparameters, which
    resulted in their replicated model.

### ProofPoint Evasion 
**Summary of Incident:** : CVE-2019-20634 describes how ML researchers evaded ProofPoint's email protection system by first building a copy-cat email protection ML model, and using the insights to evade the live system.

**Reported by:** Will Pearce (@moo_hax), Nick Landers (@monoxgas)
**Source:**
    - https://nvd.nist.gov/vuln/detail/CVE-2019-20634

**Mapping to Adversarial Threat Matrix :**
-   The researchers first gathered the scores from the Proofpoint's ML system used in email email headers .
-   Using these scores, the researchers replicated the ML mode by building a "shadow" aka copy-cat ML model
-   Next, the ML researchers algorithmically found samples that this "offline" copy cat model
-   Finally, these insights from the offline model allowed the researchers to create malicious emails that received preferrable
    scores from the real ProofPoint email protection system, hence bypassing it.

### Tay Poisoning 
 **Summary of Incident:** Microsoft created Tay, a twitter chatbot for 18- to 24- year-olds in the U.S. for entertainment purposes. Within 24 hours of its deployment, Tay had to be decommissioned because it tweeted reprehrensible words.
 
 **Source:**
    - https://blogs.microsoft.com/blog/2016/03/25/learning-tays-introduction/

**Mapping to Adversarial Threat Matrix :**
-   Tay bot used the interactions with its twitter users as training data to improve its conversations.
-   Average users of Twitter coordinated together with the intent of defacing Tay bot by exploiting this feedback loop
-   As a result of this coordinated attack, Tay's training data was poisoned which led its conversation algorithms to generate more reprehensible material

### Microsoft Red Team Exercise 
**Summary of Incident:** : The Azure Red Team and Azure Trustworthy ML team performed a red team exercise on an internal Azure service with the intention of disrupting its service

**Reported by:** Azure TrustworthyML Team (<atml@microsoft.com>), Azure Red Team
**Mapping to Adversarial Threat Matrix :**
-   The team first performed reconnaissance to gather information about the target ML model
-   Then, using a valid account the team found the model file of the target ML model and the necessary training data
-   Using this, the red team performed an offline evasion attack by methodically searching for adversarial examples
-   Via an exposed API interface, the team performed an online evasion attack by replaying the adversarial examples, which helped achieve this goal.
-   This operation had a combination of traditional ATT&CK enterprise techniques such as finding Valid account, and Executing code via an API -- all interleaved with adversarial ML specific steps such as offline and online evasion examples.

### Bosch Team Experience with EdgeAI 
**Summary of Incident:** : Bosch team performed a research exercise on an internal edge AI system with a dual intention to extract the model and craft adversarial example to evade
**Reported by:** Manoj Parmar (@mparmar47)
**Mapping to Adversarial Threat Matrix :**
-   The team first performed reconnaissance to gather information about the edge AI system device working with sensor interface
-   Then, using a trusted relationship mechanism between sensor and edge ai system team fed synthetic data on sensor to extract the model
-   Using this, the team performed an offline evasion attack by crafting adversarial example with help of extracted model
-   Via an exposed sensor interface, the team performed an online evasion attack by replaying the adversarial examples, which helped achieve this goal.
-   This operation had a combination of traditional ATT&CK industrial control system techniques such as supply chain compromise via sensor, and Executing code via sensor interface. all interleaved with adversarial ML specific steps such as,
  - offline and online evasion examples.
- The team was also able to reconstruct the edge ai system with extracted model

### MITRE Physical Adversarial Examples
- TBD 
