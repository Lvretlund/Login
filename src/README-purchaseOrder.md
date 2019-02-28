När vi läser in sidan purchaseOrder så körs ett automatiskt ajaxanrop som använder referensnumret i urlen (som motsvarar orderns ID) för att hämta just denna order. 
Ordern sparas och hanteras som {{purchaseOrder}}
Vi har ett statuskort där vi visar upp lite information om själva statusen. 
Därefter ligger två ikoner som möjliggör att antingen ändra status till Approved, eller Closed
Dessa ikoner är synliga baserat på vad vi kunde se verkade rimligt i maximo, vi provade lite för varje statustyp för att se om man kunde approva eller closea dem.
Detta sköts via en if else sats som kollar vad purchaseOrder.status är , och baserat på detta sätter den iconernas properties för style till ="display: none;"

Detta ´sköts via ett polymervärde på iconerna som heter {{shouldShow}} och {{shouldShow2}}, och ändrar dessa till "none" baserat på if else satsen.
Detta sköts i sin tur i våra statiska get properties(), där vi säger att dessa "placeholders", eller värden är av typen String och reflekterarattributen vi ger dem.

Just nu kommer ett knapptryck på en av iconerna att ändra statusen efter att man sedan klickat spara knappen. Ett sätt att komma runt detta skulle kunna vara
att simulera ett knapptryck på save knappen i statusändringens funktion.

efter ikonerna ligger en liknande dom-repeat template som i purchaseOrders. Skillnaden här är att varje item är en poline från ordern. 
Dessa får varsit kort med lite data vi valt att visa upp. Eftersom vi här hämtar hela ordern är vi inte begränsade av _urlParams i vilken data vi vill visa så som vi var
i purchaseOrders

Vi använder numeriska inputs för att ändra Quantity för enskilda order lines, detta kan göras genom att skriva in siffror, eller använda pilarna med musklick. 


När sparknappen klickas körs getsavebody funktionen, som ändrar  bodyn för ordern, vi kollar hur många polines det finns, och för varje linje hämtar vi in polinenum, och 
quantity, sen sparar vi över detta i bodyn (detta görs för varje linje) , därefter sparas bodyn och sparfunktionen kallas på.
denna i sin tur kör getsaveHeaders där vi läser in headers som "properties: *", och x-method-override = PATCH, patchtype = merge för att kunna spara över 
data i maximo. Därefter kör kallar vi på ajaxmetoden för att spara ordern, och skickar ett post anrop med dessa ovan angivna headers, och den modifierade bodyn för ordern. 

Anledningen till att statusen inte ändras utan sparknappen är för att vi i denna funktion ändrar bodyn, och vi läser här också in huruvida statusen blivit
modifierad och ändrar då detta i bodyn. 


Vi kör felmeddelanden utifrpn maximos respons på detta anrop, antingen ett success eller error meddelande. 

Den bortkommenterade koden är kvar utifall att vi skulle vilja återgå till att ändra statusar via en dropdown meny. 