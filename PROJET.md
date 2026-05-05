# PROJET.md — Dofus Idle Rétro
> Document vivant. Mis à jour à chaque session. Version : 0.1 — Mai 2026

---

## STATUT ACTUEL

| Élément | État |
|---|---|
| Phase | 🟡 Spécification complète — En attente de génération V0.1 |
| Dernière session | Mai 2026 — Cadrage + rédaction PROJET.md |
| Prochaine étape | Générer le composant React complet V0.1 |
| Stack | React JSX — 1 fichier — localStorage |
| IA principale | Claude (cadrage/coaching) |
| IA code | ChatGPT 4o / Gemini (génération React) |
| IA locale | LM Studio 8B (CSS, boilerplate, commentaires) |
| Repo | ⬜ À créer sur GitHub |

---

## RÉSUMÉ DU PROJET (pitch 30 secondes)

Jeu idle inspiré de Dofus Rétro, jouable dans le navigateur.
Le joueur choisit une classe parmi 12, nomme son Havre Monde,
et son personnage combat automatiquement pendant son absence.
Progression via XP, kamas, drops, bâtiments et un système de prestige infini.
Cible : PC + mobile, sans serveur, 100% localStorage.

---

## DÉCISIONS D'ARCHITECTURE

| Décision | Choix retenu | Raison |
|---|---|---|
| Framework | React JSX, 1 fichier | Compatible Claude artifact + déploiement sans build |
| Persistance | localStorage | Pas de serveur, offline-first |
| Tick rate | 2 secondes (setInterval) | Équilibre fluidité / performance |
| CSS | Inline style objects + keyframes dans `<style>` | Pas de lib externe |
| Icônes | lucide-react uniquement | Seule lib autorisée |
| Offline | Plafond 8h, malus 30% | Évite exploit AFK prolongé |
| Journal | FIFO 100 lignes max | Performance mémoire |
| Inventaire | FIFO 50 items max | Performance mémoire |

---

## CHANGELOG

### V0.1 — En cours
- [ ] Tutoriel 4 étapes (nom havre, classe, nom perso, premier combat)
- [ ] Layout 4 zones : topbar / sidebar / central / panneau droit
- [ ] Barre personnages bas (6 slots)
- [ ] Vue Combat avec journal scrollable
- [ ] Vue Exploration (2 zones + accordéon monstres/drops)
- [ ] Vue Havre Monde (6 bâtiments)
- [ ] Système prestige (structure + paliers P1→P10 + Incarnation)
- [ ] Sauvegarde localStorage automatique (30s) + export/import JSON
- [ ] Calcul gains hors-ligne avec popup

---

## PALETTE & IDENTITÉ VISUELLE

```css
--bg-primary:    #1a1208   /* Fond principal sombre */
--bg-secondary:  #2d1f0a   /* Sidebar, panneaux */
--bg-panel:      #3d2b0e   /* Cartes, éléments surélevés */
--border-gold:   #8B6914   /* Bordures standards */
--border-light:  #c4922a   /* Bordures actives / hover */
--accent-orange: #e8820c   /* Boutons CTA, éléments actifs */
--accent-green:  #4a8c3f   /* Gains positifs, succès */
--text-primary:  #f0d090   /* Texte principal */
--text-secondary:#c4922a   /* Labels, titres secondaires */
--text-muted:    #7a6040   /* Texte désactivé */
--hp-bar:        #c0392b   /* Barres de vie */
--xp-bar:        #27ae60   /* Barre d'expérience */
--rarity-common: #9b9b9b
--rarity-rare:   #2196F3
--rarity-epic:   #9C27B0
--rarity-legendary: #FF9800
```

**Typo :** Georgia serif pour titres/noms — monospace pour chiffres/stats — sans-serif dense pour labels UI

---

## LAYOUT (4 zones fixes)

