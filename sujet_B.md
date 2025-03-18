### Examen - Développement Web (PHP & MySQL & JavaScript)

**Durée : 1h30**

**Consignes :**

- Lisez attentivement chaque question avant de commencer.
    - Les questions auxquelles vous devez répondre sont marquées avec 👉.
- Respectez la structure demandée pour chaque fichier.
- Codez proprement et ajoutez des commentaires si nécessaire.

**Règles :**
- Vous pouvez vous servir des sujets de TP.
- Vous pouvez vous servir de vos TP.
- Vous pouvez faire des recherches sur Internet.
- En revanche, **l'utilisation de l'IA est INTERDITE durant l'examen ⛔**

**Modalités de rendu :**
- Créer une archive `zip` avec comme nom `NOM_Prénom_Groupe.zip` contenant l'ensemble des fichiers demandés.
- Transmettre cette archive en pièce jointe par email :
    - destinataire : `berenger.germain@shareandmove.fr` ou `renaud.david@shareandmove.fr`
    - objet : `BUT RT Web dynamique : NOM Prénom Groupe`
    - pièce jointe : archive `NOM_Prénom_Groupe.zip`

---

## **Contexte**

Vous allez développer une **petite application de gestion d'invités à un événement**.
Un utilisateur pourra se connecter en saisissant son prénom (stocké en session) et voir la liste des invités enregistrés dans une base de données.

---

## **1. Mise en place de la base de données (3 points)**

Créez une base de données (sur *rt_projet* ou sur votre ordinateur personnel) et une table `guests` avec la structure suivante :

```sql
CREATE TABLE guests (
    id INT AUTO_INCREMENT PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL
);
```

👉 **Question :** Écrivez la requête SQL dans un fichier `database.sql` et expliquez brièvement l'utilité de chaque ligne en ajoutant des commentaires `/* ... */`.

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
3. Rediriger vers `dashboard.php` après la connexion.

💡 **Exemple de redirection après connexion :**

```php
header("Location: dashboard.php");
exit();
```

---

## **3. Affichage des invités enregistrés en base de données (6 points)**

Créez un fichier `dashboard.php` qui affiche :

1. Un message de bienvenue avec le prénom en session.
2. Un formulaire pour ajouter un nouvel invité en base de données.
3. La liste des invités enregistrés.

**Fichier `dashboard.php`**

```html
<?php
    // Coder en PHP ici les logiques de la page.
?>

<!-- Afficher ici le message de bienvenue -->

<h2>Ajouter un invité</h2>
<form method="POST">
    <input type="text" name="full_name" required>
    <button type="submit" name="add">Ajouter</button>
</form>

<h2>Liste des invités</h2>
<ul>
    <!-- Afficher ici les invités stockés en base -->
</ul>
```

👉 **À faire en PHP :**

1. Vérifier que l'utilisateur est connecté (sinon rediriger vers `login.php`).
2. Insérer un nouvel invité en base de données quand le formulaire est soumis.
3. Afficher tous les invités depuis la base.

💡 **Exemple d'insertion en base :**

```sql
INSERT INTO guests (full_name) VALUES ('Alice Dupont');
```

💡 **Exemple de récupération des invités :**

```sql
SELECT * FROM guests;
```

---

## **4. Déconnexion (2 points)**

Ajoutez un bouton de déconnexion qui efface la session et redirige vers `login.php`.

**Complétez le fichier `dashboard.php`**

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

## **5. Suppression des invités (4 points)**

Ajoutez un bouton de suppression qui vide la table `guests` en base de données.

**Complétez le fichier `dashboard.php`**

```html
<form method="POST">
    <button type="submit" name="reset">Supprimer tous les invités</button>
</form>
```

👉 **À faire en PHP**

Si "Supprimer tous les invités" est cliqué :

1. Vider la base des invités.
2. Déconnecter l'utilisateur.

💡 **Exemple de suppression de tous les invités :**

```php
DELETE FROM guests;
```

👉 **À faire en JavaScript**

Ajouter une confirmation avec JavaScript avant la suppression.

💡 **Exemple de sélection du bouton reset**

```javascript
const button = document.querySelector("button[name='reset']");
```

💡 **Exemple d'annulation d'un événement `submit` :**

```javascript
event.preventDefault();
```
