# 🎨 Design Kit

> Un squelette duplicable par projet pour builder on-brand avec Claude Code. Volontairement minimal.

🔗 **Démo live (template)** : [design-kit-storybook.vercel.app](https://design-kit-storybook.vercel.app) — le storybook de référence du kit, en `[PROJECT NAME]`. Chaque projet dupliqué déploie ensuite le sien.

## Quickstart

> Sur GitHub : bouton **« Use this template »** → un repo neuf, sans historique. (ou `git clone`.)

```bash
# 1. récupérer le kit
git clone git@github.com:eFounders/design-kit.git mon-projet && cd mon-projet

# 2. le rendre tien (les 2 seuls fichiers à éditer pour démarrer)
#    design-system/tokens.css → marque, police, radius, densité, tags
#    CLAUDE.md                → produit, persona, ton, stack

# 3. voir le résultat
open design-system/storybook.html   # ou déployer design-system/ sur Vercel
```

## Comment l'utiliser

1. **Dupliquer** ce dossier au démarrage d'un projet.
2. **Remplir le DS** (`design-system/`) à partir de la direction visuelle / du proto : couleurs, typo, composants.
3. **Adapter `CLAUDE.md`** (contexte produit + ton).
4. **Builder** : Claude Code lit le DS et les règles automatiquement.
5. **Avant chaque PR avec de l'UI** : lancer le skill `design-review`.

## Structure

```
design-kit/
├── README.md          ← vous êtes ici
├── CLAUDE.md          ← contexte + règles design (à remplir)
├── design-system/     ← la source de vérité, lue par Claude Code
│   ├── tokens.css         tokens shadcn (--primary, --background…), 2 étages, light/dark
│   ├── components.css     composants prêts à l'emploi, 100% pilotés par les tokens
│   ├── components.md      specs des composants (variantes, états, quand utiliser)
│   ├── patterns.md        patterns UX (les 5 états, forms, erreurs, vide…)
│   └── storybook.html     playground interactif (consomme tokens.css + components.css)
└── .claude/skills/
    └── design-review/     review on-brand avant PR
```

> **Plug-and-play** : poser `tokens.css` + `components.css` dans un proto et utiliser les classes (`btn`, `tag`, `side-nav`, `card`…) → les composants s'adaptent à la marque/police/radius comme les tokens. Le storybook les consomme via ces mêmes fichiers (pas de duplication).

## Les 2 règles

1. **Le DS est la source de vérité.** Aucune couleur, spacing ou composant hors `design-system/`. Besoin non couvert → on enrichit le DS, on ne bricole pas.
2. **Pas de merge UI sans `design-review`.** Le skill compare au DS et ne remonte au designer que ce qui le nécessite.
