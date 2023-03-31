# ProjektarbeteML
Projektarbete inom maskininlärning med python

Frågor: 
Välja ett maskininlärningsproblem
Studerande har valt ett dataset som denna formulerat ett problem till. Tanken är att studerande ska försöka finna en algoritm som är välanpassad för att lösa problemet samt dokumentera problemet under pågående utveckling.

Optimera lösningen
Studerande förväntas utföra någon optimering på datasetet för att hypotetisk producera ett bättre svar. Formuleringen är hypotetisk då slumpen i somliga fall kan skapa ett sämre resultat även om optimeringen är välgrundad.

Här bör det även framgå varför en optimering görs genom användandet av grafer. Exempelvis så kan ett linjärt beroende påvisas av ett scatterplot av två features.

Leverera lösningen via ett REST API
Studerande förväntas skapa ett enklare REST API där användare kan skicka in “ny” data och få fram en förutsägelse baserat på den maskininlärningen som gjordes i steg 1 och 2.

Mina tankar i valen under denna uppgift: 

1. Jag valde detta dataset för att det var enkelt att förstå datan. Det var också rimligt mycket data vilket har varit ett problem innan och det kändes skönt att eliminera direkt. Jag såg direkt några intressanta utmaningar med detta dataset. Som att få alla värden till numeriska värden för att kunna testa olika algoritmer. Sedan att normalisera dessa värden för att få en bra vikt mellan alla features. Men också att se vilka faktorer som mest spelar in i valet av att köpa produkten eller inte. 

https://www.kaggle.com/datasets/janiobachmann/bank-marketing-dataset?datasetId=4471&searchQuery=Knn  

Jag började med att skriva ut i en dataframe för att se hur featuresen såg ut. Där såg jag direkt att det var en del data som var text och inte numerisk. Jag hittade en fin lösning via sklearn och LabelEncoder. Den behandlar datan i textform på ett bra sätt, en siffra sätts på den kategorin. I min kod så fick under arbeten Administration siffran 0, Arbetare(arbetarklassen), siffra 1, entreprenör siffra 2 osv. Detta gjorde att jag kunde använda mig av mina algoritmer och eftersom att värdena var kategoriskt behövde jag inte använda mig av normalisering på dessa värden.

Jag målade upp en heatmap över korrelationer för att se om några features hade en negativ påverkan på resultatet. Detta är ett bra sätt att måla upp features också och se deras korrelation till features men också target. Jag undersökte tabellen och tog bort några features som jag trodde kunde påverka negativt. Det resulterade i att accuracyn på RFC gick ner men steg på GNB och KNN vilket var intressant. Min tanke är då att det skapas ett mönster mellan dessa features i just RFC som gör att det blir mer träffsäkert med fler features.

2. Jag valde att normalisera datan för att de numeriska features ska ha samma vikt. Förhoppningsvis så ska detta resultera i en bättre balans mellan feautresen och därav hitta bättre och fler relevanta mönster i datasetet. Jag målade upp en boxplot för att jag själv skulle förstå mig på men också att visa upp hur datan såg ut innan och efter normaliseringen. Där fanns det en del värden som innan kan ha påverkat mer än andra så detta var ett bra och intressant beslut. Resultatet blev bättre efter normaliseringen. 

https://www.javatpoint.com/fit-transform-and-fit_transform-methods-in-python 

Sedan testade jag tre algoritmer jag valt ut då jag tänkte att de skulle passa bra på mitt dataset.







RFC: 

RFC bygger en skog med träd. Varje träd tränar på en slumpmässig del av datan. Detta resulterar i att risken för en overfitting minskar. Troligtvis fungerar detta bra för att jag använder mig av många olika features och då dras samband mellan alla olika features. Det är också troligt att det av den anledning ger mig det bästa resultatet. Jag har testat den på andra dataset men någorlunda lik data och även då fått bra resultat så därav ville jag testa den även här och återigen fick jag det bästa resultatet. 

Jag testade k-fold för att det var en teknik som var enkel att förstå sig på. Den minskar också risken för overfitting vilket är positivt. Den ger också alla observationer från den ursprungliga data en chans att få testas eller tränas med. Den formeln som fanns i dokumentation av k-fold för att skriva ut ett värde förstod jag inte exakt. Jag bröt ner den och det var framförallt 0.2f jag var osäker på. Fick fram informationen att det är ett flyttal som ska visas med 2 decimaler. Sedan kommer en tuppel som innehåller medelvärdet av poängen och det andra värdet är 2x standardavvikelsen för poängen. 

GNB: 

Gaussian Naive Bayes testade jag då jag vet att datamängden är kontinuerlig och kategorisk och denna algoritmen är bra för klassificering algoritm. Datamängden är ju inte enormt stor och vad jag kunde läsa mig till så ska algoritmen fungera på mindre data också vilket kändes rimligt. Algoritmen skall också behandla den kontinuerliga datan på ett bra sätt då den antar att de kontinuerliga variablerna är normalfördelade.

KNN:  

K Nearest Neighbor testade jag eftersom att det är en någorlunda enkel algoritm att förstå sig på och den passar också bra på klassifikationsdata. Jag har använt mig av den tidigare och förstått hur den fungerar. Det kändes skönt att komma igång med något så då tog jag den då jag vet att den passade bra på mitt dataset.  

3. Jag löste upp problemet med Flask och gjorde requesten via Postman där jag skickar in data nedanför i Json-format och får ut en prediction om “personen” köpt eller inte.  

http://localhost:5000/bank

[
    
    {"age":43, "balance": 200, "day": 8, "duration": 1040, "campaign":1, "pdays": -1, "previous": 0, "job" : 1, "marital": 1, "education": 1, "default": 0, "housing": 0, "loan": 0, "contact":2,
    "month": 8, "poutcome": 3
}


    
]


https://www.machinelearningplus.com/plots/python-boxplot/ 
https://www.analyticsvidhya.com/blog/2022/02/k-fold-cross-validation-technique-and-its-essentials/ 
https://learn.g2.com/k-nearest-neighbor
https://dataaspirant.com/gaussian-naive-bayes-classifier-implementation-python/ 
https://www.datacamp.com/tutorial/random-forests-classifier-python 
