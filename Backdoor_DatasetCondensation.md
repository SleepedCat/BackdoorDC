<h3  id="backdoorDC">BackdoorDC</h3>

Backdoor  
- [Backdoor Attacks Against Dataset Distillation](https://www.ndss-symposium.org/wp-content/uploads/2023/02/ndss2023_f287_paper.pdf)  [<a href="#NDSS2023Liu"><u>NOTE</u></a>]
- [Rethinking Backdoor Attacks on Dataset Distillation: A Kernel Method Perspective](https://openreview.net/forum?id=iCNOK45Csv)  
- [RDM-DC: poisoning resilient dataset condensation with robust distribution matching](https://proceedings.mlr.press/v216/zheng23a.html)  
- [Adaptive Backdoor Attacks Against Dataset Distillation for Federated Learning](https://ieeexplore.ieee.org/abstract/document/10622462)  

Dataset Condensation/Distillation  
- Gradient Matching
  - [Dataset Condensation with Gradient Matching](https://openreview.net/forum?id=mSAKhLYLSsl&continueFlag=634046c11e178a0606b18ce2de87a924)
  - [Dataset Condensation with Differentiable Siamese Augmentation](https://proceedings.mlr.press/v139/zhao21a.html)
  
- Distribution Matching
  - [Slimmable Dataset Condensation](https://openaccess.thecvf.com/content/CVPR2023/html/Liu_Slimmable_Dataset_Condensation_CVPR_2023_paper.html)
  - [Improved distribution matching for dataset condensation](https://openaccess.thecvf.com/content/CVPR2023/html/Zhao_Improved_Distribution_Matching_for_Dataset_Condensation_CVPR_2023_paper.html)
  - [Dataset Condensation With Distribution Matching](https://openaccess.thecvf.com/content/WACV2023/html/Zhao_Dataset_Condensation_With_Distribution_Matching_WACV_2023_paper.html)

- Generative
  - [Generalizing Dataset Distillation via Deep Generative Prior](https://openaccess.thecvf.com/content/CVPR2023/html/Cazenavette_Generalizing_Dataset_Distillation_via_Deep_Generative_Prior_CVPR_2023_paper.html)
  - [Efficient Dataset Distillation via Minimax Diffusion](https://openaccess.thecvf.com/content/CVPR2024/html/Gu_Efficient_Dataset_Distillation_via_Minimax_Diffusion_CVPR_2024_paper.html)
  - [D^4: Dataset Distillation via Disentangled Diffusion Model](https://openaccess.thecvf.com/content/CVPR2024/html/Su_D4_Dataset_Distillation_via_Disentangled_Diffusion_Model_CVPR_2024_paper.html)

<h3  id="NDSS2023Liu">Backdoor Attacks Against Dataset Distillation (NDSS2023)</h3>

1. Overview
* Problem: The existing dataset distillation techniques mainly aim at achieving the best trade-off between resource usage efficiency and model utility. The security risks (backdoor attacks) stemming from the have not been explored.  
* Scenario: In the image domain.  
* Contribution: NAIVEATTACK 【simply add pre-defined triggers to the raw data】 & DOORPING 【updates the triggers during the entire distillation procedure】.  

2. Motivation
* Assumption: Considering the backdoor attack that a malicious dataset distillation service provider can launch from the upstream (_i.e._, data distillation provider).
* Weakness of classic backdoor attacks: The classic attacks cannot be directly applied to the distilled datasets to backdoor the downstream models since these distilled datasets are small and not sufficient enough to inject the backdoor. (1) Human inspection can quickly mitigate such attacks. (2) Attack success rate is low.

3. Why DOORPING
* Triggers may not always be retained in the distilled dataset.
* Result: Empirical results show that both of our attacks maintain high model utility. NAIVEATTACK achieves a reasonable attack success rate (ASR) in some cases, while DOORPING consistently attains a higher ASR (close to 100%) in all cases.

4. Metric
* ASR, Attack Success Rate: Measures the success rate in making the model generate wrong predictions to the target label given triggered samples.
* CTA, Clean Test Accuracy: Evaluates the utility of the model given clean samples.

5. Threat Model
* Attack scenarios: 1) the victim commissions the attacker to distill a specific dataset on their behalf. 2) Instead of buying the original training dataset with millions of images, the victim opts to purchase a smaller synthesized dataset from the attacker to reduce the cost. (on the practical side)
* Attacker's capability: The only capability the attacker has is controlling the dataset distillation process. We stress that the attacker does not interfere with the downstream model training.
* Attacker's Goal: __The trigger is negligible and indistinguishable to the human moderators to avoid visual mitigation but remains effective in the downstream tasks.__
* Attack challenge: 1) The attackers must first ensure that the backdoored distilled dataset can guarantee the downstream model utility. 2) they need to ensure that the triggers are indistinguishable from the potential human inspection. 3) Finally, the attackers must make sure that the backdoor can be effectively implanted in the downstream models.

6. NAIVEATTACK: $$\mathcal{A}_{naive}(x)=x\cdot(1-m)+t\cdot m$$

7. DOORPING: 1) update trigger 2) inject trigger.


