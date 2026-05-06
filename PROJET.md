# PROJET.md — Dofus Idle Rétro
> Document vivant. Mis à jour à chaque session. Version : 0.1 — Mai 2026
> Repo : https://github.com/Jechtlarsson/dofus-idle

---

## STATUT ACTUEL

| Élément | État |
|---|---|
| Phase | 🟡 Spécification complète — En attente de génération V0.1 |
| Dernière session | Mai 2026 — Setup VS Code + Claude Code + workflow IA |
| Prochaine étape | Générer DofusIdle.jsx V0.1 via Claude Code |
| Stack | React JSX — 1 fichier — localStorage |
| Repo GitHub | https://github.com/Jechtlarsson/dofus-idle |

---

## ENVIRONNEMENT DE TRAVAIL

### Outils installés
| Outil | Rôle | Statut |
|---|---|---|
| VS Code | Éditeur principal | ✅ Installé |
| Git | Versioning | ✅ Installé |
| GitHub | Hébergement code | ✅ Repo créé |
| Claude Code (VS Code) | IA modifie les fichiers directement | ✅ À configurer |
| Live Server | Tester le jeu dans le navigateur | ✅ Extension installée |
| Prettier | Formatage code auto | ✅ Extension installée |
| GitHub Copilot | Autocomplétion IA dans VS Code | ✅ Extension installée |
| LM Studio 8B | Tâches locales (CSS, boilerplate) | ✅ Disponible |

### Répartition IA par tâche
| Tâche | IA | Méthode |
|---|---|---|
| Génération code + modification fichiers directs | **Claude Code** (terminal VS Code) | `claude` dans le terminal |
| Cadrage, architecture, coaching | **Claude** (claude.ai) | Chat web — coller PROJET.md |
| Suivi continuité entre sessions | **Gemini** (gemini.google.com) | Chat web — coller PROJET.md |
| Code répétitif, CSS, commentaires | **LM Studio 8B** | Local, 0 token cloud |
| Autocomplétion inline dans VS Code | **GitHub Copilot** | Intégré VS Code |

---

## WORKFLOW QUOTIDIEN

### Démarrer une session de travail
```bash
# 1. Ouvrir VS Code dans le dossier du projet
cd Documents/projets/dofus-idle

# 2. Lancer Claude Code dans le terminal intégré (Ctrl+ù)
claude

# 3. Décrire ce que tu veux — exemple :
"Lis le PROJET.md et génère le composant DofusIdle.jsx 
selon les specs. Sauvegarde le fichier et mets à jour 
le statut dans PROJET.md."
```

### Sauvegarder sur GitHub après chaque avancée
```bash
git add .
git commit -m "Description courte de ce qui a changé"
git push
```

### Tester le jeu
Clic droit sur `index.html` → "Open with Live Server"
Le navigateur se recharge automatiquement à chaque sauvegarde.

---

## STRUCTURE DES FICHIERS DU PROJET

```
dofus-idle/
├── PROJET.md              ← Ce fichier — état vivant du projet
├── README.md              ← Description publique du repo
├── index.html             ← Point d'entrée (charge le composant React)
├── DofusIdle.jsx          ← Composant principal (tout le jeu en 1 fichier)
├── saves/                 ← Sauvegardes exportées (JSON)
└── assets/                ← Images, sons (versions futures)
```

---

## PROMPTS DE SESSION PAR IA

### Claude Code (terminal VS Code) — génération et modification directe
```
Lis PROJET.md pour avoir le contexte complet du projet.

CONTEXTE : Jeu idle Dofus Rétro — React JSX 1 fichier — localStorage
Je ne code pas, tu génères et tu modifies directement les fichiers.

RÈGLES :
- Avant d'agir : dis-moi CE que tu vas faire et POURQUOI (1-2 lignes)
- Tu travailles par étapes courtes et validées
- Après chaque modification : mets à jour STATUT et CHANGELOG dans PROJET.md
- Code intégral sans raccourcis ni "// reste du code"
- Commit avec un message clair après chaque étape validée

MA DEMANDE :
[DÉCRIRE CE QUE TU VEUX FAIRE]
```

### Claude chat (claude.ai) — coaching et architecture
```
Tu es mon expert en développement de jeux idle et en coaching projet.
Je ne code pas — tu guides, tu architectures, tu valides.

ÉTAT DU PROJET :
[COLLER LE CONTENU DE PROJET.md]

Tu travailles par étapes courtes. Avant chaque action : confirme ce que 
tu vas faire et pourquoi. Tu poses UNE seule question à la fois.

MA DEMANDE :
[DÉCRIRE CE QUE TU VEUX DÉCIDER OU REVOIR]
```

### Gemini (gemini.google.com) — suivi de continuité
```
Tu es le gestionnaire de continuité du projet Dofus Idle Rétro.
Tu maintiens l'état, tu prépares les sessions, tu ne génères pas de code complexe.

PROJET COMPLET :
[COLLER LE CONTENU DE PROJET.md]

À chaque session :
1. Brief 5 lignes sur l'état actuel
2. Prochaine étape recommandée
3. Prompt prêt à coller dans Claude Code ou Claude chat
4. UNE seule question pour avancer

MA DEMANDE :
[DÉCRIRE CE QUE TU VEUX FAIRE OU SAVOIR]
```

