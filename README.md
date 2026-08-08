# AI See & Speak 🎨🔊

An interactive AI application that looks at an image, describes it in natural language, answers questions about it, and reads the result out loud — while also showing which parts of the image the model actually focused on.

🔗 **Live demo:** [Try it here](https://ai-see-and-speak-v2rg5dqb7dppifxwdqskeg.streamlit.app/)


---

## What it does

Upload any image, and choose one of two modes:

- **Describe** — generates a caption in one of three styles: *simple*, *detailed*, or *funny*
- **Ask** — ask a natural-language question about the image (e.g. "What color is his suit?") and get an answer

Every result is also converted to speech, and you can see a **saliency map** showing which regions of the image most influenced the model's output — a step toward making the model's decisions interpretable rather than treating it as a black box.

## How it works

```
Image
  │
  ├── Describe mode ──> BLIP (image captioning) ──> styled caption
  │
  └── Ask mode ────────> BLIP-VQA (visual question answering) ──> answer
                              │
                              ├──> gTTS ──> spoken audio
                              │
                              └──> Gradient-based saliency map ──> heatmap overlay
```

## Tech stack

- **BLIP** (`Salesforce/blip-image-captioning-base`) — image captioning, conditioned on style via prompt prefixes
- **BLIP-VQA** (`Salesforce/blip-vqa-base`) — visual question answering
- **gTTS** — text-to-speech
- **Gradient-based saliency maps** — model interpretability, computed from the gradient of the output with respect to input pixels
- **Streamlit** — web interface
- **Streamlit Community Cloud** — deployment

## Running it locally

```bash
git clone https://github.com/ayaalrahman1/ai-see-and-speak.git
cd ai-see-and-speak
pip install -r requirements.txt
streamlit run app.py
```

## Notes and limitations

- The base BLIP model was trained for captioning, not instruction-following — so styles like "funny" don't always land the way a chat-style model would handle them.
- VQA answers tend to be short (often a single word), reflecting the style of the dataset BLIP-VQA was trained on.
- The model can occasionally hallucinate details not actually present in the image — the saliency map helps surface when that's happening.

## About this project

Built as a self-directed learning project after graduating, to practice computer vision, NLP, and applied deep learning end-to-end — from model selection through deployment.