```
┌─────────────────────────────────────────────────┐
│ TOPBAR : avatar + nom + niveau + XP + ressources │
├──────────┬──────────────────────┬────────────────┤
│ SIDEBAR  │   ZONE CENTRALE      │ PANNEAU DROIT  │
│ gauche   │   (vue active)       │ session stats  │
│ 180px    │   flexible           │ 200px          │
├──────────┴──────────────────────┴────────────────┤
│ BARRE PERSOS BAS : 6 personnages cliquables      │
└─────────────────────────────────────────────────┘
```

**Topbar :** logo + avatar emoji + nom + badge Niv + barre XP + 4 compteurs (Kamas ⚜️ / Frags Magiques 🔮 / Frags Bois 🪵 / Frags Monstres 💀)

**Sidebar :** Navigation (Accueil / Personnages / Combat / Havre Monde) + sous-menu Havre + zones Exploration avec niveaux requis + zones verrouillées grisées

**Panneau droit :** Stats session (combats, monstres, XP, kamas, drops) + 5 derniers drops colorés par rareté

---

## TUTORIEL (première ouverture)

Overlay plein écran, narrateur ANKAMA (dieu bienveillant ✨), parchemin animé.

| Étape | Contenu |
|---|---|
| 0 | Écran titre : particules dorées CSS + titre Georgia + bouton "Commencer" |
| 1 | Saisie nom du Havre Monde (min 2 caractères) |
| 2 | Choix classe parmi 12 (grille 3×4, cartes avec stats) |
| 3 | Saisie nom du personnage |
| 4 | Explication idle + bouton "Lancer le farming" → démarre loop |

---

## 12 CLASSES JOUABLES

| Classe | Emoji | Tagline | Stats | Couleur |
|---|---|---|---|---|
| IOP | 💪 | Le Guerrier sans peur | FOR/VIT | rouge |
| CRÂ | 🏹 | L'Archer infaillible | AGI/INT | vert |
| ENUTROF | 💰 | L'Avare chanceux | CHA/SAG | jaune |
| SRAM | 🗡️ | Le Voleur des Ombres | AGI/INT | violet |
| XÉLOR | ⏰ | Le Maître du Temps | INT/SAG | bleu foncé |
| ECAFLIP | 🃏 | Le Joueur Imprévisible | CHA/FOR | orange |
| OSAMODAS | 🐉 | Le Dompteur | INT/VIT | vert foncé |
| SADIDA | 🌿 | L'Enfant de la Nature | SAG/INT | vert clair |
| FÉCA | 🛡️ | Le Bouclier des Dieux | FOR/VIT | gris bleu |
| PANDAWA | 🍶 | Le Moine Ivre | FOR/CHA | doré |
| ROUBLARD | 💣 | L'Artificier | AGI/CHA | marron |
| STEAMER | ⚙️ | L'Ingénieur | INT/AGI | acier |

---

## DONNÉES V0.1

### Zone 1 — Champs d'Astrub (Niv 1-10, zone par défaut)

| Monstre | Niv | PV | XP | Kamas | Drops notables |
|---|---|---|---|---|---|
| Tofu | 1 | 25 | 6 | 4 | Plumes 14.1%, Oeuf 9.9%, Sandales 0.92% |
| Moskito | 2 | 20 | 4 | 2 | Aile 20%, Dard 5% |
| Pissenlit Diabolique | 3 | 45 | 15 | 6 | Fleur 10.8%, Langue 3.7% |
| Bouftou | 4 | 83 | 30 | 14 | Laine 8%, Coiffe 4%, Amulette 1% |
| Champ Champ | 5 | 130 | 35 | 8 | Pétale 15%, Graine 8% |

### Zone 2 — Forêt d'Astrub (Niv 10-20, débloquée niv 10)

| Monstre | Niv | PV | XP | Kamas | Drops notables |
|---|---|---|---|---|---|
| Larve Verte | 11 | 150 | 55 | 20 | Carapace 18%, Oeil 4% |
| Sanglier des Bois | 12 | 180 | 65 | 25 | Défense 12%, Cuir 8% |
| Loup | 14 | 220 | 80 | 30 | Croc 10%, Anneau 0.8% |
| Rose Démoniaque | 15 | 260 | 90 | 35 | Pétale Démoniaque 15%, Épine 7% |

