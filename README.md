# An Interoretation of a Beyond-TeV-Scale Portal ark Mtter Model on Fermi-LAT Gamma-ray Excess (2024)

Thirathep N. Phiankham \
Contact: thirathep.ph@gmail.com

------------------------------------------------------------------------------------------------------------------------------------------------

This software facilitates the analysis of dark matter annihilation in the Milky Way galaxy.  Understanding the simulations used (PPPC4DM and HDMSpectra) can be beneficial before diving in. Links to their documentation are provided below:

PPPC4DM: http://www.marcocirelli.net/PPPC4DMID.html
HDMSpectra: https://github.com/NOMspectra/NOMspectra

------------------------------------------------------------------------------------------------------------------------------------------------

# Data and Methodology

The software is in the **TeV-DM-Excess** directory.

The software follows a step-by-step approach to analyze potential dark matter signals:

1. Fermi-LAT Excess Data: This section retrieves excess gamma-ray data from Fermi-LAT, which is stored within the project directory. Two versions are provided: fermi_excess (unfiltered) and fermi_excess_reduced (filtered for outliers). You can choose the data that best suits your analysis needs.

2. Dark Matter Density and J-Factor: This section models the dark matter density and J-factor distribution within the Milky Way galaxy using NFW profiles.
3. CascadeSpectra + HDMSpectra: These sections combine the strengths of two software tools to calculate the dark matter annihilation spectrum: 
	CascadeSpectra: This tool is employed for dark matter masses below 500 GeV.
	HDMSpectra: This tool takes over for dark matter masses at or above 500 GeV. Note: This calculation can be computationally expensive and may take several hours to run. Pre-calculated results are available in the dPdE_gamma directory, which you can leverage to save time.
4. Portal Dark Matter Model (User-Specific): This section allows you to implement your chosen portal dark matter model. It typically involves defining energy and number density parameters specific to your model.
5. Gamma-Ray Flux and Comparison: This section compares the simulated gamma-ray flux (dPhidE) with the Fermi-LAT data. The reduced chi-square method is used to quantify deviations, visualized via contour plots.
