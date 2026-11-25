# Installation sur son propre hébergement

## 1. Préparer l’hébergement

Prévoir PHP 8.4+ avec `pdo_sqlite`, `curl`, `mbstring` et `iconv`, `fileinfo`, HTTPS et un accès en ligne de commande. Le stockage est SQLite : aucune base MariaDB n’est nécessaire. Les coûts d’hébergement et d’API restent à la charge de chaque installateur.

Télécharger `Prepa_Entretien_Application.zip` depuis le dépôt puis le décompresser pour obtenir le dossier `application/`. Si vous avez utilisé **Code → Download ZIP**, décompresser aussi l’archive applicative incluse.

Placer **tout le dossier `application` hors de la racine Web**. Exemple :

```
/home/votre-compte/prepa-prive/application/     ← sources, configuration, données
/home/votre-compte/sites/entretiens.exemple.ch/ ← index et assets uniquement
```

Ne pas déposer l’archive complète dans le dossier accessible sur Internet. N’exposer ni `src`, ni `config`, ni `sql`, ni `tests`, ni `bin`, ni `var`, ni les médias privés.

## 2. Configurer

Copier `application/config/config.example.php` vers `application/config/config.php`.

Renseigner :

- `app.base_url` : l’adresse HTTPS de votre propre site ;
- `app.setup_username` : identifiant initial de 3 à 40 caractères, premier caractère lettre minuscule ou chiffre, puis `a-z`, `0-9`, `.`, `_`, `-` ;
- `app.setup_display_name` : nom affiché du premier administrateur ;
- `app.rate_key` : clé aléatoire, produite par exemple avec `php -r 'echo bin2hex(random_bytes(32)), PHP_EOL;'` ;
- `app.private_dir` et `db.path` : chemins privés accessibles en écriture au processus PHP ;
- `ai.openai_compatible.endpoint`, `api_key` et `model` : votre propre produit et jeton Infomaniak AI Services.

Le modèle de l’exemple est `mistralai/Ministral-3-14B-Instruct-2512`. Vérifier sa disponibilité dans votre catalogue Infomaniak au moment de l’installation. Le jeton reste côté serveur. Le client HTTP restreint les requêtes à HTTPS sur `api.infomaniak.com` ; un autre fournisseur nécessite une adaptation explicite de cette restriction.

Le mode `ai.provider = 'demo'` sert uniquement à découvrir l’interface avec des réponses fictives. Il ne constitue pas un test de connexion IA et peut ne pas fournir le JSON attendu pour le remplissage guidé des champs.

Restreindre l’accès à la configuration et au répertoire des données au compte d’hébergement. Ne jamais les committer sur GitHub.

## 3. Initialiser SQLite et les corpus génériques, d’aide et de référence

Depuis le dossier `application` :

```sh
php bin/initialiser.php
php bin/preparer-activation.php
```

Le deuxième script affiche un lien confidentiel valable une heure. Il refuse de fonctionner si un compte existe déjà. Il ne crée aucun mot de passe partagé. Si le lien expire avant la création du premier compte, relancer ce script.

## 4. Créer l’entrée publique

Dans la racine Web de votre site, créer uniquement ce fichier `index.php`, en adaptant le chemin absolu :

```php
<?php
require '/home/votre-compte/prepa-prive/application/public/index.php';
```

Copier `application/public/assets/` dans le dossier public `assets/`. Le contrôleur privé sert lui-même les capsules après authentification. Activer la redirection HTTP → HTTPS et désactiver l’indexation des dossiers dans les paramètres de l’hébergeur.

Sur un hébergement Apache autorisant `.htaccess`, on peut ajouter :

```apache
Options -Indexes
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteCond %{HTTPS} !=on
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [R=302,L]
</IfModule>
```

Ne pas appliquer cette règle sans adaptation derrière un proxy HTTPS qui ne transmet pas `%{HTTPS}`. Utiliser de préférence la fonction HTTPS de l’hébergeur.

## 5. Activer son administrateur

Ouvrir personnellement le lien obtenu à l’étape 3. Choisir et confirmer un mot de passe d’au moins 14 caractères. Confirmer l’usage avec des données fictives ou d’exercice. L’identifiant correspond à `app.setup_username`, par défaut `administrateur`.

Créer ensuite les comptes depuis l’onglet Comptes. L’invitation de chaque compte est valable 48 heures. Le message d’accompagnement est modifiable ; l’administrateur le relit et l’envoie lui-même depuis sa messagerie.

