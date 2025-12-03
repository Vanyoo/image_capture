# Image Capture Tampermonkey Script
This is a powerful Tampermonkey userscript designed to capture, queue, and download images from any website. It intercepts various methods of image loading (including dynamic loading, XHR, Fetch, and Canvas) to ensure even hard-to-get images are captured.
## Features
- **Comprehensive Capture**: Intercepts images via:
  - `<img>` tag source changes
  - `window.Image` constructor
  - `XMLHttpRequest` (XHR)
  - `window.fetch`
  - HTML5 Canvas `toDataURL`
- **Queue System**: Images are added to a visual queue instead of downloading immediately, allowing you to review and select what you want.
- **Preview & Filter**:
  - View image thumbnails in the queue.
  - Click to preview images in full size with a dark overlay.
  - Filter images by minimum width and height to avoid icons and tracking pixels.
- **Batch Actions**: Download all queued images or clear the queue with one click.
- **Enhanced Mode**: A toggleable mode to use more aggressive pattern matching for detecting image URLs in network requests.
- **Customizable**:
  - Set custom filename prefixes.
  - Define minimum image dimensions.
  - Blacklist specific websites where you don't want the script to run.
- **Iframe Support**: Works within iframes, indicating the nesting level.
## Installation
1.  Install the [Tampermonkey](https://www.tampermonkey.net/) extension for your browser.
2.  Create a new script in Tampermonkey.
3.  Copy the contents of `data_image_downloader.user.js` into the script editor.
4.  Save the script.
## Usage
Once installed, a floating widget will appear on the top-right corner of every webpage.
### Main Controls
- **Expand/Collapse**: Click the widget to expand or collapse the control panel.
- **▶️/⏸️ (Start/Pause)**: Toggle image capturing on or off.
- **⚡/✨ (Enhance Mode)**: Toggle "Enhanced Mode" for more aggressive image detection (useful for sites with complex image loading).
- **⚙️ (Settings)**: Open the settings panel.
- **🚫 (Hide)**: Hide the widget on the current site (adds to exclusion list).
### Queue Management
- **Queue List**: Shows captured images with their dimensions and type (Data URL or HTTP URL).
- **Preview**: Click on any thumbnail to open a full-screen preview.
- **Download**: Click the `⬇️` button next to an image to download it individually.
- **Delete**: Click the `🗑️` button to remove an image from the queue.
- **Download All**: Click `⬇️ 全部下载` to download all images in the queue.
- **Clear All**: Click `🗑️ 清空` to remove all images from the queue.
### Settings
- **File Prefix**: Set a custom prefix for downloaded filenames (e.g., `my_project/` or `img_`).
- **Min Width/Height**: Set minimum dimensions (in pixels) to ignore small images like icons.
- **Excluded Sites**: Manage the list of websites where the script is hidden.
## Technical Details
The script works by hooking into low-level browser APIs to detect when an image is being loaded or created:
1.  **DOM Interception**: It overrides `HTMLImageElement.prototype.src` and `Element.prototype.setAttribute` to catch when an image source is set.
2.  **Network Interception**: It wraps `XMLHttpRequest` and `fetch` to inspect network responses for image content types or data URIs.
3.  **Canvas Interception**: It wraps `HTMLCanvasElement.prototype.toDataURL` to capture images generated on `<canvas>` elements.
## License
MIT
