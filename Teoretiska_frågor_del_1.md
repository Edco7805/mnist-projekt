# Del 1 - Teoretiska frågor

Denna del syftar till att visa att du förstår vissa grundläggande och centrala koncept inom maskininlärning som är en central del inom AI. Svara gärna kort och koncist.

---

## 1. Förklara vad AI, ML respektive DL är och relationen mellan begreppen.

**AI** (Artificiell intelligens): Är det breda begreppet — allt som får datorer att göra saker som annars kräver mänskligt tänkande.

**ML** (Maskininlärning): Är ett sätt att bygga AI. Istället för att programmera regler för hand låter man systemet lära sig från data.

**DL** (Djupinlärning): Är en delmängd av ML som använder neurala nätverk med många lager. Det är det som faktiskt funkar bra på bilder, tal och text idag.

**Relationen:** DL , ML , AI — all djupinlärning är maskininlärning, all maskininlärning är AI, men inte tvärtom.

---

## 2. Julia delar upp sin data i träning och test. På träningsdatan tränar hon tre modeller: "Linjär Regression", "Lasso regression" och en "Random Forest modell". Hur skall hon välja vilken av de tre modellerna hon skall fortsätta använda när hon inte skapat ett explicit "valideringsdataset"?

Julia bör använda **korsvalidering (cross-validation)** på träningsdatan — vanligast är **k-fold CV**.

Träningsdatan delas slumpmässigt i *k* delar (ofta 5 eller 10). Modellen tränas på *k−1* delar och utvärderas på den kvarvarande. Det upprepas tills varje del fungerat som "temporär test". Snittet av felen blir modellens uppskattade prestanda.

Hon gör detta för alla tre modeller, jämför t.ex. RMSE eller R², väljer vinnaren och tränar om den på **hela träningsdatan**. Testdatan rör hon inte förrän allra sist.

---

## 3. Vad är "regressionsproblem"? Kan du ge några exempel på modeller som används och potentiella tillämpningsområden?

Regressionsproblem handlar om att prediktera en **kontinuerlig** beroende variabel (Y) med hjälp av oberoende variabler (X).

**Modeller:** Linjär regression, Ridge, Lasso, Elastic Net, SVM, Beslutsträd, Random Forest, Gradient Boosting.

**Tillämpningsområden:** Bilvärdering, fastighetsvärdering, försäkringar, energiförbrukning, aktiekurser.

---

## 4. Antag att vi har följande regressionsmodell: Y = β₀ + β₁X + ε. Vad kallas Y, X, βᵢ och ε?

| Symbol | Namn | Roll |
|--------|------|------|
| Y | Beroende variabel (responsvariabel) | Det vi vill förutsäga |
| X | Oberoende variabel (prediktor) | Det vi använder för att förutsäga |
| β₀ | Intercept | Värdet på Y när X = 0 |
| β₁ | Regressionskoefficient | Hur mycket Y ändras per enhet X |
| ε | Felterm | Allt modellen inte fångar |

---

## 5. Hur kan du tolka RMSE och vad används det till?

**RMSE** (Root Mean Squared Error) är det vanligaste måttet för att utvärdera regressionsmodeller. Enheten är samma som Y — ett RMSE på 50 000 kr i en husprismodell betyder att modellen i snitt missar med ±50 000 kr.

Används för att jämföra modeller och följa upp om prestanda försämras över tid. Stora fel straffas hårdare än små (pga kvadrering).

---

## 6. Vad är "klassificeringsproblem"? Kan du ge några exempel på modeller som används och potentiella tillämpningsområden?

Klassificeringsproblem handlar om att prediktera **kategoriska** data där utfallet kan anta två eller flera klasser.

**Modeller:** Logistisk regression, KNN, SVM, Random Forest, Neurala nätverk.

**Tillämpningsområden:** Skräppostfilter, sjukvård (malign/benign), bildigenkänning, anomalidetektion, kreditrisk.

---

## 7. Vad är en "Confusion Matrix"?

En matris som visualiserar hur väl en klassificeringsmodell presterar genom att jämföra sanna och predikterade värden.

```
                  Predikterat: Ja   Predikterat: Nej
Faktiskt: Ja           TP                FN
Faktiskt: Nej          FP                TN
```

TP = sant positiv, TN = sant negativ, FP = falskt larm, FN = missad träff.

---

## 8. Hur definieras Precision? Hur tolkas Precision?

Precision defineras som andelen av de positiva preiktionerna som faktisk är korrekta, enligt formeln. 


Tolkning: Hög precision innebär att modellen sällan larmar falskt. Viktigt när ett falskt larm är kostsamt (t.ex. spamfilter som tar bort viktig mejl). Hög precision kommer ofta på bekostnad av lägre recall.

---

## 9. Hur definieras Recall? Hur tolkas Recall?



Andelen av den positiva klassen som predikteras korrekt.

Tolkning: Hög recall innebär att modellen fångar upp de flesta verkliga positiva fall (få falska negativa). Viktigt när ett missat fall är kostsamt (t.ex. cancerdiagnostik).

Precision och Recall drar ofta åt varsitt håll — höjer du ena sänker du ofta den andra.

---

## 10. Göran påstår att datan antingen är "ordinal" eller "nominal". Julia säger att detta måste tolkas. Vem har rätt?

