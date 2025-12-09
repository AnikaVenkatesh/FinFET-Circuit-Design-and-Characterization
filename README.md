# FinFET-Circuit-Design-and-Characterization

<img width="1049" height="562" alt="image" src="https://github.com/user-attachments/assets/cd02d152-ea06-49b4-a147-cad76b9556b4" />

Supercomputers have rapidly evolved from Gigaflop performance in the 1980s to Teraflop in the late 1990s, Petaflop systems around 2008, and Exaflop machines achieved in 2021. The next major milestone is Zettascale computing (1 Zettaflop = $10^{21}$ FLOPS), expected by 2035. This advancement demands massive increases in computational performance, driven by more powerful CPUs and GPUs, while also pushing power consumption toward the 50–100 MW range for future Zetta-scale systems. The overall trend shows performance doubling every 1–2 years, enabling breakthroughs in AI, scientific modeling, climate simulation, and space research.

# Introduction To FinFETs

<img width="929" height="503" alt="image" src="https://github.com/user-attachments/assets/e24242ba-cbab-4625-800b-9c07bb4e12ad" />

<img width="938" height="513" alt="image" src="https://github.com/user-attachments/assets/6f9f4b8a-70c5-4679-828d-a1132ed43e39" />


FinFETs emerged as a solution when conventional planar MOSFETs could no longer maintain strong electrostatic control at sub-30 nm gate lengths. As the gate length shrank, the source and drain depletion regions in planar devices began to overlap, causing the gate to lose control of the channel charge. This led to severe short-channel effects such as DIBL, threshold voltage roll-off, and degraded subthreshold swing — leakage currents increased, variability worsened, and operating voltages could not be reduced without sacrificing performance.

FinFETs solved this by turning the channel into a vertical fin and wrapping the gate around it from multiple sides. With this tri-gate or double-gate structure, the gate has much stronger electrostatic influence over the channel, keeping the barrier under control even at aggressively scaled nodes. This enables near-ideal subthreshold swing and substantially reduces off-state leakage, which directly improves power efficiency. Because the fin has height as well as width, the effective channel width increases in 3D, allowing much higher drive current within the same footprint; multiple fins can also be placed in parallel to scale performance without consuming more area.

An additional advantage comes from reduced channel doping requirements. Planar MOSFETs relied heavily on doping to control the channel, which introduced random dopant fluctuations and severe $V_T$ variability. FinFETs rely primarily on geometry (fin thickness and gate wrapping), allowing lightly-doped or even undoped channels — leading to more stable threshold voltage, lower noise, and better uniformity across billions of devices.

All of this together enabled FinFETs to operate at lower supply voltage while still increasing performance. That improvement in both dynamic and static power made FinFETs ideal for everything from high-density mobile SoCs to the most performance-hungry HPC processors. Most importantly, FinFETs could be manufactured by evolving the existing CMOS process — reusing innovations such as HKMG and strain engineering — allowing the industry to continue scaling through 22 nm, 14 nm, 10 nm, 7 nm, and 5 nm nodes.

In short, FinFETs rescued CMOS scaling when planar devices reached their physical limit. They sustained Moore’s Law for an entire decade by restoring electrostatic integrity, improving leakage and variability, offering higher drive current, and enabling reduced-power operation — while setting the path toward the next evolution of transistor architecture: Gate-All-Around (GAA) nanosheet and nanowire FETs, where the channel will be fully surrounded by the gate for even tighter control.

## Standard Cell Area Scaling

As process nodes advance into deeply-scaled geometries, aggressive shrinking of traditional parameters such as gate pitch or metal pitch becomes increasingly difficult and expensive. To continue densification without driving manufacturing complexity beyond economic limits, the industry relies on scaling boosters — structural and layout innovations applied through Design-Technology Co-Optimization (DTCO). These boosters enable similar density benefits while keeping yield and process cost under control.

<img width="1036" height="557" alt="image" src="https://github.com/user-attachments/assets/0b9bda2e-58f9-4ef5-950e-f989b2ce7c0f" />

<img width="1049" height="570" alt="image" src="https://github.com/user-attachments/assets/6a9213de-04e4-4a8f-b96a-614aa8689cc0" />

**A. Track Reduction (Fin Depopulation – in FinFET libraries)**

