---
icon: material/draw-pen
---

# Equations

!!! note
    Here, capital characters refer to endogenous variables, while lowercase characters indicate exogenous parameters.

## Objective function

The objective function is expressed as the minimization of total system costs, including investment, operation and management (O&M) cost.

$$
{VTC} =
\displaystyle \sum_{n, i, r} \left[ {gacc}_{n, i, r} \cdot {VGR}_{n, i, r} + {gfoc}_{n, i, r} \cdot {VGS}_{n, i, r} + {garc}_{n, i, r} \cdot {VGP}_{n, i, r} \right] +
\displaystyle \sum_{l} \left[ {facc}_{l} \cdot {VFR}_{l} + {ffoc}_{l} \cdot {VFS}_{l} + {farc}_{l} \cdot {VFP}_{l} \right]  +
\displaystyle \sum_{n, i, s} \left[ {eacc}_{n, i, s} \cdot {VER}_{n, i, s} + {efoc}_{n, i, s} \cdot {VES}_{n, i, s} + {earc}_{n, i, s} \cdot {VEP}_{n, i, s} \right]  +
\displaystyle \sum_{t} {wt}_{t} \cdot \left[ \sum_{n, i, r} \left[ {gvoc}_{n, i, r} \cdot {VG}_{n, i, r, t} \right]  + \displaystyle \sum_{l, t} \left[ {fvoc}_{l} \cdot  ( {VFF}_{l, t} + {VFB}_{l, t} )  \right] \right] \to min
$$

## Generator operation & capacity

### Minimum/Maximum operation of generator

The output of generator is constrainted by its installed capacity and the minimum and maximum output per unit of capacity.

$$
{gmn}_{n, i, r, t} \cdot {VGS}_{n, i, r} \leq {VG}_{n, i, r, t} \leq {gmx}_{n, i, r, t} \cdot {VGS}_{n, i, r}
$$

For dispatchable generators, the output in each timeslices is constraited not to exceed the installed capacity (${gmx}_{n, i, r, t}=1$).
For non-dispatchable generators, the output in each timeslices is constrainted by output pattern ($0 \leq {gmx}_{n, i, r, t} \leq 1$).
Hense, the curtailed output of solar and wind power is accounted for in the postprocessing as follows:

$$
{gmx}_{n, i, r, t} \cdot {VGS}_{n, i, r}-{VG}_{n, i, r, t}
$$

### Minimum/Maximum capacity of generator

The capacity of generator is constrainted by the minimum and maximum capacity.

$$
{gsmn}_{n, i, r} \leq {VGS}_{n, i, r} \leq {gsmx}_{n, i, r}
$$

### Minimum/Maximum new installation of generator

The new installaion of generator is constrainted by the minimum and maximum capacity.

$$
{grmn}_{n, i, r} \leq {VGR}_{n, i, r} \leq {grmx}_{n, i, r}
$$

## Link operation & capacity

### Link Minimum/Maximum operation

The energy flow via link is constrainted by its installed capacity and the minimum and maximum energy flow per unit of capacity.

$$
{ffmn}_{l, t} \cdot {VFS}_{l} \leq {VFF}_{l, t} \leq {ffmx}_{l, t} \cdot {VFS}_{l} 
$$

$$
{fbmn}_{l, t} \cdot {VFS}_{l} \leq {VFB}_{l, t} \leq {fbmx}_{l, t} \cdot {VFS}_{l}
$$

To formulate the energy flow in a lossy transport model [^1], two separate variables are introduced for the forward and backward directions of energy flow. Each of these flows is subject to distinct parameters specifying the minimum and maximum energy flow per unit. For links that allows only unidirectional energy flow (e.g., electrolyser), the backward energy flow is constrained to zero (${fbmx}_{l, t} = 0$).

### Minimum/Maximum capacity of link

The capacity of link is constrainted by the minimum and maximum capacity.

$$
{fsmn}_{l} \leq {VFS}_{l} \leq {fsmx}_{l} 
$$

### Minimum/Maximum new installaion of link

The new installaion of link is constrainted by the minimum and maximum capacity.

$$
{frmn}_{l} \leq {VFR}_{l} \leq {frmx}_{l} 
$$

## Storage operation & capacity

### Minimum/Maximum operation of storage

The energy level of storage is constrainted by its installed capacity and the minimum and maximum energy level per unit of capacity.

$$
{emn}_{n, i, s, t} \cdot {VES}_{n, i, s} \leq {VE}_{n, i, s, t} \leq {emx}_{n, i, s, t} \cdot {VES}_{n, i, s} 
$$

### Minimum/Maximum capacity of storage

The capacity of storage is constrainted by the minimum and maximum capacity.

$$
{esmn}_{n, i, s} \leq {VES}_{n, i, s} \leq {esmx}_{n, i, s} 
$$

### Minimum/Maximum new installation of storage

The new installaion of storage is constrainted by the minimum and maximum capacity.

$$
{ermn}_{n, i, s} \leq {VER}_{n, i, s} \leq {ermx}_{n, i, s}
$$

### Time-series state of charge of storage

The energy level of storage at each timeslice ${VE}_{n, i, s, t}$ depends on the level at previous timeslice ${VE}_{n, i, s, t-1}$ and charge or discharge of storage ${VH}_{n, i, s, t}$.
Here, ${{eeta}_{n, i, s}}$ denotes the self-discharge rate of storage.

