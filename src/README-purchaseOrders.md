När purchaseOrders modulen läser in så körs ett automatisk ajaxanrop som hämtar alla purchaseOrders, ifrån ..//maximo/oslc/os/mxpo. 
De hämtas utifrån funktionen _urlParams, som tar in sidonumret och använder det i sin query. 

Queryn sker utifrån parametrarna pageSize, select, collectioncount, where, pageno (här skickas sidonumret in för att ge oss vald sida) och lean(för att underlätta framtagandet)
Detta sker via ett get anrop, vi hämtar json data som sedan sparas som {{purchaseOrders}}. 

Dessa ordrar behandlar vi sedan i en template av typen dom-repeat, vilket låter oss göra samma sak för varje item av purchaseOrders. 
Vi skapar ett kort för varje order, och visar data om den ordern på kortet (Vilken data som är tillgänglig bestäms i _urlParams under oslc.select satsen, detta
då vi inte vill hämta mer data än nödvändigt). 

Vi har felhantering som sker vid _onError i ajaxanropet, detta är taget ifrån exempelprojektet och inget vi ändrat. Vid error displayar vi det felmeddelande eventet
hämtar från maximo, och är detta undefined körs "could not authenticate the user".
Vi kör också en _handleResponse funktion som körs när ajaxanropet svarats på, och som kollar antalet sidor och antalet items. 

Detta använder vi sedan i sidoräkningen, där vi för nextpage satte en gräns att om current page == max antal sidor och man kör nästa igen så får man sida 1.
På previous page körde vi currentpage-1, så länge den var mer än 0 vilket gör att vi stannar på sida 1.