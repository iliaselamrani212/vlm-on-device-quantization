## 1. Fiche d'identité

**Papier** : *SmolVLM: Redefining small and efficient multimodal models*, Marafioti et al., Hugging Face & Stanford, arXiv:2504.05299 (7 avril 2025)

| Modèle | Params | Encodeur vision | LLM | Licence | Contexte | Date de sortie |
|---|---|---|---|---|---|---|
| SmolVLM2-2.2B | 2 246 784 880 (~2,2B) | SigLIP-SO400M (~400M, patch 14, 384 px) | SmolLM2-1.7B | Apache 2.0 | 16k¹ | 20 février 2025 |
| SmolVLM2-500M | 507 482 304 (~500M) | SigLIP-B/16 (93M, patch 16, 512 px) | SmolLM2-360M | Apache 2.0 | 8k | 20 février 2025 |
| SmolVLM2-256M | 256 484 928 (~256M) | SigLIP-B/16 (93M, patch 16, 512 px) | SmolLM2-135M | Apache 2.0 | 8k | 20 février 2025 |
| LFM2.5-VL-450M | 448 718 848 (~0,45B) | SigLIP2 NaFlex shape-optimized (86M) | LFM2.5-350M | LFM Open License v1.0 | 32 768 tokens | 8 avril 2026 |
| LFM2.5-VL-1.6B | 1 596 625 904 (~1,6B) | SigLIP2 NaFlex shape-optimized (400M) | LFM2.5-1.2B-Base | LFM Open License v1.0 | 32 768 tokens | Janvier 2026 |
| Gemma 3 4B | 4 300 079 472 (~4,3B) | SigLIP 400M (417M), gelé | Gemma 3 (decoder-only) | Gemma Terms of Use | 128K | 12 mars 2025 |
| Gemma 3n E2B | 5 439 438 272 (~5,4B bruts, ~2B effectifs) | MobileNet-V5-300M (CNN) | Gemma 3n (MatFormer + PLE) | Gemma Terms of Use | 32K | 26 juin 2025 (preview : 20 mai 2025) |

¹ Le papier indique 16k tokens pour le 2.2B, mais le `config.json` du modèle donne `max_position_embeddings: 8192`. À clarifier avant de citer.

## 2. Benchmarks (annoncés)

| Modèle | MMMU | OCRBench (v1) | DocVQA | MathVista | Autres |
|---|---|---|---|---|---|
| SmolVLM2-2.2B | 42,0 % | 72,9 % | 80,0 % | 51,5 % | AI2D 70,0 · ChartQA 68,7 · TextVQA 73,0 · ScienceQA 89,6 · MMStar 46,0 · Video-MME 52,1 · MLVU 55,2 · MVBench 46,3 · WorldSense 36,2 · TempCompass 53,7 · **Moyenne 59,8** |
| SmolVLM2-500M | 33,7 % | 61,0 % | 70,5 % | 40,1 % | AI2D 59,2 · ChartQA 62,8 · TextVQA 60,2 · ScienceQA 80,0 · MMStar 38,3 · Video-MME 42,2 · MLVU 47,3 · MVBench 39,7 · WorldSense 30,6 · TempCompass 49,0 · **Moyenne 51,0** |
| SmolVLM2-256M | 29,0 % | 52,6 % | 58,3 % | 35,9 % | AI2D 46,4 · ChartQA 55,6 · TextVQA 50,2 · ScienceQA 73,8 · MMStar 34,6 · Video-MME 33,7 · MLVU 40,6 · MVBench 32,7 · WorldSense 29,7 · TempCompass 43,1 · **Moyenne 44,0** |
| LFM2.5-VL-450M | 32,67 % (val) | 684 / 1000* | Non publié | Non publié | MMStar 43,00 · RealWorldQA 58,43 · InfoVQA 43,02 · MM-IFEval 45,00 · BLINK 43,92 · CountBench 73,31 · RefCOCO-M 81,28 |
| LFM2.5-VL-1.6B | 40,56 % (val) | Non publié** | Non publié | Non publié | MMStar 50,67 · RealWorldQA 64,84 · InfoVQA 62,71 · MM-IFEval 52,29 · BLINK 48,82 · OCRBench v2 41,44 · MMMB 76,96 |
| Gemma 3 4B (PT)*** | 39,2 % | Non publié | 72,8 % (val) | Non publié | InfoVQA 44,1 · TextVQA 58,9 · RealWorldQA 45,5 · AI2D 63,2 · ChartQA 63,6 · BLINK 38,0 · CountBenchQA 26,1 |
| Gemma 3n E2B | Non publié | Non publié | Non publié | Non publié | Aucun benchmark vision publié (le model card ne donne que des benchmarks texte, ex. MMLU 60,1 en IT) |

