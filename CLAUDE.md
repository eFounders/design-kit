# CLAUDE.md — [NOM DU PROJET]

> À remplir pendant l'onboarding. Remplacer les [crochets], puis supprimer cette ligne.

## Contexte produit

- **Produit** : [une phrase — ce que fait le produit, pour qui]
- **Persona** : [utilisateur principal + son objectif]

## Règles design — NON NÉGOCIABLES

1. **Toujours utiliser le design system** : `design-system/tokens.css` (valeurs) + `components.css` (composants, classes `btn`/`tag`/`side-nav`…) + `components.md` (specs d'usage) + `patterns.md`. Aucune couleur, taille, spacing, radius ou composant inventé.
2. **Composant manquant** : ne pas improviser → combiner l'existant + logger dans `components.md` § Composants manquants.
3. **Les 5 états** : tout écran code vide, chargement, erreur, partiel, idéal (voir `patterns.md`).
4. **Ton** : [tutoiement/vouvoiement, 2-3 mots de personnalité, vocab à éviter — à remplir].
5. **Icônes** : une SEULE bibliothèque pour tout le projet → **[Lucide]** (défaut). Alternatives au choix à l'onboarding : Phosphor, Heroicons. Tailles via `--icon-sm/md/lg`. Jamais mélanger deux libs.
6. **Simplicité** : un objectif par écran, 1 seul bouton primary. En cas de doute, le plus simple pour l'utilisateur.

## À personnaliser par projet (dans `tokens.css`)

Couleur de marque (`--brand-*`) · police (`--font-base` / `--font-mono`) · personnalité des angles (`--radius`) · densité (`--text-base`, qui rescale toute l'échelle `--text-*`) · palette de tags (`--tag-*`) · bibliothèque d'icônes (ci-dessus). Les composants et patterns suivent automatiquement — on ne les retouche pas.

## Source de vérité

Le dossier `design-system/` (code) est LA référence. Une feature ne modifie jamais un token en douce.

## Stack technique

- [Framework front : ex. React + Tailwind — où vivent les composants, comment les tokens sont importés]

## Avant une PR avec de l'UI

Lancer le skill `design-review` → il compare au DS et rend un verdict PASS / CORRECTIONS / DESIGNER REQUIS.
