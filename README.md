<!--
REQUIREMENTS:
The use of heading tags, colored text, a background color or picture, a link out to a page about your “something”.

My Discord is:
ζ͜͡๖ۣmysteriou็็็s็็็ss#4579
-->

<html>
    <head>
        <title>School Project - Dictionary</title>
        <style>
        body {
          background-image: url("https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ73TAWf396mhyY5VC_TD9uwf6hBMKC-fwn0A&usqp=CAU");
          background-size: 100% 100%;
          font-family: verdana;
          color: blue;
        }
        
        button {
          height: 30px;
          width: 75px;
          background-color: grey;
        }
        
        input {
          height: 30px;
          width: 500px;
          background-color: grey;
          color: white
        }
        
        input::placeholder{
          color: white;
        }
        </style>
    </head>
    <body>
        <script>
          function httpGet(theUrl)
          {//this func is from https://stackoverflow.com/questions/247483/http-get-request-in-javascript
              var xmlHttp = new XMLHttpRequest();
              xmlHttp.open( "GET", theUrl, false ); // false for synchronous request
              xmlHttp.send( null );
              return xmlHttp.responseText;
          }
          
          function Define() {//regex : \"definition\":\"[^,]*\",\"example
            document.getElementById('worddefinition').innerHTML = "Uh oh, Somethings wrong..."; // this'll appear if something i didnt write the code to handle happens or if theres nothing in the input box
            var request_body = httpGet("https://api.dictionaryapi.dev/api/v2/entries/en/" + document.getElementById('inputbox').value);
            if (request_body.includes("\"No definitions found\"")) {
            	document.getElementById('worddefinition').innerHTML = "Word/Definition not found.";
            }
            
            var split_body = request_body.split('"');
            var Output = "<b><p>Definitions:</p></b>";// p tag inside a p tag whatever, it works. idk if its bad practice or not.
            var DefinitionCount = 1;
            for (let index = 0; index < split_body.length; ++index) {
              if (split_body[index] == "definition") {
              	Output = Output + DefinitionCount + ". " + split_body[index + 2] + "<br><br>";
                DefinitionCount++;
              }
            }
            document.getElementById('worddefinition').innerHTML = Output;
          }
        </script>
        
        <center>
          <h1>School Project - Dictionary</h1>
          <hr>
          <br>
          <a href="https://www.merriam-webster.com/">Link to a dictionary</a>
          <br><br>
          <input id="inputbox" type="text" placeholder="Enter word to define here">
          <button id="definebutton" onclick="Define()">Define</button>
          <br>
          <p id="worddefinition"></p>
        </center>
    </body>
</html>
