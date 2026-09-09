# 🎨 EasyComfyUI — ComfyUI on Google Colab (No Coding Needed)

A simple, ready-to-run Google Colab notebook for running **ComfyUI**
(Stable Diffusion / FLUX image generation) on a free Colab GPU — no coding
experience required. Just click ▶️ on each cell in order.

---

## 🖼️ Example Edits (Before → After)

A quick look at the kind of targeted, single-element edits this pipeline can pull off — everything else in the photo stays untouched.

**Original:**

<img src="img/og1.jpg" width="400">

**Edits:**

<table>
  <tr>
    <td align="center"><b>Removed Eyeglasses</b><br><img src="img/removeeyeglass.png" width="400"></td>
    <td align="center"><b>Changed Hairstyle</b><br><img src="img/changehairstyle.png" width="400"></td>
  </tr>
  <tr>
    <td align="center"><b>Replaced Shirt</b><br><img src="img/replaceshirt.png" width="400"></td>
    <td align="center"><b>Changed Background</b><br><img src="img/changebg.png" width="400"></td>
  </tr>
</table>

---

## 🛒 Get This Notebook

👉 **[Purchase EasyComfyUI here](https://buymeacoffee.com/fawzan/e/570955)**

---

## ☕ Thank You for Your Purchase!

Thanks for buying this notebook — your support helps keep it maintained
and updated. If you'd like to support future updates even further:

<a href="https://www.buymeacoffee.com/fawzan" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me a Coffee" style="height: 60px !important;width: 217px !important;" ></a>

---

## 📋 What You Need

- A Google account (for Google Colab and Google Drive)
- A free Google Colab session with a GPU (Colab assigns this automatically)
- That's it — everything else is handled by the notebook

---

## ⚠️ Good to Know: Free Colab Limits

This notebook runs great on Google Colab's **free tier**, but free Colab
comes with some limits that are outside this notebook's control:

- **GPU availability isn't guaranteed.** Google allocates free GPUs based
  on demand — during busy periods you may be given a CPU-only session, or
  asked to wait. If that happens, just try again later.
- **Sessions have a maximum lifetime** (roughly 12 hours) and will
  disconnect once reached, no matter what. The "Keep Colab Awake" cell
  only prevents *idle* disconnects — it can't extend this hard limit.
- **Idle disconnects still depend on the browser tab staying open.**
  Closing the tab, or your computer sleeping, will end the session even
  with keep-alive running.
- Heavy free-tier usage over time may lead to Google temporarily limiting
  your GPU access for a while. This resets on its own after some time.

None of this is a bug in the notebook — it's simply how Google's free tier
works. If you need longer, uninterrupted sessions, consider Colab Pro.

---

## 🚀 How to Use — Step by Step

### Step 1: Setup
Click ▶️ on the **Step 1: Setup** cell. It will:
- Ask you to connect your Google Drive — click **"Connect to Google Drive"**
  and allow access when prompted.
- Download and install ComfyUI, plus all required components.
- Restore any add-ons or saved workflows from a previous session (if any).

There's a **`check_for_updates`** checkbox above the cell — leave it
**unchecked** for a faster setup (the default), or **check it** if you want
Step 1 to also pull the latest updates for ComfyUI itself and
ComfyUI-Manager before continuing.

Wait for the message:
```
✅ Setup complete! Continue to Step 2 (download models) or Step 3 (launch).
```

> **Tip:** If you see a few warning lines during setup, that's usually fine —
> only worry if the cell stops with a red error and no ✅ at the end.

### Step 1b: Keep Colab Awake (Optional but recommended)
Run this cell once after Step 1 if you're planning a long session. It plays
a silent audio loop and sends periodic activity signals to help prevent
Colab from disconnecting an idle tab. Leave the browser tab open in the
background while you work.

### Step 2: Download Models
Paste direct download links into the boxes for whichever model types you
need (checkpoints, UNET/diffusion models, VAE, CLIP, LoRAs, ControlNet,
upscale models, embeddings, CLIP Vision). You can also paste GitHub links
for custom nodes you want installed.

#### ✅ Recommended: FLUX.2 [klein] 9B (works well on the free Colab GPU)

Paste these into the matching Step 2 boxes to get started with a proven,
tested setup:

| Box | Link |
|---|---|
| **UNET / diffusion model** | `https://huggingface.co/black-forest-labs/FLUX.2-klein-9b-fp8/resolve/main/flux-2-klein-9b-fp8.safetensors` |
| **CLIP / text encoder** | `https://huggingface.co/Comfy-Org/vae-text-encorder-for-flux-klein-9b/resolve/main/split_files/text_encoders/qwen_3_8b_fp8mixed.safetensors` |
| **VAE** | `https://huggingface.co/Comfy-Org/flux2-dev/resolve/main/split_files/vae/flux2-vae.safetensors` |

This combination (diffusion model + text encoder + VAE loaded one at a
time via ComfyUI's split loaders) fits comfortably within a free-tier T4
GPU's ~15GB VRAM, even though the model's own official spec sheet quotes
~29GB — that figure assumes loading everything at once in full precision,
which isn't how ComfyUI runs it here.

#### 🧩 Can I use other models?

**Yes.** You are not limited to the models listed above. This notebook
works with **any model that is compatible with ComfyUI** — Stable
Diffusion 1.5/XL checkpoints, other FLUX variants, custom fine-tunes,
LoRAs, ControlNets, and community models from sites like Hugging Face or
Civitai. Just paste the model's direct `.safetensors` (or similar) file
link into the matching box in Step 2.

The only real limit is your **Colab GPU's VRAM**:
- Free-tier Colab typically gives a **T4 GPU (~15GB VRAM)**.
- A model (or the largest single component you load at once) generally
  needs to be smaller than that to run without errors.
- If a model is too large, ComfyUI may fail to load it, run very slowly,
  or crash with an out-of-memory error — in that case, look for a smaller
  or quantized (FP8/GGUF) version of the same model instead.
- If you have a paid Colab plan with a bigger GPU (A100, etc.), you can
  use much larger models too — just select **"High VRAM (A100 only)"** in
  Step 3.

- Leave any box empty to skip it.
- **You can put multiple links in one box** — separate them with a new line
  **or a comma (`,`)**. For example, in the LoRAs box:
  ```
  https://huggingface.co/example/lora-one.safetensors,https://huggingface.co/example/lora-two.safetensors
  ```
  All links in that box will be downloaded in one go.
- Already-downloaded files are automatically skipped on re-runs.
- If a model requires a Hugging Face token, either paste it into the token
  box, or (recommended) save it once as a Colab Secret named `HF_TOKEN`
  (click the 🔑 key icon in the left sidebar) so you never have to paste it
  again.

### Step 2b: Download LoRAs from Civitai (Optional)
Paste one or more Civitai LoRA download links into the box, separated by
new lines or commas (same as the other download boxes in Step 2). Leave
it empty to skip this cell entirely.

**Set up your API key first (recommended, more secure than pasting it):**
1. Go to civitai.com → Account Settings → API Keys, and generate one.
2. In Colab, click the 🔑 key icon in the left sidebar.
3. Add a new secret named exactly `CIVITAI_TOKEN`, paste your key as the
   value, and turn on "Notebook access" for it.

You can also paste the key directly into the box above the cell instead,
but the Secret method is safer — it's never saved inside the notebook
file itself, so it stays private even if you share the notebook.

Filenames are picked up automatically from Civitai, and already
downloaded files are skipped automatically on re-runs.

### Step 3: Launch ComfyUI
Choose a memory profile:
- **Low VRAM** — safest default, works well on the free-tier GPU.
- **High VRAM (A100 only)** — only use this if you have a paid Colab plan
  with an A100 GPU.

Click ▶️ and wait. After ComfyUI starts, you'll see **two links** printed:

```
✅ Cloudflare link:   https://xxxxx.trycloudflare.com
✅ Localtunnel link:  https://xxxxx.loca.lt
```

Click the **Cloudflare link** first. If it works, you're done — enjoy!

### Step 4: Save Your Work (Optional, but do this before closing)
Before you close the Colab tab, run the **Step 4: Save** cell. This backs
up your installed add-ons and saved workflows to your Google Drive, so
they're automatically restored the next time you run Step 1. If you skip
this, anything you installed or built this session will be lost.

---

## 🧩 Troubleshooting: A Custom Node Fails to Load

If you see an error in the Step 3 logs that looks like this:

```
FileNotFoundError: [Errno 2] No such file or directory: '.../custom_nodes/<some-node-name>/__init__.py'
```

This means that add-on's backup on your Google Drive is incomplete (a
file is missing), often because a previous session's Step 4 backup was
interrupted partway through (for example, if Colab disconnected while it
was saving). Fix it like this:

1. **Remove the broken copy in both places** — run a new cell with:
   ```python
   import shutil, os
   node_name = "PUT_THE_BROKEN_NODE_NAME_HERE"
   shutil.rmtree(f"/content/ComfyUI/custom_nodes/{node_name}", ignore_errors=True)
   shutil.rmtree(f"{DRIVE_DIR}/saved_custom_nodes/{node_name}", ignore_errors=True)
   ```
   (Replace `PUT_THE_BROKEN_NODE_NAME_HERE` with the folder name shown in
   the error message.)
2. **Reinstall it fresh** — paste that add-on's GitHub link into the
   "custom node repo links" box in Step 2 and run it again.
3. **Re-run Step 3**, confirm the error is gone, then **run Step 4** to
   save a complete, working copy back to Drive this time.

---

## 🌐 Troubleshooting: Cloudflare Link Not Opening

Sometimes the Cloudflare link shows a browser error like:

```
This site can't be reached
DNS_PROBE_FINISHED_NXDOMAIN
```

This is a known quirk of Cloudflare's free tunnel service, not a problem
with the notebook itself. Try these steps **in order**:

**1. The drag-and-drop retry trick**
1. Open a **new browser tab**.
2. Go back to the Colab output and **select the Cloudflare link text**,
   then **drag it into the new tab's address bar** (instead of clicking it
   directly).
