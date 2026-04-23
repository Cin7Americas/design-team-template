# Design Team Prototype Template

Auto-deploy web prototypes to Azure with Cin7-only authentication.

## Quick Start

1. **Create repo from this template** → Click "Use this template" button above
2. **Add GitHub Secrets** (Settings → Secrets and variables → Actions):

   | Secret | Value |
   |--------|-------|
   | \`AZURE_CLIENT_ID\` | \`98c9499d-9293-4484-8bae-c64b1c85ca4e\` |
   | \`AZURE_TENANT_ID\` | \`19f7ac1d-90c5-49a5-ae3d-3ad4eb14bd1e\` |
   | \`AZURE_SUBSCRIPTION_ID\` | \`42d37164-473e-4e6e-b05b-4ee43c04e295\` |

3. **Add your code** and push to \`main\`

## What Happens

On every push to \`main\`:
- Builds your project
- Uploads to the shared prototype server

**Your URL:**
\`\`\`
https://ca-design-prototypes.thankfulwave-36f43db2.australiaeast.azurecontainerapps.io/<your-repo-name>/
\`\`\`

Example: \`my-dashboard\` repo → \`/my-dashboard/\`

All prototypes listed at the [root URL](https://ca-design-prototypes.thankfulwave-36f43db2.australiaeast.azurecontainerapps.io/).

## Requirements

Your project needs:
- \`package.json\` with \`build\` script
- Build output to \`dist/\` folder

### Example package.json

\`\`\`json
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
\`\`\`

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Build fails | Run \`npm run build\` locally first |
| 401 after login | Wait 1-2 minutes, try again |
| Can't access site | Only Cin7 users can access |

## Support

Contact: tony.keung@cin7.com
