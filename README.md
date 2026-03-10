# DIP Image Viewer

## Website Provider Integration Guide

### 1. Overview
DIP Image Viewer replaces your existing vehicle image gallery or slider with our hosted image experience.

The integration supports:

- Traditional websites
- React / Vue / Angular (SPA)
- Dynamically loaded vehicle pages
- Multiple viewers per page

No DOM scraping is used.
You explicitly control where the viewer mounts.

### 2. Integration

#### Step 1: Include Script
Add this before **</body>**:

```
<script src="https://assets.dealerimagepro.com/v4/photon360script.js" async></script>
```

#### Step 2: Initialise after page load or component mount

```
const vdpViewer = window.DIP.Photon360VDP;

vdpViewer.init({
    dealer: "<<DealerId_here>>",
    vin: "<<VIN_here>>",
    stock: "<<stockno_here>>"
    parentElement: "<<unique selector>>",
    viewer: "gallery",
});
```

#### Description

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| dealer | Number/String | Yes | Numeric Autoport ID of the dealership OR comma-seperated Autoport IDs in case of grouped dealerships. Ask the support team for this |
| vin* | String | Yes if stock not given | Vehicle Identification Number |
| stock* | String | Yes if VIN not given | Stock Number as per your IMS |
| parentElement | String | Yes | Unique HTML element selector inside which the viewer is to be loaded. (Such as ID or Class selector "#element-id", or ".class-name") |
| viewer | String | No (Default: gallery) |  **gallery** (Thumbnail Viewer)  or **slider** (Full Width Carousel Viewer) |

* vin / stock - Only one parameter is required. VIN is taking priority if both are provided

### 3. Replacing Existing Gallery

Before calling DIP Image Viewer, remove or disable your existing image gallery:
- Do not overlay both viewers
- Do not dynamically re-insert your original gallery
- DIP will fully control the container.
