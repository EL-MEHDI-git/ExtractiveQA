# ExtractiveQA-CamemBert

Notre objectif dans cette partie s’étend à concevoir des architectures pour l’approche de question-answering basée sur un contexte (Context-Based). 

Le question-answering est une tâche du traitement du langage naturel qui a connu un essor considérable après la naissance des Transformers. De nombreux modèles de langage pré-entraînés se sont avérés incroyablement efficaces pour répondre à des questions extractives y compris le BERT et ses variants. Dans notre cas, nous allons utiliser le modèle CamemBERT, la version française du BERT, au cœur de notre architecture. Ensuite, nous allons opter pour des hybridations utilisant le Camembert avec le LSTM et le BiLSTM, et puis comparer les différents modèles de langage proposés dans le but de déterminer si l’ajout de plus de bidirectionnalité peut améliorer les performances du modèle.
Le modèle CamemBERT prend la question et le passage en entrée comme une seule séquence empaquetée. Les embeddings d'entrée sont la somme des embeddings de tokens et des embeddings de segments. L'entrée est traitée de la manière suivante avant d'entrer dans le modèle :

-	Token embeddings : Un token [CLS] est ajouté aux tokens de mots en entrée au début de la question et un token [SEP] est inséré à la fin de la question et du paragraphe.
-	Segment embeddings : Un marqueur indiquant la phrase A ou la phrase B est ajouté à chaque token. Cela permet au modèle de faire la distinction entre la question et le passage associé.

Le modèle CamemBERT fait passer les embeddings d’entrée par la même couche d’attention qui donne à son tour une matrice d’attention affectant un score exprimant la force de liaison entre un mots et les autres mots de la même séquence. La sortie résultante du Camembert passe par une couche dropout et puis transmise à une couche entièrement connectée, pour au final avoir l’indice de départ et de fin de la réponse extraite du passage.

Tableau comparatif des résultats:

![image](https://github.com/EL-MEHDI-git/ExtractiveQA-CamemBert/assets/66147690/516f0b9c-3a73-4954-9b63-75902901d916)

## Synthèse :
Dans l’approche d’extractive QA, nous avons entamé par ajuster le modèle camembert pré-entrainé sur la tâche (downstream task) de question answering en utilisant le dataset FQuAD version 1.0 et nous avons achevé un score F1 de 79.37%. Par la suite nous avons alimenté le camembert par des couches de réseau neuronal récurrent, le LSTM et le Bi-LSTM où on a obtenu respectivement des scores F1 de 79.99% et 79.81%. On remarque que les modèles hybridés ont pu surpasser le score atteint par le camembert seul. Certes qu’on n’est pas arrivé à achever les performances de pointes de l’état de l’art, et cela pour plusieurs raisons, à savoir, les travaux ont été effectués sur la version 1.1 du dataset FQuAD qui contient plus de données d’entrainement et de validation, mais nos modèles donnent souvent de bon résultat sur n’importe quel article français.