$$
{VE}_{n, i, s, t} =  {{eeta}_{n, i, s}}^{{rt}_{t}} \cdot {VE}_{n, i, s, t-1} - {rt}_{t} \cdot {VH}_{n, i, s, t}
$$

Furthermore, the energy level of the storage at the first timeslice ${VE}_{n, i, s, t_1}$ and the last timeslice ${VE}_{n, i, s, t_{|T|}}$ is constrained to be equal.

$$
{VE}_{n, i, s, t_1} = {VE}_{n, i, s, t_{|T|}}
$$

### Power-Energy capacity of storage

Some storage technologies (e.g., pumped hydro storage) are subject to constraints on the ratio between their power capacity (e.g., pump) and energy capacity (e.g., reservoir).

$$
{VFS}_{l} = \displaystyle \sum_{s} \displaystyle \sum_{\left(n, i\right)\in ML_{n,i,l}} ( {ecrt}_{n, i, s, l} \cdot {VES}_{n, i, s} )
$$

## Nodal energy balance

$$
\displaystyle \sum_{n\in MN_{n^{npb},n} } \displaystyle \sum_{t\in MT_{t^{npb},t} } \left[ \displaystyle \sum_{r}{VG}_{n, i, r, t} + \displaystyle \sum_{s}{VH}_{n, i, s, t} - \displaystyle \sum_{l} \left[ {kff}_{n, i, l} \cdot {VFF}_{l, t} \right]  + \displaystyle \sum_{l} \left[ {kbf}_{n, i, l} \cdot {VFB}_{l, t} \right]\right]  = {dmd}_{n^{npb}, i, t^{npb}} + \delta^{npb}_{n^{npb}, i, t^{npb}}
$$

## Technology stock balance

### 

$$
{VGS}_{n, i, r} =  ( {VGR}_{n, i, r} + {VGP}_{n, i, r} )  \cdot t\_int + \displaystyle \sum_{y}{gsc}_{n, i, r, y} \quad \left( \forall y\in \left\{y | y + {glt}_{n,i,r} \leq y^* \right\} \subset H \right)
$$

$$
{VFS}_{l} =  ( {VFR}_{l} + {VFP}_{l} )  \cdot t\_int + \displaystyle \sum_{y}{fsc}_{l, y} \quad \left( \forall y\in \left\{y | y + {flt}_{l} \leq y^* \right\} \subset H \right)
$$

$$
{VES}_{n, i, s} =  ( {VER}_{n, i, s} + {VEP}_{n, i, s} )  \cdot t\_int + \displaystyle \sum_{y}{esc}_{n, i, s, y} \quad \left( \forall y\in \left\{y | y + {elt}_{n,i,s} \leq y^* \right\} \subset H \right)
$$

$$
{gsr}_{n, i, r} \geq {VGP}_{n, i, r}
$$

$$
{fsr}_{l} \geq {VFP}_{l}
$$

$$
{esr}_{n, i, s} \geq {VEP}_{n, i, s}
$$

### Dynamic stock change

$$
{gsc}^{y+1}_{n, i, r, y} = {VGR}_{n, i, r}
$$

$$
{fsc}^{y+1}_{l, y} = {VFR}_{l}
$$

$$
{esc}^{y+1}_{n, i, s, y} = {VER}_{n, i, s}
$$

$$
{gsr}_{n, i, r} = \sum_{y} {gsc}_{n, i, r, y} \quad \left( \forall y\in \left\{y | y + {glt}_{n,i,r} \geq y^* \right\} \subset H \right)
$$

$$
{fsr}_{l} = \sum_{y} {fsc}_{l, y} \quad \left( \forall y\in \left\{y | y + {flt}_{l} \geq y^* \right\} \subset H \right)
$$

$$
{esr}_{n, i, s} = \sum_{y} {esc}_{n, i, s, y} \quad \left( \forall y\in \left\{y | y + {elt}_{n,i,s} \geq y^* \right\} \subset H \right)
$$

## Energy supply

### Energy supply accounting

$$
{VP}_{n, i, k} = \displaystyle \sum_{r, t} \left[ {wt}_{t} \cdot {VG}_{n, i, r, t} \cdot {geta}_{n, i, r, k} \right]
$$

### maximum/minimum energy supply

$$
{pmin}_{n^{sup}, k^{sup}} \leq \displaystyle \sum_{n\in ME_{n^{sup},n} } \displaystyle \sum_{k\in MK_{k^{sup},k} } \displaystyle \sum_{i}{VP}_{n, i, k}
$$

$$
{pmax}_{n^{sup}, k^{sup}} \geq \displaystyle \sum_{n\in ME_{n^{sup},n} } \displaystyle \sum_{k\in MK_{k^{sup},k} } \displaystyle \sum_{i}{VP}_{n, i, k}
$$

## CO2 emission

### CO2 emission accounting

$$
{VQ}_{n, i} = \displaystyle \sum_{k} \left[ {VP}_{n, i, k} \cdot {gas}_{n, i, k} \right]
$$

### maximum CO2 emission

$$
\displaystyle \sum_{n\in MQ_{n^{emi},n}} \displaystyle \sum_{i}{VQ}_{n, i}  \leq {qmax}_{n^{emi}}
$$

[^1]: Neumann, F., Hagenmeyer, V. & Brown, T. Assessments of linear power flow and transmission loss approximations in coordinated capacity expansion problems. Appl. Energy 314, 118859 (2022).