3. It will likely show the same DNS error the first time — that's expected.
4. Click once inside the **address bar** to select/highlight the link text
   that's already there.
5. Press **Enter**.
6. This second attempt often succeeds, even though the first one failed.

**2. Wait and retry**
If step 1 doesn't work, wait about 30–60 seconds (tunnel links sometimes
take a moment to fully register) and try opening the link again.

**3. Restart and re-run everything**
If it's still not working:
1. In Colab, go to **Runtime → Restart session**.
2. Re-run **all cells from the top**, in order (Step 1 → Step 2, if needed
   → Step 3).
3. Try the new Cloudflare link that gets printed.

**4. Use the Localtunnel link instead**
If the Cloudflare link still won't open after trying all of the above, use
the **Localtunnel link** printed alongside it instead:
- Open the Localtunnel link.
- It will show a **"Tunnel Password"** page first — this is normal.
- Click the link/button shown on that page (it auto-fills the required
  value) to continue through to ComfyUI.

> If **neither** link works at all, double-check that the Step 3 cell is
> still actively running (scroll up — you should see live logs streaming).
> If the cell stopped, restart it and wait for new links to be printed.

---

## 📚 Prompting Tips for FLUX Models

Black Forest Labs (the creators of FLUX) publish an official prompting
guide covering prompt structure, lighting, typography, model selection,
and more:

