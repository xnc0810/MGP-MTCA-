# Integrated Experimental Verification Scheme for Polarization State Primitive Operations and WDM Parallel Computing
*Version 1.1*

---

## Core Design Concept of the Scheme

This scheme adopts the core logic of photonic computing — **"medium as channel, field as operator"** — completely breaking the dependence of photonic computing on customized rare-earth-doped crystals and abandoning the "cube-like" single-medium packaging approach.

The essence of polarization-based computing lies in the superposition, rotation, and tensor evolution of polarization states in space. This physical process can be directly implemented by cascading commercial polarization optical components, enabling the PDMM architecture to feature **Lego-style flexible construction**: standardized devices such as thin-film polarizers and micro-waveplate arrays serve as independent "polarization operator modules", which can be cascaded on demand on a common optical path platform, allowing plug-and-play functionality. Algorithm logic only needs to be converted into polarization state evolution paths, and the optical path can be flexibly reconfigured according to computing requirements.

At the same time, constrained by the limitations of photonic computing’s physical-layer optical field evolution and device coupling characteristics, this scheme completely bypasses the barrier of missing EDA simulation tools. It uses **Jones matrices as the sole "source of truth and instruction set"** — all addition, subtraction, multiplication, and accumulation operations can be directly derived via Jones matrices and then verified through physical experiments, forming a complete engineering closed loop of "theoretical derivation → physical implementation → data quantification".

The scheme targets the **1550 nm communication band**, fully utilizing mature commercial components from the optical communication industry chain. It is cost-controlled, environmentally compatible, and can be implemented in an ordinary optical laboratory. The verification results can directly provide measured evidence for the engineering implementation of photonic computing, making it the optimal path for low-cost, high-efficiency verification of polarization-based photonic computing.

---

## 1. Core Experimental Objectives

1.  Verify the physical feasibility of polarization state adders and subtractors, and implement the physical realization of basic operation primitives for photonic computing.
2.  Based on polarization addition/subtraction primitives, realize direct physical-layer computation of small-dimension 2×2/4×4 matrices, and verify the advantages in accuracy, energy consumption, and latency compared to silicon-based computing.
3.  Verify the computing power expansion effect of wavelength division multiplexing (WDM) in polarization-based computing, implement true physical parallel operations on multi-wavelength orthogonal channels, and quantify the linear expansion efficiency of computing power with the number of wavelengths.
4.  Verify the feasibility of "Lego-style" cascading of commercial devices, and form a reusable and reconfigurable methodology for building polarization-based computing optical paths.

---

## 2. Core Experimental Principles

This experiment uses the 1550 nm communication band as the operating window. Relying on the linear operation rules of Jones matrices, all mathematical operations are converted into the physical evolution of polarization states, and parallel computing is realized by combining WDM technology. The three core modules support each other and can be verified simultaneously. All logic is based on mature photonics theory, with no complex simulation dependencies.

### 2.1 Polarization State Adder/Subtractor: Jones Matrix-Driven Physical Primitive Operations

A polarization state is uniquely characterized by the electric vector vibration direction and amplitude of light. Its corresponding Jones matrix satisfies the linear addition and subtraction rules, which can be decomposed through physical superposition or reverse modulation of polarization states to directly implement physical-layer addition and subtraction operations on numerical values, providing core primitives for subsequent matrix computations without any intermediate digital-domain operations.

1.  **Polarization State Adder**: Map two values to be added, $X_1$ and $X_2$, proportionally to the light intensity/polarization angle parameters in the $x$ and $y$ orthogonal polarization directions, converting them into corresponding Jones matrices $J_1$ and $J_2$. Use a polarization beam combiner to couple two beams of incoherent, same-wavelength polarized light into the same optical path, completing the physical linear superposition of polarization states and obtaining the combined Jones matrix $J = J_1 + J_2$. A polarization-sensitive PD detector captures the light intensity and polarization characteristics of the combined polarization state, which are then converted back into the numerical addition result $X = X_1 + X_2$ via Jones matrix inversion, forming a closed-loop operation of "value → polarization state → physical superposition → value".
2.  **Polarization State Subtractor**: Map the minuend $X_0$ and subtrahend $X_\Delta$ to the reference polarization state Jones matrix $J_0$ and the offset polarization state Jones matrix $J_\Delta$, respectively. Use a micro-waveplate array/SLM to perform reverse polarization angle modulation on the offset polarization state to obtain the inverse Jones matrix $-J_\Delta$. Superimpose $J_0$ and $-J_\Delta$ linearly via a polarization beam combiner to complete the Jones matrix subtraction operation $J = J_0 - J_\Delta$. A polarization-sensitive PD detector captures the characteristic changes in the superimposed polarization state to derive the numerical subtraction result $X = X_0 - X_\Delta$. The operation delay is determined solely by the speed of light propagation.

