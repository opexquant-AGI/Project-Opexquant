# Website Setup & Deployment Checklist
## Print this and check off items as you complete them

---

## PHASE 1: Environment Setup

### Install Required Software
- [ ] Install Git (https://git-scm.com/downloads)
- [ ] Install VS Code (https://code.visualstudio.com/)
- [ ] Install Node.js (https://nodejs.org/) - if using modern frameworks

### Configure Git
- [ ] Run: `git config --global user.name "Your Name"`
- [ ] Run: `git config --global user.email "your@email.com"`
- [ ] Run: `git config --global init.defaultBranch main`
- [ ] Verify: `git config --list`

### Create GitHub Account
- [ ] Go to https://github.com
- [ ] Sign up with email
- [ ] Verify email address
- [ ] Complete profile setup

### Setup Authentication
- [ ] Generate Personal Access Token (Settings → Developer settings)
- [ ] Or setup SSH key for authentication
- [ ] Test connection to GitHub

---

## PHASE 2: Repository Setup

### Create GitHub Repository
- [ ] Click "+" → "New repository"
- [ ] Name: `my-website`
- [ ] Description: (optional)
- [ ] Visibility: Public or Private
- [ ] Check: "Add a README file"
- [ ] Click "Create repository"

### Clone Repository Locally
- [ ] Copy repository URL from GitHub
- [ ] Run: `git clone YOUR_REPO_URL`
- [ ] Navigate to folder: `cd my-website`
- [ ] Verify: `git status`

### Create Project Structure
- [ ] Create folders: `assets/css`, `assets/js`, `assets/images`
- [ ] Create `index.html` file
- [ ] Create `README.md` file
- [ ] Create `.gitignore` file

### Initial Commit
- [ ] Run: `git add .`
- [ ] Run: `git commit -m "Initial commit"`
- [ ] Run: `git push origin main`
- [ ] Verify files appear on GitHub

---

## PHASE 3: VS Code Configuration

### Install Extensions
- [ ] GitLens (Git visualization)
- [ ] GitHub Pull Requests
- [ ] Live Server (local preview)
- [ ] Prettier (code formatting)
- [ ] ESLint (JavaScript linting)

### Configure Settings
- [ ] Open Settings (Ctrl+, or Cmd+,)
- [ ] Enable "Format On Save"
- [ ] Set default formatter to Prettier
- [ ] Configure file exclusions

### Test Local Development
- [ ] Open project in VS Code
- [ ] Start Live Server
- [ ] Verify website displays locally

---

## PHASE 4: Domain & Hosting

### Purchase Domain (GoDaddy)
- [ ] Go to https://godaddy.com
- [ ] Search for desired domain name
- [ ] Add to cart and purchase
- [ ] Access domain from "My Products"

### Choose Hosting Option

#### Option A: GitHub Pages (Free)
- [ ] Go to repository → Settings → Pages
- [ ] Source: Deploy from branch → main
- [ ] Folder: / (root)
- [ ] Save settings
- [ ] Note the provided URL

#### Option B: Netlify (Free Tier)
- [ ] Go to https://netlify.com
- [ ] Sign up with GitHub
- [ ] Click "Add new site" → "Import project"
- [ ] Select GitHub repository
- [ ] Deploy site

#### Option C: Vercel (Free Tier)
- [ ] Go to https://vercel.com
- [ ] Sign up with GitHub
- [ ] Click "Add New..." → "Project"
- [ ] Import GitHub repository
- [ ] Deploy

---

## PHASE 5: Custom Domain Configuration

### Configure DNS (GoDaddy)
- [ ] Go to GoDaddy → My Products → Domains
- [ ] Click domain → Manage DNS
- [ ] Delete existing A records (if any)
- [ ] Add required DNS records for your hosting:

**For GitHub Pages:**
- [ ] A record: @ → 185.199.108.153
- [ ] A record: @ → 185.199.109.153
- [ ] A record: @ → 185.199.110.153
- [ ] A record: @ → 185.199.111.153
- [ ] CNAME: www → YOUR-USERNAME.github.io

**For Netlify:**
- [ ] A record: @ → Netlify IP (from dashboard)
- [ ] CNAME: www → your-site.netlify.app

**For Vercel:**
- [ ] A record: @ → 76.76.21.21
- [ ] CNAME: www → cname.vercel-dns.com

### Configure Custom Domain on Hosting
- [ ] Go to hosting dashboard
- [ ] Add custom domain: `yourdomain.com`
- [ ] Verify domain ownership
- [ ] Enable HTTPS/SSL

### Create CNAME File (GitHub Pages)
- [ ] Create file named `CNAME` (no extension)
- [ ] Add: `www.yourdomain.com`
- [ ] Commit and push to GitHub

### Test Deployment
- [ ] Wait for DNS propagation (up to 48 hours)
- [ ] Visit `https://yourdomain.com`
- [ ] Verify site loads correctly
- [ ] Check HTTPS is working

---

## PHASE 6: Development Workflow

### Daily Workflow
- [ ] Pull latest changes: `git pull origin main`
- [ ] Make changes to files
- [ ] Stage changes: `git add .`
- [ ] Commit: `git commit -m "descriptive message"`
- [ ] Push: `git push origin main`
- [ ] Verify deployment

### Best Practices
- [ ] Write descriptive commit messages
- [ ] Commit frequently
- [ ] Test locally before pushing
- [ ] Keep sensitive data out of repository
- [ ] Regular backups

---

## PHASE 7: Final Verification

### Website Functionality
- [ ] All pages load correctly
- [ ] Images display properly
- [ ] Links work
- [ ] Responsive on mobile
- [ ] Contact forms work (if applicable)

### Security
- [ ] HTTPS enabled
- [ ] No sensitive data in repository
- [ ] .gitignore properly configured
- [ ] Environment variables not committed

### Performance
- [ ] Images optimized
- [ ] CSS/JS minified (if applicable)
- [ ] Fast loading times

---

## TROUBLESHOOTING

### Common Issues
- [ ] Git authentication errors → Check token/SSH key
- [ ] Push rejected → Pull first, then push
- [ ] Site not showing → Check DNS propagation
- [ ] HTTPS not working → Enable in hosting settings
- [ ] Changes not deploying → Check build logs

### Useful Commands
```bash
git status          # Check repository status
git log --oneline   # View recent commits
git remote -v       # Check remote URL
git diff            # See changes
```

---

## CONGRATULATIONS!

Your website is now live at: _________________________

Date deployed: _________________________

---

*Keep this checklist for future reference!*
