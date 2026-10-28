# Mon Budget : fabriquer l'APK

Le dossier `www/index.html` contient l'application. Deux façons d'obtenir l'APK.

## Option A : sans installer Android Studio (GitHub)
1. Créez un compte gratuit sur github.com et un nouveau dépôt.
2. Envoyez-y tout le contenu de ce dossier (sur ordinateur : « Add file > Upload files »). Le dossier caché `.github` doit être envoyé aussi.
3. Ouvrez l'onglet **Actions**, choisissez « Construire l'APK », puis **Run workflow**.
4. Après quelques minutes, ouvrez l'exécution terminée : le fichier **mon-budget-apk** est à télécharger en bas de page (c'est un zip qui contient `app-debug.apk`).
5. Copiez l'APK sur le téléphone et installez-le (autorisez « sources inconnues » si le téléphone le demande).

## Option B : sur ordinateur
Prérequis : Node.js 20, Java 17 et Android Studio.
```
npm install
npx cap add android
npx capacitor-assets generate --android
npx cap sync android
npx cap open android
```
Dans Android Studio : **Build > Build APK(s)**.

## Modifier l'application
Changez `www/index.html`, puis relancez `npx cap sync android` (option B) ou envoyez le fichier sur GitHub (option A).

## Plus tard
- Play Store : il faut un fichier signé (AAB) et un compte développeur.
- Notifications de rappel : module @capacitor/local-notifications.
