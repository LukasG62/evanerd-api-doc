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

> Lors de l'authentification, la réponse JSON fournira un token permettant d'utiliser certaines fonctionalités de l'API.

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

Cette route permet la connection, en reseignant les bons champs, de l'utilisateur ciblé.

### Requête HTTP 

**<span style="color:rgb(255, 180, 0)">POST</span> /auth/**

### Paramètre de requête

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

> La requête renvoie un JSON sous la forme :

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

### Paramètre de requête

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

### Paramètre d'URL

Paramètre | Par défaut| Description
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

> La requête renvoie un JSON de l'utilisateur modifié sous la forme :

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

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
uid | | L'identifiant de l'utilisateur

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre de requête

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

> La requête renvoie un JSON de l'utilisateur modifié sous la forme :

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

### Paramètre de requête

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


## Ajouter une image à un utilisateur

```javascript
var form = new FormData();
form.append("image", fileInput.files[0], "chat.jpg");

var settings = {
  "url": "https://evanerds.fr/api/v1/users/1/image",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "e3ea73940b6cef3bd12bb72e3a519468"
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

> The above command returns JSON structured like this:

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
        "photo": "https://evanerds.fr/api/ressources/users/1/image.jpg",
        "activation": 1,
        "tel": "0780647980",
        "mail": "tomasSR@gmail.com"
    }
}
```

Cette route permet d'ajouter une photo de profil à un utilisateur.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/{uid}/image**

### Paramètre d'URL

Paramètre | Par défaut| Description
--------- | ----------- | -----------
uid | | L'identifiant de l'utilisateur

### Form data

Paramètre | Par défaut| Description
--------- | ----------- | -----------
image | | L'image à ajouter

<aside class="notice">
  L'extension de l'image est obligatoirement un ".png" ou ".jpg" ou ".gif". La taille maximale du fichier est de 25 mB.
</aside>

<aside class="warning">
  La taille maximale du fichier est de 25 mB.
</aside>


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

> La requête renvoie un JSON avec l'id de l'utilisateur et l'instrument ajouté.

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

Cette route permet d'ajouter un instrument à l'utilisateur connecté.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/instruments**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
iid |  | Id de l'instrument à ajouter

<aside class="notice">
   Un instrument ne peut être rajouté qu'une seule fois.
</aside>

## Ajouter un achievement à l'utilisateur

```javascript

// TODO

```

> La requête renvoie un JSON avec l'id de l'utilisateur et l'achievement ajouté.

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":201,

}
```

Cette route permet d'ajouter un achievement à l'utilisateur connecté.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/achievements**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
aid |  | Id de l'achievement

<aside class="notice">
   Un utilisateur ne peut avoir plusieurs fois le même achievement.
</aside>

<aside class="warning">
   Il faut que l'utilisateur satisfasse les conditions d'obtention de l'achievement pour le recevoir. Sinon la route renvoie
   un JSON d'erreur avec comme code de status 403.
</aside>

## Ajouter un rôle à un utilisateur

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

> La requête renvoie un JSON avec l'id de l'utilisateur et le rôle ajouté.

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

Cette route permet d'ajouter un rôle à l'utilisateur.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/{uid}/roles**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ----------- | -----------
uid | | Identifiant de l'utilisateur

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
rid |  | Id du rôle

<aside class="notice">
   Seuls les membres du CA peuvent ajouter un rôle, dans les autres cas, la route renverra un JSON d'erreur avec comme statut 403.
</aside>

## Vérifier l'email d'un utilisateur

```javascript
  var settings = {
  "url": "https://evanerds.fr/api/v1/users/verify?token=confirme",
  "method": "POST",
  "timeout": 0,
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

> Cette route renvoie un JSON sous la forme 

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
        "id": 6,
        "firstName": "Pablo",
        "lastName": "Lito",
        "sex": 0,
        "age": 12,
        "studies": "Diplômé",
        "photo": "https://evanerds.fr/api/ressources/users/6/default.png",
        "activation": 1
    }
}
```

Cette route permet de vérifier l'email d'un utilisateur.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/verify**

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
token |  | Token d'activation du compte

## Réinitialiser son mot de passe

```javascript
  var settings = {
  "url": "https://evanerds.fr/api/v1/users/reset?resetToken=test&password=youhou1234",
  "method": "POST",
  "timeout": 0,
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

> Cette route renvoie un JSON sous la forme 

```json
  {
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
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
}
```

Cette route permet de réinitialiser le mot de passe de l'utilisateur.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/reset**

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
resetToken |  | Token de réinitialisation
password | | Nouveau mot de passe renseigné

<aside class="warning">
  Le resetToken est généré à partir des mails. Pour tester cette requête, vous pouvez modifier le resetToken dans la base de donnée.
</aside>

## Déconnecter l'utilisateur connecté

```javascript
var settings = {
  "url": "https://evanerds.fr/api/v1/users/logout",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "e3ea73940b6cef3bd12bb72e3a519468"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

> Cette route renvoie un JSON sous la forme 

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
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
}
```

Cette route permet de déconnecter l'utilisateur connecté.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /users/logout**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur



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

> La requête renvoie un JSON sous la forme :

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

### Paramètre de requête

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

> La requête renvoie un JSON sous la forme :

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

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
rid |  | Permet de modifier le rôle indiqué

### Paramètre de requête

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

> La requête renvoie un JSON sous la forme :

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

### Paramètre de requête

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

> La requête renvoie un JSON sous la forme :

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


### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

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

> La requête renvoie un JSON sous la forme :

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

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
iid |  | Identifiant de l'instrument

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
label |  | Nouveau nom de l'instrument

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

> La requête renvoie un JSON sous la forme :

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

### Paramètre de requête

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

> La requête renvoie un JSON sous la forme :

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

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
token |  | Token d'activation du compte

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

> La requête renvoie un JSON sous la forme :

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

Cette route permet de récuperer une liste des groupes de l'utilisateur connecté.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

## Lister les permissions d'un groupe

```javascript
var settings = {
  "url": "https://evanerds.fr/api/v1/groups/1/permissions",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});
```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "permissions": []
}
```

Cette route permet de récupérer la liste des permissions d'un groupe.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups/{gid}/permissions/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
gid |  | Identifiant du groupe

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

> La requête renvoie un JSON sous la forme :

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

Cette route permet de récuperer la liste des messages envoyés dans le groupe.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups/{gid}/messages**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
gid | | Identifiant du groupe


## Epingler un message

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/groups/1/messages/4/pinned",
  "method": "PUT",
  "timeout": 0,
  "headers": {
    "authToken": "9aa424f9cec0956a0e94640d3bed9c70"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "message": {
        "id": 4,
        "uid": 1,
        "gid": 1,
        "pinned": 0,
        "content": "Je suis le message épinglé !",
        "answerTo": null
    }
}
```

Cette route permet d'épingler un message d'une groupe.


### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /groups/{gid}/messages/{mid}/pinned**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
gid | | Identifiant du groupe
mid | | Identifiant du messages

<aside class="notice">
  Si le message est épinglé, il sera désépinglé et inversement.
</aside>

## Modifier le titre d'un groupe

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/groups/5?title=trucbidule",
  "method": "PUT",
  "timeout": 0,
  "headers": {
    "authToken": "9aa424f9cec0956a0e94640d3bed9c70"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "group": {
        "id": 5,
        "titre": "trucbidule",
        "image": "https://evanerds.fr/api/ressources/groups/5/image.webp"
    }
}
```

Cette route permet de modifier le titre d'un groupe.


### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /groups/{gid}/messages/{mid}/pinned**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
gid | | Identifiant du groupe
mid | | Identifiant du messages

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
title | | Nouveau nom du groupe


## Créer un groupe pour l'utilisateur connecté
```javascript

var form = new FormData();
form.append("image", fileInput.files[0], "tux.png");

var settings = {
  "url": "https://evanerds.fr/api/v1/groups?title=Les Copines d'Abord",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
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

> La requête renvoie un JSON sous la forme :

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

Cette route permet de créer un groupe pour l'utilisateur connecté.

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
L'utilisateur connecté est directement ajouté au groupe créé.
</aside>

## Ajouter un utilisateur au groupe
```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/groups/2/users/10",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "user": {
        "id": 10,
        "firstName": "Alexandre",
        "lastName": "Fizel",
        "sex": 0,
        "age": 19,
        "studies": "IG2I, Centrale Lille",
        "photo": "https://evanerds.fr/api/ressources/users/10/image.png",
        "activation": 1
    }
}
```

Cette route permet d'ajouter un utilisateur au groupe.

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
L'utilisateur connecté doit appartenir au groupe pour pouvoir ajouter un utilisateur.
</aside>

## Envoyer un message dans le groupe
```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/groups/1/messages?content=Salut !!&answerTo",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "message": {
        "id": "288",
        "content": "Salut !!",
        "pinned": 0,
        "answerTo": null
    }
}
```

Cette route permet d'envoyer un message dans le groupe.

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
L'utilisateur connecté doit appartenir au groupe pour envoyer un message.
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

> La requête renvoie un JSON sous la forme :

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

Cette route permet de récupérer la liste des posts. 

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

> La requête renvoie un JSON sous la forme :

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

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
pid |  | Identifiant du post

<aside class="warning">
  Parfois, l'emoji ne passe pas.
</aside>

## Lister les "likes" d'un post

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/posts/1/likes",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "9aa424f9cec0956a0e94640d3bed9c70"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "postId": 1,
    "total": 5,
    "likes": [
        {
            "id": 1,
            "firstName": "Tomas",
            "lastName": "Salvado Robalo",
            "photo": "https://evanerds.fr/api/ressources/users/1/image.jpg"
        },
        {
            "id": 6,
            "firstName": "Pablo",
            "lastName": "Lito",
            "photo": "https://evanerds.fr/api/ressources/users/6/default.png"
        }
    ]
}
```

Cette route permet de récupérer les likes sur un post.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /posts/{pid}/reactions**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
pid |  | Identifiant du post


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

> La requête renvoie un JSON sous la forme :

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

Cette route permet de récupérer la liste des messages envoyé sur un post.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /posts/{pid}/messages**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur


### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
pid | | Identifiant du post

## Epingler un post
```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/posts/1/pinned?pinned=1",
  "method": "PUT",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "post": {
        "id": 1,
        "author": 2,
        "content": "J'annonce mon arrivé au sein de CA !! J'espère vous êtes contents !!\nΣ>―(〃°ω°〃)♡→\n\n",
        "banner": null,
        "pinned": 0,
        "visible": 1
    }
}
```

Cette route permet d'épingler un post.

### Requête HTTP

**<span style="color:rgb(9, 123, 237)">PUT</span> /posts/{pid}/pinned**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
pid | | Identifiant du post

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
pinned |  | Booléen qui définit s'il est pin ou non


<aside class="notice">

   Les membres du CA peuvent épingler les posts des utilisateurs. Un autre membre du CA peut desépingler les posts.
</aside>


## Créer un post

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

> La requête renvoie un JSON sous la forme :

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

Cette route permet de créer un post.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /posts**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken | | Token d'identification de l'utilisateur

### Paramètre de requête

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

## Liker un post

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/posts/1/likes",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "like": {
        "uid": 6,
        "pid": 1,
        "liked": true
    }
}
```

Cette route permet d'aimer ou te détester un post.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /posts/{pid}/liked**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
pid |  | Identifiant du post

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
liked |  | Booléen qui définit s'il est like ou non

## Poster une réaction sur un post 

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/posts/1/reactions?emoji=😋",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "reaction": "😋",
    "postId": 1
}
```

Cette route permet d'ajouter une réaction un post.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /posts/{pid}/pinned**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
pid | | Identifiant du post

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
pinned |  | Booléen qui définit s'il est pin ou non

## Poster un commentaire sous un post

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/posts/1/messages?content=Je suis le contenu de réponse !!",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "9aa424f9cec0956a0e94640d3bed9c70"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "comment": {
        "id": "98",
        "content": "Je suis le contenu de réponse !!",
        "pinned": 0,
        "answerTo": null
    }
}
```

Cette route permet d'ajouter un commentaire sous un post.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /posts/{pid}/liked**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
pid |  | Identifiant du post

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
content |  | Le contenu du commentaire sous le post

# Agendas

## Créer un calendrier

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/agendas/?type=intra&title=test",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "agenda": {
        "id": "3",
        "title": "test",
        "extra": 0
    }
}
```

Cette route permet de créer un calendrier.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /agendas/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">
  La réponse dépend des permissions de lecture de l'utilisateur.
</aside>

## Créer un événement d'un calendrier

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/agendas/1/events?event=oui&start=2023-05-15 15:22:15&end=2023-05-15 16:18:46&description=c'est un test",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "event": {
        "id": "25",
        "event": "oui",
        "description": "c'est un test",
        "start": "2023-05-15 15:22:15",
        "end": "2023-05-15 16:18:46"
    }
}
```

Cette route permet de créer un événement d'un calendrier.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /agendas/{aid}/events**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
aid | | Identifiant du calendrier

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
event  |  | Nom de l'événement
description | |Description de l'événement
start | | Date de début de l'événement
end | | Date de fin de l'événement

<aside class="notice">
  La réponse dépend des permissions de lecture de l'utilisateur sur le calendrier.
</aside>

# Events

## Lister les événements

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/agendas/?type=intra&title=test",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "events": [
        {
            "id": 8,
            "aid": 2,
            "startDate": "2023-04-19 22:41:10",
            "endDate": "2023-04-19 23:45:15",
            "event": "Saut en parachute",
            "description": "blablabla"
        },
        {
            "id": 7,
            "aid": 2,
            "startDate": "2023-06-08 15:43:26",
            "endDate": "2023-08-04 15:43:26",
            "event": "la réunion de fin d'année",
            "description": "adieu les copains"
        }
    ]
}
```

Cette route permet de lister les événements.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /events/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
type  |  | Le type de l'événement
all | | Si on veut tous les événements


<aside class="notice">
  La réponse dépend des permissions de lecture de l'utilisateur.
</aside>

## Lister les participations de l'utilisateur

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/events/1/participations",
  "method": "GET",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "eventId": 1,
    "participationsRatio": "0.3636",
    "participations": {
        "y": [
            {
                "user": {
                    "id": 2,
                    "firstName": "Pedro",
                    "lastName": "Lito",
                    "photo": "https://evanerds.fr/api/ressources/users/2/image.png"
                }
            },
            {
                "user": {
                    "id": 12,
                    "firstName": "Augustin",
                    "lastName": "Husson",
                    "photo": "https://evanerds.fr/api/ressources/users/12/image.png"
                }
            }
        ],
        "n": [
            {
                "user": {
                    "id": 4,
                    "firstName": "Leevan",
                    "lastName": "David",
                    "photo": "https://evanerds.fr/api/ressources/users/4/default.png"
                }
            }
        ]
    }
}
```

Cette route permet de lister les événements.

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /events/**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
type  |  | Le type de l'événement
all | | Si on veut tous les événements


<aside class="warning">
  Le ratio est calculé en fonction du nombre de participation. Il se peut qu'il y ait une division par 0, qui renvoie un NaN.
</aside>


## Justifier son absence 

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/events/8/calls?present=0&reason=Je suis enrhumé",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});

```

> La requête renvoie un JSON sous la forme :

```json
{
    "apiname": "EVANERD API",
    "version": "1.0",
    "call": {
        "uid": 6,
        "present": 0,
        "eid": 8,
        "reason_desc": "Je suis enrhumé"
    }
}
```

Cette route permet de justifier son absence.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> /events/{eid}/calls**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
eid | | Identifiant de l'événement

### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
present *<span style="color:red">[OPTIONNEL]</span>* | 0 | Si l'utilisateur est présent ou non
reason  |  | La raison de l'absence

# Participations

## Modifier la présence d'un utilisateur

```javascript

// TODO

```

> La requête renvoie un JSON sous la forme :

```json

// TODO

```

Cette route permet de créer une participation d'un utilisateur à un événement.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">PUT</span> users/{uid}/agendas/{aeid}/calls**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken  |  | Token d'identification de l'utilisateur


### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
uid |  | Identifiant de l'utilisateur
aeid |  | Identifiant de l'événement dans l'agenda


### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
present |  | Si l'utilisateur est présent ou non
reason  *<span style="color:red">[OPTIONNEL]</span>* |  | Ajout d'une raison s'il n'est pas présent

## Ajouter une participation

```javascript

var settings = {
  "url": "https://evanerds.fr/api/v1/events/8/calls?present=0&reason=Je suis enrhumé",
  "method": "POST",
  "timeout": 0,
  "headers": {
    "authToken": "178b5d5e9c38b626cd02e26ef7974d87"
  },
};

$.ajax(settings).done(function (response) {
  console.log(response);
});


```

> La requête renvoie un JSON sous la forme :

```json
  {
    "apiname": "EVANERD API",
    "version": "1.0",
    "call": {
        "uid": 6,
        "present": 0,
        "eid": 8,
        "reason_desc": "Je suis enrhumé"
    }
}
```

Cette route permet de modifier une participation d'un utilisateur à un événement.

### Requête HTTP

**<span style="color:rgb(255, 180, 0)">POST</span> users/{uid}/agendas/{aeid}/participations?participation=?**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken  |  | Token d'identification de l'utilisateur


### Paramètre d'URL

Paramètre | Par défaut | Description
--------- | ------- | -----------
uid |  | Identifiant de l'utilisateur
aeid |  | Identifiant de l'événement dans l'agenda


### Paramètre de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
participation |  | Si la personne participe ou non
