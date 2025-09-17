# 🚀 Rezi SDK

A simple, powerful TypeScript/JavaScript SDK for creating beautiful UI components that can be easily integrated into any no-code website tool or custom application.

## ✨ Features

- 🎨 **Beautiful Components**: Pre-designed, responsive UI components
- 🔧 **No Build Required**: Drop-in solution for no-code tools
- 🌈 **Theme Support**: Light/dark themes with custom colors
- 📱 **Mobile Responsive**: Works perfectly on all devices
- 🔒 **TypeScript Support**: Full type safety for developers
- 🎯 **Simple API**: Easy to use, minimal learning curve

## 📦 Installation

### For No-Code Tools (Browser)

1. **Include CSS and JS files:**

```html
<link rel="stylesheet" href="path/to/rezi-sdk.css">
<script src="path/to/rezi-sdk.min.js"></script>
```

2. **Start using components:**

```javascript
// Create a button
const button = ReziSDK.createButton({
    text: 'Click me!',
    variant: 'primary',
    onClick: () => alert('Hello!')
});

// Render it to any container
button.render('#my-container');
```

### For Developers (NPM)

```bash
npm install @rezi/sdk
```

```typescript
import { createButton, showToast } from '@rezi/sdk';
import '@rezi/sdk/styles.css';

const button = createButton({
    text: 'Hello World',
    variant: 'primary',
    onClick: () => showToast({ message: 'Button clicked!', type: 'success' })
});

button.render('#app');
```

## 🎯 Quick Start

Open `example.html` in your browser to see all components in action!

## 📖 API Reference

### Buttons

Create interactive buttons with different styles and behaviors.

```javascript
const button = ReziSDK.createButton({
    text: 'Click me',                    // Required: Button text
    variant: 'primary',                  // 'primary' | 'secondary' | 'outline'
    size: 'md',                         // 'sm' | 'md' | 'lg'
    theme: 'light',                     // 'light' | 'dark' | 'auto'
    disabled: false,                    // Boolean
    onClick: () => console.log('Clicked!'), // Click handler function
    className: 'my-custom-class'        // Additional CSS classes
});

// Render to container
button.render('#container-id');        // By selector
button.render(document.getElementById('container')); // By element

// Update button
button.update({ text: 'New Text', disabled: true });

// Remove button
button.destroy();
```

### Toast Notifications

Show elegant notifications to users.

```javascript
const toast = ReziSDK.showToast({
    message: 'Success! Action completed.',  // Required: Toast message
    type: 'success',                       // 'success' | 'error' | 'warning' | 'info'
    duration: 5000,                        // Auto-hide duration in ms (0 = no auto-hide)
    position: 'top-right',                 // 'top-right' | 'top-left' | 'bottom-right' | 'bottom-left' | 'top-center' | 'bottom-center'
    theme: 'light',                        // 'light' | 'dark' | 'auto'
    className: 'my-toast-class'            // Additional CSS classes
});

// Manually hide toast
toast.hide();
```

### Utilities

Helpful utility functions for common tasks.

```javascript
// Generate unique IDs
const id = ReziSDK.ReziUtils.generateId('my-prefix'); // 'my-prefix-abc123def'

// Email validation
const isValid = ReziSDK.ReziUtils.isValidEmail('user@example.com'); // true

// Copy to clipboard
const success = await ReziSDK.ReziUtils.copyToClipboard('Hello World'); // true/false

// Debounce function calls
const debouncedFn = ReziSDK.ReziUtils.debounce(() => {
    console.log('Debounced!');
}, 500);

// Format currency
const formatted = ReziSDK.ReziUtils.formatCurrency(1234.56); // '$1,234.56'

// Set CSS custom properties
ReziSDK.ReziUtils.setCSSVariable('primary-color', '#ff0000');
```

## 🎨 Customization

### CSS Variables

Customize the look and feel by overriding CSS variables:

```css
:root {
    --rezi-primary: #your-brand-color;
    --rezi-primary-hover: #your-brand-color-dark;
    --rezi-secondary: #your-secondary-color;
    --rezi-success: #your-success-color;
    --rezi-error: #your-error-color;
    --rezi-warning: #your-warning-color;
    --rezi-info: #your-info-color;
    --rezi-radius: 8px;
    --rezi-font-family: 'Your Font', sans-serif;
}
```

