let loadedJSON = false;
let loadedXML = false;

function JSONLoader() {
  let requestURL = "../books.json";
  let request = new XMLHttpRequest();
  request.open("GET", requestURL);
  request.responseType = "json";
  request.send();

  request.onload = function () {
    if (!loadedJSON) {
      const catalog = request.response;
      loadJSONContent(catalog);
    }
  };
}

function loadJSONContent(obj) {
  const catalogo = obj.catalog;

  const creaTabella = document.createElement("table");
  document.getElementById("JSONContainer").appendChild(creaTabella);
  document
    .querySelector("div#JSONContainer > table")
    .setAttribute("id", "JSONContent");

  const headerTabella = document.createElement("tr");
  const headerID = document.createElement("th");
  const headerAutore = document.createElement("th");
  const headerTitolo = document.createElement("th");
  const headerGenere = document.createElement("th");
  const headerPrezzo = document.createElement("th");
  const headerDataPubblicazione = document.createElement("th");
  const headerDescrizione = document.createElement("th");

  headerID.textContent = "ID Libro";
  headerAutore.textContent = "Autore";
  headerTitolo.textContent = "Titolo";
  headerGenere.textContent = "Genere";
  headerPrezzo.textContent = "Prezzo";
  headerDataPubblicazione.textContent = "Data di Pubblicazione";
  headerDescrizione.textContent = "Descrizione";

  headerTabella.appendChild(headerID);
  headerTabella.appendChild(headerAutore);
  headerTabella.appendChild(headerTitolo);
  headerTabella.appendChild(headerGenere);
  headerTabella.appendChild(headerPrezzo);
  headerTabella.appendChild(headerDataPubblicazione);
  headerTabella.appendChild(headerDescrizione);

  document
    .querySelector("div#JSONContainer > table")
    .appendChild(headerTabella);

  // __________________________

  for (var i = 0; i < catalogo.book.length; i++) {
    const libro = document.createElement("tr");
    const idLibro = document.createElement("td");
    const autore = document.createElement("td");
    const titolo = document.createElement("td");
    const genere = document.createElement("td");
    const prezzo = document.createElement("td");
    const dataPubblicazione = document.createElement("td");
    const descrizione = document.createElement("td");

    idLibro.textContent = catalogo.book[i].bookID;
    autore.textContent = catalogo.book[i].author;
    titolo.textContent = catalogo.book[i].title;
    genere.textContent = catalogo.book[i].genre;
    prezzo.textContent = catalogo.book[i].price + "$";
    dataPubblicazione.textContent = catalogo.book[i].publish_date;
    descrizione.textContent = catalogo.book[i].description;

    libro.appendChild(idLibro);
    libro.appendChild(autore);
    libro.appendChild(titolo);
    libro.appendChild(genere);
    libro.appendChild(prezzo);
    libro.appendChild(dataPubblicazione);
    libro.appendChild(descrizione);

    document.querySelector("div#JSONContainer > table").appendChild(libro);
  }
  loadedJSON = true;
}

// _____________________________________________

function XMLLoader() {
  let requestURL = "../books.xml";
  let xhttp = new XMLHttpRequest();
  xhttp.onload = function () {
    if (!loadedXML) {
      loadXMLContent(this);
    }
  };
  xhttp.open("GET", requestURL);
  xhttp.send();
}

function loadXMLContent(obj) {
  const xmlDocument = obj.responseXML;
  const catalogo = xmlDocument.getElementsByTagName("book");

  const creaTabella = document.createElement("table");
  document.getElementById("XMLContainer").appendChild(creaTabella);
  document
    .querySelector("div#XMLContainer > table")
    .setAttribute("id", "XMLContent");

  const headerTabella = document.createElement("tr");
  const headerID = document.createElement("th");
  const headerAutore = document.createElement("th");
  const headerTitolo = document.createElement("th");
  const headerGenere = document.createElement("th");
  const headerPrezzo = document.createElement("th");
  const headerDataPubblicazione = document.createElement("th");
  const headerDescrizione = document.createElement("th");

  headerID.textContent = "ID Libro";
  headerAutore.textContent = "Autore";
  headerTitolo.textContent = "Titolo";
  headerGenere.textContent = "Genere";
  headerPrezzo.textContent = "Prezzo";
  headerDataPubblicazione.textContent = "Data di Pubblicazione";
  headerDescrizione.textContent = "Descrizione";

  headerTabella.appendChild(headerID);
  headerTabella.appendChild(headerAutore);
  headerTabella.appendChild(headerTitolo);
  headerTabella.appendChild(headerGenere);
  headerTabella.appendChild(headerPrezzo);
  headerTabella.appendChild(headerDataPubblicazione);
  headerTabella.appendChild(headerDescrizione);

  document.querySelector("div#XMLContainer > table").appendChild(headerTabella);
  console.log(catalogo);

  for (var i = 0; i < catalogo.length; i++) {
    const libro = document.createElement("tr");
    const idLibro = document.createElement("td");
    const autore = document.createElement("td");
    const titolo = document.createElement("td");
    const genere = document.createElement("td");
    const prezzo = document.createElement("td");
    const dataPubblicazione = document.createElement("td");
    const descrizione = document.createElement("td");

    idLibro.textContent = catalogo[i].id;
    autore.textContent =
      catalogo[i].getElementsByTagName("author")[0].childNodes[0].nodeValue;
    titolo.textContent =
      catalogo[i].getElementsByTagName("title")[0].childNodes[0].nodeValue;
    genere.textContent =
      catalogo[i].getElementsByTagName("genre")[0].childNodes[0].nodeValue;
    prezzo.textContent =
      catalogo[i].getElementsByTagName("price")[0].childNodes[0].nodeValue;
    dataPubblicazione.textContent =
      catalogo[i].getElementsByTagName(
        "publish_date"
      )[0].childNodes[0].nodeValue;
    descrizione.textContent =
      catalogo[i].getElementsByTagName(
        "description"
      )[0].childNodes[0].nodeValue;

    libro.appendChild(idLibro);
    libro.appendChild(autore);
    libro.appendChild(titolo);
    libro.appendChild(genere);
    libro.appendChild(prezzo);
    libro.appendChild(dataPubblicazione);
    libro.appendChild(descrizione);

    document.querySelector("div#XMLContainer > table").appendChild(libro);
  }
  loadedXML = true;
}
