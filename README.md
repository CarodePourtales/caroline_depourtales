# Caroline de Pourtalès, Ingénieure d'étude en Intelligence artificielle

## Qui suis-je ? 

Bonjour !
Tout d'abord, merci pour votre visite sur ce site. Je me présente : Caroline de Pourtalès, ingénieure généraliste diplômée de l'IMT Atlantique, titulaire d'un double-diplôme de master en Data Science à Polytech Nantes. Actuellement, je travaille depuis 3 ans au CNRS en tant qu’ingénieure d’étude en intelligence artificielle au sein du réseau PNRIA (https://www.ins2i.cnrs.fr/fr/reseau-des-ingenieurs-cnrs-du-programme-national-de-recherche-en-intelligence-artificielle-pnria).

En dehors de mon travail, j'ai de nombreux hobbies : tricot, couture, voyages... 

Je suis très curieuse et autodidacte, ainsi en ce moment, je m'intéresse à la biologie. Par exemple, j’ai lu "Tout ce que vous avez toujours voulu savoir sur le blob sans jamais oser le demander" d’Audrey Dussutour, ainsi que "Évolution, écologie et pandémies" de Samuel Alizon. Ces lectures m'ont poussé à explorer davantage la bioinformatique. Merci aux éditions Dunod pour leurs livres clairs et concis ! J’espère bientôt obtenir un projet PNRIA dans ce domaine afin de mettre à contribution ces nouvelles connaissances.

Mon intérêt pour la biologie n'est pas nouveau, je m'intéresse énormément aux liens entre médecine et intelligence artificielle et je souhaite continuer à développer des solutions à long terme pour aider les médecins. 

## Mes compétences

Jusqu'aujourd'hui j'ai participé à 9 projets de recherche. Sur chaque projet, je suis intervenue dans l'état de l'art, l'implémentation, l'entraînement et la formation des équipes à l'utilisation de l'outil.

- **Langages informatiques** : Python, R, bases de C++  
- **Bases de données** : SQL, MongoDB, SQLite  
- **Visualisation** : Bokeh, Dash (Plotly), matplotlib, RShiny  

- **Libraries de Machine Learning / Deep Learning** : Scikit-learn, Pytorch (torch, torch_geometric, lightning), Keras, Spacy, nltk, transformers (HuggingFace)
- **Entraînement d'IA** : OpenStack (cloud computing), SLURM  
- **Traitement du langage naturel** : LLMs, application aux Graph Neural Networks  
- **Apprentissage par renforcement** : Q-learning, Actor-Critic  
- **Traitement d'images** : Open-CV, scikit-image, réseaux de neurones : classification, régression, détection d’objets, fine-tuning (ResNet, Yolo, Faster-RCNN)  

- **Outil de collaboration** : Trello, GitHub, GitLab  
- **DevOps** : Docker, CI/CD

## Détail de certains projets

### *Diagnostic de la Leucémie Myéloïde Aiguë* 

Dans le cadre d’une collaboration avec le réseau PNRIA et le Cancéropole de Toulouse, un outil de diagnostic a été développé pour améliorer l’analyse d’images médicales et la prise de décision clinique. Ce projet s’appuie sur des technologies avancées en intelligence artificielle et en traitement d’images, intégrées dans un pipeline Python.

- **Filtrage des zones d’intérêt**
    Les images, très grandes et lourdes, ne peuvent pas être analysées pixel par pixel. Il est donc nécessaire de sélectionner des régions d’intérêt. Nous avons choisi de nous concentrer sur les zones présentant une densité suffisante de cellules : ni trop vide, ni trop dense au point de rendre les cellules indistinguables.

    Pour cela, les images sont ouvertes à l’aide de OpenSlide, qui permet d’obtenir des vues multi-résolution grâce à des cadrillages de différents niveaux de zoom. Le filtrage est ensuite réalisé à l’aide de filtres OpenCV, combinés à une technique de clustering basée sur k-means pour identifier les régions pertinentes.

- **Détection des cellules avec un fine-tuning de Mask-RCNN**
    Pour détecter les cellules, nous utilisons Mask-RCNN, un modèle d’apprentissage profond performant pour la segmentation d’objets dans les images. Mask-RCNN repose sur deux étapes principales : la génération de propositions de régions (Region Proposal Network) et la classification/segmentation de ces régions. Après un fine-tuning spécifique sur les données de moelle osseuse, nous avons obtenu d’excellents résultats de segmentation, avec une détection précise des contours et des zones des cellules.

- **Classification des cellules avec PyRadiomics**
    Une fois les cellules détectées, leur classification est effectuée à l’aide de PyRadiomics, un outil qui permet d’extraire des caractéristiques avancées (texture, forme). 

- **Explicabilité pour un retour du diagnostic aux médecins**
    Afin de rendre les résultats compréhensibles et exploitables par les médecins, nous avons intégré des outils d’explicabilité, notamment SHAP (SHapley Additive exPlanations). Ceux-ci permettent de fournir des explications claires sur les prédictions du modèle. Des outils de visualisation interactifs ont également été développés pour faciliter l’interprétation des résultats.

*Références*  
Bennis A, Leleux P, Canali A, Pourtales CD, Mouysset S, Simoncini D, Brousset P, Frenois FX, Recher C, Alliot JM, Rieu JB, Bertoli S. PB1764: SEGMENTATION AND CLASSIFICATION OF BONE MARROW CELLS FROM MULTI-PRECISION NUMERIZATION OF BONE MARROW SMEARS (BMS) FROM PATIENTS WITH ACUTE MYELOID LEUKEMIA (AML) USING AI TECHNIQUES. Hemasphere. 2023 Aug 8;7(Suppl ):e5127496. doi: 10.1097/01.HS9.0000973912.51274.96. PMCID: PMC10430235.