## 6. Vérifier avant utilisation

- La page de connexion doit fonctionner en HTTPS.
- Les chemins publics `/config/config.php`, `/var/`, `/src/` et `/sql/` doivent être refusés ou inexistants.
- Tester avec deux comptes fictifs : les situations, cartes et grilles restent propres à leur auteur.
- Un administrateur peut ajouter des TXT/Markdown de 2 Mo maximum à la base commune. L’import arbitraire de PDF n’est pas pris en charge ; les convertir et vérifier leur texte avant import.
- Tester un appel IA fictif, les références et l’aperçu modifiable avant d’introduire un nouveau corpus.
- Vérifier la sauvegarde et la restauration de SQLite et de la configuration dans un espace privé.

Le schéma SQLite est initialisé et ses migrations sont appliquées par les outils fournis. `sql/schema.sql` est un vestige historique MariaDB, pas le schéma de cette distribution.


## 7. Dictée et assistant structuré

Les quatre commandes de préparation nécessitent `ai.provider = 'openai_compatible'` et un modèle acceptant la sortie `json_schema` stricte. La configuration d’exemple reste un point de départ : vérifier le modèle disponible dans son compte au moment de l’installation. Le mode `demo` ne réalise pas ces opérations structurées.

L’adaptateur STT livré utilise Infomaniak AI Services : il extrait l’identifiant numérique du produit depuis l’endpoint de conversation `https://api.infomaniak.com/2/ai/{PRODUCT_ID}/openai/v1/chat/completions`, utilise le même jeton côté serveur, puis `/1/ai/{PRODUCT_ID}/openai/audio/transcriptions` et le suivi `/results/{batch_id}`. Aucun secret n’est transmis au navigateur. Un autre service STT demande une adaptation explicite de `src/Stt/Infomaniak.php` et de ses tests.

Autoriser le microphone dans le navigateur sur le domaine HTTPS. Prévoir les limites PHP `upload_max_filesize` et `post_max_size` compatibles avec le maximum de 8 Mo accepté par le contrôleur, ainsi qu’un délai serveur suffisant. Tester avec une courte dictée fictive. Quotas applicatifs : 12 transcriptions et 30 demandes de préparation par heure et par compte ; ils ne remplacent pas les limites et la facturation du fournisseur.

## 8. Mettre à jour une installation existante

Effectuer d’abord une sauvegarde privée cohérente de SQLite, de `config/config.php`, de `var/`, des sources et des corpus personnalisés. Valider dans une copie isolée avant bascule. Ne jamais relancer l’activation si des comptes existent.

Remplacer le code `src`, `templates`, `public`, `sql`, les outils CLI et les médias par la version 13, en préservant **la configuration réelle, les données et les corpus personnalisés**. Copier aussi les nouveaux assets vers la racine publique. Ajouter `help_docs` à partir du paquet ; ne pas remplacer un catalogue CDC personnalisé par les exemples fictifs.

Depuis le dossier privé `application/` :

```sh
php bin/migrer.php
php bin/importer-aide.php
```

Les migrations SQLite sont additives et idempotentes. `importer-aide.php` actualise uniquement les documents portant les titres de la fiche d’aide fournie. Ne pas lancer `initialiser.php` pour une mise à jour : il importe également les exemples génériques. Ne pas lancer `importer-references.php` sur une installation possédant son propre corpus sans vérifier auparavant `reference-data/documents.json`.

Pour des références personnalisées autorisées, adapter ensemble `reference-data/roles.json`, `documents.json` et `originals/`. Garder un `scope` stable par CDC, un `key` stable par document, les champs `title`, `text`, `category`, `resource`, `profile`, `page`, `source`. Consulter les deux exemples fictifs. Lancer `php bin/importer-references.php` après sauvegarde et vérification. Une référence désactivée n’est pas réactivée au réimport. Retirer un élément du JSON ne supprime pas son ancienne entrée : la désactiver dans la gestion documentaire si nécessaire.

Contrôler après bascule : connexion, isolation entre deux comptes fictifs, dictée/transcription, quatre commandes, modification du résumé, remplacement explicite, enregistrement, rôle et sources, séparation aide/métier, lecture des quatre nouvelles vidéos. Conserver la possibilité de restaurer ensemble sources et sauvegarde SQLite.
