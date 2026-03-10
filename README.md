# joshuacarmack.com

Personal blog built with [Hugo](https://gohugo.io/) and the [Blowfish](https://blowfish.page/) theme.

## Tech Stack

- **Framework:** Hugo (static site generator)
- **Theme:** Blowfish
- **Hosted at:** [joshuacarmack.com](https://joshuacarmack.com)

## Topics

Posts cover a range of personal projects and interests including:

- Photography
- Homelab and self-hosting
- Meshtastic and amateur radio
- Home automation
- Monitoring and infrastructure

## Local Development

```bash
# Install Hugo (extended)
# https://gohugo.io/installation/

# Clone the repo with submodules (for the theme)
git clone --recurse-submodules <repo-url>

# Start the dev server
hugo server

# Build for production
hugo
```

## Structure

```
content/        # Blog posts and pages (Markdown)
layouts/        # Custom layout overrides
assets/         # Custom CSS/JS
static/         # Static files (images, etc.)
themes/blowfish # Blowfish theme (submodule)
hugo.toml       # Site configuration
```
