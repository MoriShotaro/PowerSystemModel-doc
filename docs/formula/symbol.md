---
icon: material/alphabet-greek
---

# Symbols

!!! note
    Here, capital characters refer to endogenous variables, while lowercase characters indicate exogenous parameters.

## Sets

|name|description|
|---|---|
|$y\in Y\subset H$|set of year based on the simulation time horizon $Y$ as a subset of all years $H$ including past years. $y^*\in Y$ denotes the simulation year.|
|$t\in T$|timeslice|
|$n\in N$|region|
|$i\in I$|sector|
|$l\in L$|link|
|$r\in R$|generator|
|$s\in S$|storage|
|$k\in K$|energy carrier|

## Mapping sets

|name|description|
|---|---|
|$n^{npb}$|set of regions for nodal energy balance constraint|
|$t^{npb}$|set of timeslices for nodal energy balance constraint|
|$MN_{n^{npb},n}$|region group combination for nodal power balance constraint|
|$MT_{t^{npb},t}$|timeslice group combination for nodal power balance constraint|
|$k^{sup}$|set of energies for energy supply constraint|
|$n^{sup}$|set fo regions for energy supply constraint|
|$ME_{n^{sup},n}$|region group combination for energy supply constraint|
|$MK_{k^{sup},k}$|energy group combination for energy supply constraint|
|$n^{emi}$|set of regions for emission constraint|
|$MQ_{n^{emi},n}$|region group combination for emission constraint|
|$ML_{n,i,l}$|node, sector and link combination for power-energy capacity constraint for storage|
<!--
|$FL_IR\in n, i, r$|sector-generator flag|
|$FL_IS\in n, i, s$|sector-storage flag|
|$FL_IRK_{n, i, r, k}$|generator-energy carrier flag|
|$FL_IRY|n, i, r, Y|generator cohort term|
|$FL_IL1|n, i, l|link intra-region flag (end)|
|$FL_IMT|n^{npb}, i, MT|nodal power balance flag|
|$FL_LY|L, Y|link cohort term|
|$FL_ISY|n, i, s, Y|storage cohort term|
|$FL_IRP|n, i, r|generator replacement flag|
|$FL_LP|L|link replacement flag|
|$FL_ISP|n, i, s|storage replacement flag|
-->

## Parameters

