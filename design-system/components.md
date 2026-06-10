# Composants — [NOM DU PROJET]

> Inventaire des composants autorisés. À adapter au produit, mais la liste couvre déjà ce dont on a besoin à chaque projet.
> Chaque fiche est **auto-descriptive** : à quoi ça sert · quand l'utiliser · quand NE PAS · variantes · états · tokens · règles. C'est ce que l'agent lit pour coder juste (R. Kavcic & TJ Pitre).
> Règle absolue : toutes les valeurs viennent de `tokens.css` (`var(--…)`). Jamais de hex/px en dur.
> Composant absent → NE PAS l'inventer : combiner l'existant + logger (§ Composants manquants).

---

## Règle transversale — icône + texte sur une même ligne

Construction standard, simple, identique à Figma et shadcn :

- Conteneur en `display: inline-flex; align-items: center; gap: var(--space-2)`.
- **Hauteur fixe** (ex. bouton `min-height: 36px`, padding horizontal seulement) : c'est elle qui garantit des composants de même taille (avec ou sans icône) et le centrage vertical. On ne joue pas sur le `line-height` ni le padding vertical pour caler.
- Icône à taille fixe : `flex: none` + `width/height` en `--icon-sm/md/lg`, jamais étirée.

Parité Figma (optionnel) : Figma rogne le `leading` du texte à la hauteur de capitale, ce qui centre l'icône sur le **milieu optique** des lettres. L'équivalent CSS exact est `text-box-trim: trim-both; text-box-edge: cap alphabetic;` sur l'élément qui porte le texte. Sans ça, un centrage flex laisse l'icône ~1px plus bas (comportement identique à shadcn). À activer seulement si on vise le pixel-perfect et qu'on cible des navigateurs récents.

---

# 1 · Formulaires & saisie

