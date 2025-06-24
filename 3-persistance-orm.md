---
titre: Architecture micro-service
sous-titre: TP 5 - Premiers micro-services - La météo, ça coûte cher en bande passante !
auteur: Philippe 	extsc{Roussille}
theme: Warsaw
lang: fr-FR
section-titles: false
fontsize: 10pt
couleur-type-1: true
rendu-type: papier
rendu-logo: 3il
---

# État des lieux

(... contenu inchangé jusqu'aux questions ...)

# Questions de réflexion

## Sur la base de données

1. Pourquoi ajouter une base de données à un service météo aussi simple ? Est-ce justifié ?  
Oui, cela permet de garder en mémoire les réponses récentes et d’éviter de surcharger l’API externe.

2. Est-ce que chaque microservice devrait avoir sa propre base, ou peut-on les partager ?  
Chaque microservice devrait idéalement avoir sa propre base pour rester indépendant.

3. Que gagne-t-on (et que perd-on) en utilisant une base relationnelle plutôt qu'un fichier ou un dictionnaire Python ?  
On gagne en fiabilité, requêtes puissantes, et persistance. On perd un peu en simplicité et en vitesse d’accès brute.

4. Que permet une base comme MySQL que ne permet pas un fichier JSON ?  
Elle permet des recherches complexes, une gestion multi-utilisateur, des mises à jour fiables, et de la concurrence sécurisée.

5. Si on voulait partager cette météo avec d'autres services, la base est-elle une bonne interface ?  
Non, la base ne devrait pas être exposée directement. C’est mieux de passer par l’API du microservice.

6. Peut-on facilement sauvegarder/exporter les données ? Et les restaurer ?  
Oui, avec MySQL on peut facilement exporter en SQL ou CSV et restaurer avec des outils standards.

## Sur les performances et la scalabilité

7. Est-ce que l'ajout d'une BDD rend le service plus rapide ? Plus lent ?  
Cela peut le ralentir un peu, mais permet d’éviter des appels externes plus lents, donc c’est globalement un gain.

8. Que se passe-t-il si plusieurs clients envoient des requêtes simultanément ?  
La base gère cela sans problème, surtout avec un ORM qui organise les sessions proprement.

9. Peut-on mettre à jour une donnée météo sans recontacter l'API externe ?  
Oui, si la donnée est encore fraîche, on peut la réutiliser.

10. Est-ce qu'on peut interroger la météo d'hier ou de demain avec cette architecture ?  
Non, pas pour l’instant, car on ne stocke que les données actuelles. Il faudrait adapter le service pour ça.

# Questions de réflexion

1. Pourquoi voudrait-on éviter d'écrire directement des requêtes SQL à la main ?  
Pour éviter les erreurs, gagner du temps, et rendre le code plus lisible.

2. Que gagne-t-on en utilisant un ORM comme SQLAlchemy ?  
On peut manipuler la base avec du code Python classique, ce qui est plus pratique.

3. Est-ce que l’ORM vous empêche complètement d’accéder au SQL si besoin ?  
Non, on peut toujours écrire du SQL à la main si on veut.

4. Est-ce que le code Python devient plus clair ou plus opaque avec un ORM ?  
Il devient plus clair pour ceux qui connaissent l’ORM, mais plus opaque pour les débutants.

5. À quel moment l’ORM peut devenir un inconvénient ? (performances, complexité, etc.)  
Quand les requêtes deviennent trop complexes ou très nombreuses, cela peut ralentir l’application.
