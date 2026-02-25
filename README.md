[README.md](https://github.com/user-attachments/files/25531692/README.md)
# 🌵 AI Comic: "The Misguided Enthusiasm of the Little Cactus Boy"

> *A children's story about self-acceptance, generated entirely by AI.*

This project is a fully automated **AI comic book pipeline** that produces a 41-scene illustrated comic — complete with dialogue, speech bubbles, and a PDF output — using a combination of large language models and image diffusion models.
This project helps in practical to help people who has the ability to make comic storyies and they have the ability to visualize images and events, but they do not possess professional drawing skills or drawing skills at all!
so this project we help them by to do that by justing identifing there prompts for each panal he wants to make it and the style for the comic and comsistant prompt for each charcter in the story he/she has.

LinkedIn post --> (https://www.linkedin.com/posts/ahmed-dawod-bakr_llm-llama3-stablediffusion-ugcPost-7432019670947479552-zja2?utm_source=share&utm_medium=member_desktop&rcm=ACoAAEl1U90Br7kCP1FcNorK3QnQw_3y31b3hwE)

Drive contain the Comic and the project --> (https://drive.google.com/drive/folders/1EqDVZsoPxtjT1Qgx0xNhV7E9Zk75C2Tg?usp=drive_link)

---

## 📖 Story Summary

A small cactus boy goes to school for the first time and becomes fascinated with the rain-plant classroom. Embarrassed by his thorns, he removes them to fit in — only to get sick, become vulnerable to bird attacks, and learn a hard lesson about embracing who you are. The story unfolds across **8 acts and 41 scenes**, from morning and car ride through to rescue, resolution, and a happy ending.

---

## 🧠 Pipeline Overview

The pipeline runs entirely inside **Google Colab** and proceeds in these steps:

```
STEP 0  → Install dependencies
STEP 0B → Load API keys (Groq + HuggingFace) via Colab Secrets
STEP 1  → Imports & device setup
STEP 2  → Token count helper (CLIP tokenizer)
STEP 3  → Optional style reference image upload
STEP 4  → Character visual anchors + STYLE definition
STEP 5  → Story outline: 41 scenes across 8 acts
STEP 6  → Llama 3.1 8B via Groq API → 41 dialogues (0 VRAM)
STEP 7  → Load FLUX.1-dev (~33 GB VRAM)
STEP 8  → Generate 41 × 1024×1024 images (flat 2D cartoon style)
FREE B  → Unload FLUX.1-dev
STEP 9  → Add 50px speech bubbles (Llama-generated dialogue)
STEP 10 → Load LongCLIP for evaluation (~1 GB VRAM)
STEP 10B→ LongCLIP CLIP score per scene
FREE C  → Unload LongCLIP
STEP 11 → GPT-2 perplexity (story coherence)
STEP 12 → Human evaluation (3 sections, filled manually)
STEP 13 → Comic book PDF (6 panels per page)
STEP 14 → Evaluation report PDF
STEP 15 → Final submission package (ZIP)
```

---

## 🤖 Models Used

| Role | Model | VRAM |
|------|-------|------|
| Dialogue generation | Llama 3.1 8B Instruct via [Groq API](https://console.groq.com) | 0 GB (remote) |
| Image generation | [FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev) | ~33 GB |
| CLIP evaluation | [LongCLIP zer0int/LongCLIP-GmP-ViT-L-14](https://huggingface.co/zer0int/LongCLIP-GmP-ViT-L-14) | ~1 GB |
| Story coherence | GPT-2 (perplexity) | minimal |

> **GPU requirement:** The full pipeline requires ~33 GB VRAM for FLUX.1-dev.  
> An **H100 (80 GB)** was used for image generation in this project.

---

## ⚙️ Setup & Usage

### 1. Open in Google Colab
Upload the `.ipynb` notebook to [colab.research.google.com](https://colab.research.google.com) and set the runtime to **GPU (A100 or H100)**.

### 2. Add API Keys via Colab Secrets
Go to the 🔑 **Secrets** panel in the left sidebar and add:

| Secret Name | Value | Where to get it |
|-------------|-------|-----------------|
| `GROQ_API_KEY` | `gsk_...` | [console.groq.com](https://console.groq.com) → API Keys → Create |
| `HF_TOKEN` | `hf_...` | [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens) |

> ⚠️ You must also accept the FLUX.1-dev model gate at:  
> [huggingface.co/black-forest-labs/FLUX.1-dev](https://huggingface.co/black-forest-labs/FLUX.1-dev)

### 3. Run All Cells
Run all cells top-to-bottom. The notebook is designed to free GPU memory between heavy steps automatically.

---

## 📦 Output Files

After running the full pipeline, the following are generated in `comic/`:

- `comic/images/scene_NNN.png` — Raw generated panels (1024×1024)
- `comic/images/scene_NNN_final.png` — Panels with speech bubbles
- `comic/The Misguided Enthusiasm of the Little Cactus Boy.pdf` — Full comic book PDF
- `comic/Evaluation_Report.pdf` — Metrics and human evaluation report
- `comic/evaluation/results.json` — All evaluation data in JSON format
- `AI_Comic_Submission/` — Final submission folder

---

## 📊 Evaluation Metrics

The pipeline automatically computes:

- **LongCLIP score** — image-text alignment per scene (target: avg ≥ 25)
- **GPT-2 Perplexity** — story coherence of generated dialogue (target: < 50)
- **Human evaluation** — 3 reviewers score story, visuals, characters, dialogue (1–5 scale)

---

## 🌵 Characters

| Character | Description |
|-----------|-------------|
| **Cactus Boy** | Small green cactus child, round body, big eyes, red backpack |
| **Father Cactus** | Tall mature cactus adult, glasses, thick spines, wise and kind |
| **Monkey Orchid** | Orchid flower with monkey-face petal pattern, purple/white |
| **Rain Plant** | Tropical plant, large leaves, water droplets, cheerful |

All characters are rendered in **pure flat 2D vintage Disney cartoon style** — hand-drawn look, bold black outlines, no gradients or shading.

---

## 📜 Story Acts

| Act | Scenes | Summary |
|-----|--------|---------|
| Morning & Car Ride | 1–5 | Waking up; father drives to school and gives wise advice |
| School Arrival | 6–10 | Amazed by other plants; bored in his own desert classroom |
| Recess Drama | 11–14 | Enters rain classroom; laughed at for his thorns |
| Monkey Orchid | 15–19 | Orchid warns him; he mocks her instead of listening |
| Bad Decision | 20–25 | Removes thorns; joins rain class; gets sick from water |
| Walk Home & Attack | 26–31 | Father can't come; birds attack the thornless cactus |
| Rescue | 32–35 | Father arrives just in time and drives him to safety |
| Resolution | 36–41 | He confesses, learns his lesson, wakes up proud of himself |

---

## 📋 Requirements

See [`requirements.txt`](requirements.txt) for the full dependency list.  
All packages are installed automatically by the notebook's first cell.

---

## 💡 Notes

- FLUX.1-dev does **not** support negative prompts — style control is achieved entirely through the positive prompt using explicit language like *"flat 2D cartoon, NOT realistic, NOT 3D rendered"*.
- Dialogue generation via Groq API uses zero local VRAM and completes in under 30 seconds for all 41 scenes.
- The LongCLIP model supports up to 248 tokens, which is why scene evaluation uses the short `scene_context` field rather than the full image prompt.

---

## 🙏 Acknowledgements

This project was built over approximately **3 weeks**. For the final 2 days of image generation, an **H100 GPU** was generously made available by a friend — without which the FLUX.1-dev generation would not have been possible. *Alhamdulillah.*

Story concept and project direction by the user. AI models used under their respective open licenses.