### Donjon 1 — Donjon des Bouftous
- Zone : Champs d'Astrub | Niv recommandé : 25 | Salles : 8
- Clef : drop sur Bouftous (taux 0.5%)
- Boss salle 8 : Bouftou Royal (800PV, soigne alliés)
- Drops boss : Coiffe du Bouftou Royal 8%, Laine BR 30%, Cuisse BR 5%
- Récompense : Chacha (familier cosmétique)
- XP boss : ×5 | Kamas boss : ×8

### Donjon 2 — Donjon d'Incarnam
- Zone : Incarnam (grisée en V0.1) | Niv recommandé : 10 | Salles : 4
- Boss : Milimilou (250PV, boost PM alliés)
- Drops boss : Queue de Milimilou 99%, Floude chapeau 5%

---

## FORMULES & MÉCANIQUE

### Courbe XP
```js
xp_requis = Math.floor(100 * Math.pow(niveau, 1.6))
// Niv 1→2 : 100 XP | Niv 10 : 630 XP | Niv 30 : 4000 XP | Niv 100 : PRESTIGE
```

### Dégâts
```js
degats_base = Math.floor(stat_principale * 0.8 + Math.random() * stat_principale * 0.4)
degats_final = degats_base + bonus_equipement + bonus_prestige
hp_monstre   = hp_base_zone * (1 + niveau_monstre * 0.15)
```

### Tick (toutes les 2 secondes)
1. Calcul dégâts joueur (avec multiplicateurs actifs)
2. Réduction HP monstre
3. Si monstre mort → XP + Kamas + roll drops + next monstre
4. Dégâts monstre en retour
5. Si HP joueur = 0 → "💀 Défaite" → countdown 30s → reprendre salle 1
6. Ajout ligne journal (max 100, FIFO)
7. Auto-save si 30s écoulées

### Calcul hors-ligne
```js
temps_absent  = (Date.now() - lastSaveTime) / 1000
temps_effectif = Math.min(temps_absent, 8 * 3600)  // plafond 8h
gains = gains_par_seconde() * temps_effectif * 0.7  // malus 30%
```

---

## BÂTIMENTS HAVRE MONDE (V0.1 — 6 bâtiments)

| Bâtiment | Tag | Niv actuel | Effet | Prochaine amélioration |
|---|---|---|---|---|
| Fontaine de l'Almanax | ESSENTIEL | 3 | +30% XP combat | Niv 4 : +40% — 54 000K + 64 FragMag + 98 FragBois |
| Bibliothèque | ESSENTIEL | 4 | +20% XP globale | Niv 5 : +25% — 58 593K + 334 FragBois + 52 FragMag — 12m30 |
| Auberge | ESSENTIEL | 4 | Régén 30% PV/tick | Niv 5 : 35% — 18 740K + 417 FragBois + 125 FragMonstre — 12m30 |
| Zaap | ESSENTIEL | 2 | Change zone sans pénalité | Niv 3 : bonus changement |
| Banque | AFFAIRES | 7 | +8.39 kamas/sec | Niv 8 : +12.42 kamas/sec |
| Hôtel des Ventes | AFFAIRES | 3 | Vente 65% valeur | Niv 4 : 70% valeur |

---

## SYSTÈME PRESTIGE

**Débloqué :** Niveau 100
**Reset :** niveau → 1, XP → 0, équipements perdus
**Conservé :** kamas (50%), havre monde, donjons, succès

| Palier | Bonus | Titre |
|---|---|---|
| P1 | +10% XP globale | Aventurier Aguerri |
| P2 | +10% drop rate | Chasseur de Drops |
| P3 | +15% kamas | Marchand Prospère |
| P4 | +10% XP + débloque Forêt Maléfique | — |
| P5 | +20% dégâts + skin doré sidebar | Guerrier Émérite |
| P6 | +15% drop rate + donjon exclusif | — |
| P7 | +25% kamas + slot perso supplémentaire | — |
| P8 | +20% XP | Maître des Douze |
| P9 | +30% dégâts + zones Niv 50+ | — |
| P10 | ×2 tous les gains + débloque INCARNATION | — |

