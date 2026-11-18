# Installation sur son propre hébergement

## 1. Préparer l’hébergement

Prévoir PHP 8.4+ avec `pdo_sqlite`, `curl`, `mbstring` et `iconv`, HTTPS et un accès en ligne de commande. Le stockage est SQLite : aucune base MariaDB n’est nécessaire. Les coûts d’hébergement et d’API restent à la charge de chaque installateur.

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

## 3. Initialiser SQLite et le corpus générique

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