### *Projet ‘AUTOFILL’ pour le PEPR TooFast avec le CEA"* : 
Génération de signaux de caractérisation de nanomatériaux.  
Développement d’un **Pair-Variational Autoencoder** pour la traduction d’un signal dans une autre modalité.

Le projet AUTOFILL vise à **générer** et **traduire** automatiquement des signaux expérimentaux de caractérisation de nanomatériaux entre différentes modalités (par exemple, SAXS ↔ LES). Pour cela, nous avons implémenté un modèle inspiré du papier *Pair-Variational Autoencoders (PairVAE) for Linking and Cross-Reconstruction*.

- **Architecture à double VAE couplé** : deux autoencodeurs variationnels distincts (un pour chaque modalité) partagent un espace latent commun.
    - Chacun des VAE est d'abord entraîné indépendamment sur sa modalité. Chaque encodeur (modalité A ou B) apprend ainsi à projeter le signal observé `x_A` ou `x_B` dans un vecteur latent `z`.
    - Ensuite, on les couple avec un même vecteur latent `z` alimentant les deux décodeurs, permettant à chacun de **reconstruire** à la fois sa modalité d’origine et, via un mécanisme de cross-reconstruction, la modalité opposée.
    - L’objectif est de forcer la **cohérence croisée** : à partir d’un signal `x_A`, l’encodeur A génère `z`, puis le décodeur B doit produire un signal `x̂_B` réaliste dans la modalité B, et vice-versa.

- **Fonctions de perte** :  
  1. **Reconstruction intra-modale** : chaque décodeur minimise la divergence entre `x_A` et `x̂_A` (resp. `x_B` et `x̂_B`).
  2. **Cross-reconstruction** : le décodeur de chaque modalité doit également reconstruire la modalité opposée (`x̂_{B|A}` et `x̂_{A|B}`), ce qui renforce l’alignement des représentations latentes.
  3. **Régularisation KL** : les distributions latentes apprises sont contraintes à rester proches d’une distribution prior (gaussienne), garantissant que `z` encode efficacement l’information commune aux deux signaux.
  4. **Similarity Loss** avec la **Barlow-Twin loss** pour rapprocher les espaces latents.

- **Entraînement et résultats** :  
  - **Données simulées** : génération de jeux de signaux synthétiques pour chaque modalité.
  - **Amélioration de la précision de traduction** : comparaison des signaux reconstruits en cross-modalité (par exemple, LES reconstruit depuis un spectre SAXS) versus méthodes classiques de correspondance un à un.


*Références*  
1. G. Hajizadegan et al., “Pair-Variational Autoencoders for Linking and Cross-Reconstruction,” *JACS Au*, 2023. 

### *Projet ‘SARU’  en Éthologie et Primatologie* :  
Étude automatisée des comportements sociaux de macaques japonais à partir d’enregistrements vidéo.  
- **Détection et classification** des individus dans les séquences vidéos à l’aide de YOLO et YOLO-CLS.
    - Utilisation de la bibliothèque [Ultralytics YOLO](https://github.com/ultralytics/ultralytics) pour la détection d’instances de macaques dans chaque image.  
    - Jeu de données annoté manuellement (bords de boîtes englobantes autour des macaques) pour le fine-tuning du modèle YOLOv11.  
    - Application de techniques d’**augmentation de données** durant l’entraînement
- **Caractérisation fine des postures et comportements** via l’outil LabGym, utilisé pour analyser les dynamiques corporelles et interactions sociales.  
- **Tracking multi-individus** robuste avec BOTSort, permettant de suivre précisément chaque primate au fil du temps, malgré les occlusions et déplacements complexes.
    - Adoption de **BOTSort**, un algorithme d’association en temps réel reposant sur les résultats de YOLO et une **métrique appearance-based** :  
    - Association des détections sur plusieurs frames consécutives en utilisant à la fois la position prévue (via Kalman Filter) et un descripteur visuel (histogramme de couleurs du pelage) pour distinguer les macaques semblables.  
    - Gestion des occlusions partielles et totales :  
    - Si un individu disparaît temporairement (sous un obstacle ou dans l’ombre), BOTSort maintient la trace du même ID jusqu’à réapparition, grâce à la prédiction du déplacement.  
    - Réidentification rapide même lorsque plusieurs singes se croisent ou se chevauchent.  
    - Résultat : suivi continu (bounding box + ID unique) de chaque primate sur plusieurs minutes, permettant de reconstruire des **trajectoires individuelles** (distance parcourue, zones d’activité préférentielles) et des **interactions sociales spatialisées** (proximité, affinités de groupe).


### *Projet ‘LibSpecDL’ en médecine et biologie* : 
Développement d’un pipeline pour la **quantification automatisée des signaux de spectroscopie par résonance magnétique (MRS)**.  
- **Simulation de spectres** à partir de bases de données de métabolites, pour générer des signaux synthétiques réalistes adaptés à l'entraînement de modèles.  Utilisation de FS-MRS.
- Utilisation de **régressions multivariées** pour estimer les concentrations métaboliques à partir des spectres expérimentaux.  
- Objectif : améliorer la robustesse et la précision du diagnostic par MRS, tout en réduisant la dépendance à l’expertise humaine dans l’interprétation des signaux.