---

## RÉSUMÉ DU PROJET

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
--bg-primary:    #1a1208
--bg-secondary:  #2d1f0a
--bg-panel:      #3d2b0e
--border-gold:   #8B6914
--border-light:  #c4922a
--accent-orange: #e8820c
--accent-green:  #4a8c3f
--text-primary:  #f0d090
--text-secondary:#c4922a
--text-muted:    #7a6040
--hp-bar:        #c0392b
--xp-bar:        #27ae60
--rarity-common: #9b9b9b
--rarity-rare:   #2196F3
--rarity-epic:   #9C27B0
--rarity-legendary: #FF9800
```

**Typo :** Georgia serif pour titres/noms — monospace pour chiffres/stats

---

## LAYOUT (4 zones fixes)

```
┌─────────────────────────────────────────────────┐
│ TOPBAR : avatar + nom + niveau + XP + ressources │
├──────────┬──────────────────────┬────────────────┤
│ SIDEBAR  │   ZONE CENTRALE      │ PANNEAU DROIT  │
│ 180px    │   flexible           │ 200px          │
├──────────┴──────────────────────┴────────────────┤
│ BARRE PERSOS BAS : 6 personnages cliquables      │
└─────────────────────────────────────────────────┘
```

---

## TUTORIEL (première ouverture)

Overlay plein écran, narrateur ANKAMA ✨, parchemin animé.

| Étape | Contenu |
|---|---|
| 0 | Écran titre : particules dorées CSS + bouton "Commencer" |
| 1 | Saisie nom du Havre Monde (min 2 caractères) |
| 2 | Choix classe parmi 12 (grille 3×4) |
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

### Zone 1 — Champs d'Astrub (Niv 1-10, défaut)

| Monstre | Niv | PV | XP | Kamas | Drops notables |
|---|---|---|---|---|---|
| Tofu | 1 | 25 | 6 | 4 | Plumes 14.1%, Sandales 0.92% |
| Moskito | 2 | 20 | 4 | 2 | Aile 20%, Dard 5% |
| Pissenlit Diabolique | 3 | 45 | 15 | 6 | Fleur 10.8%, Langue 3.7% |
| Bouftou | 4 | 83 | 30 | 14 | Laine 8%, Coiffe 4%, Amulette 1% |
| Champ Champ | 5 | 130 | 35 | 8 | Pétale 15%, Graine 8% |

### Zone 2 — Forêt d'Astrub (Niv 10-20)

| Monstre | Niv | PV | XP | Kamas | Drops notables |
|---|---|---|---|---|---|
| Larve Verte | 11 | 150 | 55 | 20 | Carapace 18%, Oeil 4% |
| Sanglier des Bois | 12 | 180 | 65 | 25 | Défense 12%, Cuir 8% |
| Loup | 14 | 220 | 80 | 30 | Croc 10%, Anneau 0.8% |
| Rose Démoniaque | 15 | 260 | 90 | 35 | Pétale Démoniaque 15%, Épine 7% |

### Donjon 1 — Donjon des Bouftous
- Niv recommandé : 25 | Salles : 8 | Boss : Bouftou Royal (800PV)
- Clef : drop Bouftous 0.5% | Récompense : Chacha (familier)
- XP boss ×5 | Kamas boss ×8

### Donjon 2 — Donjon d'Incarnam
- Niv recommandé : 10 | Salles : 4 | Boss : Milimilou (250PV)
- Drops boss : Queue 99%, Floude chapeau 5%

---

## FORMULES & MÉCANIQUE

```js
// Courbe XP
xp_requis = Math.floor(100 * Math.pow(niveau, 1.6))

// Dégâts
degats_base = Math.floor(stat_principale * 0.8 + Math.random() * stat_principale * 0.4)
degats_final = degats_base + bonus_equipement + bonus_prestige
hp_monstre   = hp_base_zone * (1 + niveau_monstre * 0.15)

