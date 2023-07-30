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

Change the color of the anthities. (default : blue)
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
