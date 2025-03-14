### Examen - Développement Web (PHP & MySQL & JavaScript)

**Durée : 1h30**

**Consignes :**

- Lisez attentivement chaque question avant de commencer.
    - Les questions auxquelles vous devez répondre sont marqué avec 👉.
- Respectez la structure demandée pour chaque fichier.
- Codez proprement et ajoutez des commentaires si nécessaire.

**Règles :**
- Vous pouvez vous servir des sujets de TP.
- Vous pouvez vous servir de vos TP.
- Vous pouvez faire des recherches sur Internet.
- En revanche, **l'utilisation de l'IA est INTERDITE durant l'examen ⛔**

**Modalités de rendu :**
- Créer une archive `zip` avec comme nom `NOM_Prénom_Groupe.zip` contenant l'ensemble des fichiers demandés
- Transmettre cette archive en pièce jointe par email :
    - destinataire : `berenger.germain@shareandmove.fr` ou `renaud.david@shareandmove.fr`
    - objet : `BUT RT Web dynamique : NOM Prénom Groupe`
    - pièce jointe : archive `NOM_Prénom_Groupe.zip`

---

## **Contexte**

Vous allez développer une petite application de gestion d’utilisateurs.
Un visiteur pourra se connecter avec un prénom et sera stocké en session, puis voir une liste d’utilisateurs enregistrés en base de données.

---

## **1. Mise en place de la base de données (3 points)**

Créez une base de données (sur *rt_projet* ou sur votre ordinateur personnel) et une table `users` avec la structure suivante :

```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);
```

👉 **Question :** Écrivez la requête SQL dans un fichier `query.sql` ci-dessus et expliquez brièvement à quoi sert chaque ligne (utilisez le caractère `/* ... */` pour commenter).

---

## **2. Connexion avec les sessions (5 points)**

Créez un fichier `login.php` qui affiche un formulaire demandant un prénom et un bouton de connexion.

**Fichier `login.php`**

```html
<?php
    // Coder en PHP ici les logiques de la page.
?>

<form method="POST" action="login.php">
    <label for="name">Votre prénom :</label>
    <input type="text" id="name" name="name" required>
    <button type="submit" name="login">Se connecter</button>
</form>
```

👉 **À faire en PHP :**

1. Démarrer la session avec `session_start()`.
2. Si le formulaire est soumis, enregistrer le prénom en session.
3. Rediriger vers `index.php` après la connexion.

💡 **Exemple de redirection après connexion :**

```php
header("Location: index.php");
exit();
```

---

## **3. Affichage des utilisateurs enregistrés en base de données (6 points)**

Créez un fichier `index.php` qui affiche :

1. Un message de bienvenue avec le prénom en session.
2. Un formulaire pour ajouter un utilisateur en base de données.
3. La liste des utilisateurs enregistrés.

**Fichier `index.php`**

```html
<?php
    // Coder en PHP ici les logiques de la page.
?>

<!-- Afficher ici le message de bienvenue -->

<h2>Ajouter un utilisateur</h2>
<form method="POST">
    <input type="text" name="name" required>
    <button type="submit" name="add">Ajouter</button>
</form>

<h2>Liste des utilisateurs</h2>
<ul>
    <!-- Afficher ici les utilisateurs stockés en base -->
</ul>
```

👉 **À faire en PHP :**

1. Vérifier que l’utilisateur est connecté (sinon rediriger vers `login.php`).
2. Insérer un nouvel utilisateur en base de données quand le formulaire est soumis.
3. Afficher tous les utilisateurs depuis la base.

💡 **Exemple d’insertion en base :**

```sql
INSERT INTO users (name) VALUES ('Alice');
```

💡 **Exemple de récupération des utilisateurs :**

```sql
SELECT * FROM users;
```

---

## **4. Déconnexion (2 points)**

Ajoutez un bouton de déconnexion qui efface la session et redirige vers `login.php`.

**Complétez le fichier `index.php`**

```html
<form method="POST">
    <button type="submit" name="logout">Se déconnecter</button>
</form>
```

👉 **À faire en PHP**

Si "Se déconnecter" est cliqué :

1. Détruire la session.
2. Rediriger vers `login.php`.

---

## **5. Réinitialisation des utilisateurs (4 points)**

Ajoutez un bouton de réinitialisation qui vide la table `users` en base de données.

**Complétez le fichier `index.php`**

```html
<form method="POST">
    <button type="submit" name="reset">Réinitialiser les utilisateurs</button>
</form>
```

👉 **À faire en PHP**

Si "Réinitialiser" est cliqué :

1. Vider la base d'utilisateur
2. Déconnecter l'utilisateur.

💡 **Exemple de suppression de tous les utilisateurs :**

```php
DELETE FROM users;
```

👉 **À faire en JavaScript**

Ajouter une confirmation avec JavaScript avant la suppression, qui demande à l'utilisateur s'il veut vraiment vider la base de données.

💡 **Exemple de selection du bouton reset :**

```javascript
const button = document.querySelector("button[name='reset']");
```

💡 **Exemple d'annulation d'un événement `submit` :**

```javascript
// ...
event.preventDefault();
// ...
```
