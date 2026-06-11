# Ozone Analyzer


## Project layout

```
ozone_analyzer/
├── main.py                    # Entry point
├── config.py                  # Constants & plot styling
├── requirements.txt
├── backend/
│   ├── serial_handler.py      # Serial I/O + acquisition thread
│   └── data_processor.py      # Parse raw frames -> typed dicts
├── frontend/
│   ├── gui.py                 # Tk GraphApp (notebook + polling)
│   ├── plots.py               # Matplotlib renderers
│   └── components.py          # Reusable widgets (Tooltip)
└── utils/
    └── helpers.py
```

## Setup

```bash
python -m venv .venv
source .venv/bin/activate            # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Run

```bash
python main.py            



