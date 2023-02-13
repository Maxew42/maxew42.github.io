---
layout: post
title: Is Deep Learning in a local minimum?
lang: en
---


The spectacular success of Deep Learning makes it appear to many as a Swiss Army knife capable of anything. In reality, it remains a powerful but highly specialized tool. Seemingly simple tasks are not accessible to the most powerful models and the problem of generalization is still significant. Is Deep Learning converging towards a local minimum, far from an optimal solution embodied by biological neural networks?


<details>
  <summary><b> TL;DR</b> </summary>

<ol>
  <li>Despite rapid progress, human/animal cognition is still poorly understood. </li>
  <li>One thing is certain: ANNs operate very differently from biological neural networks. </li>
  <li>Language models, ChatGPT and others, while very powerful and useful, are not in themselves future AGIs. </li>
  <li>Deep Learning is an increasingly important tool in neuropsychology. </li>
  <li>Biomimetic methods (SNNs, Capsules, etc.) are being developed, but the surprising success of current techniques hides their progress.</li>
</ol>
</details>


# Deep Learning : Long story short
Whether you are familiar with computer science or not, you have certainly heard about Deep Learning, a branch of Machine Learning that focuses on the study of Artificial Neural Networks (ANNs). There is a phenomenal amount of research on this subject. Nearly 16,000 articles containing the keyword were published in 2022 on [arXiv.org](https://arxiv.org/), a figure that is increasing every year. This interest, which is far from being limited to laboratories, is justified by impressive results in various applications: computer vision, natural language processing, speech recognition, etc. The expectations placed on this relatively young field are therefore immense, which naturally leads to overly enthusiastic or even dubious promises.
{: .text-justify}

Indeed, the spectacular answers of chatGPT and the wonderful images of Dall-E, MidJourney, and other generative networks hide the difficulties that Deep Learning research faces today. ChatGPT writes poetry but cannot calculate a simple GCD or perform an addition (even though it performs several billion of them to give you this incorrect answer). His lack of "common sense" makes him confidently state nonsense statements. Such examples, often quite comical, swarm social networks and this lack of robustness extends to the whole field. Give a guitar to a monkey, it will be recognized as a human being by a [state of the art model](https://arxiv.org/pdf/1711.04451.pdf), see Figure 1.

Outside of their training set, ANNs are quite fragile. And some basic tasks, e.g. calculating the GCD, are not even learnable today. Why not take inspiration from the brain of our guitarist monkey to address the weaknesses of ANNs ? But do they not already behave like biological brain ?

![_config.yml]({{ site.baseurl }}/images/Pasted image 20230115201814.png)
<!-- ![[Pasted image 20230115201814.png]] -->
***Figure 1:** Bikes, motorcycles, and guitars are not common in the jungle. Without being exposed to these unlikely cases, the model provides a response reflecting a familiar situation from the training data set, the monkey becomes a person, the guitar a bird.*

# Neural Networks: Monkey & Silicone

Human and animal cognition is still poorly understood. However, no electrodes are needed to see the gap that exists today between human and ANN learning. A child is quickly able to differentiate between a dog and a cat or to predict the trajectory of a toy thrown in the air. It takes an ANN, even a basic one, hundreds of examples to achieve the same results. In the supervised learning paradigm, these examples must be labeled, thus incurring significant costs. Other paradigms; Reinforcement Learning, Self-supervised Learning, do not require this labeling, but are not more sample-efficient. So are ANNs very different from our brains?

A closer look at the functioning of biological neural networks confirms this discrepancy. Here are some points of notable divergence.

#### Backpropagation
Backpropagation, an essential mechanism in ANNs training, seems to not be possible in the brain. The arguments against it are numerous and convincing: the signals from natural neuron spikes are not derivable, hypothetical error back-propagation mechanisms do not seem compatible with our understanding of natural neurons, etc. ANNs therefore do not learn the same way as the brain.

One recent alternative proposed by Geoffrey Hinton is the [Forward-Forward Algorithm](https://www.cs.toronto.edu/~hinton/FFA13.pdf), which allows for training ANNs without backpropagation. However, it does not seem to be a replacement and its proximity to biological learning remains limited.

#### Convolutional Neural Networks
Convolutional Neural Networks (CNNs), the cornerstone of modern computer vision, were originally inspired by the functioning of the visual cortex, but actually deviate quite significantly from the functioning of the brain. In fact, the brain is particularly good at recognizing objects regardless of their position in the visual field or viewing angle, thanks to mechanisms for mental [rotation/translation](https://www.science.org/doi/10.1126/science.2911737). This ability, even in simple cases, is only accessible to CNNs through a large number of data and parameters. These neural networks are not capable of performing this translation/rotation, and instead rely on massive replication of neurons responsible for detecting a specific shape/object, as well as pooling operation which introduces some translation invariance, allowing replication to be reduced by grouping features in a single location. This pooling operation is particularly criticized by Geoffrey Hinton: "The pooling operation used in convolutional neural is a big mistake and the fact that it works so well is a disaster." He proposes an alternative model, the [Capsules](https://proceedings.neurips.cc/paper/2017/hash/2cad8fa47bbef282badbb8de5374b894-Abstract.html), which eliminates this problem by directing information about the nature of the object, accompanied by positional information, directly to specialized sub-models for recognizing specific objects. This route, trainable without backpropagation, potentially approaches the functioning of the brain. Published in 2017, this innovative architecture fulfilled its promises on simple datasets (MNIST), but six years later, it is clear that it struggles to convince.

An amusing effect of the translation invariance of CNNs is that the spatial position of components of an object to be recognized counts little. Thus, the two faces in Figure 2 are almost identical from their point of view.


![_config.yml]({{ site.baseurl }}/images/Pasted image 20230114112050.png)
***Figure 2 :** For a CNN, a face is ultimately just a "mouth, a nose, two eyes and an ellipse"*

  
# The data question

Beyond the problem of architecture and training, the form of the data is also important. Our body captures information in a format that may be more suitable for processing by neurons than the numerical data that we use today to train ANNs.

#### Biomimetic data

For example, our vision is not based, like that of ANNs, on giant pixel arrays (images). In reality, our retina is stimulated at every moment by photons in an asynchronous way. From the point of view of biological perception, "images" do not exist. This type of flow can be obtained using a [neuromorphic camera](https://en.wikipedia.org/wiki/Event_camera), or *event-based camera*. It replaces the array of pixels by a series of $(timestamp, intensity)$ couples captured asynchronously at each change of value of the pixel considered. This type of sensor has important advantages in terms of data volume reduction, but also framerate and dynamic range. However, the whole technical foundation of computer vision is based on the analysis of pixel arrays. One must therefore innovate in order to apply the power of Deep Learning to this type of data. [Spiking Neural Networks](https://hal.science/hal-03250505/document) (SNNs), operating with more or less frequent stimuli and largely inspired by the human brain, are the ideal candidates for analyzing this new kind of data.

#### Multimodal data

The multimodality of data, i.e., its diversity of formats, is also a major issue. It has been shown that in the human brain, the same neuron can react to seemingly very different perceptions. Thus, we would all have a [Luke Skywalker neuron](https://www.nature.com/articles/ncomms13408), capable of reacting to the image, the spoken or written name of the Jedi apprentice. Another example: in video conferencing it is easier and more pleasant to communicate with someone who has a webcam on. Body language, feedback, etc. play a crucial role in human to human communication. Can an ANN understand us without having access to it? Can these neural networks anticipate gravity without having fallen, or at least virtually experienced a fall? Can they imitate Beethoven by simply reading his scores?

These questions are related to the problem, long preceding Deep Learning, of the possibility of expressing the wide range of our perception in a single modality, that of language. This is a fundamental philosophical question, which in the context of Deep Learning naturally leads us to talk about language models.

# Language models : Scale is all you need ?

ChatGPT, developed by OpenAI, is the most successful publicly available chatbot to date. It is the current public peak, which will probably be quickly surpassed, of a race to ever larger language models trained on increasingly gigantic volumes of data. This race is based on the observation that simply increasing the size of the models and their training dataset allows them to acquire new skills, e.g., translation, summarization, basic mathematics, for which they have not yet received specific training.
This property is very encouraging, as it would be enough to have a very large calculation capacity and a lot of data to achieve the well-known Artificial General Intelligence (AGI). Especially since, although not strictly comparable, the number of parameters of the current models is not so far from the number of synapses in the human brain, within a very small factor of $10^3$.

However, this has to be tempered. Current experience shows that these models do not perform so well in all domains. Language models stumble on simple tasks. Mathematics, for example, is challenging, as is reasoning involving physics or [spaciality](https://twitter.com/TomerUllman/status/1599767597653729280?s=20&t=XqaRcV1lBQxGeabjs0izvg). The latter in particular are not well represented by text. In fact, language alone is not capable of producing "common sense" and the ability to generalize, in that it is a medium of [lacunar and ambiguous](https://www.noemamag.com/ai-and-the-limits-of-language)  information. Approaches based on symbolic algorithms or using simplified models of the world aim to overcome these weaknesses, with or without the help of Deep Learning. But these approaches are not without difficulties and are so far rather disappointing


>**"Thought remains beyond the reach of language**." -Bergson (Poorly translated by yours truly)

# Should we keep close to the biological brain?

A legitimate question is the need to stay close to the brain model. After all, the most successful models in image recognition are moving further and further away from the brain's behavior without ceasing to improve, as shown by the recent evolution of the *Brain Score*, visible in Figure 3.

![_config.yml]({{ site.baseurl }}/images/Pasted image 20230114133318.png)
***Figure 3 :** The Brain Score is a measure of how close the response of an ANN is to that of the macaque monkey brain. It is compared here to the performance (accuracy) on the ImageNet reference dataset.*

Moreover, the rise of *Few-shot* techniques, i.e. learning with very few examples, challenges the necessity of a huge volume of data for training ANNs.

If it works, why bother trying to imitate what we don't even understand? Nevertheless, we have to admit that the victories of Deep Learning often have a more or less important part of biomimicry, e.g. the artificial neuron, the CNNs, the attention mechanism, the dropout, etc. These attempts to stick to the functioning of the brain are therefore not futile, but suffer from a lack of understanding of human cognition, and also perhaps from an insufficient interest of Deep Learning researchers for this subject, although it is a twin to theirs.
  
> **When Deep Learning helps us understand the brain**  
> Deep Learning still has a lot to learn from the human brain. But the opposite is also true. In this [article](https://www.nature.com/articles/s41467-021-26751-5) in Nature, an ANN ($\beta$-VAE) is used to study the organization of face-encoding neurons, i.e., the neural representation of faces, in macaque monkeys. (Note the existence of a "fringe neuron"!). The result? It is possible to reconstruct the face seen by the monkey by reading its neural response. Not so far from science fiction.
> It is remarkable to obtain similar results with an ANN as with a biological neural network, even though, as we have seen, they share few characteristics. Studies combining these approaches are increasingly numerous.

## Conclusion

We can hardly speak of separation in the sense that ANNs have never really been close to the functioning of the brain. Biomimetic approaches have so far had limited success, which must be put in perspective with the difference in the amount of resources allocated to their development. 363 publications for Spiking Neural Networks on arXiv.org in 2022 against nearly 16,000 for the whole field. As with CNNs a decade ago, the introduction of [specialized hardwares](https://arxiv.org/ftp/arxiv/papers/2005/2005.01467.pdf) should accelerate research in this promising field. In parallel, the development of Deep Learning opens new perspectives for the study of the human brain, by offering experimental as well as theoretical [tools](https://www.pnas.org/doi/10.1073/pnas.2200800119).