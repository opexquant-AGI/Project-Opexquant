# Complete Website Setup & Deployment Guide
## From Zero to Deployed Website

---

## Table of Contents
1. [Prerequisites & Environment Setup](#1-prerequisites--environment-setup)
2. [GitHub Repository Setup](#2-github-repository-setup)
3. [VS Code Configuration](#3-vs-code-configuration)
4. [Connecting Local Project to GitHub](#4-connecting-local-project-to-github)
5. [GoDaddy Domain Configuration](#5-godaddy-domain-configuration)
6. [Deployment Options](#6-deployment-options)
7. [Git Workflow Best Practices](#7-git-workflow-best-practices)
8. [.gitignore Recommendations](#8-gitignore-recommendations)
9. [Git Commands Cheat Sheet](#9-git-commands-cheat-sheet)
10. [Troubleshooting](#10-troubleshooting)

---

## 1. Prerequisites & Environment Setup

### 1.1 Required Software Installation

#### Install Git
**Windows:**
```bash
# Download from https://git-scm.com/download/win
# Or use Chocolatey
choco install git
```

**Mac:**
```bash
# Using Homebrew
brew install git

# Or download from https://git-scm.com/download/mac
```

**Linux:**
```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install git

# Fedora
sudo dnf install git
```

#### Install VS Code
Download from: https://code.visualstudio.com/

**Recommended VS Code Extensions:**
- GitLens (enhanced Git visualization)
- GitHub Pull Requests and Issues
- Live Server (for local preview)
- Prettier (code formatting)
- ESLint (JavaScript linting)

#### Install Node.js (for modern web projects)
```bash
# Download from https://nodejs.org/ (LTS version recommended)
# Verify installation
node --version
npm --version
```

### 1.2 Configure Git Identity

```bash
# Set your name (will appear in commits)
git config --global user.name "Your Name"

# Set your email (use same email as GitHub account)
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Enable colored output
git config --global color.ui auto

# Verify configuration
git config --list
```

### 1.3 Create GitHub Account
1. Go to https://github.com
2. Click "Sign up"
3. Enter email, create password, choose username
4. Verify your email address
5. Complete the onboarding process

---

## 2. GitHub Repository Setup

### 2.1 Create a New Repository (Web Interface)

1. **Log in to GitHub** at https://github.com
2. **Click the "+" icon** in top-right corner
3. **Select "New repository"**
4. **Fill in repository details:**
   - **Repository name:** `my-website` (use lowercase, hyphens for spaces)
   - **Description:** (optional) "My personal portfolio website"
   - **Visibility:** 
     - Public: Anyone can see (free)
     - Private: Only you and collaborators (free)
   - **Initialize with:**
     - [x] Add a README file
     - [ ] Add .gitignore (we'll add this manually)
     - [ ] Choose a license (optional)
5. **Click "Create repository"**

### 2.2 Repository Settings for Deployment

#### For GitHub Pages:
1. Go to repository → **Settings** tab
2. Click **Pages** in left sidebar
3. Under "Source", select:
   - Deploy from a branch
   - Branch: `main`
   - Folder: `/ (root)` or `/docs`
4. Click **Save**

#### Enable GitHub Actions (for automated deployment):
1. Go to **Settings** → **Actions** → **General**
2. Under "Actions permissions", select:
   - "Allow all actions and reusable workflows"
3. Click **Save**

---

## 3. VS Code Configuration

### 3.1 Open VS Code and Install Extensions

1. **Open VS Code**
2. **Press `Ctrl+Shift+X`** (Windows/Linux) or `Cmd+Shift+X` (Mac)
3. **Search and install:**
   - `GitLens` - Git visualization
   - `GitHub Pull Requests` - GitHub integration
   - `Live Server` - Local development server
   - `Prettier - Code: formatter` - Code formatting

### 3.2 Configure VS Code Settings

**Open Settings:** `Ctrl+,` (Windows/Linux) or `Cmd+,` (Mac)

**Add these settings (JSON format):**
```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "git.enableSmartCommit": true,
  "git.confirmSync": false,
  "git.autofetch": true,
  "files.exclude": {
    "**/.git": true,
    "**/node_modules": true,
    "**/.DS_Store": true
  },
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  }
}
```

### 3.3 Configure VS Code Terminal

**Set default terminal:**
- Windows: `Ctrl+Shift+P` → "Terminal: Select Default Profile" → "Git Bash" or "PowerShell"
- Mac/Linux: Uses default shell (usually bash or zsh)

**Open integrated terminal:** `Ctrl+`` (backtick)

---

## 4. Connecting Local Project to GitHub

### 4.1 Method 1: Clone Existing Repository (Recommended for Beginners)

```bash
# Navigate to where you want to store projects
cd Documents/Projects

# Clone the repository (replace with your URL)
git clone https://github.com/YOUR-USERNAME/my-website.git

# Navigate into the project folder
cd my-website

# Check status
git status
```

### 4.2 Method 2: Initialize Local Repository First

```bash
# Create project folder
mkdir my-website
cd my-website

# Initialize Git repository
git init

# Create initial files
echo "# My Website" > README.md

# Create basic HTML structure
mkdir -p assets/css assets/js assets/images

# Create index.html
cat > index.html << 'EOF'
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Website</title>
    <link rel="stylesheet" href="assets/css/style.css">
</head>
<body>
    <h1>Welcome to My Website</h1>
    <script src="assets/js/main.js"></script>
</body>
</html>
EOF

# Create CSS file
cat > assets/css/style.css << 'EOF'
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    padding: 20px;
}
EOF

# Create JS file
cat > assets/js/main.js << 'EOF'
console.log('Website loaded successfully!');
EOF

# Add all files to staging
git add .

# Create first commit
git commit -m "Initial commit: Basic website structure"

# Connect to GitHub repository (replace with your URL)
git remote add origin https://github.com/YOUR-USERNAME/my-website.git

# Push to GitHub
git push -u origin main
```

### 4.3 Authenticate with GitHub

#### Option A: HTTPS with Personal Access Token (Recommended)

1. **Generate Personal Access Token:**
   - Go to GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
   - Click "Generate new token (classic)"
   - Select scopes: `repo` (full control of private repositories)
   - Click "Generate token"
   - **Copy and save the token immediately!**

2. **Use token when prompted for password:**
   ```bash
   git push origin main
   # When asked for password, use your Personal Access Token instead
   ```

3. **Cache credentials (optional):**
   ```bash
   # Cache for 1 hour
   git config --global credential.helper cache
   
   # Or store permanently (less secure)
   git config --global credential.helper store
   ```

#### Option B: SSH (More Secure for Regular Use)

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard
# Mac:
pbcopy < ~/.ssh/id_ed25519.pub
# Windows (Git Bash):
cat ~/.ssh/id_ed25519.pub | clip
# Linux:
cat ~/.ssh/id_ed25519.pub

# Add to GitHub:
# 1. Go to GitHub → Settings → SSH and GPG keys
# 2. Click "New SSH key"
# 3. Paste your key and save

# Test connection
ssh -T git@github.com

# Update remote URL to use SSH
git remote set-url origin git@github.com:YOUR-USERNAME/my-website.git
```

---

## 5. GoDaddy Domain Configuration

### 5.1 Purchase Domain from GoDaddy

1. Go to https://www.godaddy.com
2. Search for your desired domain name
3. Add to cart and complete purchase
4. Access your domain from "My Products" → "Domains"

### 5.2 Option A: Using GoDaddy Hosting (cPanel)

**If you purchased GoDaddy web hosting:**

1. **Log in to GoDaddy** → "My Products"
2. **Find your hosting plan** → Click "Manage"
3. **Access cPanel** (control panel)
4. **Upload your website:**
   - Use File Manager in cPanel, OR
   - Use FTP client (FileZilla) with credentials from cPanel
5. **Upload files to:** `public_html/` folder
6. **Your site will be live at:** `yourdomain.com`

**Using FTP (FileZilla):**
```
Host: ftp.yourdomain.com (or IP from cPanel)
Username: Your cPanel username
Password: Your cPanel password
Port: 21
```

### 5.3 Option B: GitHub Pages with Custom GoDaddy Domain

#### Step 1: Configure GitHub Repository

1. In your repository, go to **Settings** → **Pages**
2. Under "Custom domain", enter: `www.yourdomain.com`
3. Click **Save**
4. Check "Enforce HTTPS" (recommended)

#### Step 2: Configure GoDaddy DNS

1. **Log in to GoDaddy** → "My Products" → "Domains"
2. **Click on your domain** → "Manage DNS"
3. **Delete existing A records** (if any)
4. **Add GitHub Pages A records:**

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | 185.199.108.153 | 600 seconds |
| A | @ | 185.199.109.153 | 600 seconds |
| A | @ | 185.199.110.153 | 600 seconds |
| A | @ | 185.199.111.153 | 600 seconds |
| CNAME | www | YOUR-USERNAME.github.io | 600 seconds |

5. **Save changes**

#### Step 3: Create CNAME File in Repository

```bash
# In your local repository
echo "www.yourdomain.com" > CNAME

# Add and commit
git add CNAME
git commit -m "Add custom domain configuration"
git push origin main
```

**Or create manually:**
1. Create file named `CNAME` (no extension)
2. Contents: `www.yourdomain.com`
3. Place in root of repository

#### Step 4: Wait for DNS Propagation
- Can take 24-48 hours (usually much faster)
- Check status: https://www.whatsmydns.net/

### 5.4 Option C: Netlify with GoDaddy Domain

#### Step 1: Deploy to Netlify

1. Go to https://www.netlify.com
2. Sign up with GitHub account
3. Click "Add new site" → "Import an existing project"
4. Select GitHub and authorize
5. Choose your repository
6. Click "Deploy site"

#### Step 2: Configure Custom Domain on Netlify

1. In Netlify dashboard, go to **Site settings** → **Domain management**
2. Click "Add custom domain"
3. Enter: `yourdomain.com`
4. Click "Verify" → "Add domain"

#### Step 3: Configure GoDaddy DNS

1. **GoDaddy** → "My Products" → "Domains" → "Manage DNS"
2. **Add records from Netlify:**

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | Netlify IP (from dashboard) | 600 seconds |
| CNAME | www | your-site-name.netlify.app | 600 seconds |

#### Step 4: Enable HTTPS on Netlify
1. Netlify dashboard → **Domain management**
2. Click "HTTPS" → "Verify DNS configuration"
3. Netlify will automatically provision SSL certificate

### 5.5 Option D: Vercel with GoDaddy Domain

#### Step 1: Deploy to Vercel

1. Go to https://vercel.com
2. Sign up with GitHub
3. Click "Add New..." → "Project"
4. Import your GitHub repository
5. Click "Deploy"

#### Step 2: Add Custom Domain

1. Vercel dashboard → Select your project
2. Go to **Settings** → **Domains**
3. Enter: `yourdomain.com`
4. Click "Add"

#### Step 3: Configure GoDaddy DNS

**Vercel will provide DNS records. Typically:**

| Type | Name | Value | TTL |
|------|------|-------|-----|
| A | @ | 76.76.21.21 | 600 seconds |
| CNAME | www | cname.vercel-dns.com | 600 seconds |

---

## 6. Deployment Options

### 6.1 GitHub Pages (Free, Simple)

**Best for:** Static HTML/CSS/JS websites, portfolios, documentation

**Pros:**
- Free hosting
- Automatic deployment from Git
- Custom domain support
- HTTPS included

**Cons:**
- Static sites only (no server-side code)
- Public repositories only (for free tier)
- 1GB storage limit

**Setup:**
```bash
# Ensure your repository has index.html at root
# Push to main branch
# Enable in Settings → Pages
```

### 6.2 Netlify (Free Tier Available)

**Best for:** Static sites, JAMstack, form handling, serverless functions

**Pros:**
- Free tier with generous limits
- Automatic builds from Git
- Form handling without backend
- Edge network (fast global CDN)
- Branch previews

**Setup:**
1. Connect GitHub repo to Netlify
2. Build settings (for most static sites):
   - Build command: (leave empty for HTML/CSS/JS)
   - Publish directory: `/` (or your build output folder)

### 6.3 Vercel (Free Tier Available)

**Best for:** React, Next.js, Vue, modern frontend frameworks

**Pros:**
- Optimized for React/Next.js
- Automatic preview deployments
- Serverless functions
- Excellent performance

**Setup:**
1. Import GitHub repository
2. Vercel auto-detects framework
3. Deploy automatically

### 6.4 Traditional Hosting (GoDaddy, Bluehost, etc.)

**Best for:** PHP, WordPress, databases, full server control

**Setup via FTP:**
```bash
# Using command line FTP (or use FileZilla)
ftp yourdomain.com

# Login with credentials
# Upload files
put index.html
put -r assets/
```

---

## 7. Git Workflow Best Practices

### 7.1 Basic Workflow

```bash
# 1. Check current status
git status

# 2. Pull latest changes (before starting work)
git pull origin main

# 3. Make your changes to files

# 4. Stage changes
git add filename.html          # Stage specific file
git add .                      # Stage all changes

# 5. Commit with descriptive message
git commit -m "Add contact form with validation"

# 6. Push to GitHub
git push origin main
```

### 7.2 Feature Branch Workflow (Recommended for Team Projects)

```bash
# Create and switch to new feature branch
git checkout -b feature/contact-page

# Make changes and commit
git add .
git commit -m "Add contact page with form"

# Push branch to GitHub
git push -u origin feature/contact-page

# Create Pull Request on GitHub
# After review, merge on GitHub

# Switch back to main and update
git checkout main
git pull origin main

# Delete local branch
git branch -d feature/contact-page
```

### 7.3 Commit Message Best Practices

**Format:**
```
<type>: <subject>

<body> (optional)

<footer> (optional)
```

**Types:**
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Formatting, missing semicolons, etc.
- `refactor:` Code restructuring
- `test:` Adding tests
- `chore:` Maintenance tasks

**Examples:**
```bash
git commit -m "feat: add responsive navigation menu"
git commit -m "fix: correct contact form validation"
git commit -m "docs: update README with setup instructions"
```

---

## 8. .gitignore Recommendations

### 8.1 Basic Website Project .gitignore

Create a file named `.gitignore` in your project root:

```gitignore
# Operating System Files
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# Editor Files
.vscode/
.idea/
*.swp
*.swo
*~

# Dependencies
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
package-lock.json
yarn.lock

# Build Outputs
dist/
build/
.out/
.next/

# Environment Variables
.env
.env.local
.env.development
.env.production
.env.test

# Logs
logs/
*.log

# Temporary Files
tmp/
temp/
*.tmp

# Cache
.cache/
.parcel-cache/

# Testing
coverage/
.nyc_output/

# Optional: Uncomment if using specific tools
# .sass-cache/
# *.css.map
# *.js.map
```

### 8.2 Framework-Specific Additions

**For React projects, add:**
```gitignore
# React
build/
.env.local
.env.development.local
.env.test.local
.env.production.local
```

**For Python/Django projects, add:**
```gitignore
# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
env/
venv/
ENV/
*.sqlite3
```

**For PHP projects, add:**
```gitignore
# PHP
vendor/
composer.lock
.env
config.php
```

---

## 9. Git Commands Cheat Sheet

### Repository Setup
```bash
git init                          # Initialize new repository
git clone <url>                   # Clone existing repository
git remote -v                     # View remote URLs
git remote add origin <url>       # Add remote repository
git remote set-url origin <url>   # Change remote URL
```

### Basic Operations
```bash
git status                        # Check repository status
git add <file>                    # Stage specific file
git add .                         # Stage all changes
git commit -m "message"           # Commit staged changes
git push origin <branch>          # Push to remote
git pull origin <branch>          # Pull from remote
git fetch                         # Download remote changes (don't merge)
```

### Branching
```bash
git branch                        # List branches
git branch <name>                 # Create new branch
git checkout <branch>             # Switch to branch
git checkout -b <name>            # Create and switch to branch
git merge <branch>                # Merge branch into current
git branch -d <name>              # Delete branch
git branch -D <name>              # Force delete branch
```

### Viewing History
```bash
git log                           # View commit history
git log --oneline                 # Compact history view
git log --graph --oneline         # Visual branch history
git show <commit>                 # Show specific commit
git diff                          # Show unstaged changes
git diff --staged                 # Show staged changes
```

### Undoing Changes
```bash
git restore <file>                # Discard file changes
git restore --staged <file>       # Unstage file
git reset HEAD~1                  # Undo last commit (keep changes)
git reset --hard HEAD~1           # Undo last commit (discard changes)
git revert <commit>               # Create commit that undoes specific commit
```

### Stashing
```bash
git stash                         # Stash changes temporarily
git stash list                    # List stashes
git stash pop                     # Apply and remove stash
git stash apply                   # Apply stash (keep in list)
git stash drop                    # Delete stash
```

### Tags
```bash
git tag                           # List tags
git tag <name>                    # Create lightweight tag
git tag -a <name> -m "message"    # Create annotated tag
git push origin <tag>             # Push tag to remote
git push origin --tags            # Push all tags
```

---

## 10. Environment Setup Checklist

### Initial Setup Checklist

- [ ] Install Git
- [ ] Install VS Code
- [ ] Install Node.js (if needed)
- [ ] Create GitHub account
- [ ] Configure Git identity
- [ ] Set up SSH key or Personal Access Token

### Project Setup Checklist

- [ ] Create GitHub repository
- [ ] Clone repository locally
- [ ] Create project folder structure
- [ ] Create initial files (index.html, README.md)
- [ ] Create .gitignore file
- [ ] Make initial commit
- [ ] Push to GitHub

### Development Checklist

- [ ] Install VS Code extensions
- [ ] Configure VS Code settings
- [ ] Set up Live Server for local preview
- [ ] Configure code formatter (Prettier)

### Deployment Checklist

- [ ] Purchase domain (GoDaddy or other)
- [ ] Choose hosting platform (GitHub Pages/Netlify/Vercel)
- [ ] Configure DNS settings
- [ ] Set up custom domain
- [ ] Enable HTTPS
- [ ] Test website is accessible

### Security Checklist

- [ ] Add sensitive files to .gitignore
- [ ] Never commit API keys or passwords
- [ ] Use environment variables for secrets
- [ ] Enable HTTPS on custom domain
- [ ] Regularly update dependencies

---

## Quick Start Summary

For those who want to get started immediately:

```bash
# 1. Install Git and create GitHub account

# 2. Configure Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 3. Create GitHub repository (via web interface)

# 4. Clone repository
git clone https://github.com/YOUR-USERNAME/my-website.git
cd my-website

# 5. Create your website files
# (Create index.html, CSS, JS files)

# 6. Commit and push
git add .
git commit -m "Initial commit"
git push origin main

# 7. Enable GitHub Pages in repository settings
# 8. Configure custom domain (optional)
# 9. Your site is live!
```

---

## Additional Resources

- **Git Documentation:** https://git-scm.com/doc
- **GitHub Guides:** https://guides.github.com
- **GitHub Pages:** https://pages.github.com
- **Netlify Docs:** https://docs.netlify.com
- **Vercel Docs:** https://vercel.com/docs
- **GoDaddy Help:** https://www.godaddy.com/help

---

*Guide created for beginners to deploy their first website. Last updated: 2024*