Track reduction improves standard-cell density by reducing the number of fins per transistor or lowering the height of the active region. This decreases the standard-cell height (track count), enabling more cells to fit vertically within the same silicon footprint. Although it provides a clear density advantage, fin depopulation may reduce drive current and impose energy-performance trade-offs, since fewer fins mean reduced effective channel width and hence lower $I_{\text{ON}}$

**B. Single Diffusion Break (SDB)**

Historically, a double diffusion break (DDB) formed by a dummy gate was required at the edges of standard cells to properly isolate the source/drain regions. As cell heights shrank, this dummy structure consumed a disproportionally larger percentage of total area.
The Single Diffusion Break (SDB) optimization removes this additional dummy spacing when adjacent cells are abutted. This eliminates unnecessary isolation padding, resulting in tighter packing along the x-direction and improving effective density at both cell and block level.

**C. Contact-Over-Active-Gate (COAG)**

In conventional layouts, the gate contact is placed in the spacing between PMOS and NMOS active regions. This spacing becomes a major limiter as nodes scale.
With COAG, the contact is landed directly on top of the active gate in a self-aligned manner. This removes the need for extended diffusion end-spacing and enables y-axis standard-cell height reduction, giving higher logic density without altering transistor geometry or device performance.

**D. Buried Power Rail (BPR)**

Traditional power rails ( $ V_{DD} $, $ V_{SS} $) run through the lowest back-end metal layers (M0/M1), consuming signal routing tracks.
Buried Power Rail (BPR) moves these rails below the device layer, freeing the BEOL tracks for signal routing. This allows even further cell-height scaling, increases routing resources, and reduces local IR-drop by shortening power-delivery paths. BPR is a foundational enabler for extremely compact future standard-cell designs, especially combined with Gate-All-Around architectures.

## Parasitic Resistance And Capacitance

**1. Parasitic Capacitance**

<img width="1046" height="571" alt="image" src="https://github.com/user-attachments/assets/34c437d4-ea5a-4aa4-bf4a-34e4055296f4" />

At 22 nm nodes, intrinsic gate oxide capacitance was still the dominant contributor to the total effective capacitance $C_{\text{eff}}$. However, as scaling continued into 14 nm → 10 nm → 7 nm, the plots clearly show that parasitic spacers and gate-to-contact coupling begin to dominate. Specifically, the sidewall spacer capacitance $C_{\text{s-ch}}$ and contact-to-gate capacitance $C_{\text{c-g}}$ together grow to 60–85% of $C_{\text{eff}}$ at 10 nm and below, while the pure oxide component drops under 20%. This means transistor delay and dynamic power are now heavily governed by unwanted fringing fields, not by the active channel.

Since switching delay and energy scale as:
  $\tau \propto C_{\text{eff}}$
  $E \propto C_{\text{eff}} \cdot V_{DD}^{2}$
even a few percent increase in parasitics causes direct performance penalties. The scatter plots in the slide illustrate that devices with a low-k spacer (SiBCN/air-spacer) show ~8% delay improvement and 15% reduction in $C_{\text{eff}}$, compared to conventional high-k SiON/SiCO spacers. The TEM images also show the air-gap implementation beneath the spacer — replacing a dielectric with air (k ≈ 1) provides the most aggressive reduction in fringing and coupling capacitance.

Thus, capacitance engineering has become a primary scaling vector. New materials, air spacers, and smaller gate-contact landing areas are now critical to ensure $C_{\text{eff}}$ does not rise as physical dimensions shrink.

**2. Parasitic Resistance**

<img width="1036" height="562" alt="image" src="https://github.com/user-attachments/assets/5e538986-d901-42e7-834e-3385a4480fef" />

Earlier planar MOSFETs maintained a balance where channel resistance $R_{\text{ch}}$ dominated conduction. But in modern 3D devices, scaling the gate length reduces $R_{\text{ch}}$ rapidly, while contact and access resistance $R_{\text{ext}}$ fail to scale at the same rate. The images show the geometry-driven shift between device architectures:

