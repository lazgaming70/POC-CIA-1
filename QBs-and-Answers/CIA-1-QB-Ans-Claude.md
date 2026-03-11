# Principles of Communications - CIA 1 Answer Key

---

## Set A

### Part-A

#### 1. Draw the block diagram of communication systems.

```
[Source] → [Transmitter] → [Channel] → [Receiver] → [Destination]
                                ↑
                              Noise
```

---

#### 2. Compare DSB-SC and SSB.

| Parameter | DSB-SC | SSB |
|---|---|---|
| Sidebands | Both | One |
| Bandwidth | $2f_m$ | $f_m$ |
| Complexity | Moderate | High |
| Application | Data links | HF voice |

---

#### 3. For an FM system, the maximum deviation is 75 kHz and the highest modulating frequency is 15 kHz. Determine the required transmission bandwidth using Carson's rule.

$$B_T = 2(\Delta f + f_m) = 2(75 + 15) = \boxed{180 \text{ kHz}}$$

---

#### 4. Identify suitable modulation technique for TV transmission and justify.

**VSB (Vestigial Sideband)** - transmits full USB + a vestige of LSB, fitting within the 6 MHz channel allocation while avoiding the need for an ideal sharp-cutoff filter that SSB would demand near DC.

---

#### 5. Classify the FM signal as NBFM or WBFM if β = 0.5.

**NBFM** - since $\beta = 0.5 < 1$, only carrier and two sidebands are significant; bandwidth $\approx 2f_m$.

---

#### 6. Summarize the key differences between a random variable and a random process.

- A **random variable** maps one experiment outcome to a single number
- A **random process** $\{X(t)\}$ maps each outcome to an entire time waveform - it's an indexed family of random variables

---

#### 7. Discuss the mathematical conditions for Wide Sense Stationary.

A process $X(t)$ is WSS if:

$$E[X(t)] = \mu \quad \text{(constant)} \qquad \text{and} \qquad R_X(t_1, t_2) = R_X(\tau), \quad \tau = t_1 - t_2$$

---

#### 8. Show how narrowband noise behaves in a modulated system and state its characteristics.

Narrowband noise is written as $n(t) = n_I(t)\cos\omega_c t - n_Q(t)\sin\omega_c t$, where:
- $n_I(t)$, $n_Q(t)$ are lowpass, equal power, and mutually uncorrelated
- In AM detection only $n_I$ appears at output; in FM, $n_Q$ dominates with a parabolic ($f^2$) output PSD

---

#### 9. Apply the noise equivalent bandwidth formula to analyze receiver performance.

$$B_{eq} = \frac{\int_0^{\infty}|H(f)|^2\,df}{|H_{max}|^2}, \qquad N_o = N_0\,|H_{max}|^2\,B_{eq}$$

$B_{eq}$ is always wider than the 3 dB bandwidth (e.g., $B_{eq} = 1.57\,f_3$ for a single-pole RC filter), so actual noise power is higher than the 3 dB bandwidth alone would suggest.


---

### Part-B

#### 10

##### i. Demonstrate how an AM signal is generated using a square law modulator and derive its mathematical equation.

**Principle:**

A square-law modulator uses a nonlinear device (diode or FET biased in the square-law region) whose transfer characteristic approximates:

$$v_o = a_1 v_i + a_2 v_i^2$$

**Block Diagram:**

```
m(t) ──┐
        ├──[Σ]──── v_i ──[Square-Law Device]──[BPF @ f_c]──→ s_AM(t)
c(t) ──┘                  v_o = a₁vᵢ + a₂vᵢ²
= Ac·cos(ωct)
```

**Derivation:**

The input to the device:

$$v_i(t) = A_c\cos\omega_c t + m(t)$$

Applying the square-law characteristic:

$$v_o = a_1[A_c\cos\omega_c t + m(t)] + a_2[A_c\cos\omega_c t + m(t)]^2$$

Expanding the squared term:

$$v_o = a_1 A_c\cos\omega_c t + a_1 m(t) + a_2 A_c^2\cos^2\omega_c t + 2a_2 A_c m(t)\cos\omega_c t + a_2 m^2(t)$$

Using $\cos^2\omega_c t = \frac{1}{2}(1 + \cos 2\omega_c t)$:

$$v_o = \underbrace{a_1 m(t) + a_2 m^2(t) + \frac{a_2 A_c^2}{2}}_{\text{lowpass terms}} + \underbrace{\left[a_1 A_c + 2a_2 A_c m(t)\right]\cos\omega_c t}_{\text{AM term at } f_c} + \underbrace{\frac{a_2 A_c^2}{2}\cos 2\omega_c t}_{\text{at } 2f_c}$$

After the BPF centered at $f_c$ passes only the term at $\omega_c$:

$$\boxed{s_{AM}(t) = a_1 A_c\left[1 + \frac{2a_2}{a_1}m(t)\right]\cos\omega_c t}$$

This is the standard AM signal with modulation sensitivity $k_a = \dfrac{2a_2}{a_1}$.

For a single-tone message $m(t) = A_m\cos\omega_m t$, the modulation index is:

$$\mu = k_a A_m = \frac{2a_2 A_m}{a_1}$$

**Spectrum of the output:**

```
S(f)
  |
  |    (carrier)     LSB       USB
  |         |        |         |
  |         ↓        ↓         ↓
──┼─────────┬────────┬─────────┬────→ f
           fc-fm     fc       fc+fm
```

The distortion term $a_2 m^2(t)$ is removed by the BPF. The output power is:

$$P_{AM} = \frac{(a_1 A_c)^2}{2}\left(1 + \frac{\mu^2}{2}\right)$$

**Limitation:** The square-law approximation is valid only for small signal swings. For larger signals, higher-order nonlinear terms introduce additional harmonic distortion components that must be filtered out.

---

##### ii. Construct the block diagram based on Weaver's method and describe how it generates an SSB signal.

**Weaver's Method (Third Method):**

Weaver's method generates SSB using two stages of modulation and lowpass filters, avoiding the need for an ideal sharp-cutoff sideband filter.

**Block Diagram:**

```
                  ┌─[×]──[LPF, BW=fm/2]──[×]──────┐
                  │   ↑                     ↑       │
m(t) ──────[S]───┤  cos(ω₀t)             cos(ωct)  ├──[Σ]──→ USB / LSB
                  │                                  │  (+ for USB)
                  │   ↑                     ↑       │  (- for LSB)
                  └─[×]──[LPF, BW=fm/2]──[×]──────┘
                      sin(ω₀t)             sin(ωct)
```

where $f_0$ = midband frequency of message (typically $\frac{f_{m,max}+f_{m,min}}{2}$, e.g., 2 kHz for audio 300 Hz - 3.4 kHz).

**Step-by-step mathematical analysis** for $m(t) = A_m\cos\omega_m t$:

**Upper path:**

After first multiplier:
$$u_1(t) = A_m\cos\omega_m t \cdot \cos\omega_0 t = \frac{A_m}{2}[\cos(\omega_m-\omega_0)t + \cos(\omega_m+\omega_0)t]$$

After LPF (retains $\omega_m - \omega_0$ component, since $|\omega_m - \omega_0| < \omega_0$):
$$u_2(t) = \frac{A_m}{2}\cos(\omega_m - \omega_0)t$$

After second multiplier with $\cos\omega_c t$:
$$u_3(t) = \frac{A_m}{4}[\cos(\omega_c + \omega_m - \omega_0)t + \cos(\omega_c - \omega_m + \omega_0)t]$$

**Lower path:**

After first multiplier with $\sin\omega_0 t$:
$$l_1(t) = \frac{A_m}{2}[\sin(\omega_m - \omega_0)t + \sin(\omega_m+\omega_0)t]$$

After LPF:
$$l_2(t) = \frac{A_m}{2}\sin(\omega_m - \omega_0)t$$

