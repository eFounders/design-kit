---
name: design-review
description: Vérifie qu'une UI est on-brand et propre en la comparant au design system. Utiliser quand on dit "review ma feature", "c'est prêt", "vérifie cet écran", "audit le design", ou avant une PR avec de l'UI. Deux échelles : une feature/page (run quotidien) ou tout le produit (audit ponctuel).
---

# Design review — la passe on-brand

Tu compares une UI au design system du projet et tu listes les écarts. But : corriger seul ce qui se corrige, ne remonter au designer que ce qui le nécessite.

## 1. Périmètre
Demande ou déduis l'échelle : une feature/page (défaut, avant PR) ou tout le produit (audit ponctuel). Identifie les fichiers concernés (git diff de la branche, ou tout le dossier UI).

## 2. Charger la référence
Lis `design-system/tokens.css`, `components.md`, `patterns.md`, et le `CLAUDE.md` (contexte + ton). C'est la SEULE vérité.

## 3. Vérifier (mécanique → subjectif)
Mécanique :
- Valeurs en dur (hex/rgb, px de spacing, font-size) hors tokens → chaque occurrence = écart, avec le token correct.
- Composants/classes absents de `components.md`.
- Les 5 états présents (vide, chargement, erreur, partiel, idéal).
- Textes : conformes au ton du CLAUDE.md, aucun placeholder.
- 1 seul bouton primary par écran ; 1 seul H1.
Subjectif (prudence) : hiérarchie, simplicité. Doute → 🟡 ou 🔴, jamais ✅ par complaisance.

## 4. Verdict
```
## Design review — [périmètre]
### ✅ Conforme
### 🟡 À corriger (auto-fixable)
- [fichier:ligne] [écart] → [token/composant correct]
### 🔴 Designer requis
- [point] → [pourquoi un humain doit trancher]
Verdict : PASS / CORRECTIONS / DESIGNER REQUIS
```

## 5. Suite
- CORRECTIONS : propose d'appliquer les fixes, puis re-vérifie.
- DESIGNER REQUIS : prépare un message court (contexte + capture + question) pour le designer.
- Composant manquant : ajoute-le au log de `components.md`, ne bricole pas.

## Règles
- Toujours fichier + ligne pour un écart.
- Un écart = ce qu'un utilisateur ou le designer remarquerait, pas du pinaillage.
- Jamais ✅ si un état (vide/erreur/chargement) manque.
