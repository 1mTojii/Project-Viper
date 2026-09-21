# Project-Viper
This is my first big project. I dual booted my laptop with windows and kali linux. The Kali is focused with 100% anonymity and security from outside attacks. The biggest project here is the local AI i am working on from this Kali, Project Viper. This Ai assistant is focused on pentesting and data management

Viper is in the Alpha - Beta at phase at the moment i am still in the process developing the tool. Its pretty trash at the moment check up on this project in a couple of months.

I Dual booted my laptop into Windows + Kali, hardened the Kali side LUKS encryption, VPN, the works, and built a locally-run, uncensored pentest LLM on top of it called **Viper**.

No refusal wall, no logging, no internet dependency, runs entirely on my own hardware. Built to learn, to have a tool that actually talks to me about offensive security without hedging, and eventually to feed it my own CTF/HTB notes and reference material so it gets smarter over time.

I'm a third-year Cybersecurity student, this is just a learning project, not a production tool, and definitely not weapons-grade anything. Treat it accordingly.

## What's actually in here

- **Viper**: a custom Ai agent built on the [WhiteRabbitNeo-7B](https://huggingface.co/WhiteRabbitNeo/WhiteRabbitNeo-7B-v1.5a) LLM, with a custom Modelfile. Personality tweaks, a fixed chat template, the base model's default template didn't set stop tokens properly and would ramble into fake conversations, that took way too long to debug, and a system prompt aimed at keeping answers direct instead of walking through an unnecessary reasoning framework for every message. 
- In progress RAG setup via [AnythingLLM](https://anythingllm.com) so Viper can reference my own notes, PTES/OWASP docs, and MITRE ATT&CK data, Half of wikipedia instead of just guessing.

## Why "uncensored"

WhiteRabbitNeo is purpose-built for offensive/defensive security work. It doesn't hit you with a refusal wall for legitimate pentest questions the way general-purpose assistants sometimes do. This matters for actually learning the material, not for doing anything shady. See the Responsible Use section below, I'm not trying to dodge that conversation.

## Tech stack

- **OS**: Kali Linux (dual boot, external SSD), Windows 11 (main daily driver, untouched)
- **LLM runtime**: [Ollama](https://ollama.com)
- **Base model**: WhiteRabbitNeo-7B-v1.5a
- **VPN**: ProtonVPN (CLI, WireGuard)
- **Planned**: AnythingLLM for RAG + web search agent skills
- **Planned**: Kill switch
## Setup

Rough version - full step-by-step is still getting cleaned up as I go:

```bash
# Install Ollama
curl -fsSL https://ollama.com/install.sh | sh

# Pull the base model
ollama pull captainkyd/whiterabbitneo7b

# Build Viper from the Modelfile in this repo
ollama create viper -f ./Modelfile

# Feed it data

# Make sure it does not go rouge like mine did and start nmaping the entire home wifi :)

# Run it
ollama run viper
```

The `Modelfile` in this repo has the full system prompt, chat template, and stop tokens. Copy it as-is or tweak the SYSTEM block to change the personality.

## AI disclosure

I used Claude to help me debug this, figuring why my first few Modelfiles kept breaking (turns out newlines matter and I fumbled that more times than I'd like to admit), and general "why is this thing hallucinating a fake toolkit that doesn't exist" troubleshooting. I understand what every piece here does and why, this isn't a copy-paste project, but I'm not going to pretend I one-shotted the Modelfile syntax on the first try either. Full transparency, no shame in it.

## Responsible use

This project is built on WhiteRabbitNeo, which ships under a permissive license **plus a Usage Restrictions Extension** no military use, no harming minors, no disinformation, no discrimination, no PII misuse, etc. Since this repo's Modelfile is a derivative of that model, those same restrictions apply here too. Full terms: see WhiteRabbitNeo's model card on Hugging Face.

Practically: this is a personal learning tool for CTFs, HTB boxes, and my own lab environment. Point it at systems you own or have explicit permission to test. Same rules as any pentest tool, nmap, Metasploit, whatever, legality is about what you point it at, not the tool itself.

## What's actually in here


## Status

Actively being built. Dual boot. Viper running and behaving (mostly). RAG/knowledge feeding and a lot more - in progress. Might eventually move the LLM work to my heavier pc once Im fed up with how slow this process is.

## Credits

- [WhiteRabbitNeo](https://huggingface.co/WhiteRabbitNeo) / Kindo.ai - base model
- [Ollama](https://ollama.com) - local LLM runtime
- [ProtonVPN](https://protonvpn.com) - VPN
- [AnythingLLM](https://anythingllm.com) - RAG layer (planned)