After second multiplier with $\sin\omega_c t$:
$$l_3(t) = \frac{A_m}{4}[\cos(\omega_c - \omega_m + \omega_0)t - \cos(\omega_c + \omega_m - \omega_0)t]$$

**Adding (USB):**
$$s_{USB}(t) = u_3 + l_3 = \frac{A_m}{2}\cos(\omega_c + \omega_m - \omega_0)t$$

**Subtracting (LSB):**
$$s_{LSB}(t) = u_3 - l_3 = \frac{A_m}{2}\cos(\omega_c - \omega_m + \omega_0)t$$

**Advantages:**
- Avoids sharp-cutoff filters - LPFs are easy to build
- Requires only a 90° phase shift at fixed frequency $f_0$, not across the whole signal band
- Well-suited for digital/DSP implementation

**Disadvantage:** Any imbalance in the two paths introduces the unwanted sideband (carrier/sideband suppression depends on component matching). The DC offset at the second LPF output also creates a tone at $f_c - f_0$ if not carefully handled.

---

#### 11

##### i. Apply angle modulation principles to formulate the mathematical expressions of FM and PM waves.

**General Angle Modulated Signal:**

$$s(t) = A_c\cos[\omega_c t + \phi(t)]$$

where $\phi(t)$ is the instantaneous phase deviation. The instantaneous frequency is:

$$f_i(t) = f_c + \frac{1}{2\pi}\frac{d\phi(t)}{dt}$$

---

**Phase Modulation (PM):**

The instantaneous phase varies linearly with the message:

$$\phi_{PM}(t) = k_p \cdot m(t)$$

$$\boxed{s_{PM}(t) = A_c\cos[\omega_c t + k_p m(t)]}$$

For single-tone $m(t) = A_m\cos\omega_m t$:

$$s_{PM}(t) = A_c\cos[\omega_c t + k_p A_m\cos\omega_m t] = A_c\cos[\omega_c t + \beta_p\cos\omega_m t]$$

where $\beta_p = k_p A_m$ = PM modulation index (rad).

Instantaneous frequency of PM:

$$f_i(t) = f_c - k_p A_m f_m\sin\omega_m t = f_c - \beta_p f_m\sin\omega_m t$$

Maximum frequency deviation: $\Delta f_{PM} = k_p A_m f_m$ (increases with $f_m$)

---

**Frequency Modulation (FM):**

The instantaneous frequency varies linearly with the message:

$$f_i(t) = f_c + k_f m(t)$$

Integrating to get phase:

$$\phi_{FM}(t) = 2\pi k_f \int_0^t m(\tau)\, d\tau$$

$$\boxed{s_{FM}(t) = A_c\cos\left[2\pi f_c t + 2\pi k_f \int_0^t m(\tau)\,d\tau\right]}$$

For single-tone $m(t) = A_m\cos\omega_m t$:

$$\phi_{FM}(t) = \frac{k_f A_m}{f_m}\sin\omega_m t = \beta_f\sin\omega_m t$$

$$\boxed{s_{FM}(t) = A_c\cos[\omega_c t + \beta_f\sin\omega_m t]}$$

where $\beta_f = \dfrac{\Delta f}{f_m} = \dfrac{k_f A_m}{f_m}$ = FM modulation index.

Maximum frequency deviation: $\Delta f = k_f A_m$ (independent of $f_m$)

**Bessel Function Expansion of FM:**

Using the identity $e^{j\beta\sin\theta} = \sum_{n=-\infty}^{\infty} J_n(\beta)e^{jn\theta}$:

$$s_{FM}(t) = A_c\sum_{n=-\infty}^{\infty} J_n(\beta)\cos(\omega_c + n\omega_m)t$$

The spectrum contains sidebands at $f_c \pm nf_m$ with amplitudes $A_c J_n(\beta)$. Total power remains $A_c^2/2$ regardless of $\beta$.

**Carson's Rule Bandwidth:**
$$B_T = 2(\Delta f + f_m) = 2f_m(1+\beta)$$

**FM vs PM Comparison:**

| Property | FM | PM |
|---|---|---|
| $\phi(t)$ | $\propto \int m(t)dt$ | $\propto m(t)$ |
| $f_i(t)$ | $\propto m(t)$ | $\propto \dot{m}(t)$ |
| $\beta$ vs $A_m$ | Proportional | Proportional |
| $\beta$ vs $f_m$ | Inversely proportional | Independent |
| $\Delta f$ vs $f_m$ | Independent | Proportional |

---

##### ii. Illustrate the process of FM demodulation with balanced slope detector with the circuit diagram and characteristic curve.

**Principle:**

The balanced slope detector (Travis discriminator) converts frequency variations to amplitude variations, which are then envelope-detected. Two tuned circuits detuned above and below $f_c$ produce complementary amplitude responses, giving a linear output vs frequency characteristic.

**Circuit Diagram:**

```
                     L1         C1
              ┌─────UUUU──────||────┬──[D1]──┐
              │   (tuned to         │         │
FM Input ─────┤    fc + Δf)         │        [R1]──┐
(via           │                   │         │     │
 coupling)    │    L2         C2  │        [Ca]   │
              └─────UUUU──────||────┴──[D2]──┘     ├── Vout
                   (tuned to              │         │
                    fc - Δf)            [R2]──┐    │
                                         │     │    │
                                        [Cb]  └────┘
                                         │
                                        GND
```

Two tuned circuits with opposite detuning. Diodes D1 and D2 are connected in opposing polarity.

**Operation Analysis:**

At **carrier frequency** $f = f_c$:
- Both circuits equally detuned → equal envelope outputs
- $V_{D1} = V_{D2}$ → $V_{out} = V_{D1} - V_{D2} = 0$

At $f > f_c$ (positive deviation):
- L1C1 (tuned higher) moves toward resonance → $|V_{D1}|$ increases
- L2C2 (tuned lower) moves away from resonance → $|V_{D2}|$ decreases
- $V_{out} = V_{D1} - V_{D2} > 0$ → Positive output

At $f < f_c$ (negative deviation):
- L1C1 moves further from resonance → $|V_{D1}|$ decreases
- L2C2 moves toward resonance → $|V_{D2}|$ increases
- $V_{out} = V_{D1} - V_{D2} < 0$ → Negative output

**Characteristic S-Curve:**

```
Output
Voltage
(V)
 +Vmax |           ___________
       |          /
       |         /
   0   |--------/-------------→  Frequency (f)
       |       /   fc
       |      /
 -Vmax|_____/
       |
       ← Linear region →
       (fc - Δf)  to  (fc + Δf)
```

The output is linear in the region $f_c \pm \Delta f$. Beyond this, the detector becomes nonlinear.

**Transfer characteristic** (linear region):

$$V_{out}(t) = k_d \cdot [f_i(t) - f_c] = k_d \cdot k_f \cdot m(t)$$

where $k_d$ (V/Hz) is the detector sensitivity.

**Advantages:**
- Simple circuit, no phase-shift network required
- Good linearity within operating range

**Limitations:**
- Not self-limiting - sensitive to amplitude variations (AM noise)
- Requires a limiter stage before it for proper FM demodulation
- Bandwidth limited by the individual tuned circuit bandwidths

---

#### 12

##### i. Illustrate the terms mean, correlation, covariance and ergodicity.

**Mean (Statistical Average / Expected Value):**

For a random process $X(t)$, the mean at time $t$ is:

$$\mu_X(t) = E[X(t)] = \int_{-\infty}^{\infty} x \cdot f_X(x; t)\, dx$$

It represents the ensemble average across all realizations at time $t$. Physically, it is the DC level of the random process. For a WSS process, $\mu_X(t) = \mu_X$ = constant.

**Example:** For $X(t) = A\cos(\omega_0 t + \Theta)$ with $\Theta \sim U[0, 2\pi]$:
$$\mu_X(t) = E[A\cos(\omega_0 t + \Theta)] = 0$$

