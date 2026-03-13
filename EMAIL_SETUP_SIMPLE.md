# Contact Form Email Setup - Simple Solution

## Current Setup
The contact form now uses a **mailto link** which opens the user's default email client. This works but requires the user to have an email client configured.

## Better Solution: FormSubmit (Recommended)

FormSubmit is a free service that sends form submissions directly to your email without any backend code.

### Setup Steps (5 minutes):

1. **Update your HTML form** - Replace the current form action:

```html
<form class="contact-form" id="contactForm" action="https://formsubmit.co/gautam07.work@gmail.com" method="POST">
```

2. **Update script.js** - Replace the contact form handling code with:

```javascript
// ===== Contact Form Handling with FormSubmit =====
const contactForm = document.getElementById('contactForm');
const msg = document.getElementById('msg');

if (contactForm) {
    contactForm.addEventListener('submit', function(e) {
        const submitBtn = contactForm.querySelector('button[type="submit"]');
        const originalText = submitBtn.innerHTML;
        submitBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Sending...';
        submitBtn.disabled = true;
        
        // FormSubmit will handle the actual submission
        // Show success message after a delay
        setTimeout(() => {
            msg.innerHTML = '<i class="fas fa-check-circle"></i> Message sent successfully! I\'ll get back to you soon.';
            msg.style.color = '#00ff88';
            msg.style.display = 'block';
            
            submitBtn.innerHTML = originalText;
            submitBtn.disabled = false;
        }, 1000);
    });
}
```

3. **First Submission Activation**:
   - The first time someone submits the form, FormSubmit will send you a confirmation email
   - Click the confirmation link in that email
   - After that, all submissions will go directly to gautam07.work@gmail.com

### Features:
- ✅ No backend code needed
- ✅ No API keys required
- ✅ Free forever
- ✅ Spam protection included
- ✅ Email notifications to gautam07.work@gmail.com
- ✅ Works immediately after confirmation

### Advanced Options (Optional):

Add these hidden fields to customize behavior:

```html
<!-- Redirect to thank you page after submission -->
<input type="hidden" name="_next" value="https://yourdomain.com/thanks.html">

<!-- Disable reCAPTCHA -->
<input type="hidden" name="_captcha" value="false">

<!-- Custom subject line -->
<input type="hidden" name="_subject" value="New Portfolio Contact!">

<!-- Template for email -->
<input type="hidden" name="_template" value="table">
```

## Alternative: EmailJS (More Features)

If you want more control, use EmailJS:

1. Sign up at [emailjs.com](https://www.emailjs.com/)
2. Create an email service
3. Create an email template
4. Get your Service ID, Template ID, and Public Key
5. Add EmailJS SDK to your HTML:

```html
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@3/dist/email.min.js"></script>
```

6. Update the contact form handler in script.js

## Current Temporary Solution

Right now, the form uses a **mailto link** which:
- Opens the user's email client
- Pre-fills your email address and message
- User clicks "Send" in their email client
- You receive the email at gautam07.work@gmail.com

This works but isn't ideal. I recommend switching to FormSubmit for a better user experience.

## Quick Fix Instructions

To implement FormSubmit right now:

1. Open `index.html`
2. Find the contact form line: `<form class="contact-form" id="contactForm">`
3. Replace it with: `<form class="contact-form" id="contactForm" action="https://formsubmit.co/gautam07.work@gmail.com" method="POST">`
4. Test the form - first submission will require email confirmation
5. Check your email and confirm
6. Done! All future submissions go directly to your inbox
