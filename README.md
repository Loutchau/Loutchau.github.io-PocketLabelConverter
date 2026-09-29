# loutchau.dev — le site public

Ce dépôt **est** le site. Il est public, et GitHub Pages le sert depuis la racine de
`main` : ce qui est commité ici est en ligne une minute plus tard.

```
.
├── CNAME                                        loutchau.dev
├── .nojekyll                                    du HTML pur, pas de Jekyll
├── index.html                                   page d'accueil
├── assets/style.css                             une feuille, zéro dépendance
└── pocket-label-converter/
    ├── index.html                               ← URL d'assistance (App Store)
    └── confidentialite/index.html               ← URL de confidentialité (App Store)
```

Les deux URL que l'app et App Store Connect attendent :

| | |
|---|---|
| Confidentialité | `https://loutchau.dev/pocket-label-converter/confidentialite` |
| Assistance | `https://loutchau.dev/pocket-label-converter/` |

Chaque page est un dossier avec un `index.html`, et pas un fichier `.html` : c'est ce qui
garantit une URL sans extension, quel que soit l'hébergeur.

Les liens internes sont **absolus** (`/assets/style.css`, `/pocket-label-converter/`). Ils
supposent que le site est servi à la racine d'un domaine — ce que fait le domaine
personnalisé. Sans lui, l'adresse de repli est
`https://loutchau.github.io/Loutchau.github.io-PocketLabelConverter/` et ces chemins
tombent à côté : c'est `loutchau.dev` ou rien.

## Mise en service

**1. Pages.** Dépôt → **Settings** → **Pages** → *Source* : « Deploy from a branch »,
branche `main`, dossier `/ (root)`.

**2. Domaine.** Settings → Pages → *Custom domain* : `loutchau.dev`. Puis chez le
registrar (OVH), les enregistrements que GitHub demande :

| Type | Nom | Valeur |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `loutchau.github.io.` |

**Prends les adresses affichées dans ta page Settings → Pages** si elles diffèrent de
celles-ci. Il faut aussi **retirer les enregistrements existants** pour `@` et `www` :
tant que le domaine répond ailleurs, GitHub refuse de valider et le site reste
inaccessible.

**3. « Enforce HTTPS »** dès que GitHub a émis le certificat (la case reste grisée avant).

**4. Vérifier les deux URL** du tableau dans un navigateur, puis **depuis l'app** :
Réglages → Politique de confidentialité, et le lien sous le bouton d'abonnement. Un lien
mort sur l'écran d'achat est un motif de rejet.

## Ensuite

Les endroits à ne jamais laisser diverger :

- `pocket-label-converter/confidentialite/index.html` et le `LEGAL.md` § 3 du dépôt de
  l'app ;
- l'URL de cette page et `LegalLinks.privacyPolicy` dans l'app, qui doivent être
  **identiques au caractère près**, et identiques à ce qui est saisi dans App Store
  Connect.

Les pages ne chargent **aucune ressource distante** : pas de police Google, pas
d'analytics, pas de CDN. Une page qui promet « aucune donnée collectée » ne peut pas faire
une requête vers un tiers pour s'afficher. À vérifier avant chaque ajout.
