# Kling 2.6 Motion Control API (`kling-v2-6-motion-control`)

<!-- conv-kit:v1 -->

<p align="center">
  <img src="assets/badges/price.svg" alt="observed unit price"> <img src="assets/badges/billing.svg" alt="billing model"> <img src="assets/badges/compat.svg" alt="OpenAI-compatible endpoint">
</p>

<p align="center">
  <img src="assets/01-product-ad-ceramic-mug-thumb.jpg" width="820" alt="Sample video frame generated through APIMart">
</p>

> **from $0.0571 per second** on the APIMart route — ein einziger OpenAI-kompatibler Endpoint unter `https://api.apimart.ai/v1`, kein Monatsabo nötig. *(erfasst am 2026-10-12)*

**[API-Key erhalten](https://go.apimart.ai/k-ba9cc8)** · **[Live-Preise](https://go.apimart.ai/k-0d9c3b)** · **[Modellseite](https://go.apimart.ai/k-88c2d9)** · [⚡ Quickstart in 60 Sekunden](#quickstart)

**Warum Teams Kling 2.6 Motion Control (`kling-v2-6-motion-control`) über APIMart nutzen**

- **Ein Key, der gesamte Katalog.** Dieselbe Base-URL `https://api.apimart.ai/v1` und derselbe `Authorization`-Header erreichen Kling 2.6 Motion Control (`kling-v2-6-motion-control`) und über 300 weitere Bild-, Video- und Sprachmodelle — Sie wechseln das `model`-Feld, nicht Ihren Client.
- **$1 Minimum, Pay-as-you-go.** Kein Abo und kein Prepaid-Tarif, den Sie vorab dimensionieren müssen: ab $1 aufladen und in Calls verbrauchen.
- **Die Abrechnung kommt in der Antwort zurück.** Jede abgeschlossene Aufgabe meldet den berechneten Betrag (`cost` / `credits_cost`); eine als `failed` markierte Aufgabe wird erstattet.
- **Asynchron by Design.** Absenden, `task_id` entgegennehmen, `GET /v1/tasks/{id}` pollen — Batching und Retries sind gewöhnliche Queue-Arbeit, keine Sonderintegration.

<!-- /conv-kit:v1 -->



Kling V2.6 Motion Control on APIMart uses a reference image plus a reference video to transfer subject motion into generated clips. Use kling-v2-6-motion-control with std (720p) and pro (1080p) modes; output length follows the reference video and billing is per second. Add an optional prompt, set character orientation, and control sound or watermark settings. It brings Kling AI Motion Control to your own app through one API: use kling-v2-6-motion-control as the model.

## Model id and routes

| Route | `model` value | Billing | Notes |
| --- | --- | --- | --- |
| Text-to-video / image-to-video | `kling-v2-6-motion-control` | per generated second, by resolution | see the [model page](https://go.apimart.ai/k-88c2d9) for the exact tiers |

Endpoint: `POST https://api.apimart.ai/v1/videos/generations`, then poll `GET /v1/tasks/{task_id}`.

## Pricing

<!-- pricing:model:start -->
| Resolution | List price | Effective price |
| --- | --- | --- |
| default | 0.0714 | 0.05712 |


<!-- pricing:model:end -->

Prices are a snapshot; the [pricing page](https://go.apimart.ai/k-0d9c3b) and [`data/model.json`](data/model.json) are refreshed by CI, and a completed task reports the exact amount in its `cost` field.

## Request parameters

| Field | Type | Default | Notes |
| --- | --- | --- | --- |
| `model` | string | required | the model id shown in the route table above |
| `prompt` | string | required | the shot description; camera and subject motion belong here |
| `duration` | integer | route default | clip length in seconds — billing is per generated second |
| `resolution` | string | route default | 480P / 720P / 1080P or the route’s own tiers |
| `size` / `aspect_ratio` | string | `16:9` | output framing |
| `image_urls` | string[] | — | first frame, first + last frame, or style references, where supported |
| `seed` | integer | — | fix the seed to reproduce a take |

The table lists the fields accepted by the APIMart `videos/generations` endpoint. Check the [model page](https://go.apimart.ai/k-88c2d9) for anything this model adds on top.

## Quickstart

```bash
curl --request POST --url https://api.apimart.ai/v1/videos/generations \
  --header "Authorization: Bearer $APIMART_API_KEY" --header 'Content-Type: application/json' \
  -d '{"model":"kling-v2-6-motion-control","prompt":"A bamboo forest at sunrise, slow push-in","duration":5,"resolution":"720P","size":"16:9"}'
```

```python
import os, time, requests

BASE = "https://api.apimart.ai/v1"
HEADERS = {"Authorization": f"Bearer {os.environ['APIMART_API_KEY']}", "Content-Type": "application/json"}

created = requests.post(f"{BASE}/videos/generations", headers=HEADERS, timeout=60, json={
    "model": "kling-v2-6-motion-control", "prompt": "A bamboo forest at sunrise, slow push-in", "duration": 5,
}).json()
task_id = created["data"]["id"]

while True:
    task = requests.get(f"{BASE}/tasks/{task_id}", headers=HEADERS, timeout=60).json()["data"]
    if task["status"] in ("completed", "failed"):
        break
    time.sleep(5)
print(task.get("cost"), task["result"]["videos"][0]["url"])
```

Runnable versions: [`examples/`](examples). The task lifecycle is `pending → processing → completed | failed`.

## FAQ

**Wie lautet die Modell-id von Kling 2.6 Motion Control?**

`kling-v2-6-motion-control`. Siehe Routentabelle oben.

**Wie wird abgerechnet?**

**from $0.0571 per second** on the APIMart route. Die abgeschlossene Aufgabe meldet den genauen Betrag im Feld `cost`; eine fehlgeschlagene Aufgabe wird erstattet.

**How do I get a key?**

Use the [Get an API key](https://go.apimart.ai/k-ba9cc8) link — $1 minimum top-up, no plan required.

<!-- related-repos:auto -->
## Related repositories

- **Same model, this language** — the other half of this pair: [kling-v2-6-motion-control-prompts-de](https://github.com/ptnzf4jt/kling-v2-6-motion-control-prompts-de)
- **Same model, other languages** — 10 more language builds: English `kling-v2-6-motion-control-api` · 中文 [kling-v2-6-motion-control-api-cn](https://github.com/v0k1hdrf-4jv/kling-v2-6-motion-control-api-cn) · Español [kling-v2-6-motion-control-api-es](https://github.com/s2a52q/kling-v2-6-motion-control-api-es) · Français [kling-v2-6-motion-control-api-fr](https://github.com/il0xj8m/kling-v2-6-motion-control-api-fr) · Relay/gateway `kling-v2-6-motion-control-api-gateway` · Bahasa `kling-v2-6-motion-control-api-id` · 日本語 [kling-v2-6-motion-control-api-ja](https://github.com/swttr92mb2hr6k/kling-v2-6-motion-control-api-ja) · 한국어 [kling-v2-6-motion-control-api-ko](https://github.com/hnkcrt6/kling-v2-6-motion-control-api-ko) · Português [kling-v2-6-motion-control-api-pt](https://github.com/x-xvyf2/kling-v2-6-motion-control-api-pt) · Русский `kling-v2-6-motion-control-api-ru`
- **More models in this language** — [midjourney-api-de](https://github.com/h5fd0cofy/midjourney-api-de) · [gemini-2-5-flash-image-preview-api-de](https://github.com/kn6f69s2b8j9/gemini-2-5-flash-image-preview-api-de) · [nano-banana-api-de](https://github.com/uh6cob8op/nano-banana-api-de) · [gemini-3-1-flash-image-preview-api-de](https://github.com/k8wq8pd46e5ku/gemini-3-1-flash-image-preview-api-de) · [nano-banana-2-api-de](https://github.com/mocpl3/nano-banana-2-api-de) · [gemini-3-pro-image-preview-api-de](https://github.com/cmpxx2w/gemini-3-pro-image-preview-api-de)
- **Topic hubs** — every build of this model, all languages: [kling-v2-6-motion-control](https://github.com/topics/kling-v2-6-motion-control) · [kling-v2-6-motion-control-api](https://github.com/topics/kling-v2-6-motion-control-api)

This repository is one build in a cross-linked set of API guides for the same model family; each language build links back to the others.
<!-- /related-repos:auto -->

## Attributed links (how this repository is measured)

| Purpose | Attributed link | Target |
| --- | --- | --- |
| Model page | <https://go.apimart.ai/k-88c2d9> | `apimart.ai/de/model/kling-v2-6-motion-control` |
| Live pricing | <https://go.apimart.ai/k-0d9c3b> | `apimart.ai/de/pricing` |
| Get an API key | <https://go.apimart.ai/k-ba9cc8> | `apimart.ai/de/keys` |

Outbound APIMart links are minted through the promo link API; hand-made tracking parameters are rejected by
`tools/check_links.py` in CI.

## Disclosure

Kling 2.6 Motion Control is a third-party model served through APIMart; this repository documents how to call it and publishes
model ids and prices, and does not claim official status. Model names, prices and documentation belong to their
respective owners.

## License

MIT — see [LICENSE](LICENSE).
