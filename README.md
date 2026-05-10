# Numerical Relativity Kyoto Initiative

The Kyoto Initiative is a joint effort by several numerical relativity
groups to perform **blind** binary neutron star merger cross-code
comparisons. All groups will perform merger simulations starting from
common initial data. They will submit their waveforms, as well as their
estimated uncertainties, to the data analysis group, who will perform a
careful comparison between all models. The results will be documented in
a paper, with all participating groups listed as co-authors.

This comparison primarily focuses on gravitational waves. However, we
will also compare ejecta and remnant disk data.

At this time, we are in the planning phase for this effort.

## Timeline

* February 5, 2026: initial conception of the project at the YITP workshop
  [Multi-Messenger Astrophysics in the Dynamic
  Universe](https://www2.yukawa.kyoto-u.ac.jp/~mm2026/).

* March 23, 2026: this document is finalized. The project will
  be announced to the broader community and open to anyone who wants to join.

* May 25, 2026: initial data, list of quantities to be submitted, and
  data format specifications are released on GitHub.

* **June 1, 2027**: deadline for submitting waveforms and data

* End of 2027: paper submitted to arXiv and journal, all data and
  analysis scripts are immediately released on Zenodo.

### Note on Deadlines

Participation in a large-scale code comparison effort is time and
resource intensive. In the absence of strict deadlines, each group is
incentivized to be the last submitting. In the interest of fairness and
in recognition of the efforts of those involved, this project has a
strict deadline for submission. Failure to meet the deadline implies
exclusion from the project and from the paper.


## Initial Data

**Initial data lead:** Kenta Kiuchi <kenta.kiuchi@aei.mpg.de>

Low-eccentricity [FUKA](https://samueltootle.github.io/fuka/) initial
data corresponding to two neutron stars will be made available at a
pre-specified date, to give all groups, including those joining after the
YITP workshop, the same time to produce waveforms.

Groups may, at their discretion, opt to generate and evolve initial data
created with a different solver, but corresponding to the same physical
system.

### Initial data parameters

* **EOS:** [HS(DD2) from CompOSE](https://compose.obspm.fr/eos/18).
* **Masses:** TBD, target something like $1.4 + 1.2\ M_\odot$
* **Separation:** TBD, target ~10 orbits


## Simulation Parameters

Simulation codes should employ the CompOSE equation of state in tabular form.

To keep costs under control, simulations should employ a grid spacing
between 0.05 and 0.5 $M_\odot$.

Simulation groups will perform simulations at different resolutions, but
should only contribute a single waveform and its estimated uncertainty.
The latter could be estimated as the difference between the two highest
resolutions, or with Richardson extrapolation, or with any technique each
team prefers. We expect each group to submit complex phase and amplitude
of the strain at $\mathcal{I}_+$ decomposed in $s=-2$ spin weighted
spherical harmonics, as well as estimated uncertainties for each
quantity. Data are submitted in the [watpy](https://git.tpi.uni-jena.de/core/watpy)
/ CoRe database format, with the comparison-specific adaptations
described in the [Data Format](#data-format) section below.


### Gravitational-Wave Data

Each group submits **one** waveform per mode, corresponding to its best
estimate of the strain at future null infinity $\mathcal{I}_+$ — typically
obtained by polynomial extrapolation in $1/r$ from finite-radius
extractions, or by Cauchy-characteristic extraction. No per-resolution or
per-radius datasets are submitted; the resolution dependence is folded
into the reported uncertainties.

The $(\ell, m) = (2, 2)$ mode is required. Higher modes up to $\ell = 8$
are strongly encouraged. File and column conventions are specified in
the [Data Format](#data-format) section.


### Ejecta Data

Each team is asked to report the total ejecta mass and kinetic energy,
estimated using the geodesic criterion. To this aim, groups are
recommended to extend their simulations until the outflow rate drops to
zero. Alternatively, groups can estimate finite-duration errors and
include them in the error budget. As for gravitational waves, each group
is asked to submit two quantities — ejecta mass and kinetic energy —
together with their estimated uncertainties.

Following CompOSE's conventions, the mass density should be defined as
$\rho_b = m_n\, n_b$, where $m_n$ is the neutron mass and $n_b$ the
baryon number density. The kinetic energy density should be defined as
$\rho W (W -1)$, where $W$ is the Lorentz factor and $\rho$ is the
*energy density* in the material.

### Disk Data

Each team is asked to report the disk mass at the end of their
simulations. For the purpose of this comparison, the disk mass is
estimated as the total baryonic mass of all the material with rest-mass
density $\rho_b \leq 10^{13}\ {\rm g}\,{\rm cm}^{-3}$. 

## Data Format

Submissions follow the [watpy](https://git.tpi.uni-jena.de/core/watpy) /
CoRe database conventions, with two adaptations specific to this
comparison:

1. Each group submits **one** waveform per mode, extrapolated to
   $\mathcal{I}_+$ — not the per-radius, per-resolution datasets stored
   in the public CoRe DB.
2. Each data file (waveform or outflow) is paired with a sibling
   **`_error` file** of identical schema, in which every value is
   replaced by the $1\sigma$ uncertainty estimate of the corresponding
   entry in the data file. The shared independent variable (e.g. the
   retarded time column $u/M$) is repeated unchanged in the error file,
   so the two can be loaded with the same parser.

All quantities are in geometric units ($c = G = M_\odot = 1$). Time and
length are reported in units of the binary's gravitational mass $M$ in
solar masses; the value of $M$ is recorded in each file's header.

### Directory layout

A submission is a single flat directory, named after the evolution code:

    <code>/
    |-- metadata.txt
    |-- Rh_l2_m2.txt
    |-- Rh_l2_m2_error.txt
    |-- Rh_l2_m1.txt
    |-- Rh_l2_m1_error.txt
    |-- ...
    |-- outflows.txt
    |-- outflows_error.txt
    |-- ejecta_hist_Ye.txt
    |-- ejecta_hist_Ye_error.txt
    |-- ejecta_hist_entropy.txt
    |-- ejecta_hist_entropy_error.txt
    |-- ejecta_hist_velocity.txt
    |-- ejecta_hist_velocity_error.txt

The radius suffix from the CoRe filename convention
(`Rh_l<L>_m<M>_r<RRRRR>.txt`) is dropped, since the data correspond to
$\mathcal{I}_+$ rather than a finite extraction sphere.

### Mode files

Each `Rh_l<L>_m<M>.txt` is plain ASCII with two header lines giving the
binary mass and the column layout:

    # M=2.6000e+00
    # u/M:0  Reh/M:1  Imh/M:2  Momega:3  A/M:4  phi:5

| col | symbol            | meaning                                                   |
| --- | ----------------- | --------------------------------------------------------- |
| 0   | $u/M$             | retarded time, mass-rescaled                              |
| 1   | $\mathrm{Re}\,h/M$ | real part of the mass-rescaled mode strain $h_{\ell m}/M$ |
| 2   | $\mathrm{Im}\,h/M$ | imaginary part of $h_{\ell m}/M$                          |
| 3   | $M\omega$         | mass-rescaled instantaneous frequency $\omega = \dot\phi$ |
| 4   | $A/M$             | mode amplitude, $A = \lvert h_{\ell m}\rvert$             |
| 5   | $\phi$            | unwrapped mode phase, $h_{\ell m} = A\, e^{-i\phi}$       |

This reproduces the CoRe convention exactly, with the per-radius `t`
column omitted (it is meaningless after extrapolation to
$\mathcal{I}_+$). Watpy's `wave` loader reads these files unchanged.

The companion file `Rh_l<L>_m<M>_error.txt` shares the same schema —
two header lines and six columns — but each row contains the $1\sigma$
uncertainty estimate of the corresponding row in the data file:

    # M=2.6000e+00
    # u/M:0  d(Reh)/M:1  d(Imh)/M:2  d(Momega):3  d(A)/M:4  d(phi):5

Column 0 is the retarded time and matches the data file row-for-row.
Columns 1–5 are the $1\sigma$ errors $\delta(\mathrm{Re}\,h)/M$,
$\delta(\mathrm{Im}\,h)/M$, $M\,\delta\omega$, $\delta A/M$, and
$\delta\phi$ on the corresponding columns of `Rh_l<L>_m<M>.txt`.

### Outflows

`outflows.txt` records the integrated scalar quantities described in
the [Ejecta Data](#ejecta-data) and [Disk Data](#disk-data) sections,
one row per quantity:

    # quantity        value           unit
    ejecta_mass       <val>           Msun
    ejecta_kinetic    <val>           Msun
    disk_mass         <val>           Msun

The companion file `outflows_error.txt` has the same schema, with each
`<val>` replaced by its $1\sigma$ uncertainty estimate.

In addition, three histograms of the unbound ejecta are submitted:
distributions of mass with respect to electron fraction $Y_e$, specific
entropy $s$ (in $k_B/\mathrm{baryon}$), and asymptotic velocity
$v_\infty/c$. Each histogram is a plain-text file with two header lines
and three columns:

`ejecta_hist_Ye.txt`:

    # bin variable: Ye  (dimensionless, 0 to 0.5)
    # bin_low:0  bin_high:1  mass:2  [Msun]

`ejecta_hist_entropy.txt`:

    # bin variable: s  (kB/baryon)
    # bin_low:0  bin_high:1  mass:2  [Msun]

`ejecta_hist_velocity.txt`:

    # bin variable: v_inf/c  (dimensionless, 0 to 1)
    # bin_low:0  bin_high:1  mass:2  [Msun]

Each row gives the bin edges and the total unbound rest mass falling
within that bin. The bins should cover the full physical range of the
variable and need not be uniform, but should be fine enough to resolve
the distribution (a few tens of bins is typical). The sum of column 2
across all rows must equal the `ejecta_mass` entry of `outflows.txt`
to within the reported uncertainty.

Each histogram has a sibling `*_error.txt` file with the same
`bin_low`, `bin_high` columns and the $1\sigma$ uncertainty on the
binned mass in column 2.

### Metadata

A single `metadata.txt` per submission, in the watpy `key = value`
format defined by `watpy.coredb.metadata.MDKEYS`. The required keys for
this comparison are:

* `database_key`, `simulation_name`, `binary_type` (= `BNS`)
* `id_code`, `id_eos`, `id_mass`, `id_mass_starA`, `id_mass_starB`,
  `id_eccentricity`, `id_gw_frequency_Hz`
* `evolution_code`, `metric_scheme`, `hydro_flux`,
  `hydro_reconstruction`, `grid_spacing_min`, `number_of_orbits`

Groups should additionally document, in free-text trailing the standard
keys, (i) the procedure used to extrapolate the waveform to
$\mathcal{I}_+$ and (ii) the uncertainty estimation method used to
populate the `_error` files.

### Computing strain from $\Psi_4$

If your code outputs the Newman-Penrose scalar $\Psi_4$ rather than the
strain $h$, watpy provides a fixed-frequency double time integration
([Reisswig & Pollney, CQG **28** (2011) 195015](https://doi.org/10.1088/0264-9381/28/19/195015))
that converts $\Psi_4$ to $h$ without the unphysical low-frequency drift
of a naive double integration. The function lives at
`watpy.wave.gwutils.fixed_freq_int_2`:

```python
import numpy as np
from watpy.wave.gwutils import fixed_freq_int_2

# u: uniformly-sampled retarded time array, in units of M
# rPsi4_lm: complex r * Psi4_{lm} sampled on u
# fcut: low-frequency cutoff, in mass-rescaled units (cycles per M)
dt    = u[1] - u[0]
rh_lm = fixed_freq_int_2(rPsi4_lm, fcut, dt=dt)
```

The cutoff $f_\mathrm{cut}$ must lie below the dominant frequency of
the mode being integrated; setting it too high filters physical signal,
while setting it too low fails to suppress the drift. A standard choice
is

$$ f_\mathrm{cut} = (1 - \epsilon)\, \frac{m}{2}\, f_0 ,$$

with $f_0$ the initial gravitational-wave frequency of the (2, 2) mode
(recorded as `id_gw_frequency_Momega22 / (2\pi)` in the metadata) and
$\epsilon \sim 0.1$. The signal must be uniformly sampled in time —
interpolate first if your $\Psi_4$ time series is not evenly spaced.

## Data Analysis

**Data analysis lead:** Jocelyn Read <jread@fullerton.edu>

The data analysis group has the following tasks:

* Develop a specification for the data format (by May 25, 2026)
* Propose a set of analysis diagnostics (during summer 2026)
* Develop analysis scripts (by summer 2027)
* Analyze data, prepare figures (by end of summer 2027)

The data analysis team will present analysis results in blinded form,
meaning that code names will be replaced by a unique anonymous identifier
(e.g., a number), to the rest of the collaboration. The data will be
unblinded after all project participants have approved the draft of the
final manuscript.


## Paper Writing

A publication describing the results of this project will be prepared by
a paper writing team. The draft will then be open to comments to all
participants. The paper writing team shall consist of:

* The data analysis team: first author, discuss results
* David Radice: introduction, cleanup of the draft
* Kenta Kiuchi: initial data
* Code representatives: description of codes, methods, and approaches,
  authors 2-N in alphabetical order

Co-authorship will be offered to all active participants — code
representatives, developers, and PIs — who have actually contributed to the
project. Each author should provide a brief, one sentence statement of
work done to be part of the paper. The participants will be listed in
alphabetical order after the code representatives.


## Participating Groups

Each group should appoint a representative. The representative will be
the main point of contact for each group.

We will try to keep telecons to a minimum. The representative of each
group agrees to participate in all of them. Occasionally, they may appoint a
substitute. Only the representative of each group joins the telecons (or
a substitute), as keeping the group small will improve our efficiency.
This also ensures that all groups are given the same space. 

### AsterX

* **Spokesperson:** Jay Kalinani <jkalinan@illinois.edu>
* **URL:** https://github.com/EinsteinToolkit/AsterX

### AthenaK

* **Spokesperson:** David Radice <dur566@psu.edu>
* **URL:** https://github.com/ias-astrophysics/athenak

### BAM

* **Spokesperson:** Tim Dietrich <tim.dietrich@uni-potsdam.de>
* **URL:** https://journals.aps.org/prd/abstract/10.1103/PhysRevD.84.044012

### FIL

* **Spokesperson:** Elias R. Most <emost@caltech.edu>
* **URL:** https://academic.oup.com/mnras/article/490/3/3588/5585413

### GRaM-X

* **Spokesperson:** Philipp. Mösta <p.moesta@uva.nl>
* **URL:** https://iopscience.iop.org/article/10.1088/1361-6382/acf2d9


### GR-Athena++ 

* **Spokesperson:** Luis Felipe Longo Micchi <luis.felipe.longo.micchi@uni-jena.de> 
* **URL:** https://computationalrelativity.github.io/grathenacode/

### GRACE
* **Spokesperson:** Carlo Musolino <carlo.musolino@aei.mpg.de>
* **URL:** https://github.com/GRACE-astro/grace/tree/main

### IllinoisGRMHD/GRHayLHD

* **Spokesperson:** Leo Werneck <leonardo@uidaho.edu>
* **URL:** https://iopscience.iop.org/article/10.1088/0264-9381/32/17/175009/meta
* **URL:** https://journals.aps.org/prd/abstract/10.1103/bbtm-31r5
* **URL:** https://einsteintoolkit.org/thornguide/GRHayLET/IllinoisGRMHD/documentation.html
* **URL:** https://einsteintoolkit.org/thornguide/GRHayLET/GRHayLHD/documentation.html

### MHDuet

* **Spokesperson:** Carlos Palenzuela <carlos.palenzuela@uib.es>
* **URL:** http://mhduet.liu.edu/

### NANASI

* **Spokesperson:** Kenta Kiuchi <kenta.kiuchi@aei.mpg.de>
* **URL:** https://doi.org/10.1103/PhysRevD.106.124041

### SACRA-MPI

* **Spokesperson:** Kenta Kiuchi <kenta.kiuchi@aei.mpg.de>
* **URL:** https://doi.org/10.1103/zmdc-xkcm

### SpEC

* **Spokesperson:** Francois Foucart <francois.foucart@unh.edu>
* **URL:** https://www.black-holes.org/for-researchers/spec



## How to Participate

Make a pull request to this GitHub repository adding an entry for your
code above. Send [me](mailto:dur566@psu.edu) an email to be added to the
Kyoto Initiative Mailing list.


## Policies

**Project coordinator:** David Radice <dur566@psu.edu>
