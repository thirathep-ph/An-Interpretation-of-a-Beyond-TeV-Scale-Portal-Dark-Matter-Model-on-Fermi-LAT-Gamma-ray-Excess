# An Interpretation of a Beyond-TeV-Scale Portal Dark Matter Model on Fermi-LAT Gamma-ray Excess

Senior project (2023) by **Thirathep Naowabut Phiankham**,
Faculty of Science, Khon Kaen University (KKPaCT group).
Advisor: Asst. Prof. Dr. Chakrit Pongkitivanichkul

Contact: thirathep.ph@gmail.com

---

This project investigates whether dark matter annihilation can explain the
persistent gamma-ray excess toward the Galactic Center measured by
[Fermi-LAT](https://fermi.gsfc.nasa.gov/science/). A beyond-TeV-scale portal
dark matter model is used to predict the annihilation spectrum, which is then
fitted against the observed excess.

**Main result**: the best fit is obtained for annihilation into
$W^+W^-$ with
$m_\chi = 2.915\ \mathrm{TeV}$ and
$\langle\sigma v\rangle \approx 4.4\times10^{-23}\ \mathrm{cm^3/s}$
(see the report abstract for the full parameter set and statistical
significance).

## Repository layout

```
analysis/     Jupyter notebook implementing the full analysis pipeline
report/       Senior project report (PDF, LaTeX source, references, figures)
LICENSE       MIT license
```

### `analysis/`

| File | Description |
|------|-------------|
| `gamma_excess.ipynb` | Main analysis notebook (see pipeline below) |
| `fermi_excess.csv` | Fermi-LAT excess data, unfiltered |
| `fermi_excess_reduced.csv` | Same data, filtered for outliers |
| `dNdE_DM*.npy` | Pre-computed annihilation spectra $(dN/dE_\gamma)$ so you can skip the expensive simulation steps |
| `bbbar_allM.png`, `notes_theory.jpg` | Reference plots / explanation sketches |

### `report/`

`Report.pdf` is the final write-up; `Report.tex` + `references.bib` +
`images/` are its source.

## Analysis pipeline

The notebook proceeds step by step:

1. **Fermi-LAT excess data** — loads the observed gamma-ray excess
   (`fermi_excess.csv` / `fermi_excess_reduced.csv`).
2. **Dark matter density & J-factor** — computes DM density profiles
   (NFW, Einasto, Isothermal, Burkert, Moore, ...) and the corresponding
   line-of-sight J-factors for the Milky Way.
3. **Annihilation spectra** — $dN_\gamma/dE_\gamma$ for DM masses up to
   $10^5$ GeV:
   - [PPPC4DM / CascadeSpectra](http://www.marcocirelli.net/PPPC4DMID.html)
     for $m_\chi < 500$ GeV,
   - [HDMSpectra](https://github.com/NOMspectra/NOMspectra) for
     $m_\chi \geq 500$ GeV.
   Results are cached in `dPdE_gamma*/` CSVs (generated on first run).
4. **Portal DM model** — convolves the spectra with the mediator phase-space
   factor from the portal model to get the expected flux $d\Phi/dE_\gamma$.
5. **Flux comparison** — fits the simulated flux (with and without an
   astrophysical background term) to the Fermi-LAT data via reduced
   $\chi^2$, producing best-fit parameters and $(m_\chi, \langle\sigma v\rangle)$
   contour plots.

## Running the notebook

Requirements: Python 3 with `numpy`, `pandas`, `scipy`, `matplotlib`
(a LaTeX installation is needed for the notebook's matplotlib `usetex` plots).
Open `analysis/gamma_excess.ipynb` and run top to bottom from the `analysis/`
directory.

Two external spectrum libraries must be placed alongside the notebook
(they are large, so they are not included in this repo):

- CascadeSpectra data table → `analysis/CascadeSpectra/Spectra/AtProduction_gammas.dat`
  ([PPPC4DM](http://www.marcocirelli.net/PPPC4DMID.html))
- HDMSpectra package + data → `analysis/HDMSpectra-master/data/HDMSpectra.hdf5`
  ([HDMSpectra](https://github.com/NOMspectra/NOMspectra))

Skipping steps 3–4 is possible: load `dNdE_DM_modified.npy` directly and
continue from the fitting section.

## Report

The full manuscript is in
[`report/Report.pdf`](report/Report.pdf).
The LaTeX source can be rebuilt with `pdflatex` from `report/`.

## License

[MIT](LICENSE)
