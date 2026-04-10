python 3.13.12

# Examen arbete ML 
## Fråge ställning (Fick Betyg G)
Case: California Housing – modellering som beslutsunderlag

Introduktion
Du arbetar som dataanalytiker på ett konsultbolag som hjälper kommuner och fastighetsaktörer att fatta datadrivna beslut. Ni har fått tillgång till ett dataset som beskriver områden i Kalifornien (geografi, hushåll, inkomst m.m.).
Ledningen vill använda ML som beslutsstöd. Det betyder att de inte bara vill ha “en modell”, utan ett underlag som:
går att köra om (reproducerbart),
visar hur du utvärderat på ett rimligt sätt,
och förklarar varför du valt vissa metoder.
Du ska därför leverera:
en körbar ML-lösning (kod)
och en kort, tydlig rapport (beslutsunderlag)


Dataset
Använd filen: housing.csv (California Housing)

Notera: vissa variabler är aggregerade per område (inte per enskilt hus)
Kolumner (förklaring):
longitude: longitud (geografisk position öst/väst)
latitude: latitud (geografisk position nord/syd)
housing_median_age: medianålder på bostäder i området
total_rooms: totalt antal rum i området (summerat över hushåll)
total_bedrooms: totalt antal sovrum i området (summerat över hushåll)
population: total befolkning i området
households: antal hushåll i området
median_income: medianinkomst i området (skalat mått i datasetet)
ocean_proximity: kategorisk variabel som beskriver närhet till hav (t.ex. INLAND/NEAR OCEAN)
median_house_value: medianvärde på bostäder i området (detta är target i spår A)

Vissa kolumner är “råa totalsummor”. Ofta kan man skapa mer informativa features som “rooms per household” genom att ta total_bedrooms / households.

Alla ska använda samma dataset.


Leverans
Du ska lämna in två filer via github:
Notebook (.ipynb)
innehåller all kod + figurer + resultat
ska kunna köras “Restart & Run All” utan fel
Rapport (PDF, 1–2 sidor)
kort beslutsunderlag (för chef/kollega)
innehåller: mål, metod, resultat, rekommendation, risker
Filnamn (förslag):
ML_Uppgift1_<Förnamn_Efternamn>.ipynb
ML_Uppgift1_<Förnamn_Efternamn>.pdf

Spår B – Klassificering (identifiera “högpris-områden”)

Bakgrundshistoria
 Kunden vill bygga ett verktyg som kan användas när ett nytt område (eller ett område som inte är analyserat ännu) dyker upp. De har tillgång till områdets egenskaper (geografi, hushåll, inkomstnivåer osv.) men de vet inte bostadsvärdet än.
 För att prioritera var man ska lägga tid och resurser vill de kunna få en snabb klassning: ”ser detta ut som ett högpris-område?”

Uppdrag
Skapa en binär target high_value i historisk data:
high_value = 1 om median_house_value ligger i topp 20%
annars 0
Träna en modell som förutsäger high_value utifrån X-variablerna (t.ex. median_income, geografi, hushållsvariabler, ocean_proximity, osv.)
När du tränar modellen får du bara använda X-variablerna (alla kolumner utom median_house_value och din target high_value)

Viktigt
 När modellen används på nya områden finns inte median_house_value tillgängligt.
 Därför får median_house_value inte ingå som input-feature i klassificeringen (den används endast för att skapa target i träningsdatan).

Syfte
Att kunna prioritera områden och resonera om vilka typer av fel som är mest problematiska (t.ex. missa ett högpris-område vs flagga ett område i onödan).
Målet är inte att gissa priset, utan att snabbt flagga områden som sannolikt är högpris så att teamet kan prioritera.

Vad ska göras (gäller båda spår) – krav för G
Du ska genomföra ett komplett ML-flöde och kunna motivera dina val.

1) Dataförståelse & EDA (kort men relevant)
 Krav:
Visa datasetets storlek, datatyper och vilka features som finns.
Kontrollera saknade värden och beskriv kort hur du hanterar dem.
Minst 2 relevanta figurer/tabeller + kort tolkning.

2) Split + preprocessing
 Krav:
Dela datan i train och test.
Klassificering: använd stratifierad split (stratify) så att klasserna fördelas rimligt i train/test.
Preprocessing ska göras på ett sätt som undviker att testdata påverkar träningen.

3) Modellering
 Krav:
Skapa en baseline.
Träna minst två ytterligare modeller (totalt minst 3 inkl baseline).
Jämför modellerna med en tydlig utvärderingsmetod (t.ex. cross-validation eller valideringsupplägg).

4) Välj och optimera en modell
 Krav:
Välj en modell baserat på din jämförelse.
Optimera den valda modellen med hyperparameter-tuning (t.ex. GridSearchCV). Du väljer själv vilka parametrar som är relevanta
Beskriv kort vad du optimerade och vilken metric du optimerade mot.

5) Slutlig utvärdering på testdata + rekommendation
 Krav:
Utvärdera din slutliga modell på testdata och rapportera resultatet.
Välj minst en relevant metric och motivera valet:
Regression: t.ex. MAE eller RMSE
Klassificering: t.ex. F1 eller recall/precision
Sammanfatta resultat tydligt (tabell rekommenderas).
Skriv en kort rekommendation: vilken modell skulle du ta vidare och varför?

6) Rapport (PDF, 1–2 sidor)
 Krav:
Du ska lämna in en rapport enligt ramen under “Rapport – struktur”.

Rapport (PDF, 1–2 sidor) – struktur
Rapporten ska vara tydlig och följa denna mall:

1) Mål & valt spår
Vad vill “kunden/företaget” kunna göra?
Vilket spår valde du och varför?

2) Kort data-insikt (EDA)
2–3 observationer du gjorde om datan (med stöd av någon figur/tabell)

3) Metod (ML-flöde)
Beskriv kort varför vi har ett testset och hur du använder det.
Hur du delade data (train/test) och hur du utvärderade
Vilka modeller du testade och varför (kort)
Vilken metric du utvärderade/optimerade mot och varför

4) Resultat
Jämförelse av modeller (kort)
Resultat efter tuning av vald modell
Slutlig test-prestanda

5) Rekommendation
Vilken modell du rekommenderar och varför (koppla till metric + syfte)

6) Risker & begränsningar
Vad kan gå fel i verkligheten? (t.ex. datakvalitet, generalisering, leakage, tolkning)

7) Oövervakad inlärning
 Redogör kort för:
vad oövervakad inlärning är
när det är relevant i det här caset
vad PCA respektive klustring är till för
två risker/fallgropar
 För VG: redogörelse + din implementation (PCA eller KMeans) och kort tolkning.

8) Självreflektion
Vad gjorde du bra? Vad var svårast?
Vilket betyg (G eller VG) tycker du din inlämning motsvarar? – Motivera genom att hänvisa till konkreta krav (G/VG) i kursplanen du uppfyllt
Självskattningen påverkar inte betyget i sig, men hjälper dig visa att du förstår kraven.
