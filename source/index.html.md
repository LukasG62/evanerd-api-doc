---
title: Documentation API EVANERD

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Evanerd API
---

# Introduction

Documentation de l'API utilisé lors de la réalisation du développement du Projet PINF : 2022-2023, Groupe Evanerd

# Authentification

## Récupèrer le token d'authentification

```javascript
```

> Lors de l'authentification, la réponses JSON fournira un token permettant d'utiliser certaines fonctionalités de l'API

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":202,
  "authToken":"f7c4464eed5ba3ae5a40bb6b3e40d2a5"
  "user:"
    {
      "id": 1,
      "firstName": "Maurice",
      "lastName": "Monticule",
      "mail":"momo@gmail.com",
      "tel":"",
      "sex": 0,
      "age": 19,
      "studies":"Centrale Lille IG2I",
      "photo":"www.example/users/1/image.png"
    },


}
```
### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /auth/**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
tel |  | Numéro de téléphone de l'utilisateur
password | Mot de passe de l'utilisateur

<aside class="notice">
Lors de la connexion, un nouveau token est généré, rendant l'ancien inutilisable
</aside>

<aside class="warning">
L'utilisateur doit avoir un compte activé (compte vérifié par email).
</aside>

# Users

## Lister les utilisateurs

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "users:"
    [
      {
        "id": 1,
        "firstName": "Maurice",
        "lastName": "Monticule",
        "mail":"momo@gmail.com",
        "tel":"",
        "sex": 0,
        "age": 19,
        "studies":"Centrale Lille IG2I",
        "photo":"www.example/users/1/image.png"
      },
      {
        "id": 2,
        "firstName": "Fluffums",
        "lastName": "calico",
        "mail":"fufu@gmail.com",
        "tel":"",
        "sex": 1,
        "age": 69,
        "studies":"Ecole du rire",
        "photo":"www.example/users/2/image.png"
      }
    ]
}
```

Cette route permet de récuperer une liste d'utilisateur

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /users**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
idRole *<span style="color:red">[OPTIONNEL]</span>* |  | Permet de lister tous les utilisateurs possédant le role indiqué

## Récupérer un utilisateur

```javascript

//TODO

```

> The above command returns JSON structured like this:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "user:"
    {
      "id": 1,
      "firstName": "Maurice",
      "lastName": "Monticule",
      "mail":"momo@gmail.com",
      "tel":"",
      "sex": 0,
      "age": 19,
      "studies":"Centrale Lille IG2I",
      "photo":"www.example/users/1/image.png"
    },
}
```

Cette route permet de récupérer un utilisateur selon son id

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /users/{uid}**

### Paramètres d'URL

Parameter | Description
--------- | -----------
uid | L'identifiant de l'utilisateur

## Modifier un utilisateur

```javascript

//TODO

```

> La requête renvoie un JSON de l'utilisateur modifié sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "user:"
    {
      "id": 1,
      "firstName": "Maurice",
      "lastName": "Monticule",
      "mail":"momo@gmail.com",
      "tel":"",
      "sex": 0,
      "age": 19,
      "studies":"Centrale Lille IG2I",
      "photo":"www.example/users/1/image.png"
    },
}
```

Cette route permet de modifier les informations d'un utilisateur présent dans la base de donnée

### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /users/{uid}**

### Paramètres d'URL

Parameter | Description
--------- | -----------
uid | L'identifiant de l'utilisateur

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
mail <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son adresse mail
tel <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifer son numéro de téléphone
age <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son age
studies <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier ses études
image <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier l'image sous le format base64
password <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son mot de passe

<aside class="notice">

   Les membres du CA peuvent modifier les informations de tous les utilisateurs. Un utilisateur ne peut modifier que ses propres informations.
</aside>

<aside class="warning">
  Si l'utilisateur n'a pas les permissions pour modifier un utilisateur alors la route enverra un JSON d'erreur avec un status code 403.
</aside>

## Créer un utilisateur

```javascript

//TODO

```

> La requête renvoie un JSON de l'utilisateur modifié sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":201,
  "user:"
    {
      "id": 3,
      "firstName": "Toto",
      "lastName": "Basse",
      "mail":"totobasse@gmail.com",
      "tel":"0102030405",
      "sex": 1,
      "age": 29,
      "studies":"Ecole de la vie",
      "photo":"www.example/users/2/image.png"
    },

}


```

Cette route permet de créer un utilisateur.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
firstname |  | Prénom de l'utilisateur
lastname |  | Nom de l'utilisateur
mail |  | Adresse email de l'utilisateur
tel |  | Numéro de téléphone de l'utilisateur
password |  | Mot de passe de l'utilisateur
age |  | l'age de l'utilisateur
studies <span style="color:red">[OPTIONNEL]</span> |  | Les etudes de l'utilisateur
sex <span style="color:red">[OPTIONNEL]</span> |  | le genre de l'utilisateur
image <span style="color:red">[OPTIONNEL]</span> |  | l'image de profil sous format base64


## Ajouter un instrument à l'utilisateur

```javascript

