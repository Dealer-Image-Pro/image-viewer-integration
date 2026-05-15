# DIP Image Viewers

Dealer Image Pro eliminated photo pixelation. Unlike traditional photo feeds that compress images, this viewer delivers sharp, full-resolution photos directly from Autoport®—fast, flawless, and true to life. The result is uniform photos making SRPs and VDPs that shine online, giving the website a professional look, and empower customers to make great buying decisions.

DIP Image Viewer replaces your existing vehicle gallery or slider with a hosted viewer.

Supports:

- Static HTML
- React / Vue / Angular
- SPA / Dynamic pages
- Multiple vehicles (SRP)

### Viewer Types

| Use Case                               | Type         | Viewer          |
| -------------------------------------- | ------------ | --------------- |
| Vehicle Detail Page (Single Vehicle)   | Photon360VDP | Gallery, Slider |
| Search Results Page (Vehicle Listings) | Photon360SRP | SRP             |

## 🚀 Quick Start

1. Include Script

```html
<script src="https://assets.dealerimagepro.com/v4/photon360script.js"></script>
```

2. Select container to load viewer on your website (example html)

   2.1 VDP

   ```html
   <div id="dip-vdp"></div>
   ```

   2.2 SRP

   ```html
   <div class="vehicle-card">
     <div class="vehicle-image"></div>
     <div class="vehicle-info">
       <div class="quick-view-btn"></div>
     </div>
   </div>
   ```

3. Initialize Viewer (Basic Example)

   3.1 VDP Gallery (Single image with thumbnails)

   ```html
   <script>
     document.addEventListener('DOMContentLoaded', function () {
       const vdpGallery = window.DIP.Photon360VDP;

       vdpGallery.init({
         dealer: '123',
         vin: 'XXXXXXXXXXXXXXXXX',
         parentElements: '#dip-vdp'
       });
     });
   </script>
   ```

   3.2 VDP Slider (Full width)

   ```html
   <script>
     document.addEventListener('DOMContentLoaded', function () {
       const vdpSlider = window.DIP.Photon360VDP;

       vdpSlider.init({
         dealer: '123',
         vin: 'XXXXXXXXXXXXXXXXX',
         parentElements: '#dip-vdp',
         viewer: 'slider'
       });
     });
   </script>
   ```

   3.3 SRP

   ```html
   <script>
     document.addEventListener('DOMContentLoaded', function () {
       const srpViewer = window.DIP.Photon360VDP;

       srpViewer.init({
         dealer: '123',
         vin: 'XXXXXXXXXXXXXXXXX',
         parentElements: '.vehicle-card',
         buttonElements: '.quick-view-btn'
       });
     });
   </script>
   ```

✅ Your viewer is now live.

## 🧩 VDP Integration

#### Gallery

Following example try to load gallery viewer of single vehicle in provided elements in "parentElement". No need to pass "viewer" parameter as gallery is default.

```javascript
const vdpGallery = window.DIP.Photon360VDP;

vdpGallery.init({
  dealer: '123',
  vin: 'XXXXXXXXXXXXXXXXX',
  parentElements: '#gallery,.vdp-gallery-div'
});
```

#### Slider

```javascript
const vdpSlider = window.DIP.Photon360VDP;

vdpSlider.init({
  dealer: '123',
  vin: 'XXXXXXXXXXXXXXXXX',
  parentElements: '#slider-div',
  viewer: 'slider' // Requied to display full width slider
});
```

## 🧩 SRP Integration (Listing Page)

SRP works differently — it integrates into each vehicle card.

#### 🔧 Required Elements

Each vehicle item must have:

1. **Parent Container** (vehicle card)
2. **Image Element** (thumbnail to replace)
3. **Button Element** (quick view trigger)

#### Example HTML Structure

```html
<div id="srp_123XXX" class="vehicle-card">
  <div id="img_123XXX" class="vehicle-image"></div>

  <div class="vehicle-info">
    <div id="btn_123XXX" class="quick-view-btn"></div>
  </div>
</div>
```

#### SRP Initialization Example

```javascript
const srpViewer = window.DIP.Photon360SRP;

srpViewer.init({
  dealer: '123',
  vin: 'XXXXXXXXXXXXXXXXX',
  parentElements: '.vehicle-card,#srp_123XXX',
  imageElements: '.vehicle-image,#img_123XXX',
  buttonElements: '.quick-view-btn,#btn_123XXX'
});
```