\* Version non précisée. Score sur 1000, donc format v1. Correspond à 68,4 % sur l'échelle des SmolVLM2.
\*\* Seul OCRBench **v2** est publié (41,44, sur 100). Ne pas le comparer à du v1.
\*\*\* Scores du modèle **pré-entraîné (PT)**, pas de la version instruct.

⚠️ Ce sont des scores **auto-déclarés**, chacun avec son propre protocole. Pour une comparaison équitable, il faut tout ré-évaluer avec le même outil (VLMEvalKit).

## 3. Mémoire et taille

| Modèle | Mémoire annoncée (source officielle) | Poids BF16 (calculé) | Poids 8 bits (calculé) | Poids 4 bits (calculé) |
|---|---|---|---|---|
| SmolVLM2-2.2B | Papier : 4,9 Go (batch 1) | 4,49 Go (4,18 Gio) | 2,25 Go (2,09 Gio) | 1,12 Go (≈ 1,26 Go en Q4_0†) |
| SmolVLM2-500M | Papier : 1,2 Go (batch 1) | 1,01 Go (0,95 Gio) | 0,51 Go (0,47 Gio) | 0,25 Go (≈ 0,29 Go en Q4_0†) |
| SmolVLM2-256M | Papier : 0,8 Go (batch 1) | 0,51 Go (0,48 Gio) | 0,26 Go (0,24 Gio) | 0,13 Go (≈ 0,14 Go en Q4_0†) |
| LFM2.5-VL-450M | Non publiée | 0,90 Go (0,84 Gio) | 0,45 Go (0,42 Gio) | 0,22 Go (0,21 Gio) |
| LFM2.5-VL-1.6B | Non publiée | 3,19 Go (2,97 Gio) | 1,60 Go (1,49 Gio) | 0,80 Go (0,74 Gio) |
| Gemma 3 4B | Papier, Table 3 : 8,0 Go en bf16 · 2,6 Go en int4 · 4,4 Go en SFP8. Avec KV cache à 32K : 12,7 / 7,3 / 9,1 Go | 8,60 Go (8,01 Gio) | 4,30 Go (4,00 Gio) | 2,15 Go (2,00 Gio) |
| Gemma 3n E2B | Blog : « à partir de 2 Go » (grâce aux PLE déchargés) | 10,88 Go (10,13 Gio) | 5,44 Go (5,07 Gio) | 2,72 Go (2,53 Gio) |

**Méthode de calcul :** paramètres (safetensors) × octets par poids (BF16 = 2, 8 bits = 1, 4 bits = 0,5). 1 Go = 10⁹ octets, 1 Gio = 2³⁰ octets.
† Estimation en Q4_0, à 4,5 bits par poids en comptant les scales.

Le papier SmolVLM appelle ces valeurs « RAM Usage » dans le tableau, mais parle de mémoire GPU dans le texte. Le calcul ne compte que les poids : pas de KV cache ni d'activations.

## 4. Déploiement sur iPhone

