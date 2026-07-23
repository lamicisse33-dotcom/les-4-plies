# ÉQUILIBRE — déploiement v207

Ton site est **déjà en ligne et fonctionne** : https://equilibre.khalam.app
Il ne s'agit donc pas de créer un dépôt, mais d'une **mise à jour normale**, en upload-over.
Tu n'as **rien à recréer** : `manifest.json`, les icônes et `confidentialite.html` sont déjà là-bas.

## Ce que tu déposes

| Fichier | Pourquoi |
|---|---|
| `index.html` | modifié — les 10 habillages, la boutique, l'essai |
| `sw.js` | modifié — cache réparé, nouvelle liste |
| `plastique.webp` | **nouveau** — ciel de Plastique |
| `elements.webp` | **nouveau** — nébuleuse des Quatre Éléments |
| `coris-parchemin.webp` | **nouveau** — parchemin de Coris |
| `phenix.webp` | à remettre **à la racine** (il était dans `skins/`) |
| `phenix-anim-fond.webp` | **nouveau** — animation du Phénix, fond |
| `phenix-anim-feu.webp` | **nouveau** — animation du Phénix, feu |

**Tout à la racine**, à côté d'`index.html`. Pas de sous-dossier.

## Ce que tu NE déposes pas

- `la-revelation-des-coris.html` — **inchangé**, celui du site convient. Je te l'ai remis dans le dossier uniquement pour que tu l'aies sous la main.
- `manifest.json`, les trois icônes, `confidentialite.html` — déjà en ligne, n'y touche pas.

## Ce que tu ne supprimes pas

Rien. En particulier, laisse `skins/` où il est : le code ne s'en sert plus, mais supprimer n'apporte rien et la règle du projet est de ne jamais supprimer.

## Comment

1. github.com → dépôt `les-4-plies`
2. **Add file → Upload files**, glisse les 8 fichiers, **Commit changes**
3. Deux à trois minutes, puis ouvre https://equilibre.khalam.app

Si le jeu est déjà installé sur ton téléphone, la bannière **« Nouvelle version disponible »** apparaîtra d'elle-même.

## Vérifier

Ouvre la boutique. Sous le solde s'affiche :

- `v207 · MODE TEST · images : OK (1080px)` → tout est arrivé.
- `v207 · MODE TEST · images : ABSENTES` → les `.webp` ne sont pas à la racine.

Pour essayer les habillages sans les acheter : **cinq appuis sur « Ton solde »**. Rien n'est enregistré ; cinq appuis de plus annulent.

## ⚠️ MODE TEST — à désactiver avant Google Play

Les 10 habillages sont ouverts pour tous, le temps de la phase de test.
Dans `index.html`, cherche :

```js
const MODE_TEST = true;
```

Le jour de la publication, passe-le à `false` et redéploie. C'est la seule chose à faire :
rien n'est enregistré dans les téléphones, donc aucune donnée à nettoyer. Les points gagnés
et les vrais achats des testeurs, eux, sont conservés.

Tant que c'est actif, la boutique affiche **MODE TEST** en rose sous le solde.

Le cadeau de bienvenue est **suspendu** pendant les tests : il proposerait trois habillages
déjà possédés. Il n'est pas consommé pour autant — chaque testeur le recevra normalement
le jour où `MODE_TEST` repasse à `false`.

## Ce que cette version change

- `index.html` passe de **1 107 à 538 Ko** : les cinq plus grosses images en sont sorties.
- Elles ne sont plus chargées par tout le monde. Le service worker ne les met pas en cache à l'installation : chacune n'est téléchargée qu'à sa première utilisation, puis conservée.
- Les deux plus lourdes n'étaient pas des habillages mais les couches de l'animation du Phénix, que tous les joueurs téléchargeaient depuis toujours — 208 Ko.
