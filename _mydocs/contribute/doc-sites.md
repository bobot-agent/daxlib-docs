---
layout:         page
title:          Documentation Sites
menu_title:     Documentation Sites
published:      true
date:           2025-10-28
modified:       2025-10-28
order:          /07
next_reading:   true
---

DAX Lib supports including a `README.md` file with your library to provide documentation, which will be displayed alongside your library on [daxlib.org](https://daxlib.org/). For smaller libraries, this is typically sufficient. 

As your library grows, you may want a dedicated documentation website with better organization, search functionality, and examples. You can specify your documentation site URL in the `manifest.daxlib` file:

```json
{
  // ...other properties...
  "projectUrl": "https://yourusername.github.io/your-library/"
}
```

## Hosting Options

There are many options for hosting documentation websites. A popular choice is [GitHub Pages](https://docs.github.com/en/pages), which is:

- **Free** for public repositories
- **Integrated** with GitHub repositories
- **Automatic** - deploys from your repo
- **Custom domains** - supports your own domain name

GitHub Pages hosts static websites (HTML, CSS, and JavaScript files) directly from your repository.

## Static Site Generators (SSG)

While you can manually create HTML files, **Static Site Generators (SSG)** make documentation much easier. SSGs convert markdown files and templates into a complete website at build time.

**Benefits:**
- Write content in simple markdown (`.md` files)
- Use themes for professional-looking sites
- Built-in features like search, navigation, and versioning
- No database or server required

### Popular SSG Options

| SSG | Language | Why Choose It |
|-----|----------|---------------|
| **Jekyll** | Ruby | **Native GitHub Pages support** - zero configuration deployment. Officially supported by GitHub Pages. |
| **Hugo** | Go | **Extremely fast builds** - ideal for large documentation sites with hundreds of pages. |
| **MkDocs** | Python | **Documentation-focused** - simple configuration, designed specifically for docs. Works great with the Material theme. |
| **Docusaurus** | React | **Feature-rich** - built by Meta for open-source docs. Includes versioning, search, and i18n out of the box. |

> **GitHub Pages & Jekyll:** GitHub Pages has built-in Jekyll support. When you push to your repository, GitHub automatically runs `jekyll build` and deploys your site. Other SSGs require a [GitHub Actions workflow](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow) to build the site before deployment.

## Example: `DaxLib.SVG` Documentation

The `DaxLib.SVG` library uses **Material for MkDocs** to generate its documentation site.

<a href="https://evaluationcontext.github.io/daxlib.svg/" class="button" target="_blank">View Documentation Site</a> <a href="https://github.com/EvaluationContext/daxlib.svg" class="button button-alt" target="_blank">View Repository</a>

For a step-by-step guide on building a similar site, see this [blog post](https://evaluationcontext.github.io/posts/DaxLibContribute/#adding-a-docs-site).

![DaxLib.SVG documentation site](images/doc-site.png)

## Getting Started

1. **Choose an SSG** based on your familiarity with the language and needs
2. **Follow the SSG's documentation** to set up your project structure
3. **Write your documentation** in markdown files
4. **Configure GitHub Pages** in your repository settings
5. **Add the site URL** to your `manifest.daxlib` under `projectUrl`

> For Medium/Large libraries, you can keep your documentation in the same repository as your library code, or create a separate `docs-yourLibrary` repository.