//TODO

```

> La requête renvoie un JSON avec l'id de l'utilisateur et l'instrument ajouté

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":201,

}
```

Cette route permet d'ajouter un instrument à l'utilisateur connecté

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/instruments**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
iid |  | l'id de l'instrument à ajouter

<aside class="notice">
   Un instrument ne peut être rajouté qu'une seul fois
</aside>

## Ajout d'un achievement à l'utilisateur

```javascript

//TODO

```

> La requête renvoie un JSON avec l'id de l'utilisateur et l'achievement ajouté

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":201,

}
```

Cette route permet d'ajouter un achievement à l'utilisateur connecté

### Requête HTTP

**<span style="rgb(255, 180, 0)">POST</span> /users/achievements**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
aid |  | l'id de l'achievements

<aside class="notice">
   Un utilisateur ne peut avoir plusieurs fois le même achievements
</aside>

<aside class="warning">
   Il faut que l'utilisateur sastifait les conditions d'obtention de l'achievement pour le recevoir. Sinon la route renvoie
   un JSON d'erreur avec comme code de status 403
</aside>

## Ajout d'un role à un utilisateur

```javascript

//TODO

```

> La requête renvoie un JSON avec l'id de l'utilisateur et le role ajouté

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":201,

}
```

Cette route permet d'ajouter un role à l'utilisateur

### Requête HTTP

**<span style="rgb(255, 180, 0)">POST</span> /users/{uid}/roles**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Parameter | Description
--------- | -----------
uid | L'identifiant de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
rid |  | l'id du role

<aside class="notice">
   Seuls les membres du CA peuvent ajouter un role, dans les autres cas, la route renverra un JSON d'erreur avec comme status 403
</aside>



# Roles

## Lister les rôles

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "roles":
    [
      {
        "id":1,
        "label":0,
        "active":0,
      },
      {
        "id":1,
        "content":,
        "banner":,
        "banner":,
        "pinned":,
        "visible":,
      {
      },
    ]
}
```

Cette route permet de récuperer la listes des roles

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /roles/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
active | "both" | Permet de préciser : 0=les roles inactifs, 1=les roles actifs "both"=Les deux

## Modifier un rôle

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
// TODO
```

Cette route permet de récuperer une liste de rôle

### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /roles/{rid}**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
rid |  | Permet de modifier le role indiqué

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
label *<span style="color:red">[OPTIONNEL]</span>* |  | Permet de modifier le nom du role
acitve *<span style="color:red">[OPTIONNEL]</span>* | 1 | Si le role est active



## Créer un rôle

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
// TODO
```

Cette route permet de créer un rôle

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /roles**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
label |  | Permet de modifier le nom du role
acitve *<span style="color:red">[OPTIONNEL]</span>* | 1 | Si le role est active


# Instruments 

## Retourner tous les instruments

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
// TODO
```

Cette route de retourner tous les instruments.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /instruments**

## Modifier un instrument

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
// TODO
```

Cette route permet de modifier un instrument.

### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /instruments/{iid}**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
label |  | l'identifiant de l'instrument

## Créer un instrument

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
// TODO
```

Cette route permet de créer un instrument.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /instruments**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
label |  | Nom de l'instrument

# Achievements 

## Retourner tous les achievements

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
// TODO
```

Cette route de retourner tous les achievements.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /achievements**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
iid *<span style="color:red">[OPTIONNEL]</span>* |  | Permet de modifier le role indiqué

## Modifier un achievement

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
// TODO
```

Cette route permet de modifier un achievement.

### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /achievement/{achivid}**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
achivid |  | l'identifiant de l'achievement

### Paramètres de rêquete

Paramètre | Par défaut | Description
--------- | ------- | -----------
label |  | Titre de l'achievement

## Créer un achievement

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
// TODO
```

Cette route permet de créer un achievement.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
iid *<span style="color:red">[OPTIONNEL]</span>* |  | Permet de modifier le role indiqué

# Groups

## Lister les groupes de l'utilisateur connecté

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "groups:"
    [
      {
        "id": 1,
        "titre":"La conv des bgs"
      },
      {
        "id": 2,
        "titre":"Maurice, Jean-Pierre"
      }
    ]
}
```

Cette route permet de récuperer la listes des conversations d'un utilisateur

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

## Lister Les permissions d'un groupe

```javascript
// TODO CODE AJAX
```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "groupeId":3,
  "permissions:"
    [
      {

      },
      {
      },
    ]
}
```

Cette route permet de récuperer la listes des permissions d'un groupe

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups/{gid}/permissions/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">
  Si un groupe n'a pas de permissions affecté, alors il n'y a aucune restrictions de role sur le groupe. 
  Par conséquent tout utilisateur membre peut y être ajouté.
</aside>

## Lister Les messages d'un groupe de l'utilisateur connecté

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "groupeId":3,
  "messages:"
    [
      {
        "id": 1,
        "uid":2,
        "gid":3,
        "pinned":1,
        "content":"La basse c'est super cool",
      },
      {
        "id": 2,
        "uid":1,
        "gid":3,
        "pinned":0,
        "content":"ratio",
        "answerTo":1
      },
    ]
}
```

