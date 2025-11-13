# **Neo-Hookean UMAT for Abaqus**  
### *With Mathematica Verification, Code Generation, and Example Input Files*

This repository provides a clean, beginner-friendly demonstration of how to implement, test, and validate a **Neo-Hookean hyperelastic material** in Abaqus UMAT. It includes:

✔ UMAT implementation (Fortran)  
✔ Template-driven automatic code generation  
✔ Mathematica notebooks for stress, Jacobian derivation, and verification  
✔ Input files for uniaxial tension and simple shear  
✔ A clear folder structure + detailed documentation  

This project is designed for **students, researchers, and beginners** learning constitutive modelling and UMAT development.

---

## 📂 **Repository Structure**

```
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
```

---

## ▶️ **How to Run the UMAT in Abaqus**

### **Uniaxial Test**

Run from the command line:

```
abaqus job=uniaxial_test ^
    input=abaqus-inputs/uniaxial/uniaxial_test.inp ^
    user=umat/umat_neohookean_auto.for
```

(or use `\` instead of `^` on Linux/macOS)

This will generate:

```
uniaxial_test.odb
```

You can open it in **Abaqus/Viewer** to inspect stress, strain, and deformation.

---

### **Simple Shear Test**

```
abaqus job=simple_shear_test ^
    input=abaqus-inputs/simple-shear/simple_shear_test.inp ^
    user=umat/umat_neohookean_auto.for
```

This will generate:

```
simple_shear_test.odb
```

You can run these input files using:

- `umat_neohookean_auto.for` (auto-generated)
- `umat_neohookean_manual.for` (manually written)
- or any new UMAT you generate through Mathematica.

---

## 🧰 **Prerequisites**

To use this repository fully, you need:

- **Abaqus/Standard** (tested on 2023)
- **Intel Fortran compiler** (ifort)
- **Mathematica** (for symbolic derivation + UMAT code generation)
- Windows or Linux

No special libraries are needed.

---

## 🧪 **Mathematica Verification (Semi-Inverse Method)**

The notebook:

```
mathematica/semi_inverse_verification.nb
```

computes:

- Analytical deformation gradients  
- Cauchy stress for Neo-Hookean model  
- Verification plots for uniaxial and simple shear  
- Comparison with Abaqus results  

This ensures the UMAT implementation is mathematically correct.

---

## ⚙️ **Automatic UMAT Code Generation Workflow**

The notebook:

```
mathematica/umat_auto_generator.nb
```

performs:

1. Symbolic derivation of  
   - Invariants  
   - Cauchy stress  
   - Consistent material Jacobian  

2. Converts symbolic expressions into **Fortran code** using `FortranForm`.

3. Inserts these expressions into the UMAT template:

```
umat/umat_template_neo.for
```

4. Produces the ready-to-use UMAT:

```
umat/umat_neohookean_auto.for
```

This workflow allows fast development of new hyperelastic models without manually deriving complex tensor expressions.

---

## 📘 **Theory Summary**

The Neo-Hookean strain energy used in this repository is:

\[
W = \frac{\mu}{2}(I_1 - 3) - \mu \ln J + \frac{\lambda}{2} (\ln J)^2
\]

Where:

- \( \mu \) = shear modulus  
- \( \lambda \) = bulk modulus  
- \( I_1 \) = first invariant of **B**  
- \( J = \det F \)

The UMAT computes:

- **Cauchy stress**  
- **Consistent Jacobian** (material tangent)

More detailed derivations will be added to:

```
docs/theory.md
```

---

## 📊 **Expected Results**

### **Uniaxial Tension**
- Stress–stretch curve matches analytical Neo-Hookean response.
- Smooth monotonic increase in σ₁₁.

### **Simple Shear**
- τ₁₂ ≈ μγ for small γ  
- Nonlinear increase for larger shear levels  

Use the Mathematica verification notebook to confirm these responses.

---

## 🚀 **How to Extend This Repository**

To build another model (Ogden, Mooney–Rivlin, Gent, etc.):

1. Modify the **strain energy function** in:
   ```
   mathematica/umat_auto_generator.nb
   ```
2. Re-run the notebook → generates new Fortran code.
3. Insert into the template automatically.
4. Update the input files if needed.
5. Run in Abaqus and verify.

This workflow eliminates manual algebra and ensures tensor consistency.

---

## 📄 **License**

Released under the **MIT License**.  
You may use, modify, and distribute this repository freely.

---

## ⭐ **If this repository helped you, please consider starring it!**

It helps others discover this resource and encourages further development.
