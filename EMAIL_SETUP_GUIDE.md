# Email Setup Guide for Portfolio Contact Form

## Overview
The contact form has been enhanced with JavaScript to actually send emails. It uses **EmailJS** as the primary method and falls back to `mailto:` if EmailJS is not configured.

## Method 1: EmailJS Setup (Recommended)

EmailJS allows you to send emails directly from the frontend without a backend server.

### Step 1: Create EmailJS Account
1. Go to [https://www.emailjs.com/](https://www.emailjs.com/)
2. Sign up for a free account
3. Verify your email address

### Step 2: Create Email Service
1. In your EmailJS dashboard, go to **Email Services**
2. Click **Add New Service**
3. Choose your email provider (Gmail, Outlook, etc.)
4. Follow the setup instructions for your provider
5. Note down your **Service ID** (e.g., `service_portfolio`)

### Step 3: Create Email Template
1. Go to **Email Templates**
2. Click **Create New Template**
3. Use this template structure:

```
Subject: New message from {{from_name}} - {{subject}}

You have received a new message from your portfolio website:

From: {{from_name}} ({{from_email}})
Subject: {{subject}}

Message:
{{message}}

---
This message was sent from your portfolio contact form.
```

4. Save the template and note down your **Template ID** (e.g., `template_contact`)

### Step 4: Get Public Key
1. Go to **Integration** in your EmailJS dashboard
2. Copy your **Public Key**

### Step 5: Update the Code
In `index.html`, find this line and uncomment it, replacing with your actual public key:

```javascript
// emailjs.init('YOUR_PUBLIC_KEY'); // Uncomment and add your EmailJS public key
```

Change it to:
```javascript
emailjs.init('your_actual_public_key_here');
```

Also update the service and template IDs in the `sendEmailWithEmailJS` function:
```javascript
emailjs.send('your_service_id', 'your_template_id', {
```

## Method 2: Fallback (Current Working Method)

If EmailJS is not configured, the form will use the `mailto:` method, which:
- Opens the user's default email client
- Pre-fills the email with all form data
- Requires the user to manually send the email

This method works immediately without any setup but requires user action.

## Features Included

### Form Validation
- All fields are required
- Email format validation
- Real-time feedback

### User Experience
- Loading states during submission
- Success/error/info messages
- Form reset after successful submission
- Responsive design

### Error Handling
- Graceful fallback to mailto if EmailJS fails
- Clear error messages
- Network failure handling

## Testing the Form

1. **With EmailJS configured**: Messages will be sent directly to your email
2. **Without EmailJS**: The form will open the default email client with pre-filled content
3. **Form validation**: Try submitting with empty fields to test validation

## Email Deliverability Tips

1. **Test with multiple email clients** to ensure compatibility
2. **Set up email filters** to organize portfolio messages
3. **Consider using a dedicated email** for portfolio contacts
4. **Monitor EmailJS usage** to stay within free tier limits (200 emails/month)

## Troubleshooting

### EmailJS Not Working
- Check browser console for errors
- Verify public key, service ID, and template ID
- Ensure EmailJS service is properly configured
- Check EmailJS dashboard for usage limits

### Mailto Not Opening
- Ensure user has a default email client configured
- Some browsers may block mailto links
- Consider adding instructions for users

### Form Not Submitting
- Check browser console for JavaScript errors
- Verify all form field IDs match the JavaScript
- Ensure internet connection for EmailJS

## Security Notes

- EmailJS public key is safe to expose in frontend code
- No sensitive information is stored in the frontend
- Consider rate limiting for production use
- Monitor EmailJS dashboard for suspicious activity

---

**Note**: The current implementation works with the mailto fallback. Setting up EmailJS will enhance the user experience by sending emails automatically without requiring user interaction.