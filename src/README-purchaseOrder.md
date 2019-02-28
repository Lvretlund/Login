N�r vi l�ser in sidan purchaseOrder s� k�rs ett automatiskt ajaxanrop som anv�nder referensnumret i urlen (som motsvarar orderns ID) f�r att h�mta just denna order. 
Ordern sparas och hanteras som {{purchaseOrder}}
Vi har ett statuskort d�r vi visar upp lite information om sj�lva statusen. 
D�refter ligger tv� ikoner som m�jligg�r att antingen �ndra status till Approved, eller Closed
Dessa ikoner �r synliga baserat p� vad vi kunde se verkade rimligt i maximo, vi provade lite f�r varje statustyp f�r att se om man kunde approva eller closea dem.
Detta sk�ts via en if else sats som kollar vad purchaseOrder.status �r , och baserat p� detta s�tter den iconernas properties f�r style till ="display: none;"

Detta �sk�ts via ett polymerv�rde p� iconerna som heter {{shouldShow}} och {{shouldShow2}}, och �ndrar dessa till "none" baserat p� if else satsen.
Detta sk�ts i sin tur i v�ra statiska get properties(), d�r vi s�ger att dessa "placeholders", eller v�rden �r av typen String och reflekterarattributen vi ger dem.

Just nu kommer ett knapptryck p� en av iconerna att �ndra statusen efter att man sedan klickat spara knappen. Ett s�tt att komma runt detta skulle kunna vara
att simulera ett knapptryck p� save knappen i status�ndringens funktion.

efter ikonerna ligger en liknande dom-repeat template som i purchaseOrders. Skillnaden h�r �r att varje item �r en poline fr�n ordern. 
Dessa f�r varsit kort med lite data vi valt att visa upp. Eftersom vi h�r h�mtar hela ordern �r vi inte begr�nsade av _urlParams i vilken data vi vill visa s� som vi var
i purchaseOrders

Vi anv�nder numeriska inputs f�r att �ndra Quantity f�r enskilda order lines, detta kan g�ras genom att skriva in siffror, eller anv�nda pilarna med musklick. 


N�r sparknappen klickas k�rs getsavebody funktionen, som �ndrar  bodyn f�r ordern, vi kollar hur m�nga polines det finns, och f�r varje linje h�mtar vi in polinenum, och 
quantity, sen sparar vi �ver detta i bodyn (detta g�rs f�r varje linje) , d�refter sparas bodyn och sparfunktionen kallas p�.
denna i sin tur k�r getsaveHeaders d�r vi l�ser in headers som "properties: *", och x-method-override = PATCH, patchtype = merge f�r att kunna spara �ver 
data i maximo. D�refter k�r kallar vi p� ajaxmetoden f�r att spara ordern, och skickar ett post anrop med dessa ovan angivna headers, och den modifierade bodyn f�r ordern. 

Anledningen till att statusen inte �ndras utan sparknappen �r f�r att vi i denna funktion �ndrar bodyn, och vi l�ser h�r ocks� in huruvida statusen blivit
modifierad och �ndrar d� detta i bodyn. 


Vi k�r felmeddelanden utifrpn maximos respons p� detta anrop, antingen ett success eller error meddelande. 

Den bortkommenterade koden �r kvar utifall att vi skulle vilja �terg� till att �ndra statusar via en dropdown meny. 