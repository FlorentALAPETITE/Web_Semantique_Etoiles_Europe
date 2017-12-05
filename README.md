# Web_Semantique_Etoiles_Europe
Projet Web Semantique M1 ALMA

Pour créer le graphe rdf à partir du .csv, executer la ligne de commande suivante :

     ./executeTarql.sh

Le résultat de la requête se trouve dans le fichier : "RDFGraph_Concours_Etoiles_Europes.ttl"

## Adaptation avec Jena Fuseki

Les inférences RDF se trouvent dans un fichier **jena-fuseki-3.4.0/run/databases/rules.rules**.

Pour lancer Jena Fuseki sur **localhost:3030**: 
```cd jena-fuseki-3.4.0
./fuseki-server --update
```

Seules les données du graphe de notre projet sont présentes à son lancement, il n'en est pas de même avec les données du groupe avec lequel nous nous sommes lié. Il vous faudra donc importer le fichier **graphAutreGroupe.ttl** dans fuseki, dans un autre graphe nommé par exemple **grapheAutreGroupe**.
De même, vous pouvez y importer l'ontologie OWL **ontology.owl**.
Les inférences sont éxécutées automatiquement.
