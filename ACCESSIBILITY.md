# Accessibility Guidelines

## 🎯 Our Commitment

**Every template in this repository is WCAG 2.1 AA compliant.**

Accessibility isn't an afterthought—it's our foundation. We believe animated content should be enjoyable and usable by everyone, including people with disabilities.

## ✅ WCAG 2.1 AA Compliance Checklist

All templates must meet these criteria:

### 1. **Motion Sensitivity (WCAG 2.3.1, 2.3.2)**

```xml
<!-- MANDATORY: Respect prefers-reduced-motion -->
<style>
  @media (prefers-reduced-motion: reduce) {
    * {
      animation: none !important;
      transition: none !important;
    }
  }
</style>
```

**Requirements:**
- ✅ No flashing content > 3 times per second
- ✅ No large flashing areas (> 25% viewport)
- ✅ Animations pause when user prefers reduced motion
- ✅ Maximum animation duration: 5 seconds autoplay

### 2. **Semantic Structure (WCAG 1.3.1)**

```xml
<!-- Proper ARIA labels -->
<svg xmlns="http://www.w3.org/2000/svg" 
     role="img" 
     aria-labelledby="title-id desc-id">
  <title id="title-id">Concise Title</title>
  <desc id="desc-id">Detailed description of visual content</desc>
  <!-- Content here -->
</svg>
```

**Requirements:**
- ✅ `<title>` for brief identification
- ✅ `<desc>` for detailed description
- ✅ `role="img"` for proper semantics
- ✅ Meaningful IDs for `aria-labelledby`

### 3. **Color Contrast (WCAG 1.4.3)**

**Minimum Requirements:**
- Text < 18pt: Contrast ratio ≥ 4.5:1
- Text ≥ 18pt: Contrast ratio ≥ 3:1
- UI components: Contrast ratio ≥ 3:1

