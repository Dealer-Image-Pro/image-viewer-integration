# DIP Image Viewer  
## Developer Integration Guide (v2)

---

# 🚀 Quick Start (VDP - 2 Minutes)

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

✅ Your VDP viewer is now live.

---

# 🧭 Overview

DIP Image Viewer replaces your existing vehicle gallery or slider with a hosted viewer.

Supports:

- Static HTML  
- React / Vue / Angular  
- SPA / dynamic pages  
- Multiple vehicles (SRP)  

---

# 🧠 Viewer Types

| Use Case | Viewer |
|----------|--------|
| Vehicle Detail Page (Single Vehicle) | Photon360VDP |
| Search Results Page (Vehicle Listings) | Photon360SRP |

---

# 🧩 VDP Integration (Detail Page)

## Basic Example

```javascript
const viewer = window.DIP.Photon360VDP;

viewer.init({
  dealer: "1234",
  vin: "1HGCM82633A123456",
  parentElement: "#gallery"
});
```

---

# 🧩 SRP Integration (Listing Page)

SRP works differently — it integrates into each vehicle card.

---

## 🔧 Required Elements

Each vehicle item must have:

1. **Parent Container** (vehicle card)
2. **Image Element** (thumbnail to replace)
3. **Button Element** (quick view trigger)

---

## Example HTML Structure

```html
<div class="vehicle-card">

  <div class="vehicle-image"></div>

  <div class="vehicle-info">
    <button class="quick-view-btn">Quick View</button>
  </div>

</div>
```

---

## SRP Initialization Example

```javascript
const srpViewer = window.DIP.Photon360SRP;

srpViewer.init({
  dealer: "1234",
  vin: "1HGCM82633A123456",
  parentElement: ".vehicle-card",
  imageElement: ".vehicle-image",
  buttonElement: ".quick-view-btn"
});
```

---

## 🧠 How It Works

For each `.vehicle-card`:

- DIP replaces `.vehicle-image` with viewer thumbnail
- DIP injects viewer trigger inside `.quick-view-btn`
- Clicking button opens viewer

---

# ⚙️ Configuration

## VDP (Basic)

```javascript
viewer.init({
  dealer: "1234",
  vin: "XXX",
  parentElement: "#gallery"
});
```

---

## SRP (Basic)

```javascript
srpViewer.init({
  dealer: "1234",
  vin: "XXX",
  parentElement: ".vehicle-card",
  imageElement: ".vehicle-image",
  buttonElement: ".quick-view-btn"
});
```

---

## Advanced (VDP/SRP)

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

| Parameter | Required | Applies To | Description |
|----------|----------|------------|------------|
| dealer | Yes | VDP, SRP | Numeric Autoport ID of the dealership OR comma-seperated Autoport IDs in case of grouped dealerships. Ask the support team for this |
| vin | Yes* | VDP, SRP | Vehicle VIN |
| stock | Yes* | VDP, SRP | Stock Number |
| parentElement | Yes | VDP, SRP | Container selector where viewer will be places. Such as ID or Class selector "#element-id", or ".class-name") |
| imageElement | Yes (SRP) | SRP | Thumbnail selector |
| buttonElement | Yes (SRP) | SRP | Button selector where quick view buttons will be placed. |
| viewer | No | VDP | **gallery** (Thumbnail Viewer) <br>or <br>**slider** (Full Width Carousel Viewer) |
| activeView | No | VDP | Default view which will be active when the viewer loads |
| excludeViews | No | VDP/SRP | Views will not be displayed in the image viewer |
| logging | No | VDP/SRP | Debug logs |

---

### Notes

- Either `vin` or `stock` is required (VIN takes priority)  
- `parentElement` must exist before initialisation  
- For SRP, selectors must be relative to each vehicle card
- **Allowed values for activeView/excludeViews** - images, exterior360, interior360, video, window-sticker, map, imperfections.  

---

# 📍 Selector Examples

```javascript
"#gallery"              // ID
".vehicle-card"         // Class
".card .image"          // Nested selector
```

---

# 🔄 Replacing Existing Gallery

Before initializing DIP:

- Remove existing gallery logic  
- Do not run both viewers  
- Do not reinitialize original gallery  

---

# 🖥 Features Included

- Fullscreen  
- Web Share API  
- Mobile responsive  
- Lazy loading  
- Optimized performance  

---

# 🔁 SPA Compatibility

Supports:

- Route changes  
- Component re-rendering  
- Dynamic vehicle loading  

✅ Best Practice:  
Call `init()` after component mount.

---

# ⚠️ Common Issues

### Viewer Not Loading

- Check Dealer ID  
- Check VIN / Stock  
- Ensure container exists  

---

### SRP Not Working

- Ensure selectors are correct  
- Ensure elements exist inside each card  
- Ensure multiple cards are present  

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
- iframe allowed  
- postMessage not blocked  

---

# 🆘 Support

Provide:

- Dealer ID  
- VIN / Stock  
- Website URL  
- Integration type (VDP or SRP)  

---

# 🎯 Final Notes

- DIP does NOT support DOM scraping  
- Integration must use explicit selectors  
- Viewer fully controls target elements  
