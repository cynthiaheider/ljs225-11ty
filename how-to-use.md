# How to Use

## Create the images TEI document

### If you already have a IIIF manifest
- tell Edition Crafter to make the TEI document based on the manifest with ```editioncrafter iiif -i <iiif_url> -o <output.xml>```

### If you don't have a manifest and want to make the TEI document from a folder of images
- gather the images together and publish them via GitHub Pages or whatever other web host you're using
- create a CSV with three columns: url, label, and xml_id
 - populate the url column with the url the images will live at when they are published/hosted
 - the label column is what you want the page named
 - xml_id is the way you'll match up the XML file texts with their images; the xml_id you create for each image will then be inserted into the TEI for each page following ```<pb facs="#[the page's xml_id]>```
- direct Edition Crafter to make the TEI document by directing it to the CSV you created with this command: ```editioncrafter images -i <images.csv> -o <output.xml>```

## Combine all your stuff into one XML file to process
- in the XML file you just created above, paste or type in the contents of your TEI files within the ```<text>``` tags. There can be multiple texts! Give them unique ```xml:id``` identifiers so they can be called up separately in the viewer
- also paste in your ```<teiHeader>``` info if you have it

## Create the IIIF manifest, HTML files, and TEI-encoded XML files
- tell Edition Crafter to process your stuff with ```editioncrafter process -i <tei_file> -o <output_path> -u <base_url>```

## Make the files appear in the Edition Crafter viewer
- add the following script to a page that you want the viewer and objects to display on:
```
 <div id="ec"></div>

 <script type="text/javascript" src="https://www.unpkg.com/@cu-mkp/editioncrafter-umd" ></script>

 <script type="text/javascript">

     EditionCrafter.viewer({
         id: 'ec',
         documentName: 'BnF Ms. Fr. 640',
         iiifManifest:'https://cu-mkp.github.io/editioncrafter-data/fr640_3r-3v-example/iiif/manifest.json',
         transcriptionTypes: {
           tc: 'Diplomatic (FR)',
           tcn: 'Normalized (FR)',
           tl: 'Translation (EN)'
         }
     });

 </script>
```
- make sure this script is **after** the ```</body>``` tag, or it will result in an error in the browser
- sub in the url of your manifest after ```iiifManifest```
- ```transcriptionTypes``` is determined by whatever ```xml:id``` values you assigned to the different texts in your generated XML file