Julia har rätt.(Det beror på kontexten). Nominal vs ordinal är inte en egenskap hos datan i sig, utan hos hur vi väljer att använda den. Färger är nominala i allmänhet, men i ett specifikt sammanhang kan en ordning finnas. Bra datavetenskap kräver att man förstår domänen, inte bara kodar variabeltyper mekaniskt.

---

## 11. Vad är skillnaden mellan parametrar och hyperparametrar? Ge ett exempel på varje och förklara varför de inte kan optimeras på samma sätt.

Parametrar lär sig modellen själv under träning. Exempel: β₀, β₁ i linjär regression. De optimeras mot data via t.ex. MSE-minimering.

Hyperparametrar sätter man innan träning. Exempel: antalet träd i Random Forest, regulariseringsstyrkan λ i Lasso. De styr *hur* modellen lär sig, inte *vad* den lär sig.

De kan inte optimeras på samma sätt eftersom hyperparametrar inte ingår i förlustfunktionen — du kan inte derivera dig fram till dem. Istället används korsvalidering eller grid search.

---

## 12. Förklara skillnaden mellan overfitting och underfitting. Beskriv hur man kan upptäcka respektive åtgärda dem.

Underfitting  — modellen är för enkel. Fångar inte mönstret ens i träningsdatan. Låg träningsprestanda, låg testprestanda.
Åtgärd: mer komplex modell, fler features.

Overfitting — modellen har lärt sig träningsdatan utantill, inklusive bruset. Hög träningsprestanda, låg testprestanda.
Åtgärd: regularisering, mer data, enklare modell, dropout.

**Hur du upptäcker det:** Jämför tränings- och valideringsfel under träning. Stor gap = overfitting. Båda höga = underfitting.

---

## 13. Hur funkar OvO och OvR algoritmerna?

Båda löser multi-klassklassificering med binära klassificerare.

OvR (One vs Rest): Träna en klassificerare per klass — "är detta klass A eller inte?". K klasser → K modeller.

OvO (One vs One): Träna en klassificerare för varje par av klasser. K klasser → K(K−1)/2 modeller. Majoritetsröst avgör.

OvR är enklare och vanligast. OvO kan fungera bättre när träning på hela datasetet är dyrt.

---

## 14. Vad är intuitionen bakom att regularisera en modell?

En modell som får göra precis vad den vill tenderar att överanpassa. Regularisering lägger till en straffterm som håller koefficienterna små — modellen tvingas prioritera enkla förklaringar framför komplicerade.

Lasso (L₁) kan sätta koefficienter till exakt noll och fungerar som feature selection.
Ridge (L₂) krymper dem mot noll men tar sällan bort dem helt.

---

## 15. Vad är Bias-Variance Trade-off?

Ett teoretiskt resultat som säger att det totala prediktionsfelet för ny osedd data kan delas upp i tre delar:

**Totalt fel = Bias² + Varians + Irreducibelt brus**

- **Bias** = systematiskt fel. Enkel modell → hög bias.
- **Varians** = känslighet för förändringar i träningsdatan. Komplex modell → hög varians.

Du kan inte minimera båda samtidigt — tricket är att hitta balansen.

---

## 16. Varför är mer komplexa modeller inte alltid bättre?

En mer komplex modell har mer kapacitet att lära sig — men också mer kapacitet att lära sig fel saker. Med lite data lär sig en komplex modell bruset istället för mönstret. Dessutom minskar tolkbarhet, träning tar längre tid, och risken för overfitting ökar. En enklare modell som generaliserar bra slår ofta en komplex modell som inte gör det.

---

## 17. Hur skattas parametrarna β₀, β₁, …, βₚ med hjälp av MSE?


Vi väljer de β-värden som minimerar detta. Matematiskt deriverar vi MSE med avseende på varje β, sätter derivatan till noll och löser. För linjär regression ger detta en sluten lösning (OLS). För mer komplexa modeller används gradientnedstigning iterativt.

---

## 18. Varför används MSE och inte RMSE vid skattning? Vad är skillnaden?

De ger samma β-värden — att minimera MSE är identiskt med att minimera RMSE (kvadratroten är monoton). Men MSE är matematiskt bekvämare: det är deriverbart och leder till renare algebra.

RMSE är bättre för **tolkning** av resultatet (samma enhet som Y). MSE är bättre för **optimering**.

---

## 19. Vad betyder övervakad respektive oövervakad maskininlärning?

Övervakad: Varje träningsexempel har ett rätt svar. Modellen lär sig kopplingen input → output. Exempel: klassificering, regression.

Oövervakad: Ingen label. Modellen får hitta struktur på egen hand. Exempel: klustring (K-means), dimensionsreduktion (PCA), anomalidetektion.

---

## 20. Vad är prediktions- respektive konfidensintervall? Vilket är bredast och varför?

Båda uttrycker osäkerhet, men för olika saker.

**Konfidensintervall** — osäkerheten kring *medelvärdet* av Y för ett givet X. Hur säkra är vi på regressionslinjens position?

**Prediktionsintervall** — osäkerheten kring ett *enskilt nytt värde* av Y. Inkluderar även den naturliga variationen (ε).

Prediktionsintervallet är alltid bredare — det handlar om en individ, inte ett genomsnitt, och individer varierar mer än medelvärden.
