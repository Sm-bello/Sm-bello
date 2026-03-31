<div align="center">

<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 860 220" width="860" height="220">
  <defs>
    <!-- Background gradient -->
    <radialGradient id="bgGrad" cx="50%" cy="50%" r="65%">
      <stop offset="0%" stop-color="#0c1a2e"/>
      <stop offset="100%" stop-color="#060d18"/>
    </radialGradient>

    <!-- Radar sweep gradient (conic fake via linear + rotation) -->
    <radialGradient id="sweepFade" cx="50%" cy="50%" r="50%">
      <stop offset="0%" stop-color="#0ea5e9" stop-opacity="0.55"/>
      <stop offset="100%" stop-color="#0ea5e9" stop-opacity="0"/>
    </radialGradient>

    <!-- Glow filter for radar rings -->
    <filter id="ringGlow" x="-20%" y="-20%" width="140%" height="140%">
      <feGaussianBlur stdDeviation="1.5" result="blur"/>
      <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>

    <!-- Strong glow for sweep line -->
    <filter id="sweepGlow" x="-30%" y="-30%" width="160%" height="160%">
      <feGaussianBlur stdDeviation="3" result="blur"/>
      <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>

    <!-- Text glow -->
    <filter id="textGlow" x="-10%" y="-30%" width="120%" height="160%">
      <feGaussianBlur stdDeviation="4" result="blur"/>
      <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>

    <!-- Blip glow -->
    <filter id="blipGlow">
      <feGaussianBlur stdDeviation="2.5" result="blur"/>
      <feMerge><feMergeNode in="blur"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>

    <!-- Sweep wedge clip -->
    <clipPath id="radarClip">
      <circle cx="148" cy="110" r="98"/>
    </clipPath>

    <!-- Scanline overlay -->
    <pattern id="scanlines" x="0" y="0" width="860" height="3" patternUnits="userSpaceOnUse">
      <rect width="860" height="1" fill="#0ea5e9" fill-opacity="0.025"/>
      <rect y="1" width="860" height="2" fill="transparent"/>
    </pattern>
  </defs>

  <!-- Background -->
  <rect width="860" height="220" fill="url(#bgGrad)"/>
  <rect width="860" height="220" fill="url(#scanlines)"/>

  <!-- ── RADAR SCOPE (left side) ── -->

  <!-- Outer bezel ring -->
  <circle cx="148" cy="110" r="103" fill="none" stroke="#0ea5e9" stroke-width="1" stroke-opacity="0.25"/>

  <!-- Radar range rings -->
  <g filter="url(#ringGlow)">
    <circle cx="148" cy="110" r="78" fill="none" stroke="#0ea5e9" stroke-width="0.7" stroke-opacity="0.35"/>
    <circle cx="148" cy="110" r="58" fill="none" stroke="#0ea5e9" stroke-width="0.7" stroke-opacity="0.35"/>
    <circle cx="148" cy="110" r="38" fill="none" stroke="#0ea5e9" stroke-width="0.7" stroke-opacity="0.35"/>
    <circle cx="148" cy="110" r="18" fill="none" stroke="#0ea5e9" stroke-width="0.7" stroke-opacity="0.35"/>
    <!-- Main boundary -->
    <circle cx="148" cy="110" r="98" fill="#050f1c" fill-opacity="0.85" stroke="#0ea5e9" stroke-width="1.2" stroke-opacity="0.55"/>
  </g>

  <!-- Cross-hairs -->
  <g stroke="#0ea5e9" stroke-width="0.5" stroke-opacity="0.25" clip-path="url(#radarClip)">
    <line x1="50" y1="110" x2="246" y2="110"/>
    <line x1="148" y1="12" x2="148" y2="208"/>
    <!-- Diagonal guides -->
    <line x1="79" y1="41" x2="217" y2="179"/>
    <line x1="217" y1="41" x2="79" y2="179"/>
  </g>

  <!-- Sweep wedge — trailing fade arc segments -->
  <g clip-path="url(#radarClip)">
    <!-- Fading trail segments (static approximation) -->
    <path d="M148,110 L226,55 A98,98 0 0,1 230,68 Z" fill="#0ea5e9" fill-opacity="0.04"/>
    <path d="M148,110 L230,68 A98,98 0 0,1 234,82 Z" fill="#0ea5e9" fill-opacity="0.06"/>
    <path d="M148,110 L234,82 A98,98 0 0,1 246,110 Z" fill="#0ea5e9" fill-opacity="0.10"/>
    <path d="M148,110 L246,110 A98,98 0 0,1 234,138 Z" fill="#0ea5e9" fill-opacity="0.15"/>

    <!-- Animated sweep line group -->
    <g filter="url(#sweepGlow)">
      <animateTransform attributeName="transform" attributeType="XML"
        type="rotate" from="0 148 110" to="360 148 110"
        dur="4s" repeatCount="indefinite"/>
      <!-- Main sweep line -->
      <line x1="148" y1="110" x2="246" y2="110"
        stroke="#0ea5e9" stroke-width="1.8" stroke-opacity="0.95"/>
      <!-- Bright leading edge wedge -->
      <path d="M148,110 L246,110 A98,98 0 0,0 234,138 Z"
        fill="url(#sweepFade)" opacity="0.85"/>
    </g>
  </g>

  <!-- Center dot -->
  <circle cx="148" cy="110" r="3" fill="#0ea5e9" filter="url(#blipGlow)"/>

  <!-- Radar blips (aircraft targets) -->
  <!-- Blip 1 -->
  <g filter="url(#blipGlow)">
    <circle cx="192" cy="78" r="3.5" fill="#38bdf8">
      <animate attributeName="opacity" values="0;0;1;1;0.4;1;0;0" dur="4s" begin="0.9s" repeatCount="indefinite"/>
    </circle>
  </g>
  <!-- Blip 2 -->
  <g filter="url(#blipGlow)">
    <circle cx="168" cy="148" r="3" fill="#38bdf8">
      <animate attributeName="opacity" values="0;0;0;1;1;0.6;1;0" dur="4s" begin="2.2s" repeatCount="indefinite"/>
    </circle>
  </g>
  <!-- Blip 3 -->
  <g filter="url(#blipGlow)">
    <circle cx="115" cy="88" r="2.5" fill="#7dd3fc">
      <animate attributeName="opacity" values="0;0;0;0;1;1;0.5;0" dur="4s" begin="3.1s" repeatCount="indefinite"/>
    </circle>
  </g>
  <!-- Blip 4 (larger — flagship target) -->
  <g filter="url(#blipGlow)">
    <circle cx="210" cy="115" r="4" fill="#0ea5e9">
      <animate attributeName="opacity" values="0;0;1;0.8;1;0.3;0;0" dur="4s" begin="0.4s" repeatCount="indefinite"/>
    </circle>
    <circle cx="210" cy="115" r="7" fill="none" stroke="#0ea5e9" stroke-width="0.8">
      <animate attributeName="opacity" values="0;0;0.6;0.3;0;0;0;0" dur="4s" begin="0.4s" repeatCount="indefinite"/>
      <animate attributeName="r" values="4;9;12;16" dur="1.5s" begin="0.4s" repeatCount="indefinite"/>
    </circle>
  </g>

  <!-- Range tick labels -->
  <g fill="#0ea5e9" fill-opacity="0.4" font-family="'Courier New',monospace" font-size="6">
    <text x="227" y="112">98NM</text>
    <text x="207" y="112">78</text>
    <text x="187" y="112">58</text>
  </g>

  <!-- ── DIVIDER ── -->
  <line x1="262" y1="14" x2="262" y2="206" stroke="#0ea5e9" stroke-width="0.5" stroke-opacity="0.3"/>

  <!-- ── TEXT PANEL (right side) ── -->

  <!-- Callsign label -->
  <text x="292" y="46" font-family="'Courier New',monospace" font-size="10"
    fill="#38bdf8" fill-opacity="0.7" letter-spacing="4">PILOT IDENTIFICATION</text>

  <!-- Name with glow -->
  <text x="290" y="98" font-family="'Courier New',monospace" font-size="38"
    font-weight="bold" fill="#ffffff" filter="url(#textGlow)" letter-spacing="1">
    M. BELLO SANI
  </text>

  <!-- Subtitle line 1 -->
  <text x="292" y="126" font-family="'Courier New',monospace" font-size="12.5"
    fill="#38bdf8" letter-spacing="1.5">
    AEROSPACE ENGINEER  ·  DIGITAL TWIN ARCHITECT
  </text>

  <!-- Subtitle line 2 -->
  <text x="292" y="148" font-family="'Courier New',monospace" font-size="11"
    fill="#7dd3fc" fill-opacity="0.75" letter-spacing="1">
    CNN-BiLSTM · PHM · Blockchain Avionics · AI/ML
  </text>

  <!-- Status bar -->
  <rect x="290" y="165" width="540" height="1" fill="#0ea5e9" fill-opacity="0.2"/>

  <!-- Status readouts -->
  <g font-family="'Courier New',monospace" font-size="9.5" fill="#0ea5e9" fill-opacity="0.6">
    <text x="292" y="182">STATUS:</text>
    <text x="345" y="182" fill="#4ade80" fill-opacity="0.9">■ ACTIVE</text>

    <text x="430" y="182">AFFILIATION:</text>
    <text x="510" y="182" fill="#38bdf8" fill-opacity="0.85">AFIT · BEIHANG UNIV.</text>

    <text x="292" y="200">PAPERS:</text>
    <text x="345" y="200" fill="#fbbf24" fill-opacity="0.9">AIAA JAIS  ·  IEEE TAES</text>

    <text x="640" y="200" fill="#38bdf8" fill-opacity="0.5">CGPA 4.10/5.00</text>
  </g>

  <!-- Blinking cursor after name -->
  <rect x="820" y="168" width="8" height="2" fill="#0ea5e9">
    <animate attributeName="opacity" values="1;0;1" dur="1.1s" repeatCount="indefinite"/>
  </rect>

  <!-- Corner HUD marks -->
  <g stroke="#0ea5e9" stroke-width="1" stroke-opacity="0.35" fill="none">
    <!-- Top-left -->
    <polyline points="4,18 4,4 18,4"/>
    <!-- Top-right -->
    <polyline points="842,4 856,4 856,18"/>
    <!-- Bottom-left -->
    <polyline points="4,202 4,216 18,216"/>
    <!-- Bottom-right -->
    <polyline points="842,216 856,216 856,202"/>
  </g>

  <!-- Top HUD label -->
  <text x="50%" y="13" text-anchor="middle" font-family="'Courier New',monospace"
    font-size="8" fill="#0ea5e9" fill-opacity="0.35" letter-spacing="6">
    AIR FORCE INSTITUTE OF TECHNOLOGY  //  KADUNA
  </text>
