# Prépa Entretien

Application pédagogique autonome pour préparer des entretiens et réfléchir avant un échange professionnel. Version partageable issue de la version 8, avec édition des suggestions IA avant validation.

- Situations et échanges personnels avec un assistant IA.
- Analyse systémique **EOGI** : environnement, organisation, groupe, individu.
- Préparation d’un **feed-back** de valorisation ou d’amélioration.
- Suggestions IA modifiables dans un aperçu : seuls les champs vides cochés sont complétés après validation.
- Constellations d’équipe, recherche documentaire RAG lexicale et références consultables.
- Comptes utilisateurs et administrateurs ; ajout de documents TXT/Markdown au corpus commun par les administrateurs.
- Courriel d’invitation modifiable à copier ou à ouvrir dans sa messagerie, sans envoi automatique.
- Guide intégré et quatre capsules à voix synthétique Vivienne, sous-titres et transcriptions.

## Télécharger et installer

Télécharger **[Prepa_Entretien_Application.zip](Prepa_Entretien_Application.zip?raw=true)** puis décompresser cette archive. Elle contient le dossier `application/` prêt à configurer. Aucun compte GitHub n’est nécessaire.

**Code → Download ZIP** permet aussi de récupérer les guides et l’archive applicative dans un même téléchargement ; décompresser ensuite `Prepa_Entretien_Application.zip`.

Chaque personne installe sa propre copie avec son hébergement et ses accès. PHP 8.4 ou plus récent, SQLite, HTTPS et une clé IA personnelle sont nécessaires pour les appels au modèle. Il n’y a aucune dépendance à un portail ni à MariaDB.

➡️ **[Guide d’installation](INSTALLATION.md)** · [Utilisation](UTILISATION.md) · [Sécurité et périmètre](SECURITE.md)

La distribution comprend uniquement le code, des repères génériques et les capsules pédagogiques. Les PDF, photographies et fiches RH fournis pour l’installation privée, les comptes, les situations, les conversations, les clés et les sauvegardes en sont exclus. Aucun exemple RH réel n’est livré.

L’IA propose des formulations et des hypothèses : l’utilisateur vérifie les sources et décide. Une grille ou une carte relationnelle ne prouve pas une causalité, ne constitue pas un diagnostic et ne remplace pas un échange avec la personne.

## Vérifier le code

Depuis `application/`, exécuter `php tests/lint.php`, puis les scripts `tests/integration.php`, `tests/accounts.php`, `tests/invitation.php`, `tests/ateliers.php`, `tests/assistance.php` et `tests/fill.php`. Ces tests utilisent des données fictives et des bases en mémoire ; ils ne valident pas la qualité sémantique d’un modèle IA réel.

Ce dépôt ne déploie pas automatiquement l’application. La copie privée existante reste indépendante du dépôt public.
