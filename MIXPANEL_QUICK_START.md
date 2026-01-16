# Mixpanel Quick Start Guide

## ✅ Status: READY TO USE!

All Mixpanel code has been added to your HTML files. You just need to add your project token.

---

## 🔑 Where to Put Your Auth Key (Project Token)

### Step 1: Get Your Mixpanel Project Token

1. Go to [mixpanel.com](https://mixpanel.com) and sign up/login
2. Create a new project (or use existing)
3. Click **Settings** (gear icon) → **Project Settings**
4. Copy your **Project Token** (looks like: `abc123def456789...`)

### Step 2: Replace the Token in ALL Files

Find this line in **ALL** your HTML files:

```javascript
MixpanelTracker.init('YOUR_MIXPANEL_PROJECT_TOKEN', {
```

**Replace `'YOUR_MIXPANEL_PROJECT_TOKEN'` with your actual token:**

```javascript
MixpanelTracker.init('abc123def456789...', {  // ← Your token here
```

---

## 📁 Files to Update

Replace the token in these 5 files:

1. ✅ `index.html` (line ~60)
2. ✅ `metronome/index.html` (line ~55)
3. ✅ `soundboard/index.html` (line ~60)
4. ✅ `decibel-meter/index.html` (line ~60)
5. ✅ `beatmaker/index.html` (line ~60)

**Important:** Use the **SAME token** in all files so all events go to the same project.

---

## 🔍 How to Find the Line

In each HTML file, search for:
```
YOUR_MIXPANEL_PROJECT_TOKEN
```

You'll find it in a script block that looks like:

```html
<script>
    // Initialize Mixpanel Tracker
    // TODO: Replace 'YOUR_MIXPANEL_PROJECT_TOKEN' with your actual Mixpanel project token
    document.addEventListener('DOMContentLoaded', function() {
        if (typeof MixpanelTracker !== 'undefined') {
            MixpanelTracker.init('YOUR_MIXPANEL_PROJECT_TOKEN', {  // ← Replace this!
                debug: false
            });
        }
    });
</script>
```

---

## ✅ Testing

### 1. Enable Debug Mode (Optional)

Change `debug: false` to `debug: true` to see events in console:

```javascript
MixpanelTracker.init('your_token_here', {
    debug: true  // ← Change to true
});
```

### 2. Check Browser Console

1. Open your page in browser
2. Press F12 (Developer Tools)
3. Go to Console tab
4. You should see: `Tracked: page_viewed { page_name: "home" }`

### 3. Check Mixpanel Dashboard

1. Go to [mixpanel.com](https://mixpanel.com)
2. Click **Live View** in sidebar
3. Visit your pages and click buttons
4. Events should appear in real-time!

---

## 🎯 What Gets Tracked Automatically

Once you add your token, these events are tracked automatically:

- ✅ `page_viewed` - Every page load
- ✅ `download_button_clicked` - When users click "Download on App Store"
- ✅ `logo_clicked` - When users click app logo
- ✅ `learn_more_clicked` - When users click "Learn More" on home page
- ✅ `scroll_milestone` - When users scroll to 25%, 50%, 75%, 100%
- ✅ `page_engagement` - After 10s, 30s, 60s, 120s on page
- ✅ `screenshot_viewed` - When screenshot section becomes visible
- ✅ `features_section_viewed` - When features section becomes visible

**No additional code needed!** Just add your token and it works. 🚀

---

## ❓ Troubleshooting

### Events Not Showing?

1. **Check token is correct** - No extra spaces, quotes are correct
2. **Check browser console** - Look for errors (F12 → Console)
3. **Check ad blockers** - Some block Mixpanel, test in incognito
4. **Check network tab** - Should see requests to `api.mixpanel.com`

### Still Not Working?

Set `debug: true` and check console for error messages.

---

## 📊 Next Steps

1. ✅ Add your token to all 5 files
2. ✅ Test in browser (check console)
3. ✅ Visit Mixpanel dashboard → Live View
4. ✅ Wait 24-48 hours to collect data
5. ✅ Build dashboards and analyze!

---

**That's it!** Just replace `YOUR_MIXPANEL_PROJECT_TOKEN` with your actual token in all 5 files and you're done! 🎉