// Hors-ligne
temps_effectif = Math.min((Date.now() - lastSaveTime) / 1000, 8 * 3600)
gains = gains_par_seconde() * temps_effectif * 0.7
```

**Tick :** toutes les 2 secondes — dégâts joueur → mort monstre → XP/Kamas/drops → dégâts retour → mort joueur → countdown 30s → reprise salle 1

---

## BÂTIMENTS HAVRE MONDE (V0.1)

| Bâtiment | Tag | Effet actuel | Prochain niveau |
|---|---|---|---|
| Fontaine de l'Almanax | ESSENTIEL | Niv 3 : +30% XP combat | Niv 4 : +40% — 54 000K + 64 FragMag + 98 FragBois |
| Bibliothèque | ESSENTIEL | Niv 4 : +20% XP globale | Niv 5 : +25% — 58 593K + 334 FragBois — 12m30 |
| Auberge | ESSENTIEL | Niv 4 : Régén 30% PV/tick | Niv 5 : 35% — 18 740K + 417 FragBois — 12m30 |
| Zaap | ESSENTIEL | Niv 2 : change zone sans pénalité | Niv 3 : bonus |
| Banque | AFFAIRES | Niv 7 : +8.39 kamas/sec | Niv 8 : +12.42 kamas/sec |
| Hôtel des Ventes | AFFAIRES | Niv 3 : vente 65% valeur | Niv 4 : 70% valeur |

---

## SYSTÈME PRESTIGE

**Débloqué :** Niveau 100 | **Reset :** niv + XP + équipements | **Conservé :** kamas 50%, havre monde, succès

| Palier | Bonus | Titre |
|---|---|---|
| P1 | +10% XP globale | Aventurier Aguerri |
| P2 | +10% drop rate | Chasseur de Drops |
| P3 | +15% kamas | Marchand Prospère |
| P4 | +10% XP + Forêt Maléfique | — |
| P5 | +20% dégâts + skin doré | Guerrier Émérite |
| P6 | +15% drop rate + donjon exclusif | — |
| P7 | +25% kamas + slot perso | — |
| P8 | +20% XP | Maître des Douze |
| P9 | +30% dégâts + zones Niv 50+ | — |
| P10 | ×2 tous les gains + INCARNATION | — |

**Incarnation (P10 + Niv 200) :** INC1 ×2.0 → INC2 ×2.5 → INC3+ infini

---

## SAUVEGARDE localStorage

**Clé :** `dofus_idle_save` | **Auto-save :** 30s + actions importantes

```json
{
  "version": "0.1",
  "havreMondeName": "string",
  "playerName": "string",
  "playerClass": "string",
  "level": 1, "xp": 0, "prestige": 0, "incarnation": 0,
  "prestigeBonus": { "xpMult": 1, "dropMult": 1, "kamasMult": 1, "damageMult": 1 },
  "kamas": 0, "fragMagique": 0, "fragBois": 0, "fragMonstre": 0,
  "currentZone": "champs_astrub", "currentDungeon": null, "currentSalle": 1,
  "currentHP": 100, "maxHP": 100, "lastSaveTime": 0,
  "buildings": {
    "almanax":  { "level": 1, "upgrading": false, "upgradeEnd": null },
    "biblio":   { "level": 1, "upgrading": false, "upgradeEnd": null },
    "auberge":  { "level": 1, "upgrading": false, "upgradeEnd": null },
    "zaap":     { "level": 1, "upgrading": false, "upgradeEnd": null },
    "banque":   { "level": 1, "upgrading": false, "upgradeEnd": null },
    "hdv":      { "level": 1, "upgrading": false, "upgradeEnd": null }
  },
  "sessionStats": { "combats": 0, "monstres": 0, "xp": 0, "kamas": 0, "drops": 0 },
  "recentDrops": [], "inventory": [],
  "tutorialDone": false,
  "unlockedZones": ["champs_astrub"],
  "prestigeHistory": [], "characters": []
}
```

---

## ANIMATIONS CSS REQUISES

| Keyframe | Usage |
|---|---|
| `pulse` | Bordure orange clignotante sur monstre ciblé |
| `shimmer` | Effet brillant items légendaires |
| `particles` | Points dorés écran titre tutoriel |
| `bar-fill` | Remplissage barres HP/XP |
| `notification` | Popup gains hors-ligne |
| `fadeIn` | Transitions entre vues |

---

## CONTRAINTES TECHNIQUES

```
✅ React JSX — 1 seul fichier complet
✅ Hooks : useState, useEffect, useCallback, useReducer, useRef
✅ Seule lib externe : lucide-react
✅ CSS inline style objects + keyframes dans <style>
✅ Georgia pour titres | monospace pour chiffres
✅ Export default : composant nommé DofusIdle
✅ Code INTÉGRAL — aucun raccourci ni "// reste du code"
✅ Responsive : 3 colonnes PC | sidebar hamburger mobile
✅ Journal combat : FIFO 100 lignes | Inventaire : FIFO 50 items
```

---

## PROBLÈMES CONNUS / VIGILANCE

- [ ] Si `lastSaveTime = 0` au premier lancement → ne pas calculer gains offline
- [ ] Tutoriel ne doit pas se relancer si `tutorialDone: true` en localStorage
- [ ] Mobile 375px (iPhone SE) : vérifier barre persos bas
- [ ] FIFO inventaire : purger AVANT d'écrire en localStorage (quota 5MB)

---

## PROCHAINES ÉTAPES

- [x] Repo GitHub créé
- [x] VS Code + Git + extensions installés
- [x] Claude Code installé
- [x] **ÉTAPE 1** : Déposer ce PROJET.md sur GitHub (remplacer l'ancien)
- [ ] **ÉTAPE 2** : Générer DofusIdle.jsx V0.1 via Claude Code
- [ ] **ÉTAPE 3** : Tester avec Live Server — valider les 4 vues
- [ ] **ÉTAPE 4** : Corriger bugs + valider tutoriel + localStorage
- [ ] **ÉTAPE 5** : V0.2 — personnages multiples + équipements

---

*Dernière mise à jour : Mai 2026 | Repo : https://github.com/Jechtlarsson/dofus-idle*
