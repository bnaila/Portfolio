## Description

[Rapport de l'exercice de Data Management](https://bnaila.github.io/portfolio/Projet%20de%20data%20management/Rapport_eCRF_DataManagement_NB.html)

1) Le fichier Exemple_eCRF_Export_Base contient un export d'une base de données eCRF. On y trouve 8 patients, avec les valeurs obtenues pour chacun d'entre eux, pour chaque variable de l'eCRF.
2)  Le fichier Exemple_eCRF_Data_Specification est un fichier excel de spécifications des variables de l'eCRF.
L'étude clinique en question a été effectuée sur deux semaines, avec une visite à J0 et une visite à S2 (c'est pourquoi le fichier excel contient deux onglets : "Inclusion" et "Suivi").
Dans chaque onglet se trouve la liste des variables récupérées pour chaque patient lors des visites.

Les champs importants sont :

 - Le nom de la variable (NOM_VARIABLE)
 - Le type de la variable (TYPE)
 - L'appartenance à un dictionnaire (NOM_DICTIONNAIRE)
ie: Certaines variables ont des choix prédéfinis qui sont regroupés dans un dictionnaire (onglet Dictionnaires). C'est à dire qu'on s'attend à certaines valeurs et pas à d'autres pour cette variable.
Si le champ dictionnaire est rempli, c'est que la réponse de l'utilisateur doit être comprise dans les valeurs de la colonne CODE_REPONSE du dictionnaire associé (onglet Dictionnaires).
 - La condition d'apparition de la variable qui se décrit au travers de 7 colonnes :
OBLIGATOIRE :  si la variable est obligatoire (égale à 1) ou non (égale à 0). Si la variable n'est pas obligatoire on s'attend à ce qu'elle soit potentiellement vide.
COND_VARIABLE, COND_OPERATEUR, COND_VALEUR : qui décrivent une condition d'apparition de la variable sur l'eCRF, exemple la variable B apparaît uniquement si la variable A est égale à 1.
Les trois colonnes décrivent donc la condition : "A==1" nécessaire pour que la variable soit présente et remplie par le patient (pour plus d'informations voir l'onglet Feuille technique).
COND_VARIABLE_2, COND_OPERATEUR_2, COND_VALEUR_2 :  Il est possible qu'une variable soit présente sous deux conditions qui doivent être vérifiées simultanément.


Code R vérifie dans la base CSV les conditions suivantes en se basant sur l'excel de spécification :  
- Si la variable est présente (il se peut qu'une variable soit présente dans la base et pas dans l'excel de spécification ou inversement)
- Si la variable est manquante ou non pour un patient (en prenant en compte les conditions si elles existent, effectivement des variables peuvent être manquantes et c'est normal)
- Pour les variables avec un dictionnaire attitré, si la valeur de la variable est dans la liste prédéfinie du dictionnaire.

Le programme retourne un rapport (du format de ton choix) qui lisible et utilisable par un ARC (= assistant de recherche clinique), afin que celui-ci puisse essayer de rattraper les données en se déplaçant dans les centres hospitaliers pour consulter les dossiers médicaux des patients.


