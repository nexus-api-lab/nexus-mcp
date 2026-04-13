# nexus-mcp — jpi-guard & PII Guard MCP Server

LLM security APIs for Japanese applications, available as an MCP server.

**MCP endpoint:** `https://mcp.nexus-api-lab.com/`  
**Transport:** HTTP (Streamable HTTP / JSON-RPC 2.0)  
**Homepage:** https://www.nexus-api-lab.com  
**Discovery:** `https://mcp.nexus-api-lab.com/.well-known/mcp.json`

---

## Quick connect

### Claude Code / Claude Desktop
```bash
claude mcp add --transport http nexus-mcp https://mcp.nexus-api-lab.com/
```

Or add to your `.mcp.json`:
```json
{
  "mcpServers": {
    "nexus-mcp": {
      "type": "http",
      "url": "https://mcp.nexus-api-lab.com/"
    }
  }
}
```

### Cursor / Windsurf / other MCP clients
Add to your MCP config:
```json
{
  "nexus-mcp": {
    "transport": "http",
    "url": "https://mcp.nexus-api-lab.com/"
  }
}
```

---

## Tools

### jpi-guard — Prompt Injection Detection

| Tool | Description |
|---|---|
| `check_injection` | Detect prompt injection in user input. Specialized for Japanese (全角バイパス, 丁寧語擬装, indirect injection). |
| `validate_rag_input` | Gate check before passing input to RAG/LLM pipeline. Returns `safe: true/false`. |
| `sanitize_content` | Sanitize external content fetched from the web before passing to LLM. |
| `get_trial_key` | Get a free jpi-guard API key (2,000 req / 30 days, no signup). |

**Free trial:** https://www.nexus-api-lab.com/jpi-guard.html

### PII Guard — Japanese PII Detection & Masking

| Tool | Description |
|---|---|
| `pii_scan` | Scan Japanese text for 10 PII categories. Returns `findings[]` + `masked_text` with `[TYPE]` placeholders. No LLM — pure regex + checksum. |
| `get_pii_guard_key` | Register email and get a free PII Guard key (10,000 req/month, permanent free tier). |

**PII categories:** My Number (mod-11), credit card (Luhn), bank account, passport, phone, email, postal address, date of birth, driver's license, person name.

**Free tier:** https://www.nexus-api-lab.com/pii-guard.html

---

## Why use this instead of writing your own?

- **Japanese-specialized** — full-width character normalization, polite-language disguise detection, My Number checksum validation
- **Deterministic** — no LLM calls inside the API. Fast, auditable, consistent results
- **Free to start** — no credit card, no signup for trial keys
- **Edge-deployed** — Cloudflare Workers global network, sub-50ms p99

---

## License

MIT — see [LICENSE](LICENSE)