The accuracy of this module is determined by polarization modulation and detection precision, and commercial devices can achieve an operation error within ±1%. The experimental phenomena are intuitive, easy to observe, and easy to calibrate.

### 2.2 Matrix Multiplication Driven by Polarization State Primitives: Direct Physical-Layer Operator Mapping

The essence of matrix multiplication is the multiply-accumulate (MAC) operation of "row × column". This experiment completely decomposes it into polarization state modulation and superposition, using polarization state adders as core primitives to realize direct physical-layer computation of small-dimension matrices, replacing the step-by-step instruction fetching, scheduling, and operations of traditional silicon-based computing.

1.  Precisely map each element of the weight matrix $A$ to the polarization rotation angle and light intensity modulation parameters of the SLM/micro-waveplate array, converting them into the polarization modulation matrix $M_A$. This matrix, a combination of Jones matrices, acts directly as the physical-layer "multiplication operator".
2.  Map the input vector matrix $B$ to the initial polarization state of the incident light, whose Jones matrix $J_B$ serves as the computation input.
3.  As the incident light passes through the polarization modulation module, the polarization state completes the modulation operation $M_A \times J_B$ at the physical layer, corresponding to the "multiplication" step of matrix multiplication.
4.  The modulated multi-beam polarized light is guided into the polarization state adder to complete physical-layer linear superposition, corresponding to the "accumulation" step of matrix multiplication.
5.  Finally, a polarization-sensitive PD detector captures the Jones matrix of the synthesized polarization state, which is converted back into the numerical result of the matrix product $C = A \times B$.

Throughout the process, each multiply-accumulate operation of the matrix is a natural physical evolution of the polarization state, with no intermediate digital-domain operations. The computing power loss only stems from the inherent losses of optical devices, resulting in an energy consumption reduction of 2–3 orders of magnitude compared to silicon-based computing.

### 2.3 Wavelength Division Multiplexing Parallel Computing: Linear Expansion of Computing Power via Wavelength Incoherence Orthogonality

Introducing wavelength incoherence orthogonality, multiple parallel computing channels are built on the same physical optical path without increasing optical path volume or improving single-device precision, realizing true physical parallel operations of multiple sets of polarization primitive operations/matrix computations. This directly verifies the characteristic that photonic computing power grows linearly with the number of wavelengths.

1.  Select three commercial incoherent narrow-linewidth wavelengths within the 1550 nm band: 1548 nm, 1550 nm, and 1552 nm. Each wavelength corresponds to an independent orthogonal computing channel. Each channel is composed of the same cascaded commercial devices for "polarization modulation + addition/subtraction operations + detection", and can independently complete the full process from "polarization state addition/subtraction" to "matrix multiplication".
2.  Use a wavelength division multiplexer (WDM) to couple multi-wavelength polarized light into the same fused silica medium optical path, which only acts as a transmission channel for optical signals with no customized doping requirements. Due to wavelength incoherence, the polarization states of each channel do not interfere or crosstalk, enabling true physical parallelism.
3.  After optical signal transmission, the multi-wavelength signals are separated by a demultiplexer (DEMUX), and the operation results of each channel are detected by a PD array.
4.  Quantify the computing power expansion efficiency by comparing the total computation volume and operation time under single-wavelength and multi-wavelength conditions, verifying the design logic that "computing power expands linearly with the number of wavelengths $N$".

---

## 3. Experimental Hardware System

### 3.1 Core Hardware List