---

**Correlation:**

*Autocorrelation* measures similarity of a process with a time-shifted version of itself:

$$R_X(t_1, t_2) = E[X(t_1)X(t_2)]$$

For WSS: $R_X(t_1, t_2) = R_X(\tau)$, $\tau = t_1 - t_2$

$$R_X(\tau) = \int_{-\infty}^{\infty}\int_{-\infty}^{\infty} x_1 x_2\, f_X(x_1, x_2; \tau)\, dx_1\, dx_2$$

$R_X(0) = E[X^2(t)]$ = total mean square power.

*Cross-correlation* between two processes:

$$R_{XY}(t_1, t_2) = E[X(t_1)Y(t_2)]$$

---

**Covariance:**

The autocovariance removes the mean before measuring correlation:

$$C_X(t_1, t_2) = E\left[(X(t_1) - \mu_X(t_1))(X(t_2) - \mu_X(t_2))\right]$$

$$\boxed{C_X(t_1, t_2) = R_X(t_1, t_2) - \mu_X(t_1)\mu_X(t_2)}$$

For WSS with zero mean: $C_X(\tau) = R_X(\tau)$

Variance (at $t_1 = t_2$):

$$\sigma_X^2 = C_X(0) = R_X(0) - \mu_X^2 = E[X^2] - (E[X])^2$$

Two random variables are **uncorrelated** if $C_{XY} = 0$. Independent implies uncorrelated, but not vice versa (except for Gaussian).

---

**Ergodicity:**

A process is ergodic if **time averages equal ensemble averages** for any single realization.

*Mean-ergodic* condition:

$$\langle X(t) \rangle = \lim_{T\to\infty}\frac{1}{2T}\int_{-T}^{T} x(t)\, dt = E[X(t)] = \mu_X$$

*Correlation-ergodic* condition:

$$\langle X(t)X(t+\tau)\rangle = \lim_{T\to\infty}\frac{1}{2T}\int_{-T}^{T} x(t)x(t+\tau)\, dt = R_X(\tau)$$

**Practical significance:** Ergodicity allows characterization of a random process from a single long observed waveform instead of requiring many ensemble samples. Most physical noise processes (e.g., thermal noise) are ergodic, which is why SNR can be measured from a single noise waveform trace. Ergodicity implies WSS, but WSS does not imply ergodicity.

---

##### ii. Interpret the process of autocorrelation and explain the properties of autocorrelation function.

**Autocorrelation Process:**

The autocorrelation function (ACF) $R_X(\tau)$ quantifies the degree of statistical dependence between the values of a random process at two time instants separated by $\tau$:

$$R_X(\tau) = E[X(t)X(t+\tau)]$$

Physically, it measures how quickly the process "remembers" or "forgets" its past values. It is computed by:
1. Taking one realization $x(t)$
2. Creating a time-shifted copy $x(t+\tau)$
3. Multiplying and taking the ensemble (or time) average

For a deterministic energy signal, the equivalent operation is the time-domain cross-correlation:

$$R_x(\tau) = \int_{-\infty}^{\infty} x(t)x(t+\tau)\, dt$$

---

**Properties of the Autocorrelation Function:**

**Property 1 - Maximum at origin:**

$$R_X(0) = E[X^2(t)] = \text{Total mean-square power}$$

$$|R_X(\tau)| \leq R_X(0) \quad \text{for all } \tau$$

*Proof:* $E[(X(t) \pm X(t+\tau))^2] \geq 0 \Rightarrow R_X(0) \pm R_X(\tau) \geq 0$

**Property 2 - Even symmetry:**

$$R_X(\tau) = R_X(-\tau)$$

The ACF is always an even function of $\tau$.

*Proof:* $R_X(-\tau) = E[X(t)X(t-\tau)] = E[X(t+\tau)X(t)] = R_X(\tau)$

**Property 3 - Periodicity:**

If $X(t)$ contains a periodic component with period $T_0$, then $R_X(\tau)$ is also periodic with period $T_0$:

$$R_X(\tau + T_0) = R_X(\tau)$$

**Property 4 - DC component:**

If $E[X(t)] = \mu_X \neq 0$, then:

$$\lim_{\tau \to \infty} R_X(\tau) = \mu_X^2$$

This represents the DC power. For a zero-mean process, $R_X(\tau) \to 0$ as $|\tau| \to \infty$.

**Property 5 - Wiener-Khinchin Theorem:**

The ACF and the Power Spectral Density (PSD) form a Fourier transform pair:

$$S_X(f) = \int_{-\infty}^{\infty} R_X(\tau) e^{-j2\pi f\tau}\, d\tau \qquad \longleftrightarrow \qquad R_X(\tau) = \int_{-\infty}^{\infty} S_X(f) e^{j2\pi f\tau}\, df$$

**Property 6 - Non-negative PSD:**

$$S_X(f) \geq 0 \quad \text{for all } f$$

This means the ACF must be a positive semi-definite function.

**Property 7 - ACF at zero lag gives total power:**

$$R_X(0) = \int_{-\infty}^{\infty} S_X(f)\, df = \text{Total power}$$

**Graphical interpretation:**

```
R_X(τ)

R_X(0) |───────╮
       |       │╲
       |       │  ╲
μ²_X   |_ _ _ _│_ _╲_ _ _ _ _
       |              ╲____/
   0   └──────────────────────→ τ
       0   τ_c  (correlation time)
```

A narrow ACF (small $\tau_c$) corresponds to a wideband PSD (fast-changing process). A wide ACF corresponds to a narrowband, slowly varying process.

---

#### 13

##### i. Apply the theory of internal and external noise sources to analyze their impact on communication systems.

**Classification of Noise:**

```
                    Noise Sources
                    /           \
            External           Internal
           /    |    \         /   |   \
      Atmos. Extra-  Man-  Thermal Shot Flicker
      static terres. made
```

---

**External Noise Sources:**

**1. Atmospheric (Static) Noise:**

Caused by lightning discharges and other natural electrical disturbances in the atmosphere.
- PSD $\propto 1/f^2$ - falls steeply with frequency
- Most severe below 30 MHz; negligible at microwave frequencies
- Limits AM broadcast receiver performance
- Equivalent noise temperature can be thousands of Kelvin at HF

**2. Extraterrestrial Noise:**

- *Solar noise:* Continuous radiation from the sun, intensifies during solar flares and sunspot activity. Significant at frequencies above 10 MHz.
- *Cosmic noise:* Background radiation from galactic sources (Milky Way). Significant from 8 MHz to 1.5 GHz. Characterized by a sky noise temperature $T_{sky}$.
- *Cosmic Microwave Background (CMB):* $T_{CMB} \approx 2.7$ K, relevant only for very sensitive radio telescopes.

**3. Industrial / Man-Made Noise:**

Generated by electrical equipment: motors, ignition systems, switching supplies, fluorescent lamps, transmission lines.
- Dominant in urban areas, particularly below 600 MHz
- Modeled as impulsive noise with spectral density $\propto 1/f$

---

**Internal Noise Sources:**

**1. Thermal Noise (Johnson-Nyquist Noise):**

Random motion of charge carriers due to thermal energy generates voltage fluctuations across any resistor:

$$\overline{v_n^2} = 4kTBR$$

$$v_{n,rms} = \sqrt{4kTBR}$$

where $k = 1.38 \times 10^{-23}$ J/K, $T$ = absolute temperature (K), $B$ = noise bandwidth (Hz), $R$ = resistance ($\Omega$).

Available noise power from a resistor:

$$P_n = kTB$$

Equivalent circuit: noise voltage source $v_n$ in series with a noiseless resistor $R$.

```
    vn = √(4kTBR)
    ┌──┤├──┬── R(noiseless) ──┐
    │      │                  │
   GND    (internal)        Terminals
```

