# Shopify Theme Development Setup Guide

Store: `r15nui-a3.myshopify.com`

---

# 1. Install Shopify CLI

## macOS (Homebrew)

```bash
brew tap shopify/shopify
brew install shopify-cli
```

Verify installation:

```bash
shopify version
```

---

# 2. Create and Open Local Project Directory

```bash
mkdir shopify-theme
cd shopify-theme
```

---

# 3. Authenticate with Shopify

Login to your Shopify account:

```bash
shopify auth login
```

A browser window will open for authentication.

---

# 4. Verify Store Access

```bash
shopify theme list --store r15nui-a3.myshopify.com
```

Example output:

```text
ID        NAME             ROLE
12345678  Dawn             LIVE
87654321  Dawn Backup      UNPUBLISHED
```

Note the Theme ID of the theme you want to work on.

---

# 5. Pull Theme Code Locally

Pull the live theme:

```bash
shopify theme pull \
  --store r15nui-a3.myshopify.com \
  --theme 12345678
```

Replace `12345678` with your actual theme ID.

This will download the theme files into your local directory.

---

# 6. Initialize Git (Recommended)

```bash
git init
git add .
git commit -m "Initial Shopify theme pull"
```

Optional: Create a remote Git repository and push your code.

---

# 7. Start Local Development

Run a development server:

```bash
shopify theme dev \
  --store r15nui-a3.myshopify.com
```

Shopify will generate a preview URL.

Example:

```text
https://xxxxxxxx.shopifypreview.com
```

Any local file changes will automatically refresh in the preview.

---

# 8. Open Project in VS Code

```bash
code .
```

Useful theme folders:

```text
assets/
config/
layout/
locales/
sections/
snippets/
templates/
```

Common footer files:

```text
sections/footer.liquid
```

or

```text
snippets/footer.liquid
```

---

# 9. Push Changes to Shopify

## Push to Specific Theme

```bash
shopify theme push \
  --store r15nui-a3.myshopify.com \
  --theme 12345678
```

---

## Push Current Changes

```bash
shopify theme push \
  --store r15nui-a3.myshopify.com
```

---

# 10. Recommended Safe Workflow

## Step 1

Pull live theme:

```bash
shopify theme pull \
  --store r15nui-a3.myshopify.com
```

## Step 2

Commit to Git:

```bash
git add .
git commit -m "Initial setup"
```

## Step 3

Create a duplicate theme from Shopify Admin:

```text
Online Store
  → Themes
    → ...
      → Duplicate
```

## Step 4

Find duplicate theme ID:

```bash
shopify theme list \
  --store r15nui-a3.myshopify.com
```

## Step 5

Push changes to duplicate theme:

```bash
shopify theme push \
  --store r15nui-a3.myshopify.com \
  --theme DUPLICATE_THEME_ID
```

## Step 6

Preview and validate all changes.

## Step 7

Publish the duplicate theme from Shopify Admin.

---

# Useful Commands

## List Themes

```bash
shopify theme list \
  --store r15nui-a3.myshopify.com
```

---

## Pull Latest Theme Changes

```bash
shopify theme pull \
  --store r15nui-a3.myshopify.com
```

---

## Pull Specific Theme

```bash
shopify theme pull \
  --store r15nui-a3.myshopify.com \
  --theme THEME_ID
```

---

## Start Local Development

```bash
shopify theme dev \
  --store r15nui-a3.myshopify.com
```

---

## Push Theme

```bash
shopify theme push \
  --store r15nui-a3.myshopify.com
```

---

## Push Specific Theme

```bash
shopify theme push \
  --store r15nui-a3.myshopify.com \
  --theme THEME_ID
```

---

## Check Shopify CLI Version

```bash
shopify version
```

---

## Logout

```bash
shopify auth logout
```

---

# Recovery: Fresh Pull

If local files become inconsistent:

```bash
rm -rf assets config layout locales sections snippets templates
```

Then re-pull:

```bash
shopify theme pull \
  --store r15nui-a3.myshopify.com
```

---

# Typical Daily Workflow

```bash
cd shopify-theme

# Pull latest changes
shopify theme pull --store r15nui-a3.myshopify.com

# Start development
shopify theme dev --store r15nui-a3.myshopify.com

# Make code changes

# Commit changes
git add .
git commit -m "Updated footer for FSSAI compliance"

# Push to Shopify
shopify theme push --store r15nui-a3.myshopify.com --theme THEME_ID
```