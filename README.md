# IndexTTS2 – Enhanced Fork (Batching + Duration Control + Speed)

This repository is a [**modified fork of IndexTTS-2**](https://github.com/index-tts/index-tts).
The goal of this fork is to keep full compatibility with the original project while adding batch inference and controlling the speed of speech.

This fork includes major improvements implemented in **`infer_v2.py`** :

### ✅ New Features

* **Batch Inference (`infer_batch`)**
  Generate audio for **multiple speakers / texts / outputs in one pass**, reducing overhead and drastically improving speed.
* **Target Audio Duration (`target_length_ms`)**
  Precisely control the **final length** of the generated speech, either globally or **per-item** in a batch.
* **Speed Control (`speed`)**
  Adjust speaking rate without retraining models.
* **Improved segmentation & padding logic** for more stable long-text generation.
* **Second-stage GPT batching** for ~40–60% faster inference with multi-segment inputs.
* Drop-in replacement for the original `infer()` with total backward compatibility.

### 🗂 File Overview

* **`infer_v2.py`** – contains the upgraded **IndexTTS2** class with batching, duration control, and speed options.
  (Full file included at: )

* **`README.md` (original)** – basic project metadata from the upstream version.
  (Included at: )

### 🚀 Usage

[target_length_ms usage is optional]

#### **Single Inference**

```python
tts = IndexTTS2(...)
tts.infer(
    spk_audio_prompt="speaker.wav",
    text="Hello world!",
    output_path="out.wav",
    speed=1.2,
    target_length_ms=5000
)
```

#### **Batch Inference**

```python
tts.infer_batch(
    spk_audio_prompts=["s1.wav", "s2.wav"],
    texts=["Hello", "World"],
    output_paths=["out1.wav", "out2.wav"],
    speed=1.0,
    target_length_ms=[4000, 2500]   # per-item durations
)
```

### 🔗 Credits

All base models, structure, and original implementation belong to the **IndexTTS** team.
This repo only extends the inference logic and adds production-oriented improvements.

---