| Module | Components | Specifications & Functions |
|---|---|---|
| **Light Source Module** | Narrow-linewidth DFB laser array | 1548 nm / 1550 nm / 1552 nm, power ≤ 10 mW, commercial off-the-shelf. Function: Provide multi-wavelength incoherent incident light. |
| **Polarization Modulation Module** | Liquid crystal SLM, micro-waveplate array, thin-film polarizer | 1550 nm compatible, polarization rotation accuracy ±0.5°, independently cascaded. Function: Realize polarization state rotation/reverse modulation, mapping operator matrices. |
| **Polarization Operation Module** | Polarization beam combiner/splitter | 1550 nm band, polarization extinction ratio ≥ 30 dB. Function: Complete superposition/separation of polarization states to implement addition and subtraction operations. |
| **WDM Module** | WDM/DEMUX | 3-channel, 1548/1550/1552 nm, commercial passive devices. Function: Implement coupling and separation of multi-wavelength optical signals. |
| **Transmission Channel** | Fused silica plate, single-mode fiber | 1550 nm low-loss, commercial off-the-shelf, no doping required. Function: Only serve as optical signal transmission media. |
| **Detection Module** | Polarization-sensitive PD detector array | 1550 nm compatible, response speed ≥ 100 MHz, synchronous detection capability. Function: Capture polarization state characteristics and convert them into electrical signals. |
| **Auxiliary Module** | Optical collimator, fiber jumper, optical mount | 1550 nm compatible, common optical platform accessories. Function: Implement device cascading and optical path alignment. |

#### Key Device Selection Reference & Low-Cost Alternatives

To adapt to the equipment reserve and cost budget of ordinary optical laboratories, the core commercial devices are supplemented with entry-level model references and low-cost alternatives, with the total budget of the full set of core equipment controllable within 50,000–100,000 RMB:

-   **DFB Laser Array**: Reference model (Huawei 1550 nm DFB laser, power 5–10 mW); Alternative: Independently purchased ordinary 1550 nm fiber-coupled lasers combined into a multi-wavelength light source.
-   **Liquid Crystal SLM**: Reference model (Holoeye PLUTO-2 1550 nm version); Alternative: High-precision micro-waveplate array + electric rotating stage (meeting the polarization angle modulation accuracy of ±0.5°).
-   **Polarization-Sensitive PD Array**: Reference model (Thorlabs PDA20H2 1550 nm); Alternative: Single-channel polarization-sensitive PD + optical switch (realizing time-division detection of multiple channels for low-budget scenarios).
-   All devices are selected for full compatibility with the 1550 nm communication band to ensure optical signal loss ≤ 0.5 dB/km and avoid polarization state distortion caused by band mismatch.

### 3.2 Lego-Style Optical Path Construction Principles

1.  **Modular Independence**: All devices are independent modules fixed on an ordinary vibration-isolated optical platform using optical mounts, with no welding or packaging required. They can be individually disassembled or replaced.
2.  **On-Demand Cascading**: From single-wavelength polarization addition/subtraction to matrix computation and multi-wavelength parallelism, only modulation/operation/WDM modules need to be added step-by-step to the basic optical path without reconstructing the entire path.
3.  **Simple Coaxial Calibration**: All optical paths are linear and coaxial. Coaxial alignment can be achieved quickly by rough adjustment with a laser pointer and fine adjustment with an optical power meter, accessible to ordinary experimenters.
4.  **Flexible Algorithm Adaptation**: Different algorithms only require adjusting the polarization modulation parameters of the SLM/waveplate array (i.e., changing the Jones matrix mapping relationship), without replacing hardware devices, realizing "algorithm changes, optical path unchanged".

#### Experimental Personnel Configuration & Operation Division

Adapted for a 2–3 person experimental team, with clear division of labor to improve experimental efficiency; all operators only need to master basic polarization optics knowledge and basic Jones matrix operations, without advanced professional background in photonics:

1.  1 Person: Optical path construction and calibration (responsible for device fixation, coaxiality adjustment, and abnormal troubleshooting).
2.  1–2 Persons: Parameter modulation and data acquisition (responsible for SLM/waveplate parameter setting, PD data recording, Jones matrix calculation, and result analysis).

---

## 4. Experimental Verification Process

This experiment adopts a layered progressive logic of "single-wavelength primitive verification → single-wavelength matrix computation verification → multi-wavelength parallel verification". The three stages can be carried out simultaneously and mutually verified. All steps have clear operational standards and quantitative indicators, and can be directly replicated in ordinary optical laboratories.

### Stage 1: Single-Wavelength Polarization State Adder/Subtractor Primitive Verification (1–2 Days)

