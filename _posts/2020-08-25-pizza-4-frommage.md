---
layout: post
title: Pizza 4 Frommage
date: 2020-08-25T06:52:04.277Z
---
# Options de configuration

## [](https://www.netlifycms.org/docs/configuration-options/#configuration-file)Fichier de configuration

Toutes les options de configuration de Netlify CMS sont spécifiées dans un `config.yml`fichier, dans le dossier où vous accédez à l'interface utilisateur de l'éditeur (généralement dans le `/admin`dossier).

Vous pouvez également spécifier un fichier de configuration personnalisé à l'aide d'une balise de lien:

```html

```

Pour voir des exemples de configuration de travail, vous pouvez [partir d'un modèle](https://www.netlifycms.org/docs/start-with-a-template) ou consulter le [site de démonstration](https://cms-demo.netlify.com/) du [CMS](https://cms-demo.netlify.com/) . (Aucune connexion requise: cliquez sur le bouton de connexion et le CMS s'ouvrira.) Vous pouvez vous référer au [code de configuration de](https://github.com/netlify/netlify-cms/blob/master/dev-test/config.yml) démonstration pour voir comment chaque option a été configurée.

Vous pouvez trouver des détails sur toutes les options de configuration ci-dessous. Notez que la [syntaxe YAML](https://en.wikipedia.org/wiki/YAML#Basic_components) permet d'écrire des listes et des objets en style bloc ou en ligne, et les exemples de code ci-dessous incluent un mélange des deux.

## [](https://www.netlifycms.org/docs/configuration-options/#backend)Backend

*Ce paramètre est obligatoire.*

L' `backend`option spécifie comment accéder au contenu de votre site, y compris l'authentification. [Tous les](https://www.netlifycms.org/docs/backends-overview) détails et exemples de code sont disponibles dans [Backends](https://www.netlifycms.org/docs/backends-overview) .

**Remarque** : quel que soit l'endroit où vous accédez au CMS Netlify - qu'il soit exécuté localement, dans un environnement de préparation ou dans votre site publié - il récupérera et validera toujours les fichiers dans votre référentiel hébergé (par exemple, sur GitHub), sur la branche que vous avez configurée dans votre fichier config.yml CMS Netlify. Cela signifie que le contenu récupéré dans l'interface utilisateur d'administration correspondra au contenu du référentiel, qui peut être différent de votre site en cours d'exécution localement. Cela signifie également que le contenu enregistré à l'aide de l'interface utilisateur d'administration sera enregistré directement dans le référentiel hébergé, même si vous exécutez l'interface utilisateur localement ou en préparation.

## [](https://www.netlifycms.org/docs/configuration-options/#publish-mode)Mode de publication

Par défaut, toutes les entrées créées ou modifiées dans le CMS Netlify sont validées directement dans la branche principale du référentiel.

L' `publish_mode`option permet d'activer le mode "Flux de travail éditorial" pour plus de contrôle sur les phases de publication de contenu. Toutes les entrées non publiées seront organisées dans un tableau en fonction de leur statut, et elles peuvent être examinées et modifiées plus avant avant d'être mises en ligne.

**Remarque: le** flux de travail éditorial fonctionne avec les référentiels GitHub et la prise en charge de GitLab et Bitbucket est [en version bêta](https://www.netlifycms.org/docs/beta-features/#gitlab-and-bitbucket-editorial-workflow-support) .

Vous pouvez activer le flux de travail éditorial avec la ligne suivante dans votre `config.yml`fichier Netlify CMS :

```yaml

```

D'un point de vue technique, le workflow traduit les actions de l'interface utilisateur de l'éditeur en commandes Git courantes:

| Actions dans l'interface utilisateur Netlify ... | Effectuez ces actions Git                                                                                            |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| Enregistrer le brouillon                         | S'engage dans une nouvelle branche (nommée selon le modèle `cms/collectionName/entrySlug`) et ouvre une pull request |
| Modifier le brouillon                            | Pousse un autre commit vers le brouillon de la branche / demande d'extraction                                        |
| Approuver et publier le brouillon                | Fusionne la demande d'extraction et supprime la branche                                                              |

## [](https://www.netlifycms.org/docs/configuration-options/#media-and-public-folders)Médias et dossiers publics

Les utilisateurs du CMS Netlify peuvent télécharger des fichiers dans votre référentiel à l'aide de la galerie multimédia. Les paramètres suivants spécifient où ces fichiers sont enregistrés et où ils sont accessibles sur votre site créé.

### [](https://www.netlifycms.org/docs/configuration-options/#media-folder)Dossier multimédia

*Ce paramètre est obligatoire.*

L' `media_folder`option spécifie le chemin du dossier dans lequel les fichiers téléchargés doivent être enregistrés, par rapport à la base du dépôt.

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#public-folder)Dossier public

L' `public_folder`option spécifie le chemin du dossier où les fichiers téléchargés par la médiathèque seront accessibles, par rapport à la base du site créé. Pour les champs contrôlés par les widgets \[fichier] ou \[image], la valeur du champ est générée en ajoutant ce chemin au nom de fichier du fichier sélectionné. La valeur par défaut est de `media_folder`, avec une ouverture `/`si elle n'est pas déjà incluse.

```yaml

```

Sur la base des paramètres ci-dessus, si un utilisateur utilisait un champ de widget d'image appelé `avatar`pour télécharger et sélectionner une image appelée `philosoraptor.png`, l'image serait enregistrée dans le référentiel à `/static/images/uploads/philosoraptor.png`, et le `avatar`champ du fichier serait défini sur `/images/uploads/philosoraptor.png`.

## [](https://www.netlifycms.org/docs/configuration-options/#media-library)Médiathèque

Les intégrations de médiathèque sont configurées via la `media_library`propriété et sa valeur doit être un objet avec au moins une `name`propriété. Une `config`propriété peut également être utilisée pour les options qui doivent être transmises à la bibliothèque utilisée.

**Exemple:**

```yaml

```

## [](https://www.netlifycms.org/docs/configuration-options/#site-url)URL du site

Le `site_url`paramètre doit fournir une URL vers votre site publié. Peut être utilisé par le CMS pour diverses fonctionnalités. Utilisé avec une collection `preview_path`pour créer des liens vers du contenu en direct.

**Exemple:**

```yaml

```

## [](https://www.netlifycms.org/docs/configuration-options/#display-url)Afficher l'URL

Lorsque le `display_url`paramètre est spécifié, l'interface utilisateur du CMS comprendra un lien dans la zone fixe en haut de la page, permettant aux auteurs de contenu de revenir facilement à votre site principal. Le texte du lien se compose de l'URL sans la partie de protocole (par exemple, `your-site.com`).

La valeur par défaut est `site_url`.

**Exemple:**

```yaml

```

## [](https://www.netlifycms.org/docs/configuration-options/#custom-logo)Logo personnalisé

Lorsque le `logo_url`paramètre est spécifié, l'interface utilisateur du CMS modifie le logo affiché en haut de la page de connexion, vous permettant de personnaliser le CMS avec votre propre logo. `logo_url`est supposé être une URL vers un fichier image.

**Exemple:**

```yaml

```

## [](https://www.netlifycms.org/docs/configuration-options/#locale)Lieu

Les paramètres régionaux du CMS.

La valeur par défaut est `en`.

Les autres langues que l'anglais doivent être enregistrées manuellement.

**Exemple**

Dans votre `config.yml`:

```yaml

```

Et dans votre code JavaScript personnalisé:

```js

```

Lorsqu'une traduction pour les paramètres régionaux sélectionnés manque, la traduction anglaise sera utilisée.

> Lors de l'importation, `netlify-cms`tous les paramètres régionaux sont enregistrés par défaut (il vous suffit donc de mettre à jour votre `config.yml`).

## [](https://www.netlifycms.org/docs/configuration-options/#show-preview-links)Afficher les liens d'aperçu

[Les liens d'aperçu de déploiement](https://www.netlifycms.org/docs/deploy-preview-links) peuvent être désactivés en définissant `show_preview_links`sur `false`.

**Exemple:**

```yaml

```

## [](https://www.netlifycms.org/docs/configuration-options/#slug-type)Type de limace

L' `slug`option vous permet de modifier la façon dont les noms de fichiers pour les entrées sont créés et nettoyés. Cela s'applique également aux noms de fichiers des médias insérés via la bibliothèque multimédia par défaut.\
Pour modifier les données réelles dans un slug, consultez l'option par collection ci-dessous.

`slug` accepte plusieurs options:

* `encoding`

  * `unicode`(par défaut): Nettoyez les noms de fichiers (slugs) selon [RFC3987](https://tools.ietf.org/html/rfc3987) et la [spécification d'URL WHATWG](https://url.spec.whatwg.org/) . Cette spécification autorise l'existence de caractères non ASCII (ou non latins) dans les URL.
  * `ascii`: Nettoyez les noms de fichiers ( [slugs](https://tools.ietf.org/html/rfc3986) ) conformément à la [RFC3986](https://tools.ietf.org/html/rfc3986) . Les caractères ne sont autorisés (0-9, az, AZ, `_`, `-`, `~`).
* `clean_accents`: Réglez sur `true`pour supprimer les signes diacritiques des caractères slug avant de procéder au nettoyage. Ceci est souvent utile lors de l'utilisation de l' `ascii`encodage.
* `sanitize_replacement`: La chaîne de remplacement utilisée pour remplacer les caractères non sécurisés, par défaut `-`.

**Exemple**

```yaml

```

## [](https://www.netlifycms.org/docs/configuration-options/#collections)Les collections

*Ce paramètre est obligatoire.*

Le `collections`paramètre est au cœur de la configuration de votre CMS Netlify, car il détermine la manière dont les types de contenu et les champs de l'éditeur dans l'interface utilisateur génèrent des fichiers et du contenu dans votre référentiel. Chaque collection que vous configurez s'affiche dans la barre latérale gauche de la page Contenu de l'interface utilisateur de l'éditeur, dans l'ordre dans lequel elles sont entrées dans votre `config.yml`fichier Netlify CMS .

`collections` accepte une liste d'objets de collection, chacun avec les options suivantes:

* `name`(obligatoire): identifiant unique de la collection, utilisé comme clé lorsqu'il est référencé dans d'autres contextes (comme le [widget de relation](https://www.netlifycms.org/docs/widgets/#relation) )
* `identifier_field`: voir description détaillée ci-dessous
* `label`: étiquette de la collection dans l'interface utilisateur de l'éditeur; prend par défaut la valeur de`name`
* `label_singular`: étiquette singulière pour certains éléments dans l'éditeur; prend par défaut la valeur de`label`
* `description`: texte optionnel, affiché sous l'étiquette lors de la visualisation d'une collection
* `files`ou `folder`(nécessite l'un de ceux-ci): spécifie le type et l'emplacement de la collection; détails dans les [types de collection](https://www.netlifycms.org/docs/collection-types)
* `filter`: filtre optionnel pour les `folder`collections; détails dans les [types de collection](https://www.netlifycms.org/docs/collection-types)
* `create`: pour les `folder`collections uniquement; `true`permet aux utilisateurs de créer de nouveaux éléments dans la collection; par défaut`false`
* `publish`: pour `publish_mode: editorial_workflow`seulement; `false`masque les contrôles de publication de l'interface utilisateur pour une collection; par défaut`true`
* `hide`: `true`masque une collection dans l'interface utilisateur du CMS; par défaut `false`. Utile lors de l'utilisation du widget de relation pour masquer les collections référencées.
* `delete`: `false`empêche les utilisateurs de supprimer des éléments dans une collection; par défaut`true`
* `extension`: voir description détaillée ci-dessous
* `format`: voir description détaillée ci-dessous
* `frontmatter_delimiter`: voir description détaillée sous `format`
* `slug`: voir description détaillée ci-dessous
* `preview_path`: voir description détaillée ci-dessous
* `preview_path_date_field`: voir description détaillée ci-dessous
* `fields` (obligatoire): voir la description détaillée ci-dessous
* `editor`: voir description détaillée ci-dessous
* `summary`: voir description détaillée ci-dessous
* `sortableFields`: voir description détaillée ci-dessous
* `view_filters`: voir description détaillée ci-dessous

Les dernières options nécessitent des informations plus détaillées.

### [](https://www.netlifycms.org/docs/configuration-options/#identifier_field)`identifier_field`

Netlify CMS s'attend à ce que chaque entrée fournisse un champ nommé `"title"`qui sert d'identifiant pour l'entrée. Le champ identifiant sert de titre à une entrée lors de l'affichage d'une liste d'entrées et est utilisé dans la création de [slug](https://www.netlifycms.org/docs/configuration-options/#slug) . Si vous souhaitez utiliser un champ autre que `"title"`comme identificateur, vous pouvez définir `identifier_field`le nom de l'autre champ.

**Exemple**

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#extension-and-format)`extension` et `format`

Ces paramètres déterminent la manière dont les fichiers de collection sont analysés et enregistrés. Les deux sont facultatifs - Netlify CMS tentera de déduire vos paramètres en fonction des éléments existants dans la collection. Si votre collection est vide ou si vous souhaitez plus de contrôle, vous pouvez définir ces champs explicitement.

`extension`détermine l'extension de fichier recherchée lors de la recherche d'entrées existantes dans une collection de dossiers et il détermine l'extension de fichier utilisée pour enregistrer de nouveaux éléments de collection. Il accepte les valeurs suivantes: `yml`, `yaml`, `toml`, `json`, `md`, `markdown`, `html`.

Vous pouvez également spécifier une personnalisation `extension`non incluse dans la liste ci-dessus, à condition que les fichiers de collection puissent être analysés et enregistrés dans l'un des formats pris en charge ci-dessous.

`format`détermine comment les fichiers de collection sont analysés et enregistrés. Il sera déduit si le `extension`champ ou les extensions de fichier de collection existantes correspondent à l'une des extensions prises en charge ci-dessus. Il accepte les valeurs suivantes:

* `yml`ou `yaml`: analyse et enregistre les fichiers sous forme de fichiers de données au format YAML; enregistre avec l' `yml`extension par défaut
* `toml`: analyse et enregistre les fichiers sous forme de fichiers de données au format TOML; enregistre avec l' `toml`extension par défaut
* `json`: analyse et enregistre les fichiers sous forme de fichiers de données au format JSON; enregistre avec l' `json`extension par défaut
* `frontmatter`: analyse les fichiers et enregistre les fichiers avec le frontmatter de données suivi d'un corps de texte non analysé (édité à l'aide d'un `body`champ); enregistre avec l' `md`extension par défaut; par défaut pour les collections qui ne peuvent pas être déduites. Les collections avec un `frontmatter`format (déduit ou défini explicitement) peuvent analyser les fichiers avec frontmatter au format YAML, TOML ou JSON. Cependant, ils seront enregistrés avec le frontmatter YAML.
* `yaml-frontmatter`: identique au `frontmatter`format ci-dessus, sauf que le frontmatter sera à la fois analysé et enregistré uniquement en tant que YAML, suivi d'un corps de texte non analysé. Le délimiteur par défaut pour cette option est `---`.
* `toml-frontmatter`: identique au `frontmatter`format ci-dessus, sauf que le frontmatter sera à la fois analysé et enregistré uniquement en tant que TOML, suivi d'un corps de texte non analysé. Le délimiteur par défaut pour cette option est `+++`.
* `json-frontmatter`: identique au `frontmatter`format ci-dessus, sauf que le frontmatter sera à la fois analysé et enregistré au format JSON, suivi d'un corps de texte non analysé. Le délimiteur par défaut pour cette option est `{` `}`.

### [](https://www.netlifycms.org/docs/configuration-options/#frontmatter_delimiter)`frontmatter_delimiter`

Si vous avez déclaré un format de frontmatter explicite, cette option vous permet de spécifier un délimiteur personnalisé comme `~~~`. Si vous avez besoin de séparateurs de début et de fin différents, vous pouvez utiliser un tableau comme `["(", ")"]`.

### [](https://www.netlifycms.org/docs/configuration-options/#slug)`slug`

Pour les collections de dossiers où les utilisateurs peuvent créer de nouveaux éléments, l' `slug`option spécifie un modèle pour générer de nouveaux noms de fichiers en fonction de la date et du `title`champ de création d'un fichier . (Cela signifie que toutes les collections avec `create: true`doivent avoir un `title`champ (un champ différent peut être utilisé via [`identifier_field`](https://www.netlifycms.org/docs/configuration-options/#identifier_field)).

Le modèle de slug peut également référencer une valeur de champ par son nom, par exemple. `{{title}}`. Si un nom de champ entre en conflit avec un nom de balise de modèle intégré - par exemple, si vous avez un champ nommé `slug`et que vous souhaitez référencer ce champ via `{{slug}}`, vous pouvez le faire en ajoutant le `fields.`préfixe explicite , par exemple. `{{fields.slug}}`.

**Balises de modèle disponibles:**

* Tout champ peut être référencé en enveloppant le nom du champ entre doubles accolades, par exemple. `{{author}}`
* `{{slug}}`: une version sécurisée pour les URL du `title`champ (ou champ identifiant) du fichier
* `{{year}}`: Année à 4 chiffres de la date de création du fichier
* `{{month}}`: Mois à 2 chiffres de la date de création du fichier
* `{{day}}`: Jour à 2 chiffres du mois de la date de création du fichier
* `{{hour}}`: Heure à 2 chiffres de la date de création du fichier
* `{{minute}}`: Minute à 2 chiffres de la date de création du fichier
* `{{second}}`: Seconde à 2 chiffres de la date de création du fichier

**Exemple:**

```yaml

```

**Exemple utilisant des noms de champs:**

```yaml

```

**Exemple d'utilisation d'un nom de champ en conflit avec une balise de modèle:**

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#preview_path)`preview_path`

Chaîne représentant le chemin d'accès au contenu de cette collection sur le site en ligne. Cela permet de déployer des liens d'aperçu pour diriger vers un élément de contenu spécifique plutôt que vers la racine du site d'un aperçu de déploiement.

**Balises de modèle disponibles:**

Les balises de modèle sont les mêmes que celles de [slug](https://www.netlifycms.org/docs/configuration-options/#slug) , avec les exceptions suivantes:

* `{{slug}}`est le slug complet pour l'entrée actuelle (pas seulement l'identifiant de sécurité URL, comme c'est le cas avec la [`slug`configuration](https://www.netlifycms.org/docs/configuration-options/#slug) )
* Les balises de modèle basées sur la date, telles que `{{year}}`et `{{month}}`, sont extraites d'un champ de date dans votre entrée et peuvent nécessiter une configuration supplémentaire - voir [`preview_path_date_field`](https://www.netlifycms.org/docs/configuration-options/#preview_path_date_field)pour plus de détails. Si une balise de modèle de date est utilisée et qu'aucune date ne peut être trouvée, `preview_path`elle sera ignorée.
* `{{filename}}` Le nom du fichier sans la partie d'extension.
* `{{extension}}` L'extension de fichier.

**Exemples:**

```yaml

```

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#preview_path_date_field)`preview_path_date_field`

Le nom d'un champ de date à partir duquel analyser les balises de modèle basées sur la date `preview_path`. Si ce champ n'est pas fourni et `preview_path`contient des balises de modèle basées sur la date (par exemple `{{year}}`), Netlify CMS tentera de déduire un champ de date utilisable en vérifiant les noms de champ de date courants, tels que `date`. Si vous trouvez que vous devez spécifier un champ de date, vous pouvez utiliser `preview_path_date_field`pour indiquer à Netlify CMS quel champ utiliser pour les balises de modèle de chemin d'aperçu.

**Exemple:**

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#fields)`fields`

L' `fields`option mappe les widgets d'interface utilisateur de l'éditeur aux paires champ-valeur dans le fichier enregistré. L'ordre des champs dans votre `config.yml`fichier Netlify CMS détermine leur ordre dans l'interface utilisateur de l'éditeur et dans le fichier enregistré.

`fields` accepte une liste d'objets de collection, chacun avec les options suivantes:

* `name`(obligatoire): identifiant unique du champ, utilisé comme clé lorsqu'il est référencé dans d'autres contextes (comme le [widget de relation](https://www.netlifycms.org/docs/widgets/#relation) )
* `label`: libellé du champ dans l'interface utilisateur de l'éditeur; prend par défaut la valeur de`name`
* `widget`: définit l'interface utilisateur et les entrées de l'éditeur et les types de données de champ de fichier; détails dans les [widgets](https://www.netlifycms.org/docs/widgets)
* `default`: spécifiez une valeur par défaut pour un champ; disponible pour la plupart des types de widgets (voir [Widgets](https://www.netlifycms.org/docs/widgets) pour plus de détails sur chaque type de widget). Veuillez noter que la valeur par défaut du champ ne fonctionne que pour le type de collection de dossiers.
* `required`: spécifier `false`de rendre un champ facultatif; par défaut`true`
* `pattern`: ajoutez la validation de champ en spécifiant une liste avec un modèle regex et un message d'erreur; une validation plus approfondie peut être obtenue avec [des widgets personnalisés](https://www.netlifycms.org/docs/custom-widgets/#advanced-field-validation)
* `comment`: commentaire optionnel à ajouter avant le champ (supporté uniquement pour `yaml`)

Dans les fichiers avec frontmatter, un champ doit être nommé `body`. Ce champ spécial représente la section du document (généralement markdown) qui vient après le frontmatter.

**Exemple:**

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#editor)`editor`

Ce paramètre modifie les options de la vue éditeur de la collection. Il a jusqu'à présent une option:

* `preview`: défini sur `false`pour désactiver le volet d'aperçu de cette collection; par défaut`true`

**Exemple:**

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#summary)`summary`

Ce paramètre permet la personnalisation de la vue de la liste des collections. Similaire au `slug`champ, une chaîne avec des modèles peut être utilisée pour inclure des valeurs de différents champs, par exemple `{{title}}`. Cette option remplace la valeur par défaut de `title`field et `identifier_field`.

**Balises de modèle disponibles:**

Les balises de modèle sont les mêmes que celles de [slug](https://www.netlifycms.org/docs/configuration-options/#slug) , avec les ajouts suivants:

* `{{filename}}` Le nom du fichier sans la partie d'extension.
* `{{extension}}` L'extension de fichier.
* `{{commit_date}}` La date de validation du fichier sur les backends pris en charge (backends basés sur git).
* `{{commit_author}}` La date de création du fichier sur les backends pris en charge (backends basés sur git).

**Exemple**

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#sortablefields)`sortableFields`

Une liste facultative de champs de tri à afficher dans l'interface utilisateur.

Par défaut , les champs sont déduits `title`, et et affichera également le champ de tri dans les backends basés sur git.`dateauthordescriptionUpdate On`

Lorsque le `author`champ ne peut pas être déduit, l'auteur du commit sera utilisé.

**Exemple**

```yaml

```

### [](https://www.netlifycms.org/docs/configuration-options/#view_filters)`view_filters`

Une liste facultative de filtres de vue prédéfinis à afficher dans l'interface utilisateur.

Par défaut, une liste vide.

**Exemple**

```yaml

```