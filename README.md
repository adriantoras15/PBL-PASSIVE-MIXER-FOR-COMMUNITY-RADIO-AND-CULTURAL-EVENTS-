
# PBL-PASSIVE-MIXER-FOR-COMMUNITY-RADIO-AND-CULTURAL-EVENTS-
# Passive Mixer for Community Radio / Cultural Events

**ECE Project-Based Learning (PBL) – Report Content**

> **Project status:** This repository documents the currently described two-channel copied input arrangement and the LM741 amplifier/filter simulation work. It does **not** claim that the complete four-channel mixer, clip indicator, test-tone generator, or hardware prototype has been completed.

| Field | Details |
|---|---|
| Course | BTECH ECE |
| Department | Electronics, St Aloysius Deemed to be University, Mangaluru |
| Semester / Batch |3RD SEM ECE |
| Faculty Guide | Mr Vijay Ganesh, Dr Glenson Toney, Mr Tenson Jose (Dept of ECE) |
| Team members |RIMSHA FATHIMA|
|MOHAMMED TAUHEED|
|HENSON PINTO|
|HANEEZ K M|


---

## 1. Project Overview

### Abstract
This project aims to develop an affordable audio-mixing system for community radio stations and cultural programmes. The intended system combines audio signals from multiple sources and uses filtering and amplification to produce a suitable output.

The work completed so far focuses on a KiCad SPICE simulation of an LM741-based amplifier and an associated RC output network. The input source used in the current simulation is a 1 V-amplitude, 1 kHz sine wave with zero DC offset. A second channel was made by copying the first circuit; its source settings should be confirmed to be identical before final submission.

The current work is a **partial implementation** of the larger project. Additional channel mixing, channel-level gain control, clip indication, test-tone calibration, and complete frequency-response verification remain to be completed.

### Problem Statement
Small community radio stations and non-governmental organisations may not be able to afford commercial audio mixers. This project explores a low-cost approach to combining audio sources and conditioning the resulting signal through filtering and amplification.

### Objectives
1. Select and characterize the input signals used in the simulation.
2. Study an RC filter/tone-shaping stage for the intended audio band.
3. Simulate an LM741 amplifier stage and examine its input and output waveforms.
4. Compare calculated circuit behaviour with KiCad SPICE results where measurements are available.
5. Extend the design toward a complete multi-channel mixer in future work.

### Tools and Components Reported So Far

| Item | Details |
|---|---|
| Simulation software | KiCad with SPICE / ngspice simulation |
| Operational amplifier | LM741 |
| Supply rails | +12 V and −12 V |
| Input source | Sine wave; amplitude = 1 V; frequency = 1 kHz; DC offset = 0 V |
| Passive values visible in schematic | R2 = 100 kΩ; R3 = 1 kΩ; R4 = 100 kΩ; C2 = 10 µF; C3 = 10 nF *(confirm all values and connections against the final schematic)* |

---

## 2. Chapter 1 — Signals and Their Properties

### 1.1 Basics of audio signals
An audio signal is a time-varying electrical signal that represents sound. A pure sine wave contains one frequency, while speech and music contain many frequency components and harmonics. The human audible range is commonly approximated as 20 Hz to 20 kHz.

### 1.2 Properties of the selected signal
For a sine wave with peak amplitude Vp:

- Peak-to-peak voltage: Vpp = 2·Vp
- RMS voltage: Vrms = Vp / √2
- Period: T = 1 / f

For the current 1 V-peak, 1 kHz source: **Vpp = 2 V, Vrms ≈ 0.707 V, T = 1 ms, DC offset = 0 V.**

### 1.3 Signals selected for this project

| Channel | Signal source / type | Frequency | Amplitude (Vpp) | RMS (V) | DC offset (V) |
|---|---|---|---|---|---|
| CH1 | Sine wave input | 1000 Hz | 2 V | 0.707 V | 0 V |
| CH2 | Sine wave input (copied circuit; confirm source settings) | 1000 Hz* | 2 V* | 0.707 V* | 0 V* |
| Noise | No separate noise source applied in the current simulation | — | — | — | — |

\*CH2 values apply only if the copied source retains the same 1 V amplitude, 1 kHz frequency, and zero DC offset settings as CH1.

### 1.4 Frequency range of interest
The intended frequency range of interest for the overall project is approximately **100 Hz to 4 kHz**. This range includes important components of speech and common musical signals. The current transient simulation uses a 1 kHz sine-wave test input; it does not by itself verify the complete 100 Hz–4 kHz response.

### 1.5 Justification of signal selection
A 1 kHz sine wave is a convenient test signal because its frequency and amplitude are known, making it useful for observing amplification and waveform behaviour. A 1 V peak input corresponds to 2 V peak-to-peak and approximately 0.707 V RMS for an ideal sine wave.