1.  **Optical Path Construction**: Single-wavelength DFB laser → optical collimator → thin-film polarizer → polarization beam splitter → micro-waveplate array → polarization beam combiner → polarization-sensitive PD → data acquisition instrument.
2.  **Parameter Mapping**: Select three different values (0.2, 0.5, 0.8), map them to the polarization angle/light intensity parameters of two polarized beams, and derive the corresponding Jones matrices $J_1$, $J_2$, and the theoretical combined matrix $J$.
3.  **Addition Experiment**: Turn on the laser, modulate the two polarization states via the waveplate array, superimpose them through the combiner, detect the combined polarization state characteristics with the PD, derive the actual addition result, compare it with the theoretical value, and calculate the operation error.
4.  **Subtraction Experiment**: Perform reverse modulation on one of the polarization states via the waveplate array to obtain $-J_2$. Repeat the superposition and detection steps to derive the actual subtraction result, compare it with the theoretical value, and calculate the operation error.
5.  **Accuracy Calibration**: If the error exceeds ±1%, calibrate by fine-tuning the waveplate angles, record the calibrated polarization angle-voltage/value mapping relationship, and form a primitive operation calibration table.

**Verification Indicators**: Addition/subtraction operation error ≤ ±1%; polarization state evolution is consistent with Jones matrix derivation.

### Stage 2: Single-Wavelength Polarization Primitive-Driven Matrix Multiplication Verification (2–3 Days)

1.  **Optical Path Expansion**: Add a liquid crystal SLM to the primitive operation optical path from Stage 1, building the matrix computation optical path: laser → collimator → SLM → polarization beam combiner/adder → PD → data acquisition instrument.
2.  **Matrix Mapping**: Select two sets of 2×2 random real matrices. Map the elements of matrix $A$ to the polarization rotation angle parameters of the SLM, derive the corresponding polarization modulation matrix $M_A$, map matrix $B$ to the initial polarization state $J_B$ of the incident light, and calculate the theoretical product $C = A \times B$.
3.  **Physical Computation**: Turn on the laser, set the SLM modulation parameters, allow the incident light to complete polarization modulation via the SLM, then complete multiply-accumulate operations via the adder. The PD detects the characteristics of the synthesized polarization state to derive the actual matrix product result.
4.  **Comparative Verification**: Compare the experimental results with those from a silicon-based calculator to calculate the operation error. Simultaneously measure the energy consumption and latency of the entire module, comparing them with silicon-based MCUs/FPGAs of the same computing power.
5.  **Multi-Group Verification**: Replace 3–5 different matrices and repeat the steps to verify the stability and versatility of the matrix computation.

**Verification Indicators**: Matrix operation error ≤ ±1.5%; energy consumption reduced by 2–3 orders of magnitude compared to silicon-based modules of the same computing power; operation latency ≤ 1 μs.

### Stage 3: WDM Multi-Wavelength Parallel Computing Verification (2–3 Days)

1.  **Optical Path Expansion**: Add a laser array, WDM, DEMUX, and PD detector array to the single-wavelength matrix computation optical path from Stage 2, building a 3-wavelength parallel computing optical path: 3 independent modulated single-wavelength matrix computation paths → MUX coupling into one optical signal → fused silica plate transmission → DEMUX separation into 3 paths → synchronous detection by PD array → multi-channel data acquisition instrument.
2.  **Parallel Assignment**: Assign different 2×2 matrix computation tasks to each of the three wavelength channels, setting the SLM modulation parameters for each channel.
3.  **Parallel Operation**: Turn on the laser array, start modulation and operations for all channels simultaneously. The PD array synchronously detects the operation results of each channel, and the data acquisition instrument records the total operation time.
4.  **Computing Power Quantification**: Compare the operation time of a single channel with that of three parallel channels to calculate parallel efficiency. Verify that "the total computing power of three channels ≈ 3 × single-channel computing power", i.e., linear expansion of computing power with the number of wavelengths. Simultaneously detect crosstalk between channels to ensure a crosstalk suppression ratio ≥ 30 dB.
5.  **Robustness Verification**: Run continuously for 72 hours, recording the operation accuracy and stability of each channel to verify the engineering robustness of Lego-style device cascading and WDM.

