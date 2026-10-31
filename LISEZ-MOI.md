# Mon Budget : fabriquer l'APK signé

© 2026 @red76. Remerciements : Brimo, Kass, Safle Bogoti et mes parents.

## Étape 1 : enregistrer la clé de signature (une seule fois)
La clé se trouve dans le fichier séparé `CLE-DE-SIGNATURE-A-GARDER.txt` (ne l'envoyez JAMAIS dans le dépôt).
1. Sur GitHub, ouvrez votre dépôt > **Settings** > **Secrets and variables** > **Actions** > **New repository secret**.
2. Créez le secret `KEYSTORE_BASE64` : collez le long texte indiqué dans le fichier.
3. Créez le secret `KEYSTORE_PASSWORD` : collez le mot de passe indiqué dans le fichier.
4. Gardez le fichier `mon-budget-cle.p12` et le mot de passe dans un endroit sûr. Sans eux, plus aucune mise à jour ne pourra s'installer par-dessus l'application.

## Étape 2 : envoyer le projet
1. Créez un dépôt GitHub (privé de préférence).
2. Envoyez-y tout le contenu de ce dossier (**Add file > Upload files**), dossier caché `.github` compris.

## Étape 3 : construire l'APK
1. Onglet **Actions** > « Construire l'APK » > **Run workflow**.
2. Quand la coche verte apparaît, ouvrez l'exécution et téléchargez **mon-budget-apk** (section Artifacts) : le zip contient `Mon-Budget.apk`.
3. Installez l'APK sur le téléphone.

## Mettre à jour l'application
Remplacez `www/index.html` par la nouvelle version (même nom), validez avec **Commit changes** : l'APK se reconstruit tout seul. Le numéro de version augmente à chaque construction, et grâce à la clé fixe, l'APK s'installe par-dessus l'ancien sans perdre les données.

## Sur ordinateur (option)
Node.js 20, Java 17 et Android Studio : `npm install`, `npx cap add android`, `npx capacitor-assets generate --android`, `npx cap sync android`, `npx cap open android`.

## Rappels (notifications)
Le projet inclut le module @capacitor/local-notifications. Dans l'application : Budget > « Activer les rappels sur le téléphone », puis acceptez l'autorisation.

## Sécurité
Le projet inclut le verrouillage par empreinte / visage (@aparajita/capacitor-biometric-auth) et le blocage des captures d'écran (@capacitor-community/privacy-screen). Activez-les dans l'application : Budget > Sécurité et rappels (définissez d'abord un code PIN de secours).
