# Patterns UX — [NOM DU PROJET]

> Les situations récurrentes et LA façon de les traiter dans ce produit. Claude Code : appliquer systématiquement.

## Les 5 états de chaque écran

Tout écran code ses 5 états — c'est le critère le moins négociable de la review :

1. **Vide / Day-1** : même structure, contenu conditionnel. Jamais de fausses données. Bloc centré : icône + titre + 1-2 lignes + 1-2 CTA.
2. **Chargement** : skeleton sur la structure réelle, pas de spinner plein écran.
3. **Erreur** : cause + action de récupération. Jamais de code seul.
4. **Partiel** : peu de données / valeurs longues gérées.
5. **Idéal** : le cas nominal.

> Règle : le même composant doit tenir avec ou sans données — pas de template séparé.

## Formulaires

- Une colonne, labels au-dessus des champs.
- Validation : au blur + au submit. Jamais pendant la frappe (sauf force du mot de passe).
- Bouton submit : désactivé jamais — toujours cliquable, avec erreurs affichées au clic.
- Formulaire > 6 champs → découper en étapes ou sections.
- Sauvegarde : [auto-save / bouton explicite — choisir et tenir partout]

## États vides (empty states)

Structure obligatoire : 1) illustration ou icône discrète, 2) une phrase expliquant ce que cet espace contiendra, 3) action principale pour le remplir.
Jamais : "Aucune donnée", tableau vide brut.

## Chargement

- < 300ms : rien.
- 300ms – 2s : skeleton (pas de spinner plein écran).
- > 2s ou action lourde : message de progression.
- Squelettes : sur la structure réelle de l'écran, pas un spinner générique.

## Erreurs

- Erreur de champ : inline sous le champ.
- Erreur d'action : toast si non bloquante, inline si bloquante.
- Erreur système (500, offline) : écran ou bandeau avec 1) explication simple, 2) action de récupération (réessayer, contacter).
- Ton : voir `CLAUDE.md` (§ Ton). Jamais de code d'erreur seul.

## Confirmations & actions destructives

- Destructif réversible (archiver) : action immédiate + toast avec "Annuler".
- Destructif irréversible (supprimer) : modal de confirmation, le bouton nomme l'objet ("Supprimer le projet").
- Jamais de double confirmation.

## Feedback de succès

- Action courante : toast discret.
- Première fois / moment clé du parcours : célébration légère [à définir selon DA].

## Navigation & hiérarchie

- Profondeur max : 3 niveaux.
- L'utilisateur sait toujours : où il est (état actif visible), comment revenir (breadcrumb ou back).
- Une page = un titre H1 qui correspond au libellé de navigation.

## Responsive

- [Mobile-first ou desktop-first ? Breakpoints ? Quelles features mobile ?]

## Accessibilité — minimum non négociable

- Contraste AA (4.5:1 texte, 3:1 UI).
- Tout est utilisable au clavier, focus visible.
- Images porteuses de sens : alt. Icônes seules : label accessible.

---

# Patterns IA ✦

> Les situations propres à un produit IA. À appliquer dès qu'il y a de la génération.

## Conversation
- Fil vertical, du plus ancien au plus récent, auto-scroll vers le bas à chaque nouveau message.
- Tours distincts user / assistant (voir composant Message). L'assistant peut rendre du markdown riche.
- Actions sur un message (copier, régénérer, feedback) discrètes, révélées au survol.

## Composer & envoi
- Entrée = envoyer · Shift+Entrée = nouvelle ligne. Le bouton Envoyer devient **Stop** pendant la génération.
- Désactivé seulement si quota atteint → message clair (pas un bouton grisé muet).

## Streaming & attente
- La réponse s'écrit en flux (token par token) plutôt qu'apparaître d'un bloc.
- Agent multi-étapes → afficher l'étape en cours (« Recherche… », « Analyse… »).
- Toujours interrompable. Respecter `prefers-reduced-motion`.

## Sources & confiance
- Toute réponse factuelle peut citer ses sources : puces [1] dans le texte → liste sous la réponse.
- Réponse incertaine → le signaler et inviter à vérifier. Ne jamais masquer l'incertitude.

## Feedback & correction
- Pouce haut/bas + régénérer sur chaque réponse assistant. Pouce bas → motif rapide optionnel.
- L'utilisateur peut toujours éditer son prompt et relancer.

## Erreurs IA
- Quota / rate limit : « Limite atteinte, réessaie dans X » (jamais un échec sec).
- Réponse refusée : expliquer simplement, sans jargon ni code.
- Timeout / réseau : message + Réessayer. Le prompt saisi n'est jamais perdu.

## Day-1 IA (premier usage)
- Pas de dashboard vide : une **invite à agir**. 3-4 prompts d'exemple cliquables + une phrase sur ce que l'IA sait faire.
- Le premier succès doit arriver en un clic (exemple pré-rempli).
