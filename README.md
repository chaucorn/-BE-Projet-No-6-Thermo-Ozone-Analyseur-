# Analyseur Ozone

Interface graphique en temps réel pour la communication série avec un analyseur d'ozone Thermo Fisher 49-i.

---


## Lancer l'application
v1.0.0
```bash
python3 App.py

```

v2.0.0
```
python3 main.py

```
---

## Version v1.0.0 — Architecture via fichier CSV

Le backend écrit les données directement dans un fichier CSV sur le disque.
L'interface graphique relit et recharge l'intégralité du fichier CSV à chaque
cycle de rafraîchissement pour mettre à jour les graphiques.


---

## Version ver2.0.0 — Architecture via Queue 

Le backend pousse les trames brutes dans une `Queue`
thread-safe. 

**Améliorations par rapport à v1.0.0 :**
- Thread-safe par conception — aucun risque de *race condition*
- Les performances ne se dégradent pas dans le temps
- Le fichier CSV n'est écrit qu'une seule fois par cycle par le thread principal

---

## Fonctionnalités

- Graphiques en temps réel : Ozone, Cellules A/B, Pression, Débit A/B, Températures, O3 Lamp
- Sauvegarde automatique dans `record/` avec nom de fichier horodaté
- Export CSV manuel via le bouton Sauvegarder
- Mode simulation pour tester sans matériel
- Boutons Démarrer/Arrêter l'acquisition

---

## Dépendances

| Bibliothèque | Version | Utilisation |
|---|---|---|
| `pyserial` | ≥ 3.5 | Communication série |
| `pandas` | ≥ 1.3 | Stockage et manipulation des données |
| `matplotlib` | ≥ 3.4 | Affichage des graphiques |
| `tkinter` | — | Interface graphique (inclus dans Python) |

---
## Structure du projet
v1.0.0
```
├──App.py                      # Interface graphique et main
├── fnct_finales_valerio.py    # Port serie connexion, recuperation et traitment de donnees
```
v2.0.0
```
ozone_analyzer/
├── main.py                      # Point d'entrée
├── config.py                    # Configuration (port, baudrate, etc.)
├── requirements.txt
├── backend/
│   ├── serial_handler.py        # Communication série + thread d'acquisition
│   └── data_processor.py        # Parser des trames brutes
├── frontend/
│   ├── login.py                 # écran de démarrage 
│   ├── gui.py                   # Interface graphique principale (GraphApp)
│   ├── plots.py                 # Rendu des graphiques matplotlib
│   └── components.py            # Composants réutilisables (Tooltip)
└── record/                      # Fichiers CSV sauvegardés automatiquement
```



## Encadrant

Gilles ATHIER — Ingénieur de recherche, LAERO (CNRS), Toulouse

---
## Etudiants

Valerio ANGIONE  
Lenny SABINE  
Vu Bao Chau DANG  
Elijah PEYRAT  
