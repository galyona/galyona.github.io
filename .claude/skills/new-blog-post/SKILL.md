---
name: new-blog-post
description: Add a new blog post to the website. Use when the user has placed blog post text in blog/texts/ directory and wants to publish it. Converts text to HTML, generates image prompt, adds meta tags.
---

# New Blog Post Workflow

When the user wants to add a new blog post, follow these steps:

## Step 1: Find and Read the Source Text

Look for new files in `blog/texts/` directory. Use `textutil -convert txt <filename>.docx -stdout` to extract text from Word documents.

## Step 2: Create the HTML Blog Post

Create a new HTML file in `blog/` following the site's existing conventions:

- Match the structure of existing posts (see `blog/navigating-tradeoffs.html` as reference)
- Use semantic HTML: `<article>`, `<header>`, `<h1>`, `<time>`, `<p>`, `<blockquote>`, `<em>`, `<strong>`
- Apply minimal formatting:
  - Convert dashes to em-dashes (`&mdash;`)
  - Format definitions/quotes as `<blockquote>`
  - Emphasize key terms with `<em>`
  - Convert URLs to proper `<a target="_blank">` links
  - Use `<hr>` for section breaks
- Date format: `datetime="YYYY-MM-DD"` attribute, "Month Day, Year" display text

## Step 3: Update Blog Index and Home Page

- Add the new post to the top of `blog/index.html` with title, date, and excerpt
- Add the new post to the blog section in `index.html` (home page)
- Update `sitemap.xml` with the new post URL

## Step 4: Generate Image Prompt

Provide the user with a prompt for Gemini (Nano Banana) to generate a social sharing image:

```
Create a minimal editorial illustration for a blog post titled "[POST TITLE]" about [BRIEF TOPIC DESCRIPTION].

Style: New York Times opinion section, sophisticated and understated.

Visual concept: [ONE SIMPLE SYMBOLIC ELEMENT related to the topic]. Clean negative space. Perhaps subtle shadows.

Dimensions: 1200x630 pixels (landscape, Twitter card format).

Color palette: Muted and limited - warm off-white or cream background (#fffff8) with one accent color (soft terracotta, muted burgundy, or deep navy).

No text in the image. No digital elements. No busy details. Elegant simplicity. Editorial illustration style, slightly abstract or stylized rather than photorealistic.
```

Tell the user to save the image to `imgs/[post-slug].png`

## Step 5: Add Meta Tags

Once the user confirms the image is saved, add Open Graph and Twitter meta tags to the blog post's `<head>`:

```html
<meta name="description" content="[Brief description]">
<meta name="author" content="Gal Yona">
<link rel="canonical" href="https://galyona.github.io/blog/[slug].html">

<!-- Open Graph -->
<meta property="og:type" content="article">
<meta property="og:url" content="https://galyona.github.io/blog/[slug].html">
<meta property="og:title" content="[Post Title]">
<meta property="og:description" content="[Brief description]">
<meta property="og:image" content="https://galyona.github.io/imgs/[slug].png">
<meta property="og:site_name" content="Gal Yona">
<meta property="article:author" content="Gal Yona">
<meta property="article:published_time" content="[YYYY-MM-DD]">

<!-- Twitter -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:site" content="@_galyo">
<meta name="twitter:creator" content="@_galyo">
<meta name="twitter:title" content="[Post Title]">
<meta name="twitter:description" content="[Brief description]">
<meta name="twitter:image" content="https://galyona.github.io/imgs/[slug].png">
```

## Step 6: Commit and Push

Stage all changes and commit:
- The new blog post HTML
- Updated `blog/index.html`
- Updated `index.html`
- Updated `sitemap.xml`
- The new image in `imgs/`

Push to deploy to GitHub Pages.

## Step 7: Verify

Suggest the user test the social preview at opengraph.xyz before sharing.
