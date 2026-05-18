# AGE-TGI-IDS Verification Repository

Cross-validated verification of the AGE-TGI-IDS quantum computing stack: algebraic gate control (AGE-TGI-2S3) combined with algebraic readout (IDS 3-rail + LO) for photonic quantum computing without cryogenics.

## Key result

AGE-TGI-IDS (no cryogenics) achieves 211× lower physical error rate than a cryogenic SNSPD baseline, translating to zero observed logical failures across 250 000 combined shots on codes up to [[5,1,3]] and repetition d=13.

## Repository structure

```
AGE-TGI-IDS-VERIFICATION/
├── docs/
│   └── AGE_TGI_IDS_Verification_Report.md    # Definitive cross-validated report
├── scripts/
│   ├── consistency/
│   │   ├── consistency_check_v2.py            # PhC geometry & n_eff validation
│   │   └── verify_age_tgi.py                  # AGE-T BCH order & normalisation
│   ├── dephasing/
│   │   ├── age_dephasing_calibrated.py        # PSD-calibrated dephasing (Lorentzian)
│   │   └── improve_dephasing.py               # Correlated vs uncorrelated analysis
│   ├── loss_sweep/
│   │   └── age_t_extended_loss_sweep.py       # Extended loss grid & crossover
│   ├── ids_readout/
│   │   └── verify_sin300_dephasing.py         # SiN-300 platform & AGE regime
│   ├── qec_stack/
│   │   └── age_tgi_ids_simulator.py           # Full-stack Sim A (rep code + GHZ)
│   └── cross_validation/
│       └── compare_simulators.py              # Sim A vs Sim B cross-validation
└── data/
    ├── summary_simA.json                      # Sim A results
    ├── e1_repetition_code.csv                 # Rep code results (all backends)
    └── e3_ghz_fidelity.csv                    # GHZ fidelity results
```

## Requirements

- Python 3.8+
- numpy, scipy

## Quick start

```bash
# 1. Consistency checks
python scripts/consistency/consistency_check_v2.py
python scripts/consistency/verify_age_tgi.py

# 2. Dephasing analysis
python scripts/dephasing/age_dephasing_calibrated.py

# 3. Loss sweep (Frente 1)
python scripts/loss_sweep/age_t_extended_loss_sweep.py --mc 2000

# 4. Full-stack QEC simulation (Sim A)
python scripts/qec_stack/age_tgi_ids_simulator.py --platform SiN300 --shots 50000

# 5. Cross-validation (requires Sim B results in data/)
python scripts/cross_validation/compare_simulators.py
```

## Backends

| Backend | Gates | Readout | Cryo | p_phys |
|---------|-------|---------|------|--------|
| S0 | No AGE | SNSPD η=0.95 | Yes | 5.18×10⁻² |
| S1 | No AGE | Hot PD η=0.70 | No | 3.02×10⁻¹ |
| S2 | AGE-TGI-2S3 | IDS 3-rail+LO | No | 2.46×10⁻⁴ |

## License

AGE Quantum Research Association / Cuantic Control Technologies S.L.
