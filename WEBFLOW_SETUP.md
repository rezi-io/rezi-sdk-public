<!-- @format -->

## Use CDN

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

# Rezi Resume Import SDK - Getting Started

### Simple Auto-initialization

The easiest way to add resume upload to your website:

```html
<!DOCTYPE html>
<html>
	<head>
		<link
			rel="stylesheet"
			href="https://cdn.jsdelivr.net/npm/@rezi/sdk@latest/rezi-sdk.css"
		/>
	</head>
	<body>
		<!-- Resume Drop Zone -->
		<div
			data-resume-dropzone
			data-redirect-url="https://your-app.com/signup"
			style="border: 2px dashed #ccc; padding: 40px; text-align: center; cursor: pointer;"
		>
			<div id="replace-with-loader">📄</div>
			<h3>Drop your resume here</h3>
			<p>or click to browse (PDF, DOCX only)</p>
		</div>

		<script src="https://cdn.jsdelivr.net/npm/@rezi/sdk@latest/rezi-sdk.min.js"></script>
	</body>
</html>
```

The SDK will automatically:

1. Detect the `data-resume-dropzone` element
2. Set up drag & drop functionality
3. Handle file validation and upload
4. Show loading states
5. Redirect to your app with the resume token

### HTML Attributes

| Attribute                  | Description                                        | Required                 |
| -------------------------- | -------------------------------------------------- | ------------------------ |
| `data-resume-dropzone`     | Marks the element as a drop zone                   | ✅ Yes                   |
| `data-redirect-url`        | URL to redirect after successful upload            | ✅ Yes                   |
| `data-dev`                 | Enable development mode (uses dev API endpoints)   | ❌ No (False by default) |
| `id="replace-with-loader"` | Element to hide during loading (e.g., upload icon) | ✅ Yes                   |

## Manual Initialization

For more control over the upload process:

```html
<div id="my-upload-zone">
	<div id="upload-icon">📄</div>
	<h3>Upload Resume</h3>
</div>

<script>
	const resumeUpload = new ReziSDK.ResumeImport({
		dropZoneSelector: '#my-upload-zone',
		isDev: false,
		maxFileSize: 10 * 1024 * 1024, // 10MB
		allowedTypes: [
			'application/pdf',
			'application/vnd.openxmlformats-officedocument.wordprocessingml.document',
		],
		redirectUrl: 'https://your-app.com/signup',

		// Event callbacks
		onUploadStart: () => {
			console.log('Upload started');
		},

		onUploadSuccess: (token) => {
			console.log('Upload successful, token:', token);
			// Handle success (e.g., redirect, show message)
		},

		onUploadError: (error) => {
			console.error('Upload failed:', error.message);
			// Handle error (e.g., show error message)
		},
	});
</script>
```

## Configuration Options

```typescript
interface ResumeImportConfig {
	dropZoneSelector: string; // CSS selector for drop zone element
	isDev?: boolean; // Use development API endpoints
	maxFileSize?: number; // Max file size in bytes (default: 10MB)
	allowedTypes?: string[]; // Allowed MIME types
	redirectUrl?: string; // URL to redirect after success
	onUploadStart?: () => void; // Called when upload starts
	onUploadSuccess?: (token: string) => void; // Called on success
	onUploadError?: (error: Error) => void; // Called on error
}
```

## Styling

The SDK comes with default styles. You can customize the appearance:

### CSS Variables

```css
:root {
	--rezi-primary: #4285f4; /* Primary color */
	--rezi-primary-hover: #2563eb; /* Primary hover color */
	--rezi-error: #ef4444; /* Error color */
	--rezi-success: #10b981; /* Success color */
	--rezi-border: #e5e7eb; /* Border color */
	--rezi-radius: 0.375rem; /* Border radius */
	--rezi-font-family: system-ui, sans-serif; /* Font family */
}
```

### Custom Styling

