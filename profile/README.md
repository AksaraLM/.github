<p align="center">
  <img src="https://raw.githubusercontent.com/AksaraLLM/.github/main/banner.png" alt="AksaraLLM" width="720">
</p>

<h1 align="center">AksaraLLM</h1>

<p align="center">
  <strong>Open-source Indonesian Large Language Models — fully transparent, community-built.</strong><br>
  <em>Bahasa, kode, data, dan bobot. Semuanya terbuka.</em>
</p>

<p align="center">
  <a href="https://huggingface.co/spaces/AksaraLLM/Kiel-Pro-0.5B-v3-chat-demo"><img src="https://img.shields.io/badge/%F0%9F%A4%97-Try%20Demo-yellow" alt="Try Demo"></a>
  <a href="https://huggingface.co/AksaraLLM"><img src="https://img.shields.io/badge/%F0%9F%A4%97%20HuggingFace-Models-yellow" alt="HuggingFace"></a>
  <a href="https://discord.gg/aksarallm"><img src="https://img.shields.io/badge/Discord-Join-7289da?logo=discord&logoColor=white" alt="Discord"></a>
  <a href="https://github.com/AksaraLLM"><img src="https://img.shields.io/badge/License-Apache%202.0-blue" alt="License"></a>
  <a href="https://github.com/AksaraLLM/community/blob/main/GPU_DONATIONS.md"><img src="https://img.shields.io/badge/Sponsor-GPU-blue?logo=githubsponsors" alt="Sponsor"></a>
</p>

---

## 🌏What is AksaraLLM?

**AksaraLLM** is a community-driven effort to build truly open-source Large Language Models for Indonesian and Southeast Asian languages. "Open-weight" releases publish only model weights — we open-source everything: weights, data composition, training code, tokenizer, evaluation harness, and decision-making process (RFCs, meeting notes, training logs).

> *"Aksara"* (अक्षर) means "letter / script" — a nod to making AI literacy and language technology accessible across Southeast Asia.

## 🎯 Try It Now