**Incarnation (après P10 + Niv 200) :**
- INC1 : ×2.0 gains + particules dorées UI
- INC2 : ×2.5 gains + contenu exclusif
- INC3+ : progression infinie

---

## STRUCTURE SAUVEGARDE localStorage

**Clé :** `dofus_idle_save`
**Sauvegarde :** automatique 30s + chaque action importante

```json
{
  "version": "0.1",
  "havreMondeName": "string",
  "playerName": "string",
  "playerClass": "string",
  "level": 1,
  "xp": 0,
  "prestige": 0,
  "incarnation": 0,
  "prestigeBonus": { "xpMult": 1, "dropMult": 1, "kamasMult": 1, "damageMult": 1 },
  "kamas": 0,
  "fragMagique": 0,
  "fragBois": 0,
  "fragMonstre": 0,
  "currentZone": "champs_astrub",
  "currentDungeon": null,
  "currentSalle": 1,
  "currentHP": 100,
  "maxHP": 100,
  "lastSaveTime": 0,
  "characters": [],
  "buildings": {
    "almanax":  { "level": 1, "upgrading": false, "upgradeEnd": null },
    "biblio":   { "level": 1, "upgrading": false, "upgradeEnd": null },
    "auberge":  { "level": 1, "upgrading": false, "upgradeEnd": null },
    "zaap":     { "level": 1, "upgrading": false, "upgradeEnd": null },
    "banque":   { "level": 1, "upgrading": false, "upgradeEnd": null },
    "hdv":      { "level": 1, "upgrading": false, "upgradeEnd": null }
  },
  "sessionStats": { "combats": 0, "monstres": 0, "xp": 0, "kamas": 0, "drops": 0 },
  "recentDrops": [],
  "inventory": [],
  "tutorialDone": false,
  "unlockedZones": ["champs_astrub"],
  "prestigeHistory": []
}
```

---

## ANIMATIONS CSS (keyframes requis)

| Nom | Usage |
|---|---|
| `pulse` | Bordure orange clignotante sur monstre ciblé |
| `shimmer` | Effet brillant sur items légendaires |
| `particles` | Points lumineux dorés écran titre tutoriel |
| `bar-fill` | Remplissage progressif barres HP/XP |
| `notification` | Apparition/disparition popup gains hors-ligne |
| `fadeIn` | Transitions douces entre vues |
| `scrollLog` | Défilement smooth journal de combat |

---

## RESPONSIVE

- **PC (>768px) :** layout 3 colonnes complet
- **Mobile (<768px) :** sidebar masquée par défaut + bouton hamburger ☰ — barre persos bas en scroll horizontal

---

## CONTRAINTES TECHNIQUES STRICTES

```
✅ React JSX — 1 seul fichier complet
✅ Hooks autorisés : useState, useEffect, useCallback, useReducer, useRef
✅ Seule lib externe : lucide-react
✅ Pas de CSS externe — style inline objects + keyframes dans <style>
✅ Police Georgia pour titres | monospace pour chiffres
✅ Export default : composant nommé DofusIdle
✅ Générer le code INTÉGRALEMENT — aucun raccourci ni "// reste du code"
```

---

## JOURNAL DE COMBAT — FORMAT DES LIGNES

```
Couleur #4a8c3f → "→ [NomJoueur] lance [Sort] sur [Monstre] (-42 PV)"
Couleur #c0392b → "← [Monstre] attaque [NomJoueur] (-18 PV)"
Couleur #c4922a → "★ [Monstre] vaincu ! +85 XP +12 Kamas"
Couleur #9C27B0 → "💎 Drop : [Nom item] [Rareté]"
Couleur #f0d090 → "═══ Salle 4/8 ═══"
```

Max 100 lignes en mémoire (FIFO). Auto-scroll vers le bas.

---

## PROBLÈMES CONNUS / POINTS DE VIGILANCE

> À compléter au fur et à mesure des sessions