### Themes

Components support light and dark themes:

```javascript
// Light theme (default)
const lightButton = ReziSDK.createButton({
    text: 'Light Button',
    theme: 'light'
});

// Dark theme
const darkButton = ReziSDK.createButton({
    text: 'Dark Button',
    theme: 'dark'
});

// Auto theme (follows system preference)
const autoButton = ReziSDK.createButton({
    text: 'Auto Theme Button',
    theme: 'auto'
});
```

### Custom CSS Classes

Add your own CSS classes to any component:

```javascript
const customButton = ReziSDK.createButton({
    text: 'Custom Button',
    className: 'my-special-button pulse-animation'
});
```

```css
.my-special-button {
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    transform: translateY(-2px);
}

.pulse-animation {
    animation: pulse 2s infinite;
}

@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.05); }
    100% { transform: scale(1); }
}
```

## 🔧 Advanced Usage

### Integration with No-Code Tools

#### Webflow
1. Add CSS link to your site's head code
2. Add JS script to your site's head code
3. Add custom code blocks where you want components
4. Use the ReziSDK global object

#### WordPress (Elementor/Divi)
1. Upload CSS and JS files to your media library
2. Include them in your theme or via plugins
3. Add HTML widgets with custom JavaScript
4. Use ReziSDK to create components

#### Framer
1. Add CSS and JS as external resources
2. Use Code Components to create SDK components
3. Pass props to configure SDK components

#### Bubble.io
1. Add CSS and JS files as external resources
2. Use HTML elements with JavaScript
3. Create reusable SDK component templates

### Form Integration

Create forms that integrate with any backend:

```javascript
// Example: Contact form that posts to your API
const contactForm = ReziSDK.createForm({
    fields: [
        {
            id: 'name',
            label: 'Name',
            type: 'text',
            required: true,
            placeholder: 'Enter your name'
        },
        {
            id: 'email',
            label: 'Email',
            type: 'email',
            required: true,
            placeholder: 'your@email.com'
        },
        {
            id: 'message',
            label: 'Message',
            type: 'textarea',
            required: true,
            placeholder: 'Your message here...'
        }
    ],
    onSubmit: async (data) => {
        try {
            const response = await fetch('/api/contact', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(data)
            });
            
            if (response.ok) {
                ReziSDK.showToast({
                    message: 'Message sent successfully!',
                    type: 'success'
                });
            }
        } catch (error) {
            ReziSDK.showToast({
                message: 'Failed to send message. Please try again.',
                type: 'error'
            });
        }
    }
});

contactForm.render('#contact-form');
```

## 🚀 Performance

The SDK is optimized for performance:

- **Lightweight**: ~15KB minified and gzipped
- **No Dependencies**: Pure vanilla JavaScript
- **Lazy Loading**: Components load only when needed
- **Efficient DOM**: Minimal DOM manipulation
- **CSS Optimized**: Efficient animations and transitions

## 🆘 Troubleshooting

### Common Issues

**Q: Components don't appear styled**
A: Make sure you've included the CSS file before the JavaScript file.

**Q: ReziSDK is undefined**
A: Ensure the JavaScript file has loaded completely before using the SDK.

**Q: Toasts appear behind other elements**
A: The SDK uses z-index: 2000 for toasts. Adjust if needed.

**Q: Buttons don't respond to clicks**
A: Check that your onClick handlers are properly defined functions.

### Browser Support

- ✅ Chrome 70+
- ✅ Firefox 65+
- ✅ Safari 12+
- ✅ Edge 79+
- ✅ iOS Safari 12+
- ✅ Android Chrome 70+

## 📝 License

MIT License - see LICENSE file for details.

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📞 Support

- 📧 Email: support@rezi.io
- 🐛 Issues: [GitHub Issues](https://github.com/your-repo/issues)
- 📖 Docs: [Full Documentation](https://docs.rezi.io/sdk)

---

Made with ❤️ by the Rezi Team
