# Analyseur Ozone

Interface graphique en temps réel pour la communication série avec un analyseur d'ozone Thermo Fisher 49-i.

---


## Lancer l'application
Ver0
```bash
python3 App.py

```

Ver1
```
python3 main.py

```
---

## Version 1 — Architecture via fichier CSV (prototype)

Le backend écrit les données directement dans un fichier CSV sur le disque.
L'interface graphique relit et recharge l'intégralité du fichier CSV à chaque
cycle de rafraîchissement pour mettre à jour les graphiques.

**Limitations :**
- Les performances se dégradent avec le temps à mesure que le fichier CSV grossit
- Risque de *race condition* lorsque les deux threads accèdent simultanément au fichier
- Absence de mécanisme d'arrêt propre (boucle `while True` sans interruption)

---

## Version 2 — Architecture via Queue (version finale)

La version actuelle. Le backend pousse les trames brutes dans une `Queue`
thread-safe. L'interface graphique vide la file toutes les 200ms via
`root.after()` sur le thread principal.

**Améliorations par rapport à la Version 1 :**
- Thread-safe par conception — aucun risque de *race condition*
- Les performances ne se dégradent pas dans le temps
- Arrêt propre via `stop_event`
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
Ver0
├──App.py                      # Interface graphique et main
├── fnct_finales_valerio.py    # Port serie connexion, recuperation et traitment de donnees

Ver1
```
ozone_analyzer/
├── main.py                      # Point d'entrée
├── config.py                    # Configuration (port, baudrate, etc.)
├── requirements.txt
├── backend/
│   ├── serial_handler.py        # Communication série + thread d'acquisition
│   ├── mock_serial_handler.py   # Mode simulation (sans matériel)
│   └── data_processor.py        # Parser des trames brutes
├── frontend/
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
