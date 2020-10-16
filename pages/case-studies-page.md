## Case Studies Page
Attacks on machine learning (ML) systems are being developed and released with increased regularity. Historically, attacks against ML systems have been performed in a controlled academic settings, but as these case-studies demonstrate, attacks are being seen in-the-wild. In production settings ML systems are trainined on PII, trusted to make critical decisions with little oversight, and have little to no logging and alerting attached to their use. The case-studies were selected because of the impact to a production ML systems, and each demonstrates one of the following characteristics.

1. Range of Attacks: evasion, poisoning, model replication and exploiting traditional software flaws.
2. Range of Personas: Average user, Security researchers, ML Researchers and Fully equipped Red team
3. Range of ML Paradigms: Attacks on MLaaS, ML models hosted on cloud, hosted on- presmise, ML models on edge
4. Range of Use case: Attacks on ML systems used in both "security-sensitive" applications like cybersecurity and non-security-sensitive applications like chatbots


### ClearviewAI Misconfiguration 
**Summary of Incident:** Clearview AI's source code repository, though password protected, was misconfigured to allow an arbitrary user to register an account. This allowed an external researcher to gain access to a private code repository that contained Clearview AI production credentials, keys to cloud storage buckets containing 70K video samples, and copies of its applications and Slack tokens. With access to training data, a bad-actor has the ability to cause an arbitrary misclassificaion in the deployed model. 

**Reported by:** Mossab Hussein (@mossab_hussein)

**Source:**
    - https://techcrunch.com/2020/04/16/clearview-source-code-lapse/amp/
    
**Mapping to Adversarial Threat Matrix :**
- In this scenario, a security researcher gained initial access to via a "Valid Account" that was created through a misconfiguration. No Adversarial ML techniques were used.
- these kinds of attacks illustrate that any attempt to secure ML system should be on top of "traditional" good cybersecurity hygiene such as locking down the system with least privileges, multi factor authentication and monitoring and auditing.

    <img src="/images/ClearviewAI.png" alt="ClearviewAI" width="300" height="400"/>

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
  
    <img src="/images/OpenAI.png" alt="ClearviewAI" width="300" height="400"/>

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
 
    <img src="/images/ProofPoint.png" alt="ClearviewAI" width="300" height="400"/>

### Tay Poisoning 
 **Summary of Incident:** Microsoft created Tay, a twitter chatbot for 18- to 24- year-olds in the U.S. for entertainment purposes. Within 24 hours of its deployment, Tay had to be decommissioned because it tweeted reprehrensible words.
 
 **Source:**
    - https://blogs.microsoft.com/blog/2016/03/25/learning-tays-introduction/

**Mapping to Adversarial Threat Matrix :**
-   Tay bot used the interactions with its twitter users as training data to improve its conversations.
-   Average users of Twitter coordinated together with the intent of defacing Tay bot by exploiting this feedback loop
-   As a result of this coordinated attack, Tay's training data was poisoned which led its conversation algorithms to generate more reprehensible material

  <img src="/images/Tay.png" alt="ClearviewAI" width="300" height="400"/>


### Microsoft - Azure Service 
**Summary of Incident:** : The Azure Red Team and Azure Trustworthy ML team performed a red team exercise on an internal Azure service with the intention of disrupting its service

**Reported by:** Microsoft 
**Mapping to Adversarial Threat Matrix :**
-   The team first performed reconnaissance to gather information about the target ML model
-   Then, using a valid account the team found the model file of the target ML model and the necessary training data
-   Using this, the red team performed an offline evasion attack by methodically searching for adversarial examples
-   Via an exposed API interface, the team performed an online evasion attack by replaying the adversarial examples, which helped achieve this goal.
-   This operation had a combination of traditional ATT&CK enterprise techniques such as finding Valid account, and Executing code via an API -- all interleaved with adversarial ML specific steps such as offline and online evasion examples.

<img src="/images/Msft1.PNG" alt="ClearviewAI" width="300" height="400"/>

### Bosch - EdgeAI 
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

<img src="/images/Bosch1.PNG" alt="ClearviewAI" width="300" height="400"/>

### Microsoft – EdgeAI 
**Summary of Incident:** The Azure Red Team performed a red team exercise on a new Microsoft product designed for running AI workloads at the Edge.  
**Reported by:** Microsoft  
**Mapping to Adversarial Threat Matrix:**  
-   The team first performed reconnaissance to gather information about the target ML model
-   The team first performed reconnaissance to gather information about the target ML model
-   Then, used a publicly available version of the ML model, started sending queries and analyzing the responses (inferences) from the ML model. 
-   Using this, the red team created an automated system that continuously manipulated an original target image, that tricked the ML model into producing incorrect inferences, but the perturbations in the image were unnoticeable to the human eye. 
-   Feeding this perturbed image, the red team was able to evade the ML model into misclassifying the input image. 
-   This operation had one step in the traditional ATTACK MITRE technique to do reconnaissance on the ML model being used in the product, and then the rest of the techniques was to use Offline evasion, followed by online evasion of the targeted product. 

<img src="/images/msft2.png" alt="ClearviewAI" width="300" height="400"/>

### MITRE Physical Adversarial Examples
- TBD 


# Contributing
We welcome any comments, feedback, or new case-studies! Before submitting a case-study, consider that the attack..

1.  Exploits one or more ML vulnerabilities 
    - Evasion
    - Poisoning 
    - Model replication
    - A bug in code that enabled any of the above
2.  The attack was against a production system
    - Machine Learning as a Service (MLaaS)
    - ML models hosted on cloud (AzureML, AWS, GCP, etc), on-prem, or on the edge (Mobile, IOT, etc)
3.  Most importantly, you have permission to share the information. Please follow the proper channels before reporting a new attack. If you are unsure of how best disclose, the team here is happy to help coordinate responsible disclosure. 