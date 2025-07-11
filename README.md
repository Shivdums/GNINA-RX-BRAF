



---

# 🧬 BRAF-CXR: Redocking and Cross-Docking of BRAF Inhibitors Using GNINA for Thyroid Cancer

This project investigates the binding interactions of small-molecule inhibitors with the **BRAF V600E kinase** using **GNINA**, a deep learning-enhanced molecular docking framework. The primary goal was to compare the binding affinities and pose quality of three clinically relevant inhibitors—**Vemurafenib**, **Dabrafenib**, and **Sorafenib**—through a combination of **redocking** and **cross-docking** experiments. Emphasis was placed on evaluating how GNINA’s CNN-based scoring function handles native versus non-native ligands when docked into the same protein structure (PDB ID: 3OG7).

---

## 🎯 Objective

The aim of this study was to assess the binding behavior of three known kinase inhibitors against the **BRAF V600E** mutant kinase:

* **Vemurafenib** (co-crystallized ligand in 3OG7, redocking),
* **Dabrafenib** (BRAF inhibitor, cross-docking),
* **Sorafenib** (multi-kinase inhibitor, cross-docking).

By comparing CNNscores and predicted affinities, we aimed to determine which ligands show the best structural and energetic compatibility with the BRAF V600E binding site.

---

## 🧠 About GNINA

**GNINA** is a molecular docking framework that integrates **convolutional neural networks (CNNs)** into traditional docking pipelines. It improves pose scoring by learning spatial and chemical features from known protein–ligand complexes, outperforming classical scoring functions in many cases. GNINA builds upon AutoDock Vina but enhances docking accuracy, particularly for pose ranking, by using machine learning.

---

## 🧪 Experimental Workflow

### Receptor Preparation

The receptor structure was based on **PDB ID: 3OG7**, which features the BRAF V600E kinase domain in complex with Vemurafenib. The receptor was cleaned to remove all non-essential molecules (e.g., waters, ions) and converted into `.pdbqt` format suitable for GNINA docking.

### Ligand Selection & Preparation

Three inhibitors were selected:

* **Vemurafenib**: a selective BRAF inhibitor and the native ligand in 3OG7.
* **Dabrafenib**: another BRAF-targeted drug with a slightly different chemical scaffold.
* **Sorafenib**: a broader multi-kinase inhibitor known to bind BRAF but not co-crystallized in 3OG7.

Ligand SMILES were obtained from public databases (ZINC15, DrugBank), converted to 3D structures using **Open Babel**, and processed into docking-ready formats.

### Docking Setup and Execution

Each ligand was docked against the 3OG7 receptor using GNINA with the CNN scoring function enabled. Vemurafenib was **redocked** (as it is the native ligand), while Dabrafenib and Sorafenib were **cross-docked**.

All dockings were performed using an automatically generated docking box based on the native ligand site. The output included multiple poses per ligand, each scored by both predicted **binding affinity** and **CNNscore**.

### Scoring and Pose Evaluation

Top-ranked poses for each ligand were selected and analyzed based on:

* **Binding affinity** (kcal/mol): thermodynamic strength of binding.
* **CNNscore**: predicted probability of pose correctness using deep learning.
* **Visual fit**: examined using Py3Dmol to check orientation, pocket fit, and interactions with key residues (e.g., Cys532, Phe595, Glu501).

---

## 📊 Results & Observations

* **Vemurafenib** performed exceptionally well in redocking. It reproduced its crystal pose, forming strong hydrogen bonds and hydrophobic contacts. It had the **highest CNNscore and best predicted affinity**, confirming the reliability of the docking protocol.

* **Dabrafenib**, despite being chemically related, scored lower. The top pose deviated from expected orientation, suggesting steric hindrance or lack of optimal hydrogen bonding in the rigid conformation of the 3OG7 receptor.

* **Sorafenib** showed intermediate performance—its CNNscore and affinity were better than Dabrafenib but not as strong as Vemurafenib. Sorafenib’s broader kinase activity and structural flexibility may have contributed to moderate binding quality within this specific BRAF conformation.

---

## ✅ Conclusion

Vemurafenib showed the most favorable docking results, and this can be attributed to several factors:

1. **Native Fit Advantage**: Vemurafenib is the co-crystallized ligand in the 3OG7 structure. This redocking scenario benefits from a receptor conformation pre-optimized for this molecule.

2. **Structural Compatibility**: Vemurafenib’s rigid and planar architecture allows tight binding within the ATP-binding pocket, forming strong hydrogen bonds and π–π stacking with residues such as **Cys532** and **Phe595**.

3. **Dabrafenib’s Limitations**: Dabrafenib has greater molecular flexibility and bulk, which may not be well-accommodated in the rigid receptor structure used. This resulted in lower CNNscores and weaker docking poses during cross-docking.

4. **Sorafenib’s Broad Spectrum Profile**: Sorafenib is designed to target multiple kinases and lacks the structural specificity that Vemurafenib exhibits for BRAF. Its moderate scores reflect decent but not optimized binding in this context.

This study reinforces the significance of receptor–ligand complementarity in docking performance, and highlights the importance of redocking as a control when benchmarking ligand-binding predictions using CNN scoring models.

---

## 🧠 Future Directions

* Test Dabrafenib and Sorafenib on **alternate BRAF conformations** to account for induced fit effects or allosteric flexibility.
* Evaluate docking results across multiple PDB structures to validate robustness.
* Incorporate **ensemble docking** or **flexible side-chain modeling** to better accommodate ligands with high flexibility.
* Trying Virtual Screening would in my lists too but yup, will try it out soon!
* Use a broader ligand set to establish a scoring benchmark and potentially train custom models using GNINA's deep learning architecture.

---

## 📚 References

* GNINA: [https://github.com/gnina/gnina](https://github.com/gnina/gnina)
* BRAF V600E Structure (PDB ID: 3OG7): [https://www.rcsb.org/structure/3OG7](https://www.rcsb.org/structure/3OG7)
* DrugBank: [https://go.drugbank.com/](https://go.drugbank.com/)
* ZINC15 Ligand Library: [https://zinc15.docking.org/](https://zinc15.docking.org/)
* CNN Docking Publication: [https://pubs.acs.org/doi/10.1021/acs.jcim.0c00109](https://pubs.acs.org/doi/10.1021/acs.jcim.0c00109)
* Open Babel: [https://openbabel.org/](https://openbabel.org/)

---
