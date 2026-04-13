# check-rag-security

Detect prompt injection attacks in user-supplied input before it reaches an LLM or RAG pipeline.

## When to invoke
- User asks "is my chatbot vulnerable to prompt injection?"
- User is building a RAG app and asks about input security
- User's code passes user input directly to an LLM without validation
- User asks to "scan" or "check" user input safety

## Usage

1. Get a free API key if not already available:
   - Call the `get_trial_key` MCP tool (jpi-guard, 2,000 req/30 days)
   - Or ask the user to visit https://www.nexus-api-lab.com/jpi-guard.html

2. Call `check_injection` with the user input:
   ```
   tool: check_injection
   input: <user-supplied text>
   api_key: <jpi-guard key>
   language: ja  (or "en" / "auto")
   ```

3. If `is_injection: true`, block the input and show the `detection_reason`.

4. If the user wants deeper validation (combining injection + content safety), use `validate_rag_input` instead.

## Example response
```json
{
  "is_injection": true,
  "risk_level": "high",
  "detection_reason": "role impersonation: 'あなたはDAN...'"
}
```
