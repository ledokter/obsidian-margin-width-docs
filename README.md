---
title: CSS Obsidian — largeur & marges (doc complète)
type: doc-obsidian
maj_le: 2026-11-12
tags: [obsidian, css, theme, marges, largeur]
---

# CSS Obsidian — largeur & marges (doc complète)

Tout pour régler l'affichage des notes Obsidian : largeur de colonne, marges latérales, dépannage pas-à-pas. Sources : forum obsidian.md (thread « readable line length », extrait nov 2023), guides vidéo 2026 (Nexustech « Change Margins », Behind Tools « Full Guide »), extraits complets.

## 1. Le réglage principal d'abord : « Readable line length »

Paramètres → Éditeur → désactiver **« Readable line length »**.
C'est ce réglage qui impose la colonne étroite et crée les marges latérales. Aucun snippet CSS ne peut le contourner proprement s'il reste activé. Effet immédiat : la note s'élargit à toute la fenêtre.

## 2. Snippet largeur (colonnne personnalisée, note centrée)

Si tu préfères une colonne plus large mais centrée (au lieu du plain large complet) :
Paramètres → Apparence → Extraits CSS → icône dossier → fichier `largeur.css` :

```css
body {
  --file-line-width: 1000px;
}
```

Valeur libre : 800 px (cozy) à 1200 px++. Solution validée sur le forum (jombo, nov 2023) — fonctionne en édition et lecture.
Alternative sans CSS : plugin communautaire **Editor Width Slider** (curseur par note).

## 3. Snippet marges zéro (padding des vues)

`marges.css` — supprime les marges latérales restantes en édition et lecture :

```css
.markdown-source-view,
.markdown-reading-view {
  padding-left: 0;
  padding-right: 0;
}
```

Ajustement : `8px` au lieu de `0` pour un filet d'air.

## 4. Dépannage (si le snippet « ne fonctionne pas »)

Checklist dans l'ordre :

1. **Readable line length désactivé ?** (étape 1 — cause n°1)
2. **Fichier bien nommé** `marges.css` — Windows masque les extensions par défaut : le piège classique est `marges.css.txt` (créé par le Bloc-notes en « document texte »). Vérifier : Affichage → extensions de fichiers dans l'Explorateur, ou créer le fichier avec le Bloc-notes → Enregistrer sous → type « Tous les fichiers »
3. **Snippet visible et activé** : il doit apparaître dans Paramètres → Apparence → Extraits CSS, bouton **allumé** ; cliquer **Recharger les extraits** après toute modification du fichier
4. **Thème : les thèmes personnalisés peuvent écraser les règles** — tester en thème par défaut (Apparence → Thème → Default). Si ça marche en Default, le thème ajoute ses propres padding : passer plus de poids au snippet :
```css
.markdown-source-view,
.markdown-reading-view {
  padding-left: 0 !important;
  padding-right: 0 !important;
}
```
5. **Mode** : tester en édition ET lecture (le snippet couvre les deux)
6. Toujours bloqué : faire une capture de l'écran (la fenêtre + la note) et montrer au vault/agent pour cibler la panne

## 5. Plan B sans CSS : plugin de mise en page

Paramètres → Plugins communautaires → Parcourir → chercher **Editor Width Slider** (ou un plugin de mise en page/marges) → Installer → Activer → régler les curseurs dans ses paramètres. Avantages : pas de fichier CSS, réglage par note possible ; inconvénient : dépend d'un plugin tiers.

## 6. Spécificités de ce vault

- Le vault est synchronisé via **LiveSync** (Windows + mobile + VPS) — la config `.obsidian/` (thème, snippets) reste **locale à chaque appareil** : chaque appareil doit refaire étapes 1-3 ou recevoir ses propres fichiers dans `snippets`
- Snippets activés par appareil : les fichiers `snippets/*.css` peuvent être posés manuellement une fois par appareil (l'activation se garde ensuite dans la config locale)
- Le snippet largeur (`--file-line-width`) est celui qui a le plus d'effet sur les **tableaux** : plus la colonne est large, moins la table scrolle horizontalement

## Récap express

| Objectif | Réglage |
|---|---|
| Note pleine largeur | Readable line length OFF |
| Colonne centrée large | Snippet `body { --file-line-width: 1000px; }` |
| Marges latérales à zéro | Snippet padding 0 sur source/reading view |
| Réglage graphique sans CSS | Plugin Editor Width Slider |
