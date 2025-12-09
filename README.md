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

## Lab Implementations 

**ASAP 7nm PDK**

The ASAP 7nm Process Design Kit (PDK) is an open-source, academic design kit developed to model the characteristics of a 7 nm FinFET technology node. Instead of providing confidential foundry-specific details, ASAP7 delivers predictive transistor and interconnect models that allow researchers and designers to explore advanced-node design techniques without proprietary access restrictions.

ASAP7 includes complete design rules, device models, standard-cell libraries, and interconnect stacks, enabling accurate optimization of PPA — Performance, Power, Area. The kit also supports industry-standard EDA flows, making it suitable for RTL-to-GDSII demonstrations, architecture exploration, and CAD research.












