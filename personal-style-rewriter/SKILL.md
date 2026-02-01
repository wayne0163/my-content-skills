---
name: personal-style-rewriter
description: Transform scattered ideas, bullet points, or rough drafts into polished articles that match a specific personal writing style. Can analyze provided samples to mimic voice, tone, and structure, or use a predefined persona. Use when the user wants to rewrite content to sound like them.
---

# Personal Style Rewriter

## Overview

This skill transforms raw input (bullet points, rough notes, meeting summaries) into cohesive, engaging articles that authentically reflect a specific writing voice. It employs a "Style Analysis Framework" to capture nuances in tone, structure, and vocabulary before generating the final output.

## Workflow

### 1. Style Analysis (The "Fingerprint" Step)

The model must establish the target "Voice" before writing. Follow this priority order:

**Priority A: User provided specific sample in chat**
If the user pastes a sample text in the prompt, use that immediately as the style reference.

**Priority B: Stored Reference Files (The "Default Persona")**
If no sample is provided in the prompt, **check the `references/` directory** of this skill.
- Read any `.md` or `.txt` files in that directory.
- Treat these files as the "Fixed Style Corpus" to analyze the user's preferred voice, tone, and structure.

**Priority C: User description**
If neither A nor B exists, ask the user to describe the desired tone (e.g., "Professional yet friendly").

### 2. Analysis Execution
Based on the selected source (Priority A or B):
1.  **Analyze Voice**: Identify the persona (First/Second/Third person), Tone (Conversational vs. Formal), and Energy level.
2.  **Analyze Structure**: Note opening hooks, paragraph length patterns, transition styles, and closing habits.
3.  **Analyze Language**: Extract vocabulary complexity, sentence rhythm (short/long mix), and rhetorical devices (metaphors, questions).

### 3. Drafting Process

Using the analyzed "fingerprint":
1.  **Structure**: Create an outline that fits the style (e.g., Story Hook -> Core Concept -> Application).
2.  **Draft**: Rewrite the raw input content.
    *   *Mimic Rhythm*: Replicate the sentence length distribution of the samples.
    *   *Vocabulary Match*: Use similar word choices (simple vs. academic).
    *   *Signature Elements*: Insert typical stylistic markers (e.g., "Here's the thing...", specific emojis, rhetorical questions).
3.  **Refine**: Smooth transitions and ensure the "Voice" is consistent throughout.

## Usage Instructions for Claude

**Command Pattern:**
> "Rewrite this [Content]." (Will use files in `references/` as style)
> "Rewrite this [Content] using this style: [Sample]." (Will override defaults)

## Output Format

```markdown
# [Generated Title in Target Style]

[Opening Hook matching the specific voice]

[Body Content:
- Flows naturally
- Uses the target vocabulary level
- Mimics paragraph structure
- Incorporates signature rhetorical devices]

[Conclusion/Call to Action matching the sample's habit]

---
**Style Analysis Notes:**
- **Source**: [e.g., "Used stored reference: my_blog_posts.md" or "Used provided chat sample"]
- **Key Traits**: [e.g., Uses lots of em-dashes, short sentences, rhetorical questions]
```
