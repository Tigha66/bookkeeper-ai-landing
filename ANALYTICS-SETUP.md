# 📊 ANALYTICS SETUP GUIDE

## Google Analytics 4 (GA4)

### Step 1: Create GA4 Property
1. Go to https://analytics.google.com/
2. Click "Start measuring"
3. Account name: "BookkeeperAI"
4. Property name: "BookkeeperAI Pro"
5. Select your timezone and currency
6. Click "Next"
7. Select your business size and industry
8. Click "Create"

### Step 2: Get Measurement ID
1. Go to Admin (gear icon)
2. Under "Data Streams", click "Web"
3. Enter website URL: `https://your-domain.com`
4. Stream name: "BookkeeperAI Landing Page"
5. Click "Create stream"
6. Copy Measurement ID (starts with `G-`)

### Step 3: Add to Landing Page
Replace `G-XXXXXXXXXX` in `index.html` with your actual Measurement ID:

```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-YOUR-ID-HERE"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-YOUR-ID-HERE');
</script>
```

### Step 4: Track Events
Already configured in the landing page:
- ✅ Page views
- ✅ Waitlist signups
- ✅ Button clicks
- ✅ A/B test variants

### Step 5: View Analytics
- **Real-time**: See current visitors
- **Engagement**: Page views, time on page
- **Conversions**: Waitlist signups
- **Acquisition**: Traffic sources

---

## Google Tag Manager (Optional but Recommended)

### Step 1: Create GTM Account
1. Go to https://tagmanager.google.com/
2. Click "Create Account"
3. Account name: "BookkeeperAI"
4. Container name: "BookkeeperAI Web"
5. Select "Web" as target platform
6. Click "Create"

### Step 2: Install GTM Container
Copy the two code snippets and add to `index.html`:
- First snippet in `<head>`
- Second snippet after opening `<body>`

### Step 3: Add Tags in GTM
1. **Google Analytics 4 Configuration**
   - Tag type: GA4 Configuration
   - Measurement ID: `G-YOUR-ID-HERE`
   - Trigger: All Pages

2. **Waitlist Signup Event**
   - Tag type: GA4 Event
   - Event name: `waitlist_signup`
   - Trigger: Form submission

3. **Button Click Event**
   - Tag type: GA4 Event
   - Event name: `cta_click`
   - Trigger: Click on CTA buttons

### Step 4: Publish Container
1. Click "Submit" in top right
2. Version name: "Initial Setup"
3. Click "Publish"

---

## Conversion Tracking

### Track Waitlist Signups

**Google Analytics:**
```javascript
gtag('event', 'conversion', {
  'send_to': 'G-YOUR-ID-HERE/conversion_event'
});
```

**Facebook Pixel:**
```javascript
fbq('track', 'Lead');
```

**LinkedIn Insight:**
```javascript
_lmq.push(['track', 'Conversion', { value: 'waitlist_signup' }]);
```

---

## Heatmaps & Session Recording

### Hotjar Setup

1. Go to https://www.hotjar.com/
2. Create account
3. Add new site
4. Copy tracking code
5. Add to `index.html` before `</head>`

**Track:**
- Click heatmaps
- Scroll heatmaps
- Session recordings
- Form analytics

---

## A/B Testing Analytics

### Version A vs Version B

**Track in Google Analytics:**
```javascript
// Version A (index.html)
gtag('event', 'ab_test', {
  event_category: 'test',
  event_label: 'Version_A'
});

// Version B (index-b.html)
gtag('event', 'ab_test', {
  event_category: 'test',
  event_label: 'Version_B'
});
```

**Metrics to Compare:**
- Conversion rate (waitlist signups)
- Time on page
- Bounce rate
- Scroll depth

**Calculate Winner:**
```
Conversion Rate = (Signups / Visitors) × 100

Example:
Version A: 1000 visitors, 50 signups = 5% conversion
Version B: 1000 visitors, 75 signups = 7.5% conversion

Winner: Version B (50% improvement)
```

---

## Key Metrics Dashboard

### Daily Metrics
- **Visitors**: Total page views
- **Signups**: Waitlist conversions
- **Conversion Rate**: Signups / Visitors
- **Bounce Rate**: Single page visits
- **Avg Time on Page**: Engagement

### Weekly Metrics
- **Traffic Sources**: Where visitors come from
- **Top Pages**: Most viewed sections
- **Device Breakdown**: Mobile vs Desktop
- **Geographic**: Visitor locations