👉 [black-forest-labs/skills](https://github.com/black-forest-labs/skills)

A few quick rules from their guide worth remembering:
- FLUX does **not** support negative prompts — describe what you *want*
  instead of what you don't want.
- Natural, descriptive sentences work better than short keyword lists.
- Mentioning lighting explicitly (e.g. "soft golden-hour lighting") has one
  of the biggest impacts on output quality.
- To render text in an image, put it in quotes, e.g. `a sign that reads "OPEN"`.

---

## ❓ Frequently Asked Questions

**Q: My generated images — where do they go?**
A: Straight to your Google Drive, in a folder called `EasyComfyUI/output`.
They are not deleted when your Colab session ends.

**Q: I closed the tab without running Step 4 — did I lose my custom nodes?**
A: Yes, anything installed that session that wasn't backed up via Step 4
will need to be reinstalled next time. Models you downloaded in Step 2 are
safe either way (they live in Drive-independent local storage that's
re-downloaded, or already skipped if present).

**Q: Can I use this on Colab's free tier?**
A: Yes — the default "Low VRAM" profile is designed for the free-tier T4
GPU.

**Q: Something else broke — what do I do?**
A: Scroll up through the Step 3 logs for the first red `[ERROR]` or
`Traceback` line — that usually points to the real cause. Feel free to
reach out for support.

---

## 📄 License

This notebook is provided for personal and commercial use as licensed to
you at the time of purchase/download. Please do not redistribute the
notebook file itself without permission.

---

Made with ❤️ — thank you for your purchase! If you'd like to support future updates, consider [buying a coffee](https://www.buymeacoffee.com/fawzan) ☕