---

## 3. Chapter 2 — Filter Design

### 2.1 Need for filtering
Filtering is used to shape the frequency content of an audio signal. Depending on the selected response, a filter can reduce unwanted low- or high-frequency components and help restrict the signal to the intended audio band before or after amplification.

### 2.2 Type of filter selected
The output network contains resistors and capacitors and is intended to provide RC filtering/tone shaping. The exact filter classification and order should be stated only after confirming the complete connections in the final schematic and checking its AC response.

### 2.3 Design equations
For a simple first-order RC section:

- Cutoff frequency: `fc = 1 / (2πRC)`

For a band-pass formed by cascaded high-pass and low-pass sections:

- `fL = 1 / (2πR1C1)`
- `fH = 1 / (2πR2C2)`
- Bandwidth: `BW = fH − fL`

These equations apply to the corresponding simple RC sections; the complete circuit response may be affected by loading and interactions between stages.

### 2.4 Selected frequency range and component values
The following values are a **proposed calculation** for the intended 100 Hz–4 kHz design target. They are **not verified** as the components currently fitted in the submitted KiCad schematic, and the simulated cutoff values have not yet been measured.

| Parameter | Designed value | Standard component used | Simulated value | Error |
|---|---|---|---|---|
| Lower cutoff fL | 100 Hz | R = 160 Ω; C = 10 µF | Not measured | — |
| Upper cutoff fH | 4000 Hz | R = 3.9 kΩ; C = 10 nF | Not measured | — |
| Bandwidth | 3900 Hz | — | Not measured | — |
| Passband gain | Not specified | — | Not measured | — |

**Calculation check:**
- R = 160 Ω, C = 10 µF → fL ≈ **99.5 Hz**
- R = 3.9 kΩ, C = 10 nF → fH ≈ **4.08 kHz**
- Nominal target bandwidth = 4000 − 100 = **3900 Hz**

### 2.5 Simulation results — evidence to include
- **Figure 2.1:** KiCad schematic showing the filter stage and component values.
- **Figure 2.2:** AC analysis (Bode magnitude plot, logarithmic frequency axis) with the −3 dB cutoff points marked.
- **Figure 2.3:** Phase plot, if available.
- **Figure 2.4:** Transient plot showing an in-band and an out-of-band test signal, if measured.

### 2.6 Observations
The cutoff frequency of an RC filter is determined by the resistor and capacitor values used in the circuit. The intended design range is approximately 100 Hz to 4 kHz. Any difference between the designed and simulated cutoff frequencies may occur because of the selection of standard component values, component tolerances, and loading effects from the connected stage. The actual cutoff frequencies must be verified using AC analysis (Bode plot) in KiCad. The filter is expected to attenuate frequencies outside the selected range while allowing the desired audio frequencies to pass through.

> Do not report the proposed design values as measured simulation results. Frequency, gain, and cutoff claims must be supported by KiCad plots.

---

## 4. Chapter 3 — Amplifier Stage

### 3.1 Role of the amplifier in the mixer
The amplifier increases the amplitude of a weak audio signal to a suitable level for the next stage. In an audio mixer, amplification can compensate for signal loss in the mixing and filtering stages and help provide an appropriate output level. The LM741 operational amplifier is used in the current simulated amplifier stage.

### 3.2 Selection of inverting or non-inverting configuration
- **Inverting:** input applied to the inverting (−) terminal; output is 180° out of phase.
- **Non-inverting:** input applied to the non-inverting (+) terminal; output is ideally in phase.

The actual configuration in this project must be identified from the final pin-to-pin schematic connections; do not select one solely from the waveform screenshot.

### 3.3 Design equations
- Inverting amplifier: `Av = −Rf / Rin`
- Non-inverting amplifier: `Av = 1 + Rf / R1`
- Gain in decibels: `A(dB) = 20·log10|Av|`

The output must remain within the op-amp's available output swing to avoid clipping.

### 3.4 Anticipated versus achieved gain
The previous draft assumed a non-inverting arrangement with Rf = 100 kΩ and R1 = 100 kΩ. If those connections are confirmed, the theoretical gain is `1 + 100k/100k = 2 V/V`, or **6.02 dB**. This assumption must be checked against the actual schematic before submission.

| Parameter | Anticipated (designed) | Achieved (simulated) | Error |
|---|---|---|---|
| Rf / R1 | 100 kΩ / 100 kΩ (conditional) | Not confirmed | — |
| Input amplitude | 2 Vpp | 2 Vpp (source setting) | — |
| Output amplitude | 4 Vpp (if gain = 2) | Approx. 22 Vpp visually estimated; verify | Not verified |
| Voltage gain | 2 V/V (conditional) | Not verified | — |
| Gain | 6.02 dB (conditional) | Not verified | — |
| Phase shift | 0° if non-inverting | Not measured | — |
| −3 dB bandwidth | Not specified | Not measured | — |