### Button
- **Sert à** : déclencher une action.
- **Pas pour** : naviguer (→ lien). Réglage on/off (→ Switch).
- **Variantes** : `primary` (action principale, 1/écran), `secondary`, `ghost`, `destructive`, `outline`.
- **Tailles** : `sm` / `md` (défaut) / `lg` — via padding + `--text-*` + `--icon-*`, jamais une hauteur en dur.
- **Icône** : optionnelle, à gauche (défaut) ou à droite (mouvement vers l'avant : Next, Ouvrir). Icône en carré fixe centré (`--icon-sm`, `lg` → `--icon-md`). Icon-only : disponible dans toutes les variantes, `aria-label` obligatoire.
- **États** : default, hover (`--primary-hover`/`--secondary-hover`/`--accent`), active, focus-visible (`--ring`), disabled (`--disabled-foreground`), loading (si > 300ms).
- **Tokens** : `--primary`/`--primary-foreground`/`--primary-hover`, `--secondary…`, `--destructive…`, `--border` (outline), `--radius-md`, `--ring`.
- **Règles** : label = verbe d'action. Jamais deux `primary` côte à côte. `destructive` → confirmation.

### Icon button
- **Sert à** : action compacte sans label (barre d'outils, fermer).
- **Règles** : toujours un `aria-label`. Zone cliquable ≥ 32px. Tooltip au survol.
- **Tokens** : `--foreground`/`--muted-foreground`, `--accent` (survol), `--radius-md`.

### Input (texte)
- **Sert à** : saisir une valeur courte sur une ligne.
- **Anatomie** : label visible au-dessus (jamais placeholder seul) + champ + hint/erreur.
- **États** : default (bordure `--input`), focus (`--ring`), erreur (`--destructive`), disabled.
- **Tokens** : `--input`, `--ring`, `--destructive`, `--muted-foreground` (hint), `--radius-md`.
- **Règles** : erreur affichée sous le champ après blur/submit, pas pendant la frappe.

### Search input
- **Sert à** : filtrer/chercher dans une liste ou globalement.
- **Anatomie** : icône loupe à gauche, placeholder explicite, bouton clear (×) quand rempli.
- **Comportement** : debounce ~250ms. Résultats vides → état vide « Aucun résultat pour "X" » + suggestion d'élargir.
- **Tokens** : `--input`, `--muted-foreground` (icône/placeholder), `--ring`, `--radius-md`.

### Textarea
- **Sert à** : texte long multi-lignes. Auto-grow recommandé. Compteur si limite.
- **Tokens** : idem Input.

### Select / Dropdown
- **Sert à** : choisir UNE option parmi plusieurs.
- **Pas pour** : 2 options (→ Switch/Radio) ; >10 options (→ Combobox avec recherche).
- **Tokens** : `--popover`/`--popover-foreground` (liste), `--accent` (option survolée/sélectionnée), `--border`, `--radius-md`.

### Combobox (select cherchable)
- **Sert à** : choisir parmi beaucoup d'options, avec recherche intégrée. Multi-select possible (chips).
- **Tokens** : idem Select + chips (voir Badge).

### Checkbox / Radio
- **Checkbox** : choix multiples indépendants. **Radio** : choix exclusif (2-5 options visibles).
- **Tokens** : `--primary` (coché), `--border` (vide), `--ring` (focus).

### Switch (toggle)
- **Sert à** : activer/désactiver un réglage, effet immédiat.
- **Pas pour** : une action à conséquence (→ Button + confirmation).
- **Tokens** : `--primary` (on), `--muted`/`--border` (off).

### Form (layout)
- Une colonne, labels au-dessus. > 6 champs → sections ou étapes. Voir `patterns.md` § Formulaires.

---

# 2 · Données & affichage

### Table
- **Sert à** : afficher des lignes structurées comparables.
- **Anatomie** : header (tri), lignes, pagination, actions par ligne, sélection multiple optionnelle.
- **Fonctions** : tri par colonne, pagination ou scroll infini, ligne survolée (`--state-hover`), ligne sélectionnée (`--accent`), densité (confort/compact).
- **États** : vide (« aucune donnée » + CTA), chargement (skeleton de lignes), erreur, partiel.
- **Tokens** : `--border` (lignes/séparateurs), `--muted-foreground` (header), `--card` (fond), `--accent` (sélection), `--state-hover`.
- **Règles** : actions destructives par ligne → confirmation. Colgroup aligné (nombres à droite).

### Filter bar / Filtres
- **Sert à** : restreindre une liste/table.
- **Éléments** : boutons-filtres (déroulants), **chips actifs supprimables** (× pour retirer), bouton « Tout effacer », compteur de résultats.
- **Tokens** : `--secondary`/`--border` (boutons inactifs), `--primary-subtle`/`--primary` (filtre actif), `--accent`.
- **Règles** : un filtre actif est visible et retirable. État « aucun résultat » distinct de « pas de données ».

### Tabs
- **Sert à** : basculer entre vues d'un même contexte.
- **Tokens** : `--border` (ligne basse), `--primary` (onglet actif), `--muted-foreground` (inactif).

### Card
- **Sert à** : regrouper un contenu lié sur une surface posée.
- **Anatomie** : head (titre + action), corps, footer optionnel.
- **Tokens** : `--card`/`--card-foreground`, `--border`, `--radius-xl`.

### Stat / KPI
- **Sert à** : un chiffre clé + tendance. 3-4 max par rangée. Jamais de camembert.
- **Tokens** : `--text-xl` (valeur), `--muted-foreground` (label), `--success`/`--destructive` (delta).

### Badge / Pill
- **Sert à** : statut court d'un objet, **sémantique uniquement**.
- **Variantes sémantiques** : neutre (`--muted`/`--muted-foreground`), succès, attention, danger, info — chacune avec sa version `-subtle` en fond.
- **Pas pour** : une action (→ Button) ; une catégorie/étiquette décorative (→ Tag).

### Tag / Label
- **Sert à** : étiquette **décorative** non sémantique (catégorie, équipe, statut custom, projet). La couleur identifie, elle ne veut pas dire « erreur » ou « succès ».
- **Palette** : tokens `--tag-{teinte}-bg` + `--tag-{teinte}-fg` (gray, red, orange, amber, green, teal, blue, violet, pink). À recolorer/élargir par projet dans `tokens.css`.
- **Pas pour** : un statut sémantique (→ Badge). Ne JAMAIS détourner les couleurs feedback (`--success`…) pour une catégorie.
- **Règles** : une teinte = une catégorie, stable dans le temps. Pastille optionnelle. Retirable (×) si c'est un filtre actif.

### Avatar
- Initiales ou image, rond (`--radius-full`). Fallback initiales sur `--muted`.

### Tooltip
- Info brève au survol/focus. Fond `--popover`. Jamais d'info essentielle uniquement en tooltip.

### Empty state
- Voir `patterns.md` § États vides. Icône + titre + 1-2 lignes + CTA. Jamais « Aucune donnée » brut.

---

# 3 · Overlays & feedback

### Modal / Dialog
- **Sert à** : décision ou focus absolu.
- **Pas pour** : contenu secondaire (→ Drawer). Jamais de modal dans une modale.
- **Tokens** : `--popover`/`--popover-foreground`, `--overlay`, `--radius-lg`.
- **Règles** : fermable Esc + clic backdrop (sauf perte de données → confirmation).

### Drawer / Slide-over
- **Sert à** : détail/édition latéral sans quitter le contexte (drill-in).
- **Tokens** : `--card`, `--border`, `--overlay`.

### Dropdown menu
- **Sert à** : liste d'actions sur un objet (menu « … »).
- **Tokens** : `--popover`, `--accent` (item survolé), `--destructive` (action destructive).

### Toast / Notification
- **Sert à** : confirmer une action sans bloquer (~4s).
- **Pas pour** : une erreur bloquante (→ inline).

---

# 4 · Navigation

### Sidebar / Nav
- Structure d'IA du produit, item actif visible (`--accent`/`--primary`), groupes en `--text-2xs` majuscule `--muted-foreground`. Profondeur max 3.

### Breadcrumb
- Chemin de retour sur les vues profondes. Dernier élément = page courante (non cliquable).

### Pagination
- Pages ou « charger plus ». Indiquer la position (« 1-20 sur 240 »).

---

# 5 · Composants IA  ✦

> Le cœur d'un SaaS IA. Sans ces fiches, l'agent improvise ces écrans (= produit incohérent).

### Message (bulle de conversation)
- **Sert à** : un tour de conversation (utilisateur ou assistant).
- **Variantes** : `user` (fond `--primary-subtle` ou `--accent`, aligné à droite/distinct), `assistant` (fond `--card`, bordure `--border`, markdown riche).
- **Anatomie assistant** : contenu + barre d'actions (copier, régénérer, feedback) + sources optionnelles.
- **Tokens** : `--primary-subtle`/`--accent` (user), `--card`/`--border` (assistant), `--muted-foreground` (méta/horodatage).

### Composer (saisie du prompt)
- **Sert à** : écrire et envoyer un prompt.
- **Anatomie** : textarea auto-grow + bouton Envoyer (devient **Stop** pendant la génération) + actions (pièce jointe, modèle). Entrée = envoyer, Shift+Entrée = nouvelle ligne.
- **États** : vide (placeholder d'exemple), en frappe, **génération en cours** (Stop), désactivé (quota atteint → message clair).
- **Tokens** : `--input`, `--ring`, `--primary` (Envoyer), `--radius-lg`.

### Streaming / « en train de réfléchir »
- **Sert à** : montrer que l'IA travaille ou écrit.
- **Patterns** : curseur/typing pour le texte qui s'écrit ; libellé d'étape (« Recherche… », « Analyse… ») pour les agents multi-étapes. Toujours interrompable (Stop).
- **Tokens** : `--muted-foreground`, `--accent` (pulse léger). Respecter `prefers-reduced-motion`.

### Sources / Citations
- **Sert à** : montrer d'où vient la réponse (confiance).
- **Patterns** : puces numérotées [1] dans le texte → liste de sources sous la réponse (titre + domaine + lien). Repliable si nombreuses.
- **Tokens** : `--muted-foreground`, `--link`, `--border`, `--surface-sunken` (encart).

### Feedback IA
- **Sert à** : noter une réponse (pouce haut/bas), régénérer, copier.
- **Règles** : discret tant qu'on ne survole pas. Pouce bas → proposer un motif rapide.
- **Tokens** : `--muted-foreground` (défaut), `--foreground` (actif), `--accent`.

### États d'erreur IA
- **Sert à** : gérer les échecs propres à l'IA.
- **Cas** : quota/rate limit (« limite atteinte, réessaie dans X »), réponse refusée (expliquer sans jargon), timeout/réseau (Réessayer), réponse incertaine (signaler, inviter à vérifier).
- **Tokens** : `--warning…` (limite/incertitude), `--destructive…` (échec), `--muted-foreground`.
- **Règles** : jamais de code d'erreur brut ; toujours une action de sortie.

### Day-1 IA (premier usage)
- **Sert à** : l'écran vide d'un produit IA.
- **Pattern** : pas un dashboard vide → une **invite à agir** : 3-4 prompts d'exemple cliquables + une phrase sur ce que l'IA peut faire. Voir `patterns.md` § Patterns IA.

---

## Composants manquants — log

> Besoin d'un composant absent → on le note ici, on ne bricole pas. Décision au rituel → mise à jour du DS.

| Date | Besoin | Demandé par | Statut |
|---|---|---|---|
| | | | à créer / créé / refusé (alternative : …) |
