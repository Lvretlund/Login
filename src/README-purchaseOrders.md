N�r purchaseOrders modulen l�ser in s� k�rs ett automatisk ajaxanrop som h�mtar alla purchaseOrders, ifr�n ..//maximo/oslc/os/mxpo. 
De h�mtas utifr�n funktionen _urlParams, som tar in sidonumret och anv�nder det i sin query. 

Queryn sker utifr�n parametrarna pageSize, select, collectioncount, where, pageno (h�r skickas sidonumret in f�r att ge oss vald sida) och lean(f�r att underl�tta framtagandet)
Detta sker via ett get anrop, vi h�mtar json data som sedan sparas som {{purchaseOrders}}. 

Dessa ordrar behandlar vi sedan i en template av typen dom-repeat, vilket l�ter oss g�ra samma sak f�r varje item av purchaseOrders. 
Vi skapar ett kort f�r varje order, och visar data om den ordern p� kortet (Vilken data som �r tillg�nglig best�ms i _urlParams under oslc.select satsen, detta
d� vi inte vill h�mta mer data �n n�dv�ndigt). 

Vi har felhantering som sker vid _onError i ajaxanropet, detta �r taget ifr�n exempelprojektet och inget vi �ndrat. Vid error displayar vi det felmeddelande eventet
h�mtar fr�n maximo, och �r detta undefined k�rs "could not authenticate the user".
Vi k�r ocks� en _handleResponse funktion som k�rs n�r ajaxanropet svarats p�, och som kollar antalet sidor och antalet items. 

Detta anv�nder vi sedan i sidor�kningen, d�r vi f�r nextpage satte en gr�ns att om current page == max antal sidor och man k�r n�sta igen s� f�r man sida 1.
P� previous page k�rde vi currentpage-1, s� l�nge den var mer �n 0 vilket g�r att vi stannar p� sida 1.