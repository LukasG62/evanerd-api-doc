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

Ceci est la documentation de l'api ...

# Authentification

> Lors de l'authentification

```javascript
```
### Requête HTTP

**<span style="rgb(255, 180, 0)">POST</span> /auth/**

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
        "photo":"www.example/users/1.png"
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
        "photo":"www.example/users/2.png"
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
      "photo":"www.example/users/1.png"
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
      "photo":"www.example/users/1.png"
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
password <span style="color:red">[OPTIONNEL]</span> |  | Permet de modifier son mot de passe

<aside class="notice">

   Les membres du CA peuvent modifier les informations de tous les utilisateurs. Un utilisateur ne peut modifier que ses propres informations.
</aside>

<aside class="warning">
  Si l'utilisateur n'a pas les permissions pour modifier un utilisateur alors la route enverra un JSON d'erreur avec un status code 403.
</aside>


## Supprimer un utilisateur

```javascript

//TODO

```

> La requête renvoie un JSON de l'utilisateur supprimé sous la forme:

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
      "studies":"Centrale Lille IG2Ix",
      "photo":"www.example/users/1.png"
    },
}
```

Cette route permet de supprimer un utilisateur

### Requête HTTP

**<span style="rgb(235, 32, 19)">DEL</span> /users/{uid}**

### Paramètres d'URL

Parameter | Description
--------- | -----------
uid | L'identifiant de l'utilisateur

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

<aside class="notice">

   Les membres du CA peuvent supprimer tous les utilisateurs. Un utilisateur ne peut supprimer que son propre compte.
</aside>

<aside class="warning">
  Si l'utilisateur n'a pas les permissions pour supprimer un utilisateur alors la route enverra un JSON d'erreur avec un status code 403.
</aside>

## Ajout un instrument à l'utilisateur

```javascript

//TODO

```

> La requête renvoie un JSON avec l'id de l'utilisateur et l'instrument ajouté

```json
{
  "apiname":"EVANERD API",
  "version":"1.0",
  "status":200,

}
```

Cette route permet d'ajouter un instrument à l'utilisateur connecté

### Requête HTTP

**<span style="rgb(255, 180, 0)">POST</span> /users/instruments**

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
  "status":200,

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
  "status":200,

}
```

Cette route permet d'ajouter un role à l'utilisateur

### Requête HTTP

**<span style="rgb(255, 180, 0)">POST</span> /users/{uid}/roles**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur

### Paramètres de requête

Paramètre | Par défaut | Description
--------- | ------- | -----------
rid |  | l'id de l'achievements

<aside class="notice">
   Seuls les membres du CA peuvent ajouter un role, dans les autres cas, la route renverra un JSON d'erreur avec comme status 403
</aside>


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
  "users:"
    [
      {
        "id": 1,

      },
      {
        "id": 2,
      }
    ]
}
```

Cette route permet de récuperer une liste d'utilisateur

### Requête HTTP

**<span style="color:rgb(12, 187, 82)">GET</span> /groups**

### Headers

Paramètre | Par défaut | Description
--------- | ------- | -----------
authToken |  | Token d'identification de l'utilisateur
