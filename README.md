# A Learning-Automata Moving Target Defence Against LOFT Attacks in SDN

Code, data and figures for the paper

> T. AkhlaghPasandi and H. Haj Seyyed Javadi, "A Learning-Automata Moving Target Defence Against Low-Rate Flow-Table Overflow Attacks in Software-Defined Networks," manuscript submitted for review, 2026.

The low-rate flow-table overflow (LOFT) attack fills an OpenFlow switch's flow table while sending almost nothing. The defence here uses learning automata in three places:

* **LA-A** draws the idle timeout of every new rule from a distribution it learns;
* **LA-B** resamples the table occupancy at which mitigation starts;
* **LA-DETECT** keeps one two-action automaton per rule and decides from the rule's flow statistics over time whether it belongs to a refresher. A team of automata learns its five parameters from labelled flow sequences.

## What is in this repository

| path | contents |
|---|---|
| `LOFT_MTD_LA.ipynb` | the whole study in one notebook: simulator, attacker models, the three automata, the labelled dataset, every experiment and figure of the paper. Runs in Google Colab; outputs are saved in the file. |
| `ryu_la_mtd/` | the defence as a **Ryu application for OpenFlow 1.3**, the Mininet / Open vSwitch testbed, the scripts behind Section VII of the paper and the results of our runs. See [`ryu_la_mtd/README.md`](ryu_la_mtd/README.md). |
| `figures/` | every figure of the paper at 600 dpi. |

## Running the notebook

Open `LOFT_MTD_LA.ipynb` in Colab or Jupyter and run the cells in order. Nothing needs to be uploaded. `SCALE = "demo"` (4 seeds) takes about 10 minutes; `SCALE = "full"` (32 seeds, the paper's numbers) about an hour on two cores. Appendix E needs scikit-learn and PyTorch, which Colab already has. Locally:

```
pip install -r requirements.txt
jupyter notebook LOFT_MTD_LA.ipynb
```

## Running the defence on a switch

The testbed needs Linux, root, Mininet, Open vSwitch and Ryu 4.34 in a Python 3.9 environment. The steps are in [`ryu_la_mtd/README.md`](ryu_la_mtd/README.md). In short:

```
cd ryu_la_mtd
sudo RYU_MANAGER=/path/to/venv39/bin/ryu-manager bash run_all.sh    # about 50 minutes
python3 analyze_testbed.py && python3 validity_testbed.py
```

## Citation

If you use this code, please cite the paper above (see also `CITATION.cff`).
