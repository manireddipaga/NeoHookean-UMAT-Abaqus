Neo-Hookean UMAT for Abaqus
With Mathematica Verification, Code Generation, and Example Input Files

This repository provides a clean, beginner-friendly demonstration of how to implement, test, and validate a Neo-Hookean hyperelastic material in Abaqus UMAT. It includes:

✔ UMAT implementation (Fortran)

✔ Template-driven automatic code generation

✔ Mathematica notebooks for stress, Jacobian derivation, and verification

✔ Input files for uniaxial tension and simple shear

✔ A clear folder structure + detailed documentation

This project is designed for students, researchers, and beginners learning constitutive modelling and UMAT development.

## 📂 Repository Structure
NeoHookean-UMAT-Abaqus/
│
├── umat/
│   ├── umat_template_neo.for          ← Template with placeholders
│   ├── umat_neohookean_manual.for     ← Manually written UMAT
│   └── umat_neohookean_auto.for       ← Auto-generated via Mathematica
│
├── abaqus-inputs/
│   ├── uniaxial/
│   │   └── uniaxial_test.inp
│   └── simple-shear/
│       └── simple_shear_test.inp
│
├── mathematica/
│   ├── semi_inverse_verification.nb   ← Verifies stress response analytically
│   └── umat_auto_generator.nb         ← Generates Fortran UMAT from symbolic math
│
├── docs/
│   └── theory.md                      ← Optional theory notes (WIP)
│
└── README.md


