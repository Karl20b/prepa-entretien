# Prépa Entretien

Application pédagogique autonome pour préparer un entretien professionnel, structurer les faits et décider des questions à poser. **Version 13 — 25 novembre 2026.** PHP et SQLite, sans dépendance à un portail.

## Nouveautés

- Dictée du contexte, des faits observés, de l’objectif du cadre et des enjeux, avec pause et relecture de la transcription.
- Quatre commandes IA : **Résumer mes propos**, **M’aider à préciser**, **Explorer avec EOGI**, **Proposer une trame**.
- Résumé et propositions modifiables dans l’aperçu avant validation. Le cadre choisit la destination ; remplacer un texte existant nécessite une confirmation distincte, puis un enregistrement.
- Choix d’un rôle et de son cahier des charges. Cette distribution fournit deux exemples fictifs, sans les CDC institutionnels privés.
- Analyse systémique EOGI, feed-back de valorisation ou d’amélioration, constellation d’équipe, comptes et invitations modifiables.
- Guide P1 à P7 séparé des méthodes métier dans le RAG et **quatre nouvelles capsules avec la voix synthétique Vivienne**, sous-titres et transcriptions.

## Télécharger

[Télécharger l’application complète](Prepa_Entretien_Application.zip?raw=true), puis décompresser pour obtenir `application/` et les guides. **Aucun compte GitHub n’est nécessaire.** Avec **Code → Download ZIP**, décompresser également l’archive applicative incluse.

[Installation et mise à jour](INSTALLATION.md) · [Guide d’utilisation](UTILISATION.md) · [Sécurité et périmètre](SECURITE.md) · [Historique](CHANGELOG.md)

Les vidéos se trouvent dans `application/media/guide-01.mp4` à `guide-04.mp4`, et dans le Guide après installation. Le code source est intégralement inclus dans l’archive, sous `application/src`, `templates`, `public`, `sql` et `tests`.

## Configuration et limites

PHP 8.4+ avec SQLite, cURL, mbstring, iconv et fileinfo ; HTTPS ; clé personnelle du service IA pour activer les fonctions distantes. La transcription utilise l’adaptateur livré et son point d’accès autorisé, décrit dans le guide d’installation. Chaque installateur assume ses coûts et valide l’usage de ses données.

La saisie manuelle et la recherche documentaire restent possibles sans appel IA. Le mode `demo` ne prend pas en charge les quatre commandes structurées. Les trames d’un modèle réel peuvent être courtes ou refusées si tronquées : la rédaction manuelle reste disponible. Les références affichées ne garantissent pas la justesse d’une proposition.

Le corpus public ne contient que des repères génériques et des CDC fictifs. Aucun compte, mot de passe, jeton, situation, conversation, fichier audio dicté, PDF RH, photographie privée ou sauvegarde de l’installation privée n’est distribué. Ce dépôt ne déploie pas automatiquement l’application.

## Vérifier le code

Depuis `application/`, lancer `php tests/lint.php`, puis chaque script PHP du dossier `tests/`. Les tests utilisent SQLite en mémoire et des données fictives. Les scénarios d’interface se lancent avec `node tests/dictee-ui.cjs` et `node tests/preparation-ui.cjs` ; aucun paquet Node supplémentaire n’est requis. Ils vérifient les reprises de texte, confirmations, refus périmés et scénarios simulés, sans appeler un service IA réel.
