<p float="left">
  <img src="https://raw.githubusercontent.com/scikit-hep/mplhep/master/docs/source/_static/mplhep.png" width="300"/>
</p>

[![DOI](https://zenodo.org/badge/184555939.svg)](https://zenodo.org/badge/latestdoi/184555939)
[![Scikit-HEP][sk-badge]](https://scikit-hep.org/)

[sk-badge]: https://scikit-hep.org/assets/images/Scikit--HEP-Project-blue.svg

[![Docs](https://readthedocs.org/projects/mplhep/badge/?version=latest)](https://mplhep.readthedocs.io/en/latest/?badge=latest)
[![PyPI version](https://badge.fury.io/py/mplhep.svg)](https://badge.fury.io/py/mplhep)
[![Supported Python versions](https://img.shields.io/pypi/pyversions/mplhep.svg)](https://pypi.org/project/mplhep/)

[![Build Status](https://travis-ci.org/scikit-hep/mplhep.svg?branch=master)](https://travis-ci.org/scikit-hep/mplhep)
[![GitHub Actions Status: CI](https://github.com/scikit-hep/mplhep/workflows/CI/CD/badge.svg)](https://github.com/scikit-hep/mplhep/actions?query=workflow%3ACI%2FCD+branch%3Amaster)
[![GitHub Actions Status: Publish](https://github.com/scikit-hep/mplhep/workflows/publish%20distributions/badge.svg)](https://github.com/scikit-hep/mplhep/actions?query=workflow%3A%22publish+distributions%22+branch%3Amaster)

[![PyPI download week](https://img.shields.io/pypi/dw/mplhep?label=downloads%20%28incl%20CI%29)](https://img.shields.io/pypi/dw/mplhep?label=downloads%20%28incl%20CI%29)

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/scikit-hep/mplhep/master)

A set of helpers for `matplotlib` to more easily produce plots typically
needed in HEP as well as style them in way that's compatible with current
collaboration requirements (ROOT-like plots for CMS, ATLAS, LHCb, ALICE).


# Installation

```bash
pip install mplhep
```

# Getting Started

### Styling

```python
import mplhep as hep
hep.set_style(hep.style.ROOT) # For now ROOT defaults to CMS
# Or choose one of the experiment styles
hep.set_style(hep.style.CMS)
# or
hep.set_style("ATLAS") # string aliases work too
# or
hep.set_style("LHCb")
# or
hep.set_style("ALICE")
```

The style can be set directly from the `matplotlib` API as well

```python
import matplotlib.pyplot as plt
import mplhep as hep
plt.style.use(hep.style.ROOT)
```

Experiment specific style are also available. **If the default styles are not what you need, I'd be happy to merge in new styles or modify the current ones.**

Default experiment labels are also available.

```python
# Overall - both left and right annotation
hep.<experiment>.label()
# Just experiment label and <text> such as 'Preliminary' or 'Simulation'
hep.<experiment>.text(<text>)
```

### Plotting
#### 1D Histograms

```python
h, bins = [2, 3, 2], [0, 1, 2, 3]
hep.histplot(h, bins)
```

#### 2D Histograms

```python
import numpy as np
xbins, ybins = [0, 1, 2, 3], [0, 1, 2, 3]
H = np.array([[2,3,2], [1,2,1], [3,1,3]])
hep.hist2dplot(H, xbins, ybins)
```



# More Information

### Other styles:
- `hep.set_style("fira")` - use Fira Sans
- `hep.set_style("firamath")` - use Fira Math

#### Styles can be chained:
- e.g. `hep.set_style(["CMS", "fira", "firamath"])`
- reappearing `rcParams` get overwritten silently

#### Styles can be modified on the fly
- Since styles are dictionaries and they can be chained/overwritten they can be easily modified on the fly. e.g.
```
hep.set_style("CMS")
hep.set_style({"font.sans-serif":'Comic Sans MS'})
```

#### Styling with LaTeX
- `hep.set_style("CMSTex")` - Use LaTeX to produce all text labels
- Requires having the full tex-live distro
- True Helvetica
- Use sansmath as the math font
- Takes longer and not always better
- In general more possibilities, but a bit more difficult to get everything working properly

# Notes

## Consistency \& Fonts
As it is ROOT does not come with any fonts and therefore relies on using system fonts. Therfore the font in a figure can be dependent on whether it was produced on OSX or PC. The default sans-serif font used is Helvetica, but it only comes with OSX, in Windows this will silently fallback to Arial.

### License
Both Helvetica and Arial are proprietary, which as far as fonts go means you can use it to create any text/graphics once you have the license, but you cannot redistribute the font files as part of other software. That means we cannot just package Helvetica with this to make sure everyone has the same font in plots.

Luckily for fonts it seems only the software is copyrighted, not the actual shapes, which means there are quite a few open alternatives with similar look. The most closely resembling Helvetica being Tex Gyre Heros

#### Tex Gyre Heros
http://www.gust.org.pl/projects/e-foundry/tex-gyre/heros

You can compare yourself if the differences are meanigful below.

<p float="center">
  <img src="FontComp.png" width="400" />
</p>

They are Tex Gyre Heros, Helvetica and Arial respecively.

### Math Fonts
- Math fonts are a separate set from regular fonts due to the amount of special characters
- It's not trivial to make sure you get a matching math font to your regular font
- Most math-fonts are serif fonts, but this is not ideal if one wants to use sans-serif font for normal text like Helvetica or Arial
- The number of sans-serif math-fonts is very limited
 	- The number of **open** sans-serif math-fonts is **extremely** limited
 	- Basically there's two, Fira Sans and GFS Neohellenic Math, of which I like Fira Sans better
 	- https://tex.stackexchange.com/questions/374250/are-there-opentype-sans-math-fonts-under-development

For consistent styling Fira Sans is included as well.
#### Default Fira Sans
https://github.com/mozilla/Fira
#### Math font extension
https://github.com/firamath/firamath

## What doesn't work

### Context styles and fonts

```python
with pyplot.style.context(style.ROOT):
    plotting...
```
- This syntax would be ideal, however, it doesn't work properly for fonts and there are no plans by mpl devs to fix this behaviour https://github.com/matplotlib/matplotlib/issues/11673

For now one has to set the style globally:

### Use in publications

Updating list of citations and use cases of `mplhep` in publications:

- [Simultaneous Jet Energy and Mass Calibrations with Neural Networks](https://cds.cern.ch/record/2706189), ATLAS Collaboration, 2019
- [Integration and Performance of New Technologies in the CMS Simulation](https://arxiv.org/abs/2004.02327), Kevin Pedro, 2020 (Fig 3,4)
- [GeantV: Results from the prototype of concurrent vector particle transport simulation in HEP](https://arxiv.org/abs/2005.00949), Amadio et al, 2020 (Fig 25,26)
- [Search for the standard model Higgs boson decaying to charm quarks](https://cds.cern.ch/record/2682638), CMS Collaboration, 2019 (Fig 1)
