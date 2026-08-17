# ⚙️ Setup Guide — Data Cleanser

> Get the notebook running in under 2 minutes.

---

## Option 1 — Google Colab (Recommended — Zero Setup)

1. Open [Data_Cleanser_ParthShah.ipynb](./Data_Cleanser_ParthShah.ipynb) on GitHub
2. Click the **Open in Colab** button at the top of the file
3. In Colab: **Runtime → Run all**
4. Done. The dataset is generated inside the notebook — no external file needed.

---

## Option 2 — Local Jupyter Notebook

### Step 1 — Clone the repository
```bash
git clone https://github.com/ParthShah7099/Data-Cleanser.git
cd Data-Cleanser
```

### Step 2 — Create a virtual environment (optional but recommended)
```bash
python3 -m venv venv
source venv/bin/activate        # Mac / Linux
venv\Scripts\activate           # Windows
```

### Step 3 — Install dependencies
```bash
pip install -r requirements.txt
```

### Step 4 — Launch Jupyter
```bash
jupyter notebook
```

### Step 5 — Open and run
Open `Data_Cleanser_ParthShah.ipynb` → **Kernel → Restart & Run All**

---

## Requirements

| Requirement | Version |
|---|---|
| Python | 3.9 or above |
| pandas | 2.0.0 or above |
| numpy | 1.24.0 or above |
| matplotlib | 3.7.0 or above |
| seaborn | 0.12.0 or above |
| scikit-learn | 1.3.0 or above |
| scipy | 1.11.0 or above |

All installable in one command via `pip install -r requirements.txt`.

---

## No Dataset File Needed

The dataset is **synthetically generated inside the notebook** using `numpy.random.seed(42)`.  
Every run produces the exact same 200-row patient health records dataset — fully reproducible.

---

*Made with discipline by **THE PARTH SHAH***