| Device | Effective Current Path Width ($\frac{W_C}{W_G}$) | Dominance |
|--------|--------------------------------------------------|-----------|
| **Planar MOSFET** | $\frac{W_C}{W_G} \approx 1$ | Channel-dominated |
| **FinFET** | $\frac{W_C}{W_G} \approx \frac{P}{2H_f + D_f} \approx \frac{1}{3}$ | Balanced |
| **GAAFET** | $\frac{W_C}{W_G} \approx \frac{1}{6}$ | Access-dominated |
| **CFET** | Multiple stacked channels → narrower path | Even worse access bottleneck |



Correspondingly, the resistance ratio shifts as:
  $\frac{R_{\text{ext}}}{R_{\text{ch}}} < 1$ (Planar)

  
  $\frac{R_{\text{ext}}}{R_{\text{ch}}} \approx 1$ (FinFET)

  
  $\frac{R_{\text{ext}}}{R_{\text{ch}}} \approx 3$ (GAAFET / CFET)

So even though GAA gives great electrostatic control, its narrower conduction width means contact and access resistance become the new bottleneck. Device performance is therefore less limited by mobility, and more limited by:

- contact interface quality

- source/drain resistance

- raised S/D epi design

- number of nanosheets and their stacking

- silicide/contact material resistivity

If $R_{\text{ext}}$ remains large, gains in $I_{\text{ON}}$ and $SS$ cannot be realized, meaning GAA scaling demands aggressive resistance engineering.

## Device Scaling

<img width="1037" height="558" alt="image" src="https://github.com/user-attachments/assets/b0df998c-dd2c-42fd-9b06-2060b7152f39" />

As gate lengths shrink into the sub-5 nm regime, conventional silicon transistors begin to encounter fundamental physical limits. When the channel becomes extremely short, electrons can directly tunnel from source to drain instead of going over the potential barrier. This source-to-drain tunneling increases leakage current exponentially, making it impossible to maintain low standby power. Suppressing tunneling requires channel materials with higher carrier effective mass ($m^*$), so that electrons behave less like waves and have lower penetration probability across the barrier.

At these scales, surface roughness and thickness fluctuations also have a strong impact on electrostatics, degrading the ability of the gate to control the channel. Therefore, the material must be atomically smooth and uniform so that the threshold voltage does not vary from device to device. Another critical factor is that capacitance from the drain ($C_D$) becomes comparable to or larger than gate oxide capacitance ($C_{OX}$), which increases the subthreshold slope and worsens off-state leakage. Reducing this requires materials with low in-plane dielectric constant ($\varepsilon$).

Because silicon cannot satisfy all these constraints simultaneously at such small dimensions, scaling pushes us toward new channel materials. Transition-Metal Dichalcogenides (TMDs)—such as$MoS_2$, $WS_2$, $MoTe_2$, $WSe_2$ provide the required properties:

- Atomically thin layers (1–3 atoms thick → perfect electrostatics)

- Higher effective mass ($m^*$) → reduced tunneling

- Tunable bandgap → optimized leakage–performance trade-off

These advantages have enabled TMD-based transistors to demonstrate gate lengths as small as 1 nm, using a carbon-nanotube gate electrode, while maintaining strong switching characteristics. Dual-gate MoS$2$ MOSFETs show up to 100× reduction in tunneling leakage when compared to Si devices, while achieving near-ideal subthreshold swing (~65 mV/dec) and **high $I{\text{ON}}/I_{\text{OFF}}$ ratios (~10⁶)**. This combination of ultra-short-channel operation and energy-efficient switching makes TMDs a highly promising option for future technology nodes when industry moves beyond the scaling limits of silicon.

## BEOL Innovations

While transistor scaling continues to deliver improvements in density and speed, the interconnect layers in the Back-End-Of-Line (BEOL) have become the dominant system-level bottleneck. As metal lines shrink, resistance increases sharply due to electron scattering in narrow structures, and capacitance does not scale at the same rate — leading to interconnect-dominated delay, power loss, and reliability challenges. To maintain overall chip performance, modern process nodes must rely on manufacturing and architectural innovations in BEOL rather than depending solely on device scaling.

<img width="1039" height="534" alt="image" src="https://github.com/user-attachments/assets/3d1b4d1e-2db6-4a12-bee4-83e4882bbd90" />

**1. Extending Copper Interconnect Scaling**

Copper (Cu) has served as the industry’s primary interconnect metal for decades, but at pitches ≤ 28 nm, its resistivity rises drastically due to:

