---
title: Documentation API EVANERDS

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
    content: Documentation for the Evanerds API
---

# Introduction

Documentation de l'API utilisé lors de la réalisation du développement du Projet PINF pour l'Orchestre Etudiant de Toulouse, lors de la deuxième année à l'IG2I, Ecole de Génie Industriel et Informatique. 

2022-2023, Groupe Evanerd.

# Authentification

## Récupérer le token d'authentification

```javascript
var settings = {
  "url": "https://evanerds.fr/api/v1/auth?tel=0256696969&password=ecayon",
  "method": "POST",
  "timeout": 0,
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

> Lors de l'authentification, la réponse JSON fournira un token permettant d'utiliser certaines fonctionalités de l'API

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "authToken": "9834b0496e636d98d8623ed5de8d1692",
    "user": {
        "id": 2,
        "firstName": "Pedro",
        "lastName": "Lito",
        "sex": 1,
        "age": 2,
        "studies": "Déscolarisé",
        "photo": "https://evanerds.fr/api/ressources/users/2/image.png",
        "activation": 1,
        "tel": "0256696969",
        "mail": "pedrolito@orange.fr",
        "admin": 1,
        "noMember": 0
    }
}
```
### Requête HTTP :

**<span style="color:rgb(255, 180, 0)">POST</span> /auth/**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
tel |  | Numéro de téléphone de l'utilisateur
password | | Mot de passe de l'utilisateur

<aside class="notice">
Lors de la connexion, un nouveau token est généré, rendant l'ancien inutilisable.
</aside>

<aside class="warning">
L'utilisateur doit avoir un compte activé (compte vérifié par email).
</aside>

# Users

## Lister les utilisateurs

```javascript
var settings = {
  "url": "https://evanerds.fr/api/v1/users?idRole=1",
  "method": "GET",
  "timeout": 0,
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "users": [
        {
            "id": 2,
            "firstName": "Pedro",
            "lastName": "Lito",
            "sex": 1,
            "age": 2,
            "studies": "Déscolarisé",
            "photo": "https://evanerds.fr/api/ressources/users/2/image.png",
            "activation": 1
        },
        {
            "id": 6,
            "firstName": "Pablo",
            "lastName": "Lito",
            "sex": 0,
            "age": 19,
            "studies": "IG2I, Centrale Lille",
            "photo": "https://evanerds.fr/api/ressources/users/6/default.png",
            "activation": 1
        }
    ]
}
```

Cette route permet de récupérer une liste d'utilisateur. On peut ajouter des paramètres pour complémenter la recherche, comme l'id du rôle en question ou le nom ou prénom de l'utilisateur.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /users**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
idRole *<span style="color:red">[OPTIONNEL]</span>* |  | Permet de lister tous les utilisateurs possédant le rôle indiqué
name *<span style="color:red">[OPTIONNEL]</span>* |  | Permet de lister tous les utilisateurs possédant le nom ou le prénom indiqué


<aside class="notice">
Les deux paramètres peuvent être mis en place lors de la requête. Si la donnée n'existe pas, la requête renvoit un JSON vide.
</aside>

## Récupérer un utilisateur

```javascript
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
        "id": 2,
        "firstName": "Pedro",
        "lastName": "Lito",
        "sex": 1,
        "age": 2,
        "studies": "Déscolarisé",
        "photo": "https://evanerds.fr/api/ressources/users/2/image.png",
        "activation": 1
    }
}
```

> The above command returns JSON structured like this:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
        "id": 2,
        "firstName": "Pedro",
        "lastName": "Lito",
        "sex": 1,
        "age": 2,
        "studies": "Déscolarisé",
        "photo": "https://evanerds.fr/api/ressources/users/2/image.png",
        "activation": 1
    }
}
```

Cette route permet de récupérer un seul utilisateur selon son id.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /users/{uid}**

### Paramètres d'URL

Parameter | Par défaut| Description
--------- | ----------- | -----------
uid | | L'identifiant de l'utilisateur

<aside class="notice">
  Dans le cas ou l'uid utilisateur est celui de l'utilisateur connecté, la réponse envoie l'email et le numéro de téléphone de l'utilisateur.
</aside>

## Modifier un utilisateur

```javascript
var form = new FormData();
var settings = {
  "url": "https://evanerds.fr/api/v1/users/6",
  "method": "PUT",
  "timeout": 0,
  "headers": {
    "authToken": "2f25b70605b9e8fc308d2e879b662767"
  },
  "processData": false,
  "mimeType": "multipart/form-data",
  "contentType": false,
  "data": form
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

> La requête renvoie un JSON de l'utilisateur modifié sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": [
        {
            "id": 6,
            "firstName": "Pablo",
            "lastName": "Lito",
            "sex": 0,
            "age": 12,
            "studies": "Diplômé",
            "photo": "https://evanerds.fr/api/ressources/users/6/default.png",
            "activation": 1,
            "tel": "0202030405",
            "mail": "test@youhou.fr"
        }
    ]
}
```

Cette route permet de modifier les informations (mail, numéro de téléphone...) d'un utilisateur présent dans la base de donnée.

### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /users/{uid}**

### Paramètres d'URL

Parameter | Par défaut | Description
--------- | ------- | -----------
uid | | L'identifiant de l'utilisateur

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
firstName <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son prénom
lastName <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifer son nom
age <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son âge
sex <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son sexe
mail <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son mail
tel <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son numéro de téléphone
studies <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier ses l'intitulé de ses études
password <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son mot de passe

<aside class="notice">
  Les membres du CA peuvent modifier les informations de tous les utilisateurs. Un utilisateur ne peut modifier que ses propres informations.
</aside>

<aside class="warning">
  Cette route ne permet pas de modifier l'image d'un utilisateur.
</aside>

<aside class="warning">
  Si l'utilisateur n'a pas les permissions pour modifier un utilisateur alors la route enverra un JSON d'erreur avec un status code 403.
</aside>

## Créer un utilisateur

```javascript

var form = new FormData();
var settings = {
  "url": "https://evanerds.fr/api/v1/users?firstName=Super&lastName=LePinf&age=19&sex=0&mail=osettes2t@yopmail.com&tel=0790652329&studies=IG2I, Centrale Lille&password=pi13456&iid=iid[]=1",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "0202030405"
  },
  "processData": false,
  "mimeType": "multipart/form-data",
  "contentType": false,
  "data": form
};

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
      "firstName": "Namu",
      "lastName": "Litos",
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
age |  | Âge de l'utilisateur
studies <span style="color:red">[OPTIONNEL]</span> |  | Etudes de l'utilisateur
sex <span style="color:red">[OPTIONNEL]</span> |  | Genre de l'utilisateur
image <span style="color:red">[OPTIONNEL]</span> |  | Image de profil sous format base64


## Ajouter un instrument à l'utilisateur

```javascript
var settings = {
  "url": "https://evanerds.fr/api/v1/users/instruments?iid=1",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "815d7d4197afb6b9d3df8d744d0a8bd5"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON avec l'id de l'utilisateur et l'instrument ajouté

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "instrument": {
        "id": 1,
        "label": "Flute"
    }
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
iid |  | Id de l'instrument à ajouter

<aside class="notice">
   Un instrument ne peut être rajouté qu'une seule fois
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

**<span style="color:rgb(255, 180, 0)">POST</span> /users/achievements**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
aid |  | Id de l'achievement

<aside class="notice">
   Un utilisateur ne peut avoir plusieurs fois le même achievement
</aside>

<aside class="warning">
   Il faut que l'utilisateur satisfasse les conditions d'obtention de l'achievement pour le recevoir. Sinon la route renvoie
   un JSON d'erreur avec comme code de status 403
</aside>

## Ajout d'un rôle à un utilisateur

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/users/4/roles?rid=1",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "3bdc80f6ed463940c4cc4a9fb78704a3"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON avec l'id de l'utilisateur et le rôle ajouté

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
        "id": 4,
        "firstName": "N",
        "lastName": "twitch.tv/NamuFoxyy",
        "sex": 0,
        "age": 19,
        "studies": "IG2I, Centrale Lille",
        "photo": "https://evanerds.fr/api/ressources/users/4/default.png",
        "activation": 1
    },
    "role": {
        "id": 1,
        "label": "Membre du CA",
        "active": 1
    }
}
```

Cette route permet d'ajouter un rôle à l'utilisateur

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/{uid}/roles**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Paramètre | Par défaut | Description
--------- | ----------- | -----------
uid | | Identifiant de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
rid |  | Id du rôle

<aside class="notice">
   Seuls les membres du CA peuvent ajouter un rôle, dans les autres cas, la route renverra un JSON d'erreur avec comme statut 403
</aside>

## Vérifier l'email d'un utilisateur

```javascript
  //TODO
```

> Cette route renvoie un JSON sous la forme 

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
        "id": 1,
        "firstName": "Lukas",
        "lastName": "Grando",
        "sex": 1,
        "age": 19,
        "studies": "IG2I",
        "photo": "http://localhost/ressources/users/1/default.png",
        "activation": 1
    }
}
```

Cette route permet de vérifier l'email d'un utilisateur

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/verify**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
token |  | Token d'activation du compte


# Rôles

## Lister les rôles

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/roles",
  "method": "GET",
  "timeout": 0,
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "roles": [
        {
            "id": 1,
            "label": "Trésorier",
            "active": 1
        },
        {
            "id": 2,
            "label": "Membre du CA",
            "active": 1
        },
        {
            "id": 3,
            "label": "Membre du CA 2020",
            "active": 0
        }
    ]
}
```

Cette route permet de récuperer la liste des rôles.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /roles/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
active | "both" | Permet de préciser : 0 = Rôles inactifs; 1 = Rôles actifs; "both" = Les deux;

## Modifier un rôle

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/roles/1?label=Membre du CA 2024",
  "method": "PUT",
  "timeout": 0,
  "headers": {
    "authToken": "3bdc80f6ed463940c4cc4a9fb78704a3"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "role": {
        "id": 1,
        "label": "Membre du CA 2024",
        "active": 1
    }
}
```

Cette route permet de modifier les paramètres d'un rôle (label, actif).

### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /roles/{rid}**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
rid |  | Permet de modifier le rôle indiqué

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
label *<span style="color:red">[OPTIONNEL]</span>* |  | Permet de modifier le nom du rôle
active *<span style="color:red">[OPTIONNEL]</span>* | 1 | Si le rôle est actif



## Créer un rôle

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/roles?label=test&active=0",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "025e69eca5d7ba55d84e6f7222bb290e"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "role": {
        "id": 7,
        "label": "test",
        "active": 0
    }
}
```

Cette route permet de créer un rôle.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /roles**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
label |  | Permet de modifier le nom du rôle
active *<span style="color:red">[OPTIONNEL]</span>* | 1 | Si le rôle est actif


# Instruments 

## Lister tous les instruments

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/instruments",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "3bdc80f6ed463940c4cc4a9fb78704a3"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "instruments": [
        {
            "id": 1,
            "label": "Flute"
        },
        {
            "id": 2,
            "label": "Banjo"
        },
        {
            "id": 3,
            "label": "Guitare"
        }
    ]
}
```

Cette route permet de retourner tous les instruments.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /instruments**


### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
token |  | Token d'activation du compte

## Modifier un instrument

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/instruments/7?label=Flûte",
  "method": "PUT",
  "timeout": 0,
  "headers": {
    "authToken": "3bdc80f6ed463940c4cc4a9fb78704a3"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "instrument": {
        "id": 7,
        "label": "Flûte"
    }
}
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
label |  | Identifiant de l'instrument

## Créer un instrument

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/instruments?label=Saxophone",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "36d4e93d57c3118083dbc27e0a04f8be"
  },
};


```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "instrument": {
        "id": "11",
        "label": "Saxophone"
    }
}
```

Cette route permet de créer un instrument.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /instruments**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
label |  | Nom de l'instrument

# Achievements 

## Lister tous les achievements

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/achievements",
  "method": "GET",
  "timeout": 0,
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "achievements": [
        {
            "id": 10,
            "label": "Bavard"
        },
        {
            "id": 11,
            "label": "Loquace"
        }
    ]
}
```

Cette route permet de retourner tous les achievements.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /achievements**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
token |  | Token d'activation du compte

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
achivid |  | Identifiant de l'achievement

### Paramètres de rêquete

Paramètre | Par défaut | Description
--------- | ------- | -----------
label |  | Titre de l'achievement

# Groups

## Lister les groupes de l'utilisateur connecté

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/groups",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "2b42eb74498038880b5c533854c626ea"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "groups": [
        {
            "id": 1,
            "titre": "Conersation Sympa",
            "image": "https://evanerds.fr/api/ressources/groups/1/image.jpg"
        },
        {
            "id": 21,
            "titre": "Copains d'Abord",
            "image": "https://evanerds.fr/api/ressources/groups/21/default.png"
        }
    ]
}
```

Cette route permet de récupérer la liste des conversations d'un utilisateur

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

## Lister les permissions d'un groupe

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

Cette route permet de récupérer la liste des permissions d'un groupe

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups/{gid}/permissions/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">
  Si un groupe n'a pas de permissions affectées, alors il n'y a aucune restriction de rôle sur le groupe. 
  Par conséquent, tout utilisateur membre peut y être ajouté.
</aside>

## Lister les messages d'un groupe de l'utilisateur connecté

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/groups/2/messages",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "2b42eb74498038880b5c533854c626ea"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "groupId": 2,
    "messages": [
        {
            "id": 32,
            "author": {
                "id": 2,
                "firstName": "Pedro",
                "lastName": "Lito",
                "photo": "https://evanerds.fr/api/ressources/users/2/image.png"
            },
            "content": "44",
            "pinned": 0,
            "answerTo": null
        },
        {
            "id": 167,
            "author": {
                "id": 2,
                "firstName": "Pedro",
                "lastName": "Lito",
                "photo": "https://evanerds.fr/api/ressources/users/2/image.png"
            },
            "content": "hey",
            "pinned": 0,
            "answerTo": 165
        }
    ]
}
```

Cette route permet de récuperer la liste des messages envoyés dans le groupe

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups/{gid}/messages**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Parameter | Par défaut | Description
--------- | ------- | -----------
gid | | Identifiant du groupe

## Lister les réactions d'un message de groupe

```javascript
// TODO CODE AJAX
```

> La requête renvoie un JSON sous la forme:

```json
```

Cette route permet de récupérer la liste des réactions d'un message de groupe

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups/{gid}/messages/{mid}**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur


### Paramètres d'URL

Parameter | Par défaut | Description
--------- | ------- | -----------
gid | | Identifiant du groupe
mid | | Identifiant du message

## Créer un groupe pour l'utilisateur connecté
```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "group": {
        "id": 6,
        "titre": "Les Copines d\\'Abord",
        "image": "http://localhost/EvaNerd/Back Evanerd/ressources/groups/6/default.png"
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
image *<span style="color:red">[OPTIONNEL]</span>* |  | Donnée de l'image sous le format base64
title *<span style="color:red">[OPTIONNEL]</span>*  |  | Titre de la discussion

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
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
        "id": 1,
        "firstName": "Tomas",
        "lastName": "Salvado Robalo",
        "sex": 0,
        "age": 666,
        "studies": "IG2I, Centrale Lille",
        "photo": "http://localhost/EvaNerd/Back Evanerd/ressources/users/1/default.png",
        "activation": 1
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
gid | | Identifiant du groupe
uid | | Identifiant du l'utilisateur

<aside class="notice">
L'utilisateur connecté doit appartenir au groupe pour pouvoir ajouter un utilisateur
</aside>

## Envoyer un message dans le groupe
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
answerTo <span style="color:red">[OPTIONNEL] |  | Identifiant du message cible

<aside class="notice">
L'utilisateur connecté doit appartenir au groupe pour envoyer un message
</aside>

# Posts

## Lister les posts

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/posts",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "025e69eca5d7ba55d84e6f7222bb290e"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "posts": [
        {
            "id": 1,
            "author": {
                "id": 2,
                "firstName": "Pedro",
                "lastName": "Lito",
                "photo": "http://localhost/EvaNerd/Back Evanerd/ressources/users/2/default.png"
            },
            "content": "J'annonce mon arrivé au sein de CA !!\n\n",
            "pinned": 1,
            "visible": 1,
            "banner": null
        }
    ]
}
```

Cette route permet de récupérer la liste des posts 

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /posts/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">
  La liste de posts dépend du rôle de l'utilisateur, si l'utilisateur connecté est un non-membre alors il verra que les posts avec l'attribut visible à 1.
</aside>

## Lister les réactions d'un post

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/posts/1/reactions",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "025e69eca5d7ba55d84e6f7222bb290e"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "postId": 1,
    "reactions": {
        "🤓": [
            {
                "uid": 2,
                "firstName": "Pedro",
                "lastName": "Lito",
                "photo": "https://evanerds.fr/api/ressources/users/2/image.png"
            }
        ]
    }
}
```

Cette route permet de récupérer les réactions sur un post.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /posts/{pid}/reactions**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="warning">
  Parfois, l'emoji ne passe pas.
</aside>

## Lister les messages d'un post

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/posts/1/messages",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "025e69eca5d7ba55d84e6f7222bb290e"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "idPost": 5,
    "comments": [
        {
            "id": 1,
            "author": {
                "id": 2,
                "firstName": "Pedro",
                "lastName": "Lito",
                "photo": "http://localhost/EvaNerd/Back Evanerd/ressources/users/2/default.png"
            },
            "content": "salut",
            "pinned": 0,
            "answerTo": null
        },
        {
            "id": 2,
            "author": {
                "id": 2,
                "firstName": "Pedro",
                "lastName": "Lito",
                "photo": "http://localhost/EvaNerd/Back Evanerd/ressources/users/2/default.png"
            },
            "content": "ça va ?",
            "pinned": 0,
            "answerTo": 1
        }
    ]
}
```

Cette route permet de récupérer la liste des messages envoyé sur un post

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /posts/{pid}/messages**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur


### Paramètres d'URL

Parameter |Par défaut | Description
--------- | ------- | -----------
pid | | Identifiant du post

## Poster un post

```javascript

var form = new FormData();
form.append("banner", fileInput.files[0], "etudiants2016.jpg");

var settings = {
  "url": "https://evanerds.fr/api/v1/posts?visible=1&content=Bon mardi&pinned=1",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "025e69eca5d7ba55d84e6f7222bb290e"
  },
  "processData": false,
  "mimeType": "multipart/form-data",
  "contentType": false,
  "data": form
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "post": {
        "id": 34,
        "author": 6,
        "content": "Bon mardi",
        "banner": "image.jpg",
        "pinned": 1,
        "visible": 1
    }
}
```

Cette route permet de créer un post

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /posts**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken | | Token d'identification de l'utilisateur

### Paramètres d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
content |  | Contenu du post
visible | | Pour définir si le post est visible pour tout le monde ou non

### Form data

Paramètre |  Par défaut | Description
--------- | ------- | -----------
banner | | Image du post

<aside class="notice">
  ll faut obligatoirement fournir une image pour la réalisation de la requête.
</aside>

## Poster un like sur un post

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
}
```

Cette route permet de liker un post

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /posts/{pid}/liked**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
liked |  | Booléen qui définit s'il est like ou non

## Epingler un post
```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
}
```

Cette route permet d'epingler un post

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /posts/{pid}/pinned**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
pinned |  | Booléen qui définit s'il est pin ou non

### Paramètres d'URL

Parameter | Par défaut | Description
--------- | ------- | -----------
pid | | Identifiant du post

<aside class="notice">

   Les membres du CA peuvent épingler les posts des utilisateurs. Un autre membre du CA peut desépingler les posts.
</aside>

## Poster une réaction sur un post 

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
}
```

Cette route permet d'ajouter une réaction un post

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /posts/{pid}/pinned**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
pinned |  | Booléen qui définit s'il est pin ou non

### Paramètres d'URL

Parameter | Par défaut | Description
--------- | ------- | -----------
pid | | Identifiant du post

# Agendas

## Lister les calendriers

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

Cette route permet de récupérer la liste des calendriers

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /agendas/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">
  La réponse dépend des permissions de lecture de l'utilisateur
</aside>

## Lister les événements d'un calendrier

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

Cette route permet de récupérer les événements d'un calendrier

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /agendas/{aid}/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Parameter | Par défaut | Description
--------- | ------- | -----------
aid | | Identifiant du calendrier

<aside class="notice">
  La réponse dépend des permissions de lecture de l'utilisateur sur le calendrier
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

Cette route permet de récupérer les informations concernant l'appel

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /agendas/{aid}/event/{eid}/calls**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Parameter | Par défaut | Description
--------- | ------- | -----------
aid | | Identifiant du calendrier
eid | | Identifiant de l'event

<aside class="notice">
  Seuls les membres du CA peuvent faire l'appel
</aside>

## Créer un calendrier

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

Cette route permet de créer un calendrier

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /agendas/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">
  La réponse dépend des permissions de lecture de l'utilisateur
</aside>

## Créer un événement d'un calendrier

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

Cette route permet de créer un événement d'un calendrier

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /agendas/{aid}/events**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres d'URL

Parameter | Par défaut | Description
--------- | ------- | -----------
aid | | Identifiant du calendrier

<aside class="notice">
  La réponse dépend des permissions de lecture de l'utilisateur sur le calendrier
</aside>

# Participations

## Lister les participations

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
  A DEFINIR
```

Cette route permet de récupérer une liste d'utilisateur d'un événement

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /users/{uid}/agendas/{aeid}/participations**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken  |  | Token d'identification de l'utilisateur
uid |  | Identifiant de l'utilisateur
aeid |  | Identifiant de l'événement dans l'agenda

## Modifier une participation

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
  A DEFINIR
```

Cette route permet de modifier la participation d'un utilisateur à un événement

### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> users/{uid}/agendas/{aeid}/participations?participation=?**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken  |  | Token d'identification de l'utilisateur
uid |  | Identifiant de l'utilisateur
aeid |  | Identifiant de l'événement dans l'agenda
participation |  | Si la personne participe ou non

## Ajouter une participation

```javascript

// TODO CODE AJAX

```

> La requête renvoie un JSON sous la forme:

```json
  A DEFINIR
```

Cette route permet de créer une participation d'un utilisateur à un événement

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> users/{uid}/agendas/{aeid}/participations?participation=?**

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken  |  | Token d'identification de l'utilisateur
uid |  | Identifiant de l'utilisateur
aeid |  | Identifiant de l'événement dans l'agenda
participation |  | Si la personne participe ou non
