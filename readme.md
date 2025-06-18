# Sujet

Igensia vous missionne pour l’aider à gérer et organiser ses sites internet. Vous devez donc créer une petite application en Python qui référence ses sites.


## Pour valider le module (C)

### Première étape

*Créez le fichier vide `list1.py`.*

Votre première application permettra de saisir une adresse et de lister l’ensemble des adresses.

L’interface doit être la suivante :

```
Saisir l’adresse du site : https://www.ipi-ecoles.com/
Liste des sites :
* https://www.ipi-ecoles.com/

Saisir l’adresse du site : https://notesipi.moncampusvirtuel.fr/login
Liste des sites :
* https://www.ipi-ecoles.com/
* https://notesipi.moncampusvirtuel.fr/login
```

*Enregistrez et conservez cette application dans le fichier `list1.py`.*

### Deuxième étape

*Créez le fichier `list2.py` avec le contenu de `list1.py`.*

La deuxième version de l’application permet d’associer un nom de site à l’URL.

L’interface doit être la suivante :

```
Saisir le nom du site : IPI
Saisir l’adresse du site : https://www.ipi-ecoles.com/
Liste des sites :
* IPI : https://www.ipi-ecoles.com/

Saisir le nom du site : Notes
Saisir l’adresse du site : https://notesipi.moncampusvirtuel.fr/login
Liste des sites :
* IPI : https://www.ipi-ecoles.com/
* Notes : https://notesipi.moncampusvirtuel.fr/login
```

*Enregistrez et conservez cette application dans le fichier `list2.py`.*

### Troisième étape

*Créez le fichier `list3.py` avec le contenu de `list2.py`.*

On vous demande ensuite de sauvegarder cette liste dans un fichier JSON appelé `sites.json`.

Lors du premier lancement de l’application, lorsque le fichier n’existe pas, l’interface doit être la suivante :

```
Pas de site enregistré.

Saisir le nom du site : IPI
Saisir l’adresse du site : https://www.ipi-ecoles.com/
Liste des sites :
* IPI : https://www.ipi-ecoles.com/

Saisir le nom du site : Notes
Saisir l’adresse du site : https://notesipi.moncampusvirtuel.fr/login
Liste des sites :
* IPI : https://www.ipi-ecoles.com/
* Notes : https://notesipi.moncampusvirtuel.fr/login
```

Lors du second lancement de l’application, lorsque le fichier existe, l’interface doit être la suivante :

```
Liste des sites :
* IPI : https://www.ipi-ecoles.com/
* Notes : https://notesipi.moncampusvirtuel.fr/login

Saisir le nom du site : Igensia
Saisir l’adresse du site : https://www.igensia-education.fr/
Liste des sites :
* IPI : https://www.ipi-ecoles.com/
* Notes : https://notesipi.moncampusvirtuel.fr/login
* Igensia : https://www.igensia-education.fr/
```

*Enregistrez et conservez cette application dans le fichier `list3.py`.*


## Pour aller plus loin (B)

*Créez le fichier `list4.py` avec le contenu de `list3.py`.*

On vous demande enfin de vérifier que l’adresse du site commence bien par `https`.

L’interface doit être la suivante :

```
Pas de site enregistré.

Saisir le nom du site : IPI
Saisir l’adresse du site : www.ipi-ecoles.com
L’adresse du site ne commence pas par 'https'.

Saisir le nom du site : IPI
Saisir l’adresse du site : https://www.ipi-ecoles.com/
Liste des sites :
* IPI : https://www.ipi-ecoles.com/

Saisir le nom du site : Igensia
Saisir l’adresse du site : http://www.igensia-education.fr/
L’adresse du site ne commence pas par 'https'.

Saisir le nom du site : Igensia
Saisir l’adresse du site : https://www.igensia-education.fr/
Liste des sites :
* IPI : https://www.ipi-ecoles.com/
* Igensia : https://www.igensia-education.fr/
```

*Enregistrez et conservez cette application dans le fichier `list4.py`.*


## Pour aller encore plus loin (A)

*Créez le fichier vide `monitor.py`*

Éblouie par votre travail, votre équipe vous demande d’aller plus loin et de monitorer les sites. Vous décidez donc de construire une nouvelle application qui lira le fichier `sites.json` contenant les sites, et qui affichera leur statut.

