## Adversarial ML 101 
This is a short primer intended for security analysts

Informally, Adversarial ML is "subverting machine learning systems for fun and profit". The methods underpinning the production machine learning systems are systematically vulnerable to a new class of vulnerabilities across the machine learning supply chain collectively known as Adversarial Machine Learning. Adversaries can exploit these vulnerabilities to manipulate AI systems in order to alter their behavior to serve a malicious end goal.

Consider a typical ML pipeline shown below that is gated behind an API, wherein the only way to use the model is to send a query and observe an response. In this example, we assume a blackbox setting: the attacker does **NOT** have direct access to the training data, no knowledge of the algorithm used and no source code of the model. The attacker only queries the model and observes the response.

![Adversarial ML 101](/images/AdvML101.PNG)

Here are some of the adversarial ML attacks that an adversary can perform on this system:
| Attack 		 				| Overview	|
| :---							| :---
| Evasion Attack 				| Attacker modifies the query to get appropriate response. The attacker can find the just-the-right query to get the desired response algorithmically	|
| Poisoning attack 				| Attacker contaminates the training phase of ML systems to get intended result		|
| Model Inversion 				| Attacker recovers the secret features used in the model through careful queries	| 
| Membership Inference  		| Attacker can infer if given data record was part of the model's training dataset or not |
| Model Stealing        		| Attacker is able to recover a functionally equivalent model with similar fidelity as original model by constructing careful queries | 
| Model Replication     		| Attacker is able to recover functionally equivalent model (but generally with lower fidelity) | 
| Reprogramming ML system       | Repurpose the ML system to perform an activity it was not programmed for | 
| Attacking the ML supply chain | Attacker compromises the ML models as it is being downloaded for use | 
| Exploit Software Dependencies | Attacker uses traditional software exploits like buffer overflow or hardware exploits like GPU trojans to attain their goal. |

## Finer points 
1.  This does not cover all kinds of attacks. Adversarial ML is an active area of research with new classes constantly being discovered.
2.  These attacks are applicable to ML models in different paradigms, ML models on premise, on cloud, on Edge.
3.  Though the illustration shows blackbox attacks, these attacks have also been shown to work in whitebox (where the attacker has access to either model architecture, code or training data) settings
4.  Though we were not specific about what kind of data - image, audio, timeseries, or tabular data, research has shown that of these attacks have shown to exist in all the data types

## Next Recommended Reading 
Head to  [Adversarial ML Threat Matrix](/pages/adversarial-ml-threat-matrix.md) to learn about the structure of the matrix alongside definitions

