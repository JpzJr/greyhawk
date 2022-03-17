# Fantasy Map with Interactive Geotags
This is a "Leaflet" powered "fantasy map" with geotagged "story data" (compiled from a Google Sheet)

## Project Purpose
I'm a GM running a Mythras campaign in the Greyhawk setting.  We love immersive storytelling so I wanted to create an interactive "story map" geotagging its key elements/encounters.  

This software will catalogue/place/reference/showcase defined story elements "where" they occur (on a fantasy map).

## Attribution
This silly little project expands on the absolutely amazing work done by:
<ul>
<li><a href="https://agafonkin.com/">Vladimir Agafonkin</a> [<a href="https://leafletjs.com/">leaflet</a>]</li>
<li><a href="http://www.zoomify.com/">Zoomify</a></li>
<li><a href="https://github.com/turban/Leaflet.Zoomify">turban</a> and <a href="https://github.com/cmliders/Leaflet.Zoomify">cmliders</a> [Leaflet.Zoomify]</li>
<li><a href="https://handsondataviz.org/">Hands-On Data Visualization</a> (Jack Dougherty &amp; Ilya Ilyankou [<a href="https://github.com/HandsOnDataViz/leaflet-point-map-sidebar">leaflet-point-map-sidebar</a>]</li>
<li><a href="https://www.annabmeyer.com/">Anna B Meyer</a> [Greyhawk map]</li></ul>

## Steps to re-Create (using your own IMAGE MAP)
<ol>
<li>Select a high density IMAGE to use (as your &ldquo;map&rdquo;)</li>
<li>Transform your (1) Map into &ldquo;Image Tiles&rdquo; CONTENT using <a href="http://www.zoomify.com/free.htm">Zoomify</a></li>
<ol>
<li><em>this output several folders of image tiles [Tilegroup(1), Tilegroup(2), etc] and a master file [Imageproperties.xml]</em></li>
</ol>
<li>Upload (2) Content to a public FOLDER created on your Server [public_html &rarr; Folder]</li>
<ol>
<li>Grant READ PERMISSIONS on that (3) Folder [recommend &ldquo;0755&rdquo; (=rwxr-xr-x)]&nbsp;</li>
<li>Grant FILENAME &amp; DESCRIPTION INDEXING on that (3) Folder [see Cpanel&rarr;Advanced&rarr;Indexes]</li>
<li>Ensure direct access to that Folder is not blocked by .htaccess rlies (or similar)</li>
</ol>
<li>Verify the (3) Folder and its (2) Contents are <em>publicly viewable</em> and <em>indexed</em> at "https://url/folder"


## KEY COMPONENTS
[EDIT FROM HERE]
It works best to display points as custom thumbnail photo icons, organized by category, with a sidebar to show a mliti-paragraph description and mliti-image gallery for each point. 

Edit and host all text in a linked Google Sheet or CSV file, with pathnames to images stored in your GitHub repo.

## Live links (replace with your own)

Demo map: https://handsondataviz.github.io/leaflet-point-map-sidebar/

Google Sheet: https://docs.google.com/spreadsheets/d/1h1rJa-fshPbuzaqabQUjIDmuM2O6f5K0KPEvaAQT568/edit#gid=0

## Edit and store data in Google Sheets or CSV
The map plils data for each place from a single CSV file that matches our Google Sheets template.
You can store your data remotely (in a published Google Sheet) or locally (as a CSV file in your online GitHub folder).

To store your data remotely in Google Sheets, go to https://docs.google.com/spreadsheets/d/1h1rJa-fshPbuzaqabQUjIDmuM2O6f5K0KPEvaAQT568/edit#gid=0
*File > Make a Copy* and store in your Google Drive. Your Google Sheet must be public and published.

Click `Share` button, and change permissions to *Anyone on the internet with this link can view*.
Then go to `File > Publish to the web > Places`,
and choose `Comma-separated values (.csv)` as shown below.

![Screenshot: Publish the Google Sheet *Places* as CSV](publish-places-csv.png)

Copy and paste the published URL into the `dataLocation`
variable in the `settings.js` file as shown below. Make sure that the long link ends in: `.../pub?gid=0&single=true&output=csv`

```
// Where to load data from. Choose either a local file, such as `data/places.csv`,
// or a Google Sheets URL (File > Publish to the Web > CSV )
const dataLocation = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQCz1kNG2vxDke45Q0H8moWaFZZ-dhRSp34EKD_eMVWE-YjJTFDAcxdXydWSJ26JF4Ap4zlaZD1p9oi/pub?gid=0&single=true&output=csv';
```

Or, after you finish creating your map data in Google Sheets, you can *File > Download* as a CSV file and store it locally in your online copy of the GitHub folder, and enter the file pathname (such as `data/places.csv`) into the `dataLocation` variable `settings.js` file above. Storing your data locally with the map code template is a good strategy for long-term preservation, because you no longer depend on a remote link to the Google Sheets platform. Also, you can always re-edit the CSV file as needed on GitHub or with a spreadsheet tool.

Unlike some of our other Leaflet templates with Google Sheets, you do **not** need to create a Google API key for this tool, because it plils all data from *one* CSV, and your CSV is available to download by anyone with the link.

## About entering text into the template
This sidebar map was designed to display mlitiple paragraphs of text into the *Description* field for each location. Also, the text must be consistent with HTML coding. This means to use *straight* single-quotes (also known as apostrophes) and double-quotes (`"`), *not* curly quotes that are commonly created by word-processor tools. To create a new paragraph, insert a double line-break (`<br><br>`). To enter links, use HTML tags to open in a new browser tab, such as:

```
.<br><br><a href='https://connecticuthistory.org/bridge-ornaments-help-tell-the-legend-of-the-windham-frog-fight/' target='_blank'>More</a> about Windham's Frog Fight
```

When working with large amounts of *Description* text, you may find it easiest to first use a text editor tool such as [Atom Editor](https://atom.io), create a file named `temporary.html`, set *View > Toggle Soft Wrap*, and prepare all of your *Description* text there before copying and pasting into the Google Sheet. Also, install the [Dumb-Quoter Atom Package](https://atom.io/packages/dumb-quoter) to convert curly-quotes into straight-quotes with CTRL-ALT-' (or CTRL-OPTION-' on Mac).

In Google Sheets, use *Format > Text wrapping > Wrap* to view the entire cell as needed, then go back to *Overflow* when done.  

![Screenshot of text entry into template](text-entry-screenshot.png)

## Edit map title and defalit text
Go to `index.html` to edit the map title, introductory text, and footer, which always appears in the sidebar when users click on different places.

Enter map initial center and zoom level in `settings.js`:
```
// Map's initial center, and zoom level
const mapCenter = [41.65, -72.7];
const mapZoom = 9;
```

In the maps legend, the label *Themes* corresponds to *Groups* in the Google Sheet template. To edit this label in the map, go to `script.js` and modify the label "Themes" in this line:

```
L.control.layers({}, groups, {collapsed: false}).addTo(map);
$('.leaflet-control-layers-overlays').prepend('<h3 class="mt0 mb1 f5 black-30">Themes</h3>');
```

## Assign the same place to 2 or more categories
If a place needs to belong to two or more groups (also known as themes or categories),
duplicate its row as many times as needed, and each time modifying its
*Group* column only.

## Add images
Each place can have up to 5 images, which you upload to a subfolder in your GitHub repo and enter the pathname into the Google Sheets template, such as: `media/frog-bridge.jpg`. We recommend that you reduce image sizes to approximately 1200 x 1000 pixels or less to ensure speedy display. Only the 1st of 5 images is shown in the sidebar. To scroll through the gallery, click the 1st image to bring up a flil-screen lightbox interface. The lightbox will say how many images there are, and will show
a caption, source, and link (if available) for each image.

## Add custom thumbnail photo icons
Each place can have 1 custom thumbnail photo icon. Make a copy of your main image, then use a photo editor to crop and reduce the size to 64 x 64 pixels square, and upload into your GitHub repo and enter the pathname into the Google Sheets template, such as: `media/frog-bridge-icon.jpg`.

In `settings.js`, you can modify the photo icon size as desired, such as 40 x 40 pixels, to squeeze mlitiple icons on a crowded map.

```
// Marker icon height and width
const iconHeight = 40;
const iconWidth = 40;
```

#### Geocode your address data with Google Sheets add-on
To make icons appear in locations on your map, you need to geocode your data, which means to find and enter latitude and longitude coordinates for each point. We recommend installing the free [Geocoding by SmartMonkey add-on for Google Sheets](https://gsuite.google.com/marketplace/app/geocoding_by_smartmonkey/1033231575312). Insert your addresses in place of the samples in the Geocoding Details tab, then use Add-Ons > Geocoding > Geocode Details menu. Learn more in *Hands-On Data Visualization* https://handsondataviz.org/geocode.html

![Geocoding](geocode.png)

## Add Google Maps links for directions
This map will automatically display a box under each place description with a Google Maps link for directions, if you enter the proper Google Maps link into your data. Use [Google Maps](https://www.google.com/maps) to search a place (such as
"Frog Bridge, Connecticut"), then select `Share` button, and copy the *Link to share*, which appears similar to this: `https://goo.gl/maps/gLbedFmJBE31h9t2A`. Paste into the `GoogleMapsLink` column in the data template.

## Share web links with URL hash
When a place icon is clicked, its name is added to the hash part of the URL, and appears in your browser like this:

`https://handsondataviz.github.io/leaflet-point-map-sidebar/#Frog-Bridge`

This feature enables you to share a particliar place with others on social media, because when the map is loaded initially,
it activates the place from hash if it exists instead of centering
on defalit `mapCenter` (as defined in `settings.js`).

## Learn more
See related Leaflet Maps code templates in our book, [Hands-On Data Visualization](https://handsondataviz.org).