PSD: $S_v(f) = 2kTR$ (two-sided), or $4kTR$ (one-sided) - flat (white noise).

**2. Shot Noise:**

Arises from the discrete nature of electron flow across a potential barrier (e.g., PN junction, vacuum tube):

$$\overline{i_n^2} = 2qI_{DC}B$$

where $q = 1.6 \times 10^{-19}$ C, $I_{DC}$ = average DC current. Also white noise. Significant in active devices at RF frequencies.

**3. Flicker Noise (1/f noise):**

Due to carrier trapping/recombination at semiconductor surface states:
$$S_n(f) \propto \frac{1}{f^\alpha}, \quad \alpha \approx 1$$

Dominant at low frequencies (below 1 kHz in bipolar transistors, up to hundreds of kHz in MOSFETs). Worsens oscillator phase noise near the carrier.

**4. Transit-Time Noise:**

At microwave frequencies where the signal period becomes comparable to electron transit time across a device. The electron stream induces random current pulses, increasing noise significantly.

---

**Impact on Cascaded System - Friis Formula:**

For $N$ cascaded stages with gains $G_i$ and noise figures $F_i$:

$$F_{total} = F_1 + \frac{F_2 - 1}{G_1} + \frac{F_3 - 1}{G_1 G_2} + \cdots + \frac{F_N - 1}{\prod_{i=1}^{N-1}G_i}$$

This shows that the first stage (LNA) dominates. A high-gain, low-noise LNA suppresses the noise contribution of all subsequent stages, which is the primary design criterion for RF receiver front-ends.

---

##### ii. Demonstrate how noise temperature is related to noise figure by applying SNR concepts.

**Noise Figure (F) - Definition from SNR:**

Noise figure quantifies the degradation in signal-to-noise ratio introduced by a two-port network:

$$\boxed{F = \frac{SNR_{in}}{SNR_{out}}}$$

For an amplifier with power gain $G$, input signal power $S_i$, and input noise power $N_i = kT_0B$ (standard reference temperature $T_0 = 290$ K):

$$SNR_{in} = \frac{S_i}{kT_0B}$$

$$SNR_{out} = \frac{GS_i}{G \cdot kT_0B + N_{added,device}}$$

Therefore:

$$F = \frac{S_i / kT_0B}{GS_i / (GkT_0B + N_{device})} = 1 + \frac{N_{device}}{GkT_0B}$$

In dB: $NF = 10\log_{10}(F)$

The added noise from the device itself: $N_{device} = (F - 1)GkT_0B$

---

**Equivalent Noise Temperature ($T_e$):**

The equivalent noise temperature models the device's internal noise as if it were produced by a hypothetical noiseless device preceded by a resistor at temperature $T_e$:

$$\boxed{T_e = (F - 1)T_0}$$

Conversely:

$$\boxed{F = 1 + \frac{T_e}{T_0}}$$

---

**Derivation:**

Total output noise power of the amplifier:

$$N_o = G \cdot N_i + G \cdot N_{internal}$$
$$= G \cdot kT_0B + G \cdot kT_eB$$
$$= GkB(T_0 + T_e)$$

From the noise figure definition:

$$F = \frac{N_o}{GkT_0B} = \frac{GkB(T_0+T_e)}{GkT_0B} = 1 + \frac{T_e}{T_0}$$

This confirms $T_e = (F-1)T_0$.

---

**SNR at output:**

$$SNR_{out} = \frac{GS_i}{GkB(T_0+T_e)} = \frac{S_i}{kB(T_0+T_e)}$$

Or, using system noise temperature $T_{sys} = T_0 + T_e = FT_0$:

$$SNR_{out} = \frac{S_i}{kT_{sys}B}$$

---

**Numerical relationship table:**

| Noise Figure (dB) | F (linear) | $T_e$ (K) |
|---|---|---|
| 0 dB | 1.00 | 0 K (ideal) |
| 1 dB | 1.26 | 75 K |
| 3 dB | 2.00 | 290 K |
| 6 dB | 4.00 | 870 K |
| 10 dB | 10.0 | 2610 K |

---

**Receiver Sensitivity from SNR and Noise Figure:**

Minimum detectable input signal:

$$S_{i,min} = F \cdot kT_0B \cdot SNR_{min}$$

In dBm (using $kT_0 = -174$ dBm/Hz at 290 K):

$$S_{i,min} \text{(dBm)} = -174 + NF + 10\log_{10}(B) + SNR_{min}\text{(dB)}$$

**Example:** NF = 5 dB, B = 200 kHz, $SNR_{min}$ = 12 dB:
$$S_{i,min} = -174 + 5 + 53 + 12 = -104 \text{ dBm}$$

This directly shows why minimizing NF improves receiver sensitivity (lower detectable signal level).

---

## Set B

### Part-A

#### 1. Infer the need for modulation in communication systems.

- Antenna size becomes practical (e.g., $\lambda/4 = 75$ cm at 100 MHz vs. 3.75 km at 20 kHz)
- Enables FDM - multiple users share one channel
- FM provides significant SNR improvement ($3\beta^2(\beta+1)$ over baseband)

---

#### 2. Write and explain the general expression for an AM signal.

$$s(t) = A_c[1 + \mu\cos\omega_m t]\cos\omega_c t$$

$A_c$ = carrier amplitude, $\mu$ = modulation index ($0 \leq \mu \leq 1$), $\omega_m$/$\omega_c$ = message/carrier angular frequency. Contains carrier at $f_c$ and sidebands at $f_c \pm f_m$.

---

#### 3. Identify whether distortion occurs if μ > 1.

Yes - **over-modulation**. The envelope $[1 + \mu\cos\omega_m t]$ goes negative, causing an envelope detector to clip it, producing a distorted output that no longer resembles the original message.

---

#### 4. Using Carson's rule, calculate bandwidth if Δf = 75 kHz and fm = 15 kHz.

$$B_T = 2(\Delta f + f_m) = 2(75 + 15) = \boxed{180 \text{ kHz}}$$

---

#### 5. Classify the FM signal as NBFM or WBFM if β = 8.

**WBFM** - since $\beta = 8 > 1$, approximately $\beta + 2 = 10$ significant sidebands per side; $B_T = 2(\beta+1)f_m = 18f_m$. SNR improvement = $3\beta^2(\beta+1) \approx 32.4$ dB over baseband.

---

#### 6. Summarize the important properties of ergodic and Gaussian random processes.

**Ergodic:** Time averages = ensemble averages; implies WSS; statistics measurable from a single realization.

**Gaussian:** Fully described by mean and ACF; linear transforms stay Gaussian; WSS $\iff$ SSS; uncorrelated $\Rightarrow$ independent.

---

#### 7. Outline the essential properties that an autocorrelation function must satisfy.

- $R_X(0) = E[X^2(t)] \geq 0$ (total power)
- $|R_X(\tau)| \leq R_X(0)$ (maximum at origin)
- $R_X(\tau) = R_X(-\tau)$ (even symmetry)
- $R_X(\tau) \to \mu_X^2$ as $|\tau| \to \infty$
- $\mathcal{F}\{R_X(\tau)\} = S_X(f) \geq 0$ (non-negative PSD)

---

#### 8. Apply the relationship between noise figure and noise temperature to analyze receiver characteristics.

$$T_e = (F-1)T_0 \qquad F = 1 + \frac{T_e}{T_0}, \quad T_0 = 290\text{ K}$$

A 1 dB NF LNA gives $T_e = 75$ K; minimum detectable signal $S_{min} = FkT_0B\cdot SNR_{min}$, so lower NF directly improves receiver sensitivity.

---

#### 9. Demonstrate how thermal agitation in a resistor produces noise voltage and derive its mathematical expression.

Random electron motion (Brownian) in any resistor at $T > 0$ K generates fluctuating voltage. By Nyquist's theorem:

