# Codification - 20 juillet 2022

# Remarques
- Temps de création de l'index : une vingtaine de secondes pour les 35993 communes
- 
-
-


Options examinées pour chaque nomenclature :
* Lemmatisation (donner à un mot sa forme neutre canonique - https://fr.wikipedia.org/wiki/Lemmatisation)
* Recherche sur libellé ou sur code ?
* Démarre au début des mots ou pas
* Recherche sur le début du libellé/code
* Ordre affichage des échos correspondant à la saisie
* Recherche dès le nième caractère saisi
* Pondération des échos  
* Stopwords


## Géographie 

### Département : 

* :white_check_mark: Pas de racinisation / lemmatisation 
* :white_check_mark: Recherche sur libellé ou sur code
* :white_check_mark: Démarre au début des mots (exemple Haute Loire, Loire)
* :white_check_mark: Recherche sur le début du code (exemple : si tu tapes 1, tu n'affiches pas 01, mais 10, 11 etc)
* :white_check_mark: Ordre affichage : ordre des codes
* :x: Recherche dès le premier caractère
* :white_check_mark: Pondération : aucune
* :white_check_mark: Stopwords : aucun


#### Exemples

:white_check_mark:
→ `0`
← `01 02 03 04 05 06 07 08 09`

:white_check_mark:
→ `9`
← `90 91 92 93 94 95 971 972 973 974 976`

:white_check_mark:
→ `97`
← `971 972 973 974 976`

:x: Haute Garonne apparaît avant car il n'y a pas de priorité sur le premier mot
→ `g`
← `Gard Gers Gironde Guadeloupe Guyane Haute Garonne`


### Pays
Plusieurs cas d'usage (pays de naissance, pays de résidence actuelle). On propose que les critères de recherche soient les mêmes mais qu'on ait des listes différentes en fonction des cas d'usage (eg pays de naissance => liste historique VS pays dans lequel on vit actuellement => liste actuelle ou millésimée)

* :white_check_mark: Pas de racinisation / lemmatisation
* :white_check_mark: Recherche sur libellé uniquement (code non signifiant)
* :white_check_mark: Démarre au début de tous les mots 
* :white_check_mark: Ordre affichage : ordre alphabétique des libellés
* Recherche dès le premier caractère
* :white_check_mark: Pondération : aucune
* :white_check_mark: Stopwords : aucun


Besoin d'une liste Millésimée probablement



### Commune
Prévoir Libellé = libellé commune + code département (car homonymes)

* :white_check_mark: Pas de racinisation / lemmatisation
* :white_check_mark: Recherche sur libellé uniquement
* :white_check_mark: Démarre au début de tous les mots 
* Ordre affichage ? sur storybook, ordre alphabétique des libellés mais plutot comme Mélauto (d'abord ceux qui commencent par les saisis puis ordre alphabétique)
* Recherche dès le premier caractère
* :white_check_mark: Pondération : aucune
* :x: Synonymes : St/Saint et Sainte/Ste  (voire les 4 ?), s/s sous, ou autre abréviation habituelle : Fonctionne dans le story book mais je n'ai jamais été capable de le reproduire à partir de https://90-01z.github.io/lunatic-suggester/


## Hors géographie 

### PCS
* Racinisation / lemmatisation
* Recherche sur libellé uniquement
* Démarre au début de tous les mots 
* :x: Ordre affichage ? Melauto actuel (d'abord ceux qui commencent par les caractères saisis puis ordre alphabétique pour les autres) 
* Recherche à partir de 3 caractères  
* Pondération : aucune ou à voir ce qui est possible
* Synonymes : aucun
* Stopwords standards : 'de', 'le', la', 'les', 'du', 'et',  'au', 'aux', 'en' (+ voir la liste constituée par Théo)
* en cas d'une saisie "multimots" : afficher d'abord dans la liste des échos ceux qui ont tous les token, puis n-1 etc..


### Diplôme ?

* Pas de racinisation / lemmatisation
* Recherche sur libellé uniquement
* Démarre au début de tous les mots 
* Ordre affichage ? d'abord ceux qui commencent par les caractères saisis puis ordre alphabétique pour les autres
* Recherche à partir de 2 caractères  
* Pondération :  
* Synonymes :  
* Stopwords : diplome évoqué mais fausse idée
* en cas d'une saisie "multimots" : 


:question: Faut-il considérer un questionnement en deux parties (niveau puis spécialité) ou en seul jet ? Ou on considère les deux ?

:question: (Corollaire) Quelle question pose-t-on ?

:exclamation: Hélène se rapproche du pôle Diplôme pour savoir quelle liste doit être utilisée


### Secteur d'activité (à compléter quand intégration de l'enquête)

> On le tue (Hélène C), cf. on peut faire de l'identification employeur, c'est plus simple pour le répondant !
> sauf si on pense à l'ESA :-)

* Pas de racinisation / lemmatisation
* Recherche sur libellé et code ?
* Démarre au début de tous les mots 
* Ordre affichage ? d'abord ceux qui commencent par les caractères saisis puis ordre alphabétique pour les autres
* Recherche à partir de n ? caractères  
* Pondération :  
* Synonymes :  
* Stopwords : 
* en cas d'une saisie "multimots" : 


### BDF et EDT ? liste des activités et des "produits"

A traiter
Ajout Anne du 2 aout (présentation du storybook à EDT) : lemmatisation à prévoir surement et synonymes


==RESUME==
 
|Paramètres |DEP|PAYS|COMM|PCS|Diplome|
|-- |---|-|--|---|--|
| Lemmatisation |non|non|non|oui|non|
| Recherche sur libellé ou sur code|les deux|libellé|libellé|libellé|libellé|
| Démarre au début des mots ou pas|au début de chaque|au début de chaque|au début de chaque|au début de chaque|au début de chaque|
| Recherche sur le début du code|oui|so|so|so|so|
| Ordre affichage|ordre des codes|alphabétique libellé|d'abord ceux qui commencent par les saisis puis ordre alphabétique| d'abord ceux qui commencent par les saisis puis ordre alphabétique|d'abord ceux qui commencent par les saisis puis ordre alphabétique|
| Recherche dès le nième caractère|1|1|1|3 |2|
| Pondération des échos  |non|non|non|à voir ce qui est possible d'abord ceux qui ont tous les token, puis n-1 etc..|non|
| Stopwords|non|non|St/Saint et Sainte/Ste  (voire les 4 ?) |'de', 'le', la', 'les', 'du', 'et',  'au', 'aux', 'en' (+ voir la liste constituée par Théo)| diplome évoqué mais fausse idée|
    