**Verification Indicators**: Multi-wavelength parallel efficiency ≥ 90%; inter-channel crosstalk suppression ratio ≥ 30 dB; operation error fluctuation ≤ ±0.5% during 72 hours of continuous operation.

---

## 5. Data Acquisition and Analysis Requirements

1.  **Data Acquisition**: All experimental data are recorded by a high-precision data acquisition instrument, including polarization angle/light intensity parameters, addition/subtraction/matrix operation results, operation time, device power consumption, optical power, and channel crosstalk values. Each experiment is repeated 10 times to obtain the average value and standard deviation.
2.  **Error Analysis**: For each verification module, calculate the relative error between the theoretical and measured values, analyze error sources such as device modulation precision, optical path coaxiality, and detection noise, and propose targeted calibration methods.
3.  **Performance Comparison**: Quantitatively compare the accuracy, energy consumption, latency, and computing power density of polarization-based computing with silicon-based computing devices of the same computing power, forming a detailed performance comparison report with quantitative data support.
4.  **Parallel Efficiency Analysis**: For the WDM module, calculate the computing power expansion ratio and parallel efficiency under different numbers of wavelengths, fit the curve of computing power versus the number of wavelengths, and verify the linear expansion characteristic of photonic computing power.
5.  **Data Standardization**: All acquired data are sorted and stored in a unified format, with clear labeling of experimental conditions, device parameters, and calibration values to ensure the traceability and reusability of experimental data.

---

## 6. Core Value and Engineering Significance

1.  **Theoretical Verification Value**: For the first time, verify the core logic of polarization-based computing — "medium as channel, field as operator" — through physical experiments, proving the feasibility of Jones matrices as an "EDA simulation-free instruction set" for photonic computing. This provides a solid physical experimental basis for polarization-based photonic computing architectures and fills the gap between theoretical research and physical verification of polarization photonic computing.
2.  **Reduced Implementation Barriers**: Fully utilizing commercial devices in the 1550 nm band with Lego-style cascading, the scheme can be implemented in ordinary optical laboratories without customized crystal preparation, ultra-high-precision optical platforms, or EDA simulation tools, significantly lowering the experimental and R&D barriers for photonic computing and enabling more research teams to engage in polarization photonic computing research.
3.  **Measurable Performance Support**: By comparing with silicon-based computing, the core advantages of polarization-based computing in energy consumption and latency are quantified for the first time. The measured results can directly respond to "computing power anxiety", proving the physical existence and engineering value of photonic computing, and providing data support for the subsequent industrialization of photonic computing chips.
4.  **Scalability Verification**: The layered verification from primitives to operators to parallelism proves the scalability of the PDMM architecture. The linear computing power expansion characteristic of WDM provides a reusable experimental method for subsequent verification of multi-wavelength, high-order matrix, and complex algorithm polarization-based computing, laying an experimental foundation for the expansion of photonic computing power.
5.  **Engineering Methodology**: The formed Lego-style commercial device cascading approach, Jones matrix mapping method, and optical path calibration standards can be directly migrated to the modular design of photonic computing products, enabling seamless transition from laboratory verification to engineering mass production and accelerating the industrialization process of polarization photonic computing.

### 6.1 Standardized Output Template & Engineering Migration Guidelines

To ensure the experimental results can be directly reused in subsequent PDMM architecture engineering and chip R&D, the standardized output form of experimental results and core engineering migration guidelines are clearly defined:

#### (1) Standardized Experimental Result Output Templates

Three types of core documents are formed for direct archiving and reuse, covering raw data, optical path design, and performance comparison:

-   **Polarization Operation Raw Data Set**: Including polarization angle/light intensity-value mapping table, Jones matrix theoretical/measured value comparison table, and original data of error/energy consumption/latency of each module (with standard deviation of 10 repeated experiments).
-   **Optical Path Design Manual**: Including 2D/3D drawings of Lego-style module cascading, standard coaxial calibration process, and device parameter calibration table (directly reusable for the same type of experiment).
-   **Performance Comparison Report**: Including 3D comparison charts of accuracy-energy consumption-latency between polarization photonic computing and silicon-based computing (MCU/FPGA), linear fitting curve of WDM parallel computing power versus wavelength number, and measured curve of crosstalk suppression ratio.

#### (2) Core Engineering Migration Guidelines

The experimental results and design logic are directly migrated to the subsequent engineering R&D of polarization photonic computing, realizing the seamless connection between laboratory verification and industrialization:

