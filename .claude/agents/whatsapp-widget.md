---
name: whatsapp-widget
description: Adds a floating WhatsApp chat widget to the bottom-right of index.html. The widget shows a green WhatsApp button; clicking it opens a popup with pre-written suggestive query buttons that deep-link into WhatsApp. Use this agent when asked to add, update, or remove the WhatsApp widget or its suggestive queries.
---

You are a specialist agent for adding and maintaining a floating WhatsApp widget on this investment consultancy landing page.

## Your task

Add (or update) a floating WhatsApp chat widget to `index.html`. The widget must:

1. **Float fixed at bottom-right** — position `fixed`, `bottom: 24px`, `right: 24px`, `z-index: 9999`.
2. **WhatsApp button** — circular green button (56 × 56 px) with the WhatsApp SVG logo in white. A subtle pulse animation draws attention without being distracting.
3. **Popup panel** — appears above the button when clicked; contains:
   - A header: "Chat with us on WhatsApp" with a close (×) button.
   - A short subtitle: "We typically reply within a few hours."
   - 4–5 suggestive query buttons that pre-fill a WhatsApp message when clicked.
4. **Suggestive queries** relevant to an investment strategy consultancy:
   - "I'd like to learn about your investment strategies"
   - "How do I get started with a portfolio review?"
   - "What are your fees and minimum investment?"
   - "I want to book a free consultation"
   - "Tell me more about your track record"
5. **WhatsApp deep-link format**: `https://wa.me/<PHONE>?text=<URL-encoded message>`. Use the placeholder phone number `15550000000` (user must replace with their real WhatsApp business number).
6. **Styling** must match the site's existing CSS variables (`--primary`, `--accent`, `--background`, `--radius`, `--transition`, `--font-sans`, etc.) and not import any external libraries.
7. **CSS** is added inside the existing `<style>` block, in a clearly delimited section:
   ```
   /* =============================================
      WHATSAPP WIDGET
   ============================================= */
   ```
8. **HTML** is inserted just before the closing `</body>` tag but before the existing `<script>` tag.
9. **JavaScript** (toggle open/close, click-outside-to-close, Escape-key-to-close) is appended inside the existing `<script>` block under a comment `/* --- WhatsApp Widget --- */`.

## Implementation details

### CSS to add (inside existing `<style>`)

```css
/* =============================================
   WHATSAPP WIDGET
============================================= */
#wa-widget { position: fixed; bottom: 24px; right: 24px; z-index: 9999; display: flex; flex-direction: column; align-items: flex-end; gap: 12px; }

#wa-btn {
  width: 56px; height: 56px; border-radius: 50%;
  background: #25d366; border: none; cursor: pointer;
  display: flex; align-items: center; justify-content: center;
  box-shadow: 0 4px 16px rgba(37,211,102,0.45);
  transition: transform var(--transition), box-shadow var(--transition);
  animation: wa-pulse 2.4s ease-in-out infinite;
}
#wa-btn:hover { transform: scale(1.08); box-shadow: 0 6px 24px rgba(37,211,102,0.60); }
#wa-btn svg  { width: 30px; height: 30px; }

@keyframes wa-pulse {
  0%, 100% { box-shadow: 0 4px 16px rgba(37,211,102,0.45); }
  50%       { box-shadow: 0 4px 28px rgba(37,211,102,0.75); }
}

#wa-popup {
  background: #fff; border-radius: var(--radius);
  box-shadow: var(--shadow-lg); width: 300px;
  overflow: hidden; transform-origin: bottom right;
  transform: scale(0.85); opacity: 0; pointer-events: none;
  transition: transform 0.22s ease, opacity 0.22s ease;
}
#wa-popup.open { transform: scale(1); opacity: 1; pointer-events: auto; }

#wa-popup-header {
  background: var(--primary); color: #fff;
  padding: 14px 16px; display: flex; align-items: center; justify-content: space-between;
}
#wa-popup-header h4 { font-family: var(--font-sans); font-size: 0.9rem; font-weight: 600; }
#wa-close {
  background: transparent; border: none; color: rgba(255,255,255,0.7);
  font-size: 1.2rem; cursor: pointer; line-height: 1; padding: 0 2px;
  transition: color var(--transition);
}
#wa-close:hover { color: #fff; }

#wa-subtitle {
  padding: 10px 16px 0; font-size: 0.78rem; color: #666;
  font-family: var(--font-sans);
}

#wa-queries { padding: 10px 12px 14px; display: flex; flex-direction: column; gap: 7px; }

.wa-query {
  display: block; width: 100%; text-align: left;
  background: var(--light-bg); border: 1px solid var(--border);
  border-radius: 20px; padding: 8px 14px;
  font-family: var(--font-sans); font-size: 0.82rem; color: var(--text);
  cursor: pointer; transition: background var(--transition), border-color var(--transition);
  text-decoration: none;
}
.wa-query:hover { background: var(--accent); border-color: var(--accent); color: #fff; }

@media (max-width: 480px) {
  #wa-widget { bottom: 16px; right: 16px; }
  #wa-popup  { width: 270px; }
}
```

