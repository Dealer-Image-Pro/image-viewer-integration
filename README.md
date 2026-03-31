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

##### a. VDP Viewer

```
const vdpViewer = window.DIP.Photon360VDP;

vdpViewer.init({
    dealer: "<<DealerId_here>>",
    vin: "<<VIN_here>>",
    stock: "<<stockno_here>>"
    parentElement: "<<unique selector>>",
    viewer: "gallery",
    activeView: "images",
    excludeViews: "<<List of views to be>>"
});
```

##### b. SRP Viewer

```
const srpViewer = window.DIP.Photon360SRP;

srpViewer.init({
    dealer: "<<DealerId_here>>",
    vin: "<<VIN_here>>",
    stock: "<<stockno_here>>"
    parentElement: "<<unique selector>>",
    excludeViews: "<<List of views to be>>",
    buttonElement: "<<unique selector to place Quickview button or icons>>",
    imageElement: "<<unique selector to replace thumbnail>>"
});
```

#### Description

| Attribute     | Type          | Viewer   | Required               | Description                                                                                                                              |
| ------------- | ------------- | -------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| dealer        | Number/String | VDP, SRP | Yes                    | Numeric Autoport ID of the dealership OR comma-seperated Autoport IDs in case of grouped dealerships. Ask the support team for this      |
| vin\*         | String        | VDP, SRP | Yes if stock not given | Vehicle Identification Number                                                                                                            |
| stock\*       | String        | VDP, SRP | Yes if VIN not given   | Stock Number as per your IMS                                                                                                             |
| parentElement | String        | VDP, SRP | Yes                    | Unique HTML element selector inside which the viewer is to be loaded. <br>(Such as ID or Class selector "#element-id", or ".class-name") |
| viewer        | String        | VDP      | No (Default: gallery)  | **gallery** (Thumbnail Viewer) <br>or <br>**slider** (Full Width Carousel Viewer)                                                        |
| activeView    | String        | VDP      | No                     | The initial view to be displayed. (Default: images)                                                                                      |
| excludeViews  | String        | VDP, SRP | No                     | Comma seperated views to be excluded from viewer.                                                                                        |
| buttonElement | String        | SRP      | Yes                    | Unique HTML element selector inside which the Quick View button or Icons to be loaded.                                                   |
| imageElement  | String        | SRP      | No                     | Unique HTML element selector to replace thumbnail. It can be image or div                                                                |
| logging       | Boolean       | VDP, SRP | No                     | To print extra logs in browser console for development purpose. Omit in production.                                                      |
|               |

- **vin / stock** - Only one parameter is required. VIN is taking priority if both are provided
- **Allowed values for activeView/excludeViews** - images, exterior360, interior360, video, window-sticker, map, imperfections.

### 3. Replacing Existing Gallery

Before calling DIP Image Viewer, remove or disable your existing image gallery:

- Do not overlay both viewers
- Do not dynamically re-insert your original gallery
- DIP will fully control the container.
