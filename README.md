# Design Team Prototype Template

Auto-deploy web prototypes to Azure with Cin7-only authentication.

## 🚀 Quick Start (Design Team)

### Step 1: Create Your Repo
1. Go to [this template](https://github.com/Cin7Americas/design-team-template)
2. Click **"Use this template"** → **"Create a new repository"**
3. Name your repo (e.g., `checkout-redesign`)
4. Keep it in **Cin7Americas** organization

### Step 2: Add GitHub Secrets
Go to your new repo → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

Add these 3 secrets:

| Secret Name | Value |
|-------------|-------|
| `AZURE_CLIENT_ID` | `98c9499d-9293-4484-8bae-c64b1c85ca4e` |
| `AZURE_TENANT_ID` | `19f7ac1d-90c5-49a5-ae3d-3ad4eb14bd1e` |
| `AZURE_SUBSCRIPTION_ID` | `42d37164-473e-4e6e-b05b-4ee43c04e295` |

### Step 3: Request Deployment Access
⚠️ **One-time setup required** - Ask SRE team to enable deployment for your repo:
> "Please enable deployment for `Cin7Americas/<your-repo-name>`"

This is a one-time admin task that allows your repo to deploy to Azure.

### Step 4: Add Your Code & Push
Replace the sample files with your prototype code and push to `main`:
```bash
git add .
git commit -m "My awesome prototype"
git push origin main
```

### Step 5: Access Your Site
After the workflow completes (~1-2 min), your site is at:
```
https://ca-design-prototypes.thankfulwave-36f43db2.australiaeast.azurecontainerapps.io/<your-repo-name>/
```

🔐 **Login required** - Only Cin7 users can access.

---

## 📁 Project Requirements

Your project needs:
- `package.json` with a `build` script
- Build output goes to `dist/` folder

### Included Sample
This template includes a working Vite setup. Just modify `index.html` or add React/Vue/etc.

### Example package.json
```json
{
  "name": "my-prototype",
  "scripts": {
    "dev": "vite",
    "build": "vite build"
  },
  "devDependencies": {
    "vite": "^5.0.0"
  }
}
```

---

## 🔧 Admin Setup (Tony Only)

When a design team member creates a new repo, run this command to enable deployment:

```bash
az ad app federated-credential create \
  --id 98c9499d-9293-4484-8bae-c64b1c85ca4e \
  --parameters '{
    "name": "github-<REPO_NAME>",
    "issuer": "https://token.actions.githubusercontent.com",
    "subject": "repo:Cin7Americas/<REPO_NAME>:ref:refs/heads/main",
    "audiences": ["api://AzureADTokenExchange"]
  }'
```

Replace `<REPO_NAME>` with the actual repo name.

### Existing Federated Credentials
- `cin7_product_webpages`
- `design-team-template`
- `design-team-template-test`

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Build fails | Run `npm run build` locally first |
| "No matching federated identity" | Ask Tony to enable deployment for your repo |
| 401 after login | Wait 1-2 minutes, try again |
| Can't access site | Only Cin7 users can access |
| Files not updating | Check GitHub Actions tab for errors |

---

## 📋 Architecture

| Component | Details |
|-----------|---------|
| **Host** | Azure Container App with nginx |
| **Storage** | Azure File Share (each repo = subfolder) |
| **Auth** | Entra ID (Cin7 tenant only) |
| **CI/CD** | GitHub Actions with OIDC |

**All prototypes:** https://ca-design-prototypes.thankfulwave-36f43db2.australiaeast.azurecontainerapps.io/

---

## 📞 Support

Contact: tony.keung@cin7.com