- Surface and grain-boundary scattering

- Barrier/liner overhead consuming a larger fraction of cross-sectional area

Manufacturers have prolonged Cu usability through dual → single damascene transitions and barrier/via metal optimization, reducing via resistance by ~50%. These improvements help Cu remain viable down to ≈ 3 nm node, but beyond this, further scaling becomes cost-inefficient and resistivity-limited.

**2. Transition to Non-Copper Metals (Post-Cu Damascene Era)**

As Cu scaling approaches its physical limit, alternative metals such as Ru, Co, Mo, Rh, Ir are being adopted. Unlike copper, these metals can be used barrier-less in subtractive patterning processes, enabling taller and more conductive lines at extremely tight pitches.

Benefits of Post-Cu interconnect metals:

- Improved electromigration reliability, enabling longer operational lifetime

- Lower resistivity at nanoscale due to reduced scattering

- Barrier-less integration → more conductive cross-section
This transition ensures interconnect performance continues to scale even when Cu stagnates.

**3. Back-Side Power Delivery Network (BS-PDN)**

In classical Front-Side PDN (FS-PDN), power and signal lines compete for limited routing area in BEOL, creating severe IR-drop and routing congestion.
Back-Side PDN solves this by relocating power vias through the backside of the wafer, separating power delivery from signal interconnects.

Advantages demonstrated in measurements:

- IR-drop reduction (≈ 23–95% improvement in static and dynamic IR drop)

- More front-side routing tracks for signals → improved timing and reduced RC delay

- Standard-cell height reduction (6T → 5T libraries), increasing logic density

By decoupling power and signaling layers, BS-PDN provides both power integrity and layout density benefits, making it a key enabler for nodes below 2 nm.

<img width="1048" height="565" alt="image" src="https://github.com/user-attachments/assets/122f113d-4d47-4e6c-8aaf-a735d9964aca" />

## Lab Implementations 1

**ASAP 7nm PDK**

The ASAP 7nm Process Design Kit (PDK) is an open-source, academic design kit developed to model the characteristics of a 7 nm FinFET technology node. Instead of providing confidential foundry-specific details, ASAP7 delivers predictive transistor and interconnect models that allow researchers and designers to explore advanced-node design techniques without proprietary access restrictions.

ASAP7 includes complete design rules, device models, standard-cell libraries, and interconnect stacks, enabling accurate optimization of PPA — Performance, Power, Area. The kit also supports industry-standard EDA flows, making it suitable for RTL-to-GDSII demonstrations, architecture exploration, and CAD research.

**Characterization of CMOS VTC**

**Nfet Id and Vd Characteristics**

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/6d85cf93-5988-46aa-aa4d-3446105a12b5" />

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/6fac87ae-e0b1-401c-a204-448723b4a676" />

**Plot of Id vs Vd**

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/5b993665-493a-4e9a-8fac-a1779336fe2d" />

**Schematic of Nfet**

<img width="861" height="606" alt="image" src="https://github.com/user-attachments/assets/36b634d5-937c-4c4d-bb5f-4c3989ed9f7b" />

**CMOS Inverter_vtc Characteristics**

Inverter_vtc.spice file

