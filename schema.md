# Prénoms des nouveaux-nés

Spécification du modèle de données relatif aux prénoms des nouveaux-nés déclarés à l’état-civil

- nom : `prenoms`
- page d'accueil : https://github.com/CharlesNepote/liste-prenoms-nouveaux-nes
- URL du schéma : https://github.com/CharlesNepote/liste-prenoms-nouveaux-nes/raw/v1.1.4/schema.json
- version : `1.1.5`
- date de création : 2018-04-12
- date de dernière modification : 2020-05-18
- concerne le pays : FR
- valeurs manquantes représentées par : `[""]`
- contributeurs :
  - Charles Nepote (auteur) [charles.nepote@fing.org](charles.nepote@fing.org)
  - Simon Chignard (contributeur) [simon.chignard@data.gouv.fr](simon.chignard@data.gouv.fr)
  - Bernadette Kessler (contributeur)
  - Christian Quest (contributeur)
  - Christophe Benz (contributeur) [christophe.benz@jailbreak.paris](christophe.benz@jailbreak.paris)
  - Pierre Dittgen (contributeur) [pierre.dittgen@jailbreak.paris](pierre.dittgen@jailbreak.paris)
  - Johan Richer (contributeur) [johan.richer@jailbreak.paris](johan.richer@jailbreak.paris)
