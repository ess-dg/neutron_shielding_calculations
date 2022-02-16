# General considerations for effective thermal neutron shielding in detector applications

This repository contains tools for calculating neutron transmission and albedo probabilities in different shielding materials. It shows how the shielding performance depends on shielding thickness, incident neutron energy, and material composistion, such as <sup>10</sup>B-content in B<sub>4</sub>C and component ratio in epoxy-Gd<sub>2</sub>O<sub>3</sub>. In addition, it contains calculation tools to decide appropriate shielding parameters for shielding in different regions in the detector, which includes external, side, end and interstack shielding. The details of how the investigation is performed can be found in the paper 'General considerations for effective thermal neutron shielding in detector applications'.

In this repository, there is also a data folder with two subfolders which contains all the data used in the analysis. The 'material_data'-subfolder contains all the cross-sections files used for the analysis, while the 'simulation_results'-subfolder contains the simulations results used to evaluate the validity of the analytical calculations. The format of the data is presented below in the 'Data'-section.

## Running in browser

Alternatively to the installation method stated below, it is possible to run the notebook directly in the browser using binder. Simply click on the link below, wait for binder to compile and then click on 'main.ipynb' to open the Jupyter Notebook.

Link: https://mybinder.org/v2/gh/ess-dg/neutron_shielding_calculations/HEAD

## Requisties
- Python3 (https://www.python.org/downloads/)
- LaTeX (https://www.latex-project.org/get/)
- Jupyter (https://jupyter.org/)

## Installation

First, install Python3 and LaTeX according to the instructions on their respective websites.

Then, install Jupyter according to:
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
jupyter lab
```
then click on 'main.ipynb' to open the Jupyter Notebook.

## Basic usage

After opening the notebook, make sure to run the cells in the correct order the first time running the notebook. Otherwise, code snippets further down the notebook might be missing dependecies which are declared earlier.

## Data
The data format of the files in two data subfolders, 'material_data' and 'simulation_results', are presented below, resepctively.

### material_data
This folder contains the neutron interaction cross-section files for the materials analyzed, extracted from Geant4 using the ESS Detector Group simulation framework. The files are stored as '.txt'-files and they start with a header containing general information about the material. The header from the cadmium-file is presented below, as an example:

> #FileType: Geant4 XSECTSPY DATA
<br/>#PhysicsList: QGSP_BIC_HP_EMZ
<br/>#ParticleName: neutron
<br/>#ParticleCode: 2112
<br/>#ParticleMass[MeV/c^2]: 939.565
<br/>#ParticleCharge: 0.000000
<br/>#Material: G4_Cd
<br/>#MaterialDensity [g/cm3]: 8.65
<br/>#MaterialTemperature [K]: 293.15
<br/>#MaterialPressure [bar]: 1.01325
<br/>#MaterialAverageAtomicWeight [amu]: 112.411
<br/>#NAtomsPerVolume [1/cm3]: 4.63401e+22
<br/>#ConvertXSectBarnToMeanFreePathMilliMeter: 215.796
<br/>#EnergyUnit: eV
<br/>#XSectUnit: barn

After the header, the cross-section data appears. This is stored in two columns, the first column contains the neutron energies in [eV], while the second column contains the corresponding interaction cross-sections in [barns]. The file contains four different interaction cross-sections: hadronic elastic, neutron inelastic, neutron capture and total. These are separated by headers, as examplified below:

> #Process 0: hadElastic
<br/> 1.01157945426e-09 3544.55083972
<br/> 1.02329299228e-09 3528.635719
<br/> 1.03514216668e-09 3555.12686029
<br> <span>&#8942;</span>
<br/>#Process 1: neutronInelastic
<br/>10964.7819614 0.00236589309542
<br/>11091.7481526 0.0530968104758
<br/>11220.184543 0.0530900886024
<br> <span>&#8942;</span>
<br/>#Process 2: nCapture
<br/>1.03514216668e-09 9274499.29054
<br/>1.04712854805e-09 9226870.87881
<br/>1.05925372518e-09 9174990.61906
<br> <span>&#8942;</span>
<br/>#Process -: Total
<br/>1.04712854805e-09 9278043.84138
<br/>1.05925372518e-09 9230399.51453
<br/>1.07151930524e-09 9178545.74592
<br> <span>&#8942;</span>

A function to parse this data, 'parse_data', is included in the notebook in this repository.

### simulation_results
This folder contains the simulation results, gather according to the description in the 'General considerations for effective thermal neutron shielding in detector applications' paper. The files are stored as '.npy'-files, and can be read using the numpy 'load'-function (https://numpy.org/doc/stable/reference/generated/numpy.load.html). The numpy arrays are structured in the following format:

> numpy.array([
>> numpy.array([wavelengths_in_angstrom]),
<br> numpy.array([
>>> numpy.array([thicknesses_in_mm, transmission_counts, number_of_incident_neutrons, transmission_probability]),
<br>      <span>&#8942;</span>
<br>  numpy.array([thicknesses_in_mm, transmission_counts, number_of_incident_neutrons, transmission_probability])])

>> numpy.array([
>>> numpy.array([thicknesses_in_mm, albedo_counts, number_of_incident_neutrons, transmission_probability]),
<br> <span>&#8942;</span>
<br> numpy.array([thicknesses_in_mm, albedo_counts, number_of_incident_neutrons, albedo_probability])])

Note that the second and third numpy arrays contains a number of numpy arrays equal to the length of wavelengths in the first numpy array. That is, each of the numpy arrays correspond to a specific neutron wavelength investigated.

