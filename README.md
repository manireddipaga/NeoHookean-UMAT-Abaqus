Neo-Hookean UMAT for Abaqus
With Mathematica Verification, Code Generation, and Example Input Files

This repository provides a clean, beginner-friendly demonstration of how to implement, test, and validate a Neo-Hookean hyperelastic material in Abaqus UMAT. It includes:

✔ UMAT implementation (Fortran)
✔ Template-driven automatic code generation
✔ Mathematica notebooks for stress, Jacobian derivation, and verification
✔ Input files for uniaxial tension and simple shear
✔ A clear folder structure + detailed documentation

This project is designed for students, researchers, and beginners learning constitutive modelling and UMAT development.

📂 Repository Structure
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

▶️ How to Run the UMAT in Abaqus
Uniaxial Test

Run from command line:

abaqus job=uniaxial_test \
    input=abaqus-inputs/uniaxial/uniaxial_test.inp \
    user=umat/umat_neohookean_auto.for

Simple Shear Test
abaqus job=simple_shear_test \
    input=abaqus-inputs/simple-shear/simple_shear_test.inp \
    user=umat/umat_neohookean_auto.for


This will generate .odb files that you can open in Abaqus/Viewer to inspect stress, strain, and deformation.

🧰 Prerequisites

To use this repository fully, you need:

Abaqus/Standard (tested on 2023)

Intel Fortran compiler (ifort)

Mathematica (for symbolic derivation + code generation)

OS: Windows or Linux

🧪 Mathematica Verification (Semi-Inverse Method)

The notebook:

mathematica/semi_inverse_verification.nb


computes:

Analytical deformation gradients

Cauchy stress for Neo-Hookean model

Comparison with Abaqus UMAT results

Verification plots (uniaxial + simple shear)

This ensures the UMAT implementation is mathematically correct.

⚙️ Automatic UMAT Code Generation Workflow

The notebook:

mathematica/umat_auto_generator.nb


performs:

Symbolic derivation of:

invariants

stress tensor

consistent material Jacobian

Converts symbolic expressions to Fortran code (FortranForm[])

Inserts generated code into:

umat/umat_template_neo.for


Produces the ready-to-use UMAT:

umat/umat_neohookean_auto.for


This makes it extremely easy to:

implement new hyperelastic models

avoid manual algebra

keep stress and tangent consistent

teach UMAT workflow effectively
