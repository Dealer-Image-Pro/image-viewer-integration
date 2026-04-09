# DIP Image Viewer  
## Developer Integration Guide (v2)

---

# 🚀 Quick Start (2-Minute Integration)

### 1. Add Container

```html
<div id="dip-gallery"></div>
```

---

### 2. Include Script

```html
<script src="https://assets.dealerimagepro.com/v4/photon360script.js"></script>
```

---

### 3. Initialize Viewer

```html
<script>
document.addEventListener("DOMContentLoaded", function () {

  const viewer = window.DIP.Photon360VDP;

  viewer.init({
    dealer: "1234",
    vin: "1HGCM82633A123456",
    parentElement: "#dip-gallery"
  });

});
</script>
```

---

✅ Your viewer is now live.

---

# 🧭 Overview

DIP Image Viewer replaces your existing vehicle gallery or slider with a hosted, high-performance viewer.

### Supported Environments

- Static HTML websites  
- React / Vue / Angular (SPA)  
- Server-rendered platforms  
- Dynamic vehicle pages  

---

# 🧩 Integration Methods

---

## Method 1 — Standard Integration (Recommended)

### Before

```html
<div id="gallery">
  <!-- Existing gallery -->
</div>
```

---

### After

```html
<div id="gallery"></div>
```

---

### Initialize Viewer

```javascript
const viewer = window.DIP.Photon360VDP;

viewer.init({
  dealer: "1234",
  vin: "1HGCM82633A123456",
  parentElement: "#gallery"
});
```

---

## Method 2 — SPA Integration (React Example)

```javascript
useEffect(() => {

  const instance = window.DIP.Photon360VDP.init({
    dealer: "1234",
    vin: vin,
    parentElement: "#gallery"
  });

  return () => instance?.destroy?.();

}, [vin]);
```

---

# 🧠 Viewer Types

| Use Case | Viewer |
|----------|--------|
| Vehicle Detail Page | Photon360VDP |
| Search Results Page | Photon360SRP |

---

# ⚙️ Configuration

## Basic

```javascript
viewer.init({
  dealer: "1234",
  vin: "XXX",
  parentElement: "#gallery"
});
```

---

## Advanced

```javascript
viewer.init({
  dealer: "1234",
  vin: "XXX",
  stock: "ABC123",
  parentElement: "#gallery",
  viewer: "gallery",
  activeView: "images",
  excludeViews: "map,imperfections",
  logging: false
});
```

---

# 📌 Parameters

| Parameter | Required | Description |
|----------|----------|------------|
| dealer | Yes | Dealer ID |
| vin | Yes* | Vehicle VIN |
| stock | Yes* | Stock Number |
| parentElement | Yes | CSS selector of container |
| viewer | No | gallery / slider |
| activeView | No | Default view |
| excludeViews | No | Exclude views |
| logging | No | Debug logs |

---

### Notes

- Either `vin` or `stock` is required (VIN takes priority)  
- `parentElement` must exist before initialization  
- Viewer fully replaces container content  

---

# 📍 Understanding parentElement

Examples:

```javascript
"#gallery"        // ID selector
".image-wrapper"  // Class selector
"#main .gallery"  // Nested selector
```

⚠️ Important:

- Only first matched element is used  
- Ensure element exists before calling init()  

---

# 🔄 Replacing Existing Gallery

Before initializing DIP:

- Remove your existing gallery logic  
- Do not run both viewers together  
- Do not reinitialize original gallery  

---

# 🖥 Features Included

- Fullscreen support  
- Web Share API + fallback  
- Mobile responsive  
- Lazy loading  
- Optimized performance  

---

# 🔁 SPA Compatibility

Supports:

- Route changes  
- Component re-rendering  
- Async data loading  

✅ Best Practice:  
Always call `init()` inside component lifecycle.

---

# ⚠️ Common Issues

### Viewer Not Loading

- Check Dealer ID  
- Check VIN / Stock  
- Ensure container exists  

---

### Nothing Happens

- Script not loaded  
- init() called before DOM ready  

---

### Duplicate Viewer

- Avoid multiple init calls  
- Destroy previous instance in SPA  

---

# 🔍 Debug Mode

```javascript
viewer.init({
  dealer: "1234",
  vin: "XXX",
  parentElement: "#gallery",
  logging: true
});
```

---

# 🔐 Requirements

- HTTPS required  
- iframe embedding must be allowed  
- postMessage must not be blocked  

---

# 🆘 Support

Provide:

- Dealer ID  
- VIN / Stock  
- Website URL  
- Integration method  

---

# 🎯 Final Notes

- DIP does NOT support DOM scraping  
- Integration must use `parentElement`  
- Viewer fully controls the container  
