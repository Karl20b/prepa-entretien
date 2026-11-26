# Guide d’utilisation — version 15.1

## Se connecter et associer Authenticator

Ces étapes s’appliquent après activation de la sécurité par l’exploitant, décrite dans [INSTALLATION.md](INSTALLATION.md).

1. Saisir son identifiant et son mot de passe. À la première connexion sécurisée, ouvrir Authenticator sur son téléphone : **+ → Ajouter un compte → Scanner un QR code**.
2. Scanner le QR affiché sur l’ordinateur. Il est généré dans l’application sans service externe. Si le scan est impossible, utiliser la saisie manuelle proposée.
3. Saisir dans Prépa Entretien le code à six chiffres du téléphone puis **Vérifier le code**. Ce code change toutes les 30 secondes ; la clé d’association ne change pas à ce rythme. La première association dispose de **15 minutes** après le mot de passe.
4. Conserver les **huit codes de secours** dans son gestionnaire de mots de passe, puis confirmer leur conservation. Ils ne seront plus affichés ; chaque code ne fonctionne qu’une fois.
5. Renouveler son mot de passe si demandé, puis continuer jusqu’à **Mes situations**. Après validation du facteur, la suite du parcours dispose de cinq minutes.

Aux connexions suivantes : mot de passe puis code Authenticator, avec cinq minutes pour valider ce second facteur. Aucun nouveau scan n’est nécessaire. Ne jamais partager le QR, la clé ou les codes. Un code déjà accepté est refusé ; cinq échecs bloquent les essais pendant dix minutes.

Si le code échoue, attendre le suivant et vérifier le réglage automatique de l’heure du téléphone. Si la page a expiré, se reconnecter. Sans téléphone, utiliser un code de secours inutilisé dans le même champ. Sans téléphone ni secours, contacter l’exploitant ; une réinitialisation du mot de passe ne supprime pas la 2FA.

## Renouveler son mot de passe tous les 90 jours

L’application impose le renouvellement après 90 jours, ainsi qu’aux anciens comptes dont la date de changement est inconnue. Saisir le mot de passe actuel, un nouveau mot de passe d’au moins **14 caractères**, différent des cinq derniers, puis sa confirmation. Le renouvellement invalide les autres sessions et anciens liens de réinitialisation. Authenticator reste associé.

## Comprendre le chiffrement

Après activation serveur, les contenus métier, messages, analyses, documents et fragments RAG, originaux et sessions sont chiffrés au repos. Certaines métadonnées restent lisibles : identifiants, rôles, catégories, relations et dates techniques. Les mots de passe et codes de secours sont hachés.

La clé de stockage est conservée par l’exploitant hors Web et hors application, avec une sauvegarde indépendante dans son coffre. Elle est distincte du QR Authenticator et des codes de secours ; les utilisateurs ne la saisissent pas. Sa perte compromet la récupération des contenus.

Le serveur autorisé peut déchiffrer les contenus. Les éléments nécessaires à une demande explicite sont transmis au service IA ou de transcription configuré. Il ne s’agit ni de chiffrement de bout en bout ni de chiffrement intégral de SQLite. Les anciennes copies et sauvegardes externes doivent être inventoriées séparément. Voir [SECURITE.md](SECURITE.md).

## Modifier et exporter sa préparation

La préparation actuelle est affichée une seule fois. Les échanges et générations antérieurs restent repliés dans Historique. Choisir **Modifier et exporter la préparation** pour corriger une version de travail indépendante. Les réponses d’origine sont conservées. Une nouvelle génération ne remplace pas les corrections ; un changement de contexte est signalé.

Dans EOGI ou Feed-back, choisir **Modifier la trame et exporter Word / PDF**. Le texte est modifiable même avant génération, à partir de la grille. La version de travail et la grille sont distinctes : modifier le document ne remplit pas automatiquement les champs de la grille.

Les boutons **Enregistrer et télécharger Word / PDF** enregistrent d’abord le texte affiché. Le document contient cette version et ses références, sans l’historique complet des échanges. Aucun nouvel appel IA n’est nécessaire. Les conflits entre onglets sont refusés ; copiez vos corrections avant de recharger. Les exports sont lisibles hors application : conservez-les dans un espace privé.

## Préparer la situation

Créer une situation avec un titre, le type d’entretien et, si applicable, le rôle du collaborateur. Les deux CDC de la distribution publique sont fictifs : vérifier ou remplacer les références avant usage.

Renseigner le contexte, les faits observés, ce que vous souhaitez obtenir et les enjeux perçus. Distinguer ce qui est observé, rapporté, supposé ou encore inconnu.

## Dicter puis relire

