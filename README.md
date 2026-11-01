# SciMathSoc — Universal 9:16 Vertical Math Reel Generator Template

[](https://colab.research.google.com)
[](https://opensource.org/licenses/MIT)
[](https://www.manim.community/)
[](https://www.python.org/)
[](https://github.com)

A production-grade, modular framework for creating viral, mathematically rigorous **9:16 vertical short-form video reels** (YouTube Shorts, Instagram Reels, TikTok) using **Manim** and synchronized **neural AI voiceover narration**.

Developed and maintained by **SciMathSoc — Indian Institute of Technology Kanpur (IIT Kanpur)**.

---

## 🚀 Key Features

- **Single Source of Truth (`SCENE_PIPELINE`)**: Define your scene metadata, visual durations, titles, and voiceover scripts in **one single Python table**. The pipeline automatically synchronizes the Manim visual timeline, neural speech synthesis, silence padding, and `.srt` subtitles in lockstep—guaranteeing zero audio-visual drift.
- **10 Pre-Built Mathematical Scene Archetypes**: Ready-to-use visual components for 2D coordinate curves, chord-tangent group laws, matrix grid enumeration, dual-card algebraic decompositions, Euler product flows, and analytic root comparisons.
- **Riemann 9:16 Phone Design System**: Pre-calibrated canvas boundaries that prevent native mobile app overlays (like like/comment buttons, scrubbers, and account handles) from obscuring equations or card contents.
- **Two-Stage Rendering Pipeline**: Rapid low-resolution visual drafts (540×960 @ 24 fps) for quick layout iteration, followed by broadcast-quality master renders (1080×1920 @ 30 fps) with automated FFmpeg audio mixing.
- **Native $\LaTeX$ Mathematical Typography**: Robust equation banners (`formula_banner`), directional callouts (`callout`), and elevated bottom takeaway plates (`footer_note`) with automatic math-mode detection.

---

## 📂 Repository Structure

```text
├── notebooks/
│   └── SciMathSoc_Universal_Manim_Reel_Template.ipynb   # Master Colab / Jupyter notebook
├── scripts/
│   ├── universal_manim_reel.py                         # Modular Manim scene source
│   ├── build_subtitles.py                              # Timestamped .srt generator
│   └── mix_audio.py                                    # FFmpeg audio muxing & ducking
├── assets/
│   ├── scimathsoc_logo_circle.png                      # Persistent corner watermark
│   └── music_bed.mp3                                   # (Optional) Instrumental background track
├── output/                                             # Generated video & audio deliverables
│   ├── SciMathSoc_Reel_MASTER_READY.mp4                # 1080x1920 final video with voiceover
│   ├── Master_AI_Voiceover.wav                         # 48 kHz stereo voiceover track
│   └── subtitles.srt                                   # Aligned subtitle cues
└── README.md                                           # Project documentation
```

---

## ⚡ Quickstart Guide

### Option A: Run in Google Colab (Recommended)
1. Click the **Open In Colab** badge at the top of this repository.
2. Navigate to **Cell 1** (`REEL_CONFIG` & `SCENE_PIPELINE`) and define your topic title, scene timings, and voiceover text.
3. Select **Runtime > Run all** (`Ctrl + F9`). The notebook installs dependencies, validates $\LaTeX$ syntax, renders the 540p preview, compiles the 1080p master, synthesizes AI speech, and downloads the finished video bundle.

### Option B: Local Setup (Ubuntu / Debian)
1. **Clone the repository**:
   ```bash
   git clone https://github.com/<YOUR_ORGANIZATION>/<YOUR_REPO>.git
   cd <YOUR_REPO>
   ```
2. **Install system dependencies & TeX Live**:
   ```bash
   sudo apt-get update -qq
   sudo apt-get install -y ffmpeg pkg-config libcairo2-dev libpango1.0-dev \
       texlive-latex-base texlive-latex-extra texlive-fonts-recommended texlive-science dvisvgm
   ```
3. **Install Python requirements**:
   ```bash
   pip install "numpy==2.2.6" "scipy==1.15.3" "manim==0.22.0" "edge-tts==7.3.1" "pillow" "pdf2image"
   ```
4. **Render the video**:
   ```bash
   manim -qh --resolution 1080,1920 --fps 30 -o SciMathSoc_Reel_HD scripts/universal_manim_reel.py BSDReelV7
   ```

---

## 🎛️ How the Universal Pipeline Works

The entire video is driven by the central `SCENE_PIPELINE` list in Section 1 of the notebook:

```python
SCENE_PIPELINE = [
    ("01_hook", 6.0, "FINITE COUNTS. INFINITE POINTS.",
     "Can finite prime number clocks reveal whether an equation has infinitely many fraction solutions?"),
    
    ("02_geometry", 11.0, "WHAT ARE RATIONAL POINTS?",
     "Take the elliptic curve y squared equals x cubed minus x plus one. Its real graph is smooth, but we seek rational points: exact fractions."),
    
    ("03_group_law", 14.0, "CHORD & TANGENT ADDITION.",
     "Remarkably, rational points form a group. A line through two points hits a third; reflect it to add them. A tangent line doubles a point."),
    ...
]
```

When you update this table:
1. **Manim Timeline**: `SEGMENTS` is dynamically updated, and `finish_segment()` guarantees every scene starts and ends exactly on schedule.
2. **AI Voiceover**: `edge_tts` generates neural speech for each scene, measures the clip duration, applies rate adjustments if needed, and pads the remaining tail with silence to reach the exact slot length.
3. **Subtitles**: Timestamped `.srt` cue blocks are generated matching the scene windows.
4. **Master Mux**: FFmpeg combines the 1080p video with the 48 kHz stereo voiceover with automatic intro/outro fades.

---

## 📐 The 10 Mathematical Scene Archetypes

| # | Scene Archetype | Visual Pattern & Manim Components |
| :---: | :--- | :--- |
| **1** | **Hook & Central Question** | `make_header` question banner + framed `formula_banner` + continuous teaser curve. |
| **2** | **2D Curve Geometry** | Coordinate `Axes` + parametric/implicit `make_curve` + rational point `Dot`s + `callout` badges. |
| **3** | **Group & Operation Law** | Secant line through $P_1, P_2$ hitting $R$ + dashed reflection line + tangent doubling line. |
| **4** | **Dual-Card Decomposition** | Side-by-side comparison cards (`make_card`) comparing infinite lattice ($\mathbb{Z}^r$) and finite torsion ($T$). |
| **5** | **Discrete / Clock Field** | Cyclic residue chips ($0 \to 1 \to \cdots \to p-1$) + modular congruence cards. |
| **6** | **2D Grid Solution Enumeration** | Animated $p \times p$ matrix cell scanning + tick mark labels + solution pop-ins. |
| **7** | **Statistical Metric Cards** | $2 \times 2$ grid displaying prime point counts $\#E(\mathbb{F}_p)$ and traces $a_p$ with lagged entrance. |
| **8** | **Hierarchical Product Assembly** | Token chips $\to$ local Euler factor card $\to$ global Hasse–Weil product $L(E, s)$. |
| **9** | **Analytic Continuation & Roots** | Number line convergence interval $\to$ continuation arrow $\to$ local zero-order graphs ($r = 0, 1, 2$). |
| **10** | **Theorem Equality & Outro** | Side-by-side equality bridge ($r_{\mathrm{alg}} = r_{\mathrm{an}}$) + Millennium Prize badge + IIT Kanpur branded closing card. |

---

## 🎨 Riemann 9:16 Design System Specifications

### Color Palette (Deep Petrol Teal & Warm Coral)

| Role | Name | Hex Code | Purpose |
| :--- | :--- | :--- | :--- |
| **Background Top** | Petrol Teal | `#06181E` | Primary canvas gradient top |
| **Background Base** | Dark Abyss | `#041014` | High-contrast dark foundation |
| **Card Fill** | Rich Teal | `#0C252E` | Card surface (`opacity = 0.96`) |
| **Active Card** | Highlight Teal | `#133542` | Callout badges & accented cards |
| **Primary Text** | Warm Ivory | `#FFFDF7` | High-legibility headlines and body text |
| **Curves & Highlights** | Vivid Coral | `#FF6B6B` | Primary curves and theorem callouts |
| **Points & Tags** | Emerald Mint | `#2EE59D` | Rational coordinates, section tags, solutions |
| **Equations & Math** | Amber Gold | `#FFD166` | Principal $\LaTeX$ equations and arithmetic |
| **Analytic & Torsion** | Electric Lilac | `#C4B5FD` | Analytic ranks, torsion cycles, continuation |
| **Arrows & Callouts** | Sky Cyan | `#38BDF8` | Directional arrows and coordinate callouts |
| **Subtitles & Topic Bar** | Sage Grey | `#94B2BD` | Persistent bottom topic bars and subtitles |
| **Coordinate Axes** | Slate Teal | `#4A707F` | Axes, grid lines, and tick marks |

### Safe Margins & Vertical Budget (9:16 Frame)
- **Top Safe Band ($y = +5.20$ to $+7.60$)**: Dedicated header, section tag, and top-right circular watermark.
- **Central Visualization Band ($y = -3.80$ to $+4.80$)**: Bounded equation banners, coordinate axes, and comparison cards.
- **Bottom Takeaway Card ($y = -5.20$)**: Elevated takeaway plate positioned safely above mobile player controls and progress bars.
- **Persistent Topic Bar ($y = -6.45$ to $-6.80$)**: Left-aligned branding (`SciMathSoc · IIT Kanpur`).

---

## 🎙️ Voiceover & Audio Configuration

Voice synthesis is powered by `edge-tts`. You can select any supported voice by updating `voice_name` in `REEL_CONFIG`:

- **Indian English (Female)**: `en-IN-NeerjaNeural` *(Default)*
- **Indian English (Male)**: `en-IN-PrabhatNeural`
- **US English (Female)**: `en-US-AriaNeural`
- **US English (Male)**: `en-US-GuyNeural`
- **UK English (Male)**: `en-GB-RyanNeural`

### Audio Normalization Chain
Each audio segment passes through an FFmpeg filter chain that applies:
1. `atempo`: Dynamic tempo scaling if spoken text exceeds the scene window.
2. `highpass=f=85,lowpass=f=11000`: Rumble and sibilance reduction.
3. `equalizer`: Vocal warmth boost at 240 Hz and intelligibility presence at 3.5 kHz.
4. `acompressor`: Dynamic range leveling (`threshold = -18dB`, `ratio = 2.5`).
5. `apad,atrim`: Frame-accurate silence padding to match the exact scene slot length.

---

## 📜 Contributing & License

Contributions, new mathematical scene archetypes, and topic suggestions are welcome! Please open an issue or submit a pull request.

Distributed under the **MIT License**. See `LICENSE` for more information.

Maintained by **SciMathSoc**, Indian Institute of Technology Kanpur.