The earlier waveform screenshot visually suggested about 1 V peak on the blue trace and about 11 V peak on the amplifier output trace. These are **visual estimates only**. The output also appears close to the ±12 V supply rails, so possible clipping/saturation must be checked before using the estimated amplitude or gain as a final result.

### 3.5 Proof of achieved gain — evidence to include
- **Figure 3.1:** KiCad schematic of the amplifier stage with LM741 pin connections visible.
- **Figure 3.2:** Transient plot with input and output on the same axes, using cursors to mark peak values.
- **Figure 3.3:** AC analysis showing gain (dB) across frequency.
- **Figure 3.4:** Complete mixer schematic and final output waveform, once the complete system is implemented.

### 3.6 Observations
The transient simulation shows sinusoidal input and output waveforms. The output trace appears to have a larger amplitude than the input trace, indicating amplification. However, the displayed output approaches the supply rails, so clipping or saturation may be present. Exact gain, phase shift, and bandwidth should be obtained using cursor measurements and AC analysis rather than visual estimates alone.

---

## 5. Chapter 4 — Conclusion and Inference

### 4.1 Summary of results

| Stage | Target | Current status / evidence | Met? |
|---|---|---|---|
| Input signals | 1 kHz, 1 V peak sine input | CH1 settings known; CH2 is copied and should be checked | Partly |
| Filter | Intended 100 Hz–4 kHz | AC cutoff measurements not yet available | Not verified |
| Amplifier | Gain based on confirmed feedback network | Transient waveform shown; exact gain/configuration needs verification | Partly |
| Complete mixer | Combined multi-channel output | Full four-channel system not yet completed | No |

### 4.2 Conclusion
The project investigates an affordable audio mixer for community radio and cultural events. The work completed so far includes a KiCad SPICE simulation using an LM741 operational amplifier, ±12 V supply rails, and a 1 V peak, 1 kHz sine-wave input. The transient waveform indicates that the amplifier stage changes the signal amplitude, while the output RC network is intended to provide filtering or tone shaping. The complete filter response and amplifier gain have not yet been verified with AC analysis and precise cursor measurements. The current work therefore represents a partial implementation and simulation study of the larger multi-channel mixer.

### 4.3 Inference
The simulation demonstrates the use of an operational amplifier for signal amplification and shows how resistors and capacitors can be used for frequency-dependent signal conditioning. The results also indicate the importance of selecting suitable gain and supply conditions, because an output that approaches the supply rails may become clipped or distorted. Calculated cutoff frequencies and gain values must be compared with measured KiCad AC and transient results before concluding that the design meets its targets.

### 4.4 Challenges faced
- Understanding and configuring the LM741 operational amplifier and its supply connections in KiCad.
- Identifying the correct input and output nodes in the SPICE waveform viewer.
- Interpreting transient plots and distinguishing input, amplifier output, and filter output.
- Checking whether the large output amplitude approaches the supply limits and causes clipping.
- Completing the full multi-channel design and obtaining AC frequency-response evidence.

### 4.5 Future scope
- Complete and test the four-channel mixing network.
- Add independent channel-level gain or volume controls.
- Verify the filter's lower and upper cutoff frequencies using AC analysis.
- Add a clip indicator and a test-tone generator for calibration.
- Build a hardware prototype and compare practical measurements with SPICE simulation.
- Improve output-stage performance and ensure adequate headroom with an appropriate audio amplifier design.

---

## 6. Appendix

### A. Complete KiCad schematic
Include a high-resolution image of the actual completed circuit, clearly labelling which stages are implemented and which remain proposed.

### B. Bill of materials — values visible/reported so far

| Component | Value | Quantity known from available information |
|---|---|---|
| LM741 | Operational amplifier | 1 shown in supplied schematic |
| R2 | 100 kΩ | 1 shown |
| R3 | 1 kΩ | 1 shown |
| R4 | 100 kΩ | 1 shown |
| C2 | 10 µF | 1 shown |
| C3 | 10 nF | 1 shown |
| DC supplies | +12 V and −12 V | One dual-rail supply arrangement |
| Sine source | 1 V amplitude, 1 kHz, 0 V offset | At least one; CH2 copied, exact source count to confirm |

### C. Simulation settings
The schematic screenshot shows a transient command written as `.tran 10u 0.1`. Confirm the final simulator settings and record the actual stop time and maximum time step used. The AC sweep range has not yet been supplied.

---