**Testing Tools:**
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- Chrome DevTools Color Picker
- [Stark Plugin](https://www.getstark.co/)

### 4. **Keyboard Navigation (WCAG 2.1.1)**

While SVG in README doesn't support keyboard interaction, if templates evolve to interactive versions:

- ✅ All interactive elements must be keyboard accessible
- ✅ Focus indicators visible (outline, border, etc.)
- ✅ Logical tab order
- ✅ Escape key to dismiss modals/overlays

### 5. **Text Alternatives (WCAG 1.1.1)**

**For icons/symbols:**
```xml
<g role="img" aria-label="Success checkmark">
  <circle cx="50" cy="50" r="20" fill="green"/>
  <path d="M45,50 L48,53 L55,46" stroke="white"/>
</g>
```

**For decorative elements:**
```xml
<g aria-hidden="true">
  <!-- Decorative shapes -->
</g>
```

### 6. **Animation Timing (WCAG 2.2.2)**

**Rules:**
- ✅ Autoplay animations ≤ 5 seconds
- ✅ Looping animations must be subtle (low amplitude)
- ✅ No essential information conveyed through animation alone
- ✅ Users can pause, stop, or hide animations (via `prefers-reduced-motion`)

## 🧪 Testing Process

Before submitting a template, verify:

### **1. PEAT Testing (Photosensitive Epilepsy Analysis Tool)**

Download: [Trace Research PEAT](https://trace.umd.edu/peat/)

**Steps:**
1. Export SVG animation as video (screen recording)
2. Run through PEAT analyzer
3. Ensure "Pass" result (no flashing violations)

### **2. Screen Reader Testing**

**macOS:** VoiceOver (Cmd + F5)
```
Expected: "<title> content, <desc> content, image"
```

**Windows:** NVDA (free) or JAWS
```
Expected: Announces title and description
```

**Test Checklist:**
- [ ] Title announced clearly
- [ ] Description provides context
- [ ] Decorative elements ignored (`aria-hidden="true"`)

### **3. Reduced Motion Testing**

**macOS:**
```
System Preferences → Accessibility → Display → Reduce Motion
```

**Windows:**
```
Settings → Ease of Access → Display → Show animations
```

**Test:**
- [ ] Animations stop completely
- [ ] Layout remains functional
- [ ] No content hidden when animations disabled

### **4. Color Blindness Simulation**

**Tools:**
- [Colorblind Web Page Filter](https://www.toptal.com/designers/colorfilter/)
- Chrome DevTools Emulation (Rendering > Emulate vision deficiencies)

**Test types:**
- Protanopia (red-blind)
- Deuteranopia (green-blind)
- Tritanopia (blue-blind)
- Achromatopsia (total color blindness)

### **5. Contrast Verification**

**Manual Check:**
```
Contrast Ratio = (L1 + 0.05) / (L2 + 0.05)
Where L1 = lighter color luminance, L2 = darker
```

**Automated Tools:**
- [axe DevTools](https://www.deque.com/axe/devtools/)
- [WAVE Extension](https://wave.webaim.org/extension/)

## 📊 Accessibility Report Template

For each template, maintain this report:

```markdown
## Template: [NAME]

### WCAG 2.1 AA Compliance
- [x] Motion sensitivity (prefers-reduced-motion)
- [x] No flashing > 3 Hz
- [x] Semantic structure (title, desc, role)
- [x] Color contrast ≥ 4.5:1 (text)
- [x] Animation duration ≤ 5s autoplay

### Testing Results
- **PEAT:** Pass ✅
- **Screen Reader (VoiceOver):** Pass ✅
- **Reduced Motion:** Pass ✅
- **Color Blindness:** Pass ✅ (all types)
- **Contrast Ratio:** 7.2:1 (exceeds minimum) ✅

### Known Limitations
- None

### Last Updated
2024-11-06
```

## 🚨 Common Accessibility Mistakes to Avoid

### ❌ **Missing prefers-reduced-motion**
```xml
<!-- BAD -->
<animate attributeName="x" values="0;100" dur="2s" repeatCount="indefinite"/>
```

```xml
<!-- GOOD -->
<style>
  @media (prefers-reduced-motion: reduce) {
    * { animation: none !important; }
  }
</style>
<animate attributeName="x" values="0;100" dur="2s" repeatCount="indefinite"/>
```

### ❌ **Flashing Content**
```xml
<!-- BAD: Rapid flashing (5 Hz) -->
<animate attributeName="opacity" values="1;0;1" dur="0.2s" repeatCount="indefinite"/>
```

```xml
<!-- GOOD: Slow fade (0.5 Hz) -->
<animate attributeName="opacity" values="1;0.5;1" dur="2s" repeatCount="indefinite"/>
```

### ❌ **Missing Descriptions**
```xml
<!-- BAD -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">
  <circle cx="50" cy="50" r="40"/>
</svg>
```

```xml
<!-- GOOD -->
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" role="img" aria-labelledby="circle-title">
  <title id="circle-title">Blue loading indicator</title>
  <desc>Animated circle showing loading progress</desc>
  <circle cx="50" cy="50" r="40"/>
</svg>
```

### ❌ **Low Contrast**
```xml
<!-- BAD: Light gray on white (1.2:1) -->
<text fill="#cccccc">Low contrast text</text>
<rect fill="white"/>
```

```xml
<!-- GOOD: Dark gray on white (7:1) -->
<text fill="#333333">High contrast text</text>
<rect fill="white"/>
```

## 📚 Resources

### **Standards**
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [SVG Accessibility (W3C)](https://www.w3.org/TR/svg-aam-1.0/)

### **Tools**
- [PEAT Analyzer](https://trace.umd.edu/peat/)
- [axe DevTools](https://www.deque.com/axe/devtools/)
- [WAVE Extension](https://wave.webaim.org/extension/)
- [Contrast Checker](https://webaim.org/resources/contrastchecker/)

### **Tutorials**
- [Accessible SVG (CSS-Tricks)](https://css-tricks.com/accessible-svgs/)
- [ARIA in SVG (MDN)](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques)

## 💬 Questions?

If you're unsure about accessibility compliance:

1. Open an issue with your template
2. Tag it with `accessibility` label
3. We'll review and provide guidance

**Email:** nexusstudio100@gmail.com

---

**Remember:** Accessibility benefits everyone. A template that works for users with disabilities is a better template for all users.