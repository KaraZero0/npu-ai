🇬🇧 [Read in English](#-english) | 🇮🇹 [Leggi in Italiano](#-italiano)

---

# 🇬🇧 English

# Intel NPU Local AI Toolkit (`npu-ai` & `npu-upscale`)

Lightweight Linux CLI utilities for running **local LLMs and Super-Resolution models directly on Intel AI Boost NPU** via **OpenVINO** (with automatic fallback to Intel Arc iGPU/CPU), designed to keep CPU/RAM impact minimal on modern Intel Core Ultra laptops.

## ✨ Components

1. **`bin/npu-ai`**: Local terminal assistant powered by `openvino_genai` (`Qwen2.5-Coder-1.5B-Instruct` OpenVINO IR).
   - **Single-shot & piped mode**: explain logs (`journalctl -xe | npu-ai`) or ask quick questions.
   - **Command-only mode (`-c`)**: returns a single executable Zsh/Bash command.
   - **Persistent memory**: stores infrastructure notes (`context.md`) and learns facts interactively (`remember that ...`).
   - **Zsh `Ctrl+G` integration**: convert natural-language descriptions directly inside your terminal prompt into shell commands.
2. **`bin/npu-upscale`**: Tiled **Real-ESRGAN (`2x` / `4x`)** image upscaler accelerated on Intel NPU via OpenVINO.
   - Processes `256x256` tiles with `16px` overlap and 2D feather blending to avoid visible seams.
   - Preserves alpha channels and supports desktop notifications (`--notify` for file managers like KDE Dolphin).
3. **`bin/copilot-popup`**: Toggleable floating terminal launcher for KDE Wayland.

## 🛠️ Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# Optional: copy and customize your local system context (gitignored)
export NPU_AI_HOME="$PWD"
cp context.example.md context.md

# Place OpenVINO IR models in:
#   $NPU_AI_HOME/models/llm/Qwen2.5-Coder-1.5B-Instruct-npu-ov/
#   $NPU_AI_HOME/models/upscaler/models/real_esrgan_x4plus_anime_6B_fp32.xml
```

### Zsh Widget (`Ctrl+G`)

Add to your `~/.zshrc`:

```zsh
_npu_zsh_widget() {
  local query="$BUFFER"
  [[ -z "$query" ]] && return
  BUFFER="⚡ Generating command..."
  zle -R
  local cmd
  cmd=$(/path/to/npu-ai/bin/npu-ai -c "$query" 2>/dev/null)
  BUFFER="$cmd"
  CURSOR=$#BUFFER
}
zle -N _npu_zsh_widget
bindkey '^G' _npu_zsh_widget
```

---

# 🇮🇹 Italiano

# Intel NPU Local AI Toolkit (`npu-ai` & `npu-upscale`)

Suite leggera di utility CLI Linux per eseguire **modelli LLM e Super-Resolution localmente su Intel AI Boost NPU** tramite **OpenVINO** (con fallback automatico su iGPU Intel Arc/CPU), pensata per ridurre al minimo il carico su CPU e batteria nei notebook Intel Core Ultra.

## ✨ Componenti

1. **`bin/npu-ai`**: Assistente da terminale locale basato su `openvino_genai` (`Qwen2.5-Coder-1.5B-Instruct` OpenVINO IR).
   - **Modalità singola e pipe**: analizza log (`journalctl -xe | npu-ai`) o risponde a domande rapide.
   - **Modalità solo comando (`-c`)**: restituisce un comando Bash/Zsh eseguibile su una singola riga.
   - **Memoria persistente**: legge il contesto utente (`context.md`) e memorizza nuove note (`ricorda che ...`).
   - **Scorciatoia Zsh (`Ctrl+G`)**: trasforma una descrizione in linguaggio naturale direttamente nel prompt nel comando Linux corrispondente.
2. **`bin/npu-upscale`**: Upscaler **Real-ESRGAN (`2x` / `4x`)** accelerato su Intel NPU via OpenVINO.
   - Elaborazione a tasselli `256x256` con sovrapposizione di `16px` e maschere di fusione sfumate per eliminare le giunzioni.
   - Preserva il canale alfa (trasparenze PNG) e supporta notifiche desktop (`--notify` per Dolphin/KDE).
3. **`bin/copilot-popup`**: Launcher rapido a finestra per KDE Wayland.

## 🛠️ Configurazione

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

export NPU_AI_HOME="$PWD"
cp context.example.md context.md
```
