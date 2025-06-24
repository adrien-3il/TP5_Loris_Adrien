---
titre: Architecture micro-service
sous-titre: TP 5 - Premiers micro-services - Faites des blagues
auteur: Philippe 	extsc{Roussille}
theme: Warsaw
lang: fr-FR
section-titles: false
fontsize: 10pt
couleur-type-1: true
rendu-type: papier
rendu-logo: 3il
---

# Contexte

> 2023. Roger et Ginette, responsables informatiques historiques de l'usine CanaDuck, préparent leur départ en retraite. Pour assurer la continuité de l'infrastructure numérique de l'entreprise et transmettre un peu de leur savoir à Lucie et Matthieu, leurs enfants bientôt en DUT (eh oui, ça passe vite), ils ont lancé un chantier de modernisation : tout passer en microservices.

Premier élément migré : le générateur de blagues internes. Cette fonction, jadis embarquée dans un vieux script console, doit devenir un **microservice indépendant** et réutilisable.

# Objectifs pédagogiques

Dans ce TP, nous allons commencer à implémenter la vision microservice : **donner vie à de petites fonctionnalités**, en les rendant **autonomes**, **réutilisables**, et **indépendantes**. Plutôt qu'un gros service qui fait tout, chaque service est responsable d'une seule chose. Cela rend le système plus souple, plus modulaire, et plus facile à maintenir.

# Questions de compréhension

Avant de parler microservices, posons-nous quelques questions simples :

## Pourquoi faire des petits services ?

1. Pourquoi voudrait-on **diviser** un gros service web en plusieurs morceaux plus petits ?  
Parce que cela rend le système plus simple à comprendre, à modifier, à tester, et à faire évoluer.

2. Imaginez que vous travaillez sur un gros projet. Que se passe-t-il si vous devez modifier une seule fonctionnalité ? Est-ce facile ? Risqué ?  
C’est risqué car une modification peut casser autre chose. Ce n’est pas facile car tout est mélangé.

3. Peut-on confier un petit service à une autre équipe ou un autre développeur sans qu'il ait besoin de connaître tout le reste ?  
Oui, c’est l’avantage. Un service bien séparé peut être géré de façon autonome.

4. Que se passe-t-il si une partie tombe en panne ? Peut-on réparer sans tout redémarrer ?  
Oui, si un microservice tombe, on peut le redémarrer sans toucher aux autres.

5. Avez-vous déjà vu ou utilisé un site ou une appli qui semblait "modulaire" ?  
Oui, par exemple un site avec des parties indépendantes comme la messagerie, les notifications ou les paiements.

## Comment découper un service ?

6. Sur quels critères peut-on séparer un gros service en plusieurs petits ?  
On peut découper par fonctionnalité, par domaine métier ou selon les données manipulées.

7. Faut-il découper par fonctionnalité (ex : blague, météo, cantine...) ? Par type de donnée ? Par public cible ?  
Il vaut mieux découper par fonctionnalité, car c’est plus logique et pratique pour les utilisateurs et les développeurs.

8. À partir de combien de lignes de code ou de routes HTTP faut-il envisager un découpage ?  
Il n’y a pas de nombre exact, mais dès que ça devient difficile à maintenir ou trop gros, il faut penser au découpage.

9. Le découpage doit-il être figé ou peut-il évoluer ?  
Il peut évoluer selon les besoins, la croissance du projet ou les retours d’expérience.

# Le premier micro-service

## Spécifications fonctionnelles

### Endpoints à implémenter

#### `GET /joke`

* Renvoie une blague aléatoire
* Réponse attendue (JSON) :

```json
{ "joke": "Où se cachent les canards ? Dans le coin coin coin." }
```

#### `POST /joke`

* Ajoute une nouvelle blague au service
* Corps de requête (JSON) :

```json
{ "joke": "Que dit un canard qui s'est perdu? Coin !" }
```

* Le champ `joke` est obligatoire et doit faire au moins 10 caractères.
* Réponse en cas de succès : code HTTP `201 Created`
* Réponse en cas d'erreur : code HTTP `400 Bad Request` + message JSON

#### Données

Voici quelques exemples de blagues que vous pouvez intégrer à votre liste initiale :

```json
[
  { "joke": "Pourquoi un canard est toujours à l'heure ? Parce qu'il est dans l'étang." },
  { "joke": "Quel est le jeu de cartes préféré des canards ? La coin-che." },
  { "joke": "Qu'est-ce qui fait Nioc nioc? Un canard qui parle en verlan." },
  { "joke": "Comment appelle-t-on un canard qui fait du DevOps ? Un DuckOps." }
]
```

* Ces blagues peuvent être codées en dur dans une liste Python.
* Vous pouvez les enrichir librement (j'ai probablement raté une longue carrière d'humoriste).
* Blagues stockées en **mémoire** (liste Python)

... (le reste du fichier reste inchangé)