Pour vérifier le statut des pages d’accueil des sites, vous utilisez cette fonction :

```py
from urllib.request import HTTPErrorProcessor, build_opener

def open_url(url):
    class Processor(HTTPErrorProcessor):
        http_response = https_response = lambda self, request, response: response
    return build_opener(Processor).open(url)
```

```py
>>> response = open_url("https://www.ipi-ecoles.com/")
>>> print(response.status)
200
```

Vous devez d’abord supprimer la liste des sites `sites.json`, puis entrer les sites suivants avec `list4.py` :

- IPI : https://www.ipi-ecoles.com/
- Igensia : https://www.igensia-education.fr/
- Inconnu : https://www.igensia-education.fr/inconnu

L’interface de votre application `monitor.py` est alors :

```
Test de IPI (https://www.ipi-ecoles.com/)
OK (Code 200)

Test de Igensia (https://www.igensia-education.fr/)
OK (Code 200)

Test de Inconnu (https://www.igensia-education.fr/inconnu)
ERROR (Code 404)
```

Pour simplifier, le site est considéré comme fonctionnel si l’on a un statut 200, et dysfonctionnel pour tous les autres statuts.

À l’aide de la bibliothèque `time`, vous pouvez demander à votre programme d’attendre.

```py
>>> from time import sleep
>>> sleep(5)  # Wait for 5 seconds
```

Vous modifiez donc votre programme pour qu’il vérifie les sites toutes les minutes.

```
Test de IPI (https://www.ipi-ecoles.com/)
OK (Code 200)

Test de Igensia (https://www.igensia-education.fr/)
OK (Code 200)

Test de Inconnu (https://www.igensia-education.fr/inconnu)
ERROR (Code 404)

Attente d’une minute.

Test de IPI (https://www.ipi-ecoles.com/)
OK (Code 200)

Test de Igensia (https://www.igensia-education.fr/)
OK (Code 200)

Test de Inconnu (https://www.igensia-education.fr/inconnu)
ERROR (Code 404)

Attente d’une minute.
```

*Enregistrez cette application dans le fichier `monitor.py`.*



# Consignes

Le but de ce devoir est d’évaluer votre compréhension du langage. Le niveau attendu est celui d’une personne avec très peu d’expérience sur Python.

Vous rendrez votre travail par mail (guillaume.asr@yabz.fr) avec vos deux noms et tous vos fichiers en pièces jointes (si besoin dans une archive). Vérifiez auprès de moi que j’ai votre rendu avant de partir.

**Tout le code doit être réalisé avec le code vu en cours et les exemples donnés dans le sujet.**

Ce devoir, en particulier sa première partie (C), peut être réalisé en bien moins de temps que les 2 heures maximales. Prenez votre temps, avancez étape par étape, vérifiez et revérifiez votre rendu.

J’évalue durant ce devoir votre capacité à réfléchir pour résoudre des problèmes, pas votre capacité à écrire du code, ni à utiliser des outils, ni à faire appel à des collègues. Je prends beaucoup en compte le soin apporté au code, votre rigueur, et l’honnêteté de votre travail :

- **Vos fichiers doivent fonctionner sans modification de ma part.** Mettez un commentaire si vous savez que ce n’est pas le cas.
- Essayez d’avoir **exactement la même interface** que celle que je vous demande.
- **Nommez correctement vos variables,** suivez les bonnes pratiques vues dans les exemples de code de la documentation.
- Abstenez-vous de copier-coller du code trouvé sur internet ou partagé par quelqu’un d’autre dans la classe.
- Vous devez garder une continuité entre les différentes versions d’un script. Vous pouvez commenter vos fichiers pour expliquer les évolutions entre chaque version.
- N’hésitez pas à indiquer avec des commentaires les bouts de code que vous trouvez étranges ou moches, ou certaines de vos réflexions.

Pour valider le module, il faut réaliser la première partie (C) **parfaitement**. Si vous avez des doutes sur la qualité de votre rendu pour la partie (C), vous pouvez faire la partie (B), mais je note avant tout la qualité du rendu, pas la quantité. Ne faites pas la dernière partie (A) si vous n’avez pas une bonne maîtrise des deux parties précédentes.

Bon courage !
