# Mixpanel Analytics Tracking Plan
**For iOS App Landing Pages**  
**Date:** January 15, 2026

---

## 🎯 Overview

This document outlines the **best events to track** for your iOS app landing pages using Mixpanel. Focus is on **conversion tracking**, **user engagement**, and **acquisition insights**.

---

## 📊 Why Track These Events?

### Your Business Goals:
1. **Conversion:** Get users to click "Download on App Store" → Install app
2. **Engagement:** Understand which pages/features interest users most
3. **Acquisition:** Know where users come from (UTM, referrer)
4. **Optimization:** Identify drop-off points in the conversion funnel

---

## 🏆 Priority Events (Must-Track)

### 1. **Page View** ⭐⭐⭐
**Event:** `page_viewed`  
**When:** Every page load  
**Why:** Foundation metric - tracks traffic, page popularity, user journey

**Properties:**
```javascript
{
  page_name: "metronome" | "soundboard" | "decibel-meter" | "beatmaker" | "home",
  page_path: "/metronome/",
  referrer: "google.com" | "direct" | "twitter.com",
  utm_source: "google" | "facebook" | null,
  utm_campaign: "summer_promo" | null,
  utm_medium: "cpc" | "organic" | null,
  device_type: "mobile" | "desktop" | "tablet",
  browser: "Chrome" | "Safari" | "Firefox",
  os: "iOS" | "Android" | "Windows" | "macOS",
  country: "US" | "UK" | etc.
}
```

---

### 2. **Download Button Click** ⭐⭐⭐
**Event:** `download_button_clicked`  
**When:** User clicks "Download on the App Store" button  
**Why:** **PRIMARY CONVERSION EVENT** - This is your money metric!

**Properties:**
```javascript
{
  app_name: "metronome" | "soundboard" | "decibel-meter" | "beatmaker",
  button_location: "hero" | "cta_section" | "footer",
  page_name: "metronome",
  device_type: "mobile" | "desktop",
  time_on_page: 45, // seconds
  scroll_depth: 75, // percentage
  referrer: "google.com",
  utm_source: "google"
}
```

**Why Track Location:**
- Know which button placement converts best (hero vs CTA section)
- Optimize button placement based on data

---

### 3. **Logo Click** ⭐⭐
**Event:** `logo_clicked`  
**When:** User clicks app logo (which also goes to App Store)  
**Why:** Alternative conversion path - some users click logo instead of button

**Properties:**
```javascript
{
  app_name: "metronome" | "soundboard" | "decibel-meter" | "beatmaker",
  page_name: "metronome",
  device_type: "mobile" | "desktop"
}
```

---

### 4. **Learn More Click** ⭐⭐
**Event:** `learn_more_clicked`  
**When:** User clicks "Learn More" on main index page app cards  
**Why:** Measures interest in specific apps, helps prioritize which apps to promote

**Properties:**
```javascript
{
  app_name: "metronome" | "soundboard" | "decibel-meter" | "beatmaker",
  source_page: "home"
}
```

---

### 5. **Scroll Depth** ⭐⭐
**Event:** `scroll_milestone`  
**When:** User scrolls to 25%, 50%, 75%, 100% of page  
**Why:** Measures engagement - users who scroll more are more interested

**Properties:**
```javascript
{
  page_name: "metronome",
  scroll_depth: 25 | 50 | 75 | 100, // percentage
  time_to_scroll: 12 // seconds to reach this depth
}
```

**Implementation Note:** Throttle to avoid too many events (only fire once per milestone)

---

### 6. **Time on Page** ⭐
**Event:** `page_engagement`  
**When:** User spends 10s, 30s, 60s, 120s on page  
**Why:** Engagement metric - longer time = more interest

**Properties:**
```javascript
{
  page_name: "metronome",
  time_on_page: 10 | 30 | 60 | 120, // seconds
  scroll_depth: 50 // percentage at this time
}
```

---

### 7. **Screenshot View** ⭐
**Event:** `screenshot_viewed`  
**When:** User scrolls to screenshot section (screenshots become visible)  
**Why:** Screenshots are important - users viewing them are more engaged

**Properties:**
```javascript
{
  page_name: "metronome",
  screenshot_count: 4, // total screenshots on page
  device_type: "mobile" | "desktop"
}
```

---

### 8. **Feature Section View** ⭐
**Event:** `features_section_viewed`  
**When:** User scrolls to features section  
**Why:** Measures interest in app features

**Properties:**
```javascript
{
  page_name: "metronome",
  feature_count: 6 // number of features shown
}
```

---

## 📈 Secondary Events (Nice to Have)

### 9. **External Link Click**
**Event:** `external_link_clicked`  
**When:** User clicks Privacy/Terms/Support links in footer  
**Properties:** `link_type: "privacy" | "terms" | "support"`, `page_name`

### 10. **Image Load Error**
**Event:** `image_load_failed`  
**When:** Screenshot image fails to load  
**Properties:** `image_url`, `page_name`  
**Why:** Technical monitoring - helps catch broken images

---

## 🎯 Conversion Funnel