```
** sch_path: /home/hprcse/Finfet/inverter_vtc.sch
**.subckt inverter_vtc
Xpfet1 nfet_out nfet_in vdd vdd asap_7nm_pfet l=7e-009 nfin=14
Xnfet1 nfet_out nfet_in GND GND asap_7nm_nfet l=7e-009 nfin=14
V1 nfet_in GND pulse(0 0.7 20p 10p 10p 20p 500p 1)
V2 vdd GND 0.7
**** begin user architecture code


.dc v1 0 0.7 1m
.control
* First run DC
    dc v1 0 0.7 1m
    run
        * DC measurements
    meas dc v_th when nfet_out = nfet_in
    plot nfet_out nfet_in
    
    
    
    let gain_av = abs(deriv(nfet_out))
    meas dc max_gain max gain_av
    plot gain_av
    
    let gain_target = max_gain * 0.999
    meas dc vil find nfet_in when gain_av = gain_target cross=1
    meas dc voh find nfet_out when gain_av = gain_target cross=1
    meas dc vih find nfet_in when gain_av = gain_target cross=2
    meas dc vol find nfet_out when gain_av = gain_target cross=2
    let nmh = voh - vih
    let nml = vil - vol
    print v_th max_gain vil voh vih vol nmh nml
    
    *Transconductance
    
    let id = v2#branch
    plot id
    let gm = real(deriv(id, nfet_in))
    plot gm
    meas dc gm_max MAX gm
    
    let r_out= deriv(nfet_out,id)
    plot r_out
    
    
    * Transient measurements
    tran 1e-12 100e-12
    meas tran tpr when nfet_in = 0.35 rise = 1
    meas tran tpf when nfet_out = 0.35 fall = 1
    let tp = (tpr + tpf) / 2
    let trans_current = v2#branch
    meas tran id_pwr integ trans_current from=2e-11 to=6e-11
    let pwr = id_pwr * 0.7
    let power = abs(pwr / 40e-12)
    print tpr tpf tp id_pwr pwr power
  
    tran 0.1 100p                         
    meas tran tr when nfet_in=0.07 RISE=1  
    meas tran tf when nfet_out=0.63 FALL=1 
    let t_delay = tr + tf                  
    print t_delay                         
    let f = 1/t_delay                     
    print f 
    
    ** Trasient Drain current, Id
    let Id_transient = v2#branch
    plot Id_transient
    meas tran Id_peak_transient min Id_transient

    ** Total Energy, Avg. Power per cycle
    * Integral t1 to t2:
    *   t1 = start of pulse waveform (=PULSE_TD)
    *   t2 = end   of pulse waveform (= t1 + [tr+pw+tf])
    let t1 = 20p
    let t2 = t1 + (10p+40p+10p)
    meas TRAN Integral_Id INTEG Id_transient from={t1} to={t2}
    let energy_per_cycle = abs(Integral_Id * VDD_V)
    let avg_power = (energy_per_cycle / 60e-12)
    
    set xbrushwidth=3
    plot nfet_out nfet_in
    meas dc v_th when nfet_out=nfet_in
    
    
    
.endc


**** end user architecture code
**.ends
.GLOBAL GND
**** begin user architecture code

.subckt asap_7nm_pfet S G D B l=7e-009 nfin=14
	npmos_finfet S G D B BSIMCMG_osdi_P l=7e-009 nfin=14
.ends asap_7nm_pfet

.model BSIMCMG_osdi_P BSIMCMG_va (
+ TYPE = 0

************************************************************
*                         general                          *
************************************************************
+version = 107             bulkmod = 1               igcmod  = 1               igbmod  = 0
+gidlmod = 1               iimod   = 0               geomod  = 1               rdsmod  = 0
+rgatemod= 0               rgeomod = 0               shmod   = 0               nqsmod  = 0
+coremod = 0               cgeomod = 0               capmod  = 0               tnom    = 25
+eot     = 1e-009          eotbox  = 1.4e-007        eotacc  = 3e-010          tfin    = 6.5e-009
+toxp    = 2.1e-009        nbody   = 1e+022          phig    = 4.9278          epsrox  = 3.9
+epsrsub = 11.9            easub   = 4.05            ni0sub  = 1.1e+016        bg0sub  = 1.17
+nc0sub  = 2.86e+025       nsd     = 2e+026          ngate   = 0               nseg    = 5
+l       = 2.1e-008        xl      = 1e-009          lint    = -2.5e-009       dlc     = 0
+dlbin   = 0               hfin    = 3.2e-008        deltaw  = 0               deltawcv= 0
+sdterm  = 0               epsrsp  = 3.9             nfin    = 1
+toxg    = 1.8e-009
************************************************************
*                            dc                            *
************************************************************
+cit     = 0               cdsc    = 0.003469        cdscd   = 0.001486        dvt0    = 0.05
+dvt1    = 0.36            phin    = 0.05            eta0    = 0.094           dsub    = 0.24
+k1rsce  = 0               lpe0    = 0               dvtshift= 0               qmfactor= 0
+etaqm   = 0.54            qm0     = 2.183e-012      pqm     = 0.66            u0      = 0.0237
+etamob  = 4               up      = 0               ua      = 1.133           eu      = 0.05
+ud      = 0.0105          ucs     = 0.2672          rdswmin = 0               rdsw    = 200
+wr      = 1               rswmin  = 0               rdwmin  = 0               rshs    = 0
+rshd    = 0               vsat    = 60000           deltavsat= 0.17            ksativ  = 1.592
+mexp    = 2.491           ptwg    = 25              pclm    = 0.01            pclmg   = 1
+pdibl1  = 800             pdibl2  = 0.005704        drout   = 4.97            pvag    = 200
+fpitch  = 2.7e-008        rth0    = 0.15            cth0    = 1.243e-006      wth0    = 2.6e-007
+lcdscd  = 0               lcdscdr = 0               lrdsw   = 1.3             lvsat   = 1441
************************************************************
*                         leakage                          *
************************************************************
+aigc    = 0.007           bigc    = 0.0015          cigc    = 1               dlcigs  = 5e-009
+dlcigd  = 5e-009          aigs    = 0.006           aigd    = 0.006           bigs    = 0.001944
+bigd    = 0.001944        cigs    = 1               cigd    = 1               poxedge = 1.152
+agidl   = 2e-012          agisl   = 2e-012          bgidl   = 1.5e+008        bgisl   = 1.5e+008
+egidl   = 1.142           egisl   = 1.142
************************************************************
*                            rf                            *
************************************************************
************************************************************
*                         junction                         *
************************************************************
************************************************************
*                       capacitance                        *
************************************************************
+cfs     = 0               cfd     = 0               cgso    = 1.6e-010        cgdo    = 1.6e-010
+cgsl    = 0               cgdl    = 0               ckappas = 0.6             ckappad = 0.6
+cgbo    = 0               cgbl    = 0
************************************************************
*                       temperature                        *
************************************************************
+tbgasub = 0.000473        tbgbsub = 636             kt1     = 0               kt1l    = 0
+ute     = -1.2            utl     = 0               ua1     = 0.001032        ud1     = 0
+ucste   = -0.004775       at      = 0.001           ptwgt   = 0.004           tmexp   = 0
+prt     = 0               tgidl   = -0.007          igt     = 2.5
************************************************************
*                          noise                           *
************************************************************
**)
.control
pre_osdi /home/vsduser/Desktop/asap_7nm_Xschem/bsimcmg.osdi
.endc



.subckt asap_7nm_nfet S G D B l=7e-009 nfin=14
	nnmos_finfet S G D B BSIMCMG_osdi_N l=7e-009 nfin=14
.ends asap_7nm_nfet

.model BSIMCMG_osdi_N BSIMCMG_va (
+ TYPE = 1
************************************************************
*                         general                          *
************************************************************
+version = 107             bulkmod = 1               igcmod  = 1               igbmod  = 0
+gidlmod = 1               iimod   = 0               geomod  = 1               rdsmod  = 0
+rgatemod= 0               rgeomod = 0               shmod   = 0               nqsmod  = 0
+coremod = 0               cgeomod = 0               capmod  = 0               tnom    = 25
+eot     = 1e-009          eotbox  = 1.4e-007        eotacc  = 1e-010          tfin    = 6.5e-009
+toxp    = 2.1e-009        nbody   = 1e+022          phig    = 4.2466          epsrox  = 3.9
+epsrsub = 11.9            easub   = 4.05            ni0sub  = 1.1e+016        bg0sub  = 1.17
+nc0sub  = 2.86e+025       nsd     = 2e+026          ngate   = 0               nseg    = 5
+l       = 2.1e-008        xl      = 1e-009          lint    = -2e-009         dlc     = 0
+dlbin   = 0               hfin    = 3.2e-008        deltaw  = 0               deltawcv= 0
+sdterm  = 0               epsrsp  = 3.9             nfin    = 1
+toxg    = 1.80e-009
************************************************************
*                            dc                            *
************************************************************
+cit     = 0               cdsc    = 0.01            cdscd   = 0.01            dvt0    = 0.05
+dvt1    = 0.47            phin    = 0.05            eta0    = 0.07            dsub    = 0.35
+k1rsce  = 0               lpe0    = 0               dvtshift= 0               qmfactor= 2.5
+etaqm   = 0.54            qm0     = 0.001           pqm     = 0.66            u0      = 0.0303
+etamob  = 2               up      = 0               ua      = 0.55            eu      = 1.2
+ud      = 0               ucs     = 1               rdswmin = 0               rdsw    = 200
+wr      = 1               rswmin  = 0               rdwmin  = 0               rshs    = 0
+rshd    = 0               vsat    = 70000           deltavsat= 0.2             ksativ  = 2
+mexp    = 4               ptwg    = 30              pclm    = 0.05            pclmg   = 0
+pdibl1  = 0               pdibl2  = 0.002           drout   = 1               pvag    = 0
+fpitch  = 2.7e-008        rth0    = 0.225           cth0    = 1.243e-006      wth0    = 2.6e-007
+lcdscd  = 5e-005          lcdscdr = 5e-005          lrdsw   = 0.2             lvsat   = 0
************************************************************
*                         leakage                          *
************************************************************
+aigc    = 0.014           bigc    = 0.005           cigc    = 0.25            dlcigs  = 1e-009
+dlcigd  = 1e-009          aigs    = 0.0115          aigd    = 0.0115          bigs    = 0.00332
+bigd    = 0.00332         cigs    = 0.35            cigd    = 0.35            poxedge = 1.1
+agidl   = 1e-012          agisl   = 1e-012          bgidl   = 10000000        bgisl   = 10000000
+egidl   = 0.35            egisl   = 0.35
************************************************************
*                            rf                            *
************************************************************
************************************************************
*                         junction                         *
************************************************************
************************************************************
*                       capacitance                        *
************************************************************
+cfs     = 0               cfd     = 0               cgso    = 1.6e-010        cgdo    = 1.6e-010
+cgsl    = 0               cgdl    = 0               ckappas = 0.6             ckappad = 0.6
+cgbo    = 0               cgbl    = 0
************************************************************
*                       temperature                        *
************************************************************
+tbgasub = 0.000473        tbgbsub = 636             kt1     = 0               kt1l    = 0
+ute     = -0.7            utl     = 0               ua1     = 0.001032        ud1     = 0
+ucste   = -0.004775       at      = 0.001           ptwgt   = 0.004           tmexp   = 0
+prt     = 0               tgidl   = -0.007          igt     = 2.5
************************************************************
*                          noise                           *
************************************************************
**)
.control
pre_osdi /home/vsduser/Desktop/asap_7nm_Xschem/bsimcmg.osdi
.endc


**** end user architecture code
.end
```