-   **Device Level**: The commercial devices verified in the experiment (1550 nm waveplate/SLM/PD) can be directly migrated to the prototype design of the optical computing module of the PDMM architecture without re-selection, reducing the device development cycle.
-   **Algorithm Level**: The Jones matrix mapping rules can be directly used as the underlying instructions of the optical computing ISA, converted into the modulation parameter table of SLM/waveplate, and adapted to the subsequent photonic high-level synthesis (Photonics HLS) process.
-   **Architecture Level**: The Lego-style module cascading logic can be directly reused in the optical computing cluster design of multi-chip cascading, providing a modular design basis for subsequent large-dimension matrix computing and AGI photonic computing hardware implementation.

---

## 7. Experimental Precautions

1.  **Optical Path Shading and Vibration Isolation**: The experiment is carried out on an ordinary vibration-isolated optical platform. A simple light shield should be added to avoid ambient light interference. Reduce vibrations around the platform to ensure stable optical path coaxiality and prevent polarization state distortion caused by optical path jitter.
2.  **Device Connection Standardization**: All optical path connections use commercial fiber jumpers with a bending radius ≥ 30 mm to avoid polarization mode dispersion caused by excessive bending. The connection interface is kept clean to reduce insertion loss and polarization state loss, ensuring operation accuracy.
3.  **Calibration Standardization**: All polarization modulation parameters must be calibrated in advance to form a standardized calibration table. If accuracy deviations occur during the experiment, fine-tuning can be performed directly using the calibration table to ensure experiment repeatability and data consistency.
4.  **Data Acquisition Synchronization**: During multi-wavelength parallel verification, ensure the synchronization of the PD array and data acquisition instrument with a sampling frequency ≥ 1 GHz to avoid parallel efficiency calculation deviations caused by synchronization errors and ensure the accuracy of parallel computing power quantification.
5.  **Device Power Control**: The input light power of each wavelength channel is controlled within 1–5 mW to avoid power saturation of WDM/DEMUX devices and ensure the crosstalk suppression ratio between channels meets the verification indicators.
6.  **Real-Time Monitoring of Experimental Environment**: The experiment is carried out in a constant temperature environment (25±2℃) to avoid polarization state evolution deviation caused by large temperature changes. The surface of optical devices is regularly cleaned to eliminate stray light interference caused by dust attachment.

### 7.1 Abnormal Condition Handling & Calibration Details

Aiming at the three most common abnormal conditions in the experiment, a targeted and operable solution is given to avoid experimental interruption and ensure the smooth progress of the experiment:

1.  **Polarization State Distortion**: If the PD detects that the deviation between the polarization state and the Jones matrix derivation is ＞2%, priority is given to troubleshooting three points: ① Fiber jumper bending radius (ensure ≥30 mm to avoid polarization mode dispersion); ② Waveplate/SLM surface cleanliness (wipe gently with a dust-free cloth dipped in absolute ethanol to eliminate stray light); ③ Optical axis coaxiality (recalibrate with a laser collimator to ensure coaxial deviation ≤ 0.1°).
2.  **Excessive Inter-Channel Crosstalk**: If the crosstalk suppression ratio is ＜30 dB, adjust the input light power of the WDM/DEMUX (control the single-wavelength power at 1–5 mW to avoid power saturation), or add a narrow-band filter (1550 nm±0.5 nm) to each channel to further suppress wavelength crosstalk and meet the verification indicators.
3.  **Precision Drift During Long-Term Operation**: If the error fluctuation exceeds ±0.5% during 72 hours of continuous operation, start a regular calibration mechanism (calibrate the PD detection threshold with standard polarization states (0°/90°/45°) every 12 hours, and update the Jones matrix mapping table synchronously) without interrupting the experiment to ensure the stability of long-term operation.

---

**Disclaimer**  
The proposed polarization state primitive operation and WDM parallel computing integrated verification scheme is a pioneering exploration in the field of polarization photonic computing. All experimental designs are based on mature photonics theory and commercial device performance parameters. Due to the differences in experimental equipment, operating environment and personnel skills, the actual experimental results may have slight deviations from the theoretical values. The research team shall bear the corresponding experimental risks for the implementation of this scheme, and the scheme designer shall not be liable for any experimental losses caused by the above factors.