- ressources :
  - Exemple de fichier des prénoms valide ([lien](https://github.com/CharlesNepote/liste-prenoms-nouveaux-nes/raw/v1.1.4/examples/prenoms-nouveaux-nes_exemple-valide.csv))
  - Exemple de fichier des prénoms invalide ([lien](https://github.com/CharlesNepote/liste-prenoms-nouveaux-nes/raw/v1.1.4/examples/prenoms-nouveaux-nes_exemple-invalide.csv))
- sources :
  - Code civil ([lien](https://www.legifrance.gouv.fr/affichCode.do?cidTexte=LEGITEXT000006070721&dateTexte=20170327))
  - Circulaire du 28 octobre 2011 relative aux règles particulières à divers actes de l&#x27;état civil relatifs à la naissance et à la filiation — NOR : JUSC1119808C ([lien](http://www.textes.justice.gouv.fr/art_pix/JUSC1119808C.pdf))
  - Circulaire du 23 juillet 2014 relative à l’état civil — NOR : JUSC1412888C ([lien](http://circulaire.legifrance.gouv.fr/pdf/2014/07/cir_38565.pdf))
  - Normes techniques de l&#x27;INSEE ([lien](http://xml.insee.fr/schema/etat-civil/))

## Modèle de données

Ce modèle de données repose sur les 6 champs suivants correspondant aux colonnes du fichier tabulaire.

### `COMMUNE_NOM`

- titre : Nom de la commune d'enregistrement à l'état-civil
- description : Nom de la commune où les prénoms sont enregistrés à l'état-civil, c'est-à-dire le lieu de naissance. Le lieu de naissance peut être différent du lieu de résidence des parents, comme cela peut être le cas pour les enfants nés dans une maternité. Le renseignement de ce champ est facultatif. Il permet cependant de faciliter l'usage des données, notamment par le grand public.
- type : chaîne de caractères
- valeur optionnelle
- motif : `^(Le |La |Les |Los |Aux |L'|)([A-ZÉÇŒÈÎ])(((-| | - |')[A-ZÉÇŒÈÎ])|('|-| |)[a-zàâéèêëïîÿôûüœç])*( \([A-Z][a-z]*\)|)$`

### `COLL_INSEE`

- titre : Code INSEE de la commune d'enregistrement à l'état-civil
- description : Code INSEE de la commune où les prénoms sont enregistrés à l'état-civil, c'est-à-dire le lieu de naissance. Issu du Code Officiel Géographique, le [code INSEE de la commune](https://fr.wikipedia.org/wiki/Code_Insee) est composé de 5 caractères alphanumériques (les deux premiers correspondent au département et peuvent donc contenir les lettres 'A' et 'B' utilisées pour la Corse).
- type : chaîne de caractères
- valeur obligatoire
- motif : `^([013-9]\d|2[AB1-9])\d{3}$`

### `ENFANT_SEXE`

- titre : Sexe relatif au prénom
- description : Sexe correspondant au prénom, codé 'M' ou 'F' ou 'I', respectivement pour Masculin, Féminin ou Intersexué/Indéterminé. L'information est importante car certains prénoms sont aussi bien masculins que féminins, comme 'Camille'. 'I' signale un genre spécifiquement intersexué ou indéterminé et, contrairement à ce qu'il pourrait laisser penser, il ne mentionne pas un sexe inconnu. 'I' n'est théoriquement pas encore utilisé en France mais plusieurs pays ont créé un tel statut et de nombreux éléments suggèrent une évolution prochaine du droit en France.
- type : chaîne de caractères
- valeur obligatoire
- valeurs autorisées : `["M","F","I"]`

### `ENFANT_PRENOM`

- titre : Prénom
- description : Prénom de nouveau(x)-né(s) constaté comme premier prénom dans les actes d'état-civil de l'année correspondante. Un acte de naissance peut désigner un nouveau-né avec plusieurs prénoms et le législateur a prévu que "[_tout prénom inscrit dans l'acte de naissance peut être choisi comme prénom usuel_](https://fr.wikipedia.org/wiki/Prénom_usuel)_"_. La plupart du temps le premier prénom est le prénom d'usage initialement choisi par le(s) parent(s). Cette spécification ne retient donc que le premier prénom : si un nouveau-né est appelé 'Armelle Julia Blanche', seul 'Armelle' sera retenu pour constituer ce jeu de données. Un prénom composé comme 'Marie-Jeanne' compte pour un prénom complet. Attention, "[_l'alphabet utilisé doit être celui qui sert à l'écriture du français. Les caractères alphabétiques étrangers ne sont donc pas autorisés (par exemple le « ñ »)_](https://www.demarches.interieur.gouv.fr/particuliers/choix-prenom-enfant)". Outre les caractères alphabétiques, un prénom peut posséder un trait d'union, voire deux, comme dans 'Lou-Anne' ou 'Mohamed-El-Amine'. Des prénoms peuvent posséder une apostrophe comme dans Gwenc'Hlan ou N'Deye, voire peut-être deux. Nous considérons aussi qu'un prénom pourrait se terminer, voire débuter, par une apostrophe - cette dernière étant parfois utilisée en français pour marquer la suppression de la finale ou le début d'un mot, comme dans Boul' Mich'.
- type : chaîne de caractères
- valeur obligatoire
- motif : `^'?[A-ZÉÀÈÙÄËÏÖÜŸÂÊÎÔÛŶÇŒÆ][a-zéàèùäëïüöÿâêîôûŷçæœ]*(|'|(('[A-ZÉÀÈÙÄËÏÖÜŸÂÊÎÔÛŶÇŒÆa-zéàèùäëïüöÿâêîôûŷçæœ][a-zéàèùäëïüöÿâêîôûŷçæœ]*'?){1,2}|(-[A-ZÉÀÈÙÄËÏÖÜŸÂÊÎÔÛŶÇŒÆ][a-zéàèùäëïüöÿâêîôûŷçæœ]*'?){1,2}){1,5})$`

### `NOMBRE_OCCURRENCES`

- titre : Nombre d'occurrences
- description : Nombre d'occurrences du prénom pour l'année correspondante. Tous les prénoms sont comptabilisés, y compris les prénoms uniques - un seuil minimum est exclu car il conduirait à passer sous silence une importante part des naissances, voire la totalité dans les petites communes. La valeur de ce champ est donc un nombre entier d'1 à 6 chiffres maximum, 0 étant exclu.
- type : nombre entier
- valeur obligatoire
- valeur minimale : 1
- valeur maximale : 999,999

### `ANNEE`

- titre : Année
- description : Année de relevé, sur quatre chiffres, au format AAAA.
- type : année
- valeur obligatoire