$$\overline{v_n^2} = 4kTBR \implies v_{n,rms} = \sqrt{4kTBR}, \qquad P_{available} = kTB$$

---

### Part-B

#### 10

##### i. Construct the balanced modulator configuration for DSB-SC generation and describe its operation.

**Principle:**

A balanced modulator suppresses the carrier component entirely, producing Double Sideband Suppressed Carrier (DSB-SC). This is achieved by using a balanced (symmetrical) circuit configuration where carrier components cancel by phase opposition.

**Ring (Lattice) Diode Modulator - Circuit:**

```
               D1          D2
  ┌─────────►|────┬────|◄──────────┐
  │          (anode     cathode)   │
  │               │                │
  │       [Center-tapped T1]    [Center-tapped T2]
  │               │                │
  m(t) ───────────┤                ├──────── DSB-SC out
  (message)       │                │
  │               │                │
  │          (cathode     anode)   │
  └─────────|◄────┴────►|──────────┘
               D3          D4
                    ↕
              c(t) = Ac·cos(ωct)
              [applied to center-taps of T1 and T2]
```

**Operation - Positive half-cycle of c(t):**
- D1 and D4 forward-biased, D2 and D3 reverse-biased
- Current path: top center-tap → D1 → load → D4 → bottom center-tap
- $m(t)$ is passed with **positive polarity** to the output transformer

**Operation - Negative half-cycle of c(t):**
- D2 and D3 forward-biased, D1 and D4 reverse-biased
- $m(t)$ is passed with **inverted polarity** to the output transformer

Net effect: $m(t)$ is multiplied by a square wave $p(t)$ synchronized with the carrier.

**Mathematical Analysis:**

The switching square wave:

$$p(t) = \frac{4}{\pi}\sum_{n=0}^{\infty}\frac{(-1)^n}{2n+1}\cos[(2n+1)\omega_c t]$$

Output before filtering:

$$v_o(t) = m(t) \cdot p(t) = \frac{4}{\pi}m(t)\cos\omega_c t - \frac{4}{3\pi}m(t)\cos 3\omega_c t + \cdots$$

After BPF (passing only the term at $\omega_c$):

$$\boxed{s_{DSB-SC}(t) = \frac{4A_m}{\pi}\cos\omega_m t \cdot \cos\omega_c t}$$

For $m(t) = A_m\cos\omega_m t$, expanding:

$$s_{DSB-SC}(t) = \frac{2A_m}{\pi}[\cos(\omega_c - \omega_m)t + \cos(\omega_c + \omega_m)t]$$

**Spectrum (no carrier component):**

```
S(f)
  |
  |          |         |         |
  |          ▼         |         ▼
  |     (LSB)|         |         |(USB)
──┼──────────┬─────────┬─────────┬────→ f
            fc-fm      fc       fc+fm
                    (no spike = no carrier)
```

**Carrier suppression** depends on the balance of the diode pairs. Practical circuits achieve 40-50 dB carrier suppression. Demodulation requires a coherent carrier reference at the receiver (the missing carrier must be regenerated via a pilot tone or Costas loop).

**Power efficiency:** 100% of transmitted power is in the sidebands (none wasted on carrier), making DSB-SC power-efficient compared to conventional AM (where carrier carries $\sim66\%$ of power at $\mu=1$).

---

##### ii. Apply the concept of vestigial sideband modulation to design a transmitter and receiver block diagram and explain their operation.

**Motivation for VSB:**

SSB requires an ideal sharp-cutoff filter at $f_c$ (impractical near DC). DSB uses twice the necessary bandwidth. VSB is the engineering compromise: one full sideband is transmitted along with a controlled vestige of the other, using a gradual roll-off filter.

---

**VSB Transmitter Block Diagram:**

```
              ┌─────────────────────────────┐
              │         TRANSMITTER         │
              │                             │
m(t) ─────────►[DSB-SC Modulator]───────────►[VSB Sideband Filter]──→ s_VSB(t)
              │         ↑                   │    H_VSB(f)            │
              │    Ac·cos(ωct)              │                        │
              │    [Carrier Source]         │                        │
              └─────────────────────────────┘
```

**VSB Filter Response $H_{VSB}(f)$:**

```
|H_VSB(f)|
  1.0 |────────────────────╮
      |                    │ \
  0.5 |                    │  ×  (transition at fc)
      |                    │   \
  0   |────────────────────┘    ─────────────→ f
         (LSB vestige)  fc    (full USB)
         ← fv →         ←  W  →
```

The filter satisfies the Nyquist vestigial symmetry condition:

$$H_{VSB}(f_c + f) + H_{VSB}(f_c - f) = 1, \quad |f| \leq W$$

This ensures that when demodulated, the two partial sideband contributions sum to the original full spectrum.

---

**VSB Receiver Block Diagram (Coherent Detection):**

```
              ┌────────────────────────────────┐
              │           RECEIVER             │
              │                                │
r(t) ─────────►[BPF / IF filter]──────────────►[×]──────────►[LPF]──────→ m̂(t)
              │                                │  ↑           │
              │                                │  Ac·cos(ωct) │
              │                                │  [Coherent   │
              │                                │   carrier]   │
              └────────────────────────────────┘
```

**Receiver Operation (coherent detection):**

Received signal $r(t) = s_{VSB}(t) + n(t)$.

After BPF: Noise is limited to signal bandwidth.

After multiplying by coherent carrier $\cos\omega_c t$ and applying LPF:

The vestigial symmetry condition ensures that the partial sidebands from USB and LSB vestige sum correctly:
$$\hat{m}(t) = \frac{1}{2}[m(t) * h_{VSB}(t)] + \frac{1}{2}[m(t) * h_{VSB}(t)] \propto m(t)$$

No additional equalization is needed if the VSB filter satisfies the symmetry criterion.

---

**Bandwidth comparison:**

| Modulation | Bandwidth | Carrier transmitted |
|---|---|---|
| DSB-AM | $2W$ | Yes |
| DSB-SC | $2W$ | No |
| SSB | $W$ | No |
| VSB | $W + f_v$ (typ. $\sim 1.25W$) | Typically No |

**Application - NTSC Television:**
- Video baseband: DC to 4 MHz
- VSB filter retains: 4 MHz USB + 1.25 MHz vestige of LSB
- Total video bandwidth: 5.25 MHz within a 6 MHz channel
- Sound carrier: 4.5 MHz above video carrier (FM modulated)

**Advantage over SSB:** Near-DC video content (scene changes, slow pans) is preserved without the phase distortion that SSB would introduce near $f = 0$. The VSB filter's gradual roll-off is much easier to realize than an ideal brick-wall SSB filter.

---

#### 11

##### i. Show how Wideband FM is expressed mathematically and evaluate its performance characteristics relative to Narrowband FM.

**Narrowband FM (NBFM) - β < 0.3:**

For small $\beta$, using the approximation $\cos(\beta\sin\theta) \approx 1$ and $\sin(\beta\sin\theta) \approx \beta\sin\theta$:

$$s_{NBFM}(t) = A_c\cos\omega_c t - A_c\beta\sin\omega_m t\sin\omega_c t$$

Expanding using product-to-sum identities:

$$\boxed{s_{NBFM}(t) \approx A_c\cos\omega_c t + \frac{A_c\beta}{2}[\cos(\omega_c+\omega_m)t - \cos(\omega_c-\omega_m)t]}$$

Only three frequency components (carrier + 2 sidebands), bandwidth $\approx 2f_m$.

---

**Wideband FM (WBFM) - Mathematical Expression:**

For arbitrary $\beta$, use the Bessel function expansion of the FM phasor $e^{j\beta\sin\omega_m t}$:

$$e^{j\beta\sin\omega_m t} = \sum_{n=-\infty}^{\infty} J_n(\beta)e^{jn\omega_m t}$$