Cette route permet de récuperer la listes des messages envoyés dans le groupe

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups/{gid}/messages**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Parameter | Description
--------- | -----------
gid | L'identifiant du groupe

## Lister Les reactions d'un message de groupe

```javascript
// TODO CODE AJAX
```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "groupeId":3,
  "messageId":1,
  "reactions:"
    [
      {
        "id":,
        "mid":,
        "gid":,
        "uid":,
        "emoji":
      },
      {
      },
    ]
}
```

Cette route permet de récuperer la listes des reactions d'un message de le groupe

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups/{gid}/messages/{mid}**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur


### Paramètres d'URL

Parameter | Description
--------- | -----------
gid | L'identifiant du groupe
mid | L'identifiant du message

## Créer un groupe pour l'utilisateur connecté
```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "groupe":
    {
    }
}
```

Cette route permet de créer un groupe pour l'utilisateur connecté

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /groups**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
image *<span style="color:red">[OPTIONNEL]</span>* |  | donnée de l'image sous le format base64
title *<span style="color:red">[OPTIONNEL]</span>*  |  | titre de la discussion

<aside class="notice">
L'utilisateur connecté est directement ajouté au groupe créé
</aside>

## Ajouter un utilisateur au groupe
```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "groupe":
    {
    }
}
```

Cette route permet d'ajouter un utilisateur au groupe

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /groups/{gid}/users/{uid}**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
gid | | L'identifiant du groupe
uid | | L'identifiant du l'utilisateur

<aside class="notice">
L'utilisateur connécté doit appartenir au groupe pour pouvoir ajouter un utilisateur
</aside>

## Envoyé un message dans le groupe
```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "groupe":
    {
    }
}
```

Cette route permet d'envoyer un message dans le groupe

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /groups/{gid}/messages**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
gid | | L'identifiant du groupe

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
content | | Contenu du message
answerTo <span style="color:red">[OPTIONNEL] |  | L'id du message cible

<aside class="notice">
L'utilisateur connécté doit appartenir au groupe pour envoyer un message
</aside>

# Posts

## Lister Les postes

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "posts":
    [
      {
        "id":1,
        "content":"",
        "banner":"",
        "pinned":0,
        "visible":1:

      },
      {
        "id":2,
        "content":"",
        "banner":"www.example.com/posts/2/image.png",
        "pinned":1,
        "visible":0,
      },
    ]
}
```

Cette route permet de récuperer la listes des postes 

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /posts/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">
  La listes de postes dépends du role de l'utilisateur, si l'utilisateur connecté est un non-membre alors il verra que les postes avec l'attribut visible à 1.
</aside>

## Lister Les reactions d'un post

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "posts":
    [
      {
      },
      {
      },
    ]
}
```

Cette route permet de récuperer la listes des postes 

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /posts/{pid}/reactions**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

## Lister Les messages d'un poste

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "postId":3,
  "messages:"
    [
      {
        "id": 1,
        "uid":2,
        "pid":3,
        "pinned":1,
        "content":"La basse c'est super cool",
      },
      {
        "id": 2,
        "uid":1,
        "pid":3,
        "pinned":0,
        "content":"ratio",
        "answerTo":1
      },
    ]
}
```

Cette route permet de récuperer la listes des messages envoyé sur un post

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /posts/{pid}/messages**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur


### Paramètres d'URL

Parameter | Description
--------- | -----------
pid | L'identifiant du post

# Agendas

## Lister Les calendriers

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "agendas":
    [
      {
      },

      {
      },
    ]
}
```

Cette route permet de récuperer la listes des calendriers

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /agendas/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">
  La réponses dépends des permissions de lecture de l'utilisateur
</aside>

## Lister Les évenements d'un calendrier

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "agendas":1,
  "events":
    [
      {
      },
      
      {
      },
    ]
}
```

Cette route permet de récuperer les événements d'un calendrier

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /agendas/[aid}/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Parameter | Description
--------- | -----------
aid | L'identifiant du calendrier

<aside class="notice">
  La réponses dépends des permissions de lecture de l'utilisateur sur le calendrier
</aside>

## Lister les membres de l'appel

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,
  "agendas":1,
  "event":2,
  "calls":
    [
      {
      },
      
      {
      },
    ]
}
```

Cette route permet de récuperer les informations concernant l'appel

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /agendas/{aid}/event/{eid}/calls**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Parameter | Description
--------- | -----------
aid | L'identifiant du calendrier
eid | L'identifiant de l'event

<aside class="notice">
  Seuls les membres du CA peuvent faire l'appel
</aside>

