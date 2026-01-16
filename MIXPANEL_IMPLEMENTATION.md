# Mixpanel Implementation Guide

## Quick Start

### Step 1: Get Your Mixpanel Project Token

1. Sign up at [mixpanel.com](https://mixpanel.com)
2. Create a new project
3. Go to **Settings** → **Project Settings**
4. Copy your **Project Token** (looks like: `abc123def456...`)

### Step 2: Add Mixpanel SDK to Your Pages

Add this to the `<head>` section of **ALL** your HTML files (before closing `</head>`):

```html
<!-- Mixpanel SDK -->
<script>
    (function(e,a){if(!a.__SV){var b=window;try{var c,l,i,j=b.location,g=j.hash;c=function(a,b){return(m=a.match(RegExp(b+"=([^&]*)")))?m[1]:null};l=function(a,b){return a.split(b,2)[1]};i=c(g,"state");if(i){var h=JSON.parse(decodeURIComponent(i)),d=h["$mp_meta"];if(d&&d.distinct_id){a.people.identify(d.distinct_id);a.people.set(d.people);a.register(d.register);a.init(d.config);}}}catch(m){}var k,h;window.mixpanel=a;k=e.createElement("script");k.type="text/javascript";k.async=!0;k.src=e.getElementsByTagName("script")[0].getAttribute("data-site")+"/mixpanel-jslib.min.js";h=e.getElementsByTagName("script")[0];h.parentNode.insertBefore(k,h);a._i=[];a.init=function(b,d,f){function g(b,e){var a=e.split(".");2==a.length&&(b=b[a[0]],e=a[1]);b[e]=function(){b.push([e].concat(Array.prototype.slice.call(arguments,0)))}}var c=a;"undefined"!==typeof f?c=a[f]=[]:f="mixpanel";c.people=c.people||[];c.toString=function(b){var a="mixpanel";"mixpanel"!==f&&(a+="."+f);b||(a+=" (stub)");return a};c.people.toString=function(){return c.toString(1)+".people (stub)"};var l="init identify alias track register unregister register_once track_with_groups set_group get_group clear_groups name_tag set_config reset opt_in_tracking opt_out_tracking has_opted_in_tracking has_opted_out_tracking clear_opt_in_out_tracking start_batch_senders send_event delete_user people.set people.set_once people.unset people.increment people.append people.union people.track_charge people.clear_charges people.delete_user people.remove".split(" ");for(h=0;h<l.length;h++)g(c,l[h]);a._i.push([b,d,f])};a.__SV=1.2;b=e.createElement("script");b.type="text/javascript";b.async=!0;b.src="undefined"!==typeof MIXPANEL_CUSTOM_LIB_URL?MIXPANEL_CUSTOM_LIB_URL:"https://cdn.mixpanel.com/lib/mixpanel-2-latest.min.js";c=e.getElementsByTagName("script")[0];c.parentNode.insertBefore(b,c)}})(document,window.mixpanel||[]);
</script>
```

**OR** use the official CDN (simpler):

```html
<!-- Mixpanel SDK -->
<script src="https://cdn.mixpanel.com/lib/mixpanel-2-latest.min.js"></script>
```

### Step 3: Add Tracker Script

Add this **after** the Mixpanel SDK (still in `<head>`):

```html
<!-- Mixpanel Tracker -->
<script src="assets/js/mixpanel-tracker.js"></script>
```

### Step 4: Initialize Tracker

Add this **right before** closing `</head>` tag:

```html
<script>
    // Initialize Mixpanel Tracker
    // Replace 'YOUR_PROJECT_TOKEN' with your actual Mixpanel project token
    document.addEventListener('DOMContentLoaded', function() {
        if (typeof MixpanelTracker !== 'undefined') {
            MixpanelTracker.init('YOUR_PROJECT_TOKEN', {
                debug: false // Set to true during development to see console logs
            });
        }
    });
</script>
```

---

## Complete Example

Here's what your `<head>` section should look like:

```html
<head>
    <!-- ... your existing meta tags ... -->
    
    <!-- Mixpanel SDK -->
    <script src="https://cdn.mixpanel.com/lib/mixpanel-2-latest.min.js"></script>
    
    <!-- Mixpanel Tracker -->
    <script src="assets/js/mixpanel-tracker.js"></script>
    
    <!-- Initialize Mixpanel -->
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            if (typeof MixpanelTracker !== 'undefined') {
                MixpanelTracker.init('YOUR_PROJECT_TOKEN', {
                    debug: false
                });
            }
        });
    </script>
    
    <!-- ... rest of your head content ... -->
</head>
```

---

## Files to Update

Add the Mixpanel code to these files:

1. ✅ `index.html` (main page)
2. ✅ `metronome/index.html`
3. ✅ `soundboard/index.html`
4. ✅ `decibel-meter/index.html`
5. ✅ `beatmaker/index.html`

**Important:** Use the **same project token** in all files so all events go to the same Mixpanel project.

---

## Testing

### 1. Enable Debug Mode

Set `debug: true` in the initialization:

```javascript
MixpanelTracker.init('YOUR_PROJECT_TOKEN', {
    debug: true
});
```

This will log all events to the browser console.

### 2. Check Browser Console

Open your browser's Developer Tools (F12) and check the Console tab. You should see:
```
Tracked: page_viewed { page_name: "home" }
```

### 3. Use Mixpanel Live View

1. Go to your Mixpanel dashboard
2. Click **Live View** in the left sidebar
3. Visit your pages and click buttons
4. You should see events appearing in real-time

### 4. Test Events

- ✅ Visit a page → Should see `page_viewed`
- ✅ Click download button → Should see `download_button_clicked`
- ✅ Click logo → Should see `logo_clicked`
- ✅ Scroll down → Should see `scroll_milestone` at 25%, 50%, 75%, 100%
- ✅ Wait 10 seconds → Should see `page_engagement` with `time_on_page: 10`

---

## Customization

### Change Project Token Per Environment

```javascript
// Development
const token = window.location.hostname === 'localhost' 
    ? 'DEV_TOKEN' 
    : 'PROD_TOKEN';

MixpanelTracker.init(token);
```

### Disable Specific Events

If you want to disable scroll tracking, modify `mixpanel-tracker.js`:

```javascript
setupScrollTracking: function() {
    // Disabled - uncomment to enable
    // if (!this.config.throttleScroll) return;
    // ... rest of code
}
```

---

## Troubleshooting

### Events Not Showing Up?

1. **Check Mixpanel SDK is loaded:**
   ```javascript
   console.log(typeof mixpanel); // Should be "object"
   ```

2. **Check tracker is initialized:**
   ```javascript
   console.log(typeof MixpanelTracker); // Should be "object"
   ```

3. **Check ad blockers:**
   - Some ad blockers block Mixpanel
   - Test in incognito mode or disable ad blocker

4. **Check network tab:**
   - Open DevTools → Network tab
   - Filter by "mixpanel"
   - You should see requests to `api.mixpanel.com`

### Events Firing Multiple Times?

- Make sure you only initialize once per page
- Check that you're not including the script multiple times

### Console Errors?

- Make sure Mixpanel SDK loads before the tracker script
- Check that the tracker file path is correct: `assets/js/mixpanel-tracker.js`

---

## Next Steps

1. ✅ Add Mixpanel SDK and tracker to all pages
2. ✅ Test events in Live View
3. ✅ Wait 24-48 hours to collect data
4. ✅ Build dashboards in Mixpanel:
   - Conversion funnel
   - Page views by app
   - Download button click rate
   - Scroll depth distribution
5. ✅ Analyze and optimize based on data

---

## Support

- **Mixpanel Docs:** https://docs.mixpanel.com
- **Mixpanel Community:** https://community.mixpanel.com

---

**Ready to implement?** Follow the steps above and you'll be tracking in minutes! 🚀
