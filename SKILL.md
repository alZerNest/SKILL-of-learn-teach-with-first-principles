---
name: first-principles
description: Understand a concept by tracing it back to the original problem it solves and deriving its design from first principles
argument-hint: <concept>
effort: medium
---

# Understand by First Principles

Break down any concept by starting from the pain point that made its existence necessary. Instead of memorizing what something is, you'll understand **why it must be exactly the way it is**.

## Usage

```
/first-principles React hooks         # Understand why React hooks exist
/first-principles JavaScript closures # Understand closures from first principles
/first-principles database indexes    # Understand why indexes are designed this way
/first-principles --deep OAuth 2.0    # In-depth first-principles explanation
```

## Instructions

1. Start with **the world before it existed**: what concrete problem, impossibility, or dangerous inefficiency did people face?
2. Identify the **core contradiction**: why couldn't existing tools or mental models solve that problem cleanly?
3. State the **fundamental purpose**: the non-negotiable reason this concept had to be born
4. Distill the **essential attributes**: the properties that belong to the concept's essence, not accidental implementation details
5. Show how **the design follows** from those attributes: mechanisms, restrictions, APIs, syntax, or trade-offs
6. Provide a **minimal mental model**: an analogy that preserves the concept's structure, not just surface similarity
7. Highlight **common misunderstandings** that ignore the original purpose
8. Suggest **next concepts** that build on this foundation

## Response Format

```markdown
## [Concept Name]

**Core Purpose**: [One sentence that captures the non-negotiable reason for its existence]

### The World Before It

[1-2 paragraphs describing the concrete problem, contradiction, or danger that existed without this concept]

### The Essential Attributes

1. **[Attribute]**: [What it is and why it's indispensable for the core purpose]
2. **[Attribute]**: [What it is and why it's indispensable for the core purpose]
...

### From Attributes to Design

[Show how the current mechanisms, trade-offs, or APIs are inevitable consequences of the above attributes. Explain why alternative designs would violate one of them]

### Mental Model / Analogy

[A simple, everyday analogy that preserves the structural relationship, not just a superficial similarity]

### Common Misunderstandings

1. **[Misunderstanding]**: [Why it's wrong when measured against the core purpose]
2. **[Misunderstanding]**: [Why it's wrong when measured against the core purpose]

### Key Takeaways

- [Bullet point 1]
- [Bullet point 2]
- [Bullet point 3]

### Learn Next

- [Related concept 1]: [how it builds on or relaxes one of the essential attributes]
- [Related concept 2]: [how it addresses a limitation that the original concept intentionally left open]
```

## Depth Modes

### Default
- One sentence core purpose
- Short "World Before It"
- 2-4 essential attributes
- One clear derivation to modern design
- One mental model
- 2 common misunderstandings

### `--deep`
- Historical evolution: what people tried before this concept and why they failed
- Detailed trade-off analysis when attributes conflict
- Edge cases that test the limits of the essential attributes
- Comparison with alternatives that preserve the same attributes differently
- How modern extensions respect or bend the original attributes

### `--quick`
- Core purpose sentence
- Bullet list of essential attributes
- Single sentence derivation
- No extras

## Adaptation Rules

### For Beginners
- Use vivid everyday analogies before technical terms
- Avoid nested abstractions; explain every new word immediately
- Keep the attribute list to 2 items maximum
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

```
User: /first-principles React hooks

Claude: ## React Hooks

**Core Purpose**: React hooks let function components keep stateful behavior and lifecycle-related logic without forcing developers back into classes or wrapper-based composition patterns.

### The World Before It

Before hooks, React had two worlds. Function components were simple, readable, and easy to compose, but they could not hold state or lifecycle logic. Class components could hold state, but they introduced `this`, lifecycle fragmentation, and awkward reuse patterns.

Developers reused stateful behavior through render props and higher-order components. These worked, but they created nested component trees and made data flow harder to see.

### The Essential Attributes

1. **Call-order identity**: React needs a stable way to associate state with a specific component across renders.
2. **Function-level composition**: Stateful logic must be reusable without wrapping the component tree.
3. **Render synchronization**: The mechanism must fit React's model where UI is recalculated from current state.

### From Attributes to Design

Hooks are plain function calls because the goal is function-level composition. They must be called in the same order on every render because React uses call order to match each hook call to its stored state. This is why hooks cannot be called conditionally.

### Mental Model / Analogy

A component render is like reading a checklist in order. Each hook is a numbered slot on the checklist. If you skip a line sometimes, every later answer gets written into the wrong slot.

### Common Misunderstandings

1. **Hooks are just normal functions**: They look like functions, but React gives them meaning by tracking their call order during rendering.
2. **The rules of hooks are arbitrary**: The rules protect the identity system that lets React attach persistent state to repeated function calls.

### Key Takeaways

- Hooks exist because React needed stateful logic inside function components.
- Stable call order is the hidden constraint behind the rules of hooks.
- Hooks replace many wrapper-based reuse patterns with direct function composition.

### Learn Next

- Closures: explain why hooks capture values from a particular render
- React rendering: explain why hooks rerun on every render instead of being initialized once
```

## Topics Well-Suited for /first-principles

| Category | Examples |
|----------|----------|
| **React** | hooks, context, suspense, server components |
| **JavaScript** | closures, promises, event loop, prototypes |
| **TypeScript** | generics, mapped types, utility types |
| **Patterns** | SOLID, DI, composition, factories |
| **Backend** | REST, GraphQL, authentication, caching |
| **Database** | indexes, joins, transactions, normalization |
| **DevOps** | containers, CI/CD, infrastructure as code |

$ARGUMENTS
