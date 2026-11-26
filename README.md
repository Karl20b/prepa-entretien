# Prépa Entretien

Application pédagogique autonome pour préparer un entretien professionnel, structurer les faits et décider des questions à poser. **Version 16.1 — 26 novembre 2026.** PHP et SQLite, sans dépendance à un portail.

## Nouveautés

- Installation : contrôle des permissions des fichiers CSS/JavaScript et outil CLI de correction ciblée pour prévenir les plateaux vides et erreurs 403.

- Feed-back : faits de la situation proposés pour relecture et pistes récentes de l’assistant intégrées à la génération de la trame.
- Édition par rubriques, avec titres lisibles sans marques Markdown ; reprise explicite de la proposition actuelle sans écrasement automatique des corrections.
- Constellation : cercles nommés autour des formes sélectionnées, réglables et conservés dans les exports PNG/SVG.

- Sixième capsule Vivienne : modifier la préparation et la trame de feed-back, enregistrer et exporter en Word ou PDF. Sous-titres et transcription inclus.

- Préparation courante affichée une fois, historique replié, version de travail modifiable et sauvegardée indépendamment des réponses IA.
- Exports Word `.docx` et PDF du texte corrigé ; trames de feed-back modifiables.
- Base documentaire réservée aux administrateurs ; Tester le RAG accessible aux deux rôles.
- Cinquième capsule Vivienne : Authenticator, codes de secours et renouvellement du mot de passe (1 min 54).

- Connexion avec QR code Authenticator généré localement, huit codes de secours, renouvellement du mot de passe tous les 90 jours et chiffrement des contenus au repos après activation serveur.

- Dictée du contexte, des faits observés, de l’objectif du cadre et des enjeux, avec pause et relecture de la transcription.
- Quatre commandes IA : **Résumer mes propos**, **M’aider à préciser**, **Explorer avec EOGI**, **Proposer une trame**.
- Résumé et propositions modifiables dans l’aperçu avant validation. Le cadre choisit la destination ; remplacer un texte existant nécessite une confirmation distincte, puis un enregistrement.
- Choix d’un rôle et de son cahier des charges. Cette distribution fournit deux exemples fictifs, sans les CDC institutionnels privés.
- Analyse systémique EOGI, feed-back de valorisation ou d’amélioration, constellation d’équipe, comptes et invitations modifiables.
- Guide P1 à P7 séparé des méthodes métier dans le RAG et **six capsules avec la voix synthétique Vivienne**, sous-titres et transcriptions.

## Télécharger

[Télécharger l’application complète](Prepa_Entretien_Application.zip?raw=true), puis décompresser pour obtenir `application/` et les guides. **Aucun compte GitHub n’est nécessaire.** Avec **Code → Download ZIP**, décompresser également l’archive applicative incluse.

[Installation et mise à jour](INSTALLATION.md) · [Guide d’utilisation](UTILISATION.md) · [Sécurité et périmètre](SECURITE.md) · [Historique](CHANGELOG.md)

Les vidéos se trouvent dans `application/media/guide-01.mp4` à `guide-06.mp4`, et dans le Guide après installation. Le code source est intégralement inclus dans l’archive, sous `application/src`, `templates`, `public`, `sql` et `tests`.

## Configuration et limites

PHP 8.4+ avec SQLite, libsodium, cURL, mbstring, iconv et fileinfo ; HTTPS ; clé personnelle du service IA pour activer les fonctions distantes. La transcription utilise l’adaptateur livré et son point d’accès autorisé, décrit dans le guide d’installation. Chaque installateur assume ses coûts et valide l’usage de ses données.

La saisie manuelle et la recherche documentaire restent possibles sans appel IA. Le mode `demo` ne prend pas en charge les quatre commandes structurées. Les trames d’un modèle réel peuvent être courtes ou refusées si tronquées : la rédaction manuelle reste disponible. Les références affichées ne garantissent pas la justesse d’une proposition.

Le corpus public ne contient que des repères génériques et des CDC fictifs. Aucun compte, mot de passe, jeton, situation, conversation, fichier audio dicté, PDF RH, photographie privée ou sauvegarde de l’installation privée n’est distribué. Ce dépôt ne déploie pas automatiquement l’application.

## Vérifier le code

Depuis `application/`, lancer `php tests/lint.php`, puis chaque script PHP du dossier `tests/`. Les tests utilisent SQLite en mémoire et des données fictives. Les scénarios d’interface se lancent avec `node tests/dictee-ui.cjs` et `node tests/preparation-ui.cjs` ; aucun paquet Node supplémentaire n’est requis. Ils vérifient les reprises de texte, confirmations, refus périmés et scénarios simulés, sans appeler un service IA réel.


## Sécurité version 15

La version 15 ajoute l’authentification TOTP obligatoire après activation serveur, huit codes de secours à usage unique, un renouvellement du mot de passe tous les 90 jours et le chiffrement authentifié des contenus au repos avec libsodium. Les réglages restent désactivés tant que la migration et la conservation de la clé n’ont pas été effectuées.

Le titulaire scanne personnellement le QR code Authenticator (15 minutes pour la première association) puis renouvelle son mot de passe si demandé. Le chiffrement couvre les contenus métier, les documents et fragments RAG, les originaux et les sessions ; certaines métadonnées techniques restent lisibles. La clé de 32 octets reste hors de la racine Web et du dossier applicatif. Elle doit être sauvegardée indépendamment de l’hébergement. Les données nécessaires aux demandes explicites sont déchiffrées par le serveur avant utilisation.

La migration de stockage ne remplace pas une procédure de déploiement avec maintenance, contrôle d’intégrité et sauvegarde cohérente. Le guide `SECURITE.md` décrit les périmètres, limites et tests. Les extensions PHP `sodium` et `pdo_sqlite` sont nécessaires. Les tests `security.php` et `security-migration.php` utilisent uniquement des données fictives.