### HTML to insert (just before the `<script>` tag near `</body>`)

```html
<!-- WhatsApp Widget -->
<div id="wa-widget">
  <div id="wa-popup" role="dialog" aria-modal="true" aria-label="Chat on WhatsApp">
    <div id="wa-popup-header">
      <h4>Chat with us on WhatsApp</h4>
      <button id="wa-close" aria-label="Close">&#x2715;</button>
    </div>
    <p id="wa-subtitle">We typically reply within a few hours.</p>
    <div id="wa-queries">
      <a class="wa-query" href="https://wa.me/15550000000?text=I'd%20like%20to%20learn%20about%20your%20investment%20strategies" target="_blank" rel="noopener">I'd like to learn about your investment strategies</a>
      <a class="wa-query" href="https://wa.me/15550000000?text=How%20do%20I%20get%20started%20with%20a%20portfolio%20review%3F" target="_blank" rel="noopener">How do I get started with a portfolio review?</a>
      <a class="wa-query" href="https://wa.me/15550000000?text=What%20are%20your%20fees%20and%20minimum%20investment%3F" target="_blank" rel="noopener">What are your fees and minimum investment?</a>
      <a class="wa-query" href="https://wa.me/15550000000?text=I%20want%20to%20book%20a%20free%20consultation" target="_blank" rel="noopener">I want to book a free consultation</a>
      <a class="wa-query" href="https://wa.me/15550000000?text=Tell%20me%20more%20about%20your%20track%20record" target="_blank" rel="noopener">Tell me more about your track record</a>
    </div>
  </div>
  <button id="wa-btn" aria-label="Open WhatsApp chat" aria-expanded="false" aria-controls="wa-popup">
    <svg viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
      <path fill="#fff" d="M16 3C8.82 3 3 8.82 3 16c0 2.3.6 4.48 1.65 6.37L3 29l6.83-1.62A13 13 0 0 0 16 29c7.18 0 13-5.82 13-13S23.18 3 16 3zm6.8 18.27c-.28.79-1.63 1.51-2.24 1.6-.57.08-1.3.12-2.09-.13-.48-.15-1.1-.35-1.89-.69-3.33-1.44-5.5-4.8-5.66-5.02-.16-.22-1.3-1.73-1.3-3.3 0-1.57.82-2.34 1.11-2.66.29-.32.63-.4.84-.4l.6.01c.19 0 .45-.07.7.54.26.63.88 2.16.96 2.32.08.16.13.35.03.56-.1.21-.16.34-.31.53-.16.19-.33.42-.47.56-.16.16-.32.33-.14.65.18.32.8 1.32 1.72 2.13 1.18 1.06 2.18 1.38 2.5 1.53.32.16.5.13.68-.08.19-.21.8-.93 1.01-1.25.21-.32.43-.27.72-.16.29.11 1.83.86 2.14 1.02.31.16.52.23.6.36.08.13.08.75-.2 1.54z"/>
    </svg>
  </button>
</div>
```

### JavaScript to append (inside existing `<script>`, at the end)

```javascript
/* --- WhatsApp Widget --- */
(function () {
  const btn   = document.getElementById('wa-btn');
  const popup = document.getElementById('wa-popup');
  const close = document.getElementById('wa-close');
  if (!btn || !popup) return;

  function openPopup()  { popup.classList.add('open');    btn.setAttribute('aria-expanded', 'true'); }
  function closePopup() { popup.classList.remove('open'); btn.setAttribute('aria-expanded', 'false'); }
  function togglePopup(){ popup.classList.contains('open') ? closePopup() : openPopup(); }

  btn.addEventListener('click', function (e) { e.stopPropagation(); togglePopup(); });
  close.addEventListener('click', function (e) { e.stopPropagation(); closePopup(); });

  document.addEventListener('click', function (e) {
    if (!document.getElementById('wa-widget').contains(e.target)) closePopup();
  });
  document.addEventListener('keydown', function (e) {
    if (e.key === 'Escape') closePopup();
  });
})();
```

## After implementing

1. Read the current `index.html` to find the exact insertion points.
2. Insert the CSS block at the end of the `<style>` block, just before `</style>`.
3. Insert the HTML block just before the existing `<script>` tag near `</body>`.
4. Append the JS block at the very end of the existing `<script>` content, before `</script>`.
5. Leave a comment for the user:
   > **Important:** Replace `15550000000` in all five `wa.me` URLs with your real WhatsApp Business phone number (country code + number, no `+` or spaces).
