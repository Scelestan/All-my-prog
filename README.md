# All-my-prog Html

        CRITJS matrice front interface

        There are a front, back, full stack and full interface matrice and also full compiled release...

        initialise a page for the prog-ramme
        var ok = prog("page1", 1, 1);
        the parameter is the name, the ratio of the size relative to the window like 1 = 100%
        prog(nameOfInstance, width, height)

        make an other instance :
        var ok2 = prog("page2", 1, 1);

        add a cadre like a object it enter in a all instance size...
        ajoue = ok.cadreGeometry("Cadre"); 
        you can parameter in latlng :
        cadreGeometry(NameCadre, left, bottom, width, height); 

        same for the other instance...
        var ajoue2 = ok2.cadreGeometry("Cadre");
        two cadre can be loaded in the same time, but don't name your "Cadre" with the same name if is so...

        you can load your item to display, the matrice can load lot of item.
        ajoue.plusItem("item1", 40, 40, 20, 20);
        ajoue.plusItem("item1-2", 10, 10, 20, 20);
        ajoue.plusItem("item1-3", 70, 70, 20, 20);
        in lat lng :
        plusItem(NameItem, left, bottom, width, height); 

        Put an item in an other instance :
        ajoue2.plusItem("item2", 40, 40, 20, 20);

        Change the color of the anthities. (default : rgba(0,0,0,0))
        ajoue.changeCouleur("item1", "white"); 
        ajoue.changeCouleur("Cadre", "yellow"); 
        ajoue2.changeCouleur("item2", "blue"); 
        ajoue2.changeCouleur("Cadre", "red"); 

        Define click, when click in item1, the page load in the div name CritJS the instance "page2" like ok2
        ajoue.definirClique("item1", "this_CritJS_page2");

        Or define click for your personnalise function :
        ajoue2.definirClique("item2", "this*function_clickItem(this)");

        Change the Z-index :
        ajoue.changeOrdre("Cadre", "-5");
        ajoue.changeOrdre("item1", "50");
        ajoue2.changeOrdre("Cadre", "-5");
        ajoue2.changeOrdre("item2", "2");

        Use html in an item :
        ajoue2.utiliserHTML("item2", "<p style='font-size:30px; position:absolute; left:40%; top:40%;'>Tu as bien cliqué !</p>");

        Just the most complicate, you can attribute an inscrutation of a color in an item when the user click one time, and if out his cursor of the item, the item is reset.
        Here is use for reset an item3 it display after a click in item1, but the two item have the same position..
        ajoue.definirContour("item1", "mouse*DIVitem3_rgba(15,25,15,1)_page1");

        Compilation of the geojson in geostring, now after this command the instance exist for the calcul :
        ok.ajouterGeometry("page1", ajoue.GeoString());
        ok.ajouterGeometry("page2", ajoue2.GeoString());

        activate this calcul... :
        charge = ok.Activer(); 

        And finaly load the page1 in a div name CritJS (this div is create if don't exist)
        charge.ChargerPage("CritJS", "page1", true, true);

        for zoom :
        ok.autoZoom(true);

        for resize :
        charge.autoRedimention(false, "CritJS");


        Exemple for the next :



        function clickItem(Element) {
        Element.innerHTML = "<button onclick='secondItemClick()' style='font-size:30px; color:black; text-align:center;'>Validation</button>";
        }
        function secondItemClick() {
        var ok3 = prog("page3", 1, 1);
        var ajoue3 = ok3.cadreGeometry("Cadre3"); 
        ajoue3.plusItem("item3", 10, 10, 80, 80);
        ajoue3.changeCouleur("item3", "purple"); 
        ajoue3.changeOrdre("Cadre3", "-5");
        ajoue3.changeOrdre("item3", "50");
        ajoue3.definirClique("item3", "this_DIVitem3_page1");
        ajoue3.definirContour("item3", "arc");
        ok.ajouterGeometry("page3", ajoue3.GeoString());
        charge.ChargerPage("CritJS", "page3", true, true);
        }


        CONVERT PNG TO GEOJSON USING SVG INDIRECTLY (in split mode)
        
//_______________________________________________________________________________________________________________________
function IMGtoGeojson(fileN) {
	
var infilepath = __dirname + '/Matrice/IMGtoGeojson/' + fileN;
var outfilepath = (__dirname + '/Adjy/ClientProjection/' + fileN + '/' + fileN + ".geojson");
 
 
fs.readFile(
        
    infilepath,
    
    function( err, bytes ){ // fs.readFile callback
        if(err){ console.log(err); throw err; }
    
        var reader = new PNGReader(bytes);
    
        reader.parse( function( err, png ){ // PNGReader callback
            if(err){ console.log(err); throw err; }
            
            // creating an ImageData object
            var myImageData = { width:png.width, height:png.height, data:png.pixels };
         

            // tracing to SVG string
            var options = { scale:1, strokewidth:0.1, ltres:12, qtres:12, pathomit:12 }; // options object; option preset string can be used also
            
            var svgstring = ImageTracer.imagedataToSVG( myImageData, options );
			
			svgstring = svgstring.split('Z " />');
			
			var geojsonA = `{
"type":"Collection",
"name":"XML_doss",
"crs":{"type":"name","utilisation":{"name": "CritCanvas"}},
"item":[`;
			for (var t = 0; t < svgstring.length-1; t ++) {
				geojsonA += `{"type":"Feature","utilisation":{"id":"${t}","route":"null","couleur":"`;
				geojsonA += svgstring[t].split('d="M')[0].split('<path fill="')[1].split('" stroke="')[0];
				geojsonA += `","utiliser":"","contour":null,"Ordre":"0"},"geometry":{"type":"Polygon","coordinates":[[`;
				console.log(svgstring[t].split('d="M')[1]);
             var test = '[' + svgstring[t].split('d="M')[1].replace(/ L /g, '],[').replace(/ Q /g, '],[').replace(/ Z M /g, '],[').replace(/ Z /g, '],[').replace(/\s/g, ',-') + ']';
			 
			 var test3 = test.split('[,-');
			 
			 for (var l = 0; l < test3.length-1; l ++) {
			 test = test.replace('[,-', "[").replace(',-]', ']').replace('--', '');
			 }
			 var test4 = test.split('],[')[0];
			 for (var l1 = 0; l1 < test.split('],[').length-1; l1 ++) {
				 if (test.split('],[')[l1].split(',').length == 2 || test.split('coordinates":[[').length == 2) {
			var test2 = '],[' + test.split('],[')[l1];
			test2 = test2.replace(',[[', ',[');
			test4 += test2;
				 }
			 }
			 test4 += '],[' + test.split('],[')[test.split('],[').length-1];
			  
			  geojsonA += test4;
			  if (t == svgstring.length-2) {
				  geojsonA += `]]}}
				  ]
}`;
			  } else {
			  geojsonA += `]]}} ,
 `;
			}
			}
			 var geojsonB = JSON.parse(geojsonA);
			 
			 for (var a = 0; a < geojsonB.item.length; a ++) {
			 for (var aa = 0; aa < geojsonB.item[a].geometry.coordinates[0].length; aa ++) {
			 geojsonB.item[a].geometry.coordinates[0][aa][0] = (geojsonB.item[a].geometry.coordinates[0][aa][0]*0.00008)+4.6325;
			 geojsonB.item[a].geometry.coordinates[0][aa][1] = (geojsonB.item[a].geometry.coordinates[0][aa][1]*0.00008)+43.9925;
			 }
			 }
			 geojsonB = JSON.stringify(geojsonB).replace(/utilisation/g, "properties").replace(/item/g, "features").replace(/CritCanvas/g, "urn:ogc:def:crs:OGC:1.3:CRS84");
			 var test2 = new Buffer.from(geojsonB);
            // writing to file
			if (fs.existsSync(__dirname + '/Adjy/ClientProjection/' + fileN)) {
  console.log('The path exists already.');
} else {
  fs.mkdir(__dirname + '/Adjy/ClientProjection/' + fileN, (err) => {
    
            fs.writeFile(
                outfilepath,
                test2,
                function(err){ if(err){ console.log(err); throw err; }

var solution = fs.readFileSync(__dirname + '/Parsing/sources/client.html').toString().replace(/\*\*\*\*/g, fileN);
var solut = new Buffer.from(solution);

fs.writeFile((__dirname + '/Adjy/ClientProjection/' + fileN + '/' + fileN) + ('.html'), solut, (err) => {
  if (err) console.log(err);
	console.log("one record created html for " + fileN);

GeoJsonLoad(fileN);
HtmlLoad(fileN);
ArrOfProject.push(fileN);
	AOPsave();
  });
  
	

				console.log( outfilepath + ' was saved!' ); }
            );
            if (err) console.log(err);
  });
}
        });// End of reader.parse()
        
    }// End of readFile callback()
    
);// End of fs.readFile()
}
