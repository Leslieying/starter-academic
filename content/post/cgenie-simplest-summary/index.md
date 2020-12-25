---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "cGEnIE Simplest Summary"
subtitle: ""
summary: "A simple note of cgenie study"
authors: [Rui Ying]
tags: [cGEnIE]
categories: [cGEnIE]
date: 2020-12-25T16:44:18Z
lastmod: 2020-12-25T16:44:18Z
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

# Table of Contents

1. [Basic](#org3528a6d)
    1.  [Install and Test](#orgf2ef73c)
    2.  [Running model](#org6ee389f)
    3.  [Model output](#org3f3d873)
2.  [Ocean circulation](#org9b24787)
    1.  [Tracing ocean circulation](#orgadfec09)
    2.  [Results to view](#orgf327405)
3.  [Climate of Past](#org1cddfe8)
    1.  [Cretaceous (70 Ma)](#org4146d9d)
    2.  [early Eocene (56 Ma)](#orga7d3860)
4.  [Fossil fuel CO<sub>2</sub>](#orga8ddb3c)
    1.  [customise emission forcing scale](#orgacb3969)
    2.  [Historical emission forcing](#org94702d4)
5.  [Ocean biogeomchemical cycle](#orgae79f6b)
    1.  [nutrient's control on biological productivity](#org3b09411)
    2.  [Iron and Phosphate fertilisation](#org2288c23)
    3.  [What to view](#org6b52392)
6.  [EcoGEnIE](#orga61e628)
    1.  [Customization](#org9b9f935)
    2.  [Result to view](#org6604fe8)



<a id="org3528a6d"></a>

# Basic


<a id="orgf2ef73c"></a>

## Install and Test

1.  Use git to download source codes.
2.  make sure dependencies(gfortran, netCDF) are pre-installed.
3.  Modify `user.mak` to specify NetCDF path; and uncomment something in `makefile.arc` according to your system to use (see the instruction).
4.  Test the model by typing `make testbiogem`.


<a id="org6ee389f"></a>

## Running model

Command to run model: `qsub -q dog.q -j y -o cgenie_log -V -S /bin/bash runmuffin.sh basic-cofing user-config years spin-file`. Or another direct but not practical way: `cd genie-main`, and `./runmuffin.sh ...`
Parameters in `qsub`:
-q: bind job to queue
-j: y/n to merge stdout and stderr of job
-o: output file
-V: export all environment variables
-S: shell to use
To check, use `qstat -f`.

**Note.1**: you CANNOT submit job with new base-config file directly. The correct way is to run the model at the command line to re-compile the model.
**Note2** : You should create a **new config** file and set **control group** in every new experiment. Do not attempt to modify configuration file directly.


<a id="org3f3d873"></a>

## Model output

Model output store in `~/cgenie_output`. Two types of output are defined.

1.  Time-slices: \*.nc(netcdf) files. (average) spatial distribution of properties (keytracer, flux, and physical characteristics) every
2.  Time-series: \*.res files. Time-varying suitable reduced indicators


<a id="org9b24787"></a>

# Ocean circulation


<a id="orgadfec09"></a>

## Tracing ocean circulation

Basic-config to use: `cgenie.eb_go_gs_ac_bg.worjh2.rb` (contains red color tracer)
What and where to inject your tracer:
Variables:

```bash
    bg_par_forcing_name="pyyyyz_Fred" #forcing name
    bg_par_force_point_i=22 #3D coordinate
    bg_par_force_point_j=33
    bg_par_force_point_k=8
    bg_par_ocn_force_scale_val_48=0.0 #scale in mol/yr
```

<a id="orgf327405"></a>

## Results to view

`ocn_colr` in 3D netCDF
Tracer distribution: `ocn_int_colr` (long name: water-column integrated tracer inventory)
Atlantic streamfunction: `phys_opsia`
Barotropic streamfunction: `phys_psi` (something like circulation in lat-lon plot.)
Deep water formation: `convective cost` or `ventilation age`
Trace inventory: `biogem_series_ocn_colr.res`

What’s streamfunction? [This link](http://www.climate.be/textbook/glossary_m.xml) worth viewing. Basically, positive values represent clockwise direction along contour lines.


<a id="org1cddfe8"></a>

# Climate of Past

Not many things to play with


<a id="org4146d9d"></a>

## Cretaceous (70 Ma)

Basic-config: `cgenie.eb_go_gs_ac_bg.p0067f.NONE`
Add Color-injection: `cgenie.eb_go_gs_ac_bg.p0067f.rb`


<a id="orga7d3860"></a>

## early Eocene (56 Ma)

Basic-config `cgenie.eb_go_gs_ac_bg.p0055c.NONE`


<a id="orga8ddb3c"></a>

# Fossil fuel CO<sub>2</sub>

Basic-config: `cgenie.eb_go_gs_ac_bg.worjh2.BASE`


<a id="orgacb3969"></a>

## customise emission forcing scale

-   `bg_par_atm_force_scale_val_3 =8.3333e+013` scale variable in user-config.
-   `biogem_force_flux_atm_pCO2_sig.dat` (in mol) forcing file in `cgenie.muffin/genie_forcings/`

Then the true flux is 1&times; 8.33E13 mol/yr = 10E15 g C/yr = 1 Pg C/yr.

    -START-OF-DATA-
    	0.0  1.0
    	1.0  1.0
    	1.0  0.0
    999999999.0  0.0
    -END-OF-DATA-

This can be plot as y~x.


<a id="org94702d4"></a>

## Historical emission forcing

Define the forcing as `worjh2.historical2010` in user-config and comment the scale variable, because this historical emission forcing directly follows **the observed change** in atmospheric concentration with time.
set `bg_par_misc_t_start=1765.0` which is the year to start transient (it's often defined in pre-industrial age like 1700s). You can define as following to decide which year's data should be saved (the profile is in `biogem/data/input`).

    bg_par_infile_slice_name='save_timeslice_historicalfuture.dat'
    bg_par_infile_sig_name='save_timeseries_historicalfuture.dat'

Then run for 245 years and we come to year 2010. Any future modelling then can use this as new spin-up.
There're also some IPCC/SRES scenarios can be used, such as `worjh2.FeMahowald2006.FpCO2_Fp13CO2_A2_02180PgC` which provide IPCC 'A2' scenario.


<a id="orgae79f6b"></a>

# Ocean biogeomchemical cycle


<a id="org3b09411"></a>

## nutrient's control on biological productivity

Basic-config: `cgenie.eb_go_gs_ac_bg.worjh2.BASES` (add more traces than last chapter)
Parameters to play:

```bash
      bg_par_bio_k0_PO4=1.9582242E-06 #maximum rate of conversion of dissolved PO4 into organic matter (mol kg-1 yr-1)
      bg_par_bio_remin_POC_eL1=550.5195 #the depth-scale where POM is remineralizated
      bg_par_bio_remin_POC_frac2=6.4591110E-02 #the fraction of POM to export
      bg_par_bio_red_POC_CaCO3=0.044372 #CaCO3/POC ratio
      ea_36=y #climate-CO2 feedback
      bg_par_data_save_level=5 #data to save, check the instruction
      bg_par_bio_c0_PO4=2.1989611E-07 #[PO4] M-M half-sat value (mol kg-1)
      bg_par_bio_red_POP_POC=106.0 #redfield ratio
      bg_par_bio_red_DOMfrac=0.66 #how many organic matter produced is partitioned into dissolved (DOM)
    bg_par_bio_remin_DOMlifetime=0.5 #DOM mean lifetime (yr) in the ocean
```

<a id="org2288c23"></a>

## Iron and Phosphate fertilisation

This determines the total flux of Fe and P.

```bash
    ## --- GEO: Fe ---
    bg_par_forcing_name="worjh2.FeMahowald2006.FpCO2_Fp13CO2_A2_02180PgC_FFe"
    bg_par_ocn_force_scale_val_9=1.0e+09
    ## --- GEO: PO4 ---
    bg_par_forcing_name="worjh2.FeMahowald2006.FpCO2_Fp13CO2_A2_02180PgC_FPO4"
    bg_par_ocn_force_scale_val_8=2.0e+12
    ## --- GEO: ALK ---
    bg_par_forcing_name="worjh2.FeMahowald2006.FpCO2_Fp13CO2_A2_02180PgC_FALK"
    bg_par_ocn_force_scale_val_12=5.0e+13
```

<a id="org6b52392"></a>

## What to view

Maybe pCO<sub>2</sub> is a good option.


<a id="orga61e628"></a>

# EcoGEnIE

**Description**: ECOGEM has poorer performance than BIOGEM in biogeochemistry (also because BIOGEM has been calibrated), but BIOGEM is unrealistic because it transform nutrient to POM/DOM instantly without passing from plankton biomass.
Basic-config: `muffin.CBE.worlg4.BASESFeTDTL`


<a id="org9b9f935"></a>

## Customization

In user-config, we can define plankton file (another text file) by variable `eg_par_ecogem_plankton_file`. The data is in `genie-ecogem/data/input/*.eco` which has form like:

    -START-OF-DATA-
     Phytoplankton     0.60   1
     Phytoplankton      6.0   1
     Phytoplankton     60.0   1
     Zooplankton        6.0   1
     Zooplankton       60.0   1
     Zooplankton      600.0   1
    -END-OF-DATA-

Columns mean functional type (including Diatom, Coccolithophore etc), diameter. The number 1 means nothing.

**Nutrient limitation:**
Turn on Fe limitation: set `eg_useFe=.true.` and `eg_fquota=.true.`. Then define `eg_qminFe_a` and `eg_qmaxFe_a` as the range of Fe. And `bg_par_det_Fe_sol_exp` determines the solubility of atmospheric iron inputs in seawater.


<a id="org6604fe8"></a>

## Result to view

-   Nutrient limitation: `eco2D_xGamma_Fe_001` and `co2D_xGamma_P_001` in netCDF file. The value is from 0 to 1, higher value means less limitation.
-   Size metric: `eco2D_Size_Mean/Stdev`
-   Size distribution: `eco2D_Size_Frac_pico/nano/microphytoplankton`.
    pico &rarr; &le; 2 &mu; m
    nano &rarr; 2~20
    micro &rarr; &ge; 20 um
-   C:P biomass ratio
-   Distribution pattern in different size class

