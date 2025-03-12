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
+ https://www.ipi-ecoles.com/

Saisir l’adresse du site : https://notesipi.moncampusvirtuel.fr/login
Liste des sites :
+ https://www.ipi-ecoles.com/
+ https://notesipi.moncampusvirtuel.fr/login
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
+ IPI : https://www.ipi-ecoles.com/

Saisir le nom du site : Notes
Saisir l’adresse du site : https://notesipi.moncampusvirtuel.fr/login
Liste des sites :
+ IPI : https://www.ipi-ecoles.com/
+ Notes : https://notesipi.moncampusvirtuel.fr/login
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
+ IPI : https://www.ipi-ecoles.com/

Saisir le nom du site : Notes
Saisir l’adresse du site : https://notesipi.moncampusvirtuel.fr/login
Liste des sites :
+ IPI : https://www.ipi-ecoles.com/
+ Notes : https://notesipi.moncampusvirtuel.fr/login
```

Lors du second lancement de l’application, lorsque le fichier existe, l’interface doit être la suivante :

```
Liste des sites :
+ IPI : https://www.ipi-ecoles.com/
+ Notes : https://notesipi.moncampusvirtuel.fr/login

Saisir le nom du site : Igensia
Saisir l’adresse du site : https://www.igensia-education.fr/
Liste des sites :
+ IPI : https://www.ipi-ecoles.com/
+ Notes : https://notesipi.moncampusvirtuel.fr/login
+ Igensia : https://www.igensia-education.fr/
```

*Enregistrez et conservez cette application dans le fichier `list3.py`.*

### Quatrième étape

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
+ IPI : https://www.ipi-ecoles.com/

Saisir le nom du site : Igensia
Saisir l’adresse du site : http://www.igensia-education.fr/
L’adresse du site ne commence pas par 'https'.

Saisir le nom du site : Igensia
Saisir l’adresse du site : https://www.igensia-education.fr/
Liste des sites :
+ IPI : https://www.ipi-ecoles.com/
+ Igensia : https://www.igensia-education.fr/
```

*Enregistrez et conservez cette application dans le fichier `list4.py`.*


## Pour aller plus loin (B)

*Créez le fichier vide `monitor1.py`*

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

L’interface de votre application `monitor1.py` est alors :

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

*Enregistrez et conservez cette application dans le fichier `monitor1.py`.*


## Pour aller encore plus loin (A)

*Créez le fichier `monitor2.py` avec le contenu de `monitor1.py`, et créez le fichier vide `website.py`.*

Votre dernière mission consiste à stocker le résultat de ce monitoring. Enregistrez dans un fichier `monitoring.json` chaque vérification, en stockant :

- L’URL testée
- Le jour et l’heure
- Le code de statut
- Le temps de réponse de la requête HTTP
- Le nom du serveur HTTP

Les données de ce fichier sont conservées à chaque lancement de `monitor2.py`.

Pour `monitor2.py`, vous avez seulement besoin de `datetime` en plus des bibliothèques déjà utilisées.

*Enregistrez et conservez cette application dans le fichier `monitor2.py`.*

Vous créez ensuite dans `website.py` un site internet permettant de voir le résultat de ce monitoring. À chaque requête à la racine de ce site, vous affichez le résultat suivant :

```html
<h1>MonitorIPI</h1>

<h2 style="color: green">IPI</h2>
<table>
  <thead>
    <tr> <th>Date et heure</th> <th>Statut</th> <th>Temps de réponse</th> </tr>
  </thead>
  <tbody>
    <tr style="color: green"> <td>21/12/2025 14:32:22</td> <td>200</td> <td>1.2293s</td> </tr>
    <tr style="color: green"> <td>21/12/2025 14:31:20</td> <td>200</td> <td>0.9232s</td> </tr>
    <tr style="color: red">   <td>21/12/2025 14:30:17</td> <td>500</td> <td>0.9232s</td> </tr>
  </tbody>
</table>

<h2 style="color: green">Igensia</h2>
<table>
 […]
</table>

<h2 style="color: red">Inconnu</h2>
<table>
 […]
</table>
```

Les résultats sont groupés par site, dans l’ordre décroissant. La couleur des lignes dépend du statut (200 est vert, les autres sont rouges). La couleur du nom du site est celle du statut le plus récent pour ce site.

Lorsque l’application `monitor2.py` fonctionne, elle met à jour le fichier `monitoring.json` à chaque vérification. Le site `website.py` lit ce fichier à chaque requête qu’il reçoit, il affiche donc les données à jour à chaque rafraîchissement.

Pour `website.py`, vous avez seulement besoin de `http.server` en plus des bibliothèques déjà utilisées.

Vous devez vous appuyer sur cette base de code :

```py
from http.server import BaseHTTPRequestHandler, HTTPServer

class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.end_headers()
        text = "<h1>MonitorIPI</h1>"
        self.wfile.write(text.encode("latin-1"))

HTTPServer(("", 8000), Handler).serve_forever()
```

Lorsque vous exécutez ce programme, vous pouvez aller sur `http://localhost:8000/` sur votre navigateur.

*Enregistrez et conservez cette application dans le fichier `website.py`.*

# Consignes

Le but de ce devoir est d’évaluer votre compréhension du langage. Le niveau attendu est celui d’une personne avec quelques jours d’expérience sur Python.

Vous rendrez votre travail par mail (guillaume.tsa@yabz.fr) avec tous vos fichiers en pièces jointes (si besoin dans une archive). Vérifiez auprès de moi que j’ai votre rendu avant de partir.

**Tout le code des deux premières parties (C et B) doit être réalisé avec le code vu en cours et les exemples donnés dans le sujet.** Le code de la partie A nécessite uniquement la lecture supplémentaire des modules de la bibliothèque standard proposés.

Ce devoir, en particulier sa première partie (C), peut être réalisé en bien moins de temps que les 3 heures maximales. Prenez votre temps, avancez étape par étape, vérifiez et revérifiez votre rendu.

J’évalue durant ce devoir votre capacité à réfléchir pour résoudre des problèmes, pas votre capacité à écrire du code, ni à utiliser des outils, ni à faire appel à des collègues. Je prends beaucoup en compte le soin apporté au code, votre rigueur, et l’honnêteté de votre travail :

- **Vos fichiers doivent fonctionner sans modification de ma part.** Mettez un commentaire si vous savez que ce n’est pas le cas.
- Essayez d’avoir **exactement la même interface** que celle que je vous demande.
- **Nommez correctement vos variables,** suivez les bonnes pratiques vues dans les exemples de code de la documentation.
- Évitez de copier-coller du code trouvé sur internet ou partagé par quelqu’un d’autre dans la classe.
- Vous devez garder une continuité entre les différentes versions d’un script. Vous pouvez commenter vos fichiers pour expliquer les évolutions entre chaque version.
- N’hésitez pas à indiquer avec des commentaires les bouts de code que vous trouvez étranges ou moches, ou certaines de vos réflexions.

Pour valider le module, il faut réaliser la première partie (C) **parfaitement**. Si vous avez des doutes sur la qualité de votre rendu pour la partie (C), vous pouvez faire la partie (B), mais je note avant tout la qualité du rendu, pas la quantité. Ne faites pas la dernière partie (A) si vous n’avez pas une bonne maîtrise des deux parties précédentes.

Bon courage !
