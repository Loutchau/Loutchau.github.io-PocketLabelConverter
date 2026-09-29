# Le site public — source

Ce dossier contient **le site à publier**, tel quel. Il vit ici pour être versionné avec
l'app (les textes doivent rester vrais quand l'app change), mais **ce n'est pas d'ici qu'il
est servi** : ce dépôt est privé, et GitHub Pages publie un dépôt entier, pas un dossier.

```
Legal/
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

---

## Pourquoi un second dépôt

La visibilité, sur GitHub, se règle **par dépôt**. Rendre un seul dossier public à
l'intérieur d'un dépôt privé n'existe pas. Trois issues :

1. **Un dépôt public dédié** — gratuit, et le code de l'app reste privé. C'est ce qui suit.
2. Rendre `Pocket-Label-Converter` public — le site marcherait, mais tout le code avec.
3. GitHub Pages depuis un dépôt privé — possible avec un abonnement GitHub Pro. Le site
   reste public de toute façon : seule la source est cachée. Payer pour ça n'a d'intérêt
   que si tu veux un seul dépôt.

## Publier (une fois, ~10 minutes)

**1. Créer le dépôt public.** Sur GitHub, un nouveau dépôt **public** nommé exactement
`Loutchau.github.io`. Ce nom a un sens particulier : il devient le site *utilisateur* de ton
compte, servi à la racine du domaine. C'est ce qui donne des URL propres, sans nom de dépôt
au milieu.

**2. Y copier ce dossier**, son contenu à la racine du dépôt — pas le dossier `Legal`
lui-même :

```sh
git clone https://github.com/Loutchau/Loutchau.github.io.git
cp -R "Pocket-Label-Converter/Legal/." Loutchau.github.io/
cd Loutchau.github.io
git add -A && git commit -m "Pages légales et assistance" && git push
```

**3. Activer Pages.** Dépôt → **Settings** → **Pages** → *Source* : « Deploy from a
branch », branche `main`, dossier `/ (root)`. Une minute plus tard, le site répond sur
`https://loutchau.github.io/`.

**4. Brancher le domaine.** Toujours dans Settings → Pages → *Custom domain* :
`loutchau.dev`. GitHub demande alors des enregistrements DNS, à créer chez ton registrar :

| Type | Nom | Valeur |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `loutchau.github.io.` |

Ces adresses sont celles que GitHub publie ; **prends celles affichées dans ta page
Settings → Pages**, pas celles-ci, si elles diffèrent. La propagation DNS prend de quelques
minutes à quelques heures.

**5. Cocher « Enforce HTTPS »** dès que GitHub a émis le certificat (bouton grisé tant que
ce n'est pas fait).

**6. Vérifier les deux URL** du tableau plus haut dans un navigateur, puis **depuis l'app** :
Réglages → Politique de confidentialité, et le lien sous le bouton d'abonnement. Un lien
mort sur l'écran d'achat est un motif de rejet.

## Ensuite

Quand un texte change ici, il faut le recopier dans le dépôt public — c'est le prix du
dépôt privé. Les deux endroits à ne jamais laisser diverger :

- `Legal/pocket-label-converter/confidentialite/index.html` et `LEGAL.md` § 3 ;
- l'URL de la page et `LegalLinks.privacyPolicy` dans l'app, qui doivent être **identiques
  au caractère près**, et identiques à ce qui est saisi dans App Store Connect.

Les pages ne chargent **aucune ressource distante** : pas de police Google, pas d'analytics,
pas de CDN. Une page qui promet « aucune donnée collectée » ne peut pas faire une requête
vers un tiers pour s'afficher.