**Switching Threshold Voltage**

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/c3be29ae-e9cf-4103-9295-e76cb9932ab3" />

```
meas dc v_th when nfet_out = nfet_in
plot nfet_out nfet_in
```

**Drain Current (Id)**

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/2ed55613-68a3-42c8-84c5-0a13bb4d7fec" />


```
let id = v2#branch
plot id
```
**Power Consumption**

Average power is obtained by integrating the transient drain current over one switching cycle, multiplying by $V_{DD}$, and dividing by the signal period.

```
let trans_current = v2#branch
meas tran id_pwr integ trans_current from=20e-12 to=60e-12
let pwr = id_pwr *0.7
let power = abs(pwr/40)
print power
```

**Propagation Delay (Tp)**

Propagation delay of a logic gate (e.g., an inverter) is the time difference between the input reaching 50% of its transition and the output reaching 50% of its corresponding transition.
Rise time ($t_r$) is the time it takes the output to move from 10% → 90% of its final high level, while fall time ($t_f$) is the time taken to move from 90% → 10% of the high level.
Some design methodologies instead use 30% ↔ 70% thresholds depending on the specification requirements.

```
meas tran tpr when nfet_in=0.35 RISE=1 
meas tran tpf when nfet_out=0.35 FALL=1 
let tp = (tpf + tpr)/2 
print tp 
```

