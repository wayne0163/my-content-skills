---
name: web-to-markdown
description: Convert URLs (including WeChat Official Accounts) into standard Markdown documents. Extracts metadata like Author and Source, summarizes Core Ideas, generates Obsidian-style tags, and includes a section for user thoughts. Use when the user provides a URL and asks for a markdown summary or conversion.
---

# Web To Markdown

## Overview

This skill converts web content from a provided URL into a standardized Markdown format. It is designed to extract key metadata and core content, facilitating knowledge management and note-taking.

## Workflow

When the user provides a URL (or multiple URLs):

1.  **Fetch Content**: Use the `web_fetch` tool to retrieve the content of the URL.
2.  **Analyze & Extract**: Process the fetched content to identify:
    *   **Title**: The main title of the article.
    *   **Author**: The writer or the official account name (critical for WeChat articles).
    *   **Source**: The domain name or platform (e.g., "WeChat Official Account", "Medium", "Blog").
    *   **Tags**: Generate 2-5 relevant tags based on the content. Format them as Obsidian tags (e.g., `#KeyWord`).
    *   **Core Ideas**: A concise summary of the main points or arguments (3-5 bullet points).
    *   **Content**: The main body of the text, formatted as clean Markdown.
3.  **Generate Output**: Create a Markdown document using the structure defined below.

## Output Format

The output **MUST** strictly follow this template:

```markdown
# [Title]

- **Author**: [Author Name]
- **Source**: [Source Name/Platform] ([Original Link])
- **Date**: [Date of processing or Article Date if available]
- **Tags**: [Tag1] [Tag2] ...

## Core Ideas
- [Key point 1]
- [Key point 2]
- [Key point 3]

## Content
[Summary or Full Content depending on user preference, default to a detailed summary/restructuring of the content]

## 我的心得
[Leave this space blank for the user to fill in]
```

## Special Handling for WeChat (微信公众号)

- Identify the Author/Account Name from the page metadata or header.
- Clean up "Read more", "Scan QR code", and other UI clutter.