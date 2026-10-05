# Automatisation et analyse de données sportives

Projet Python réalisé dans le cadre du cours Coursera **Automation and Scripting with Python**. Le notebook automatise le traitement de statistiques de baseball, produit des visualisations, prépare une alerte par e-mail et gère les versions successives du fichier de résultats.

## Objectifs

- Charger et nettoyer un jeu de données CSV avec pandas.
- Analyser les statistiques de baseball : `BB`, `SO`, `AB`, `HR`, singles, doubles et triples.
- Générer des graphiques avec Matplotlib.
- Calculer des moyennes et le ratio `SO/BB`.
- Préparer l’envoi d’une notification avec SendGrid et gérer les erreurs.
- Planifier une tâche quotidienne à 9 h avec `schedule`.
- Sauvegarder les résultats en conservant une copie précédente.
- Utiliser Git pour suivre les modifications du projet.

## Structure du projet

| Fichier                   | Description                                             |
| ------------------------- | ------------------------------------------------------- |
| `submission.ipynb`        | Notebook contenant toutes les étapes du projet.         |
| `sports_data_missing.csv` | Jeu de données source contenant des valeurs manquantes. |
| `statistics_CURRENT.csv`  | Résultats nettoyés et actualisés.                       |
| `statistics_OLD.csv`      | Sauvegarde de la version précédente des résultats.      |

## Prérequis

- Python 3.8 ou supérieur
- Jupyter Notebook ou JupyterLab
- Une connexion Internet uniquement pour l’intégration SendGrid

Installer les bibliothèques nécessaires :

```bash
pip install pandas matplotlib sendgrid schedule jupyter
```

## Exécution

1. Ouvrir le dossier du projet dans VS Code ou un terminal.
2. Lancer Jupyter :

   ```bash
   jupyter notebook
   ```

3. Ouvrir `submission.ipynb`.
4. Exécuter les cellules dans l’ordre.

Le notebook commence par supprimer les lignes contenant des valeurs manquantes, puis exclut les joueurs dont le nombre de buts sur balles (`BB`) ou de retraits sur prises (`SO`) est égal à zéro. Il calcule ensuite la colonne `SO/BB`, crée les graphiques et sauvegarde le DataFrame nettoyé.

## Visualisations et résultats

Le notebook produit notamment :

- un nuage de points `BB` contre `SO` ;
- un nuage de points `HR` contre `AB` ;
- un diagramme en boîte pour les singles, doubles, triples et home runs ;
- les moyennes des différents types de frappes ;
- les valeurs minimale et maximale du ratio `SO/BB`.

Lors de la sauvegarde, `statistics_CURRENT.csv` est renommé en `statistics_OLD.csv` avant l’écriture du nouveau fichier. Ainsi, les résultats précédents ne sont pas écrasés sans sauvegarde.

## SendGrid et sécurité

Le notebook contient une démonstration de configuration SendGrid avec une clé d’exercice non fonctionnelle. Pour une utilisation réelle :

- ne jamais publier une clé API dans le notebook ou dans Git ;
- stocker la clé dans une variable d’environnement ;
- utiliser une adresse d’expéditeur autorisée par SendGrid ;
- remplacer les adresses d’exemple par des adresses valides.

Exemple sous PowerShell :

```powershell
$env:SENDGRID_API_KEY = "votre_cle_api"
```

## Planification

La tâche d’envoi est configurée pour s’exécuter chaque jour à `09:00` avec la bibliothèque `schedule`. Pour une automatisation permanente, le programme doit rester actif ou être lancé par un planificateur système comme le Planificateur de tâches Windows.

## Git

Initialiser le dépôt et enregistrer les modifications :

```bash
git init
git add .
git commit -m "Initialisation du projet d automatisation"
```

Effectuer ensuite des commits réguliers avec des messages décrivant clairement les changements.

## Limites connues

- L’API SendGrid utilise des valeurs d’exemple et ne permet pas nécessairement d’envoyer un e-mail.
- Le nettoyage supprime les lignes incomplètes au lieu d’imputer les valeurs manquantes.
- Le notebook sert de démonstration ; pour une exécution quotidienne fiable, le code devrait être extrait dans un script Python avec une configuration sécurisée.
