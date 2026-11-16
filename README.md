# Super Smash Kheys — appli Android

La même partie que le script Tampermonkey, dans une appli Android.
L'appli se connecte au même serveur en ligne (projet Firebase `smash-kheys`) : les joueurs de l'appli et ceux du script se retrouvent dans le même appart, les mêmes salons, la même ville.

## Installer l'appli (joueurs)

1. Ouvre la page **Releases** de ce dépôt sur ton téléphone.
2. Télécharge le fichier `SmashKheys-X.Y.Z.apk` de la dernière version.
3. Ouvre-le. Si Android le demande, autorise l'installation depuis ton navigateur.
4. Lance **Smash Kheys**, choisis ton pseudo, joue.

Mise à jour : installe la nouvelle APK par-dessus l'ancienne, la progression est gardée. L'appli prévient elle-même quand une nouvelle version est publiée.

## Contenu du dépôt

| Fichier | Rôle |
|---|---|
| `app/src/main/assets/game/smash-kheys.user.js` | le jeu (copie du script Tampermonkey) |
| `app/src/main/assets/index.html` | écran d'accueil de l'appli (pseudo, bouton retour, son en arrière-plan, avis de mise à jour) |
| `app/src/main/assets/lib/` | three.js et Firebase (copies locales : l'appli n'en a pas besoin en ligne) |
| `app/src/main/java/fr/kheys/smash/MainActivity.java` | la fenêtre Android (plein écran, paysage) |
| `.github/workflows/apk.yml` | construction automatique de l'APK par GitHub |

## Publier une nouvelle version de l'appli

1. Remplace `app/src/main/assets/game/smash-kheys.user.js` par la nouvelle version du script.
2. Crée un tag `vX.Y.Z` (par exemple `v0.93.0`) : sur GitHub, **Releases → Draft a new release → Choose a tag → v0.93.0 → Create new tag**, puis **Publish release**.
   GitHub construit l'APK tout seul (onglet **Actions**, ~5 min) et l'ajoute à la release.

## Clé de signature (à faire une seule fois)

Android n'accepte une mise à jour que si elle est signée avec **la même clé** que l'appli installée.
La clé n'est pas dans le dépôt : elle est donnée à GitHub sous forme de deux secrets.

Dans le dépôt : **Settings → Secrets and variables → Actions → New repository secret**, et crée :

- `SSK_KEYSTORE_B64` : le contenu du fichier `SSK_KEYSTORE_B64.txt`
- `SSK_KEYSTORE_PASS` : le contenu du fichier `SSK_KEYSTORE_PASS.txt`

Garde aussi `ssk.jks` en lieu sûr (hors de GitHub) : sans lui, impossible de publier une mise à jour installable par-dessus.
