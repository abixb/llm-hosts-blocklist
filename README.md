# AI/LLM Blocklist – `hosts` Edition

Keep your workstation, home lab, or network squeaky‑clean of public Large‑Language‑Model (LLM) endpoints by black‑holing them at the operating‑system level.

> **Why?**
> • Privacy — prevent accidental data leakage to third‑party AI services.
> • Bandwidth — stop hefty inference calls from chewing through your quota.
> • Focus — remove chat‑bots and AI pop‑ups that hijack concentration.

---

## 📥 Quick Start

1. **Grab the file**

   ```bash
   curl -O https://github.com/abixb/llm-hosts-blocklist/edit/main/hosts
   ```
2. **Backup** your existing hosts file:

   ```bash
   sudo cp /etc/hosts /etc/hosts.bak
   ```
3. **Append** the blocklist (or replace the file if you prefer):

   ```bash
   sudo cat hosts >> /etc/hosts
   ```
4. **Flush DNS** (pick your OS):

   * macOS: `sudo dscacheutil -flushcache && sudo killall -HUP mDNSResponder`
   * Linux: `sudo systemd-resolve --flush-caches`
   * Windows: `ipconfig /flushdns`
5. **Verify**: `ping api.openai.com` ➜ should route to `0.0.0.0`.

> **Heads‑up:** The `hosts` file does **not** support wildcards.  Regional or tenant‑specific sub‑domains (e.g. `myco.openai.azure.com`) may still resolve until you list them explicitly.

---

## 🗂 What’s Inside?

| Provider               | Sample Domains Blocked                                              |
| ---------------------- | ------------------------------------------------------------------- |
| OpenAI                 | `api.openai.com`, `chat.openai.com`, `labs.openai.com`              |
| Anthropic              | `api.anthropic.com`, `claude.ai`                                    |
| Google Gemini / PaLM 2 | `generativelanguage.googleapis.com`, `gemini.google.com`            |
| Amazon Bedrock         | `bedrock.amazonaws.com`                                             |
| Cohere                 | `api.cohere.ai`                                                     |
| …and more              | Perplexity, Hugging Face, Replicate, Meta Llama, Stability AI, etc. |

Open the [`hosts`](./hosts) file to see the full list, grouped and commented for clarity.

---

## 🔄 Keeping It Fresh

This list is **community‑driven**.  New domains appear whenever vendors spin up fresh regions, versions, or proxy layers.  Please:

* **Open an Issue** for false‑positives or missed endpoints.
* **Submit a PR** (one provider per commit is ideal) adding the new entries, following the comment style already in the file.

A scheduled GitHub Action runs weekly to bump the *Last updated* date so you can keep track at a glance.

---

## 🛠 Automation Ideas

* **CLI install script** – Detect OS and patch hosts safely.
* **Pi‑hole / AdGuard export** – Convert to Gravity list format for network‑wide blocking.
* **DNS firewall** – Publish as a blocklist on NextDNS or Cloudflare Gateway.

Feel free to fork the repo and wire up these niceties! 

---

## ❗ Limitations & Disclaimer

* This repo targets **public consumer‑grade LLM endpoints**.  Self‑hosted or on‑prem models aren’t (and can’t be) blocked here.
* Enterprise tenants may use vanity sub‑domains.  Blocking those could break internal workflows — tread carefully.
* Use at your own risk. I'm not liable for downtime, lost productivity, or broken CI pipelines.

---

## 📜 License

[MIT](./LICENSE)

---

### 🙏 Acknowledgements

Inspired by the excellent privacy‑focused blocklists from [StevenBlack/hosts](https://github.com/StevenBlack/hosts) and contributions from developers and sysadmins around the globe.

> *“The price of freedom is eternal vigilance.”* – Thomas Jefferson (…and probably every network engineer, ever)

-- Balaji Abishek a.k.a Abi