</svg>

</div>

<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=18&duration=3000&pause=800&color=38BDF8&center=true&vCenter=true&multiline=false&repeat=true&width=700&lines=CNN-BiLSTM+Edge+Digital+Twin+%7C+AIAA+JAIS+2026;Blockchain+Avionics+Security+%7C+IEEE+TAES+2026;Physics-Informed+Machine+Learning+for+Aviation;Incoming+M.Sc.+%40+Beihang+University+%7C+Smart+Aviation)](https://git.io/typing-svg)

</div>

<div align="center">

<a href="https://smbello.vercel.app">
  <img src="https://img.shields.io/badge/MISSION_STATUS-OPERATIONAL-0ea5e9?style=for-the-badge&logo=vercel&logoColor=white&labelColor=0f172a"/>
</a>
&nbsp;
<a href="https://smbello.vercel.app">
  <img src="https://img.shields.io/badge/🌐_Portfolio-smbello.vercel.app-0f172a?style=for-the-badge&logoColor=white"/>
</a>
&nbsp;
<a href="https://www.linkedin.com/in/mohammed-bello-sani-369a89284">
  <img src="https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white"/>
</a>
&nbsp;
<a href="mailto:bellosani2drescue@gmail.com">
  <img src="https://img.shields.io/badge/Email-Contact_Me-ea580c?style=for-the-badge&logo=gmail&logoColor=white"/>
</a>

<br/><br/>

<img src="https://komarev.com/ghpvc/?username=SMBello&color=0ea5e9&style=flat-square&label=Profile+Views" alt="Profile Views"/>
&nbsp;
<img src="https://img.shields.io/github/followers/Sm-bello?color=0ea5e9&style=flat-square&label=Followers" alt="Followers"/>

</div>

---

<div align="center">

```
┌─────────────────────────────────────────────────────────────────────┐
│  AEROTWIN SYSTEM STATUS — DORNIER 228-212 LANDING GEAR MONITOR      │
├──────────────────────┬──────────────────────┬───────────────────────┤
│  Model Accuracy      │  Fault Classes       │  Inference Latency    │
│  ██████████  98.5%   │  11 Conditions       │  47 ms on Edge        │
├──────────────────────┼──────────────────────┼───────────────────────┤
│  Training Cycles     │  Feature Vectors     │  Cost vs. HUMS        │
│  9,500 (physics)     │  273 per window      │  350× cheaper         │
└──────────────────────┴──────────────────────┴───────────────────────┘
```

</div>

---

## 📡 Mission Briefing

<img align="right" width="340" src="https://github-readme-activity-graph.vercel.app/graph?username=Sm-bello&bg_color=0f172a&color=38bdf8&line=0ea5e9&point=ffffff&area=true&hide_border=true&radius=8"/>

I'm a final-year Aerospace Engineering student at **AFIT Kaduna** (CGPA 4.10/5.00) and an incoming M.Sc. candidate at **Beihang University's Smart Aviation Center** (Hangzhou International Innovation Institute).

My work lives at the intersection of **physics-informed machine learning**, **aviation digital twins**, and **secure avionics communication**. I don't just simulate aircraft — I build systems that monitor, predict, and defend them.

**Active Research:**
- 📄 `AIAA JAIS` — *AeroTwin: CNN-BiLSTM Edge Digital Twin for Landing Gear PHM* (MS ID: 2026-02-I011895)
- 📄 `IEEE TAES` — *PHI-CHAIN: Blockchain Security for Avionics Comm* (Ref: TAES-2026-0772)

<br clear="right"/>

---

## 🛠️ Technical Loadout

<div align="center">

**Core Engineering Stack**

![MATLAB](https://img.shields.io/badge/MATLAB-0076A8?style=for-the-badge&logo=mathworks&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Simulink](https://img.shields.io/badge/Simulink-8E44AD?style=for-the-badge&logo=mathworks&logoColor=white)
![FlightGear](https://img.shields.io/badge/FlightGear-1a1a2e?style=for-the-badge&logo=airplane&logoColor=38bdf8)

**Data & Telemetry**

![InfluxDB](https://img.shields.io/badge/InfluxDB-22ADF6?style=for-the-badge&logo=influxdb&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![MQTT](https://img.shields.io/badge/MQTT-3C5280?style=for-the-badge&logo=mqtt&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

**Security & Blockchain**

![Hyperledger](https://img.shields.io/badge/Hyperledger_Fabric-2F3134?style=for-the-badge&logo=hyperledger&logoColor=white)
![Ed25519](https://img.shields.io/badge/Ed25519_Signing-0f172a?style=for-the-badge&logo=gnuprivacyguard&logoColor=38bdf8)
![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=for-the-badge&logo=wireshark&logoColor=white)

**Dev & Platform**

![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![ANSYS](https://img.shields.io/badge/ANSYS_Workbench-FFB71B?style=for-the-badge&logo=ansys&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)

</div>

---

## 🚀 Flagship Projects

<table>
<tr>
<td width="50%" valign="top">

### 🛬 AeroTwin
**CNN-BiLSTM Edge Digital Twin**

[![Repo](https://img.shields.io/badge/GitHub-Sm--bello%2FAEROTWIN-0f172a?style=flat-square&logo=github)](https://github.com/Sm-bello/AEROTWIN-Dornier228-LandingGear-Dataset)
[![Kaggle](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=flat-square&logo=kaggle)](https://www.kaggle.com/)
[![Paper](https://img.shields.io/badge/Paper-AIAA_JAIS_2026-red?style=flat-square&logo=arxiv)](https://arc.aiaa.org/)

Physics-based digital twin for **Dornier 228-212** landing gear health monitoring. 9,500 physics-simulated landing cycles → 11-class fault classification at **98.5% accuracy** with **47 ms edge latency**. Delivers **350× cost reduction** vs. commercial HUMS.

`CNN-BiLSTM` · `MATLAB Simscape` · `SHAP` · `PHM`

</td>
<td width="50%" valign="top">

### 🔐 PHI-CHAIN
**Blockchain Avionics Security Framework**

[![Paper](https://img.shields.io/badge/Paper-IEEE_TAES_2026-blue?style=flat-square&logo=ieee)](https://ieeexplore.ieee.org/)

Hyperledger Fabric + Ed25519 + Merkle batching to secure **ADS-B, ACARS, CPDLC, ADS-C, and Telemetry** channels. Features a Physics-Informed Digital Twin Validator (PIDT) for semantic anomaly detection beyond cryptographic checks.

`Hyperledger Fabric` · `Ed25519` · `Merkle Tree` · `PIDT`

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🔥 Gas Turbine Ignition DT
**Reliability-Centred Digital Twin**

[![Repo](https://img.shields.io/badge/GitHub-B787--Ignition--DT-0f172a?style=flat-square&logo=github)](https://github.com/Sm-bello/B787-ignition-digital-twin)
[![Kaggle](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?style=flat-square&logo=kaggle)](https://www.kaggle.com/)

26,000-sample FMEA-backed digital twin for B787 ignition systems. 11-mode failure analysis, reliability block diagrams, RF/XGBoost/LightGBM ensemble with SMOTE balancing. Submitted to *Reliability Engineering & System Safety*.

`FMEA` · `Reliability Engineering` · `SMOTE` · `RESS`

</td>
<td width="50%" valign="top">

### 🤖 Penelope — Sovereign AI Agent
**Fully Offline Hardware-Fingerprinted Agent**

Local model router running on HP ProBook via WSL2. Auto-routes to `phi4:14b` → `qwen2.5-coder:7b` → `deepseek-r1:7b` based on task class. Calls MATLAB, ANSYS, and FlightGear via Windows interop. Upgrades to cloud (OpenRouter) when internet is detected.

`Ollama` · `WSL2` · `phi4` · `MATLAB interop`

</td>
</tr>
</table>

---

## ✈️ Operational Experience

<div align="center">

```
╔══════════════════════════════════╦══════════════════════════════════╗
║  🏛️  NCAA — Airworthiness Dept.  ║  🔧  Executive Airlift — MRO     ║
╠══════════════════════════════════╬══════════════════════════════════╣
║  Technical log audits            ║  Wheel assembly overhauls        ║
║  Certification documentation     ║  Hydraulic system checks         ║
║  Regulatory standards review     ║  VIP aircraft line maintenance   ║
║  Airworthiness standards         ║  Abuja International Airport     ║
╚══════════════════════════════════╩══════════════════════════════════╝
```

</div>

---

## 🎓 Academic & Research Milestones

<div align="center">

| Year | Milestone |
|------|-----------|
| 2026 | 📄 Manuscript submitted — *AIAA Journal of Aerospace Information Systems* |
| 2026 | 📄 Manuscript submitted — *IEEE Transactions on Aerospace & Electronic Systems* |
| 2026 | 🎓 B.Eng. Aerospace Engineering — AFIT Kaduna *(Expected)* |
| 2026 | 🏛️ M.Sc. Electronic Information — Beihang University, Smart Aviation Center |
| 2026 | 🏆 MathWorks Drone Competition — Virtual Line-Follower Track |
| 2025 | 📦 Datasets published on Kaggle — AeroTwin + Gas Turbine Ignition DT |

</div>

---

## 📊 GitHub Analytics

<div align="center">
  <img height="165em" src="https://github-readme-stats.vercel.app/api?username=Sm-bello&show_icons=true&theme=tokyonight&include_all_commits=true&count_private=true&hide_border=true&bg_color=0f172a&title_color=38bdf8&icon_color=0ea5e9&text_color=94a3b8"/>
  &nbsp;
  <img height="165em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Sm-bello&layout=compact&langs_count=7&theme=tokyonight&hide_border=true&bg_color=0f172a&title_color=38bdf8&text_color=94a3b8"/>
</div>

<div align="center">
  <br/>
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=Sm-bello&theme=tokyonight&hide_border=true&background=0f172a&ring=38bdf8&fire=0ea5e9&currStreakLabel=38bdf8&sideLabels=94a3b8&dates=475569"/>
</div>

---

## 🏆 GitHub Trophies

<div align="center">
  <img src="https://github-profile-trophy.vercel.app/?username=Sm-bello&theme=darkhub&no-frame=true&no-bg=false&margin-w=6&column=7"/>
</div>

---

## 🐍 Contribution Activity

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Sm-bello/Sm-bello/output/github-snake-dark.svg"/>
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Sm-bello/Sm-bello/output/github-snake.svg"/>
    <img alt="contribution snake animation" src="https://raw.githubusercontent.com/Sm-bello/Sm-bello/output/github-snake-dark.svg"/>
  </picture>
</div>

<div align="center">

**💬 Current Focus**

*Beihang M.Sc. prep · IEEE TAES revision · MATLAB Onramp certifications · Upwork freelance launch*

<br/>

[![forthebadge](https://img.shields.io/badge/Open_To-Research_Collaboration-0ea5e9?style=for-the-badge&logo=academia&logoColor=white)]()
[![forthebadge](https://img.shields.io/badge/Available_For-Aviation_AI_Projects-1e3a5f?style=for-the-badge&logo=airplane&logoColor=white)]()

<br/>

> *"The aircraft does not lie. Every vibration is a sentence. I build the translators."*

</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f172a,50:1e3a5f,100:0ea5e9&height=100&section=footer&animation=fadeIn"/>
