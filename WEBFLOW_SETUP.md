<!-- @format -->

# 🚀 Webflow Setup Instructions

## Step 1: Create GitHub Repository

1. Go to GitHub and create a new **public** repository called `rezi-sdk-public`
2. Upload all files from this directory to that repository
3. Enable GitHub Pages in repository settings

## Step 2: Add to Webflow

Add this to your Webflow site's **Custom Code** > **Head**:

```html
<!-- Rezi SDK CSS -->
<link
	rel="stylesheet"
	href="https://yourusername.github.io/rezi-sdk-public/rezi-sdk.css"
/>

<!-- Rezi SDK JavaScript -->
<script src="https://yourusername.github.io/rezi-sdk-public/rezi-sdk.min.js"></script>
```

Replace `yourusername` with your actual GitHub username.

## Step 3: Use in Webflow

Add an Embed element anywhere on your page:

```html
<div id="my-button"></div>

<script>
	const button = ReziSDK.createButton({
		text: 'Click Me!',
		variant: 'primary',
		onClick: () => {
			ReziSDK.showToast({
				message: 'Hello from Rezi SDK!',
				type: 'success',
			});
		},
	});

	button.render('#my-button');
</script>
```

## Alternative: Use jsDelivr CDN (Recommended)

After publishing to GitHub, you can use jsDelivr for faster, global delivery:

### Latest Version (Development)

```html
<link
	rel="stylesheet"
	href="https://cdn.jsdelivr.net/gh/rezi-io/rezi-sdk-public/rezi-sdk.css"
/>
<script src="https://cdn.jsdelivr.net/gh/rezi-io/rezi-sdk-public/rezi-sdk.min.js"></script>
```

### Specific Commit (Production)

```html
<link
	rel="stylesheet"
	href="https://cdn.jsdelivr.net/gh/rezi-io/rezi-sdk-public@ebc9721/rezi-sdk.css"
/>
<script src="https://cdn.jsdelivr.net/gh/rezi-io/rezi-sdk-public@ebc9721/rezi-sdk.min.js"></script>
```

**Benefits:** Global CDN, faster loading, automatic caching, version control