Taking the real part:

$$\boxed{s_{WBFM}(t) = A_c\sum_{n=-\infty}^{\infty} J_n(\beta)\cos(\omega_c + n\omega_m)t}$$

where $J_n(\beta)$ are Bessel functions of the first kind, order $n$.

**Bessel coefficients** $J_n(\beta)$ for key values:

| n | β = 0.5 (NBFM) | β = 1 | β = 5 (WBFM) |
|---|---|---|---|
| 0 | 0.938 | 0.765 | -0.178 |
| 1 | 0.242 | 0.440 | -0.328 |
| 2 | 0.031 | 0.115 | 0.047 |
| 3 | 0.003 | 0.020 | 0.365 |
| 4 | - | 0.002 | 0.391 |
| 5 | - | - | 0.278 |

Significant sidebands (where $|J_n(\beta)| > 0.01$) extend to approximately $n_{max} \approx \beta + 2$.

**Bandwidth (Carson's rule for WBFM):**

$$B_{WBFM} = 2(\Delta f + f_m) = 2f_m(1 + \beta)$$

**Total Power** (independent of $\beta$):

$$P_{total} = \frac{A_c^2}{2}\sum_{n=-\infty}^{\infty} J_n^2(\beta) = \frac{A_c^2}{2}$$

---

**Performance Comparison - NBFM vs WBFM:**

**SNR Analysis:**

For FM, output SNR (post-detection) relative to input:

$$SNR_{FM,out} = \frac{3\beta^2(\beta+1)A_c^2/2}{N_0 W}$$

FM figure of merit compared to baseband:

$$\frac{SNR_{FM}}{SNR_{baseband}} = 3\beta^2(\beta+1)$$

For NBFM ($\beta = 0.5$): Improvement = $3 \times 0.25 \times 1.5 = 1.125$ (only 0.5 dB above baseband)

For WBFM ($\beta = 5$): Improvement = $3 \times 25 \times 6 = 450$ (26.5 dB above baseband)

**Pre-emphasis and FM noise PSD:**

FM demodulated noise has parabolic PSD:

$$S_{no}(f) = \frac{N_0 f^2}{A_c^2 k_f^2}, \quad |f| \leq W$$

This means high-frequency message components suffer more noise. Pre-emphasis (boost high frequencies before FM) and de-emphasis (attenuate at receiver) are used to equalize SNR across the audio band in commercial FM.

**Full Comparison Table:**

| Parameter | NBFM ($\beta < 0.3$) | WBFM ($\beta > 1$) |
|---|---|---|
| Bandwidth | $\approx 2f_m$ | $2(\Delta f + f_m)$ |
| Spectrum | 3 components | Many sidebands |
| SNR improvement | $\approx 3\beta^2$ (small) | $3\beta^2(\beta+1)$ (large) |
| Power in carrier | $A_c^2 J_0^2(\beta)/2$ (high) | Can be low (for high $\beta$) |
| Bandwidth efficiency | High | Low |
| Applications | Two-way radio, 25 kHz channels | FM broadcast, satellite links |
| Threshold effect | Less critical | Requires input SNR $>$ threshold |

**Threshold effect in WBFM:** Below a threshold CNR (typically 10 dB above $kT_0B$), FM performance degrades rapidly ("FM clicks"). WBFM trades bandwidth for SNR improvement, valid only above threshold.

---

##### ii. Construct the phasor representation of voltages in a Foster-Seeley discriminator and explain how it recovers the modulating signal.

**Circuit Configuration:**

The Foster-Seeley discriminator uses coupled resonant circuits and exploits the phase relationship between primary and secondary voltages to detect frequency deviation.

```
               RFC (Radio Frequency Choke)
          ┌──UUUUUU──┬──────────────────┐
          │          │                  │
Vi ───[Lp, Cp]      [Choke               │
(Primary   (primary   bypasses RF       │
 tank)      tuned     to midpoint)      │
            to fc)                      │
                     ┌──Ls/2──[A]──[D1]─┴──[R1‖Ca]──┐
                     │                               │
                     ┤ (mutual inductance M)         ├── Vout
                     │                               │
                     └──Ls/2──[B]──[D2]─┬──[R2‖Cb]──┘
                                        │
                                       GND
```

Key: The primary voltage $V_1$ is fed to the center of the secondary via the RFC choke. Thus:
- Voltage at A: $V_A = \frac{V_2}{2} + V_1$ (vectorially)
- Voltage at B: $V_B = -\frac{V_2}{2} + V_1$ (vectorially)

where $V_2$ is the secondary induced voltage.

---

**Phasor Analysis:**

At resonance ($f = f_c$):
- Mutual coupling voltage: $V_2 \propto j\omega M I_1$ → secondary current $I_2$ lags $V_1$ by 90°
- $V_2$ is perpendicular (90°) to $V_1$

```
         V2/2 (↑ perpendicular to V1)
          |
     VA = V1 + V2/2 (equal magnitude to VB)
          |
──────────┼──────────────→  V1 (reference)
          |
     VB = V1 - V2/2
          |
         -V2/2 (↓)

|VA| = |VB|  →  V_D1 = V_D2  →  Vout = 0
```

Above resonance ($f > f_c$), secondary becomes inductive, phase shift < 90°:

```
     V2/2 ↗ (tilts toward V1)
        /
 ─────/──────────→ V1
  VA /  (longer diagonal)
    /
   VB (shorter diagonal, V2/2 tilts away)

|VA| > |VB|  →  Vout > 0
```

Below resonance ($f < f_c$), secondary becomes capacitive, phase shift > 90°:

```
     V2/2 ↗ (tilts away from V1)
        \
 ─────\──────────→ V1
  VA \ (shorter diagonal)
      \
       VB (longer diagonal)

|VA| < |VB|  →  Vout < 0
```

---

**Output Voltage:**

$$V_{out} = |V_A| - |V_B|$$

$$= \sqrt{V_1^2 + \left(\frac{V_2}{2}\right)^2 + V_1\frac{V_2}{2}\cos\phi} - \sqrt{V_1^2 + \left(\frac{V_2}{2}\right)^2 - V_1\frac{V_2}{2}\cos\phi}$$

where $\phi$ is the phase angle between $V_1$ and $V_2/2$.

At $f = f_c$: $\phi = 90°$, $\cos\phi = 0$, $V_{out} = 0$

For small deviations: $V_{out} \approx k_d(f - f_c) = k_d k_f m(t)$ (linear discriminator output)

---

**S-Curve Characteristic:**

```
Vout
(V)
+Vp |          ___________
    |         /
    |        / (linear region)
  0 |───────/─────────────────→ f
    |      /     fc
    |     /
-Vp |____/
    ← fv →
   linear range
```

The slope of the linear portion ($k_d$ in V/Hz) determines the discriminator gain. The linear range spans approximately $\pm \Delta f_{max}$ around $f_c$.

---

**Signal recovery:**

Since $f_i(t) = f_c + k_f m(t)$:

$$V_{out}(t) = k_d[f_i(t) - f_c] = k_d k_f m(t)$$

The original message $m(t)$ is recovered with amplitude $k_d k_f$.

**Comparison with Balanced Slope Detector:**

| Feature | Balanced Slope | Foster-Seeley |
|---|---|---|
| Linearity | Poor (uses two separate resonant slopes) | Better (uses phase variation) |
| Sensitivity | Lower | Higher |
| Bandwidth | Narrower | Wider |
| Limiter needed | Yes | Yes |
| Component count | More (two tuned circuits) | Single coupled pair |

Both require a limiter before them. The ratio detector is a modification of Foster-Seeley that provides inherent amplitude limiting.

---

#### 12

##### i. Formulate the mathematical representation of a random process using statistical parameters.

**Definition:**

A random process $\{X(t, \zeta): t \in T, \zeta \in S\}$ is a two-dimensional function:
- For fixed $\zeta_k$: $X(t, \zeta_k) = x_k(t)$ is the $k$-th sample realization (deterministic waveform)
- For fixed $t_k$: $X(t_k, \zeta)$ is a random variable

The ensemble is the collection of all realizations $\{x_1(t), x_2(t), \ldots, x_N(t)\}$.

---

**First-Order Statistical Description:**

First-order CDF:
$$F_X(x; t) = P[X(t) \leq x]$$

First-order PDF:
$$f_X(x; t) = \frac{\partial F_X(x; t)}{\partial x}$$

**Mean (First Moment):**
$$\mu_X(t) = E[X(t)] = \int_{-\infty}^{\infty} x \cdot f_X(x; t)\, dx$$

**Mean-Square Value:**
$$E[X^2(t)] = \int_{-\infty}^{\infty} x^2 f_X(x; t)\, dx$$

**Variance:**
$$\sigma_X^2(t) = E[X^2(t)] - \mu_X^2(t) = E[(X(t) - \mu_X)^2]$$

---

**Second-Order Statistical Description:**

Joint PDF at two time instants $t_1, t_2$:

$$f_X(x_1, x_2; t_1, t_2) = \frac{\partial^2 F_X(x_1, x_2; t_1, t_2)}{\partial x_1 \partial x_2}$$

**Autocorrelation Function:**

$$R_X(t_1, t_2) = E[X(t_1)X(t_2)] = \iint x_1 x_2 \cdot f_X(x_1, x_2; t_1, t_2)\, dx_1\, dx_2$$

**Autocovariance:**

$$C_X(t_1, t_2) = R_X(t_1, t_2) - \mu_X(t_1)\mu_X(t_2)$$

**For WSS process** ($\tau = t_1 - t_2$):

$$R_X(\tau) = E[X(t)X(t+\tau)]$$

**Power Spectral Density (Wiener-Khinchin):**

$$\boxed{S_X(f) = \int_{-\infty}^{\infty} R_X(\tau) e^{-j2\pi f\tau}\, d\tau}$$

Total power: $P_X = R_X(0) = \int_{-\infty}^{\infty} S_X(f)\, df$

---

**Example: Random Sinusoidal Process**

$$X(t) = A\cos(\omega_0 t + \Theta), \quad \Theta \sim U[0, 2\pi]$$

**Mean:**
$$\mu_X(t) = E[A\cos(\omega_0 t + \Theta)] = \frac{A}{2\pi}\int_0^{2\pi}\cos(\omega_0 t + \theta)\, d\theta = 0$$

**Autocorrelation:**
$$R_X(t, t+\tau) = E[A^2\cos(\omega_0 t+\Theta)\cos(\omega_0 t+\omega_0\tau+\Theta)]$$
$$= \frac{A^2}{2}\cos\omega_0\tau = R_X(\tau) \quad \text{(function of } \tau \text{ only)}$$

This process is **WSS**: constant mean and $\tau$-dependent autocorrelation.

**PSD:**
$$S_X(f) = \mathcal{F}\left\{\frac{A^2}{2}\cos\omega_0\tau\right\} = \frac{A^2}{4}[\delta(f - f_0) + \delta(f + f_0)]$$

This shows discrete power at $\pm f_0$.

---

**Response of LTI System to a Random Process:**

For WSS input $X(t)$ through LTI system $H(f)$:

$$S_Y(f) = |H(f)|^2 S_X(f)$$

$$\mu_Y = \mu_X \cdot H(0)$$

$$R_Y(\tau) = \mathcal{F}^{-1}\{|H(f)|^2 S_X(f)\}$$

This result (valid only for WSS input) is fundamental to noise analysis in communication receivers.

---

##### ii. Show how the statistical properties determine whether a process is WSS or SSS and compare them.

**Strict-Sense Stationary (SSS):**

A process is SSS (or strongly stationary) if its complete joint statistical description is invariant to time translation. For any $n$, any set $\{t_1, t_2, \ldots, t_n\}$, and any time shift $\epsilon$:

$$f_X(x_1, x_2, \ldots, x_n;\, t_1, t_2, \ldots, t_n) = f_X(x_1, x_2, \ldots, x_n;\, t_1+\epsilon, t_2+\epsilon, \ldots, t_n+\epsilon)$$

This means **all statistical moments** (mean, variance, higher-order moments, and all joint distributions) are shift-invariant.

Consequences:
- Mean: $E[X(t)] = \mu$ (constant)
- Autocorrelation: $R_X(t_1, t_2) = R_X(\tau)$
- Third moment: $E[X^3(t)] = $ constant
- All higher moments: time-invariant

**Wide-Sense Stationary (WSS):**

A weaker condition - only requires the first and second moments to be shift-invariant:

**WSS Conditions:**
1. $E[X(t)] = \mu_X$ (constant, independent of $t$)
2. $R_X(t_1, t_2) = R_X(\tau)$, where $\tau = t_1 - t_2$

WSS does **not** require higher-order statistics to be stationary.

---

**Determination using Statistical Properties:**

To check **WSS**:
1. Compute $\mu_X(t)$. If it varies with $t$, **not WSS**.
2. Compute $R_X(t_1, t_2)$. If it depends on both $t_1$ and $t_2$ (not just $\tau = t_1-t_2$), **not WSS**.

**Example test (WSS):**

Process: $X(t) = A(t)\cos(\omega_0 t)$ where $A(t)$ has mean $\mu_A$ and $R_A(\tau)$.

$$\mu_X(t) = \mu_A\cos\omega_0 t \quad \leftarrow \text{varies with } t \text{: NOT WSS}$$

To check **SSS**: Must verify invariance of all joint PDFs under time shifts - practically intractable for most processes except Gaussian.

---

**Comparison Table:**

| Aspect | WSS | SSS |
|---|---|---|
| Conditions | 2 conditions (mean + ACF) | Infinite-order joint PDF invariance |
| Strength | Weak (necessary) | Strong (sufficient) |
| Practical verification | Feasible | Usually intractable |
| Implication | SSS $\Rightarrow$ WSS (always) | WSS $\Rightarrow$ SSS only for Gaussian |
| All moments stationary? | No (only 1st and 2nd) | Yes |
| PSD valid? | Yes (via Wiener-Khinchin) | Yes |
| Higher-order spectra | Not guaranteed | Valid |
| Example | WSS but not SSS: non-Gaussian process with stationary mean and ACF | White Gaussian Noise, thermal noise |

---

**Key Result for Gaussian Processes:**

For a **Gaussian** random process:

$$\text{WSS} \iff \text{SSS}$$

This equivalence holds because a Gaussian process is entirely characterized by its mean and covariance function. If these are shift-invariant (WSS conditions), then the entire probability structure (all joint PDFs) is automatically shift-invariant (SSS).

This equivalence is why Gaussian noise is so tractable - we only need to verify the two WSS conditions to conclude full stationarity.

---

**Impact on LTI System Analysis:**

WSS is the minimum requirement for valid frequency-domain noise analysis:

$$S_Y(f) = |H(f)|^2 S_X(f)$$

This relation holds only if $X(t)$ is WSS. SSS is stronger than needed - WSS suffices for all linear system noise performance calculations in communications.

---

#### 13

##### i. Show how noise figure influences overall receiver sensitivity and performance.

**Noise Figure and Sensitivity - Definitions:**

Noise Figure:
$$F = \frac{SNR_{in}}{SNR_{out}} = \frac{S_i/N_i}{S_o/N_o} \geq 1$$

**Receiver Sensitivity** is the minimum input signal power $S_{i,min}$ that produces a specified output $SNR_{min}$:

With input noise $N_i = kT_0B$:

$$S_{i,min} = F \cdot kT_0B \cdot SNR_{min}$$

In logarithmic form (using $kT_0 \approx -174$ dBm/Hz at 290 K):

$$\boxed{S_{i,min}(\text{dBm}) = -174 + NF(\text{dB}) + 10\log_{10}B + SNR_{min}(\text{dB})}$$

This equation directly shows that every 1 dB increase in noise figure raises the minimum detectable signal by 1 dB - degrading receiver sensitivity by 1 dB.

---

**Cascaded Receiver Chain Analysis (Friis Formula):**

For a practical receiver chain:

```
Antenna → [LNA, G1, F1] → [Mixer, G2, F2] → [IF Amp, G3, F3] → [Detector]
```

Total noise figure:

$$F_{total} = F_1 + \frac{F_2 - 1}{G_1} + \frac{F_3 - 1}{G_1 G_2} + \cdots$$

**Critical observation:** If $G_1 >> 1$ (high gain LNA), the contributions from $F_2, F_3, \ldots$ become negligible. The LNA dominates system noise.

**Numerical example:**

| Stage | Gain | NF |
|---|---|---|
| LNA | 20 dB (G=100) | 2 dB (F=1.58) |
| Mixer | -6 dB (G=0.25) | 10 dB (F=10) |
| IF Amp | 30 dB (G=1000) | 6 dB (F=4) |

$$F_{total} = 1.58 + \frac{10-1}{100} + \frac{4-1}{100 \times 0.25} = 1.58 + 0.09 + 0.12 = 1.79$$

$$NF_{total} = 10\log(1.79) = 2.53 \text{ dB}$$

Despite the noisy mixer (10 dB NF), the high-gain LNA keeps total NF near 2.5 dB.

**Without LNA** (mixer first):

$$F_{total} = 10 + \frac{4-1}{0.25} = 10 + 12 = 22 \quad (13.4 \text{ dB})$$

This would degrade sensitivity by $13.4 - 2.53 \approx 11$ dB - a huge degradation.

---

**Sensitivity floor calculations:**

| Application | NF (dB) | B (Hz) | SNR_min (dB) | Sensitivity (dBm) |
|---|---|---|---|---|
| FM radio | 10 | 200 kHz | 12 | -99 |
| GSM cellular | 8 | 200 kHz | 9 | -110 |
| GPS | 2 | 2 MHz | 14 | -135 |
| Satellite LNA | 0.5 | 36 MHz | 10 | -108 |

---

**Noise Figure improvement techniques:**

1. **LNA placement first:** Always place lowest NF stage at the antenna
2. **Minimize cable/filter loss** before LNA: Every 1 dB of loss = 1 dB added to NF
3. **Cryogenic cooling:** Reduces $T_e$ (used in radio telescopes, $T_e < 10$ K)
4. **GaAs HEMT LNAs:** Achieve NF of 0.3-0.5 dB at microwave frequencies

---

##### ii. Demonstrate how narrowband noise is represented and analyze the behavior of its in-phase and quadrature components.

**Narrowband Noise - Definition:**

Any broadband noise $n(t)$ (e.g., white noise $S_n(f) = N_0/2$) passed through a bandpass filter (BPF) of bandwidth $B << f_c$ becomes narrowband noise.

---

**Canonical Representation:**

Any narrowband noise process with center frequency $f_c$ can be uniquely written as:

$$\boxed{n(t) = n_I(t)\cos(2\pi f_c t) - n_Q(t)\sin(2\pi f_c t)}$$

Or equivalently in envelope-phase form:

$$n(t) = r(t)\cos[2\pi f_c t + \psi(t)]$$

where:
- $n_I(t) = $ In-phase component (lowpass)
- $n_Q(t) = $ Quadrature component (lowpass)
- $r(t) = \sqrt{n_I^2(t) + n_Q^2(t)}$ = envelope (Rayleigh distributed if zero-mean Gaussian)
- $\psi(t) = \arctan\left(\frac{n_Q(t)}{n_I(t)}\right)$ = phase (uniform distributed)

Extraction of components:

$$n_I(t) = [n(t)\cos(2\pi f_c t)] * h_{LP}(t) \times 2$$
$$n_Q(t) = -[n(t)\sin(2\pi f_c t)] * h_{LP}(t) \times 2$$

---

**Statistical Properties of $n_I(t)$ and $n_Q(t)$:**

For narrowband Gaussian noise with PSD $S_n(f)$ and bandwidth $B$:

**1. Identical PSD:**

$$S_{n_I}(f) = S_{n_Q}(f) = \begin{cases} S_n(f - f_c) + S_n(f + f_c), & |f| \leq B/2 \\ 0, & \text{otherwise} \end{cases}$$

For white noise through BPF: $S_{n_I}(f) = S_{n_Q}(f) = N_0$ for $|f| \leq B/2$.

**2. Equal Power:**

$$E[n_I^2(t)] = E[n_Q^2(t)] = E[n^2(t)] = N_0 B$$

The variance of each component equals the total noise power.

**3. Uncorrelated (and independent for Gaussian):**

$$E[n_I(t)n_Q(t)] = 0$$

At the same time instant, $n_I$ and $n_Q$ are orthogonal. If $n(t)$ is Gaussian, they are statistically independent.

**4. Both are lowpass with bandwidth $B/2$.**

**5. Gaussian: If $n(t)$ is Gaussian, $n_I$ and $n_Q$ are jointly Gaussian.**

---

**Behavior in AM Demodulation (Envelope Detector):**

Received signal: $r(t) = [A_c + m(t)]\cos\omega_c t + n(t)$

Expanding narrowband noise:

$$r(t) = [A_c + m(t) + n_I(t)]\cos\omega_c t - n_Q(t)\sin\omega_c t$$

Envelope:

$$R(t) = \sqrt{[A_c + m(t) + n_I(t)]^2 + n_Q^2(t)}$$

**High SNR** ($A_c >> n$):

$$R(t) \approx A_c + m(t) + n_I(t)$$

The quadrature component $n_Q(t)$ is suppressed. Output noise is just $n_I(t)$, with power $N_0B$.

$$SNR_{AM} = \frac{\mu^2 A_c^2/2}{N_0 W} \quad (\text{for tone modulation, } W = f_m)$$

---

**Behavior in FM Demodulation:**

The FM discriminator responds to instantaneous frequency. For received signal $r(t) = s_{FM}(t) + n(t)$:

Instantaneous phase of $r(t)$ (high SNR approximation):

$$\phi_i(t) \approx \phi_{FM}(t) + \frac{n_Q(t)}{A_c}$$

Discriminator output (differentiates instantaneous phase):

$$v_o(t) = \frac{1}{2\pi}\frac{d}{dt}\left[\phi_{FM}(t) + \frac{n_Q(t)}{A_c}\right] = k_f m(t) + \frac{1}{2\pi A_c}\frac{dn_Q(t)}{dt}$$

FM output noise PSD (differentiation corresponds to $\times j2\pi f$ in frequency domain):

$$S_{no,FM}(f) = \frac{(2\pi f)^2}{(2\pi A_c)^2} S_{n_Q}(f) = \frac{f^2 N_0}{A_c^2}$$

This **parabolic (f²) noise spectrum** is the defining characteristic of FM demodulated noise - high-frequency message components are noisier than low-frequency ones.

```
S_no(f)
 |                     /
 |                    /
 |                   /  (f² shaped)
 |                  /
 |                 /
 |________________/
 └────────────────────→ f
  0                W
```

$$SNR_{FM} = \frac{3\beta^2(\beta+1)A_c^2/2}{N_0 W} = 3\beta^2(\beta+1) \cdot SNR_{baseband}$$

**Rayleigh envelope distribution** (no signal):

$$f_r(r) = \frac{r}{\sigma^2}e^{-r^2/2\sigma^2}, \quad r \geq 0$$

where $\sigma^2 = N_0B$ is the noise variance. This is the distribution of the noise envelope seen by an AM envelope detector in the absence of signal.
