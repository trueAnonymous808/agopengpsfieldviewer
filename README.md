# AgOpenGPS Field Viewer

A single-file, browser-based viewer that shows your [AgOpenGPS](https://github.com/AgOpenGPS/AgOpenGPS) fields on a map. Open a KML, an ISOXML `TASKDATA.xml` or a ZIP of fields, and see boundaries, guidance lines, recorded paths and flags in seconds. No install, no server, no build step.

<!-- Add a screenshot here: ![Screenshot](docs/screenshot.png) -->

## Features

- Opens **KML**, **KMZ**, **ISOXML (`TASKDATA.xml`)** and **ZIP** files (including a zipped AgOpenGPS `Fields` folder)
- Drag and drop, or pick several files at once
- Satellite (Esri) and street map (OpenStreetMap) base layers
- Field boundaries drawn as polygons, with names and area in hectares
- Sidebar with field list, search, click-to-zoom and total area
- Layer toggles for boundaries, AB lines, curves, recorded paths, flags and other items
- Click any item to see its field and type
- Runs entirely in your browser: **your field data is never uploaded anywhere**

## Quick start

1. Download `agopengps-field-viewer.html`.
2. Open it in any modern browser (Chrome, Edge, Firefox, Safari).
3. Click **Open files…** or drag your files onto the page.

An internet connection is needed for the map tiles and the two libraries loaded from a CDN (Leaflet and JSZip).

### Host it on GitHub Pages (optional)

1. Rename the file to `index.html` and push it to your repo.
2. Go to **Settings → Pages**, choose your branch and the root folder, then save.
3. Your viewer will be available at `https://<user>.github.io/<repo>/`.

Files you open are still processed locally in the visitor's browser.

## Supported formats

| Format | What is read |
|---|---|
| **AgOpenGPS KML** (`Field.kml`, `AllFields.kml`) | Boundaries, AB lines, curve lines, recorded path, flags. Folder structure is used to group items by field. |
| **ISOXML** (`TASKDATA.xml`) | Partfield (`PFD`) names, boundaries (`LSG` type 1), guidance patterns (`GPN`), points and lines. Comma decimals are handled. |
| **ZIP / KMZ** | Every `.kml` inside is loaded. If there is none, `TASKDATA.xml` is used (the `v4` copy is preferred, to avoid drawing a field twice from v3 and v4). |

Not supported yet: AgOpenGPS plain-text files such as `Boundary.txt`.

## How fields are matched

- **KML:** the field name is the folder that contains the category folders (`Boundaries`, `Flags`, `Recorded Path`, and so on). A KML without that structure is treated as one field named after the file.
- **ISOXML:** each `PFD` element is one field, named by its `C` attribute.

Items with the same field name from different files are merged into one entry.

## Colours

| Colour | Item |
|---|---|
| Amber | Boundary |
| Blue (dashed) | AB lines |
| Green | Curves |
| Purple | Recorded path |
| Red | Flags |
| Grey | Other |

## Notes and limitations

- Area is calculated from the outer boundary ring with a local flat-earth approximation. It is accurate for field-sized areas but is not a survey-grade figure, and inner holes are not subtracted.
- Very large recorded paths are drawn on a canvas for speed, but huge files may still be slow on older devices.
- The interface is in Hungarian. To switch language, edit the strings near the top of the `<script>` block and in the HTML.

## Built with

- [Leaflet](https://leafletjs.com/) for the map
- [JSZip](https://stuk.github.io/jszip/) for reading ZIP and KMZ files
- Map tiles by [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors and Esri World Imagery. Please respect their tile usage policies if you host this publicly with heavy traffic.

## Contributing

Issues and pull requests are welcome. Sample files from other guidance systems that fail to load are especially useful for improving the parsers.

## License

Choose a license for your repository (for example MIT) and add a `LICENSE` file.