```css
/* Customize drop zone appearance */
[data-resume-dropzone] {
	border: 2px dashed #ddd;
	border-radius: 12px;
	padding: 40px;
	text-align: center;
	background: #fafafa;
	transition: all 0.3s ease;
}

[data-resume-dropzone]:hover {
	border-color: #4285f4;
	background: #f0f4ff;
	transform: translateY(-2px);
}

/* Dragover state */
[data-resume-dropzone].dragover {
	border-color: #4285f4 !important;
	background-color: rgba(66, 133, 244, 0.05) !important;
}

/* Loading state */
[data-resume-dropzone].loading {
	opacity: 0.8;
	pointer-events: none;
}

/* Custom loader styling */
.resume-loader .spinner {
	width: 40px;
	height: 40px;
	border: 3px solid #e3f2fd;
	border-top: 3px solid #4285f4;
	border-radius: 50%;
	animation: spin 1s linear infinite;
}
```

## Advanced Usage

### File Validation

The SDK automatically validates files, but you can customize validation:

```javascript
const resumeUpload = new ReziSDK.ResumeImport({
	dropZoneSelector: '#upload-zone',
	maxFileSize: 5 * 1024 * 1024, // 5MB limit
	allowedTypes: ['application/pdf'], // PDF only

	onUploadError: (error) => {
		if (error.message.includes('file size')) {
			alert('File too large! Please upload a file smaller than 5MB.');
		} else if (error.message.includes('PDF')) {
			alert('Please upload a PDF file only.');
		} else {
			alert('Upload failed: ' + error.message);
		}
	},
});
```

### Custom Success Handling

```javascript
const resumeUpload = new ReziSDK.ResumeImport({
	dropZoneSelector: '#upload-zone',

	onUploadSuccess: (token) => {
		// Store token
		localStorage.setItem('resume_token', token);

		// Show success message
		document.getElementById('success-message').style.display = 'block';

		// Redirect after delay
		setTimeout(() => {
			window.location.href = '/dashboard?token=' + token;
		}, 2000);
	},
});
```

### Development Mode

For testing with development API endpoints:

```html
<div
	data-resume-dropzone
	data-dev
	data-redirect-url="http://localhost:3000/signup"
>
	Upload Resume (Dev Mode)
</div>
```

Or programmatically:

```javascript
const resumeUpload = new ReziSDK.ResumeImport({
	dropZoneSelector: '#upload-zone',
	isDev: true,
	redirectUrl: 'http://localhost:3000/signup',
});
```

## API Reference

### ResumeImport Class

#### Constructor

```typescript
new ResumeImport(config: ResumeImportConfig)
```

#### Methods

```typescript
// Destroy the component and clean up event listeners
destroy(): void

// Update configuration
updateConfig(newConfig: Partial<ResumeImportConfig>): void

// Get the drop zone element
getDropZone(): HTMLElement | null

// Check if upload is in progress
isUploading(): boolean
```

### Utility Functions

```typescript
// Validate a resume file
ReziSDK.validateResumeFile(file: File, maxSize?: number, allowedTypes?: string[])

// Check if file is a Rezi file
ReziSDK.isReziFile(file: File): Promise<boolean>

// Format file size for display
ReziSDK.formatFileSize(bytes: number): string

// Session storage helpers
ReziSDK.setSessionToken(token: string): void
ReziSDK.getSessionToken(): string | null
```

## Error Handling

The SDK provides comprehensive error handling:

```javascript
const resumeUpload = new ReziSDK.ResumeImport({
	dropZoneSelector: '#upload-zone',

	onUploadError: (error) => {
		console.error('Upload error:', error);

		// Common error types:
		if (error.message.includes('No file selected')) {
			// Handle no file error
		} else if (error.message.includes('file size')) {
			// Handle file size error
		} else if (error.message.includes('PDF or DOCX')) {
			// Handle file type error
		} else if (error.message.includes('HTTP error')) {
			// Handle API error
		} else {
			// Handle other errors
		}
	},
});
```
