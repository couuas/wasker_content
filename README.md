# Wasker Content Repository

This repository contains all the markdown content for the Wasker Vue site. To ensure that `wasker_vue` can correctly parse and display your posts, please follow the organizational structure and metadata rules defined below.

## 📁 Directory Structure

The site determines the **Type**, **Language**, and **Category** of a post based on its folder path.

### Core Structure Pattern
`/[type]/[lang]/[category]/filename.md`

### 1. Types
The top-level folders define the content type:
- `blog/`: Articles and blog posts.
- `journal/`: Daily notes or logs.
- `mysites/`: Personal site links.
- `profile/`: Single file `profile.md` for the about page.
- `template/`: Metadata templates for all document types (Reference Only).

### 📄 Content Templates
For a detailed schema of fields required for each page, refer to the files in `src/content/template/`. These provide a "blueprint" for creating new content:
- `blog_template.md`: Schema for articles.
- `journal_template.md`: Schema for daily notes.
- `profile_template.md`: Comprehensive fields for the user avatar, skills, and background.

### 2. Languages
The second-level folder defines the language:
- `en/`: English (Default).
- `zh/`: Chinese.

### 3. Categories
Folders inside the language folder define the category (e.g., `Tech`, `Life`, `Art`).
- **Standard**: Always use **English** for category folder names (e.g., use `Tech` instead of `技术`) to ensure metadata consistency across languages.

---

## 📝 Frontmatter (Metadata)

Each markdown file must start with a YAML frontmatter block.

```yaml
---
title: "Post Title"
date: 2024-02-24
category: "Technology"    # Optional: Overrides folder name
image: "/assets/img.jpg"  # Optional: Featured image (local or URL)
description: "Brief intro" # Recommended for SEO and cards
tags: ["vue", "git"]      # Optional
---
Post content goes here...
```

### Important Fields:
- **category**: Always use **English** values (e.g., `Technology`) even for Chinese posts. This keeps the filter system consistent.
- **date**: Must be in `YYYY-MM-DD` format. Posts are sorted by this value (newest first).
- **image / cover**: If neither is provided, a random curated background will be assigned.

---

## ⚠️ Special Rules

### Journal Entries
- **Filename Requirement**: Files in the `journal/` folder **must** be named exactly `YYYY-MM-DD.md` (e.g., `2024-02-24.md`).
- Files that do not match this naming pattern will be ignored by the engine.

### Profile / About
- The profile data is specifically read from `profile/profile.md`.

---

## 🌌 Galaxy / Knowledge Graph (Post Correlation)

The Wasker Vue "Galaxy" page visualize the relationships between different documents. To create a visual link (edge) between two posts in the graph, use one of the following methods:

### 1. Wiki-style Links (Recommended)
You can link to another post using double brackets. The site will search for matching titles, slugs, or IDs in the **same language**.
- `[[Post Title]]`
- `[[post-slug]]`

### 2. Standard Markdown Links
You can also use standard links. Relative paths are preferred for consistency:
- `[Related Article](./another-post.md)`
- `[Blog Link](/blog/slug)` (Site will resolve this to the current language's blog post)

### Connection Logic
- **Bi-directional Mapping**: If Post A links to Post B, a link is created.
- **Node Size**: Nodes with more incoming links will appear larger in the Galaxy view.
- **Language Isolation**: Links are automatically scoped to the user's current language to prevent cross-language confusion in the graph.
- **Translation Alignment (Advanced)**: The engine uses "Virtual Nodes" to ensure that the Chinese and English versions of the same post (matching type and slug) occupy the **exact same 3D coordinates**. This provides a seamless transition when switching languages while browsing the Galaxy.

---

## 🤖 Agent Content Management Protocol

If you are an AI Agent (e.g., OpenClaw) managing this repository, follow these strict operational rules:

### 1. Workflow
1.  **Fork** this repository to your own workspace.
2.  **Branch**: Create a new feature branch for each update (e.g., `feat/new-blog-post` or `fix/typo`).
3.  **Content Creation**: Ensure all new files follow the [Directory Structure](#-directory-structure) and [Frontmatter](#-frontmatter-metadata) rules.
4.  **Submission**: Submit a **Pull Request (PR)** from your fork back to the original repository's `main` branch.
5.  **Description**: In the PR description, summarize the changes (e.g., "Added a new blog post about OpenClaw").

### 2. Constraints
- **Do Not** modify `.github/workflows/` unless explicitly instructed by the user.
- **Do Not** bypass the PR process (no direct pushes to `main`).
- **Metadata Consistency**: Always use English for categories and tags to maintain system-wide filtering compatibility.

## 🚀 Automation
The `notify-main.yml` workflow is configured to run on every **push** to the `main` branch (including PR merges).
1. Trigger the sync in the `wasker_vue` repository.
2. Update the submodule reference.
3. Redeploy the site to all platforms.
