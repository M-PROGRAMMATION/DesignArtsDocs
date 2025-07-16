# 🧾 Formulaire Dynamique – Guide de Configuration

Ce document décrit la structure d'un formulaire dynamique multi-étapes en JSON, permettant de guider l'utilisateur selon ses réponses. Ce système peut être utilisé dans un projet web pour créer un formulaire intelligent, conditionnel et évolutif.

---

## 📌 Structure Générale

Le fichier JSON contient des **étapes numérotées** (`"1"`, `"2"`, etc.), chacune représentant une étape du formulaire.

### ➤ Exemple :

```json
{
  "1": { ... },
  "2": { ... }
}
```

---

## 🥇 Étape 1 : Objectif principal

```json
"1": {
  "question": "Je veux :",
  "sub-title": "Choisissez votre objectif principal",
  "responses": [
    "Faire des travaux",
    "Calculer mes aides et primes",
    "Savoir quels travaux réaliser",
    "Passer au solaire"
  ],
  "required": true,
  "default": "",
  "placeholder": "",
  "type": "dropdown"
}
```

- `question`: Le texte affiché à l'utilisateur.
- `sub-title`: Description secondaire (facultative).
- `responses`: Liste des choix proposés.
- `type`: Type de champ (`dropdown`, `text`, `radio`, etc.).
- `required`: Si la réponse est obligatoire.

---

## 🥈 Étape 2 : Dépend du choix fait à l'étape 1

```json
"2": {
  "type": {
    "faire_des_travaux": {
      "question": "Quel type de logement ?",
      "responses": ["Maison", "Appartement", "Bungalow", "Autre"],
      ...
    },
    "calculer_mes_aides_et_primes": { ... },
    "savoir_quels_travaux_realiser": { ... },
    "passer_au_solaire": { ... }
  }
}
```

- La clé `type` contient des objets pour chaque **option choisie à l'étape 1**.
- Chaque clé (`faire_des_travaux`, etc.) **doit correspondre** à une version normalisée (minuscule + underscore) d'une réponse.

---

## ➕ Ajouter une nouvelle option à l’étape 1

1. Ajouter le texte dans `responses` de `"1"` :

   ```json
   "Rénover une résidence secondaire"
   ```

2. Ajouter une configuration correspondante dans `"2".type` :
   ```json
   "renover_une_residence_secondaire": {
     "question": "Quel est l’état actuel du logement ?",
     "sub-title": "Précisez si le logement est habitable",
     "responses": ["Habitable", "À rénover complètement", "En ruine"],
     "required": true,
     "default": "",
     "placeholder": "",
     "type": "dropdown"
   }
   ```

---

## ✏️ Modifier un champ existant

- Pour modifier une question ou les réponses, il suffit de mettre à jour le champ concerné dans l’objet JSON.
- Exemple : changer les réponses pour `"passer_au_solaire"` :
  ```json
  "responses": ["Oui, je suis propriétaire", "Non, je suis locataire"]
  ```

---

## 🧪 Validation des réponses

Chaque champ peut contenir :

- `required: true` → bloque l'étape suivante tant qu’aucune réponse n’est donnée.
- `default`: valeur par défaut (souvent vide `""`).
- `placeholder`: texte d’aide dans les champs de saisie libre (`text`, `number`, etc.).

---

## 🧰 Types de champs supportés

- `"dropdown"` : liste déroulante
- `"radio"` : boutons radio
- `"text"` : champ de texte libre
- `"number"` : champ numérique

> Vous pouvez ajouter d'autres types selon vos besoins dans le moteur de rendu du formulaire.

---

## 💡 Bonnes pratiques

- Toujours garder les noms de clés **normalisés** (ex : `"Passer au solaire"` devient `"passer_au_solaire"`).
- Assurez-vous qu’à chaque nouvelle réponse de l’étape 1 correspond une entrée dans `"2".type`.
- Évitez les doublons ou espaces spéciaux dans les clés.

---

## 📈 Évolution possible

- Ajouter une **étape 3** conditionnelle selon les réponses précédentes.
- Intégrer des validations spécifiques (`min`, `max`, regex...).
- Générer dynamiquement le formulaire dans un framework frontend (Angular, React, Vue...).

---
