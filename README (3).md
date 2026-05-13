# 🤖 Hand Muscle Tone Monitoring in Robot-Assisted Rehabilitation
### *Paper Notes & Key Insights — Ranzani et al., 2023*

<p align="center">
  <img src="https://img.shields.io/badge/Field-Rehabilitation%20Robotics-4f46e5?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Journal-Frontiers%20in%20Robotics%20%26%20AI-0ea5e9?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Year-2023-10b981?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Open%20Access-CC--BY-22c55e?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Institution-ETH%20Zurich-e11d48?style=for-the-badge" />
</p>

---

## 📄 Paper Details

| | |
|---|---|
| **Title** | An Online Method to Monitor Hand Muscle Tone During Robot-Assisted Rehabilitation |
| **Authors** | Raffaele Ranzani, Giorgia Chiriatti, Anne Schwarz, Giada Devittori, Roger Gassert, Olivier Lambercy |
| **Institution** | ETH Zurich — Rehabilitation Engineering Laboratory |
| **Journal** | *Frontiers in Robotics and AI*, Vol. 10, February 2023 |
| **DOI** | [10.3389/frobt.2023.1093124](https://doi.org/10.3389/frobt.2023.1093124) |
| **Full text** | [PubMed Central — PMC9939644](https://pmc.ncbi.nlm.nih.gov/articles/PMC9939644/) |

---

## 🎯 The Problem This Paper Solves

Robot-assisted rehabilitation is increasingly delivering stroke therapy at home — without a therapist present. This is great for increasing therapy **dose**, but carries a hidden risk: **intensive hand exercises can silently spike muscle tone and spasticity**. If undetected, this leads to pain, joint contractures, and setbacks in recovery.

The authors' answer: build the safety monitor directly into the robot, running continuously during every session.

> *"Only 3% of studies on technology-assisted spasticity assessment focus on the hand."*
> — Guo et al., 2022 (cited in paper)

---

## 🔧 Figure 1 — The ReHandyBot Device

<p align="center">
  <img src="./fig1_rehandybot_device.png" width="720" alt="Figure 1: The ReHandyBot device in use"/>
</p>

**Figure 1** from the paper shows a subject performing the sponge exercise with the ReHandyBot. Key hardware components are labelled: the **hand cover**, **pushbutton keyboard**, **graphical user interface**, **emergency stop button**, and the **finger pads** with embedded load cells. The inset shows a close-up of the ellipsoidal finger pad design — shaped to keep spastic fingers comfortably in place.

**What makes this device special:**
- **2 degrees of freedom**: trains finger flexion-extension AND forearm pronosupination simultaneously
- **Load cells under each finger pad**: measure interaction forces in real-time
- **Pushbutton keyboard**: colour-coded, operable without therapist supervision
- **Movable hand cover**: allows unsupervised operation without visual distraction
- The robot can be configured for left or right hand use

---

## ⚡ Figure 2 — The Perturbation Method in Action

<p align="center">
  <img src="./fig2_perturbation_force_trace.png" width="700" alt="Figure 2: Force and hand aperture traces during perturbation"/>
</p>

This is the core technical result of the paper. **Figure 2** shows a representative fast (150 ms) ramp-and-hold perturbation for one stroke subject (red) and one unimpaired subject (blue).

**How to read this figure:**
- **Top panel**: Force at the fingertips over time. The shaded regions mark the baseline window (light grey) and the measurement window (dark grey)
- **Bottom panel**: Hand aperture in mm — the robot opens the hand 20 mm (amplitude *a*) and holds it there

**The key numbers leaping out:**
- Stroke subject: F_peak = **21.3 N**, stiffness k = **0.81 N/mm**
- Unimpaired subject: F_peak = **8.0 N**, stiffness k = **0.33 N/mm**

That's a 2.5× difference in peak force — detectable automatically, mid-exercise, without stopping the session.

The formula for stiffness:

> **k = (F_peak − F_base) / a**

where *a* = 20 mm perturbation amplitude.

---

## 🧩 Figure 3 — Exercise Design & Study Protocol

<p align="center">
  <img src="./fig3_exercise_protocol.png" width="700" alt="Figure 3: Exercise structure and pilot study protocol"/>
</p>

**Figure 3** shows exactly how the tone monitoring was embedded into the therapy. The sponge exercise structure (top) has subjects squeeze virtual sponges of different stiffness, memorise them, then identify them blind. Perturbations (⚡) are injected **between sponges**, while the hand is relaxed.

**The session timeline (bottom):**
- One supervised familiarisation block
- Then 12 minutes of fully unsupervised blocks
- Perturbations happen in up to **3 blocks**, spaced at least 3 minutes apart
- MAS assessments bookend the session (stroke patients only)
- aROM and FMA-UE are measured at the start

This design is clever: perturbations are invisible to the patient (small, fast, mid-task) and the monitoring adds zero time to the session.

---

## 🔩 Figure 4 — Testbench Validation with Springs

<p align="center">
  <img src="./fig4_spring_testbench.png" width="680" alt="Figure 4: Spring testbench setup"/>
</p>

Before testing on humans, the team validated the force measurement accuracy using **physical springs of known stiffness** connected to the finger pads. This is a rigorous engineering step that many clinical robotics papers skip.

**Results:**

| Spring | True Stiffness | Error (RMSPE) |
|---|---|---|
| Soft | 0.97 N/mm | **3.8%** ✅ |
| Stiff | 1.57 N/mm | **11.3%** ✅ |

Error was not speed-dependent — good news, since the method works equally well at both perturbation speeds. The higher error for the stiff spring comes from slight bending in the metallic frame at high forces, but is still below the 15–25% errors reported by other devices.

---

## 📊 Figure 5 — Individual Muscle Tone Over Exercise Time

<p align="center">
  <img src="./fig5_individual_results_over_time.png" width="780" alt="Figure 5: Individual peak force and stiffness over exercise time"/>
</p>

**Figure 5** shows every perturbation measurement for every subject, plotted over the 12-minute session.

- **Panels A & C** = stroke group (S-sub 1–6): higher scatter, higher overall values
- **Panels B & D** = unimpaired group (U-sub 1–10): lower values, tighter clustering
- **Triangles** = slow perturbations; **squares** = fast perturbations
- **Open markers** = excluded (voluntary contraction was present)
- **Dashed lines** = linear fit per subject over time

**What stands out:**
- 4 of 6 stroke patients showed a *decreasing* trend over time — the exercise did not worsen spasticity
- The robot successfully tracked individual variation, something a single MAS score at the start could never capture
- You can visually see the separation between groups — the method has clinical discriminative power

---

## 📈 Figure 6 — Average Results Per Perturbation Block

<p align="center">
  <img src="./fig6_average_results_per_block.png" width="780" alt="Figure 6: Average force and stiffness per perturbation block"/>
</p>

**Figure 6** summarises results across the three perturbation blocks (approximately at 0, 6, and 12 minutes), with 90% confidence intervals.

- **Black circles** = slow perturbation results
- **Grey circles** = fast perturbation results
- **Light grey dotted line** = difference (fast − slow), representing speed-dependency

**Key takeaways:**
- Stroke group (A, C): forces stay elevated (~11–14 N) and **stable** across all three blocks — no dangerous escalation
- Unimpaired group (B, D): lower forces (~5–7 N), also stable
- Speed-dependency exists but is **not statistically significant** after correction — likely because the two speeds are close to each other (40 vs 67 mm/s)
- Both groups show consistent group separation across all three time points — the method is reliable and repeatable throughout the session

---

## 💡 My Key Insights

### 1. Safety Monitoring That Doesn't Interrupt Therapy
The entire method is invisible to the patient. Perturbations happen between exercise repetitions, during natural hand relaxation. The session continues without pause. This is the right architecture for unsupervised home use.

### 2. Two Perturbation Speeds = Two Neural Pathways
Fast (150 ms) targets the **spinal monosynaptic reflex** — the same fast reflex elicited in a clinical reflex test. Slow (250 ms) targets the **transcortical long-loop reflex** — the cortically-mediated, voluntary response. Measuring both gives a richer readout of spasticity than either alone.

### 3. Robots Can Outperform the MAS
The Modified Ashworth Scale is a 0–5 subjective score, taken once per session by a human clinician. This robot provides continuous, objective, quantitative data at 3-minute intervals. The paper found no correlation between MAS and robot metrics — not because the robot is wrong, but because MAS lacks the resolution and reliability to match it.

### 4. Exercise Doesn't Worsen Spasticity
A longstanding clinical concern was that intensive therapy might increase tone. This paper provides direct evidence that, at least for this exercise, tone was **stable or mildly decreasing** during the session. That's reassuring for the future of unsupervised robot rehab.

### 5. Limitations to Acknowledge
- Only **6 stroke patients**, all chronic (>10 years post-stroke) — acute stroke populations remain untested
- Cannot separate **neurological** from **biomechanical** (e.g., contracture) contributions to stiffness
- The two perturbation speeds are **too close** to reliably detect speed-dependency — wider speed range needed
- Tested in a simulated unsupervised setting; true home deployment untested

### 6. The Future: Closed-Loop Adaptive Therapy
The paper opens the door to robots that sense rising tone mid-session and automatically reduce exercise intensity — then resume when tone normalises. That would be genuine closed-loop neurorehabilitation. **This paper builds the sensor layer that makes it possible.**

---

## 📁 Files in This Repo

| File | Description |
|---|---|
| `README.md` | This page |
| `fig1_rehandybot_device.png` | The ReHandyBot device in use (Figure 1 from paper) |
| `fig2_perturbation_force_trace.png` | Force & hand aperture during perturbation (Figure 2) |
| `fig3_exercise_protocol.png` | Exercise structure and study protocol (Figure 3) |
| `fig4_spring_testbench.png` | Spring validation testbench setup (Figure 4) |
| `fig5_individual_results_over_time.png` | Individual force/stiffness over session time (Figure 5) |
| `fig6_average_results_per_block.png` | Average results per perturbation block (Figure 6) |
| `ReHandyBot_Muscle_Tone_Notes.docx` | Full structured notes document |

---

## 🚀 How to Upload This to GitHub

**Step 1 — Create a new repository**
1. Go to [github.com/new](https://github.com/new)
2. Give it a name, e.g. `rehandybot-paper-notes`
3. Set it to **Public** (so others can find it)
4. Check **"Add a README file"** — we'll replace it
5. Click **Create repository**

**Step 2 — Upload all files**
1. On your new repo page, click **"Add file" → "Upload files"**
2. Drag and drop ALL the files from this folder:
   - `README.md`
   - All 6 `fig*.png` images
   - `ReHandyBot_Muscle_Tone_Notes.docx`
3. Scroll down, write a commit message like `Add paper notes and figures`
4. Click **"Commit changes"**

**Step 3 — Verify it looks right**
- Click on `README.md` in the file list — you should see the full formatted page with images rendered inline
- If images don't appear, make sure the filenames in the README exactly match the uploaded file names (they should — just don't rename anything)

> 💡 **Tip:** GitHub renders Markdown and displays images automatically. The README will look exactly like a webpage once uploaded. No extra setup needed.

---

## 🔗 Links

- 📖 [Full paper — Frontiers in Robotics and AI](https://doi.org/10.3389/frobt.2023.1093124)
- 🔬 [Free full text — PubMed Central](https://pmc.ncbi.nlm.nih.gov/articles/PMC9939644/)
- 🏫 [ETH Zurich Rehabilitation Engineering Lab](https://relab.ethz.ch/)

---

## 📜 Disclaimer

Personal reading notes. All figures are from Ranzani et al. (2023), published open access under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/). Credit and citation belong to the original authors.

---

<p align="center"><em>Notes compiled May 2026</em></p>
