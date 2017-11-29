# Web_Semantique_Etoiles_Europe
Projet Web Semantique M1 ALMA

Pour créer le graphe rdf à partir du .csv, executer la ligne de commande suivante :

     ./executeTarql.sh

Le résultat de la requête se trouve dans le fichier : "RDFGraph_Concours_Etoiles_Europes.ttl"

## Adaptation avec Jena Fuseki

Les inférences RDF se trouvent dans un fichier **jena-fuseki-3.4.0/run/databases/rules.rules**.

Pour lancer Jena Fuseki sur **localhost:3030**: 
```cd jena-fuseki-3.4.0
./fuseki-server --update```

Les données sont déjà présentes dans fuseki au lancement ;)