#### 🧠 How It Works

First it will decide the first element that exists on the page for each of the selector provided in `parentElements`, `imageElements` and `buttonElements`.

Then for each selected `parentElement`:

- DIP replaces selected `imageElement` with viewer thumbnail
- DIP injects viewer trigger inside selected `buttonElement`
- Clicking button opens viewer

## ⚙️ Configuration

| Parameter      | Required  | Applies To | Description                                                                                                                                                                                                                  |
| -------------- | --------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| dealer         | Yes       | VDP, SRP   | Numeric Autoport ID of the dealership OR comma-seperated Autoport IDs in case of grouped dealerships. Ask the support team for details `dealer:"123,45,678"`                                                                 |
| vin            | Yes\*     | VDP, SRP   | Vehicle VIN `vin: "YOUR_VEHICLE_VIN_HERE"`                                                                                                                                                                                   |
| stock          | Yes\*     | VDP, SRP   | Stock Number `stock: "STXXX"`                                                                                                                                                                                                |
| parentElements | Yes       | VDP, SRP   | Comma-seperated list of elements where viewer will be places. Such as ID or Class selectors "#element-id,.class-name". It will try to load viewer in one of the element found first. `parentElements:".hasPhotos,.noPhotos"` |
| replaceParent  | No        | VDP        | Replace everything in parent container of parentElement. `replaceParent: true` (Default false)                                                                                                                               |
| imageElements  | Yes (SRP) | SRP        | Comma-seperated list of elements where thumbnail will be placed `imageElements: ".srp_image_div"`                                                                                                                            |
| buttonElements | Yes (SRP) | SRP        | Comma-seperated list of elements where quick view buttons will be placed. `buttonElements: ".srp_button_div"`                                                                                                                |
| viewer         | No        | VDP        | **gallery** (Thumbnail Viewer) <br>or <br>**slider** (Full Width Carousel Viewer) `viewer: slider`                                                                                                                           |
| logging        | No        | VDP/SRP    | Debug logs                                                                                                                                                                                                                   |

---

<!-- | activeView     | No        | VDP        | Default view which will be active when the viewer loads |
| excludeViews   | No        | VDP/SRP    | Views will not be displayed in the image viewer | -->

### Notes

- Either `vin` or `stock` is required (VIN takes priority)
- `parentElements` must exist before initialisation
- For SRP, selectors must be relative to each vehicle card
<!-- - **Allowed values for activeView/excludeViews** - images, exterior360, interior360, video, window-sticker, map, imperfections. -->

#### 📍 Element Selector Examples

```javascript
'#gallery'; // ID Selector
'.vehicle-card'; // Class Selector
'.card .image'; // Nested selector
```

#### Advanced Options

```javascript
dipViewer.init({
  dealer: '123',
  vin: 'XXXXXXXXXXXXXXXXX',
  stock: 'ABCXXX',
  parentElements: '.viewer-div,#my-viewer',
  replaceParent: true // VDP only to replace parent element of provided selector
});
```

#### 🔍 Debug Mode (VDP/SRP)

```javascript
dipViewer.init({
  dealer: '123',
  vin: 'XXXXXXXXXXXXXXXXX',
  parentElements: '#gallery',
  logging: true
});
```

## 🔄 Replacing Existing Gallery

Before initializing DIP:

- Remove existing gallery logic
- Do not run both viewers
- Do not reinitialize original gallery

## 🖥 Features Included

- Fullscreen
- Web Share API
- Mobile responsive
- Lazy loading
- Optimized performance

## 🔁 SPA Compatibility

Supports:

- Route changes
- Component re-rendering
- Dynamic vehicle loading

✅ Best Practice:  
Call `init()` after component mount.

## ⚠️ Common Issues

###### Viewer Not Loading

- Check Dealer ID
- Check VIN / Stock
- Ensure container exists

###### SRP Not Working

- Ensure selectors are correct
- Ensure elements exist inside each card
- Ensure multiple cards are present

###### Duplicate Viewer

- Avoid multiple init calls
- Destroy previous instance in SPA

## 🔐 Requirements

- HTTPS required
- iframe allowed
- postMessage not blocked

## 🆘 Support

Provide:

- Dealer ID
- VIN / Stock
- Website URL
- Integration type (VDP Gallery, VDP Slider or SRP)

## 🎯 Final Notes

- DIP does NOT support DOM scraping
- Integration must use explicit selectors
- Viewer fully controls target elements
