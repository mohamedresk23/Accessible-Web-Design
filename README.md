# Accessible Web Design for Front-End Developers

A comprehensive guide to creating inclusive and accessible web experiences that work for everyone.

## Table of Contents

- [Introduction to Web Accessibility](#introduction-to-web-accessibility)
- [WCAG Guidelines Overview](#wcag-guidelines-overview)
- [Semantic HTML Foundation](#semantic-html-foundation)
- [Keyboard Navigation](#keyboard-navigation)
- [Screen Reader Support](#screen-reader-support)
- [Color and Contrast](#color-and-contrast)
- [Typography for Accessibility](#typography-for-accessibility)
- [Images and Media](#images-and-media)
- [Forms Accessibility](#forms-accessibility)
- [Interactive Components](#interactive-components)
- [Testing and Tools](#testing-and-tools)
- [Common Pitfalls](#common-pitfalls)
- [Resources and Further Learning](#resources-and-further-learning)

## Introduction to Web Accessibility

Web accessibility means designing and developing websites that people with disabilities can use effectively. This includes users with:
- **Visual impairments** (blindness, low vision, color blindness)
- **Hearing impairments** (deafness, hard of hearing)
- **Motor impairments** (limited fine motor control, paralysis)
- **Cognitive impairments** (dyslexia, ADHD, memory issues)

### Why Accessibility Matters

- **Legal compliance**: Many countries require accessible websites
- **Inclusive design**: Serves 15% of the global population with disabilities
- **Better UX for everyone**: Accessibility improvements benefit all users
- **Business benefits**: Larger audience, better SEO, improved usability

### The Curb-Cut Effect

```html
<!-- Example: Captions help everyone, not just deaf users -->
<video controls>
  <source src="video.mp4" type="video/mp4">
  <track kind="captions" src="captions.vtt" srclang="en" label="English">
  Your browser does not support the video tag.
</video>
```

**Why it matters**: Accessibility features designed for people with disabilities often benefit everyone.

## WCAG Guidelines Overview

The Web Content Accessibility Guidelines (WCAG) 2.1 are organized around four principles:

### 1. Perceivable
Information must be presentable in ways users can perceive.

```css
/* High contrast for better visibility */
:root {
  --text-primary: #212529;
  --text-secondary: #495057;
  --background: #ffffff;
  --link-color: #0056b3;
}

/* Minimum 4.5:1 contrast ratio for normal text */
.text-content {
  color: var(--text-primary);
  background-color: var(--background);
}

/* 3:1 for large text (18px+ or 14px+ bold) */
.large-text {
  font-size: 1.25rem;
  color: var(--text-secondary);
  background-color: var(--background);
}
```

### 2. Operable
Interface components must be operable by all users.

```css
/* Focus indicators for keyboard navigation */
button:focus,
a:focus,
input:focus,
select:focus,
textarea:focus {
  outline: 2px solid #005fcc;
  outline-offset: 2px;
}

/* Ensure clickable areas are at least 44x44px */
.touch-target {
  min-height: 44px;
  min-width: 44px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
```

### 3. Understandable
Information and UI operation must be understandable.

```html
<!-- Clear language and instructions -->
<form>
  <fieldset>
    <legend>Contact Information</legend>
    <div class="form-group">
      <label for="email">
        Email Address
        <span class="required" aria-label="required">*</span>
      </label>
      <input 
        type="email" 
        id="email" 
        name="email" 
        required 
        aria-describedby="email-help email-error"
        autocomplete="email"
      >
      <div id="email-help" class="help-text">
        We'll use this to send you updates about your order.
      </div>
      <div id="email-error" class="error-text" aria-live="polite"></div>
    </div>
  </fieldset>
</form>
```

### 4. Robust
Content must be robust enough for various assistive technologies.

```html
<!-- Valid, semantic HTML that works across technologies -->
<article role="article" aria-labelledby="article-title">
  <header>
    <h1 id="article-title">Understanding Web Accessibility</h1>
    <p class="byline">
      By <span class="author">Jane Developer</span> on 
      <time datetime="2024-01-15">January 15, 2024</time>
    </p>
  </header>
  <main>
    <p>Content goes here...</p>
  </main>
</article>
```

**Why it matters**: Following WCAG ensures your site works for the widest possible audience.

## Semantic HTML Foundation

### Using Proper HTML Elements

```html
<!-- ❌ Bad: Generic divs and spans -->
<div class="header">
  <div class="nav">
    <div class="nav-item">Home</div>
    <div class="nav-item">About</div>
  </div>
</div>
<div class="main-content">
  <div class="article">
    <div class="title">Article Title</div>
    <div class="content">Article content...</div>
  </div>
</div>

<!-- ✅ Good: Semantic HTML -->
<header role="banner">
  <nav role="navigation" aria-label="Main navigation">
    <ul>
      <li><a href="/" aria-current="page">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
  </nav>
</header>
<main role="main">
  <article>
    <h1>Article Title</h1>
    <p>Article content...</p>
  </article>
</main>
```

### Document Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title - Site Name</title>
</head>
<body>
  <!-- Skip to content link -->
  <a href="#main-content" class="skip-link">Skip to main content</a>
  
  <header role="banner">
    <!-- Site header content -->
  </header>
  
  <nav role="navigation" aria-label="Main navigation">
    <!-- Navigation menu -->
  </nav>
  
  <main id="main-content" role="main">
    <!-- Main page content -->
  </main>
  
  <aside role="complementary">
    <!-- Sidebar content -->
  </aside>
  
  <footer role="contentinfo">
    <!-- Site footer -->
  </footer>
</body>
</html>
```

### Heading Hierarchy

```html
<!-- ✅ Proper heading structure -->
<main>
  <h1>Main Page Title</h1>
  
  <section>
    <h2>Section Title</h2>
    <p>Section content...</p>
    
    <h3>Subsection Title</h3>
    <p>Subsection content...</p>
    
    <h3>Another Subsection</h3>
    <p>More content...</p>
  </section>
  
  <section>
    <h2>Another Section</h2>
    <p>Section content...</p>
  </section>
</main>
```

**Why it matters**: Semantic HTML provides structure and meaning that assistive technologies can understand.

## Keyboard Navigation

### Focus Management

```css
/* Visible focus indicators */
:focus {
  outline: 2px solid #005fcc;
  outline-offset: 2px;
}

/* Custom focus styles */
.button:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(0, 95, 204, 0.3);
  background-color: #0056b3;
}

/* Skip link styles */
.skip-link {
  position: absolute;
  top: -40px;
  left: 6px;
  background: #000;
  color: #fff;
  padding: 8px;
  text-decoration: none;
  border-radius: 4px;
  z-index: 1000;
}

.skip-link:focus {
  top: 6px;
}
```

### Tab Order and Navigation

```html
<!-- Logical tab order -->
<form>
  <div>
    <label for="first-name">First Name</label>
    <input type="text" id="first-name" tabindex="1">
  </div>
  
  <div>
    <label for="last-name">Last Name</label>
    <input type="text" id="last-name" tabindex="2">
  </div>
  
  <div>
    <label for="email">Email</label>
    <input type="email" id="email" tabindex="3">
  </div>
  
  <button type="submit" tabindex="4">Submit</button>
  <!-- Note: Usually avoid explicit tabindex, let natural order work -->
</form>
```

### Keyboard Event Handling

```javascript
// Handle keyboard interactions for custom components
class AccessibleDropdown {
  constructor(element) {
    this.dropdown = element;
    this.trigger = element.querySelector('.dropdown-trigger');
    this.menu = element.querySelector('.dropdown-menu');
    this.items = element.querySelectorAll('.dropdown-item');
    this.currentIndex = -1;
    
    this.bindEvents();
  }
  
  bindEvents() {
    this.trigger.addEventListener('click', (e) => this.toggle(e));
    this.trigger.addEventListener('keydown', (e) => this.handleTriggerKeydown(e));
    
    this.items.forEach((item, index) => {
      item.addEventListener('keydown', (e) => this.handleItemKeydown(e, index));
    });
  }
  
  handleTriggerKeydown(event) {
    switch (event.key) {
      case 'Enter':
      case ' ':
      case 'ArrowDown':
        event.preventDefault();
        this.open();
        this.focusItem(0);
        break;
      case 'ArrowUp':
        event.preventDefault();
        this.open();
        this.focusItem(this.items.length - 1);
        break;
    }
  }
  
  handleItemKeydown(event, index) {
    switch (event.key) {
      case 'ArrowDown':
        event.preventDefault();
        this.focusItem(index + 1);
        break;
      case 'ArrowUp':
        event.preventDefault();
        this.focusItem(index - 1);
        break;
      case 'Escape':
        this.close();
        this.trigger.focus();
        break;
      case 'Tab':
        this.close();
        break;
    }
  }
  
  focusItem(index) {
    if (index < 0) index = this.items.length - 1;
    if (index >= this.items.length) index = 0;
    
    this.currentIndex = index;
    this.items[index].focus();
  }
}
```

**Why it matters**: Many users navigate entirely by keyboard due to motor impairments or personal preference.

## Screen Reader Support

### ARIA Labels and Descriptions

```html
<!-- Descriptive labels -->
<button aria-label="Close dialog">×</button>

<input 
  type="search" 
  aria-label="Search products"
  placeholder="Enter product name"
>

<!-- Additional descriptions -->
<input 
  type="password" 
  id="password"
  aria-describedby="password-help"
>
<div id="password-help">
  Password must be at least 8 characters long and contain a number.
</div>

<!-- Complex widgets -->
<div 
  role="tabpanel" 
  aria-labelledby="tab1"
  aria-describedby="panel1-desc"
>
  <h2 id="tab1">Account Settings</h2>
  <p id="panel1-desc">Manage your account preferences and privacy settings.</p>
  <!-- Panel content -->
</div>
```

### Live Regions

```html
<!-- Status updates -->
<div aria-live="polite" aria-atomic="true" class="sr-only" id="status">
  <!-- Dynamic content announcements -->
</div>

<div aria-live="assertive" aria-atomic="true" class="sr-only" id="alerts">
  <!-- Urgent announcements -->
</div>
```

```javascript
// Announce dynamic content changes
function announceToScreenReader(message, priority = 'polite') {
  const liveRegion = document.getElementById(priority === 'assertive' ? 'alerts' : 'status');
  liveRegion.textContent = message;
  
  // Clear after announcement
  setTimeout(() => {
    liveRegion.textContent = '';
  }, 1000);
}

// Usage examples
announceToScreenReader('Form submitted successfully');
announceToScreenReader('Error: Please fix the highlighted fields', 'assertive');
```

### Screen Reader Only Content

```css
/* Screen reader only text */
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

/* Show on focus for keyboard users */
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
  white-space: normal;
}
```

```html
<!-- Examples of screen reader only content -->
<button>
  <span class="sr-only">Add to cart: </span>
  <span aria-hidden="true">🛒</span>
  Product Name
</button>

<nav aria-label="Pagination">
  <a href="/page/1">
    <span class="sr-only">Go to page </span>1
  </a>
  <span aria-current="page" class="sr-only">Current page, </span>
  <span>2</span>
</nav>
```

**Why it matters**: Screen readers need additional context and announcements that visual users get automatically.

## Color and Contrast

### Color Contrast Requirements

```css
/* WCAG AA Standards */
:root {
  /* Normal text: minimum 4.5:1 ratio */
  --text-on-white: #212529;      /* 16.75:1 ratio */
  --text-secondary: #495057;     /* 9.5:1 ratio */
  
  /* Large text: minimum 3:1 ratio */
  --large-text-light: #6c757d;   /* 4.7:1 ratio */
  
  /* Interactive elements */
  --link-default: #0056b3;       /* 4.77:1 ratio */
  --link-hover: #004085;         /* 7.2:1 ratio */
  
  /* Status colors with sufficient contrast */
  --success-bg: #d4edda;
  --success-text: #155724;       /* 4.5:1 on success-bg */
  --error-bg: #f8d7da;
  --error-text: #721c24;         /* 4.5:1 on error-bg */
}
```

### Color-Blind Friendly Design

```css
/* Don't rely on color alone */
.status-indicator {
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-weight: 500;
}

/* Success state */
.status-success {
  background-color: var(--success-bg);
  color: var(--success-text);
  border-left: 4px solid #28a745;
}

.status-success::before {
  content: "✓ ";
  font-weight: bold;
}

/* Error state */
.status-error {
  background-color: var(--error-bg);
  color: var(--error-text);
  border-left: 4px solid #dc3545;
}

.status-error::before {
  content: "⚠ ";
  font-weight: bold;
}
```

### Testing Color Contrast

```javascript
// Function to calculate contrast ratio
function getContrastRatio(color1, color2) {
  const l1 = getLuminance(color1);
  const l2 = getLuminance(color2);
  const lighter = Math.max(l1, l2);
  const darker = Math.min(l1, l2);
  
  return (lighter + 0.05) / (darker + 0.05);
}

function getLuminance(color) {
  // Convert hex to RGB
  const r = parseInt(color.substr(1, 2), 16) / 255;
  const g = parseInt(color.substr(3, 2), 16) / 255;
  const b = parseInt(color.substr(5, 2), 16) / 255;
  
  // Calculate relative luminance
  const rsRGB = r <= 0.03928 ? r / 12.92 : Math.pow((r + 0.055) / 1.055, 2.4);
  const gsRGB = g <= 0.03928 ? g / 12.92 : Math.pow((g + 0.055) / 1.055, 2.4);
  const bsRGB = b <= 0.03928 ? b / 12.92 : Math.pow((b + 0.055) / 1.055, 2.4);
  
  return 0.2126 * rsRGB + 0.7152 * gsRGB + 0.0722 * bsRGB;
}

// Usage
console.log(getContrastRatio('#000000', '#ffffff')); // 21:1 (perfect)
console.log(getContrastRatio('#767676', '#ffffff')); // 4.54:1 (AA compliant)
```

**Why it matters**: Sufficient color contrast ensures content is readable for users with visual impairments.

## Typography for Accessibility

### Readable Font Choices

```css
/* Accessible font stacks */
body {
  font-family: 
    -apple-system, 
    BlinkMacSystemFont, 
    'Segoe UI', 
    'Roboto', 
    'Helvetica Neue', 
    Arial, 
    sans-serif;
  
  /* Optimal reading settings */
  font-size: 1rem;        /* 16px minimum */
  line-height: 1.5;       /* 1.5x spacing minimum */
  letter-spacing: 0.05em; /* Slight letter spacing */
}

/* Headings with proper spacing */
h1, h2, h3, h4, h5, h6 {
  line-height: 1.2;
  margin-bottom: 0.5em;
  font-weight: 600;
}

/* Paragraph spacing */
p {
  margin-bottom: 1em;
  max-width: 70ch; /* Optimal line length */
}
```

### Responsive Typography

```css
/* Fluid typography that scales with viewport */
:root {
  --font-size-sm: clamp(0.875rem, 2vw, 1rem);
  --font-size-base: clamp(1rem, 2.5vw, 1.125rem);
  --font-size-lg: clamp(1.125rem, 3vw, 1.25rem);
  --font-size-xl: clamp(1.25rem, 4vw, 1.5rem);
  --font-size-2xl: clamp(1.5rem, 5vw, 2rem);
}

/* Respect user preferences */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

/* High contrast mode support */
@media (prefers-contrast: high) {
  :root {
    --text-primary: #000000;
    --background: #ffffff;
    --border-color: #000000;
  }
  
  button, input, select, textarea {
    border: 2px solid var(--border-color);
  }
}
```

**Why it matters**: Readable typography reduces cognitive load and helps users with dyslexia and other reading difficulties.

## Images and Media

### Alternative Text

```html
<!-- Informative images -->
<img 
  src="chart.png" 
  alt="Sales increased 25% from January to March 2024, with the highest peak in February"
>

<!-- Decorative images -->
<img src="decorative-border.png" alt="" role="presentation">

<!-- Complex images -->
<figure>
  <img 
    src="complex-chart.png" 
    alt="Quarterly sales data visualization"
    aria-describedby="chart-description"
  >
  <figcaption id="chart-description">
    Sales data showing Q1 at $50k, Q2 at $75k, Q3 at $60k, and Q4 at $85k. 
    Q4 shows the highest growth with a 41% increase from Q3.
  </figcaption>
</figure>

<!-- Images with text -->
<img 
  src="save-button.png" 
  alt="Save document"
>

<!-- Better: Use actual text when possible -->
<button class="save-btn">
  <svg aria-hidden="true"><!-- icon --></svg>
  Save Document
</button>
```

### Video and Audio Accessibility

```html
<!-- Video with captions and descriptions -->
<video controls preload="metadata">
  <source src="video.mp4" type="video/mp4">
  <source src="video.webm" type="video/webm">
  
  <!-- Captions for dialogue -->
  <track 
    kind="captions" 
    src="captions-en.vtt" 
    srclang="en" 
    label="English Captions"
    default
  >
  
  <!-- Audio descriptions for visual content -->
  <track 
    kind="descriptions" 
    src="descriptions-en.vtt" 
    srclang="en" 
    label="English Descriptions"
  >
  
  <!-- Subtitles in other languages -->
  <track 
    kind="subtitles" 
    src="subtitles-es.vtt" 
    srclang="es" 
    label="Español"
  >
  
  <p>
    Your browser doesn't support video. 
    <a href="video.mp4">Download the video</a> instead.
  </p>
</video>

<!-- Audio with transcript -->
<figure>
  <audio controls>
    <source src="podcast.mp3" type="audio/mpeg">
    <source src="podcast.ogg" type="audio/ogg">
    Your browser doesn't support audio.
  </audio>
  <figcaption>
    <p>Podcast Episode 1: Introduction to Web Accessibility</p>
    <details>
      <summary>View Transcript</summary>
      <div class="transcript">
        <p><strong>Host:</strong> Welcome to our podcast about web accessibility...</p>
        <!-- Full transcript content -->
      </div>
    </details>
  </figcaption>
</figure>
```

### Icon Accessibility

```html
<!-- Decorative icons -->
<button>
  <svg aria-hidden="true" focusable="false">
    <use href="#icon-heart"></use>
  </svg>
  Add to Favorites
</button>

<!-- Informative icons -->
<span class="status">
  <svg aria-label="Warning" role="img">
    <use href="#icon-warning"></use>
  </svg>
  <span class="sr-only">Warning: </span>
  Check your internet connection
</span>

<!-- Icon-only buttons -->
<button aria-label="Close dialog">
  <svg aria-hidden="true" focusable="false">
    <use href="#icon-close"></use>
  </svg>
</button>
```

**Why it matters**: Alternative text and media descriptions make visual content accessible to users with visual impairments.

## Forms Accessibility

### Form Labels and Structure

```html
<form novalidate>
  <fieldset>
    <legend>Personal Information</legend>
    
    <!-- Required field with proper labeling -->
    <div class="form-group">
      <label for="full-name">
        Full Name
        <span class="required" aria-label="required">*</span>
      </label>
      <input 
        type="text" 
        id="full-name" 
        name="fullName"
        required
        aria-describedby="name-error"
        aria-invalid="false"
        autocomplete="name"
      >
      <div id="name-error" class="error-message" role="alert"></div>
    </div>
    
    <!-- Email with help text -->
    <div class="form-group">
      <label for="email">Email Address</label>
      <input 
        type="email" 
        id="email" 
        name="email"
        aria-describedby="email-help"
        autocomplete="email"
      >
      <div id="email-help" class="help-text">
        We'll use this to send you updates about your account.
      </div>
    </div>
    
    <!-- Password with requirements -->
    <div class="form-group">
      <label for="password">Password</label>
      <input 
        type="password" 
        id="password" 
        name="password"
        aria-describedby="password-requirements"
        autocomplete="new-password"
      >
      <div id="password-requirements" class="help-text">
        <p>Password must contain:</p>
        <ul>
          <li>At least 8 characters</li>
          <li>One uppercase letter</li>
          <li>One number</li>
        </ul>
      </div>
    </div>
  </fieldset>
  
  <!-- Radio button group -->
  <fieldset>
    <legend>Preferred Contact Method</legend>
    <div class="radio-group">
      <label>
        <input type="radio" name="contact" value="email" checked>
        Email
      </label>
      <label>
        <input type="radio" name="contact" value="phone">
        Phone
      </label>
      <label>
        <input type="radio" name="contact" value="mail">
        Mail
      </label>
    </div>
  </fieldset>
  
  <button type="submit">Create Account</button>
</form>
```

### Form Validation

```javascript
class AccessibleFormValidator {
  constructor(form) {
    this.form = form;
    this.errorSummary = null;
    this.setupValidation();
  }
  
  setupValidation() {
    this.form.addEventListener('submit', (e) => this.handleSubmit(e));
    
    // Real-time validation for better UX
    this.form.querySelectorAll('input, select, textarea').forEach(field => {
      field.addEventListener('blur', (e) => this.validateField(e.target));
      field.addEventListener('input', (e) => this.clearFieldError(e.target));
    });
  }
  
  handleSubmit(event) {
    event.preventDefault();
    
    const errors = this.validateForm();
    
    if (errors.length > 0) {
      this.displayErrors(errors);
      this.focusFirstError();
    } else {
      this.submitForm();
    }
  }
  
  validateField(field) {
    const errors = [];
    
    if (field.hasAttribute('required') && !field.value.trim()) {
      errors.push({
        field: field,
        message: `${this.getFieldLabel(field)} is required`
      });
    }
    
    if (field.type === 'email' && field.value && !this.isValidEmail(field.value)) {
      errors.push({
        field: field,
        message: 'Please enter a valid email address'
      });
    }
    
    this.updateFieldError(field, errors[0]);
    return errors.length === 0;
  }
  
  updateFieldError(field, error) {
    const errorElement = document.getElementById(field.getAttribute('aria-describedby'));
    
    if (error) {
      field.setAttribute('aria-invalid', 'true');
      if (errorElement) {
        errorElement.textContent = error.message;
        errorElement.setAttribute('role', 'alert');
      }
    } else {
      field.setAttribute('aria-invalid', 'false');
      if (errorElement) {
        errorElement.textContent = '';
        errorElement.removeAttribute('role');
      }
    }
  }
  
  displayErrors(errors) {
    // Create or update error summary
    let summary = document.getElementById('error-summary');
    if (!summary) {
      summary = document.createElement('div');
      summary.id = 'error-summary';
      summary.className = 'error-summary';
      summary.setAttribute('role', 'alert');
      summary.setAttribute('aria-labelledby', 'error-summary-title');
      this.form.insertBefore(summary, this.form.firstChild);
    }
    
    summary.innerHTML = `
      <h2 id="error-summary-title">Please fix the following errors:</h2>
      <ul>
        ${errors.map(error => `
          <li>
            <a href="#${error.field.id}">
              ${error.message}
            </a>
          </li>
        `).join('')}
      </ul>
    `;
    
    // Announce to screen readers
    summary.focus();
  }
  
  focusFirstError() {
    const firstErrorField = this.form.querySelector('[aria-invalid="true"]');
    if (firstErrorField) {
      firstErrorField.focus();
    }
  }
}

// Initialize form validation
document.addEventListener('DOMContentLoaded', () => {
  const forms = document.querySelectorAll('form[data-validate]');
  forms.forEach(form => new AccessibleFormValidator(form));
});
```

**Why it matters**: Proper form accessibility ensures all users can successfully complete tasks and receive clear feedback.

## Interactive Components

### Modal Dialogs

```html
<!-- Modal HTML -->
<div 
  class="modal" 
  id="example-modal"
  role="dialog"
  aria-labelledby="modal-title"
  aria-describedby="modal-description"
  aria-modal="true"
  style="display: none;"
>
  <div class="modal-overlay" aria-hidden="true"></div>
  <div class="modal-container">
    <header class="modal-header">
      <h1 id="modal-title">Confirm Action</h1>
      <button 
        type="button" 
        class="modal-close"
        aria-label="Close dialog"
        data-dismiss="modal"
      >
        <span aria-hidden="true">&times;</span>
      </button>
    </header>
    
    <div class="modal-body">
      <p id="modal-description">
        Are you sure you want to delete this item? This action cannot be undone.
      </p>
    </div>
    
    <footer class="modal-footer">
      <button type="button" class="btn btn-secondary" data-dismiss="modal">
        Cancel
      </button>
      <button type="button" class="btn btn-danger" id="confirm-delete">
        Delete Item
      </button>
    </footer>
  </div>
</div>
```

```javascript
class AccessibleModal {
  constructor(modalElement) {
    this.modal = modalElement;
    this.overlay = modalElement.querySelector('.modal-overlay');
    this.container = modalElement.querySelector('.modal-container');
    this.closeButtons = modalElement.querySelectorAll('[data-dismiss="modal"]');
    this.focusableElements = null;
    this.previouslyFocusedElement = null;
    
    this.bindEvents();
  }
  
  bindEvents() {
    // Close button clicks
    this.closeButtons.forEach(button => {
      button.addEventListener('click', () => this.close());
    });
    
    // Overlay click to close
    this.overlay.addEventListener('click', () => this.close());
    
    // Escape key to close
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape' && this.isOpen()) {
        this.close();
      }
    });
    
    // Trap focus within modal
    this.modal.addEventListener('keydown', (e) => {
      if (e.key === 'Tab') {
        this.trapFocus(e);
      }
    });
  }
  
  open() {
    // Store currently focused element
    this.previouslyFocusedElement = document.activeElement;
    
    // Show modal
    this.modal.style.display = 'flex';
    document.body.classList.add('modal-open');
    
    // Get focusable elements
    this.focusableElements = this.getFocusableElements();
    
    // Focus first element or modal container
    if (this.focusableElements.length > 0) {
      this.focusableElements[0].focus();
    } else {
      this.container.focus();
    }
    
    // Announce to screen readers
    this.announceModalOpen();
  }
  
  close() {
    if (!this.isOpen()) return;
    
    // Hide modal
    this.modal.style.display = 'none';
    document.body.classList.remove('modal-open');
    
    // Return focus to previously focused element
    if (this.previouslyFocusedElement) {
      this.previouslyFocusedElement.focus();
    }
    
    // Announce to screen readers
    this.announceModalClose();
  }
  
  isOpen() {
    return this.modal.style.display !== 'none';
  }
  
  getFocusableElements() {
    const selector = 'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])';
    return Array.from(this.container.querySelectorAll(selector))
      .filter(element => !element.hasAttribute('disabled'));
  }
  
  trapFocus(event) {
    if (this.focusableElements.length === 0) return;
    
    const firstElement = this.focusableElements[0];
    const lastElement = this.focusableElements[this.focusableElements.length - 1];
    
    if (event.shiftKey) {
      // Shift + Tab
      if (document.activeElement === firstElement) {
        event.preventDefault();
        lastElement.focus();
      }
    } else {
      // Tab
      if (document.activeElement === lastElement) {
        event.preventDefault();
        firstElement.focus();
      }
    }
  }
  
  announceModalOpen() {
    const announcement = document.createElement('div');
    announcement.setAttribute('aria-live', 'assertive');
    announcement.setAttribute('aria-atomic', 'true');
    announcement.className = 'sr-only';
    announcement.textContent = 'Dialog opened';
    document.body.appendChild(announcement);
    
    setTimeout(() => {
      document.body.removeChild(announcement);
    }, 1000);
  }
  
  announceModalClose() {
    const announcement = document.createElement('div');
    announcement.setAttribute('aria-live', 'assertive');
    announcement.setAttribute('aria-atomic', 'true');
    announcement.className = 'sr-only';
    announcement.textContent = 'Dialog closed';
    document.body.appendChild(announcement);
    
    setTimeout(() => {
      document.body.removeChild(announcement);
    }, 1000);
  }
}

// Initialize modals
document.addEventListener('DOMContentLoaded', () => {
  const modals = document.querySelectorAll('.modal');
  modals.forEach(modal => new AccessibleModal(modal));
});
```

### Accordion Component

```html
<div class="accordion" role="tablist" aria-multiselectable="true">
  <div class="accordion-item">
    <h3>
      <button
        class="accordion-trigger"
        aria-expanded="false"
        aria-controls="panel1"
        id="accordion1"
        role="tab"
      >
        <span>What is web accessibility?</span>
        <span class="accordion-icon" aria-hidden="true">+</span>
      </button>
    </h3>
    <div
      class="accordion-panel"
      id="panel1"
      role="tabpanel"
      aria-labelledby="accordion1"
      aria-hidden="true"
    >
      <div class="accordion-content">
        <p>Web accessibility means designing and developing websites that people with disabilities can use effectively...</p>
      </div>
    </div>
  </div>
  
  <div class="accordion-item">
    <h3>
      <button
        class="accordion-trigger"
        aria-expanded="false"
        aria-controls="panel2"
        id="accordion2"
        role="tab"
      >
        <span>Why is accessibility important?</span>
        <span class="accordion-icon" aria-hidden="true">+</span>
      </button>
    </h3>
    <div
      class="accordion-panel"
      id="panel2"
      role="tabpanel"
      aria-labelledby="accordion2"
      aria-hidden="true"
    >
      <div class="accordion-content">
        <p>Accessibility is important because it ensures equal access to information and functionality...</p>
      </div>
    </div>
  </div>
</div>
```

```css
/* Accordion styles */
.accordion {
  border: 1px solid #ddd;
  border-radius: 4px;
  overflow: hidden;
}

.accordion-item {
  border-bottom: 1px solid #ddd;
}

.accordion-item:last-child {
  border-bottom: none;
}

.accordion-trigger {
  width: 100%;
  padding: 1rem;
  background: #f8f9fa;
  border: none;
  text-align: left;
  font-size: 1rem;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.accordion-trigger:hover {
  background: #e9ecef;
}

.accordion-trigger:focus {
  outline: 2px solid #0056b3;
  outline-offset: -2px;
}

.accordion-trigger[aria-expanded="true"] {
  background: #e9ecef;
}

.accordion-trigger[aria-expanded="true"] .accordion-icon {
  transform: rotate(45deg);
}

.accordion-icon {
  font-size: 1.2rem;
  font-weight: bold;
  transition: transform 0.2s ease;
}

.accordion-panel {
  overflow: hidden;
  transition: max-height 0.3s ease;
}

.accordion-panel[aria-hidden="true"] {
  max-height: 0;
}

.accordion-panel[aria-hidden="false"] {
  max-height: 500px; /* Adjust based on content */
}

.accordion-content {
  padding: 1rem;
}
```

### Dropdown Menu

```html
<div class="dropdown">
  <button
    class="dropdown-trigger"
    aria-expanded="false"
    aria-haspopup="true"
    aria-controls="dropdown-menu"
    id="menu-button"
  >
    Options
    <span class="dropdown-arrow" aria-hidden="true">▼</span>
  </button>
  
  <ul
    class="dropdown-menu"
    role="menu"
    aria-labelledby="menu-button"
    id="dropdown-menu"
    style="display: none;"
  >
    <li role="none">
      <a href="#" role="menuitem">Profile Settings</a>
    </li>
    <li role="none">
      <a href="#" role="menuitem">Account Preferences</a>
    </li>
    <li role="separator" class="dropdown-separator"></li>
    <li role="none">
      <button type="button" role="menuitem">Sign Out</button>
    </li>
  </ul>
</div>
```

**Why it matters**: Interactive components need proper ARIA attributes and keyboard support for screen reader users.

## Testing and Tools

### Automated Testing Tools

```javascript
// Example using axe-core for automated accessibility testing
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

describe('Accessibility Tests', () => {
  test('should not have accessibility violations', async () => {
    const { container } = render(<YourComponent />);
    const results = await axe(container);
    expect(results).toHaveNoViolations();
  });
  
  test('should have proper focus management', () => {
    const { getByRole } = render(<YourModal />);
    const openButton = getByRole('button', { name: /open modal/i });
    
    fireEvent.click(openButton);
    
    const modal = getByRole('dialog');
    expect(modal).toBeInTheDocument();
    expect(modal).toHaveFocus();
  });
});
```

### Manual Testing Checklist

```markdown
## Keyboard Testing Checklist

- [ ] All interactive elements are focusable
- [ ] Focus order is logical and follows visual layout
- [ ] Focus indicators are clearly visible
- [ ] All functionality available via mouse is available via keyboard
- [ ] No keyboard traps (except modals with proper escape)
- [ ] Skip links work and are properly hidden/shown

## Screen Reader Testing

- [ ] Content structure makes sense when read linearly
- [ ] Headings create a logical outline
- [ ] Form labels are properly associated
- [ ] Images have appropriate alt text
- [ ] Complex content has additional descriptions
- [ ] Dynamic content changes are announced

## Color and Contrast Testing

- [ ] Text meets minimum contrast ratios (4.5:1 for normal, 3:1 for large)
- [ ] Information isn't conveyed by color alone
- [ ] Content is usable in high contrast mode
- [ ] Color blind users can distinguish important elements

## Responsive and Zoom Testing

- [ ] Content is usable at 200% zoom
- [ ] No horizontal scrolling at standard widths
- [ ] Touch targets are at least 44x44 pixels
- [ ] Content reflows properly on mobile devices
```

### Browser Developer Tools

```javascript
// Check for accessibility issues in browser console
function runAccessibilityCheck() {
  // Check for missing alt attributes
  const imagesWithoutAlt = document.querySelectorAll('img:not([alt])');
  if (imagesWithoutAlt.length > 0) {
    console.warn('Images without alt attributes:', imagesWithoutAlt);
  }
  
  // Check for form inputs without labels
  const inputsWithoutLabels = document.querySelectorAll('input:not([aria-label]):not([aria-labelledby])');
  const unlabeledInputs = Array.from(inputsWithoutLabels).filter(input => {
    const id = input.getAttribute('id');
    return !id || !document.querySelector(`label[for="${id}"]`);
  });
  
  if (unlabeledInputs.length > 0) {
    console.warn('Form inputs without labels:', unlabeledInputs);
  }
  
  // Check for insufficient color contrast
  const elements = document.querySelectorAll('*');
  elements.forEach(el => {
    const styles = window.getComputedStyle(el);
    const color = styles.color;
    const backgroundColor = styles.backgroundColor;
    
    // Basic contrast check (simplified)
    if (color && backgroundColor && color !== 'rgba(0, 0, 0, 0)' && backgroundColor !== 'rgba(0, 0, 0, 0)') {
      // Implementation would require color parsing and contrast calculation
      // This is a simplified example
    }
  });
}

// Run the check
runAccessibilityCheck();
```

### Testing with Assistive Technology

```markdown
## Screen Reader Testing Setup

### NVDA (Windows - Free)
1. Download from https://www.nvaccess.org/
2. Install and restart computer
3. Use NVDA + Space to turn speech on/off
4. Navigate with Tab, Arrow keys, H (headings), F (forms)

### JAWS (Windows - Commercial)
1. Download trial from Freedom Scientific
2. Use Insert + F12 to turn speech on/off
3. Similar navigation patterns to NVDA

### VoiceOver (Mac - Built-in)
1. Enable in System Preferences > Accessibility
2. Use Cmd + F5 to toggle on/off
3. Use VO keys (Control + Option) + arrows to navigate

### Testing Workflow
1. Navigate your site with keyboard only
2. Use screen reader to test content structure
3. Test form submission and error handling
4. Verify dynamic content announcements
5. Test on mobile devices with screen reader enabled
```

**Why it matters**: Regular testing ensures accessibility features work as intended for real users.

## Common Pitfalls

### Avoid These Accessibility Mistakes

```html
<!-- ❌ Common Mistakes -->

<!-- Generic link text -->
<a href="/article1">Read more</a>
<a href="/article2">Read more</a>

<!-- Missing form labels -->
<input type="text" placeholder="Enter your name">

<!-- Div soup instead of semantic HTML -->
<div class="button" onclick="submit()">Submit</div>

<!-- Color as only indicator -->
<span style="color: red;">Error: Invalid input</span>

<!-- Inaccessible custom components -->
<div class="dropdown" onclick="toggle()">
  <div class="options">
    <div onclick="select(1)">Option 1</div>
    <div onclick="select(2)">Option 2</div>
  </div>
</div>

<!-- ✅ Better Alternatives -->

<!-- Descriptive link text -->
<a href="/article1">Read more about web accessibility basics</a>
<a href="/article2">Read more about ARIA implementation</a>

<!-- Proper form labels -->
<label for="name">Full Name</label>
<input type="text" id="name" name="name">

<!-- Semantic HTML -->
<button type="submit">Submit</button>

<!-- Multiple indicators for status -->
<div class="error" role="alert">
  <span class="error-icon" aria-hidden="true">⚠</span>
  <strong>Error:</strong> Invalid input
</div>

<!-- Accessible custom dropdown -->
<div class="dropdown">
  <button
    aria-expanded="false"
    aria-haspopup="listbox"
    aria-controls="options"
  >
    Select Option
  </button>
  <ul role="listbox" id="options" style="display: none;">
    <li role="option" tabindex="0">Option 1</li>
    <li role="option" tabindex="0">Option 2</li>
  </ul>
</div>
```

### Performance Impact Considerations

```css
/* Optimize accessibility features for performance */

/* Use CSS transforms for smooth animations */
.modal {
  transform: translateY(-50px);
  opacity: 0;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.modal.open {
  transform: translateY(0);
  opacity: 1;
}

/* Efficient focus indicators */
:focus-visible {
  outline: 2px solid #0056b3;
  outline-offset: 2px;
}

/* Reduce motion for users who prefer it */
@media (prefers-reduced-motion: reduce) {
  .modal {
    transition-duration: 0.01ms;
  }
}
```

**Why it matters**: Understanding common mistakes helps you avoid accessibility barriers from the start.

## Resources and Further Learning

### Essential Tools and Extensions

```markdown
## Browser Extensions
- **axe DevTools** (Chrome, Firefox) - Automated accessibility testing
- **WAVE** (Chrome, Firefox) - Web accessibility evaluation
- **Lighthouse** (Chrome built-in) - Accessibility auditing
- **Colour Contrast Analyser** - Color contrast checking

## Design Tools
- **Figma Accessibility Plugins**
  - Stark - Color contrast and accessibility checking
  - A11y Annotation Kit - Accessibility annotations
- **Adobe XD Accessibility Plugins**

## Testing Tools
- **Pa11y** - Command line accessibility testing
- **axe-core** - JavaScript accessibility testing library
- **Accessibility Insights** - Microsoft's accessibility testing tools

## Documentation and Guidelines
- **WCAG 2.1 Guidelines** - https://www.w3.org/WAI/WCAG21/quickref/
- **MDN Accessibility** - https://developer.mozilla.org/en-US/docs/Web/Accessibility
- **WebAIM** - https://webaim.org/
- **A11y Project** - https://www.a11yproject.com/
```

### Code Snippets and Patterns

```javascript
// Utility functions for accessibility
const a11yUtils = {
  // Announce to screen readers
  announce(message, priority = 'polite') {
    const announcement = document.createElement('div');
    announcement.setAttribute('aria-live', priority);
    announcement.setAttribute('aria-atomic', 'true');
    announcement.className = 'sr-only';
    announcement.textContent = message;
    
    document.body.appendChild(announcement);
    setTimeout(() => document.body.removeChild(announcement), 1000);
  },
  
  // Trap focus within element
  trapFocus(element) {
    const focusableElements = element.querySelectorAll(
      'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
    );
    
    const firstElement = focusableElements[0];
    const lastElement = focusableElements[focusableElements.length - 1];
    
    element.addEventListener('keydown', (e) => {
      if (e.key === 'Tab') {
        if (e.shiftKey) {
          if (document.activeElement === firstElement) {
            e.preventDefault();
            lastElement.focus();
          }
        } else {
          if (document.activeElement === lastElement) {
            e.preventDefault();
            firstElement.focus();
          }
        }
      }
    });
  },
  
  // Check if element is visible to screen readers
  isAccessible(element) {
    const style = window.getComputedStyle(element);
    return !(
      style.display === 'none' ||
      style.visibility === 'hidden' ||
      element.hasAttribute('aria-hidden') ||
      element.offsetParent === null
    );
  }
};
```

### Learning Path Recommendations

```markdown
## Beginner Level
1. **Start with HTML semantics** - Learn proper use of headings, lists, forms
2. **Understand WCAG basics** - Focus on Level A and AA requirements
3. **Practice keyboard navigation** - Navigate sites without a mouse
4. **Learn about screen readers** - Install NVDA or use built-in options

## Intermediate Level
1. **ARIA fundamentals** - Labels, descriptions, roles, states
2. **Form accessibility** - Validation, error handling, complex inputs
3. **Color and contrast** - Design with accessibility in mind
4. **Testing integration** - Add automated tests to your workflow

## Advanced Level
1. **Complex widgets** - Build accessible custom components
2. **Performance considerations** - Optimize accessibility features
3. **Advanced ARIA patterns** - Trees, grids, complex interactions
4. **Accessibility auditing** - Conduct comprehensive site reviews

## Ongoing Practice
- Test with real users who use assistive technology
- Stay updated with WCAG developments
- Participate in accessibility communities
- Advocate for accessibility in your organization
```

## Conclusion

Web accessibility is not just about compliance—it's about creating inclusive experiences that work for everyone. By following these principles and patterns, you can build web applications that are truly accessible.

### Key Takeaways

1. **Start with semantic HTML** - It provides the foundation for accessibility
2. **Design with users in mind** - Consider different ways people interact with technology  
3. **Test early and often** - Use both automated tools and manual testing
4. **Learn from real users** - Engage with people who use assistive technology
5. **Make it part of your process** - Integrate accessibility into your development workflow

### The Business Case

Accessible design benefits everyone:
- **Larger market reach** - 15% of the global population has a disability
- **Better SEO** - Semantic HTML and good structure improve search rankings
- **Improved usability** - Clear navigation and content helps all users
- **Legal protection** - Compliance reduces litigation risk
- **Brand reputation** - Shows commitment to inclusion and social responsibility

Remember: Accessibility is a journey, not a destination. Every improvement makes the web more inclusive for everyone.

---

*"The power of the Web is in its universality. Access by everyone regardless of disability is an essential aspect."* - Tim Berners-Lee, W3C Director and inventor of the World Wide Web
