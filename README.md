```markdown
# 🗣️ Automatic Speech Recognition + Speaker Diarization on LibriTTS

This repository demonstrates a full speech processing pipeline using:
- **OpenAI Whisper** for **Automatic Speech Recognition (ASR)**
- **pyannote-audio** for **Speaker Diarization**

🎯 Built on the [LibriTTS Dev Clean dataset](https://www.kaggle.com/datasets/luizfelipebjcosta/libri-tts-dev/data)

---

## 📁 Dataset

**LibriTTS Dev Clean**  
➡️ Download from [Kaggle](https://www.kaggle.com/datasets/luizfelipebjcosta/libri-tts-dev/data)  
📦 File: `dev-clean.zip`  
📂 Extract to:
```

/content/audio/dev-clean/

```

Dataset file structure:
```

/dev-clean/{speaker\_id}/{chapter\_id}/{utterance\_id}.wav
/dev-clean/{speaker\_id}/{chapter\_id}/{utterance\_id}.normalized.txt

````

---

## 🛠️ Setup

Install dependencies:
```bash
pip install -U openai-whisper
pip install git+https://github.com/pyannote/pyannote-audio
````

Authenticate with Hugging Face (for diarization):

```python
from huggingface_hub import login
login()  # Paste your Hugging Face token when prompted
```

---

## 🔄 Pipeline Overview

### ✅ Step 1: Transcription using Whisper

Randomly sample 2 audio files from 5 folders → transcribe → save output as `.json`.

Output format:

```json
{
  "file_name": "1993_147965_000003_000003.wav",
  "language": "en",
  "text": "this is a sample transcription.",
  "segments": [
    {
      "start": 0.0,
      "end": 2.3,
      "text": "this is a sample"
    },
    ...
  ]
}
```

📁 Output folder: `/content/transcriptions_json/`

---

### 🔊 Step 2: Speaker Diarization

Use `pyannote/speaker-diarization` to identify who spoke when. Each Whisper transcript is aligned with diarized segments.

Output format:

```json
{
  "file": "1993_147965_000003_000003.wav",
  "language": "en",
  "segments": [
    {
      "start": 0.15,
      "end": 2.50,
      "speaker": "SPEAKER_00",
      "text": "hello how are you"
    },
    ...
  ]
}
```

📁 Output folder: `/content/diarized_outputs/`

---

## 📁 Directory Structure

```
📦 project-root/
├── audio/
│   └── dev-clean/               # LibriTTS dataset
├── transcriptions_json/        # Whisper transcription outputs
├── diarized_outputs/           # Speaker-labeled transcription outputs
├── speech_to_text.ipynb        # Colab notebook (optional)
└── README.md
```

---

## 📌 Future Improvements

* [ ] Add speaker embedding comparison to improve diarization
* [ ] Add evaluation using CER or BLEU
* [ ] Streamlit app for UI-based exploration

---

## 🙋‍♀️ Author

**Jasleen Kaur**
🎓 M.Tech (ESC), NIT Rourkela
💼 [LinkedIn](https://www.linkedin.com/in/jasleen-kaur-ml)

---

## 🤝 Contributing

Pull requests are welcome! If you’d like to contribute:

```bash
# 1. Fork this repository
# 2. Create your feature branch
git checkout -b feature/your-feature-name
# 3. Commit and push your changes
git commit -m "Add your feature"
git push origin feature/your-feature-name
# 4. Open a Pull Request!
```

---

## 📜 License

This project is licensed under the MIT License.
Credits to [OpenAI Whisper](https://github.com/openai/whisper) and [pyannote-audio](https://github.com/pyannote/pyannote-audio).

---

## 🌟 Acknowledgements

* [LibriTTS Dataset (Kaggle)](https://www.kaggle.com/datasets/luizfelipebjcosta/libri-tts-dev/data)
* [OpenAI Whisper](https://github.com/openai/whisper)
* [pyannote-audio by Hervé Bredin](https://github.com/pyannote/pyannote-audio)

---


