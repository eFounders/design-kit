# 🎨 Design Kit

> Un squelette duplicable par projet pour builder on-brand avec Claude Code. Volontairement minimal.

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
│   ├── components.md      composants autorisés + règles
│   ├── patterns.md        patterns UX (les 5 états, forms, erreurs, vide…)
│   └── storybook.html     playground interactif (perso live : marque, dark, radius, densité, police, icônes ; tokens, composants, tags)
└── .claude/skills/
    └── design-review/     review on-brand avant PR
```

## Les 2 règles

1. **Le DS est la source de vérité.** Aucune couleur, spacing ou composant hors `design-system/`. Besoin non couvert → on enrichit le DS, on ne bricole pas.
2. **Pas de merge UI sans `design-review`.** Le skill compare au DS et ne remonte au designer que ce qui le nécessite.