Pengguna casual: chat langsung di browser tanpa setup —
**👉 [huggingface.co/spaces/AksaraLLM/Kiel-Pro-0.5B-v3-chat-demo](https://huggingface.co/spaces/AksaraLLM/Kiel-Pro-0.5B-v3-chat-demo)**

Pengguna lokal (laptop CPU, no GPU needed):
```bash
huggingface-cli download AksaraLLM/Kiel-Pro-0.5B-v3-chat-GGUF \
  Kiel-Pro-0.5B-v3-chat.q4_k_m.gguf Modelfile --local-dir .
ollama create aksara-kiel-pro -f Modelfile
ollama run aksara-kiel-pro "Halo, siapa kamu?"
```

## 📦 Current Lineup (jujur)

| Model | Params | Format | Best For | PPL (id-wiki) | Notes |
|---|---:|---|---|---:|---|
| [Kiel-Pro-0.5B-v3](https://huggingface.co/AksaraLLM/Kiel-Pro-0.5B-v3) | 494M | safetensors + GGUF | Edge / CPU / mobile | 14.7 | base completion model |
| [Kiel-Pro-0.5B-v3-chat](https://huggingface.co/AksaraLLM/Kiel-Pro-0.5B-v3-chat) | 494M | safetensors + GGUF | Chat lokal kecil | 14.7 | identity-calibrated chat |
| [AksaraLLM-Qwen-1.5B-v5-public](https://huggingface.co/AksaraLLM/AksaraLLM-Qwen-1.5B-v5-public) | 1.78B | safetensors + GGUF | General use | **8.4** | best quality so far |
| [aksarallm-1.5b-native](https://huggingface.co/AksaraLLM/aksarallm-1.5b-native) | 2.04B | safetensors + GGUF | Research preview | 113 | from-scratch, ID-only, undertrained |

**In training (parallel TPU run, 2025):**
- `aksarallm-2b-dense` — from-scratch on 132B kept-tokens corpus, custom 131K BPE tokenizer
- Future: 7B and 20B targets pending TPU capacity

## 🧪 Honest evaluation (CPU bench, 2 threads)

| Model (q4_k_m GGUF) | pp32 prefill | tg16 generation | Indonesian sample (greedy) |
|---|---:|---:|---|
| Kiel-Pro-0.5B-v3-chat | 36.8 t/s | **21.6 t/s** | "Saya Kiel-Pro, model bahasa Indonesia dari proyek AksaraLLM…" |
| Qwen-1.5B-v5-public | 23.7 t/s | 12.5 t/s | "Jakarta. Kota ini terletak di bagian tengah pulau Jawa…" *(fact mostly OK)* |
| aksarallm-1.5b-native | 17.2 t/s | 9.7 t/s | high PPL, semantik gibberish, untuk eksperimen saja |

> Detail audit + sample outputs jujur ada di README masing-masing model di HuggingFace.

## 📦 Repositories

| Repo | What | Status |
|---|---|---|
| [`aksaraLLM`](https://github.com/AksaraLLM/aksaraLLM) | Architecture, inference utilities | active |
| [`aksara-data`](https://github.com/AksaraLLM/aksara-data) | Corpus + SFT/DPO data builders | **active**, 132B-token corpus produced |
| [`aksara-train`](https://github.com/AksaraLLM/aksara-train) | Training scripts (pretrain / SFT / DPO, EasyDeL/JAX) | active, TPU pretrain running |
| [`aksara-tokenizer`](https://github.com/AksaraLLM/aksara-tokenizer) | 131K BPE multilingual tokenizer | active |
| [`aksara-eval`](https://github.com/AksaraLLM/aksara-eval) | Evaluation harness (IndoMMLU, IndoNLU, identity, leak) | active |
| [`community`](https://github.com/AksaraLLM/community) | Governance, RFCs, contribution docs | active |

## 🗺 Realistic roadmap (2026)

| Quarter | Goal |
|---|---|
| **Q2** (now) | Corpus 132B+ tokens deduped ✓ · 2B from-scratch run on TPU v6e-8 (in progress) · Identity SFT for 1.5B (queued, pending TPU) · HF Space demo ✓ |
| **Q3** | 1.5B-v6 from-scratch with 131K tokenizer · Indonesian LLM Leaderboard launch · Discord community active · Tech report draft |
| **Q4** | 7B from-scratch (pending TPU upgrade) · Full SFT + DPO pipeline · Community labeling for preference data · ACL/EMNLP IndoNLP submission |
| **2027 Q1** | 20B from-scratch (pending v5p / v6e-32 access) · Production inference endpoint · University partnerships |

> **Honest constraint**: We currently run on a single TPU v6e-8. 20B from-scratch needs 100×+ that compute. We're applying to TRC, HF GPU grants, and community sponsors. Help is welcome.

## 🤝 How to Contribute

Skill yang dibutuhkan (semua level diterima!):

| Role | What you'd do | Beginner friendly |
|---|---|:---:|
| **Data curation** | Verify SFT examples, review corpus samples, flag bias | ✅ |
| **Translator / labeler** | Translate eval prompts to ID/JV/SU, review answers | ✅ |
| **Documentation** | Tulis tutorial, perbaiki README, terjemahkan docs | ✅ |
| **ML engineer** | Fix training loop, optimize, add features | |
| **Researcher** | Architecture, scaling laws, evaluation methodology | |
| **DevOps** | CI/CD, Docker, deployment, infra | |
| **Community** | Manage Discord, write blog posts, social media | ✅ |

### Getting started (5 minutes)

1. **[Try the demo](https://huggingface.co/spaces/AksaraLLM/Kiel-Pro-0.5B-v3-chat-demo)** — chat with our 0.5B model, file feedback as a GitHub issue.
2. **Join [Discord](https://discord.gg/aksarallm)** — introduce yourself in `#general`.
3. **Read [`community/CONTRIBUTING.md`](https://github.com/AksaraLLM/community/blob/main/CONTRIBUTING.md)**.
4. **Browse [good first issues](https://github.com/issues?q=is%3Aissue+is%3Aopen+org%3AAksaraLLM+label%3A%22good+first+issue%22)** across repos.

### Sponsorship

Help fund GPU/TPU compute: [GPU Donations Guide](https://github.com/AksaraLLM/community/blob/main/GPU_DONATIONS.md). Even $5/month helps.

## 🙏 Acknowledgments

- [Qwen Team (Alibaba)](https://huggingface.co/Qwen) — base model lineage for current Qwen-derived variants
- [Google TPU Research Cloud](https://sites.research.google/trc/) — TPU access
- [Hugging Face](https://huggingface.co) — hosting + free Spaces tier
- [llama.cpp](https://github.com/ggerganov/llama.cpp) + [Ollama](https://ollama.com) — local inference
- [EasyDeL](https://github.com/erfanzar/EasyDeL) — JAX training framework
- All contributors and the broader Indonesian NLP community ([IndoNLP](https://indonlp.github.io), Sahabat-AI, SEA-LION, Cendol, Komodo) — for paving the way

## 📜 License

All AksaraLLM source code: **Apache License 2.0**.
Models: see individual model cards (most are Apache 2.0; some inherit base-model licenses).
