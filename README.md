# Design Team Prototype Template

Auto-deploy web prototypes to Azure with Cin7-only authentication.

## Quick Start

1. **Create repo from this template** → Click "Use this template" button above
2. **Add GitHub Secrets** (Settings → Secrets and variables → Actions):

   | Secret | Value |
   |--------|-------|
   | `AZURE_CLIENT_ID` | `98c9499d-9293-4484-8bae-c64b1c85ca4e` |
   | `AZURE_TENANT_ID` | `19f7ac1d-90c5-49a5-ae3d-3ad4eb14bd1e` |
   | `AZURE_SUBSCRIPTION_ID` | `42d37164-473e-4e6e-b05b-4ee43c04e295` |
   | `AAD_CLIENT_SECRET` | *(Get from Tony or password manager)* |

3. **Add your code** and push to `main`

## What Happens

On every push to `main`:
- Creates Azure Static Web App (if doesn't exist)
- Configures Cin7 authentication automatically
- Deploys your site

Your URL: `https://<random-name>.azurestaticapps.net`

## Requirements

Your project needs:
- `package.json` with `build` script
- Build output to `dist/` folder

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

### Supported Frameworks

Works with any framework that builds to `dist/`:
- Vite (React, Vue, Svelte)
- Create React App (change `output_location` to `build`)
- Plain HTML/CSS/JS (no build needed - remove build step)

## Customization

### Different output folder

Edit `.github/workflows/deploy.yml`:
```yaml
output_location: "build"  # Change from "dist"
```

### No build step

For static HTML, edit workflow to skip build:
```yaml
skip_app_build: true
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Build fails | Run `npm run build` locally first |
| 401 after login | Wait 1-2 minutes, try again |
| Can't access site | Only Cin7 users can access |

## Support

Contact: tony.keung@cin7.com
