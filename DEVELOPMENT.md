<!-- @format -->

# Development Guide

This repository contains the **built and distributed assets** for the Rezi SDK.
It serves as the public CDN distribution point and should **not** be edited directly.

## 📁 Repository Structure

```
rezi-sdk-public/
├── package.json         # Distribution package metadata
├── rezi-sdk.min.js     # 🚫 Built JS (DO NOT EDIT)
├── rezi-sdk.css        # 🚫 Built CSS (DO NOT EDIT)
├── README.md           # Public documentation
├── WEBFLOW_SETUP.md    # Integration guide
└── DEVELOPMENT.md      # This file
```

## 🚨 Important: DO NOT EDIT BUILT FILES

The files `rezi-sdk.min.js` and `rezi-sdk.css` are **automatically generated** and will be overwritten. Any manual changes will be lost.

## 🔄 Development Workflow

### 1. Source Code Location

The actual source code lives in:

```
rezi-mono-repo/libs/sdk/
```

### 2. Making Changes

1. **Navigate to the monorepo:**

   ```bash
   cd path/to/rezi-mono-repo
   ```

2. **Make your changes in:**

   ```
   libs/sdk/src/           # Source TypeScript/JavaScript
   libs/sdk/styles/        # Source CSS/SCSS
   libs/sdk/tests/         # Tests
   ```

3. **Test your changes:**
   ```bash
   # From monorepo root or libs/sdk
   npm test
   npm run dev    # If available
   ```

### 3. Building and Deployment

After making changes in the monorepo:

1. **Run the deployment script:**

   ```bash
   ./scripts/deploy-sdk.sh  # Adjust path as needed
   ```

2. **Commit and push to rezi-sdk-public:**
   ```bash
   cd path/to/rezi-sdk-public
   git add .
   git commit -m "feat: update SDK to v1.x.x"
   git push origin main
   ```

## 📦 Release Process

### CDN Distribution

Once pushed to GitHub, the files are automatically available via:

- **jsDelivr:** `https://cdn.jsdelivr.net/gh/rezi-io/rezi-sdk-public@latest/rezi-sdk.min.js`
- **GitHub Raw:** `https://raw.githubusercontent.com/rezi-io/rezi-sdk-public/main/rezi-sdk.min.js`

## 🧪 Testing Changes

### Local Testing

1. **Build the SDK in monorepo**
2. **Copy files to a test directory:**
   ```bash
   cp dist/rezi-sdk.min.js /path/to/test/
   cp dist/rezi-sdk.css /path/to/test/
   ```
3. **Test in a local HTML file:**
   ```html
   <!DOCTYPE html>
   <html>
   	<head>
   		<link rel="stylesheet" href="./rezi-sdk.css" />
   	</head>
   	<body>
   		<div data-resume-dropzone data-redirect-url="http://localhost:3000">
   			Test Upload
   		</div>
   		<script src="./rezi-sdk.min.js"></script>
   	</body>
   </html>
   ```

### Integration Testing

Test with the actual CDN URLs in development:

```html
<link
	rel="stylesheet"
	href="https://cdn.jsdelivr.net/gh/rezi-io/rezi-sdk-public@main/rezi-sdk.css"
/>
<script src="https://cdn.jsdelivr.net/gh/rezi-io/rezi-sdk-public@main/rezi-sdk.min.js"></script>
```

## 📝 Documentation Updates

### When to Update Documentation

- New features added
- API changes
- Configuration options changed
- New examples needed

### Files to Update

- `README.md` - Main public documentation
- `WEBFLOW_SETUP.md` - Integration guides
- `package.json` - Version and metadata

## 🚀 Deployment Checklist

Before deploying:

- [ ] Changes tested in monorepo
- [ ] All tests passing
- [ ] Build successful
- [ ] Version numbers updated
- [ ] Documentation updated
- [ ] Examples tested

After deploying:

- [ ] Files updated in rezi-sdk-public
- [ ] Committed and pushed
- [ ] Tagged if new version
- [ ] CDN cache cleared (if needed)
- [ ] Integration tested

## 🔍 Troubleshooting

### Common Issues

**"My changes aren't showing up"**

- Ensure you're editing files in the monorepo, not this repository
- Check that the build script ran successfully
- Verify the deployment script copied files correctly

**"CDN still serving old version"**

- CDNs may cache files for up to 24 hours
- Use commit-specific URLs for immediate updates:
  ```html
  <script src="https://cdn.jsdelivr.net/gh/rezi-io/rezi-sdk-public@COMMIT_HASH/rezi-sdk.min.js"></script>
  ```

---

## Quick Reference

| Task             | Location                  | Command              |
| ---------------- | ------------------------- | -------------------- |
| Edit source code | `rezi-mono-repo/libs/sdk` | `code .`             |
| Build SDK        | `rezi-mono-repo/libs/sdk` | `npm run build`      |
| Deploy to public | `rezi-mono-repo`          | `npm run deploy:sdk` |
| Update version   | Both repos                | `npm version patch`  |
| Test locally     | Test directory            | Open HTML file       |

Remember: **Never edit `rezi-sdk.min.js` or `rezi-sdk.css` directly!**
