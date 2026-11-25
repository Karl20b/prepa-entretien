# Sécurité et périmètre du partage

Ce dépôt contient une distribution générique, sans base utilisateurs, situations, conversations, jetons, accès Infomaniak ni documents RH privés. Les PDF fournis, leurs extractions, les photos et leurs reformulations spécifiques sont exclus. Les capsules sont des supports pédagogiques génériques à voix synthétique.

La configuration réelle et le dossier `var/` restent hors du Web et hors Git. Le `.gitignore` est une protection complémentaire ; il n’efface pas un secret déjà committé. Vérifier chaque fichier avant publication.

La version 14 fournit une activation explicite du chiffrement applicatif au repos et de la 2FA. Avant cette activation, les contenus restent en clair dans le répertoire privé. Prévoir des sauvegardes privées, une durée de conservation adaptée et une procédure de restauration ; aucune purge automatique n’est fournie.

Les comptes utilisent des mots de passe hachés, des liens individuels temporaires, une limitation des essais, des sessions expirantes et des contrôles CSRF. Les données personnelles d’un utilisateur sont filtrées par propriétaire. Les administrateurs peuvent gérer le corpus commun et les comptes, mais n’accèdent pas par l’interface aux situations d’autrui.

L’API IA reçoit les éléments du contexte et les extraits documentaires nécessaires à la demande. L’IA peut produire des erreurs ou suivre imparfaitement ses consignes. Relire les faits, citations et hypothèses. La validation d’un texte ne prouve pas l’accord du collaborateur.

Cette version est destinée aux données fictives ou d’exercice. Son partage ne constitue ni une homologation ni une autorisation institutionnelle pour des données RH réelles. Une exploitation avec de telles données demande son propre cadre de protection et de validation.

Signaler un problème sans publier de mot de passe, de lien d’activation ou de dossier RH dans une issue publique.


## Dictée et préparation assistée — version 13

La transcription transmet l’audio au service configuré sur action explicite. Les appels de l’assistant transmettent le récit nécessaire et, pour EOGI/trame, les extraits retenus du corpus. Les règles de conservation du fournisseur doivent être vérifiées par l’exploitant. La dictée ne doit contenir que des données fictives ou d’exercice dans ce prototype.

La validation du résumé ne suffit pas à enregistrer la situation : utiliser Enregistrer. Les champs existants nécessitent une confirmation distincte avant remplacement. Les réponses périmées, tronquées ou structurellement invalides sont refusées. Ces contrôles ne garantissent ni l’exactitude des faits ni la pertinence d’une question. Aucun contenu dicté ou échange n’est automatiquement ajouté au RAG.

Le corpus d’aide `aide_utilisation` est exclu des recherches métier par défaut. Les attentes d’un CDC ne constituent pas une appréciation de performance. Les deux CDC publics sont entièrement fictifs ; les CDC et documents RH privés restent exclus de la distribution.


## Connexion sécurisée — version 14

Après activation serveur : TOTP RFC 6238, SHA-1, six chiffres et période de 30 secondes, tolérance d’un pas avant/après. Le secret de chaque compte est chiffré avec une portée liée à l’identifiant ; le QR est généré localement, sans transmission externe. Première association : 15 minutes ; confirmation d’une connexion suivante : cinq minutes. Un code accepté ne peut pas être rejoué. Cinq échecs entraînent un blocage de dix minutes.

Huit codes de secours aléatoires de 128 bits sont fournis au titulaire ; seules leurs empreintes SHA-256 sont conservées en base, avec consommation atomique. Un lien de réinitialisation ne supprime pas le second facteur. Aucun accès métier ou média authentifié n’est donné pendant la préauthentification.

La politique de cette application demande un renouvellement tous les 90 jours, 14 caractères minimum et un mot de passe différent des cinq derniers. Un renouvellement révoque les autres sessions et les liens de réinitialisation existants. Ce choix de 90 jours ne constitue pas une exigence universelle de sécurité.

## Chiffrement au repos — version 14

Le coffre utilise libsodium XChaCha20-Poly1305, un nonce aléatoire et des clés dérivées par domaine à partir d’une clé maîtresse de 32 octets. La portée de stockage est authentifiée ; un contenu altéré ou une mauvaise clé sont refusés.

| Périmètre | Protection après activation |
| --- | --- |
| Situations, messages, grilles, analyses et cartes | Contenus métier chiffrés |
| RAG | Titres, provenance, documents et fragments chiffrés ; recherche déchiffrée en mémoire |
| Sources physiques | Originaux, corpus d’import et fichiers couverts par la migration chiffrés |
| Sessions | Stockage chiffré avec verrouillage de session |
| Métadonnées | Identifiants, rôles, catégories, relations et horodatages restent lisibles |
| Mots de passe et secours | Empreintes ; pas de déchiffrement |
| Configuration technique et jeton API | Fichier privé à accès restreint, non chiffré par ce coffre |
| Capsules génériques | Hors de ce chiffrement |

La clé est hors Web et hors application (0600), dans un répertoire privé (0700), avec une sauvegarde indépendante conservée par l’exploitant. Elle est différente du secret TOTP et des codes de secours. Ne distribuer aucune de ces clés. La perte de la clé empêche la récupération des contenus.

Il s’agit d’un chiffrement applicatif des contenus, pas de SQLCipher ni de chiffrement de bout en bout. Le serveur peut déchiffrer et transmettre les éléments nécessaires aux demandes explicites vers le service configuré. La conservation chez ce fournisseur reste à vérifier séparément. Les anciennes installations, exports, copies de recette et sauvegardes de l’hébergeur hors périmètre doivent faire l’objet d’un inventaire et d’un traitement distincts.

La migration doit être répétée hors production, sous maintenance, avec sauvegarde cohérente et restauration testée. Voir [INSTALLATION.md](INSTALLATION.md). Le composant QR adapté de Project Nayuki conserve sa licence MIT dans `application/src/Security/LICENCE-QR.txt`.