**Gain (Av)**

Gain represents how much the output voltage changes in response to a small change at the input essentially the ratio of output variation to input variation.

```
let gain_av=deriv(nfet_out) : this gives out negative gain

let gain_av=abs(deriv(nfet_out)) : Gives the absolute value of gain.
plot gain
```

**Noise Margin**

Noise margin represents how much noise the VTC can tolerate without corrupting digital logic levels.
NMH = $V_{OH} - V_{IH}$ ensures a valid logic-high;
NML = $V_{IL} - V_{OL}$ ensures a valid logic-low.
Higher margins → better noise immunity.

```
meas dc vil find nfet_in when gain_av = gain_target cross=1
meas dc voh find nfet_out when gain_av = gain_target cross=1
meas dc vih find nfet_in when gain_av = gain_target cross=2
meas dc vol find nfet_out when gain_av = gain_target cross=2
let nmh = voh - vih
let nml = vil - vol
print v_th max_gain vil voh vih vol nmh nml
```

**Transconductance (Gm)**

Transconductance is defined as the ratio of change in drain current and change in Vgs (Gate-source Voltage).

```
let gm = real(deriv(id, nfet_in))
plot gm
meas dc gm_max MAX gm
```

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/32c47faf-53e0-4fb1-a690-b3790e1962cf" />

