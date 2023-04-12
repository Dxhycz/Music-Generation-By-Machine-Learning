# Music-Generation-By-Machine-Learning
# Ptolémée

Ptolémée est l'IHM pour les analyses de l'équipe DGEX DIGIT Données.

Pour plus d'informations, consulter la note de conception.

### Backend Python

Le développement requiert l'outil `poetry`, qui peut être installé avec `pip install poetry`.

Apres, on peut ouvrir un invite de command dans le dossier dans lequel on a cloné le repository git
et installer les dépendances Python avec `poetry install`.

Enfin, pour démarrer l'IHM, il faut utiliser le command `poetry run ptolemee run-server --reload`.
L'IHM sera disponible sur http://localhost:8123.

### Frontend NodeJS

Il faut commencer avec l'installation d'Angular. Les instructions sont disponibles sur le site officiel :
https://angular.io/guide/setup-local.

Après avoir ouvert un invite de command dans le sous-dossier `ptoapp_js`, on peut installer les dépendances 
JavaScript (Angular, ecc...) avec `npm install`.

Ensuite, il faut exporter certains modèles du backend vers le frontend avec `poetry run ptolemee gen-schemas`,
à la première compilation et à chaque fois ces modèles sont modifiés.

Enfin, on peut démarrer la version en développement du frontend, avec `ng serve`. 
Cette version sera disponible sur http://localhost:4200 et demande d'avoir ouvert aussi le backend Python.

### Distribution

Après avoir fait des "commits" git avec les modifications, on peut créer une nouvelle version de Ptolémee
avec le command `poetry run invoke release [major|minor|patch]` (major : version majeure, 1.1.3 -> 2.0.0 ;
minor : version mineure, 1.1.3 -> 1.2.0 ; patch : 1.1.3 -> 1.1.4). Ce command crée automatiquement un
commit git qui contient le nouveau pyproject.toml.

Avec `poetry run invoke build-exe`, on peut générer un fichier .exe avec Pyinstaller (idéal pour le
déploiement sur le serveur SNCF).

Pour aider le déploiement, le script `poetry run invoke build-and-deploy` positionne dans le dossier
C:\Deploiement le fichier .exe et les scripts .bat conçus pour aider le lancement de Ptolémée sur le
serveur (cronjob). En outre, le fichier .exe peut être distribué sur le Sharepoint d'équipe avec
`poetry run invoke build-and-distribute`.

### Documentation

[mkdocs](https://www.mkdocs.org) est utilisé pour la documentation. Après avoir fait `poetry
install` (voir step "Backend Python"), on peut lancer `poetry run mkdocs serve` pour visualiser la
doc.

La documentation est aussi disponible sur https://pto-metier.gitlab.io/ptolemee/.
