# Caroline de Pourtalès, Ingénieure d'étude en Intelligence artificielle

## Qui suis-je ? 

Bonjour !
Tout d'abord, merci pour votre visite sur ce site. Je me présente : Caroline de Pourtalès, ingénieure généraliste diplômée de l'IMT Atlantique, titulaire d'un double-diplôme de master en Data Science à Polytech Nantes. Actuellement, je travaille depuis 3 ans au CNRS en tant qu’ingénieure d’étude en intelligence artificielle au sein du réseau PNRIA (https://www.ins2i.cnrs.fr/fr/reseau-des-ingenieurs-cnrs-du-programme-national-de-recherche-en-intelligence-artificielle-pnria).

En dehors de mon travail, j'ai de nombreux hobbies : tricot, couture, voyages... Ce qui m'amuse particulièrement en ce moment, c'est d'animer des patrons de couture grâce à des modèles Image-to-Video. Je suis de nature très curieuse et, croyez-moi, ce genre de passe-temps apprend la patience !

Autodidacte par nature, je suis aussi sortie un peu de mon côté créatif dernièrement pour m’intéresser à la biologie. Par exemple, j’ai lu Tout ce que vous avez toujours voulu savoir sur le blob sans jamais oser le demander d’Audrey Dussutour, ainsi que Évolution, écologie et pandémies de Samuel Alizon. Ces lectures m'ont poussé à explorer davantage la bioinformatique. Merci aux éditions Dunod pour leurs livres clairs et concis ! J’espère bientôt obtenir un projet PNRIA dans ce domaine afin de mettre à contribution ces nouvelles connaissances.

Mon intérêt pour la biologie n'est pas nouveau, je m'intéresse énormément aux liens entre médecine et intelligence artificielle et je souhaite continuer à développer des solutions à long terme pour aider les médecins. 

## Mes compétences

Jusqu'aujourd'hui j'ai participé à 7 projets de recherche. Sur chaque projet, je suis intervenue dans l'état de l'art, l'implémentation, l'entraînement et la formation des équipes à l'utilisation de l'outil.

- **Langages informatiques** : Python, R, bases de C++  
- **Bases de données** : SQL, MongoDB, SQLite  
- **Visualisation** : bokeh, Dash (Plotly), matplotlib, RShiny  

- **Libraries de Machine Learning / Deep Learning** : Scikit-learn, Pytorch (torch, torch_geometric, torch_lightning), Keras, Spacy, nltk, transformers  
- **Entraînement d'IA** : OpenStack (cloud computing), SLURM  
- **Traitement du langage naturel** : LLMs, application aux Graph Neural Networks  
- **Apprentissage par renforcement** : Q-learning, Actor-Critic  
- **Traitement d'images** : Open-CV, scikit-image, réseaux de neruones : classification, régression, détection d’objets, fine-tuning (ResNet, Yolo, Faster-RCNN)  

- **Outil de collaboration** : Trello, Git, GitHub, GitLab  
- **DevOps** : Docker  

## Détail de certains projets

### *Diagnostic de la Leucémie Myéloïde Aiguë* 

Dans le cadre d’une collaboration avec le réseau PNRIA et le Cancéropole de Toulouse, un outil de diagnostic a été développé pour améliorer l’analyse d’images médicales et la prise de décision clinique. Ce projet s’appuie sur des technologies avancées en intelligence artificielle et en traitement d’images, intégrées dans un pipeline Python.


**Les données :**
Pour le moment, le projet utilise uniquement des images de moelle osseuse, mais l’objectif à terme est d’intégrer également des données tabulaires afin de réaliser des analyses de survie.


**Les étapes du pipeline :**
- Filtrage des zones d’intérêt
    Les images, très grandes et lourdes, ne peuvent pas être analysées pixel par pixel. Il est donc nécessaire de sélectionner des régions d’intérêt. Nous avons choisi de nous concentrer sur les zones présentant une densité suffisante de cellules : ni trop vide, ni trop dense au point de rendre les cellules indistinguables.

    Pour cela, les images sont ouvertes à l’aide de OpenSlide, qui permet d’obtenir des vues multi-résolution grâce à des cadrillages de différents niveaux de zoom. Le filtrage est ensuite réalisé à l’aide de filtres OpenCV, combinés à une technique de clustering basée sur k-means pour identifier les régions pertinentes.

- Détection des cellules avec un fine-tuning de Mask-RCNN
    Pour détecter les cellules, nous utilisons Mask-RCNN, un modèle d’apprentissage profond performant pour la segmentation d’objets dans les images. Mask-RCNN repose sur deux étapes principales : la génération de propositions de régions (Region Proposal Network) et la classification/segmentation de ces régions. Après un fine-tuning spécifique sur les données de moelle osseuse, nous avons obtenu d’excellents résultats de segmentation, avec une détection précise des contours et des zones des cellules.

- Classification des cellules avec PyRadiomics
    Une fois les cellules détectées, leur classification est effectuée à l’aide de PyRadiomics, un outil qui permet d’extraire des caractéristiques avancées (texture, forme). 

- Explicabilité pour un retour du diagnostic aux médecins
    Afin de rendre les résultats compréhensibles et exploitables par les médecins, nous avons intégré des outils d’explicabilité, notamment SHAP (SHapley Additive exPlanations). Ceux-ci permettent de fournir des explications claires sur les prédictions du modèle. Des outils de visualisation interactifs ont également été développés pour faciliter l’interprétation des résultats.
