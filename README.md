<p align="center">
  <img src="assets/banner.png" alt="HumanMark - Open Source AI Content Detection" width="100%">
</p>

<h1 align="center">HumanMark</h1>

<p align="center">
  <strong>Open source AI content detection. One API. Zero dependencies.</strong>
</p>

<p align="center">
  <a href="https://github.com/vinpatel/humanmark/stargazers">
    <img src="https://img.shields.io/github/stars/vinpatel/humanmark?style=social" alt="Stars">
  </a>
  <a href="https://github.com/vinpatel/humanmark/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License">
  </a>
  <a href="https://go.dev">
    <img src="https://img.shields.io/badge/Go-1.21+-00ADD8?logo=go" alt="Go Version">
  </a>
</p>

---

Detect AI-generated text, images, audio, and video—entirely offline, with no external API calls.

## Why HumanMark?

| Feature | HumanMark | GPTZero, etc. |
|---------|-----------|---------------|
| Self-hosted | ✅ | ❌ |
| Works offline | ✅ | ❌ |
| Zero cost | ✅ | ❌ |
| Privacy-first | ✅ | ❌ |
| Open source | ✅ | ❌ |
| Multi-modal | ✅ Text, Image, Audio, Video | ⚠️ Mostly text-only |

## Use Cases

### For Developers
| Use Case | Description |
|----------|-------------|
| Content platforms | Filter AI spam from submissions |
| Hiring tools | Check candidate writing samples |
| Education apps | Verify student work |
| Social apps | Flag synthetic profiles/posts |
| CMS plugins | WordPress, Ghost, etc. |
| CI/CD pipelines | Lint content like you lint code |
| Browser extensions | Detect AI on any page |

### For Organizations
| Who | Why HumanMark |
|-----|---------------|
| Enterprises | Compliance requirements—can't send data to third-party APIs (HIPAA, GDPR, SOC2) |
| Government & Defense | Air-gapped networks, classified environments |
| Law firms | Attorney-client privilege, can't upload client docs to cloud |
| Healthcare | Patient data must stay on-premise |
| Banks & Financial | Regulatory restrictions on data sharing |
| Universities | High volume (100K+ students), budget constraints |
| Publishers & Media | Own the tool, don't rent it |

## Quick Start

### Option 1: Go Install

```bash
go install github.com/vinpatel/humanmark/cmd/api@latest
```

### Option 2: Docker

```bash
docker run -p 8080:8080 humanmark/humanmark
```

### Option 3: Build from Source

```bash
git clone https://github.com/vinpatel/humanmark.git
cd humanmark
go run cmd/api/main.go
```

Server runs at `http://localhost:8080`

## Usage

### Detect Text

```bash
curl -X POST http://localhost:8080/verify \
  -H "Content-Type: application/json" \
  -d '{"text": "Your content here"}'
```

### Response

```json
{
  "id": "abc123",
  "human": true,
  "confidence": 0.85,
  "content_type": "text"
}
```

### Detailed Analysis

```bash
curl -X POST "http://localhost:8080/verify?detailed=true" \
  -H "Content-Type: application/json" \
  -d '{"text": "Your content here"}'
```

## How It Works

HumanMark uses statistical and forensic analysis—no ML models required.

### Text Detection

| Signal | Human | AI |
|--------|-------|-----|
| Sentence length variance | High | Low |
| Vocabulary richness | Varied | "Safe" words |
| Contractions | "don't", "I'm" | "do not", "I am" |
| Punctuation variety | !?;:— | Mostly periods |
| AI phrases | Rare | "As an AI...", "It's important to note..." |

### Image Detection

| Signal | Real Photo | AI Image |
|--------|------------|----------|
| EXIF metadata | Present | Missing/fake |
| Camera make | Apple, Canon, etc. | None |
| Sensor noise | Natural pattern | Too clean |

### Audio and Video Detection

Analyzes format metadata, encoder signatures, and AI tool markers.

## API Reference

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/verify` | POST | Analyze content |
| `/verify/{id}` | GET | Get result by ID |
| `/health` | GET | Health check |

## Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `PORT` | 8080 | Server port |
| `ENV` | development | Environment |
| `LOG_LEVEL` | info | Logging level |

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md).

**Help us improve accuracy** by [reporting false positives/negatives](https://github.com/vinpatel/humanmark/issues/new).

## License

MIT License. See [LICENSE](LICENSE).

---

<p align="center">
  <b>Star this repo if you find it useful!</b>
</p>
