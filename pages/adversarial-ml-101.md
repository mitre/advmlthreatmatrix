# Adversarial Machine Learning 101 
Informally, Adversarial ML is “subverting machine learning systems for fun and profit”. The methods underpinning the production machine learning systems are systematically vulnerable to a new class of vulnerabilities across the machine learning supply chain collectively known as Adversarial Machine Learning. Adversaries can exploit these vulnerabilities to manipulate AI systems in order to alter their behavior to serve a malicious end goal.

Consider a typical ML pipeline shown below that is gated behind an API, wherein the only way to use the model is to send a query and observe a response.  In this example, we assume a blackbox setting: the attacker does NOT have direct access to the training data, no knowledge of the algorithm used and no source code of the model. The attacker only queries the model and observes the response. We will look at two broad categories of attacks: 

**Train time vs Inference time:** 

Training refers to the process by which data is modeled. This process includes collecting and processing data, training a model, validating the model works, and then finally deploying the model. An attack that happens at "train time" is an attack that happens while the model is learning prior its deployment. After a model is deployed, consumers of the model can submit queries and receive outputs (inferences).  
An attack that happens at "inference time" is an attack where the learned state of the model does not change and the model is just providing outputs. In practice, a model could be re-trained after every new query providing an attacker with some interesting scenarios by which they could use an inference endpoint to perform a "train-time" attack. In any case, the delineation is useful to describe how an attacker could be interacting with a target model.

With this in mind, we can jump into the attacks on ML systems. 

![Adversarial ML 101](/images/AdvML101.PNG)


# Machine Learning Attacks
Attacks on machine learning systems can be categorized as follows.

| Attack 		        | Overview	| Type |
| :---			        | :---      | :---:|
| Model Evasion         | Attacker modifies a query in order to get a desired outcome. These attacks are performed by iteratively querying a model and observing the output. | Inference |
| Functional Extraction | Attacker is able to recover a functionally equivalent model by iteratively querying the model. This allows an attacker to examine the offline copy of the model before further attacking the online model. | Inference |
| Model Poisoning 	    | Attacker contaminates the training data of an ML system in order to get a desired outcome at inference time. With influence over training data an attacker can create "backdoors" where an arbitrary input will result in a particular output. The model could be "reprogrammed" to perform a new undesired task. Further, access to training data would allow the attacker to create an offline model and create a Model Evasion. Access to training data could also result in the compromise of private data.  | Train |
| Model Inversion 	    | Attacker recovers the features used to train the model. A successful attack would result in an attacker being able to launch a Membership inference attack. This attack could result in compromise of private data. | Inference | 
| Traditional Attacks   | Attacker uses well established TTPs to attain their goal. | Both |



# Attack Scenarios
## Attack Scenario #1: Inference Attack 
Consider the most common deployment scenario where a model is deployed as an API endpoint. In this blackbox setting an attacker can only query the model and observe the response. The attacker controls the input to the model, but the attacker does not know how it is processed.

![Adversarial ML 101](/images/AdvML101_Inference.PNG)

---- 
## Attack Scenario #2: Training Time Attack
Consider that an attacker has control over training data. This flavor of attack is shown in [Tay Poisoning Case Study](/pages/case-studies-page.md#tay-poisoning) where the attacker was able to compromise the training data via the feedback mechanism.


![Adversarial ML 101](/images/AdvML101_Traintime.PNG)


## Attack Scenario #3: Attack on Edge/Client
Consider that a model exists on a client (like a phone) or on the edge (such as IoT) . An attacker might have access to model code through reversing the service on the client. This flavor of attack is shown in [Bosch Case Study with EdgeAI](/pages/case-studies-page.md#bosch---edge-ai).

![Adversarial ML 101](/images/AdvML101_Client.PNG)


# Important Notes
1.  This does not cover all kinds of attacks -- adversarial ML is an active area of research with new classes of attacks constantly being discovered.
2.  Though the illustration shows blackbox attacks, these attacks have also been shown to work in whitebox (where the attacker has access to either model architecture, code or training data)  settings.
3.  Though we were not specific about what kind of data – image, audio, time series, or tabular data - research has shown that of these attacks are data agnostic.

# Next Recommended Reading 
Head over to [Adversarial ML Threat Matrix](/pages/adversarial-ml-threat-matrix.md#adversarial-ml-threat-matrix) page to see a compendium of attacks in ATT&CK style. 