### Monthly Metrics
- **Growth Rate**: Month-over-month visitor growth
- **Funnel Analysis**: Visitor → Signup conversion
- **Cohort Analysis**: User retention
- **ROI**: Cost per acquisition

---

## Custom Events to Track

### Already Implemented:
```javascript
// Page view
gtag('event', 'page_view');

// Waitlist signup
gtag('event', 'waitlist_signup', {
  event_category: 'conversion',
  event_label: 'Waitlist Signup'
});

// A/B test variant
gtag('event', 'ab_test', {
  event_category: 'test',
  event_label: 'Version_A' // or Version_B
});
```

### Add These:
```javascript
// CTA button click
gtag('event', 'cta_click', {
  event_category: 'engagement',
  event_label: 'Start Free Trial'
});

// Demo video play
gtag('event', 'video_play', {
  event_category: 'engagement',
  event_label: 'Watch Demo'
});

// Pricing plan selection
gtag('event', 'pricing_click', {
  event_category: 'engagement',
  event_label: 'Growth Plan'
});

// Scroll depth (50%)
gtag('event', 'scroll_50', {
  event_category: 'engagement'
});
```

---

## UTM Parameters for Campaigns

### Track Traffic Sources

**Example URLs:**
```
// Twitter campaign
https://your-domain.com/?utm_source=twitter&utm_medium=social&utm_campaign=launch

// LinkedIn campaign
https://your-domain.com/?utm_source=linkedin&utm_medium=social&utm_campaign=launch

// Email newsletter
https://your-domain.com/?utm_source=newsletter&utm_medium=email&utm_campaign=launch

// Google Ads
https://your-domain.com/?utm_source=google&utm_medium=cpc&utm_campaign=launch
```

### UTM Builder
Use: https://ga-dev-tools.google/campaign-url-builder/

---

## Dashboard Tools

### Google Data Studio (Looker Studio)
1. Go to https://lookerstudio.google.com/
2. Create new report
3. Connect Google Analytics data source
4. Build custom dashboard with:
   - Visitors over time
   - Conversion rate
   - Traffic sources
   - Top pages

### Recommended Dashboards:
1. **Executive Dashboard**
   - Daily visitors
   - Conversion rate
   - Total signups
   - Revenue (future)

2. **Marketing Dashboard**
   - Traffic by channel
   - Campaign performance
   - Cost per acquisition
   - ROI by channel

3. **Product Dashboard**
   - Feature usage
   - User engagement
   - Retention rate
   - Churn rate

---

## Privacy & Compliance

### GDPR Compliance
1. Add cookie consent banner
2. Allow users to opt-out
3. Document data collection
4. Provide data deletion option

### CCPA Compliance
1. "Do Not Sell My Info" link
2. Privacy policy update
3. Data access requests
4. Opt-out mechanism

### Add to Landing Page:
```html
<!-- Cookie Consent Banner -->
<div id="cookie-banner" class="fixed bottom-0 left-0 right-0 bg-gray-900 text-white p-4 hidden">
  <div class="max-w-6xl mx-auto flex justify-between items-center">
    <p>We use cookies to improve your experience.</p>
    <button onclick="acceptCookies()" class="gradient-bg px-6 py-2 rounded-lg">Accept</button>
  </div>
</div>
```

---

## Testing Your Setup

### Verify Google Analytics
1. Install Google Tag Assistant Chrome extension
2. Visit your landing page
3. Check if GA4 tag fires
4. Trigger events (click buttons, submit form)
5. Verify events in Real-time report

### Test Conversions
1. Submit waitlist form
2. Check GA4 Real-time > Events
3. Verify `waitlist_signup` event appears
4. Check localStorage for signup data

### Test A/B Testing
1. Visit `index.html` (Version A)
2. Check GA4 for `Version_A` event
3. Visit `index-b.html` (Version B)
4. Check GA4 for `Version_B` event
5. Compare conversion rates

---

## Quick Start Checklist

- [ ] Create GA4 property
- [ ] Get Measurement ID
- [ ] Add to index.html and index-b.html
- [ ] Test in Real-time report
- [ ] Set up conversion tracking
- [ ] Configure A/B test tracking
- [ ] Add UTM parameters to campaigns
- [ ] Create Looker Studio dashboard
- [ ] Set up Hotjar (optional)
- [ ] Add cookie consent banner
- [ ] Test all events
- [ ] Document baseline metrics

---

**You're ready to track everything!** 📊