Choisir le champ, autoriser le microphone, démarrer la prise, mettre en pause ou reprendre, puis terminer. Cliquer explicitement sur **Transcrire**. Une prise dure cinq minutes au maximum ; le quota est distinct de celui de l’assistant. Relire et corriger le texte avant de l’utiliser. Il s’agit de dicter votre préparation, pas d’enregistrer l’entretien avec le collaborateur.

L’envoi au service de transcription n’a lieu qu’à votre demande. Une transcription ne devient ni une preuve ni une entrée automatique du corpus RAG.

## Utiliser les quatre commandes

1. **Résumer mes propos** : reformulation du récit fourni, sans recherche dans le corpus documentaire. Le résumé peut reprendre le libellé du rôle choisi, sans ses exigences.
2. **M’aider à préciser** : jusqu’à trois questions pour clarifier le contexte. Vos réponses restent vos propres précisions ; les propositions de l’assistant ne deviennent pas des faits.
3. **Explorer avec EOGI** : hypothèses à vérifier aux niveaux environnement, organisation, groupe et individu, à partir des sources actives et du CDC choisi.
4. **Proposer une trame** : questions et déroulement à relire puis adapter. Une réponse tronquée peut être refusée ; vous pouvez toujours rédiger manuellement.

## Modifier le résumé avant de valider

Modifier directement le texte du résumé dans l’aperçu. Choisir le champ de destination. Vérifier le texte corrigé, puis valider sa reprise. Si le champ contient déjà du texte, confirmer explicitement son remplacement. Cliquer ensuite sur **Enregistrer** pour conserver la situation.

Les propositions par champ sont également modifiables. Choisir celles à reprendre. Une modification du contexte ou du rôle peut rendre une proposition antérieure périmée : refaire la demande dans ce cas. Les ajouts EOGI sélectionnés et la trame retenue ne sont conservés qu’après validation et enregistrement.

## EOGI, feed-back et références

Dans les ateliers EOGI et feed-back, solliciter l’assistance, corriger l’aperçu et sélectionner les champs vides à compléter. Vérifier les références citées et les hypothèses. Les observations, ressentis et liens de causalité supposés doivent rester distincts. Le cadre conserve la décision et conduit l’entretien.

Les administrateurs peuvent alimenter le corpus commun avec des fichiers TXT/Markdown autorisés, de 2 Mo maximum. Les fiches d’aide sont classées `aide_utilisation`, séparément des CDC et des méthodes métier. La recherche d’aide seule n’appelle pas le modèle IA.

## Comptes et invitations

Identifiant : 3 à 40 caractères, premier caractère lettre minuscule ou chiffre, puis lettres minuscules, chiffres, point, tiret ou soulignement ; sans espace ni accent. L’administrateur crée le compte, choisit son rôle et prépare un message d’invitation modifiable. L’envoi est effectué par l’administrateur dans sa messagerie. Lien d’activation valable 48 heures ; mot de passe personnel de 14 caractères minimum. Le rôle administrateur permet la gestion du corpus et des comptes, sans accès aux situations d’autres utilisateurs. La base documentaire et son URL sont réservées aux administrateurs. **Tester le RAG reste disponible pour les utilisateurs et les administrateurs**, avec les extraits de recherche nécessaires.

## Guide et capsules

Le Guide intégré présente le parcours P1 à P7 et les exemples d’utilisation. Les capsules avec voix synthétique Vivienne couvrent :

| Fichier | Sujet | Durée |
| --- | --- | --- |
| `media/guide-01.mp4` | Dicter et relire sa préparation | 1 min 32 |
| `media/guide-02.mp4` | Choisir parmi les quatre commandes IA | 1 min 38 |
| `media/guide-03.mp4` | Modifier le résumé avant validation | 1 min 40 |
| `media/guide-04.mp4` | Utiliser les références dans EOGI et le feed-back | 1 min 35 |
| `media/guide-05.mp4` | Authenticator, secours et renouvellement du mot de passe | 1 min 54 |
| `media/guide-06.mp4` | Modifier la préparation et le feed-back, puis exporter Word/PDF | 1 min 35 |

Les sous-titres `.vtt`, transcriptions `.txt` et affiches `.webp` sont inclus. Les vidéos sont consultables après connexion dans l’application ou directement dans le dossier extrait.

La cinquième capsule explique le nouveau parcours de sécurité ; les quatre premières conservent leur sujet.

La capsule 06 montre les deux chemins d’édition, l’enregistrement de la version de travail, les exports DOCX et PDF et les précautions de conservation. [Vidéo seule](Guide_06_Modifier_et_exporter.mp4).
