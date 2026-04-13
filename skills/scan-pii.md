# scan-pii

Scan Japanese text for personally identifiable information (PII) and return masked output safe for downstream LLM pipelines.

## When to invoke
- User is processing Japanese text that may contain personal information
- User asks to "mask PII", "redact personal data", or "check for sensitive info"
- User's pipeline ingests user-generated content before passing to an LLM
- User is building a compliance tool or data anonymization feature

## Usage

1. Get a free PII Guard API key if not already available:
   - Call the `get_pii_guard_key` MCP tool with an email address
   - Or visit https://www.nexus-api-lab.com/pii-guard.html

2. Call `pii_scan`:
   ```
   tool: pii_scan
   text: <Japanese text to scan>
   api_key: <PII Guard key>
   mask: true  (default)
   ```

3. The response includes:
   - `findings[]` — detected PII with type, score, and position
   - `has_high_risk` — true if My Number, credit card, or passport detected
   - `masked_text` — text with PII replaced by `[NAME]`, `[PHONE]`, `[CARD]` etc.

## Detected PII categories (10 types)
- My Number / マイナンバー (mod-11 checksum validated)
- Credit card number (Luhn-validated)
- Bank account number
- Passport number
- Phone number
- Email address
- Postal address
- Date of birth
- Driver's license number
- Person name

## Example response
```json
{
  "findings": [
    { "type": "phone", "score": 0.95, "value": "090-1234-5678", "start": 5, "end": 18 }
  ],
  "has_high_risk": false,
  "masked_text": "私の[PHONE]に連絡してください"
}
```
