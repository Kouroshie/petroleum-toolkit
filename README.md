# 🛢️ Petroleum Engineering Toolkit

A free, browser-based calculator for the **critical and complex parameters petroleum engineers use every day**: PVT fluid properties, gas Z-factor, reservoir volumetrics, oil and gas decline-curve analysis, and surface-choke performance. No install, no sign-up, no data leaves your device. Everything runs client-side in a single HTML file.

### ▶️ Live tool: **https://kouroshie.github.io/petroleum-toolkit/**

Five modules (Oil PVT, Gas Properties, Volumetrics, Decline Curve, and Choke Performance), each with an interactive chart: Rs & Bₒ vs pressure, Z-factor vs pressure, production forecast, a reservoir-volume breakdown, and a choke performance curve.

![Petroleum Engineering Toolkit screenshot](docs/screenshot.png)

---

## Why this exists

Reservoir and production engineers constantly need quick, defensible estimates of fluid and reservoir properties, whether to sanity-check a simulator, teach a concept, or make a screening decision before the lab PVT report arrives. This toolkit puts the industry-standard correlations in one clean interface, with every formula and reference stated openly so you can trust (and audit) the numbers.

## What it calculates

| Module | Parameters | Correlation |
|---|---|---|
| **Oil PVT** | Bubble-point pressure, oil FVF (Bₒ), oil density, dead- & saturated-oil viscosity | Standing (1947), Beggs–Robinson (1975) |
| **Gas Properties** | Pseudo-criticals, Z-factor, gas FVF (Bg), gas density, gas viscosity | Sutton (1985), Dranchuk–Abou-Kassem (1975), Lee et al. (1966) |
| **Volumetrics** | STOIIP / OGIP, pore & hydrocarbon pore volume, recoverable reserves | Volumetric method |
| **Decline Curve** | Oil **or gas** well rate forecast, time to economic limit, EUR (MMSTB or Bcf) | Arps (1945): exponential / hyperbolic / harmonic, plus a modified-hyperbolic terminal-decline switch (Robertson, 1988) for gas wells fit with b > 1 |
| **Choke Performance** | Solves for liquid rate, wellhead pressure **or** bean size in critical flow; gas rate, bean diameter and area, critical-flow check | Gilbert (1954), Ros (1960), Baxendell (1957), Achong (1961): P_wh = A·q_L·R^B / S^C |

## How to use

Just open the [live link](https://kouroshie.github.io/petroleum-toolkit/), or clone and open `index.html` locally:

```bash
git clone https://github.com/kouroshie/petroleum-toolkit.git
cd petroleum-toolkit
# open index.html in any browser
```

No build step, no dependencies.

## Validation

The correlations are verified against published reference values. For example, the Dranchuk–Abou-Kassem Z-factor reproduces the Standing–Katz chart to within chart-reading accuracy across the validated range (0.2 ≤ P_pr ≤ 30, 1.0 < T_pr ≤ 3.0). Results outside a correlation's valid range are flagged in the UI.

The choke module uses the constants A, B, C stated for **R in scf/STB**, q_L in STB/day, S in 64ths of an inch and P_wh in psig (Gilbert: A = 10.00, B = 0.546, C = 1.89). Texts that write R in Mscf/STB scale the coefficient by 1000^B, giving A = 435 for Gilbert; both forms return the same pressure. Solving for rate, pressure and bean size round-trips exactly, and the four correlations agree within roughly 25% over normal field conditions. Because the correlations assume the bean is choked, the module flags any case where the downstream/upstream absolute pressure ratio leaves the critical-flow region.

## ⚠️ Disclaimer

These are **screening-level estimates** from published correlations, provided for educational and preliminary use with **no warranty**. They are not a substitute for laboratory-measured PVT or history-matched simulation. Always calibrate to measured data before any reserves booking, engineering commitment, or financial decision. The author accepts no liability for decisions made using this tool.

## References

- Standing, M.B. (1947). *A Pressure-Volume-Temperature Correlation for Mixtures of California Oils and Gases.* API Drilling & Production Practice.
- Sutton, R.P. (1985). *Compressibility Factors for High-Molecular-Weight Reservoir Gases.* SPE 14265.
- Dranchuk, P.M. & Abou-Kassem, J.H. (1975). *Calculation of Z Factors for Natural Gases Using Equations of State.* JCPT.
- Beggs, H.D. & Robinson, J.R. (1975). *Estimating the Viscosity of Crude Oil Systems.* JPT.
- Lee, A.L., González, M.H. & Eakin, B.E. (1966). *The Viscosity of Natural Gases.* JPT.
- Arps, J.J. (1945). *Analysis of Decline Curves.* Trans. AIME.
- Robertson, S. (1988). *Generalized Hyperbolic Equation.* SPE 18731 (terminal-decline / modified hyperbolic).
- Gilbert, W.E. (1954). *Flowing and Gas-Lift Well Performance.* API Drilling & Production Practice (surface-choke critical-flow correlation).
- Baxendell, P.B. (1957), Ros, N.C.J. (1960), Achong, I.B. (1961). Refits of Gilbert's choke correlation constants.

## License

MIT © Seyed Kourosh Mahjour, Ph.D. See [LICENSE](LICENSE). Contributions welcome via pull request.
