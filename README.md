# Neutron shielding calculations

This repository contains tools for calculating neutron transmission and albedo probabilities in different shielding materials. It shows how the shielding performance depends on shielding thickness, incident neutron energy, and material composistion, such as B-10 content in B4C and component ratio in epoxy-Gd2O3. In addition, it contains calculation tools to decide appropriate shielding parameters for shielding in different regions in the detector, which includes side, end and interstack shielding.

## Requisties
- Python3 (https://www.python.org/downloads/)
- Jupyter Notebook (https://jupyter.org/)

## Installation

First, install Python3 according to the instructions on the website.

Then, install Jupyter Notebook according to:
```
python -m pip install jupyter 
```

Finally, clone the code repository according to:
```
git clone https://github.com/ess-dg/neutron_shielding_calculations.git
```

## Execution

Open a terminal, navigate to 'neutron_shielding_calculations' and run the command:
```
jupyter notebook
```
then click on 'main.ipynb' to open the Jupyter Notebook.

Alternatively, the notebook can be run directly using binder in a web browser using the following link:
https://mybinder.org/v2/gh/ess-dg/neutron_shielding_calculations/HEAD
