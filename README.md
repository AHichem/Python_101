# Python 101 — Les bases pour commencer à coder (en 2 heures)

Un récap complet et pratique : **Python de base → fonctions & bibliothèques → NumPy → Pandas**, avec du code exécutable, des mini-exercices et leurs corrections.

## ⏱️ Planning de la session (2h)

| Créneau | Notebook | Contenu |
|---|---|---|
| 0:00 – 0:35 | [`01_bases_python.ipynb`](01_bases_python.ipynb) | variables, types, opérateurs, f-strings, **listes, tuples, dictionnaires, sets**, if/else, boucles, compréhensions |
| 0:35 – 0:55 | [`02_fonctions_bibliotheques.ipynb`](02_fonctions_bibliotheques.ipynb) | **fonctions**, lambda, **import de bibliothèques**, pip, try/except |
| 0:55 – 1:00 | ☕ | pause |
| 1:00 – 1:25 | [`03_numpy.ipynb`](03_numpy.ipynb) | arrays, shape, **sélection / slicing / filtres booléens**, stats, `axis`, broadcasting |
| 1:25 – 2:00 | [`04_pandas.ipynb`](04_pandas.ipynb) | Series, **DataFrame**, read_csv, exploration, **sélection (`[]`, `loc`, `iloc`, filtres)**, NaN, nouvelles colonnes, tri, **groupby**, pivot, merge |
| bonus | [`05_exercices.ipynb`](05_exercices.ipynb) | corrections de tous les mini-exercices + mini-projet final |

📄 **[`MEMO.md`](MEMO.md)** : la fiche mémo d'une page à garder ouverte à côté.

> Petite précision de vocabulaire : on dit un **tuple** (pas « tulipe » 🌷) — c'est une liste non modifiable, ex. `(3, 5)`.

## 🚀 Comment l'utiliser

**Option 1 – sans rien installer (le plus simple)** : ouvre un notebook dans [Google Colab](https://colab.research.google.com/) → *Fichier › Importer un notebook › GitHub* → colle l'URL de ce dépôt.
Pour le notebook Pandas, importe aussi le dossier `data/` (icône 📁 à gauche dans Colab).

**Option 2 – en local** :
```bash
git clone <url-de-ce-repo> && cd Python_101
pip install -r requirements.txt
jupyter lab        # ou : jupyter notebook
```

Dans un notebook : **Shift + Entrée** exécute une cellule. Les sorties sont déjà affichées, mais **ré-exécute et modifie** le code : c'est le plus efficace pour retenir.

## 📁 Contenu

```
├── 01_bases_python.ipynb
├── 02_fonctions_bibliotheques.ipynb
├── 03_numpy.ipynb
├── 04_pandas.ipynb
├── 05_exercices.ipynb        # corrections + mini-projet
├── MEMO.md                   # fiche mémo
├── data/
│   ├── ventes.csv            # 30 ventes fictives (avec quelques valeurs manquantes)
│   └── vendeurs.csv          # pour l'exemple de merge
└── requirements.txt
```