| Modèle | GGUF dispo ? (lien) | MLX dispo ? (lien) | Pris en charge par llama.cpp (vision) ? |
|---|---|---|---|
| SmolVLM2-2.2B | [ggml-org/SmolVLM2-2.2B-Instruct-GGUF](https://huggingface.co/ggml-org/SmolVLM2-2.2B-Instruct-GGUF) (Q4_K_M, Q8_0, F16 + mmproj Q8_0/F16) | [mlx-community/SmolVLM2-2.2B-Instruct-mlx](https://huggingface.co/mlx-community/SmolVLM2-2.2B-Instruct-mlx) · 4 bits communautaire : [smdesai/SmolVLM2-2.2B-Instruct-4bit](https://huggingface.co/smdesai/SmolVLM2-2.2B-Instruct-4bit) (≈ 1,46 Go) | Oui, via libmtmd (`llama-mtmd-cli`, `llama-server`) |
| SmolVLM2-500M | [ggml-org/SmolVLM2-500M-Video-Instruct-GGUF](https://huggingface.co/ggml-org/SmolVLM2-500M-Video-Instruct-GGUF) (Q8_0, F16 + mmproj, **pas de Q4**) | [mlx-community/SmolVLM2-500M-Video-Instruct-mlx](https://huggingface.co/mlx-community/SmolVLM2-500M-Video-Instruct-mlx) | Oui, via libmtmd |
| SmolVLM2-256M | [ggml-org/SmolVLM2-256M-Video-Instruct-GGUF](https://huggingface.co/ggml-org/SmolVLM2-256M-Video-Instruct-GGUF) (Q4_K_M, Q8_0, BF16, F16 + mmproj) | [mlx-community/SmolVLM2-256M-Video-Instruct-mlx](https://huggingface.co/mlx-community/SmolVLM2-256M-Video-Instruct-mlx) | Oui, via libmtmd |
| LFM2.5-VL-450M | Officiel : [LiquidAI/LFM2.5-VL-450M-GGUF](https://huggingface.co/LiquidAI/LFM2.5-VL-450M-GGUF) (Q4_0 → F32 + 4 mmproj) | Officiel (bf16, 8/6/5/4 bits) : [LiquidAI/LFM2.5-VL-450M-MLX-4bit](https://huggingface.co/LiquidAI/LFM2.5-VL-450M-MLX-4bit), [MLX-bf16](https://huggingface.co/LiquidAI/LFM2.5-VL-450M-MLX-bf16) | Oui (mmproj fourni, `llama-cli` + `/image`) |
| LFM2.5-VL-1.6B | Officiel : [LiquidAI/LFM2.5-VL-1.6B-GGUF](https://huggingface.co/LiquidAI/LFM2.5-VL-1.6B-GGUF) (Q4_0 → F16 + 3 mmproj) | ⚠️ Communautaire seulement : [mlx-community/LFM2.5-VL-1.6B-4bit](https://huggingface.co/mlx-community/LFM2.5-VL-1.6B-4bit) (aussi 5/6/8 bits et bf16) | Oui (mmproj fourni, `llama-cli` + `/image`) |
| Gemma 3 4B | Officiel QAT : [google/gemma-3-4b-it-qat-q4_0-gguf](https://huggingface.co/google/gemma-3-4b-it-qat-q4_0-gguf) · [ggml-org/gemma-3-4b-it-GGUF](https://huggingface.co/ggml-org/gemma-3-4b-it-GGUF) (Q4_K_M, Q8_0, F16 + mmproj) | ⚠️ Communautaire : [mlx-community/gemma-3-4b-it-4bit](https://huggingface.co/mlx-community/gemma-3-4b-it-4bit) · version QAT : [mlx-community/gemma-3-4b-it-qat-4bit](https://huggingface.co/mlx-community/gemma-3-4b-it-qat-4bit) | Oui (`llama-mtmd-cli`) |
| Gemma 3n E2B | ⚠️ [ggml-org/gemma-3n-E2B-it-GGUF](https://huggingface.co/ggml-org/gemma-3n-E2B-it-GGUF) (Q8_0, F16, **sans mmproj**) · [unsloth/gemma-3n-E2B-it-GGUF](https://huggingface.co/unsloth/gemma-3n-E2B-it-GGUF) | ⚠️ Communautaire : [lmstudio-community/gemma-3n-E2B-it-MLX-4bit](https://huggingface.co/lmstudio-community/gemma-3n-E2B-it-MLX-4bit) | ⚠️ Expérimental : vision MobileNetV5 ajoutée en build b7689 (PR #18256). Le GGUF ggml-org est texte seul. Format mobile officiel : [google/gemma-3n-E2B-it-litert-lm](https://huggingface.co/google/gemma-3n-E2B-it-litert-lm) |

**Notes :**
- Le model card GGUF de LFM2.5-VL-1.6B contient une coquille : son exemple pointe vers `LiquidAI/LFM2.5-VL-3B-GGUF`.
- Certains dépôts mlx-community « gemma-3n-E2B » déclarent `google/gemma-3n-E4B` comme modèle de base. Vérifie la lignée avant de les utiliser.
- Autres formats officiels : ONNX (LiquidAI/LFM2.5-VL-450M-ONNX, LiquidAI/LFM2.5-VL-1.6B-ONNX) et LiteRT-LM (Gemma 3n).

## 5. Sources (vérifiées le 22/11/2026)

**SmolVLM2**
- Papier : https://arxiv.org/abs/2504.05299 (Table 1 pour les benchmarks et la RAM, texte pour les encodeurs, LLM et contexte)
- Blog de lancement (20 février 2025) : https://huggingface.co/blog/smolvlm2
- Paramètres et licence (API HF) : https://huggingface.co/api/models/HuggingFaceTB/SmolVLM2-2.2B-Instruct · https://huggingface.co/api/models/HuggingFaceTB/SmolVLM2-500M-Video-Instruct · https://huggingface.co/api/models/HuggingFaceTB/SmolVLM2-256M-Video-Instruct
- Résolution, patch et contexte (config) : https://huggingface.co/HuggingFaceTB/SmolVLM2-2.2B-Instruct/blob/main/config.json · https://huggingface.co/HuggingFaceTB/SmolVLM2-256M-Video-Instruct/blob/main/config.json

**LFM2.5-VL**
- Model cards : https://huggingface.co/LiquidAI/LFM2.5-VL-450M · https://huggingface.co/LiquidAI/LFM2.5-VL-1.6B
- Paramètres (API HF) : https://huggingface.co/api/models/LiquidAI/LFM2.5-VL-450M · https://huggingface.co/api/models/LiquidAI/LFM2.5-VL-1.6B
- Blog 450M (date, benchmarks) : https://www.liquid.ai/blog/lfm2-5-vl-450m
- Date du 1.6B : https://artificialanalysis.ai/models/lfm2-5-vl-1-6b
- LFM2 Technical Report : https://arxiv.org/abs/2511.23404

**Gemma 3**
- Technical report (Tables 1 et 3) : https://arxiv.org/abs/2503.19786
- Model card (benchmarks PT) : https://huggingface.co/google/gemma-3-4b-it
- Paramètres (API HF) : https://huggingface.co/api/models/google/gemma-3-4b-it
- Blog de lancement : https://blog.google/technology/developers/gemma-3/

**Gemma 3n**
- Developer guide : https://developers.googleblog.com/en/introducing-gemma-3n-developer-guide/
- Model card : https://ai.google.dev/gemma/docs/gemma-3n/model_card
- Paramètres (API HF) : https://huggingface.co/api/models/google/gemma-3n-E2B-it
- MatFormer : https://arxiv.org/abs/2310.07707

**llama.cpp**
- Doc multimodal : https://github.com/ggml-org/llama.cpp/blob/master/docs/multimodal.md
- Release b7689 (vision Gemma 3n) : https://newreleases.io/project/github/ggml-org/llama.cpp/release/b7689