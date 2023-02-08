---
layout: post
title: Is Deep Learning in a local minimum?
lang: en
---


The spectacular successes of Deep Learning make it appear to many as a Swiss Army knife capable of everything. In reality, it remains today a powerful but highly specialized tool. Simple seeming tasks are not accessible to the most powerful models and the problem of generalization is still significant. Is Deep Learning converging towards a local minimum, far from an optimal solution embodied by biological neural networks?


<details>
  <summary><b> TL;DR</b> </summary>

<ol>
  <li>Malgré des progrès fulgurants, la cognition humaine/animale est encore mal comprise. </li>
  <li>Une chose est sûre, le fonctionnement des ANNs est très différent de celui des réseaux de neurones biologiques.  </li>
  <li>Les modèle de langage, ChatGPT et consorts, bien que très performants et utiles, ne sont pas en eux-mêmes de futurs AGIs. </li>
  <li>Le Deep Learning est un outil de plus en plus important en neuropsychologie. </li>
  <li>Des méthodes biomimétiques (SNNs, Capsules, etc.) sont en cours de développement, mais le succés surprenant des techniques actuelles les dissimulent.</li>
</ol>
</details>


# Très courte histoire du Deep Learning

Familiar or not with IT news, you have certainly heard of Deep Learning, a branch of Machine Learning focusing on the study of Artificial Neural Networks (ANNs). It concentrates a phenomenal amount of research. Nearly 16,000 articles containing the keyword were published in 2022 on [arXiv.org](https://arxiv.org/), a figure in sharp increase every year. This enthusiasm, which is far from being confined to the laboratories, is justified by impressive results in various applications: computer vision, natural language processing, speech recognition, etc. The hopes resting on this relatively young field are therefore immense which naturally leads to sometimes overly enthusiastic, even dubious promises.
{: .text-justify}

En effet, les réponses spectaculaires de chatGPT et les merveilleuses images des Dall-E, MidJourney, et autres réseaux génératifs cachent les difficultés que rencontrent aujourd'hui la recherche en Deep Learning. ChatGPT écrit de la poésie mais ne parvient pas à calculer un simple PGCD ou à réaliser une addition (alors même qu'il en effectue plusieurs milliards pour vous donner cette réponse incorrecte). Son absence de "bon sens" lui fait énoncer avec la plus grande confiance des faits insensés. De tels exemples, souvent assez comiques, pullulent sur les réseaux sociaux et ce constat de manque de robustesse s'étend à l'ensemble du domaine. Donnez une guitare à singe, il sera reconnu comme un être humain par un [modèle state of the art](https://arxiv.org/pdf/1711.04451.pdf), cf. Figure 1.

En dehors de leur base de données d'apprentissages, les ANNs sont bien fragiles. Et certaines tâches basiques, e.g., le calcul de PGCD, ne sont aujourd'hui même pas apprenables. Pourquoi ne pas s'inspirer du cerveau de notre singe guitariste pour pallier les faiblesses des ANNs ? Mais ceux-ci ne se comportent-t-ils pas déjà comme le cerveau biologique ?

![_config.yml]({{ site.baseurl }}/images/Pasted image 20230115201814.png)
<!-- ![[Pasted image 20230115201814.png]] -->
***Figure 1 :** Les motos, vélos et autre guitares ne sont pas courants dans la jungle. Sans avoir été exposé à ces cas improbables, le modèle propose une réponse reflétant une situation connue du jeu de données d'entrainement, le singe devient une personne, la guitare un oiseau.*

# Réseaux de Neurones : le singe face au silicone

La cognition de l'être humain comme de l'animal est encore mal comprise. Toutefois, pas besoin d'électrodes pour remarquer le gouffre existant aujourd'hui entre l'apprentissage humain et celui d'un ANN. Un enfant est vite capable de différencier un chien d'un chat ou de prédire la trajectoire d'un jouet lancé en l'air. Il faut à un ANN, même basique, des centaines d'exemples pour parvenir aux mêmes résultats. Dans le paradigme de l'apprentissage supervisé ces exemples doivent être étiquetés, entrainant, de fait, des coûts importants. D'autres paradigmes ; Reinforcement Learning, Self-supervised Learning, ne demandent certes pas cet étiquetage, mais ne sont pas plus "sample-efficient". Les ANNs seraient-ils donc très différents de nos cerveaux ?

Une confrontation plus fine avec le fonctionnement des réseaux de neurones biologiques confirme cet écart. Voici quelques points de divergence notable.  

#### Backpropagation
La backpropagation, mécanisme aujourd'hui indispensable dans l'entrainement des ANNs, ne semble pas être possible dans le cerveau. Les arguments en sa défaveur sont nombreux et convaincants : les signaux par pics des neurones naturels ne sont pas dérivables, les mécanismes hypothétiques de retro-propagation de l'erreur ne semblent pas compatibles avec notre connaissance des neurones naturels, etc. Les ANNs n'apprennent donc sûrement pas comme le cerveau.

On peut citer le [Forward-Forward Algorithm](https://www.cs.toronto.edu/~hinton/FFA13.pdf) proposé récemment par Geoffrey Hinton et permettant d'entrainer des ANNs sans recourir à la backpropagation. Toutefois, celui-ci ne semble pas amené à la remplacer et sa proximité avec l'apprentissage biologique reste a priori limitée.

#### Convolutional Neural Networks
Les Convolutional Neural Networks (CNNs), pierre angulaire de la vision par ordinateur moderne et pourtant initialement inspirés du fonctionnement du cortex visuel se détache en réalité assez nettement du fonctionnement du cerveau. En effet, celui-ci est particulièrement apte à reconnaître des objets indépendamment de leur positionnement dans le champ visuel ou de l'angle de vue, grâce notamment à des mécanismes de [rotation/translation mentales](https://www.science.org/doi/10.1126/science.2911737). Cette capacité, même dans des cas simples, n'est accessible aux CNNs qu'à travers un grand nombre de données et de paramètres. En effet, ces réseaux de neurones ne sont pas capables d'effectuer cette translation/rotation. Ils se reposent donc sur une réplication massive des neurones responsables de détecter une forme/ un objet spécifique, ainsi que sur l'opération de pooling qui introduit une certaine invariance à la translation, permettant donc de réduire la réplication en regroupant les features à un endroit unique. Cette opération de pooling est particulièrement décriée par Geoffrey Hinton : “The pooling operation used in convolutional neural is a big mistake and the fact that it works so well is a disaster”. Celui-ci propose un modèle alternatif, les [Capsules](https://proceedings.neurips.cc/paper/2017/hash/2cad8fa47bbef282badbb8de5374b894-Abstract.html), qui éliminent cette problématique de point de vue en dirigeant l'information sur la nature de l'objet, accompagnée d'informations positionelles, directement à des sous-modèles spécialisés à la reconnaissance d'objets spécifiques. Ce routage, entrainable sans backpropagation, se rapproche donc potentiellement du fonctionnement du cerveau. Publié en 2017, cette architecture innovante répond à ses promesses sur des datasets simples (MNIST), mais six ans après, force est de constater qu'elle peine à convaincre.

Un effet amusant de l'invariance par translation des CNNs est que la position spatiale des composants d'un objet à reconnaître entre peu en compte. Ainsi les deux visages de la Figure 2 sont quasi-identiques de leur point de vue.


![_config.yml]({{ site.baseurl }}/images/Pasted image 20230114112050.png)
***Figure 2 :** Pour un CNN, un visage n'est finalement qu'une "bouche, un nez, deux yeux et une ellipse"*

  
## Le problème des données

Au-delà du problème d'architecture et d'entrainement, la forme des données a aussi son importance. Notre corps capte l'information dans un format peut être plus adapté au traitement par des neurones que les données numérisées que nous utilisons aujourd'hui pour entrainer nos ANNs.

#### Des données biomimétiques

Par exemple, notre vision n'est pas basée, comme celle des ANNs, sur des tableaux de pixels géants (des images). En réalité, notre rétine est stimulée à chaque instant par des photons de façon asynchrone. Du point de vue de la perception biologique les "images" n'existent pas. Ce type de flux peut être obtenu à l'aide d'une [caméra neuromorphique](https://en.wikipedia.org/wiki/Event_camera), ou *event-based camera*. Celle-ci remplace le tableau de pixels par une série de couples $(timestamp, intensity)$ captés asynchroniquement à chaque changement de valeur du pixel considéré. Ce type de capteurs présente d'importants avantages en terme de réduction du volume de données, mais aussi de framerate et de plage dynamique. Toutefois, tout l'édifice technique de la vision par ordinateur se base sur l'analyse de tableaux de pixels. Il faut dès lors innover pour pouvoir appliquer la puissance du Deep Learning à ce type de données. Les [Spiking Neural Networks](https://hal.science/hal-03250505/document) (SNNs), fonctionnant à l'aide stimuli plus ou moins fréquents et largement inspirés du cerveau humain sont les candidats idéaux pour analyser ces nouvelles données.

#### Des données multimodales

La question de la multimodalité des données, i.e., de sa diversité de formes, est aussi majeure. Il est démontré que dans le cerveau humain un même neurone peut réagir à des perceptions en apparence très différentes. Ainsi, nous disposerions tous d'un [neurone Luke Skywalker](https://www.nature.com/articles/ncomms13408), capable de réagir à l'image, au nom prononcé ou écrit de l'apprenti jedi. Un autre exemple : en visioconférence il est plus simple et agréable de communiquer avec quelqu'un ayant une webcam allumée. Le langage corporel, le feedback, etc jouent un rôle crucial dans la communication entre humains. Un ANN peut-il nous comprendre sans y avoir accès ? Ces réseaux de neurones peuvent-ils anticiper la gravité sans avoir chuté, ou tout du moins expérimenté virtuellement une chute. Peuvent-ils imiter Beethoven en lisant simplement ses partitions ?

Ces questions rejoignent le problème, bien antérieur au Deep Learning, de la possibilité d'exprimer le large éventail de notre perception dans une modalité unique, celle du langage. C'est une question philosophique fondamentale, qui dans le cadre du Deep Learning nous amène naturellement à parler des modèles de langage.

## Modèles de langage : Scale is all you need ?

ChatGPT, développé par OpenAI, le chatbot grand public le plus abouti à ce jour ne cesse de faire l'actualité. Il est l'apogé publique actuelle, et qui sera vraisemblablement vite dépassé, d'une course aux modèles de langages toujours plus grands et entrainés sur des volumes de données de plus en plus gigantesques. Cette course part du constat que simplement augmenter la taille des modèles et de leur dataset d'entrainement leur permet d'acquérir de nouvelles compétences, e.g., traduction, résumé, mathématiques basique, pour lesquels ils n'ont pourtant pas reçu d'entrainements spécifiques.
Cette propriété est très encourageante, il suffirait donc de disposer d'une très grande capacité de calculs et de beaucoup de données pour parvenir à la fameuse Artificial General Intelligence (AGI). D'autant plus que, bien que pas strictement comparables, le nombre de paramètres des modèles actuels n'est plus si loin du nombre de synapses du cerveau humain, à un bien mince facteur $10^3$ près.
  
Il faut toutefois nuancer ce propos. L'expérience actuelle montre que ces modèles ne progressent pas si bien que ça dans tous les domaines. Les modèles de langage butent sur des tâches simples. Les mathématiques leur posent par exemple problème, ainsi que les raisonnements impliquant une notion de physique ou de [spacialité](https://twitter.com/TomerUllman/status/1599767597653729280?s=20&t=XqaRcV1lBQxGeabjs0izvg). Ces derniers en particulier ne sont pas bien représentés par du texte. En réalité, le langage n'est pas capable, seul, de produire du "bon sens" et la capacité à généraliser, en cela qu'il est un support d'information [lacunaire et ambigu](https://www.noemamag.com/ai-and-the-limits-of-language](https://www.noemamag.com/ai-and-the-limits-of-language). Des approches basées sur des algorithmes symboliques ou utilisant des modèles simplifiés du monde souhaitent pallier ces faiblesses, à l'aide ou non du Deep Learning. Mais ces approches ne sont pas sans difficulté et sont à ce jour plutôt décevantes.

>**"La pensée demeure incommensurable avec le langage**." -Bergson

### Doit-on rester proche du cerveau biologique ?

Une question légitime est celle de la nécessité de rester proche du modèle du cerveau. Après tout, les modèles les plus performants en reconnaissance d'images s'éloignent de plus en plus du comportement du cerveau sans cesser de progresser pour autant, comme en témoigne l'évolution récente du *Brain Score*, visible dans la Figure 3.

![_config.yml]({{ site.baseurl }}/images/Pasted image 20230114133318.png)
***Figure 3 :** Le Brain Score est une mesure de la proximité entre la réponse d'un ANN et celle du cerveau du singe macaque. Il est ici comparé à la performance (accuracy) sur le dataset de référence ImageNet.*

De plus, l'émergence de techniques *Few-shot*, i.e, apprendre avec très peu d'exemples, remet en question la nécessité d'un volume considérable de données pour l'entrainement des ANNs.

Si ça marche à quoi bon à tout prix chercher à imiter ce que nous ne comprenons même pas ? Pour autant il faut bien admettre que les victoires du Deep Learning ont bien souvent une part plus ou moins importante de biomimétisme, e.g. le neurone artificiel, les CNNs, le mécanisme d'attention, le dropout, etc. Ces tentatives de coller au fonctionnement du cerveau ne sont donc pas stériles, mais pâtissent d'un manque de compréhension de la cognition humaine, et aussi peut-être d'un intérêt insuffisant des chercheurs en Deep Learning pour cette matière pourtant jumelle à la leur.

  
> **Quand le Deep Learning aide à comprendre le cerveau**  
> Le Deep Learning a encore beaucoup à tirer de la compréhension du cerveau humain. Mais le contraire est aussi vrai. Dans cet [article](https://www.nature.com/articles/s41467-021-26751-5) paru dans Nature, un ANN ($\beta$-VAE) est utilisé pour étudier l'organisation des neurones codant pour les visages, i.e., la représentation neuronale des visages, chez le singe macaque. (Notez l'existence d'un "neurone de la frange" !). Le résultat ? Il est possible de reconstruire le visage vu par le singe en lisant sa réponse neuronale. Pas si loin de la science-fiction.
> Il est remarquable d'obtenir à l'aide d'un ANN des résultats similaires à ceux d'un réseau de neurones biologique alors que, comme on l'a vu, ils ne partagent finalement que peu de caractéristiques. Les études mêlant ces approches sont d'ailleurs de plus en plus nombreuses.


## Conclusion

On ne peut pas parler d'éloignement en cela que les ANNs n'ont jamais vraiment été proches du fonctionnement du cerveau. Les approches biomimétiques ont jusqu'ici connu des succès mitigés, ce qui doit être mis en perspective avec la différence de moyens alloués à leur développement. 363 publications pour les Spiking Neural Networks sur arXiv.org en 2022 contre près de 16 000 pour l'ensemble du domaine. Comme pour les CNNs il y a une dizaine d'années, l'introduction d'[hardwares specialisés](https://arxiv.org/ftp/arxiv/papers/2005/2005.01467.pdf) devrait permettre une accélération de la recherche sur ce domaine prometteur. En parallèle, le développement du Deep Learning ouvre de nouvelles perspectives pour l'étude du cerveau humain, en lui offrant des [outils](https://www.pnas.org/doi/10.1073/pnas.2200800119) aussi bien expérimentaux que théoriques.