|name|description|
|---|---|
|$wt_t$|weighting of timeslice (-)|
|$rt_t$|granularity of timeslice (-)|
|$gmn_{n, i, r, t}$|minimum output of generator per unit of nominal power (GW/GW)|
|$gmx_{n, i, r, t}$|maximum output of generator per unit of nominal power (GW/GW)|
|$gsmn_{n, i, r}$|minimum capacity of generator (GW)|
|$gsmx_{n, i, r}$|maximum capacity of generator (GW)|
|$grmn_{n, i, r}$|minimum new installation of generator (GW)|
|$grmx_{n, i, r}$|maximum new installation of generator (GW)|
|$geta_{n, i, r, k}$|efficiency of generator per output (PW/GW)|
|$gacc_{n, i, r}$|annualized capital cost of extending capacity of generator (million USD/GW)|
|$gfoc_{n, i, r}$|fixed operational cost of generator (million USD/GW)|
|$gvoc_{n, i, r}$|variable operational cost of generator (million USD/GWh)|
|$garc_{n, i, r}$|annualized replacement cost of generator (million USD/GW)|
|$gsc_{n, i, r, y}$|existing stock of generator (GW)|
|$gsr_{n, i, r}$|retired stock of generator (GW)|
|$ffmn_{l, t}$|minimam forward energy flow of link per unit of nominal power (GW/GW)|
|$ffmx_{l, t}$|maximum forward energy flow of link per unit of nominal power (GW/GW)|
|$fbmn_{l, t}$|minimam backward energy flow of link per unit of nominal power (GW/GW)|
|$fbmx_{l, t}$|maximum backward energy flow of link per unit of nominal power (GW/GW)|
|$fsmn_{l}$|minimum capacity of link (GW)|
|$fsmx_{l}$|maximum capacity of link (GW)|
|$frmn_{l}$|minimum new installation of link (GW)|
|$frmx_{l}$|maximum new installation of link (GW)|
|$kff_{n, i, l}$|incidence matrix of forward flow (GW/GW)|
|$kbf_{n, i, l}$|incidence matrix of backward flow (GW/GW)|
|$facc_{l}$|annualized capital cost of extending capacity of link (million USD/GW)|
|$ffoc_{l}$|fixed operational cost of link (million USD/GW)|
|$fvoc_{l}$|variable operational cost of link (million USD/GWh)|
|$farc_{l}$|annualized replacement cost of link (million USD/GW)|
|$fsc_{l, y}$|existing stock of link (GW)|
|$fsr_{l}$|retired stock of link (GW)|
|$emn_{n, i, s, t}$|minimum energy level of storage (GWh/GWh)|
|$emx_{n, i, s, t}$|minimum energy level of storage (GWh/GWh)|
|$esmn_{n, i, s}$|minimum capacity of storage (GWh)|
|$esmx_{n, i, s}$|maximum capacity of storage (GWh)|
|$ermn_{n, i, s}$|minimum new installation of storage (GWh)|
|$ermx_{n, i, s}$|maximum new installation of storage (GWh)|
|$eeta_{n, i, s}$|standing loss of storage (GWh/GWh)|
|$eacc_{n, i, s}$|annualized capital cost of extending capacity of storage (million USD/GWh)|
|$efoc_{n, i, s}$|fixed operational cost of storage (million USD/GWh)|
|$earc_{n, i, s}$|annualized replacement cost of storage (million USD/GWh)|
|$esc_{n, i, s, y}$|existing stock of storage (GWh)|
|$esr_{n, i, s}$|retired stock of storage (GWh)|
|$ecrt_{n, i, s, l}$|C-rate of storage (GW/GWh)|
|$dmd_{n^{npb}, i, MT}$|hourly energy demand (GW)|
|$gas_{n, i, k}$|emission factor (MtCO2/PWh)|
|$pmin_{n^{sup}, k^{sup}}$|annual minimum energy supply (PWh)|
|$pmax_{n^{sup}, k^{sup}}$|annual maximum energy supply (PWh)|
|$qmax_{n^{emi}}$|annual emission constraint (MtCO2)|
|$t\_int$|time interval for simulation|

## Variables

|name|description|
|---|---|
|$VTC$|total system cost (million USD)|
|$VG_{n, i, r, t}$|energy output of generator (GW)|
|$VGR_{n, i, r}$|new installation of generator (GW)|
|$VGS_{n, i, r}$|caparity of generator (GW)|
|$VGP_{n, i, r}$|repracement of generator (GW)|
|$VFF_{l, t}$|forward energy flow of link (GW)|
|$VFB_{l, t}$|backward energy flow of link (GW)|
|$VFR_l$|new installation of link (GW)|
|$VFS_l$|capacity of link (GW)|
|$VFP_l$|replacement of link (GW)|
|$VE_{n, i, s, t}$|energy level of storage (GWh)|
|$VH_{n, i, s, t}$|energy charge and discharge of storage (GW)|
|$VER_{n, i, s}$|new installation of storage (GWh)|
|$VES_{n, i, s}$|capacity of storage (GWh)|
|$VEP_{n, i, s}$|replacement of storage (GWh)|
|$VP_{n, i, k}$|primary energy supply (PWh)|
|$VQ_{n, i}$|CO2 emission (MtCO2)|
|$\delta^{npb}_{n^{npb}, i, t^{npb}}$|slack variable for nodal power balance (GW)|
<!-- 
|RES_GSCB|n, i, r|slack variable for generator stock balance (GW)|
|RES_FSCB|L|slack variable for link stock balance (GW)|
|RES_ESCB|n, i, s|slack variable for storage stock balance (GWh)|
-->