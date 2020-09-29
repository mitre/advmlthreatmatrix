Questions? <Ramk@microsoft.com>

Table of Contents {#table-of-contents .TOC-Heading}
=================

[Git Hub Landing Page 2](#git-hub-landing-page)

[Adversarial ML -- 101 2](#adversarial-ml-101)

[Finer points: 3](#finer-points)

[Why Adversarial ML Threat Matrix? 3](#why-adversarial-ml-threat-matrix)

[Structure of Adversarial ML Threat Matrix
3](#structure-of-adversarial-ml-threat-matrix)

[Things to keep in mind before you use the framework:
4](#things-to-keep-in-mind-before-you-use-the-framework)

[Contributors 5](#contributors)

[Feedback: 5](#feedback)

[Adversarial ML Threat Matrix 7](#adversarial-ml-threat-matrix)

[Case Studies Page 8](#case-studies-page)

[ClearviewAI Misconfiguration 8](#clearviewai-misconfiguration)

[GPT-2 Model Replication 9](#gpt-2-model-replication)

[ProofPoint Evasion 9](#proofpoint-evasion)

[Tay Poisoning 10](#tay-poisoning)

[Microsoft Red Team Exercise 11](#microsoft-red-team-exercise)

[Bosch Team Experience with EdgeAI
12](#bosch-team-experience-with-edgeai)

[MITRE -- Physical Adversarial Examples -- TBD
13](#mitre-physical-adversarial-examples-tbd)

Git Hub Landing Page
====================

The goal of this project is to position attacks on ML systems in an
ATT&CK-style framework so that security analysts can orient themselves
in this new and upcoming threats.

Adversarial ML -- 101 
---------------------

Informally, Adversarial ML is "subverting machine learning systems for
fun and profit". The methods underpinning the production machine
learning systems are systematically vulnerable to a new class of
vulnerabilities across the machine learning supply chain collectively
known as Adversarial Machine Learning. Adversaries can exploit these
vulnerabilities to manipulate AI systems in order to alter their
behavior to serve a malicious end goal.

Consider a typical ML pipeline shown in the left that is gated behind an
API, wherein the only way to use the model is to send a query and
observe an response. In this example, we assume a blackbox setting: the
attacker does **[NOT]{.ul}** have direct access to the training data, no
knowledge of the algorithm used and no source code of the model. The
attacker only queries the model and observes the response.

![](media/image1.png){width="3.2930555555555556in"
height="2.457638888888889in"}

Here are some of the adversarial ML attacks that an adversary can
perform on this system:

  Attack                          Overview
  ------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------
  Evasion Attack                  Attacker modifies the query to get appropriate response. The attacker can find the just-the-right query to get the desired response algorithmically,
  Poisoning attack                Attacker contaminates the training phase of ML systems to get intended result
  Model Inversion                 Attacker recovers the secret features used in the model through careful queries
  Membership Inference            Attacker can infer if given data record was part of the model's training dataset or not
  Model Stealing                  Attacker is able to recover a functionally equivalent model with similar fidelity as original model by constructing careful queries
  Model Replication               Attacker is able to recover functionally equivalent model (but generally with lower fidelity)
  Reprogramming ML system         Repurpose the ML system to perform an activity it was not programmed for
  Attacking the ML supply chain   Attacker compromises the ML models as it is being downloaded for use
  Exploit Software Dependencies   Attacker uses traditional software exploits like buffer overflow or hardware exploits like GPU trojans to attain their goal.

### Finer points: 

1)  This does not cover all kinds of attacks \-- adversarial ML is an
    active area of research with new classes constantly being discovered

2)  These attacks are applicable to ML models in different paradigm --
    ML models on premise, on cloud, on Edge.

3)  Though the illustration shows blackbox attacks, these attacks have
    also been shown to work in whitebox (where the attacker has access
    to either model architecture, code or training data) settings

4)  Though we were not specific about what kind of data -- image, audio,
    timeseries, or tabular data, research has shown that of these
    attacks have shown to exist in all the data types)

Why Adversarial ML Threat Matrix? 
---------------------------------

1.  In the last three years, major companies such
    as [Google](https://www.zdnet.com/article/googles-best-image-recognition-system-flummoxed-by-fakes/), [Amazon](https://www.fastcompany.com/90240975/alexa-can-be-hacked-by-chirping-birds), [Microsoft](https://www.theguardian.com/technology/2016/mar/24/tay-microsofts-ai-chatbot-gets-a-crash-course-in-racism-from-twitter),
    and [Tesla](https://spectrum.ieee.org/cars-that-think/transportation/self-driving/three-small-stickers-on-road-can-steer-tesla-autopilot-into-oncoming-lane), ,
    have had their ML systems tricked, evaded, or misled.

2.  This trend is only set to rise: According to [Gartner
    report](https://www.gartner.com/doc/3939991). 30% of cyberattacks by
    2022 will involve data poisoning, model theft or adversarial
    examples.

3.  However, industry is underprepared. In a
    [survey](https://arxiv.org/pdf/2002.05646.pdf) of 28 organizations
    spanning small as well as large organizations, 25 organizations did
    not know how to secure their ML systems.

Unlike traditional cybersecurity vulnerabilities that are tied to
specific software and hardware systems, adversarial ML vulnerabilities
are enabled by inherent limitations underlying ML algorithms. As a
result, data can now be weaponized in new ways requiring that we extend
the way we model cyber adversary behavior, reflecting emerging threat
vectors and the rapidly evolving adversarial machine learning attack
lifecycle.

This threat matrix came out of partnership with 12 industry and academic
research groups with the goal of empowering security analysts to orient
themselves in this new and upcoming threats. **We are seeding this
framework with a curated set of vulnerabilities and adversary behaviors
that Microsoft and MITRE have vetted to be effective against production
ML systems**

Since the primary audience is security analysts, we used ATT&CK as
template to position attacks on ML systems given its popularity and wide
adoption in the industry.

Structure of Adversarial ML Threat Matrix
-----------------------------------------

Because it is fashioned after [ATT&CK
Enterprise](https://attack.mitre.org/matrices/enterprise/), the
Adversarial ML Threat Matrix retains the terminologies: for instance,
The column heads of the Threat Matrix are called "Tactics" and the
individual entities are called "Techniques".

However, there are two main differences:

1)  ATT&CK Enterprise is generally designed for corporate network which
    is composed of many sub components like workstation, bastion hosts,
    database, network gear, active directory, cloud component and so on.
    The tactics of ATT&CK enterprise (initial access, persistence, etc)
    are really a short hand of saying initial access to *corporate
    network;* persistence *in corporate network.* In Adversarial ML
    Threat Matrix, we acknowledge that ML systems are part of corporate
    network but wanted to highlight the uniqueness of the attacks.

> **[Difference:]{.ul}** In the Adversarial ML Threat Matrix, the
> "Tactics" should be read as "reconnaissance of ML subsystem",
> "persistence in ML subsystem", "evading the ML subsystem"

2)  When we analyzed real-world attacks on ML systems, we found out that
    attackers can pursue different strategies: Rely on traditional
    cybersecurity technique only; Rely on Adversarial ML techniques
    only; or Employ a combination of traditional cybersecurity
    techniques and ML techniques

> **[Difference:]{.ul}** In Adversarial ML Threat Matrix, "Techniques"
> come in two flavors:

-   Techniques in orange are specific to ML systems

-   Techniques in white are applicable to both ML and non-ML systems and
    come directly from Enterprise ATT&CK

Note: The Adversarial ML Threat Matrix is not yet part of the ATT&CK
matrix.

Things to keep in mind before you use the framework:
----------------------------------------------------

1.  This is a **[first cut attempt]{.ul}** at collating known adversary
    techniques against ML Systems. We plan to iterate on the framework
    based on feedback from the security and adversarial machine learning
    community (please engage with us and help make the matrix better!).

Net-Net: This is a *[living document]{.ul}* that will be routinely
updated.

2.  Only known bad is listed in the Matrix. Adversarial ML is an active
    area of research with new classes constantly being discovered. If
    you find a technique that is not listed, please enlist it in the
    framework (see section on Feedback)

3.  We are not prescribing definitive defenses at this point -- The
    world of adversarial. We are already in conversations to add best
    practices in future revisions such as adversarial training for
    adversarial examples, restricting the number of significant digits
    in confidence score for model stealing.

4.  This is not a risk prioritization framework -- The Threat Matrix
    only collates the known techniques; it does not provide a means to
    prioritize the risks.

Contributors
------------

  **Organization**                                            **Contributors**
  ----------------------------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Microsoft                                                   Ram Shankar Siva Kumar, Hyrum Anderson, Will Pearce, Suzy Shapperle, Blake Strom, Madeline Carmichael, Matt Swann, Nick Beede, Kathy Vu, Andi Comissioneru, Sharon Xia, Mario Goertzel, Jeffrey Snover, Abhishek Gupta
  MITRE                                                       Mikel D. Rodriguez, Christina E Liaghati, Keith R. Manville, Michael R Krumdick
  Bosch                                                       Manojkumar Parmar
  IBM                                                         Pin-Yu Chen
  NVIDIA                                                      David Reber Jr., Keith Kozo, Christopher Cottrell, Daniel Rohrer
  Airbus                                                      Adam Wedgbury
  Deep Instinct                                               Nadav Maman
  TwoSix                                                      David Slater
  University of Toronto                                       Adelin Travers, Jonas Guan, Nicolas Papernot
  Cardiff University                                          Pete Burnap
  Software Engineering Institute/Carnegie Mellon University   Nathan M. VanHoudnos
  Berryville Institute of Machine Learning                    Gary McGraw, Harold Figueroa, Victor Shepardson, Richie Bonett

Feedback: 
---------

The Adversarial ML Threat Matrix is a first-cut attempt at collating a
knowledge base of how ML systems can be attacked. We need your help to
make it holistic and fill in the missing gaps!

-   Please submit a Pull Request with suggested changes! We are excited
    to make this system better with you!

-   For discussions around Adversarial ML Threat Matrix, we invite
    everyone to join our Google Group
    [here](https://groups.google.com/forum/#!forum/advmlthreatmatrix/join)

    -   If you want to access this forum using your corporate email (as
        opposed to your gmail),

        -   Open your browser in Incognito mode.

> Once you sign up with your corporate, and complete captcha, you may
> get an error \--  Ignore it!

-   Also note, emails from Google Forums generally go to "Other"/"Spam"
    folder. So, you may want to create a rule to go into your inbox
    instead

```{=html}
<!-- -->
```
-   Want to work with us on the next iteration of the framework?

    -   We are partnering with Defcon's AI Village to open up the
        framework to all community members to get feedback and make it
        better. Current thinking is to have this event circa
        Jan/Feb 2021.

    -   Please register here for the workshop for more hands on feedback
        session

-   If you have questions/comments that you'd like to discuss privately,
    please email: <Ram.Shankar@microsoft.com> and <Mikel@mitre.org>

Adversarial ML Threat Matrix 
============================

(Interactive Version to be built by MITRE. For Editable version, contact
<Ramk@Microsoft.com> )

![](media/image2.png){width="8.05361220472441in"
height="4.778260061242345in"}

Case Studies Page
=================

We chose **[real world attacks on production ML systems]{.ul}** based
on:

1.  Range of Attacks: evasion, poisoning, model replication and
    exploiting traditional software flaws.

2.  Range of Personas: Average user, Security researchers, ML
    Researchers and Fully equipped Red team

3.  Range of ML Paradigms: Attacks on MLaaS, ML models hosted on cloud,
    hosted on- presmise, ML models on edge

4.  Range of Use case: Attacks on ML systems used in both
    "security-sensitive" applications like cybersecurity and non
    security-sensitive applications like chatbots

ClearviewAI Misconfiguration 
----------------------------

a.  **Summary of Incident:** Clearview AI's source code repository,
    though password protected, was misconfigured. This allowed an
    external researcher to register as a new user to the code repository
    and gain access to Clearview AI's credentials, keys to cloud storage
    buckets containing 70K video samples, copies of its applications and
    Slack tokens

b.  **Reported by:** Mossab Hussein \@mossab_hussein

c.  **Source:**
    <https://techcrunch.com/2020/04/16/clearview-source-code-lapse/amp/>

d.  **Mapping to Adversarial Threat Matrix :**

    -   In this scenario, a security researcher gained initial access to
        via a "Valid Account" that was created through a
        misconfiguration. No Adversarial ML techniques were used.

    -   These kinds of attacks illustrate that any attempt to secure ML
        system should be on top of "traditional" good cybersecurity
        hygiene such as locking down the system with least privileges ,
        multi factor authentication and monitoring and auditing.

GPT-2 Model Replication 
-----------------------

a.  **Summary of Incident:** : OpenAI built GPT-2, a powerful natural
    language model and calling it "too dangerous to release" adopted a
    staged-release process to incrementally release 1.5 Billion
    parameter model. Before the 1.5B parameter model could be released
    by OpenAI, two ML researchers replicated the model and released it
    to the public.

Note this is a model replication attack: Here, attacker is able to
recover functionally equivalent model (but generally with lower
fidelity), perhaps to do reconnaissance (See proof point attack). In
Model stealing, the fidelity of the model is comparable to the original,
victim model.

b.  **Reported by: Vanya Cohen (**\@VanyaCohen) **, Aaron Gokaslan
    (**\@SkyLi0n**) , Ellie Pavlick, Stefanie Tellex**

c.  **Source:**
    <https://blog.usejournal.com/opengpt-2-we-replicated-gpt-2-because-you-can-too-45e34e6d36dc>
    ; <https://www.wired.com/story/dangerous-ai-open-source/>

d.  **Mapping to Adversarial Threat Matrix :**

    -   Using public documentation about GPT-2, ML researchers gathered
        similar datasets used during the original GPT-2 training.

    -   Next, they used a different publicly available NLP model (called
        Grover) and modified Grover's objective function to reflect
        GPT-2's objective function

    -   The researchers then trained the modified Grover on the dataset
        they curated, using Grover's initial hyperparameters, which
        resulted in their replicated model.

ProofPoint Evasion 
------------------

a.  **Summary of Incident:** : CVE-2019-20634 describes how ML
    researchers evaded ProofPoint's email protection system by first
    building a copy-cat email protection ML model, and using the
    insights to evade the live system.

b.  **Reported by:** \@moo_hax

c.  **Source:** <https://nvd.nist.gov/vuln/detail/CVE-2019-20634>

d.  **Mapping to Adversarial Threat Matrix :**

    -   The researchers first gathered the scores from the Proofpoint's
        ML system used in email email headers .

    -   Using these scores, the researchers replicated the ML mode by
        building a "shadow" aka copy-cat ML model

    -   Next, the ML researchers algorithmically found samples that this
        "offline" copy cat model

    -   Finally, these insights from the offline model allowed the
        researchers to create malicious emails that received preferrable
        scores from the real ProofPoint email protection system, hence
        bypassing it.

Tay Poisoning 
-------------

a.  **Summary of Incident:** Microsoft created Tay, a twitter chatbot
    for 18- to 24- year-olds in the U.S. for entertainment purposes.
    Within 24 hours of its deployment, Tay had to be decommissioned
    because it tweeted reprehrensible words.

b.  **Source:**
    <https://blogs.microsoft.com/blog/2016/03/25/learning-tays-introduction/>

c.  **Mapping to Adversarial Threat Matrix :**

    -   Tay bot used the interactions with its twitter users as training
        data to improve its conversations.

    -   Average users of Twitter coordinated together with the intent of
        defacing Tay bot by exploiting this feedback loop

    -   As a result of this coordinated attack, Tay's training data was
        poisoned which led its conversation algorithms to generate more
        reprehensible material

Microsoft Red Team Exercise 
---------------------------

a.  **Summary of Incident:** : The Azure Red Team and Azure Trustworthy
    ML team performed a red team exercise on an internal Azure service
    with the intention of disrupting its service

b.  Reported by: Azure TrustworthyML Team (<atml@microsoft.com>), Azure
    Red Team

c.  **Mapping to Adversarial Threat Matrix :**

    -   The team first performed reconnaissance to gather information
        about the target ML model

    -   Then, using a valid account the team found the model file of the
        target ML model and the necessary training data

    -   Using this, the red team performed an offline evasion attack by
        methodically searching for adversarial examples

    -   Via an exposed API interface, the team performed an online
        evasion attack by replaying the adversarial examples, which
        helped achieve this goal.

    -   This operation had a combination of traditional ATT&CK
        enterprise techniques such as finding Valid account, and
        Executing code via an API -- all interleaved with adversarial ML
        specific steps such as offline and online evasion examples.

Bosch Team Experience with EdgeAI 
---------------------------------

a.  **Summary of Incident:** : Bosch team performed a research exercise
    on an internal edge AI system with a dual intention to extract the
    model and craft adversarial example to evade

b.  **Reported by:** Manoj Parmar (\@mparmar47)

c.  **Mapping to Adversarial Threat Matrix :**

    -   The team first performed reconnaissance to gather information
        about the edge AI system device working with sensor interface

    -   Then, using a trusted relationship mechanism between sensor and
        edge ai system team fed synthetic data on sensor to extract the
        model

    -   Using this, the team performed an offline evasion attack by
        crafting adversarial example with help of extracted model

    -   Via an exposed sensor interface, the team performed an online
        evasion attack by replaying the adversarial examples, which
        helped achieve this goal.

    -   This operation had a combination of traditional ATT&CK
        industrial control system techniques such as supply chain
        compromise via sensor, and Executing code via sensor interface--
        all interleaved with adversarial ML specific steps such as
        offline and online evasion examples.

    -   The team was also able to reconstruct the edge ai system with
        extracted model

MITRE -- Physical Adversarial Examples -- TBD 
---------------------------------------------
