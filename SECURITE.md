# Sécurité et périmètre du partage

Ce dépôt contient une distribution générique, sans base utilisateurs, situations, conversations, jetons, accès Infomaniak ni documents RH privés. Les PDF fournis, leurs extractions, les photos et leurs reformulations spécifiques sont exclus. Les capsules sont des supports pédagogiques génériques à voix synthétique.

La configuration réelle et le dossier `var/` restent hors du Web et hors Git. Le `.gitignore` est une protection complémentaire ; il n’efface pas un secret déjà committé. Vérifier chaque fichier avant publication.

La base SQLite stocke les contenus en clair dans le répertoire privé. Prévoir des sauvegardes privées, une durée de conservation adaptée et une procédure de restauration. L’application ne fournit ni chiffrement applicatif ni purge automatique.

Les comptes utilisent des mots de passe hachés, des liens individuels temporaires, une limitation des essais, des sessions expirantes et des contrôles CSRF. Les données personnelles d’un utilisateur sont filtrées par propriétaire. Les administrateurs peuvent gérer le corpus commun et les comptes, mais n’accèdent pas par l’interface aux situations d’autrui.

L’API IA reçoit les éléments du contexte et les extraits documentaires nécessaires à la demande. L’IA peut produire des erreurs ou suivre imparfaitement ses consignes. Relire les faits, citations et hypothèses. La validation d’un texte ne prouve pas l’accord du collaborateur.

Cette version est destinée aux données fictives ou d’exercice. Son partage ne constitue ni une homologation ni une autorisation institutionnelle pour des données RH réelles. Une exploitation avec de telles données demande son propre cadre de protection et de validation.

Signaler un problème sans publier de mot de passe, de lien d’activation ou de dossier RH dans une issue publique.
