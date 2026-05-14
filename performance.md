**Rendering on the Web:**

- https://web.dev/articles/rendering-on-the-web#a-rehydration-problem-one-app-for-the-price-of-two

### Core Web Vitals

_Set of metrics that measure real-world user experience for loading performance, interactivity, and visual stability of the page._

- **Largest Contentful Paint (LCP):** _Measures loading performance - Good: < 2.5s_
  LCP reports the render time of the largest image, text block, or video visible in the viewport, relative to when the user first navigated to the page.
  [Read more](https://web.dev/articles/lcp)

- **Interaction to Next Paint (INP):** _Measures responsiveness - Good: < 200ms_
  INP is a metric that assesses a page's overall responsiveness to user interactions by observing the latency of all click, tap, and keyboard interactions that occur throughout the lifespan of a user's visit to a page. The final INP value is the longest interaction observed, ignoring outliers.
  [Read more](https://web.dev/articles/inp)

- **Cumulative Layout Shift (CLS):** _Measures visual stability. Good - < 0.1_
  CLS is a measure of the largest burst of layout shift(when one or more individual layout shifts occur in rapid succession with less than 1-second between each shift) scores for every unexpected layout shift that occurs during entire lifecycle of the page.
  [Read more](https://web.dev/articles/cls)

##### Why important:

- SEO ranking factor
- Real user experience
- Business impact (bounce rate, conversions)

#### How would you improve LCP:

- Optimize server response time(TTFB)
- CDN Usage
- Compress images (WebP/AVIF)
- Preload hero image
- Critical CSS
- Reduce render-blocking JS
- SSR/SSG
- Lazy load below-the-fold assets

#### How do you reduce CLS:

- Set width/height on images/videos
- Reserve ad/banner space
- Avoid inserting content above existing content
- Font loading optimization (font-display: swap)
- Skeleton loaders

---

### Lighthouse

_An automated auditing tool by Google for:_

- Performance
- Accessibility
- Best Practices
- SEO
- PWA

#### Important metrics

- FCP
- LCP
- TBT (Total Blocking Time)
- CLS
- Speed index

#### Lighthouse vs Core Web Vitals

##### Lighthouse

- Lab data
- Simulated environment

##### Core Web Vitals

- Field data
- Real users

---

### Real User Monitoring (RUM) vs Synthetic Monitoring

##### RUM:

- Actual user devices
- Chrome UX Report
- Google Analytics Web Vitals

##### Synthetic:

- Controlled tests
- Lighthouse
- WebPageTest

---

### Bundle Optimization

#### How do you reduce JS bundle size?

- Tree shaking
- Dynamic imports
- Route-level code splitting
- Remove unused polyfills
- Analyze bundles (webpack-bundle-analyzer)
- Use modern builds (module/nomodule)
- Replace heavy libraries (Moment -> Days.js)

#### Tree Shaking

Dead code elimination for unused ES module exports during build.

---

### Network Performance

#### preload, prefetch, preconnect

| Preload                         | Prefetch                           | Preconnect               |
| ------------------------------- | ---------------------------------- | ------------------------ |
| Critical current page resources | Likely future navigation resources | Early DNS/TLS connection |

---

### Caching

##### Frontend caching strategies

- HTTP cache headers
- Service workers
- CDN edge cache
- Stale-while-revalidate

---

### Performance Debugging

##### Debugging techniques

- Chrome DevTools Performance tab
- Lighthouse
- React Profiler
- Network waterfall
- Bundle analyzer
- Identify:
  - Long tasks
  - Re-renders
  - JS blocking
  - Large assets

##### Browser / DevTools:

- Chrome DevTools Performance
- Lighthouse
- React Profiler
- Coverage Tab
- Memory Tab

##### External

- WebPageTest
- GTmetrix
- PageSpeed Insights
- Bundlephobia
- webpack-bundle-analyzer
- sentry performance
- New Relic
- Datadog RUM

---

#### Q: Your bundle is 3MB. What would you do?

- Split routes
- Analyze dependencies
- Lazy load heavy modules
- Image optimization
- Remove duplicate packages
- CDN
- Broti/GZip

#### Q: Key Metrics Cheat Sheet

| Metric | Meaning                    | Good Score |
| ------ | -------------------------- | ---------- |
| FCP    | First content visible      | < 1.8s.    |
| LCP    | Main content visible.      | < 2.5s.    |
| CLS.   | Layout stability           | < 0.1.     |
| INP.   | Interaction responsiveness | < 200ms.   |
| TBT    | Blocking time              | < 200ms.   |

---

**Images:**

- https://web.dev/serve-images-webp/

#### Related Links

- https://web.dev/case-studies
- https://checkout.stripe.dev/checkout
- https://web.dev/learn/forms/autofill/
- https://innovation.ebayinc.com/stories/autofill-deep-dive/
- https://developers.google.com/maps/documentation/javascript/legacy/place-autocomplete

#### References

- https://web.dev/
