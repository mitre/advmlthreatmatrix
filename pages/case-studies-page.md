## Case Studies Page

  - [ClearviewAI Misconfiguration](/pages/case-studies-page.md#clearviewai-misconfiguration)
  - [GPT-2 Model Replication](/pages/case-studies-page.md#gpt-2-model-replication)
  - [ProofPoint Evasion](/pages/case-studies-page.md#proofpoint-evasion)
  - [Tay Poisoning](/pages/case-studies-page.md#tay-poisoning)
  - [Microsoft - Azure Service - Evasion](/pages/case-studies-page.md#microsoft---azure-service)
  - [Microsoft Edge AI - Evasion](/pages/case-studies-page.md#microsoft---edge-ai)
  - [MITRE - Physical Adversarial Attack on Face Identification](/pages/case-studies-page.md#mitre---physical-adversarial-attack-on-face-identification)
  

Attacks on machine learning (ML) systems are being developed and released with increased regularity. Historically, attacks against ML systems have been performed in a controlled academic settings, but as these case-studies demonstrate, attacks are being seen in-the-wild. In production settings ML systems are trained on personally identifiable information (PII), trusted to make critical decisions with little oversight, and have little to no logging and alerting attached to their use. The case-studies were selected because of the impact to production ML systems, and each demonstrates one of the following characteristics.

1. Range of Attacks: evasion, poisoning, model replication and exploiting traditional software flaws.
2. Range of Personas: Average user, Security researchers, ML Researchers and Fully equipped Red team.
3. Range of ML Paradigms: Attacks on MLaaS, ML models hosted on cloud, hosted on-premise, ML models on edge.
4. Range of Use case: Attacks on ML systems used in both "security-sensitive" applications like cybersecurity and non-security-sensitive applications like chatbots.

----

## ClearviewAI Misconfiguration 
**Summary of Incident:** Clearview AI's source code repository, though password protected, was misconfigured to allow an arbitrary user to register an account. This allowed an external researcher to gain access to a private code repository that contained Clearview AI production credentials, keys to cloud storage buckets containing 70K video samples, and copies of its applications and Slack tokens. With access to training data, a bad-actor has the ability to cause an arbitrary misclassification in the deployed model. 

**Mapping to Adversarial Threat Matrix :**
- In this scenario, a security researcher gained initial access to via a "Valid Account" that was created through a misconfiguration. No Adversarial ML techniques were used.
- These kinds of attacks illustrate that any attempt to secure ML system should be on top of "traditional" good cybersecurity hygiene such as locking down the system with least privileges, multi-factor authentication and monitoring and auditing.

<img src="/images/ClearviewAI.png" alt="ClearviewAI" width="275" height="150"/>

**Reported by:** 
-   Mossab Hussein (@mossab_hussein)

**Source:**
-   https://techcrunch.com/2020/04/16/clearview-source-code-lapse/amp/
-   https://gizmodo.com/we-found-clearview-ais-shady-face-recognition-app-1841961772

----

## GPT-2 Model Replication 

**Summary of Incident:** : OpenAI built GPT-2, a powerful natural language model and adopted a staged-release process to incrementally release 1.5 Billion parameter model. Before the 1.5B parameter model could be released by OpenAI eventually, two ML researchers replicated the model and released it to the public. *Note this is an example of model replication NOT model model extraction. Here, the attacker is able to recover a functionally equivalent model but generally with lower fidelity than the original model, perhaps to do reconnaissance (See ProofPoint attack). In Model extraction, the fidelity of the model is comparable to the original, victim model.*

**Mapping to Adversarial Threat Matrix :**
-   Using public documentation about GPT-2, ML researchers gathered similar datasets used during the original GPT-2 training.
-   Next, they used a different publicly available NLP model (called Grover) and modified Grover's objective function to reflect
GPT-2's objective function.
-   The researchers then trained the modified Grover on the dataset they curated, using Grover's initial hyperparameters, which
    resulted in their replicated model.
  
<img src="/images/OpenAI.png" alt="GPT2_Replication" width="275" height="150"/>

**Reported by:**
- Vanya Cohen (@VanyaCohen) 
- Aaron Gokaslan (@SkyLi0n)
- Ellie Pavlick
- Stefanie Tellex

**Source:**
- https://www.wired.com/story/dangerous-ai-open-source/
- https://blog.usejournal.com/opengpt-2-we-replicated-gpt-2-because-you-can-too-45e34e6d36dc


----

## ProofPoint Evasion 

**Summary of Incident:** : CVE-2019-20634 describes how ML researchers evaded ProofPoint's email protection system by first building a copy-cat email protection ML model, and using the insights to evade the live system.

**Mapping to Adversarial Threat Matrix :**
-   The researchers first gathered the scores from the Proofpoint's ML system used in email email headers.
-   Using these scores, the researchers replicated the ML mode by building a "shadow" aka copy-cat ML model.
-   Next, the ML researchers algorithmically found samples that this "offline" copy cat model.
-   Finally, these insights from the offline model allowed the researchers to create malicious emails that received preferable scores from the real ProofPoint email protection system, hence bypassing it.

<img src="/images/ProofPoint.png" alt="PFPT_Evasion" width="625" height="175"/>

**Reported by:**
- Will Pearce (@moo_hax)
- Nick Landers (@monoxgas)

**Source:**
- https://nvd.nist.gov/vuln/detail/CVE-2019-20634
- https://github.com/moohax/Talks/blob/master/slides/DerbyCon19.pdf
- https://github.com/moohax/Proof-Pudding

----

## Tay Poisoning 

 **Summary of Incident:** Microsoft created Tay, a twitter chatbot for 18- to 24- year-olds in the U.S. for entertainment purposes. Within 24 hours of its deployment, Tay had to be decommissioned because it tweeted reprehensible words.
 
**Mapping to Adversarial Threat Matrix :**
-   Tay bot used the interactions with its twitter users as training data to improve its conversations.
-   Average users of Twitter coordinated together with the intent of defacing Tay bot by exploiting this feedback loop.
-   As a result of this coordinated attack, Tay's training data was poisoned which led its conversation algorithms to generate more reprehensible material.

<img src="/images/Tay.png" alt="Tay_Poisoning" width="350" height="150"/>


**Source:**
- https://blogs.microsoft.com/blog/2016/03/25/learning-tays-introduction/
- https://spectrum.ieee.org/tech-talk/artificial-intelligence/machine-learning/in-2016-microsofts-racist-chatbot-revealed-the-dangers-of-online-conversation

----

## Microsoft - Azure Service 
**Summary of Incident:** : The Azure Red Team and Azure Trustworthy ML team performed a red team exercise on an internal Azure service with the intention of disrupting its service.

**Reported by:** Microsoft 
**Mapping to Adversarial Threat Matrix :**
-   The team first performed reconnaissance to gather information about the target ML model.
-   Then, using a valid account the team found the model file of the target ML model and the necessary training data.
-   Using this, the red team performed an offline evasion attack by methodically searching for adversarial examples.
-   Via an exposed API interface, the team performed an online evasion attack by replaying the adversarial examples, which helped achieve this goal.
-   This operation had a combination of traditional ATT&CK enterprise techniques such as finding Valid account, and Executing code via an API -- all interleaved with adversarial ML specific steps such as offline and online evasion examples.

![MS_Azure](/images/Msft1.PNG)


**Reported by:**
- Microsoft (Azure Trustworthy Machine Learning)

**Source:**
- None

----

## Microsoft - Edge AI
**Summary of Incident:** The Azure Red Team performed a red team exercise on a new Microsoft product designed for running AI workloads at the Edge.  

**Mapping to Adversarial Threat Matrix:**  
-   The team first performed reconnaissance to gather information about the target ML model.
-   Then, used a publicly available version of the ML model, started sending queries and analyzing the responses (inferences) from the ML model. 
-   Using this, the red team created an automated system that continuously manipulated an original target image, that tricked the ML model into producing incorrect inferences, but the perturbations in the image were unnoticeable to the human eye. 
-   Feeding this perturbed image, the red team was able to evade the ML model into misclassifying the input image. 
-   This operation had one step in the traditional MITRE ATT&CK techniques to do reconnaissance on the ML model being used in the product, and then the rest of the techniques was to use Offline evasion, followed by online evasion of the targeted product. 

![alt_text](/images/msft2.png)

**Reported by:**
Microsoft  

**Source:**
None

----
## MITRE - Physical Adversarial Attack on Face Identification

**Summary of Incident:** MITRE’s AI Red Team demonstrated a physical-domain evasion attack on a commercial face identification service with the intention of inducing a targeted misclassification.

**Mapping to Adversarial Threat Matrix:**

- The team first performed reconnaissance to gather information about the target ML model.
- Using a valid account, the team identified the list of IDs targeted by the model.
- The team developed a proxy model using open source data.
- Using the proxy model, the red team optimized a physical domain patch-based attack using an expectation of transformations.
- Via an exposed API interface, the team performed an online physical-domain evasion attack including the adversarial patch in the input stream which resulted in a targeted misclassification.
- This operation had a combination of traditional ATT&CK enterprise techniques such as finding Valid account, and Executing code via an API – all interleaved with adversarial ML specific attacks.

![mitre](/images/mitre.png)

**Reported by:** 
MITRE AI Red Team

**Source:** 
None

----
# Contributing New Case Studies

We are especially excited for new case-studies! We look forward to contributions from both industry and academic researchers. Before submitting a case-study, consider that the attack:
1.  Exploits one or more vulnerabilities that compromises the confidentiality, integrity or availability of ML system.
2.  The attack was against a *production, commercial* ML system. This can be on MLaaS like Amazon, Microsoft Azure, Google Cloud AI, IBM Watson etc or ML systems embedded in client/edge. 
3.  You have permission to share the information/published this research. Please follow the proper channels before reporting a new attack and make sure you are practicing responsible disclosure.

You can email advmlthreatmatrix-core@googlegroups.com with summary of the incident, Adversarial ML Threat Matrix mapping and associated resources. 
