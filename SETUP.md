# Setup steps

This file is for my own reference. It can be deleted once the site is live.

## 1. Place the folder

Unzip so that the project sits at:

```
D:/mengtingyu88/geospatial-coursework
```

Single level, not nested. Open `geospatial-coursework.Rproj` in RStudio.

## 2. Install packages

Run once in the R Console:

```r
install.packages("pacman")

pacman::p_load(sf, tidyverse, tmap, spdep, sfdep, spatstat,
               raster, GWmodel, SpatialAcc,
               olsrr, corrplot, ggpubr, plotly, knitr)
```

Then verify each one loads before relying on it:

```r
library(sf); library(tmap); library(spdep); library(GWmodel)
```

`sf` on Windows installs as a binary with GDAL, GEOS and PROJ bundled, so it normally needs no system setup. `GWmodel` and `spatstat` are large. `maptools` has been retired from CRAN, so skip it if a tutorial calls for it and find the modern equivalent.

## 3. First render

From the project root, in the Terminal:

```bash
pwd          # must show the project root
ls -la       # must show _quarto.yml, index.qmd
quarto render
```

Success looks like `_site/index.html` existing.

## 4. Git

Create an empty repo on GitHub first. Do not tick README, .gitignore or licence.

```bash
git init
git add .
git commit -m "Initial site framework for geospatial analytics coursework"
git branch -M main
git remote add origin https://github.com/mengtingyu88/geospatial-coursework.git
git push -u origin main
```

Use straight quotes in the commit message. Curly quotes break Bash string parsing.

## 5. Vercel

Import the repo. Change one setting only:

- Root Directory: `_site`
- Framework Preset: Other
- Build Command: leave empty
- Install Command: leave empty

Set the Project Name deliberately. It becomes the URL, and it is globally unique across Vercel, so a generic name may already be taken. Once the URL is submitted to the instructor, the Vercel project name is fixed. The GitHub repo name can still be changed freely.

## 6. Update site-url

After Vercel gives the real URL, edit `site-url` in `_quarto.yml` to match, then render, commit and push again.

## Routine from then on

Always from the project root, always all four steps:

```bash
quarto render
git add .
git commit -m "message"
git push
```

## Two directories that must stay in git

- `_site/` is what Vercel serves.
- `_freeze/` is the computed-output cache. Losing it means every page re-executes.

Neither is in `.gitignore`, and neither should be added to it.
