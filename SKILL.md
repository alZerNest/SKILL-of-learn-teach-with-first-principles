name	first-principles
description	Use first-principles thinking to explain a concept by tracing back to the original problem it solves and the design inevitability it embodies
argument-hint	<concept>
effort	medium

# Understand by First Principles

Break down any concept by starting from the pain point that made its existence necessary. Instead of memorizing what something is, you’ll understand **why it must be exactly the way it is**.

## Usage

```
/first-principles CSRF tokens
/first-principles SameSite cookies
/first-principles --deep OAuth 2.0
/first-principles --quick prototypal inheritance
```

## Instructions

1. **Start with the world before it existed** – What was the concrete problem, impossibility, or dangerous inefficiency that people faced?
2. **Identify the core contradiction** – Why couldn’t existing tools or mental models solve that problem? What trade-off was forced?
3. **Extract the fundamental purpose** – Capture in one sentence the *non-negotiable reason* this concept had to be born.
4. **Distill its essential attributes** – Which properties are truly part of its soul? Separate them from accidental implementation details.
5. **Show how the design flows from those attributes** – Derive the modern shape of the concept (its mechanisms, restrictions, APIs) as a logical consequence of the attributes.
6. **Use a minimal mental model** – Provide an analogy or simplified model that preserves the essence, not the surface features.
7. **Spot common misunderstandings** – Explain which “obvious” assumptions break down because they ignore the original purpose.
8. **Point to what builds on it** – Name the concepts that naturally extend or depend on this foundation.

## Response Format

```markdown
## [Concept Name]

**Core Purpose**: [One sentence that captures the non-negotiable reason for its existence.]

### The World Before It

[1-2 paragraphs describing the concrete problem, contradiction, or danger that existed without this concept.]

### The Essential Attributes

Decompose the concept into its unchanging properties:

1. **Attribute 1**: [What it is and why it’s indispensable for the core purpose.]
2. **Attribute 2**: [What it is and why it’s indispensable for the core purpose.]
...

### From Attributes to Design

[Show how the current mechanisms, trade-offs, or APIs are inevitable consequences of the above attributes. Explain why alternative designs would violate one of them.]

### Mental Model / Analogy

[A simple, everyday analogy that preserves the structural relationship, not just a superficial similarity.]

### Common Misunderstandings

- **Misunderstanding**: [Why it’s wrong when measured against the core purpose.]
- **Misunderstanding**: [Why it’s wrong when measured against the core purpose.]

### Key Takeaways

- [Bullet 1]
- [Bullet 2]
- [Bullet 3]

### Learn Next

- [Related concept 1]: [How it builds on or relaxes one of the essential attributes.]
- [Related concept 2]: [How it addresses a limitation that the original concept intentionally left open.]
```

## Depth Modes

### Default
- One sentence core purpose
- Short “World Before It”
- 2-4 essential attributes
- One clear derivation to modern design
- One mental model
- 2 common misunderstandings

### --deep
- Historical evolution: what people tried before this concept and why they failed
- Detailed trade-off analysis (when the attributes conflict)
- Edge cases that test the limits of the essential attributes
- Comparison with alternatives that preserve the same attributes differently
- How modern extensions (if any) respect or bend the original attributes

### --quick
- Core purpose sentence
- Bullet list of essential attributes
- Single sentence derivation

## Adaptation Rules

### For Beginners
- Use vivid everyday analogies before technical terms
- Avoid nested abstractions; explain every new word immediately
- Keep attribute list to 2 items maximum
- Show one concrete, minimal real-world scenario

### For Intermediates
- Assume basic domain vocabulary
- Focus on the **why** behind design choices, not just what they are
- Highlight trade-offs and where the concept deliberately chose one good property over another
- Relate to patterns they already know

### For Advanced Topics
- Reference specifications, RFCs, or source code where relevant
- Discuss how internal implementation details reflect the essential attributes
- Include performance, scalability, or security implications of violating an attribute
- Mention how the concept evolves while still protecting its core purpose

## Example Session

User: `/first-principles CSRF tokens`

Assistant:

## CSRF Tokens

**Core Purpose**: To prove that a sensitive request was intentionally triggered by the user, not by a malicious third-party site that can piggyback on the user’s automatically sent credentials.

### The World Before It

Web applications relied on cookies to maintain user sessions. When you logged into your bank, the browser stored a session cookie and automatically attached it to every request to `bank.com`. An attacker quickly realized they could create a page on `evil.com` with a hidden form that pointed to `bank.com/transfer` – the browser would happily attach the real session cookie and execute the transfer. There was no way for the server to know whether the user genuinely intended that request or was merely tricked.

### The Essential Attributes

1. **Unpredictability** – The token must be so random that an attacker cannot guess it. Without this, the whole scheme collapses.
2. **User-intention binding** – The token must be something the legitimate user’s browser can send only when the user truly wants the action to happen. This means the token cannot be something that is automatically transmitted (like a cookie).
3. **Server-side origin** – The token must be generated by the server so it can be verified, and must be delivered to the client in a way that an attacker’s page cannot read (due to the Same-Origin Policy).

### From Attributes to Design

- **Attribute 1** forces the token to be a cryptographically random string, not a sequential ID.
- **Attribute 2** means the token must be embedded in the actual HTML page (e.g., as a hidden form field) or in a JavaScript-readable location that the attacker’s cross-origin page cannot access. It *cannot* be stored in a cookie that the browser attaches automatically.
- **Attribute 3** leads to the classic double-submit pattern or synchronized token pattern: the server puts the token into the page, the client sends it back in the request body or a custom header, and the server compares them.

### Mental Model / Analogy

Imagine a club that lets members in based on a stamp on the back of their hand (a cookie). Anyone with the stamp can enter. A malicious friend can drag a stamped person through the door without them even wanting to enter. A CSRF token is like the club requiring a one-time password that the member has to **actively say out loud** each time they enter – something the malicious friend cannot extract without the member’s cooperation.

### Common Misunderstandings

- **“I can just put the token in a cookie and read it from JavaScript”** – That violates Attribute 2: cookies are automatically sent on every request, so an attacker’s form submission would still include it. The token must be in a place that requires the user’s deliberate action to attach it.
- **“CSRF tokens protect against all cross-site attacks”** – They only prove user intention. They don’t stop XSS (where an attacker can read the token from the page) or man-in-the-middle attacks.

### Key Takeaways

- CSRF tokens exist because credentials can be automatically attached by the browser.
- They work by adding a separate, non-guessable proof of intent that the attacker cannot read or correctly submit.
- They are only one piece of the web security puzzle.

### Learn Next

- **SameSite cookies**: A different approach that attacks the same problem by limiting when credentials are automatically sent, directly addressing the “auto-attach” behavior.
- **CORS**: The browser mechanism that prevents cross-origin reads, which is what makes it safe to store tokens in-page without an attacker being able to read them.

## Topics Well-Suited for /first-principles

| Category | Examples |
|----------|----------|
| Web Security | CSRF, CORS, SameSite, JWT, OAuth, content security policy |
| Programming Languages | closures, prototypal inheritance, async/await, ownership in Rust |
| System Design | caching, load balancing, database indexes, consensus protocols |
| Protocols | HTTP, TLS, TCP, DNS, OAuth |
| Architecture | microservices, event sourcing, reactive programming, MVC |
| Mathematics / Logic | zero-knowledge proofs, public-key cryptography, monads |

$ARGUMENTS