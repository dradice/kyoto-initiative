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
quantity. The exact data format will be determined by the data analysis
team.


### Gravitational-Wave Data

This section will describe the details of the gravitational-wave data.


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
