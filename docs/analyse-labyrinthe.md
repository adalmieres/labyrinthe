# **Analyse Complète du Jeu de Plateau *Labyrinthe* (Ravensburger)**
*Guide pour le développement d'une application d'aide à la décision*

---

---

## **📜 Sommaire**
1. **[Règles du jeu](#-règles-du-jeu)**
2. **[Particularités du plateau](#-particularités-du-plateau)**
3. **[Types de pièces et objets spéciaux](#-types-de-pièces-et-objets-spéciaux)**
4. **[Logique algorithmique pour l'aide à la décision](#-logique-algorithmique-pour-laide-à-la-décision)**

---

---

---

## **🎮 1. Règles du jeu**

### **📌 Concept général**
- **Créateur** : Max J. Kobbert (1986)
- **Éditeur** : Ravensburger
- **Public** : 2 à 4 joueurs (à partir de 7 ans)
- **Durée** : ~20 minutes par partie
- **But** :
  Chaque joueur doit **trouver tous ses trésors** (représentés par des cartes) dans le labyrinthe **en déplaçant son pion** vers les tuiles correspondantes, puis **revenir à sa case de départ**.
  Le premier à accomplir cela remporte la partie.

---

### **📦 Contenu du jeu**
| Élément | Quantité | Description |
|---------|----------|-------------|
| **Plateau de jeu** | 1 | Grille de **49 cases** (7×7) avec des emplacements pour tuiles fixes et mobiles. |
| **Tuiles "Couloir"** | 34 | Tuiles **mobiles** représentant des chemins (murs et passages). |
| **Tuiles fixes** | 16 ou 15 | **Intégrées au plateau**, ne bougent **jamais** pendant la partie. |
| **Cartes Trésor** | 24 | Chaque joueur en reçoit **6** (ou moins selon le nombre de joueurs). Elles indiquent les **objets à trouver** dans le labyrinthe. |
| **Pions** | 4 | Un par joueur (couleurs : bleu, rouge, jaune, vert). |
| **Tuile supplémentaire** | 1 | Utilisée pour **faire coulisser** les rangées/colonnes du plateau. **Peut être tournée dans 4 orientations avant insertion.** |

---

### **🔄 Déroulement d’un tour**
1. **Déplacer une rangée ou une colonne** :
   - Le joueur **choisit une rangée ou une colonne** (3 rangées mobiles + 3 colonnes mobiles = **6 options**).
   - Il **insère la tuile supplémentaire** d’un côté (2 options : haut/bas pour une colonne, gauche/droite pour une rangée).
   - **La tuile supplémentaire peut être tournée** dans l’une des **4 orientations possibles** (0°, 90°, 180°, 270°) **avant insertion**.
     → **Total : 6 × 2 × 4 = 48 actions possibles** par tour.
   - Cela **pousse toutes les tuiles** de cette rangée/colonne **d’un cran**, et **expulse une tuile** de l’autre côté.
   - La tuile expulsée devient la **nouvelle tuile supplémentaire** pour le tour suivant.

2. **Déplacer son pion** :
   - Après avoir modifié le plateau, le joueur peut **déplacer son pion** **aussi loin qu’il le souhaite** le long des **chemins ouverts** (sans traverser les murs).
   - **Règle importante** : Si la poussée expulse le pion du joueur, il **réapparaît sur la tuile insérée** et peut encore se déplacer pendant ce tour.

3. **Atteindre un trésor** :
   - Si le pion se trouve sur une tuile correspondant à **la carte Trésor du haut de sa pile**, le joueur **la retourne** (preuve de collecte).
   - Il peut alors **regarder la carte suivante** de sa pile pour connaître son prochain objectif.

4. **Fin de la partie** :
   - Le premier joueur à **trouver tous ses trésors** **ET** à **revenir à sa case de départ** gagne.

---

### **💡 Variantes et règles spécifiques**
- **Labyrinthe Junior** : Plateau 5×5, 2 lignes/colonnes mobiles (au lieu de 3). La tuile supplémentaire **ne peut pas être tournée** dans cette version.
- **Labyrinthe Master** : Introduction d’un **ordre imposé** pour la collecte des trésors + système de points.
- **Règle alternative** : Certains trésors peuvent être **découverts dans n’importe quel ordre** (selon les versions).
- **Interdiction** : On ne peut **pas annuler immédiatement** le mouvement du joueur précédent en repoussant la tuile qu’il vient d’insérer.

---

---

---

## **🧩 2. Particularités du plateau**

### **🔍 Structure du plateau**
- **Taille** : **7×7 cases** (49 emplacements).
- **Composition** :
  - **15 ou 16 tuiles fixes** (selon les versions) :
    - **Ne bougent jamais** pendant la partie.
    - **Positionnées aux coins et au centre** (ex. : les 4 coins pour les cases de départ, et d’autres réparties aléatoirement).
    - **Rôle** : Stabiliser le labyrinthe et éviter une reconfiguration totale à chaque tour.
  - **34 tuiles mobiles** :
    - **Insérées dans les emplacements restants** (33 sur le plateau + 1 tuile supplémentaire hors plateau).
    - **Organisées en 3 rangées et 3 colonnes mobiles** (les autres sont fixes ou partiellement fixes).
    - **Peut être déplacées** par insertion de la tuile supplémentaire.

---

### **🔄 Mécanisme de mouvement des tuiles**
| Action | Conséquence |
|--------|-------------|
| **Insérer une tuile** dans une rangée/colonne | Toutes les tuiles de cette rangée/colonne **glissent d’un cran**. |
| **Expulsion d’une tuile** | La tuile à l’extrémité opposée **sort du plateau** et devient la nouvelle tuile supplémentaire. |
| **Rotation de la tuile supplémentaire** | La tuile peut être **tournée dans 4 orientations** avant insertion pour aligner les passages. |
| **Effet sur le labyrinthe** | **Reconfiguration des chemins** : Les murs et passages changent, ouvrant ou fermant des voies. |

---

### **🎯 Implications stratégiques**
✅ **Avantages des tuiles fixes** :
- **Repères stables** : Les joueurs peuvent s’appuyer sur elles pour planifier leurs déplacements.
- **Points de départ/arrivée** : Les cases de départ (coins) sont fixes, ce qui permet de toujours savoir où revenir.

⚠️ **Défis des tuiles mobiles** :
- **Instabilité** : Un chemin ouvert peut **disparaître** au tour suivant.
- **Anticipation nécessaire** : Il faut **prévoir les mouvements adverses** qui peuvent bloquer un accès.
- **Effet domino** : Un seul déplacement peut **changer plusieurs chemins** simultanément.

✨ **Opportunité de la rotation** :
- La possibilité de **tourner la tuile supplémentaire** avant insertion permet de **créer des chemins stratégiques** ou de **bloquer les adversaires**.

---

---

---

## **💎 3. Types de pièces et objets spéciaux**

---

### **📌 Les tuiles "Couloir" (34 + 1 supplémentaire)**
Chaque tuile représente un **morceau de labyrinthe** vu du dessus, avec :
- **Murs** (lignes épaisses) : **Bloquent le passage**.
- **Passages** (espaces libres) : **Permettent de circuler**.
- **Formes possibles** :
  | Type | Description | Exemple visuel |
  |------|-------------|----------------|
  | **T** | 3 passages en forme de "T" | ```
    █
   ███
    █
  ``` |
  | **L** | 2 passages en angle (90°) | ```
   ██
    █
  ``` |
  | **I** | Passage droit (2 ouvertures opposées) | ```
   █
   █
   █
  ``` |
  | **⊞** | 4 passages (croisement) | ```
   ███
   █ █
   ███
  ``` |
  | **⊣** | 3 passages (en "Y") | Variantes selon les éditions. |
  | **Cul-de-sac** | 1 passage + 3 murs | ```
    █
   ██
  ``` |

> ⚠️ **Remarque** : Les tuiles **n’ont pas de symboles spéciaux** en dehors des murs/passages. Les **trésors sont représentés sur les tuiles fixes ou mobiles** sous forme d’**icônes** (ex. : couronne, épée, calice, etc.).

---

### **🎁 Les cartes Trésor (24 au total)**
- **24 cartes illustrées**, chacune représentant un **objet unique** (ex. : fantôme, dragon, coffre, clé, etc.).
- **Répartition** :
  - Chaque joueur reçoit **6 cartes** (pour 4 joueurs) ou **8 cartes** (pour 2-3 joueurs).
  - Les cartes sont **empilées face cachée** devant chaque joueur.
  - **Seule la première carte** de la pile est visible pour le joueur (son objectif actuel).

---

### **🏆 Objets spéciaux et symboles**
| Symbole | Type | Description |
|---------|------|-------------|
| **Couronne** | Trésor | Objectif à atteindre. |
| **Épée** | Trésor | Objectif à atteindre. |
| **Calice** | Trésor | Objectif à atteindre. |
| **Fantôme** | Trésor | Objectif à atteindre. |
| **Dragon** | Trésor | Objectif à atteindre. |
| **Clé** | Trésor | Objectif à atteindre. |
| **Potion** | Trésor | Objectif à atteindre. |
| **Livre** | Trésor | Objectif à atteindre. |
| **...** | Trésor | **24 symboles différents** (varie selon les éditions). |

> 💡 **Important** :
> - Les **trésors sont placés aléatoirement** sur les tuiles (fixes ou mobiles) **au début de la partie**.
> - Une tuile peut **ne pas avoir de trésor**, ou en avoir **un seul**.
> - **Pas de tuiles "pièges"** ou "spéciales" dans le jeu de base (contrairement à d’autres jeux comme *Carcassonne Labyrinth*).

---

---

---

## **🤖 4. Logique algorithmique pour l’aide à la décision**

---

### **🎯 Objectif de l’application**
Développer un **système d’aide** qui, à chaque tour, propose au joueur :
1. **Le meilleur coup possible** (quelle rangée/colonne déplacer, dans quelle direction, et avec quelle orientation de la tuile supplémentaire).
2. **Le chemin optimal** pour atteindre son trésor actuel **après le déplacement**.
3. **Une évaluation des risques** (ex. : "Ce mouvement ouvre un chemin pour l’adversaire vers son trésor").

---

---

### **🧠 Modélisation du problème**

#### **📊 Représentation du plateau**
- **Graphe dynamique** :
  - **Nœuds** = Cases du plateau (49).
  - **Arêtes** = Passages entre cases adjacentes (si pas de mur entre elles).
  - **Poids** : 1 (déplacement d’une case).
- **État du jeu** :
  - Position des **34 tuiles mobiles** + **1 tuile supplémentaire** (avec son orientation actuelle).
  - Position des **pions** (4 joueurs).
  - **Cartes Trésor** de chaque joueur (objectifs actuels).
  - **Tuiles fixes** (statiques).

---

#### **🔄 Dynamique du jeu**
À chaque tour :
1. Le joueur **choisit une rangée ou une colonne** (6 options : 3 rangées + 3 colonnes).
2. Il **insère la tuile supplémentaire** d’un côté (2 options : haut/bas pour une colonne, gauche/droite pour une rangée).
3. Il **tourne la tuile supplémentaire** dans l’une des **4 orientations possibles** (0°, 90°, 180°, 270°).
   → **Total : 6 × 2 × 4 = 48 actions possibles** par tour.
4. Le plateau est **reconfiguré** (tuiles glissent, une nouvelle tuile sort).
5. Le joueur **déplace son pion** (optionnel, mais souvent utile).

---

---

### **🔍 Algorithmes nécessaires**

#### **🔹 1. Calcul de chemin (Pathfinding)**
Pour évaluer un coup, il faut :
1. **Simuler le déplacement** de la rangée/colonne + la **rotation de la tuile supplémentaire**.
2. **Recalculer le graphe** du labyrinthe avec la nouvelle configuration.
3. **Trouver le chemin le plus court** entre :
   - La **position actuelle du pion** et **son trésor actuel**.
   - (Optionnel) La **position actuelle du pion** et **les trésors futurs** (anticipation).

**Algorithmes adaptés** :
| Algorithme | Avantages | Inconvénients | Complexité |
|------------|-----------|---------------|------------|
| **A*** | ✅ Optimal (trouve le chemin le plus court) <br> ✅ Efficace avec une bonne heuristique | ⚠️ Nécessite une heuristique adaptée | O(b^d) (b = facteur de branchement, d = profondeur) |
| **Dijkstra** | ✅ Garantit le chemin le plus court <br> ✅ Simple à implémenter | ⚠️ Moins efficace que A* pour les grands graphes | O((V + E) log V) |
| **BFS (Parcours en largeur)** | ✅ Simple <br> ✅ Garantit le chemin le plus court (si poids = 1) | ⚠️ Moins adapté pour les graphes pondérés | O(V + E) |
| **DFS (Parcours en profondeur)** | ✅ Simple | ❌ Ne garantit pas le chemin le plus court <br> ❌ Risque de boucles infinies | O(V + E) |

> **Recommandation** :
> Utiliser **A*** avec une **heuristique de Manhattan** (distance en lignes droites entre deux points, en ignorant les murs).
> **Pourquoi ?**
> - Le plateau est une grille **7×7** (petite taille).
> - A* est **optimal** et **rapide** pour cette échelle.
> - L’heuristique de Manhattan est **admissible** (ne surestime jamais la distance réelle).

---

#### **🔹 2. Évaluation des coups possibles**
Pour chaque **action possible** (48 au total) :
1. **Simuler le déplacement** de la rangée/colonne + **rotation de la tuile supplémentaire**.
2. **Recalculer le graphe** du labyrinthe.
3. **Calculer le chemin le plus court** vers le trésor actuel avec A*.
4. **Noter le coup** en fonction de :
   - **Longueur du chemin** (plus court = meilleur).
   - **Accessibilité** (le chemin existe-t-il ?).
   - **Risque pour les adversaires** (est-ce que ce mouvement **aide un adversaire** à atteindre son trésor ?).
   - **Stabilité** (le chemin reste-t-il ouvert au tour suivant ?).

---

#### **🔹 3. Anticipation des mouvements adverses**
Pour un **niveau avancé**, l’application peut :
1. **Simuler les 48 coups possibles pour chaque adversaire**.
2. **Évaluer si un coup** du joueur actuel **ouvre un chemin** pour un adversaire vers **son trésor**.
3. **Pénaliser les coups** qui **avantagent les adversaires**.

> **Exemple** :
> - Si le joueur A déplace une colonne avec une certaine orientation et que cela **crée un chemin direct** entre le pion du joueur B et son trésor, ce coup est **moins bon** pour A.

---

#### **🔹 4. Priorisation des objectifs**
Si le joueur a **plusieurs trésors à atteindre** :
1. **Calculer le chemin vers chaque trésor** (actuel et futurs).
2. **Choisir le trésor le plus proche** (stratégie "gloutonne").
3. **Ou** : **Anticiper les trésors futurs** pour éviter de bloquer son propre chemin.

---

---

### **📋 Pseudocode de l’algorithme principal**

```python
def meilleur_coup(etat_jeu):
    coups_possibles = generer_coups_possibles(etat_jeu)  # 48 actions (6 rangées/colonnes × 2 sens × 4 orientations)
    meilleur_coup = None
    meilleur_score = -infinité

    for coup in coups_possibles:
        # 1. Simuler le déplacement + rotation
        nouveau_plateau = simuler_deplacement_avec_rotation(etat_jeu, coup)

        # 2. Calculer le chemin vers le trésor actuel
        chemin = a_star(
            position=etat_jeu.pion_joueur,
            objectif=etat_jeu.tesor_actuel,
            graphe=nouveau_plateau
        )

        if chemin is None:
            score = -1000  # Pas de chemin possible
        else:
            # 3. Évaluer le coup
            score = evaluer_coup(
                longueur=len(chemin),
                risque_adversaire=calculer_risque_adversaire(nouveau_plateau, etat_jeu),
                stabilite=chemin_est_stable(nouveau_plateau)
            )

        # 4. Mettre à jour le meilleur coup
        if score > meilleur_score:
            meilleur_score = score
            meilleur_coup = coup

    return meilleur_coup
```

---

#### **🔹 5. Fonctions auxiliaires**
| Fonction | Description | Complexité |
|----------|-------------|------------|
| `generer_coups_possibles(etat)` | Génère les 48 actions (6 rangées/colonnes × 2 sens × 4 orientations). | O(1) |
| `simuler_deplacement_avec_rotation(etat, coup)` | Applique le déplacement + rotation et retourne le nouveau plateau. | O(1) (grille 7×7) |
| `a_star(depart, arrivee, graphe)` | Trouve le chemin le plus court avec A*. | O(b^d) (rapide pour 7×7) |
| `calculer_risque_adversaire(plateau, etat)` | Évalue si le coup aide un adversaire. | O(n) (n = nombre d’adversaires) |
| `evaluer_coup(longueur, risque, stabilite)` | Note le coup (ex. : `score = -longueur - 10*risque + stabilite`). | O(1) |

---

---

### **🎯 Optimisations possibles**
1. **Précalcul des graphes** :
   - Stocker le graphe du labyrinthe **sous forme de matrice d’adjacence** pour un accès rapide.
   - Mettre à jour **uniquement les arêtes modifiées** après un déplacement.

2. **Cache des chemins** :
   - Mémoriser les **chemins déjà calculés** pour éviter des recalculs inutiles.

3. **Heuristique améliorée** :
   - Utiliser **l’heuristique de Manhattan** (distance en x + distance en y).
   - **Exemple** :
     ```python
     def heuristique(a, b):
         return abs(a.x - b.x) + abs(a.y - b.y)
     ```

4. **Parallélisation** :
   - Évaluer les **48 coups possibles en parallèle** (si nécessaire pour optimiser les performances).

5. **Limitation de la profondeur** :
   - Pour l’anticipation des adversaires, limiter à **1 ou 2 tours à l’avance** (au-delà, le nombre de combinaisons devient trop élevé).

---

---

### **📊 Exemple concret**
**Situation** :
- Joueur **Rouge** : Pion en (0,0), trésor actuel en (4,3).
- Tuile supplémentaire : Tuile "L" (passage en haut et à droite).
- Plateau actuel : Configuration aléatoire.

**Actions possibles** (extrait) :
1. Déplacer **colonne 1** vers le **haut** (insérer la tuile en bas, **sans rotation**).
2. Déplacer **colonne 1** vers le **haut** (insérer la tuile en bas, **rotation 90°**).
3. Déplacer **colonne 1** vers le **haut** (insérer la tuile en bas, **rotation 180°**).
4. Déplacer **colonne 1** vers le **haut** (insérer la tuile en bas, **rotation 270°**).
5. Déplacer **colonne 1** vers le **bas** (insérer la tuile en haut, **sans rotation**).
...
48. Déplacer **rangée 3** vers la **droite** (insérer la tuile à gauche, **rotation 270°**).

**Évaluation** (pour quelques coups) :
| Coup | Orientation | Chemin vers trésor | Longueur | Risque adversaire | Score |
|------|-------------|---------------------|----------|--------------------|-------|
| Colonne 1 → Haut | 0° | Existe | 5 | Faible | **8** |
| Colonne 1 → Haut | 90° | Existe | 3 | Moyen | **10** |
| Colonne 1 → Bas | 0° | Existe | 7 | Élevé (aide Bleu) | 2 |
| Rangée 3 → Droite | 180° | Existe | 4 | Faible | **9** |

**Résultat** :
→ **Meilleur coup** : **Colonne 1 → Haut avec rotation 90°** (score = 10).

---

---

---

## **🎉 Conclusion**

---

### **🔹 Résumé des points clés**
| Aspect | Détails |
|--------|---------|
| **Règles** | Jeu de 1 à 4 joueurs, but : trouver ses trésors et revenir au départ. |
| **Plateau** | 7×7 cases : **15-16 tuiles fixes** + **34 tuiles mobiles** + 1 tuile supplémentaire. |
| **Tuiles** | Représentent des **chemins** (murs/passages) en formes variées (T, L, I, etc.). La **tuile supplémentaire peut être tournée** (4 orientations). |
| **Trésors** | 24 cartes, **6 par joueur**, symboles variés (couronne, épée, etc.). |
| **Algorithme** | **A*** pour le pathfinding + **évaluation des 48 coups possibles** (6 rangées/colonnes × 2 sens × 4 orientations). |
| **Optimisation** | Heuristique de Manhattan, cache des chemins, parallélisation si nécessaire. |

---

### **📚 Ressources utiles**
- **Règles officielles** :
  - [Règles du Labyrinthe (Ravensburger)](https://www.ravensburger.org/spielanleitungen/ecm/Spielanleitungen/26743%20anl%201%202362054.pdf)
  - [Wikipédia - Labyrinthe (jeu)](https://fr.wikipedia.org/wiki/Labyrinthe_(jeu))
- **Algorithmes** :
  - [A* (Wikipédia)](https://fr.wikipedia.org/wiki/Algorithme_A*)
  - [Pathfinding (Red Blob Games)](https://www.redblobgames.com/pathfinding/a-star/introduction.html)

---

---

**📌 Document rédigé par Vibe Code**