### Your Funnel Should Be:
```
1. page_viewed (home)
   ↓
2. learn_more_clicked (if from home)
   ↓
3. page_viewed (app page)
   ↓
4. scroll_milestone (25%, 50%, 75%)
   ↓
5. features_section_viewed
   ↓
6. screenshot_viewed
   ↓
7. download_button_clicked ⭐ CONVERSION
```

**Key Metrics to Track:**
- **Conversion Rate:** `download_button_clicked` / `page_viewed` (app pages)
- **Drop-off Rate:** Where users leave the funnel
- **Time to Convert:** Average time from page view to download click

---

## 🔍 User Properties to Set

Set these once per user/session (not per event):

```javascript
{
  distinct_id: "user_123" or session_id,
  first_seen: "2026-01-15",
  device_type: "mobile",
  browser: "Safari",
  os: "iOS",
  country: "US",
  referrer: "google.com",
  utm_source: "google",
  utm_campaign: "summer_promo"
}
```

---

## 📊 Key Metrics You'll Measure

### 1. **Conversion Metrics**
- Download button click rate per page
- Logo click rate
- Overall conversion rate (clicks / page views)

### 2. **Engagement Metrics**
- Average time on page
- Scroll depth distribution
- Feature section view rate
- Screenshot view rate

### 3. **Acquisition Metrics**
- Traffic sources (UTM, referrer)
- Which apps get most interest
- Device/browser breakdown
- Geographic distribution

### 4. **Funnel Analysis**
- Drop-off points in conversion funnel
- Which page sections lead to conversions
- Time to convert

---

## 🚀 Implementation Priority

### Phase 1 (Start Here) - Critical Events:
1. ✅ `page_viewed` - Foundation
2. ✅ `download_button_clicked` - Primary conversion
3. ✅ `logo_clicked` - Alternative conversion path

### Phase 2 (After 1 week) - Engagement:
4. ✅ `scroll_milestone` - Engagement depth
5. ✅ `learn_more_clicked` - Interest measurement

### Phase 3 (After 1 month) - Advanced:
6. ✅ `page_engagement` - Time-based engagement
7. ✅ `screenshot_viewed` - Content engagement
8. ✅ `features_section_viewed` - Feature interest

---

## 💡 Best Practices

### 1. **Naming Convention**
- Use `snake_case` for events: `download_button_clicked`
- Use descriptive names: `download_button_clicked` not `click1`
- Be consistent across all pages

### 2. **Properties Over Events**
- Don't create separate events for each app
- Use `app_name` property instead:
  - ✅ `download_button_clicked` with `app_name: "metronome"`
  - ❌ `metronome_download_clicked`, `soundboard_download_clicked`

### 3. **Throttle High-Frequency Events**
- `scroll_milestone`: Fire once per milestone (25%, 50%, 75%, 100%)
- `page_engagement`: Fire once per time milestone (10s, 30s, 60s, 120s)

### 4. **Privacy & Compliance**
- Don't send PII (personally identifiable information)
- Use session IDs, not user emails
- Consider GDPR/CCPA compliance if needed

### 5. **Error Handling**
- Wrap tracking in try-catch to prevent JS errors
- Use fallback for ad-blockers (optional: server-side tracking)

---

## 📝 Event Summary Table

| Event | Priority | Frequency | Key Properties |
|-------|----------|-----------|----------------|
| `page_viewed` | ⭐⭐⭐ | Every page load | page_name, referrer, utm_source |
| `download_button_clicked` | ⭐⭐⭐ | On button click | app_name, button_location |
| `logo_clicked` | ⭐⭐ | On logo click | app_name |
| `learn_more_clicked` | ⭐⭐ | On link click | app_name |
| `scroll_milestone` | ⭐⭐ | At 25/50/75/100% | scroll_depth |
| `page_engagement` | ⭐ | At 10/30/60/120s | time_on_page |
| `screenshot_viewed` | ⭐ | When visible | screenshot_count |
| `features_section_viewed` | ⭐ | When visible | feature_count |

---

## 🎯 What This Data Tells You

### Business Questions You Can Answer:

1. **Which app is most popular?**
   - Compare `page_viewed` counts per app
   - Compare `download_button_clicked` rates

2. **Where do users come from?**
   - Analyze `referrer` and `utm_source` in `page_viewed`

3. **Which button placement works best?**
   - Compare `download_button_clicked` with `button_location: "hero"` vs `"cta_section"`

4. **Are users engaged?**
   - Average `scroll_depth` and `time_on_page`

5. **What's the conversion rate?**
   - `download_button_clicked` / `page_viewed` per app

6. **Where do users drop off?**
   - Funnel analysis: see where users leave before converting

---

## 🔧 Next Steps

1. **Get Mixpanel Project Token** from your Mixpanel dashboard
2. **Implement Phase 1 events** (page_viewed, download_button_clicked, logo_clicked)
3. **Test events** using Mixpanel's Live View
4. **Wait 1 week** to collect baseline data
5. **Add Phase 2 events** (scroll, learn_more)
6. **Build dashboards** in Mixpanel to visualize metrics
7. **Iterate** based on insights

---

**Ready to implement?** See the implementation guide in the next document!