**Frequency (f)**

```
tran 0.1 100p                         
meas tran tr when nfet_in=0.07 RISE=1  
meas tran tf when nfet_out=0.63 FALL=1 
let t_delay = tr + tf                  
print t_delay                         
let f = 1/t_delay                     
print f 
```
**Output Resistance**

The output resistance is defined as the ratio of output node voltage and the change in drain current.

```
let r_out= deriv(nfet_out,id)   
plot r_out                      
```

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/6cbf80b3-3420-4e9f-baac-eb9ab069bfa5" />

**Transient Analysis: Vin, Vout waveforms**

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/d4fd7920-f256-4662-bbbb-0a1fe14645cf" />

```
tran 1e-12 100e-12
meas tran tpr when nfet_in = 0.35 rise = 1
meas tran tpf when nfet_out = 0.35 fall = 1
let tp = (tpr + tpf) / 2
let trans_current = v2#branch
meas tran id_pwr integ trans_current from=2e-11 to=6e-11
let pwr = id_pwr * 0.7
let power = abs(pwr / 40e-12)
print tpr tpf tp id_pwr pwr power
```

**Switching Energy, Avg. Power**

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/826d5c0f-7b40-47d3-88a1-c151849287e6" />

```
let Id_transient = v2#branch
plot Id_transient
meas tran Id_peak_transient min Id_transient

** Total Energy, Avg. Power per cycle
* Integral t1 to t2:
*   t1 = start of pulse waveform (=PULSE_TD)
*   t2 = end   of pulse waveform (= t1 + [tr+pw+tf])
let t1 = 20p
let t2 = t1 + (10p+40p+10p)
meas TRAN Integral_Id INTEG Id_transient from={t1} to={t2}
let energy_per_cycle = abs(Integral_Id * VDD_V)
let avg_power = (energy_per_cycle / 60e-12)
```

## Lab Implementations 2

**Design of a BandGap Reference Circuit**

<img width="886" height="558" alt="image" src="https://github.com/user-attachments/assets/e7a68144-a1fc-4960-94c7-17b0bf9102b2" />

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/20bf6303-682f-49a6-b3c6-3275c0fdc452" />

**VCTAT**

<img width="654" height="547" alt="image" src="https://github.com/user-attachments/assets/f25c3923-be5f-4e6c-aa73-564e85a2020e" />

**VPTAT**

<img width="677" height="568" alt="image" src="https://github.com/user-attachments/assets/76e99f7d-8ca3-4a2e-aba2-d6601e3e205b" />

**VREF**

<img width="650" height="545" alt="image" src="https://github.com/user-attachments/assets/1e83335b-b9d9-4032-8351-e3d79c87beaa" />

**d(vref/dT)**

<img width="654" height="553" alt="image" src="https://github.com/user-attachments/assets/69d45eb1-7a94-46a7-baa6-5f4e3f4f4113" />

**VDD = 1V, Temp = 27C**

**VREF**

<img width="639" height="540" alt="image" src="https://github.com/user-attachments/assets/b6e82712-d2e4-497c-99f1-0e3ec40f0b24" />

**VPTAT**

<img width="642" height="527" alt="image" src="https://github.com/user-attachments/assets/47fdec4c-3bb1-47da-93d4-6312cd6733d1" />

**VCTAT**

<img width="660" height="541" alt="image" src="https://github.com/user-attachments/assets/53e17ea8-6ff0-47d5-b975-249559d0000e" />







































