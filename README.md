# Bot or User? - Twitter Classification

In this repository the Heterogeneous Graph Transformer [1] is applied on the TwiBot-22 Twitter dataset [2] to distinguish bots from real users on the platform.

The focus of this project diverges from classification based on text or images - towards the behavioral and interaction patterns as well as user metadata to distinguish real from fake users. <br> These patterns are more difficult to camouflage, and thus are a promising direction of research.

**Because:**<br>
With the increasing effectiveness as well as ease of access to generative AI, such as text and image generation models more sophisticated impersonations and generation of fake media can be achieved, difficult or impossible to distinguish from real content. Malicious-bot operators have gained access to multi-billion dollar means which camouflage their bots' behavior. The generative models, trained with human feedback , effectively to be indistinguishable from real content, diminish the out-of-distribution shift which was previously easily detectable. 

Experiments can be found in the main.ipynb.
<br><br>
[1] https://arxiv.org/abs/2003.01332 <br>
[2] https://arxiv.org/abs/2206.04564 

## Experimental Results
Below, the training loss and validation F1 score are shown (Figure 1 and 2).<br>
In the loss, equal class weighting for positives and negatives is applied.<br>
The model is trained for 25 epochs.
This amounts to 50 hours on a NVIDIA P100 GPU.

One training epoch corresponds to 300,000 node classifications. The model is trained with the Adam optimizer and a learning rate of 0.0002 and a minibatch size of 32. The evaluation is done on the remaining 90,000 test set nodes, which the model has not seen.<br><br><br>
![Testing performance](image.png)<br><br><br>
The result (37.1% F1, 0.69% precision,
0.25% recall) is  short a few percent from the Twibot-22 paper (39.6%) (maybe because the model uses only graph-based information, opposed to the paper's implemementation).<br>

The naive logistic regression baseline (user vector + degree counts from the graph) outperforms the model with an F1 of 43%, (30% precision, 77% recall).<br>
Since the GNN achieves similar results to the Twibot-22 paper, despite not knowing their exact implementation we can guessably observe that the logistic regression baseline outperforms over 58% of the algorithms (17/29) implemented for demonstration of the Twibot-22 dataset.<br><br> 

The GNN might show more desirable performance for real-world application compared to the logistic regression model without any tuning (0.69% vs 30% precision).

