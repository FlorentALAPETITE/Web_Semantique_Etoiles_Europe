# Web_Semantique_Etoiles_Europe
Projet Web Semantique M1 ALMA

Pour lancer le projet, executer la ligne de commande suivante :

     ./executeTarql.sh

Le résultat de la requête se trouve dans le fichier : "RDFGraph_Concours_Etoiles_Europes.ttl"

## Adaptation avec Jena Fuseki
Dans la version *3.4* de Jena Fuseki, configurer un fichier **run/configuration/Etoiles.ttl** comme ceci:
```
@prefix :      <http://base/#> .
@prefix tdb:   <http://jena.hpl.hp.com/2008/tdb#> .
@prefix rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix ja:    <http://jena.hpl.hp.com/2005/11/Assembler#> .
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
@prefix fuseki: <http://jena.apache.org/fuseki#> .
 
:service1  a                          fuseki:Service ;
        fuseki:dataset                :dataset ;
        fuseki:name                   "Etoiles" ;
        fuseki:serviceQuery           "query" , "sparql" ;   # SPARQL query service
        fuseki:serviceReadGraphStore  "get" ;                # Graph store protocol (read only)
        fuseki:serviceReadWriteGraphStore "data" ;           # Graph store protocol (read/write)
        fuseki:serviceUpdate          "update" ;             # SPARQL update service
        fuseki:serviceUpload          "upload" .             # File upload
 
:dataset a ja:RDFDataset ;
    ja:defaultGraph       <#model_inf> ;
     .
 
<#model_inf> a ja:InfModel ;
     ja:baseModel <#graph> ;
     ja:reasoner [
        ja:rulesFrom <../../run/databases/rules.rules>;
        ja:reasonerURL <http://jena.hpl.hp.com/2003/GenericRuleReasoner>; 
    ] .
 
<#graph> rdf:type tdb:GraphTDB ;
  tdb:dataset :tdb_dataset_readwrite .
 
:tdb_dataset_readwrite
        a             tdb:DatasetTDB ;
        tdb:location  "run/databases/etoiles"
        .
```

Ne pas oublier de mettre les inférences RDF dans un fichier **run/databases/rules.rules**, comme ceci : 
```
@prefix rdf:  <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

[(?x ?a ?y) -> (?x rdf:type rdfs:Ressource)]
[(?x ?a ?y) -> (?y rdf:type rdfs:Ressource)]
[(?a rdfs:domain ?x) (?y ?a ?z) -> (?y rdf:type ?x)]
[(?a rdfs:range ?x) (?y ?a ?z) -> (?z rdf:type ?x)]
[(?x rdfs:subPropertyOf ?y) (?y rdfs:subPropertyOf ?z) -> (?x rdfs:subPropertyOf ?z)]
[(?x rdf:type rdf:Property) -> (?x rdfs:subPropertyOf ?x)]
[(?a rdfs:subPropertyOf ?b) (?x ?a ?y) -> (?x ?b ?y)]
[(?x rdf:type rdfs:Class) -> (?x rdfs:subClassOf rdfs:Ressource)]
[(?x rdfs:subClassOf ?y) (?z rdf:type ?x) -> (?z rdf:type ?y)]
[(?x rdf:type rdfs:Class) -> (?x rdfs:subClassOf ?x)]
[(?x rdfs:subClassOf ?y) (?y rdfs:subClassOf ?z) -> (?x rdfs:subClassOf ?z)]
[(?x ?a rdfs:Datatype) -> (?x rdfs:subClassOf rdfs:Litteral)]
```