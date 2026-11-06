# Mon Budget

Application de gestion de salaire pensée pour le quotidien au Mali : répartition du salaire en volets, dépenses, projets, tontines, comptes (espèces, Orange Money, Moov Money, banque), dettes, mode commerçant, bilan PDF, sécurité (PIN, empreinte).

© 2026 @red76. Remerciements : Brimo, Kass, Safle Bogoti et mes parents.

## Pensée pour la vie quotidienne au Mali
- Suivi du **carburant** (litres, prix réellement payé, comparaison avec le prix officiel que vous saisissez) et **carnet de prix** pour mesurer la vie chère autour de vous.
- **Énergie et frais** : ce que coûtent l'électricité, le groupe électrogène, le gaz, l'eau et les retraits de mobile money.
- **Salaire en retard**, **dettes et avances**, **tontines**, **fonds de sécurité**, envois de la famille ou de la diaspora.
- **Commerce** : ventes, achats, stock, ventes à crédit, bénéfice et prélèvement.
- **Outils du quotidien** : popote du jour, carnet de solidarité (baptêmes, mariages, décès), papiers et échéances, provision de vivres, patrimoine, plan de précaution, calculateurs (€ ↔ FCFA à la parité fixe de 655,957, prix de vente, trajet, zakat indicative).
- **Présentation illustrée** au premier lancement et **démo animée** de 45 secondes (rejouables depuis Aide), aperçu du patrimoine, rappels et astuces personnalisés, animations fluides, quatre thèmes de couleurs, mode simplifié, saisie rapide.

Les montants et prix affichés par l'application sont toujours ceux que vous saisissez : elle n'impose aucun tarif.

## Contenu du dépôt

| Dossier ou fichier | Rôle |
|---|---|
| `www/index.html` | L'application complète (un seul fichier) |
| `www/manifest.webmanifest`, `www/sw.js`, `www/icons/` | Version web installable (PWA) |
| `assets/icon.png` | Icône (les icônes Android sont générées à partir d'elle) |
| `capacitor.config.json`, `package.json` | Configuration Android (Capacitor) |
| `.github/workflows/build-apk.yml` | Construit l'APK signé automatiquement |
| `.github/workflows/pages.yml` | Publie la version web (facultatif) |
| `PRIVACY.md`, `docs/play-store.md` | Politique de confidentialité et modèle de fiche Play Store |

## Obtenir l'APK (sans Android Studio)

### 1. Enregistrer la clé de signature (une seule fois)
La clé est dans le fichier séparé `CLE-DE-SIGNATURE-A-GARDER.txt` (ne l'envoyez jamais dans ce dépôt).
1. Dépôt GitHub > **Settings > Secrets and variables > Actions > New repository secret**.
2. Créez `KEYSTORE_BASE64` (le long texte du fichier) et `KEYSTORE_PASSWORD` (le mot de passe).
3. Gardez une copie de la clé en lieu sûr : sans elle, une mise à jour ne pourra plus s'installer par-dessus l'ancienne version.

Sans ces deux secrets, le workflow produit tout de même un APK de test, mais il ne se mettra pas à jour proprement.

### 2. Construire
1. Onglet **Actions > Construire l'APK > Run workflow** (il se lance aussi à chaque envoi de fichiers).
2. À la fin (coche verte), téléchargez **mon-budget-apk** en bas de la page de l'exécution : le zip contient `Mon-Budget.apk`.
3. Installez l'APK sur le téléphone (autorisez les sources inconnues si demandé).

### 3. Mettre à jour l'application
Remplacez `www/index.html` (même nom) puis validez avec **Commit changes**. L'APK se reconstruit ; son numéro de version augmente à chaque construction et s'installe par-dessus l'ancien sans perdre les données (clé identique).

## Installer sur iPhone et iPad (version web)
Il faut d'abord publier la version web (section suivante) : iPhone n'installe pas d'APK, il utilise une application web.
1. Sur l'iPhone, ouvrez le lien de la version web dans **Safari**.
2. Touchez **Partager** (le carré avec une flèche vers le haut), faites défiler, puis **Sur l'écran d'accueil**.
3. Touchez **Ajouter**. L'icône Mon Budget apparaît : ouvrez toujours l'application depuis cette icône.

Limites sur iPhone : pas de notifications automatiques, pas d'empreinte ni de blocage des captures (ces trois fonctions existent seulement dans l'APK Android). Le code PIN, les sauvegardes, le PDF et l'export calendrier (.ics) fonctionnent. Installez bien l'application : sans cela, Safari peut effacer les données d'un site peu utilisé.

## Version web (facultatif)
1. **Settings > Pages > Source : GitHub Actions**.
2. **Actions > Publier la version web > Run workflow**.
3. Ouvrez le lien affiché et choisissez « Ajouter à l'écran d'accueil » : l'application s'installe comme une application.

Les données de la version web et celles de l'APK sont séparées. Pour passer de l'une à l'autre, utilisez Aide > Sauvegarder ou restaurer.

## Sur ordinateur
Prérequis : Node.js 20, Java 17, Android Studio.
```
npm install
npx cap add android
npx capacitor-assets generate --android
npx cap sync android
npx cap open android   # Build > Build APK(s)
```

## Rappels et sécurité
- Rappels : Budget > Sécurité et rappels > « Activer les rappels sur le téléphone ».
- Empreinte ou visage : définissez d'abord un code PIN de secours, puis activez l'option.
- Le PIN et la biométrie bloquent l'accès à l'application ; ils ne chiffrent pas les données enregistrées.

## Pour le Play Store
Voir `docs/play-store.md` et `PRIVACY.md` (complétez l'e-mail de contact). Il faut un compte développeur Google et un fichier AAB signé.

## Licence
Tous droits réservés. Voir `LICENSE`.