- [ ] Vérifier que le calcul offline ne génère pas de gains négatifs si `lastSaveTime = 0`
- [ ] S'assurer que le tutoriel ne se relance pas si `tutorialDone: true` en localStorage
- [ ] Mobile : vérifier que la barre de persos bas ne casse pas le layout sur iPhone SE (375px)
- [ ] Le FIFO inventaire doit purger AVANT d'écrire en localStorage pour éviter quota dépassé

---

## RÉPARTITION IA — QUI FAIT QUOI

| Tâche | IA recommandée |
|---|---|
| Cadrage, idées, coaching, revue architecture | **Claude** |
| Génération du composant React complet | **ChatGPT 4o free** ou **Gemini** |
| Suivi de continuité entre sessions | **Gemini** (contexte 1M tokens) |
| CSS boilerplate, renommage, commentaires | **LM Studio 8B (local)** |
| Debug logique complexe | **Claude** ou **ChatGPT** |

---

## PROMPT DE SESSION — À COLLER SELON L'IA

### Pour ChatGPT / Gemini (génération de code)

```
Tu es un expert développeur de jeux idle/RPG.
Je développe un idle game inspiré de Dofus Rétro en React JSX (1 fichier).
Je ne suis pas développeur — tu génères le code, je valide.

CONTEXTE COMPLET DU PROJET :
[COLLER LE CONTENU DE CE FICHIER PROJET.md]

CONTRAINTES STRICTES :
- React JSX, 1 fichier complet, export default DofusIdle
- Hooks : useState, useEffect, useCallback, useReducer, useRef
- Seule lib externe : lucide-react
- CSS inline style objects + keyframes dans <style>
- Code intégral sans raccourcis ni "// ... reste du code"
- Commence par les keyframes CSS, puis le composant complet

MA DEMANDE DU JOUR :
[DÉCRIRE PRÉCISÉMENT CE QUE TU VEUX GÉNÉRER OU CORRIGER]
```

### Pour Claude (coaching, architecture, revue)

```
Tu es mon expert en développement de jeux idle et en coaching projet.
Contexte : projet Dofus Idle Rétro, React JSX, 1 fichier, localStorage.
Je ne code pas — tu guides, tu architectures, tu valides.

ÉTAT DU PROJET :
[COLLER LE CONTENU DE CE FICHIER PROJET.md]

Tu travailles par étapes courtes. Avant chaque action :
tu confirmes ce que tu vas faire et pourquoi.
Tu poses UNE seule question à la fois.
Après chaque session, tu me fournis la mise à jour du PROJET.md.

MA DEMANDE :
[DÉCRIRE CE QUE TU VEUX DÉCIDER OU REVOIR]
```

### Pour Gemini (suivi de continuité)

```
Tu es le gestionnaire de continuité du projet Dofus Idle Rétro.
Tu maintiens l'état du projet, tu prépares les sessions, tu poses les bonnes questions.
Tu ne génères pas de code complexe.

PROJET COMPLET :
[COLLER LE CONTENU DE CE FICHIER PROJET.md]

À chaque session :
1. Brief 5 lignes sur l'état actuel
2. Prochaine étape recommandée
3. Prompt de session prêt à coller dans ChatGPT ou Claude
4. UNE seule question pour avancer

MA DEMANDE :
[DÉCRIRE CE QUE TU VEUX FAIRE OU SAVOIR]
```

---

## PROCHAINES ÉTAPES (dans l'ordre)

- [ ] **ÉTAPE 1 :** Créer le repo GitHub et y déposer ce PROJET.md
- [ ] **ÉTAPE 2 :** Générer le composant React V0.1 complet (via ChatGPT/Gemini)
- [ ] **ÉTAPE 3 :** Tester dans Claude artifact — valider les 4 vues
- [ ] **ÉTAPE 4 :** Corriger les bugs visuels et de logique (avec Claude)
- [ ] **ÉTAPE 5 :** Valider le tutoriel complet + sauvegarde localStorage
- [ ] **ÉTAPE 6 :** Passer à V0.2 — personnages multiples + équipements

---

*Dernière mise à jour : Mai 2026 | Auteur : [TON NOM] | IA partenaire : Claude*
