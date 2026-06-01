# Challenge Python - Gestion des réparations de véhicules

## Contexte

Dans un garage automobile, on souhaite gérer différentes opérations de maintenance sur plusieurs types de véhicules.

### Types de véhicules

* Citadine
* Camionnette

### Opérations disponibles

* Vidange
* Changement de pneu

L'objectif est de modéliser ce système en Python de manière propre et évolutive.

---

## Modèle attendu

### Classe `Vehicule`

Classe de base contenant :

* l'immatriculation du véhicule

### Classes dérivées

* `Citadin`
* `Camionnete`

Ces classes héritent de `Vehicule`.

### Enumération `Operation`

Les opérations possibles :

* `VIDANGE`
* `CH_PNEU`

### Classe `Reparation`

Une réparation associe :

* un véhicule
* une opération

Elle doit permettre d'exécuter l'opération sur le véhicule concerné.

---

## Exemple d'utilisation

```python
citadine = Citadin("AA-BB-ZZ")
camionnette = Camionnete("CC-DD-EE")

r1 = Reparation(citadine, Operation.VIDANGE)
r2 = Reparation(camionnette, Operation.CH_PNEU)

r1.executer()
r2.executer()
```

### Résultat attendu

```text
Exécution de l'opération 'Vidange' sur le véhicule Citadin (AA-BB-ZZ)
Exécution de l'opération 'Changement de pneu' sur le véhicule Camionnete (CC-DD-EE)
```

---

## Bonus

Refactoriser la solution en utilisant le design pattern **Bridge** afin de séparer :

* les types de véhicules
* les opérations de réparation

Cette approche doit permettre d'ajouter facilement :

* de nouveaux véhicules (SUV, Berline, Moto, ...)
* de nouvelles opérations (Révision, Freinage, Contrôle technique, ...)

sans multiplier le nombre de classes.



"""
Dans un garage de réparation, on souhaite réaliser deux opérations
(vidange, changement de pneu) pour deux types de véhicules
(citadine, camionnette).
"""

```python
from enum import Enum


class Vehicule:
    def __init__(self, immatriculation: str):
        self.immatriculation = immatriculation

    def __str__(self):
        return f"{self.__class__.__name__} ({self.immatriculation})"


class Citadin(Vehicule):
    pass


class Camionnete(Vehicule):
    pass


class Operation(Enum):
    VIDANGE = "Vidange"
    CH_PNEU = "Changement de pneu"


class Reparation:
    def __init__(self, vehicule: Vehicule, operation: Operation):
        self.vehicule = vehicule
        self.operation = operation

    def executer(self):
        print(
            f"Exécution de l'opération '{self.operation.value}' "
            f"sur le véhicule {self.vehicule}"
        )


# Exemple d'utilisation
citadine = Citadin("AA-BB-ZZ")
camionnette = Camionnete("CC-DD-EE")

r1 = Reparation(citadine, Operation.VIDANGE)
r2 = Reparation(camionnette, Operation.CH_PNEU)

r1.executer()
r2.executer()
```
