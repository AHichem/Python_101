# 🧾 Fiche mémo Python / NumPy / Pandas

## Python de base
```python
# Variables & types
x = 10            # int
y = 3.14          # float
nom = "Hichem"    # str
ok = True         # bool
rien = None
type(x); int("5"); float("2.5"); str(10)

# Opérateurs
+  -  *  /  //(div. entière)  %(reste)  **(puissance)
== != < > <= >=   and or not   in

# f-string
f"{nom} a {x} ans, prix {y:.2f} €"
```

| Structure | Exemple | Modifiable | Accès |
|---|---|---|---|
| liste | `l = [1, 2, 3]` | ✅ | `l[0]`, `l[-1]`, `l[1:3]` |
| tuple | `t = (1, 2)` | ❌ | `t[0]`, `a, b = t` |
| dict | `d = {"a": 1}` | ✅ | `d["a"]`, `d.get("z", 0)` |
| set | `s = {1, 2}` | ✅ | `x in s` (pas d'index) |

```python
l.append(4); l.remove(2); l.pop(); len(l); sorted(l); sum(l); min(l); max(l)
d["b"] = 2; d.keys(); d.values(); d.items()
"a,b".split(","); "-".join(["a","b"]); s.upper(); s.strip(); s.replace("a","b")

# Slicing : [debut inclus : fin exclue : pas]
l[:3]   l[2:]   l[::-1]

# Conditions
if x > 10:
    ...
elif x > 5:
    ...
else:
    ...

# Boucles
for i in range(5): ...
for i, val in enumerate(l): ...
for k, v in d.items(): ...
for a, b in zip(l1, l2): ...
while cond: ...        # break / continue

# Compréhension
[x**2 for x in l if x > 0]
{k: v for k, v in d.items()}
```

## Fonctions, bibliothèques, erreurs
```python
def prix_ttc(ht, tva=0.2):
    """docstring"""
    return ht * (1 + tva)

carre = lambda x: x ** 2

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from math import sqrt
# installer : pip install numpy pandas   (notebook : !pip install ...)

try:
    ...
except ValueError as e:
    ...
```

## NumPy
```python
a = np.array([1, 2, 3])
np.zeros(3); np.ones((2, 3)); np.arange(0, 10, 2); np.linspace(0, 1, 5)
rng = np.random.default_rng(42); rng.integers(1, 7, 10); rng.normal(0, 1, 100)

a.shape  a.ndim  a.dtype  a.reshape(3, -1)  a.T
a * 2    a + b    a @ b                     # vectorisé, pas de boucle
a.sum()  a.mean()  a.std()  a.min()  a.argmax()  np.median(a)
m.sum(axis=0)   # par colonne      m.sum(axis=1)   # par ligne

m[0, 2]   m[:, 0]   m[1]   m[0:2, 1:3]      # [ligne, colonne]
a[a > 5]                                    # filtre booléen
a[(a > 2) & (a < 8)]                        # & | ~  + parenthèses (pas and/or)
np.where(a > 5, "haut", "bas")
np.nan  np.isnan(a)  np.nanmean(a)  a.copy()
```

## Pandas
```python
df = pd.read_csv("f.csv")              # sep=";"  parse_dates=["date"]
df = pd.DataFrame({"col1": [...], "col2": [...]})
df.to_csv("out.csv", index=False)

# Explorer
df.head()  df.tail()  df.shape  df.columns  df.info()  df.describe()
df["col"].value_counts()  df["col"].unique()  df["col"].nunique()  df.isna().sum()

# Sélectionner
df["col"]                    # Series
df[["c1", "c2"]]             # DataFrame (doubles crochets)
df.loc[lignes, colonnes]     # par ÉTIQUETTES (fin incluse)
df.iloc[0:5, 0:2]            # par POSITIONS (fin exclue)

# Filtrer
df[df["age"] > 30]
df[(df["ville"] == "Paris") & (df["age"] > 30)]
df[df["ville"].isin(["Paris", "Lyon"])]
df.query("age > 30 and ville == 'Paris'")
df.loc[df["age"] > 30, ["nom", "age"]]

# Nettoyer
df.dropna()  df.fillna(0)  df["c"].astype(int)  df.drop_duplicates()
df.rename(columns={"old": "new"})  df.drop(columns=["c"])

# Transformer
df["total"] = df["qte"] * df["prix"]
df["cat"] = np.where(df["total"] > 100, "gros", "petit")
df["c"].apply(ma_fonction)        df["c"].apply(lambda x: x * 2)
df["txt"].str.upper()  df["date"].dt.month

# Trier / agréger / combiner
df.sort_values("col", ascending=False)   df.nlargest(5, "col")
df.groupby("cat")["val"].sum()
df.groupby("cat").agg(total=("val", "sum"), n=("val", "count")).reset_index()
pd.pivot_table(df, values="val", index="a", columns="b", aggfunc="sum")
pd.merge(df1, df2, on="cle", how="left")   # left / right / inner / outer
pd.concat([df1, df2], ignore_index=True)

# Graphique rapide
df["col"].plot(kind="hist"); df.groupby("cat")["val"].sum().plot(kind="bar")
```

## ⚠️ Pièges classiques
- L'indexation commence à **0**. Dans un slice, la **fin est exclue** (sauf avec `.loc`).
- L'**indentation** compte. N'oublie pas les `:` après `if`, `for`, `def`.
- `=` affecte, `==` compare.
- NumPy/Pandas : `&`, `|`, `~` avec des **parenthèses**, jamais `and`/`or`.
- `df["a", "b"]` ❌ → `df[["a", "b"]]` ✅
- Beaucoup de méthodes pandas renvoient une **nouvelle** copie : `df = df.dropna()` (sinon rien ne change).
- `KeyError` sur un DataFrame = nom de colonne mal écrit (vérifie `df.columns`).
