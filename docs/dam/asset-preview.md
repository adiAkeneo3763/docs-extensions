# Previewing Assets

Every asset in the library can be previewed in place — no downloading, no external viewer. Images, video, audio, and PDFs each get a purpose-built viewer.

---

## Opening a Preview

Click anywhere on an asset card in the gallery to open its preview. The hover action buttons (edit, download, delete) keep working independently, so clicking a button does not open the preview.

![Asset gallery with the cursor over a card, showing the hover action buttons and the clickable card area](./assets/placeholder.png)

The preview also renders inline on the **asset edit page**, so you can see the file while you edit its tags and properties.

> [!NOTE]
> Opening a preview requires the **View** permission (`dam.asset.view`).

---

## Image Preview

Images open in a viewer with full zoom and pan support:

| Control | What it does |
|---|---|
| **Zoom in / out** | Scale the image up or down |
| **Fit** | Scale the image to fit the viewport |
| **1:1** | Reset to actual pixel size |
| **Rotate** | Turn the image 90° at a time |
| **Pan** | Click and drag to move around a zoomed image |
| **Double-click** | Toggle between fit and zoomed |

![Image preview with the zoom, fit, 1:1 and rotate controls visible in the viewer toolbar](./assets/placeholder.png)

![Image preview zoomed in, showing the panned detail of a zoomed image](./assets/placeholder.png)

![Image preview after rotating the image 90 degrees](./assets/placeholder.png)

The same zoomable viewer is used on the [public share page](./shared-links.md), so people you share a link with get the same experience.

---

## Video and Audio Preview

Video and audio files play in a custom player rather than the browser's default controls. The player provides play/pause, a scrub bar, volume, and playback speed.

![Video preview with the custom player controls — play/pause, scrub bar, volume and speed](./assets/placeholder.png)

For audio files, DAM reads the **embedded ID3 cover art** and uses it as both the asset thumbnail in the gallery and the backdrop of the audio player.

![Audio asset preview showing the embedded album cover art as the player background](./assets/placeholder.png)

---

## PDF Preview

PDFs render page-by-page inside the browser using PDF.js — you can page through the document without leaving DAM.

![PDF preview rendering the first page of a document inside the DAM preview modal](./assets/placeholder.png)

![PDF preview paged to a later page, showing the page navigation controls](./assets/placeholder.png)

---

## Thumbnails for PDFs and Videos

DAM generates **real thumbnails** for PDFs (first page) and videos (first frame) when they are uploaded. The work happens on the queue, so the thumbnail appears shortly after upload completes.

This requires two tools to be installed on the server:

| Tool | Used for |
|---|---|
| `ffmpeg` | Video first-frame thumbnails |
| `poppler-utils` (provides `pdftoppm`) | PDF first-page thumbnails |

![Asset gallery showing real first-page PDF thumbnails and first-frame video thumbnails alongside image assets](./assets/placeholder.png)

If either is missing, the gallery falls back to a generic file-type icon and a warning is written to the log — nothing breaks, you just do not get a real preview image.

![Asset gallery with ffmpeg and poppler-utils missing, showing generic file-type icons for PDF and video assets](./assets/placeholder.png)

### Backfilling existing assets

Assets uploaded before this feature existed will not have thumbnails. Generate them in bulk:

```bash
php artisan dam:backfill-thumbnails
```

See [Artisan Commands](./commands.md#dambackfill-thumbnails) for the options.

---

## Metadata

The **Metadata** tab on the asset edit page shows the technical metadata extracted from the file — dimensions, camera data, codec, duration, and so on, depending on the file type. This data is extracted once at upload and stored, so the tab loads instantly.

![Asset edit page with the Metadata tab open, listing extracted EXIF and technical metadata](./assets/placeholder.png)

> [!NOTE]
> The Metadata tab is permission-gated. A role needs **Embedded Meta Info** (`dam.asset.meta_data`) to see it.

---

## Breadcrumbs and Navigation

Both the gallery and the asset edit page show the **full ancestor path** of the asset as a breadcrumb. Every segment is a link that jumps straight to that directory.

![Asset edit page breadcrumb showing the full directory path, e.g. Root / Marketing / Campaigns / Summer](./assets/placeholder.png)

The **previous / next** arrows on the asset edit page move between assets **within the same directory**, and the position counter (`3 of 48`) reflects that directory's scope — not the whole library.

![Asset edit page with the previous/next navigation arrows and the "3 of 48" position counter](./assets/placeholder.png)

---

## Downloading

| Action | What you get |
|---|---|
| **Download** | The original file, exactly as uploaded |
| **Download Zip** | The asset packaged inside a ZIP container |
| **Custom Download** | An image converted to a chosen format (JPG, PNG, WebP, JPEG) and, optionally, resized to custom dimensions |

![Asset hover actions in the gallery, showing the Download, Download Zip and Custom Download options](./assets/placeholder.png)

![Custom Download dialog with format selection and width/height fields](./assets/placeholder.png)

Each of these is separately permissioned — see [Setup](./setup.md).

---

## Related

- [Image Editor](./image-editor.md) — cropping, adjusting, and replacing backgrounds
- [Shared Links](./shared-links.md) — letting people outside UnoPim view an asset
- [Artisan Commands](./commands.md) — thumbnail backfill
