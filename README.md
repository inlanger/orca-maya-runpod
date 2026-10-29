![ORCA / MAYA — DeepSeek V4.1 Flash Mix-256G, abliterated model](https://raw.githubusercontent.com/inlanger/orca-maya-runpod/refs/heads/codex/public/assets/orca-maya-banner.png)

# DeepSeek V4.1 Flash 1017 — Orca Mix-256G Abliterated on Maya

[![Deploy on Runpod](https://img.shields.io/badge/Deploy_on_Runpod-673AB7?style=for-the-badge)](https://console.runpod.io/hub/template/jac6t7pq8l)

Run **OrcaRouter's abliterated DeepSeek-V4.1-Flash-1017 GGUF** with the
**Project Maya** inference engine on **2× RTX PRO 6000 Blackwell 96 GB**.
Fast generation, a **1M context window** and an authenticated OpenAI-compatible
API, with **automatic deletion after 30 idle minutes**.

## Who this is for

A large **abliterated / uncensored DeepSeek model** for security researchers,
application security engineers and developers who want fewer refusals and control
over their inference setup.

- **Security reviews:** audit code and configurations, investigate vulnerabilities,
  review suspicious scripts and analyze findings or logs.
- **Authorized pentesting and CTFs:** reason through attack paths, develop lab
  reproductions and explore security tools and techniques.
- **AI red-teaming:** study refusal behavior, adversarial prompts and agent robustness.
- **Coding and document analysis:** debug, draft tests and work with large codebases,
  documentation and log collections.
- **Creative writing and RP:** fiction, roleplay and open-ended conversation with
  an abliterated model's less restrictive response style.

Connect your existing API client or chat frontend. The template starts the model
service on your own Runpod instance.

## What to expect

- **~125–136 tokens/s on ordinary requests** in our two-GPU tests, including reasoning.
- **1M context window** for large codebases, documents and conversations.
- **Around 7 minutes to model-ready** in our measured cold start using HF/Xet.
- **Automatic deletion after 30 idle minutes**, including the temporary Pod disk.

Speed and startup time depend on the prompt, host and network.

## Before deploying

1. Accept the model's access conditions using your own Hugging Face account:
   [OrcaRouter DeepSeek V4.1 Flash 1017 Abliterated GGUF](https://huggingface.co/orcarouter/DeepSeek-V4.1-Flash-1017-abliterated-GGUF).
2. In the deployment screen, use **Edit Template → Environment Variables → Add
   Environment Variable** to add both required variables below. Select your own
   Runpod secrets through the key selector. No credentials are supplied:

   | Variable | Value to provide |
   | --- | --- |
   | `HF_TOKEN` | Your Hugging Face read token with access to the Orca repository |
   | `API_KEY` | Your own strong, unique key for accessing the model API |

3. Select **two RTX PRO 6000 Blackwell Server Edition GPUs**, **at least 320 GB
   system RAM**, **32 vCPUs** and a host with **local NVMe**. Keep the template's
   **600 GB temporary container disk** and CUDA 13.0-or-newer host requirement.
   The template does not select the GPU count for you.
4. Deploy and watch the Pod logs. Wait for Maya's `ready:` line before sending
   requests. The first start downloads approximately **406 GB**.

This recipe uses temporary local storage. No persistent or network volume is
required. Runpod supplies the Pod-scoped `RUNPOD_API_KEY` and `RUNPOD_POD_ID` used
to delete this Pod; do not put your account-wide Runpod key in the template.

## Connect

OpenAI-compatible base URL:

```text
https://<POD_ID>-8080.proxy.runpod.net/v1
```

Set your client's API key to the `API_KEY` you supplied. All public HTTP routes,
including health, model lists and metrics, require authentication. Send
`Authorization: Bearer <API_KEY>` or `x-api-key: <API_KEY>`. Streaming is enabled.

The API model name is `deepseek-v4.1-flash-abliterated`. Defaults are
temperature **1.0**, top-p **1.0**, high reasoning effort and no server thinking
budget. The full **1M context window is configured and available**.

## Idle deletion and cost

After **30 minutes without queued requests or active generation**, the watchdog
**deletes the Pod and its temporary disk**. Health checks and model-list requests
do not keep it alive. Save anything you need before the idle deadline.

Startup and the idle grace period are billable. Any network volumes you attach
have a separate lifecycle; this template requires none. Check the Pod's status
if the service becomes unhealthy, as monitoring or network failures can delay
automatic cleanup.

## What starts automatically

The **latest Maya `main`** is fetched on every new Pod. The official HF CLI
fetches the model through **HF/Xet**, then Maya verifies and prepares the files.
The tested two-GPU profile uses **DSpark speculative decoding** and Maya's native
GPU/RAM placement. Calibration is skipped at startup.

All public API routes require your key. SSH and Jupyter startup are disabled.
The recipe uses temporary storage, with no persistent disk required.

## Credits

- Inference engine: [Project Maya](https://github.com/mw00/project-maya).
- Abliterated model: [OrcaRouter](https://huggingface.co/orcarouter/DeepSeek-V4.1-Flash-1017-abliterated-GGUF).
- Original model: [DeepSeek](https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash-1017).
- Engram and DSpark artifacts: [Peasant Smith's Maya GGUF repository](https://huggingface.co/peasantsmith/DeepSeek-V4.1-Flash-1017-Maya-GGUF).

This is a community deployment recipe. Model weights are downloaded from their
publishers at startup; their respective access conditions and licenses apply.
