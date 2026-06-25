---
language: en
tags:
  - behavioral-science
  - psychological-research
  - research-methodology
  - group-dynamics
  - llm-training-data
  - ai-training-data
  - role-playing-research
  - data-collection
  - verification-method
  - bivrest-method
license: mit
---

[![GitHub stars](https://img.shields.io/github/stars/olesyalazareva/bivrest-method.svg?style=social)](https://github.com/olesyalazareva/bivrest-method/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# BIVREST — Group Verification Protocol for Role-Based Behavior

**Version:** 1.0  
**Status:** Registered in NRIS (Russian Scientific Research Registry)

---

## 📑 Table of Contents

- [Method Description](#method-description)
- [Who Is BIVREST For](#who-is-bivrest-for)
- [How the Protocol Works](#how-the-protocol-works)
- [Data Structure](#data-structure)
- [Quick Start](#quick-start)
- [Implementation in UNIVERSE 69 Game](#implementation-in-universe-69-game)
- [Limitations](#limitations)
- [Citation](#citation)
- [Contacts](#contacts)

---

## Method Description

**The Problem:** In role-playing games and research sessions, it's difficult to objectively assess the quality of roleplay. The facilitator's assessment is subjective, participants lack unified criteria, and data is hard to structure and compare.

Traditional data collection methods (interviews, surveys, focus groups) produce distorted results due to social desirability bias. Participants say what is "socially acceptable" rather than what they actually think.

**What BIVREST Offers:** A unified assessment mechanism through group voting. The group votes "Believe / Don't Believe" after each action. The verdict is determined by majority vote. The result is recorded in a structured log.

**This protocol is designed for data collection in situations where conventional methods (interviews, surveys) produce distorted results due to social desirability.** Role-playing helps reduce this effect because participants act as characters, not as themselves.

BIVREST is a data collection protocol based on role-playing games. It relies on the binary voting mechanism **"Believe / Don't Believe"**.

The protocol records:
- participant actions
- group voting results
- final verdict

All of this is saved in a structured log.

---

## Who Is BIVREST For

| Audience | Purpose |
|---|---|
| **Researchers** | Collect structured data on role-based behavior in conditions where social desirability interferes with obtaining truthful responses |
| **Psychologists** | Record group dynamics and moments of role breakdown |
| **Game Designers** | Ready-made mechanics for evaluating roleplay to integrate into games |
| **AI Engineers** | Protocol for collecting labeled data for model training |

### Name Breakdown

| Letter | Meaning | Description |
|---|---|---|
| **B** | Bifurcation | Gap between the "Self" and the avatar |
| **I** | Inversion | Acting through the opposite role |
| **V** | Verification | "Believe / Don't Believe" mechanism |
| **R** | Role | Avatar as a protective screen |
| **E** | Empty | Deconstruction through the "Empty Chair" |
| **S** | Script | The script to be deconstructed |
| **T** | Therapy | Integration of a new script |

---

## How the Protocol Works

### Protocol Participants

| Role | Description |
|---|---|
| **Group** | Minimum 3 people, vote after each action |
| **Observer** | Records voting results and maintains the log |
| **Facilitator** | Manages the session, assigns tasks (optional) |

### Voting Criterion

BIVREST doesn't prescribe a specific criterion — it's set before the session begins.

**Examples of criteria:**
- "Does this action match the role?"
- "Does this look convincing?"
- "Is this truthful in the game context?"

The group votes "Believe / Don't Believe" according to the defined criterion.

### Protocol Stages

| Letter | Stage | Action |
|---|---|---|
| **B** | Believe / Don't Believe | The group votes according to the defined criterion |
| **I** | Information | Presenting information for evaluation |
| **V** | Voting | Each participant casts their vote |
| **R** | Record | Recording the voting results |
| **E** | Evaluate | Determining the verdict by majority |
| **S** | Store | Saving the structured log |
| **T** | Transfer | Transferring data for analysis |

### Complete Iteration Cycle

**Participant Action → Group Voting → Result Recording → Log Entry**

Each iteration produces one entry in the log.

---

## Data Structure

### Log Format

| Field | Type | Description |
|---|---|---|
| `session_id` | string | Session identifier |
| `round` | integer | Round number |
| `player_id` | string | Player identifier |
| `avatar` | string | Player's role |
| `task` | string | Task from the card |
| `action_text` | text | Roleplay (what was said/done) |
| `votes_believe` | integer | Number of "Believe" votes |
| `votes_dont_believe` | integer | Number of "Don't Believe" votes |
| `verdict` | string | "Believe" or "Don't Believe" |
| `tokens_lost` | integer | How many tokens were lost |
| `empty_chair` | boolean | Whether role exit occurred |

**Example of a filled log:** [session_example.en.txt](session_example.en.txt)

**Empty template for filling:** [templates/log_template.csv](templates/log_template.csv)

---

## 🚀 Quick Start

### 1. Download the Protocol Description
This repository contains everything you need to conduct a research session.

### 2. Read the Key Documents
- **[Protocol Specification](protocol_specification.en.md)** — technical details for researchers
- **[Annotation Guide](annotation_guide.en.md)** — for those labeling data for AI
- **[Log Example](session_example.en.txt)** — what a filled record looks like

### 3. Conduct a Session
1. Gather a group (minimum 3 people)
2. Agree on a voting criterion (e.g., "Does the action match the role?")
3. After each action — vote "Believe / Don't Believe"
4. Record the results in the log (template available in `templates/`)

### 4. Analyze the Data
The resulting log can be used for:
- Statistical analysis of behavior
- Training LLMs to recognize persuasiveness
- Group dynamics research

**If you need consultation on applying the method** — contact the author (contacts below).

---

## Implementation in UNIVERSE 69 Game

UNIVERSE 69 is a game where BIVREST is built in as a core mechanic. Full rules, cards, and roles are in a separate repository:

**→ [UNIVERSE 69 on GitHub](https://github.com/olesyalazareva/universe-69)**

### How BIVREST Is Integrated into UNIVERSE 69 Mechanics

| UNIVERSE 69 Mechanic | Role in BIVREST |
|---|---|
| **Task Cards** | Generate information for evaluation (Stage I — Information) |
| **Avatars (Roles)** | Set the context in which actions are evaluated |
| **"Believe / Don't Believe" Voting** | Core verification mechanism (Stage B — Believe) |
| **"Chance" Tokens** | Resource lost on "Don't Believe" (sanction mechanism) |
| **"Empty Chair"** | Role exit upon repeated "Don't Believe" (Stage E — Empty) |
| **Logging** | Recording all actions and votes (Stages R, E, S) |

BIVREST can be used with other role-playing systems, but in UNIVERSE 69 it's implemented as a ready-made mechanic.

---

## Limitations

- Voting results reflect group opinion, not objective truth
- The protocol doesn't guarantee consistency of assessments across different groups
- Multiple sessions are required for statistically significant data
- A ready-made dataset is not provided

---

## Citation

```bibtex
@misc{lazareva2025bivrest,
  author = {Lazareva, Olesya},
  title = {BIVREST: Group Verification Protocol for Role-Based Behavior},
  year = {2025},
  howpublished = {GitHub},
  url = {https://github.com/olesyalazareva/bivrest-method}
}
Contacts
Olesya Lazareva
Psychoanalyst-Sexologist, Game Master with 25 years of experience

Telegram: @olesyalazarevalove

Email: psi-tech@yandex.com

Method Status: Registered in NRIS (Russian Scientific Research Registry)

License and Terms
Non-commercial use (scientific research, open-source projects) — free with mandatory attribution and link to this repository

Commercial use (selling AI solutions based on BIVREST, corporate implementations) — by agreement with the author

⭐ If this method is useful for your work, please star the repository — so other researchers and engineers can find it.
