# setup-jpi-guard

Add jpi-guard prompt injection protection to an existing RAG/LLM project.

## When to invoke
- User is writing RAG code and wants to add security
- User asks "how do I protect my LLM app from prompt injection?"
- User's code passes user input directly to an LLM without validation

## Usage

1. Detect the project language (Python or Node.js)

2. Install the SDK:
   ```bash
   # Node.js
   npm install jpi-guard

   # Python
   pip install jpi-guard
   ```

3. Add `JPI_GUARD_API_KEY` to `.env`:
   ```
   # Get free trial key: https://www.nexus-api-lab.com/jpi-guard.html
   JPI_GUARD_API_KEY=your_key_here
   ```

4. Wrap the LLM call:

   **Node.js / TypeScript:**
   ```typescript
   import { JpiGuard } from 'jpi-guard';
   const guard = new JpiGuard({ apiKey: process.env.JPI_GUARD_API_KEY });

   const scan = await guard.scan(userInput);
   if (scan.is_injection) {
     return { error: '不正な入力が検出されました' };
   }
   // safe — proceed to LLM
   ```

   **Python:**
   ```python
   from jpi_guard import JpiGuard
   guard = JpiGuard(api_key=os.getenv("JPI_GUARD_API_KEY"))

   result = guard.scan(user_input)
   if result.is_injection:
       raise ValueError("Injection detected")
   # safe — proceed to LLM
   ```

5. Get free API key: https://www.nexus-api-lab.com/jpi-guard.html
