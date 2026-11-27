# A/B test di due campagne pubblicitarie


## Domanda: 

Quale tra la campagna di controllo e la campagna di test è più efficiente nel convertire i clic in acquisti e nel ridurre il costo per acquisto?

## Dati: 

Ho preso i dati da un dataset pubblico trovato su Kaggle (https://www.kaggle.com/datasets/amirmotefaker/ab-testing-dataset) e l'analisi è stata svolta da me. In esso riguardo al gruppo test abbiamo 30 giorni di campioni, mentre per il controllo 29, ne ho tolto 1 dal controllo  (5 agosto 2019) perché non erano presenti tutti i dati necessari, era presente la spesa effettuata ma non il numero di click. Una riga è un giorno di campagna e ogni riga comprende : Campaign Name (test o controllo), Data, soldi spesi (in dollari), reach, numero di impressions, numero di click nel sito, numero di ricerche all'interno del sito, numero di contenuti visualizzati nel sito, numero di volte in cui è stato schiacciato "aggiungi al carrello", numero di acquisti 

## Metodo: 

Per svolgere questa analisi ho scelto il test di Welch,  una sottocategoria del t-test a campioni indipendenti siccome i 2 gruppi hanno deviazione standard diversa, che risponde alla domanda, quanto è probabile, per puro caso, vedere questa differenza. Per giungere alla nostra conclusione ho dovuto scrivere la seguente formula per trovare, per ogni giorno, il costo per acquisto: ---> ```python
df["costo per acquisto"] = df["Spend [USD]"] / df["# of Purchase"]
```. Con "acquisti/click" invece troviamo la conversione (il costo per acquisto era quello principale, la conversione un controllo aggiuntivo). Ho fissato la soglia di significatività solita a 0,05. Trovando una p di 0,19 (costo d'acquisto) possiamo affermare che, supponendo non ci sia una differenza reale, una differenza tra le 2 campagne grande almeno quanto quella osservata capiterebbe poco meno di 1 volta su 5. Infine ho utilizzato anche un boxplot per visualizzare anche graficamente i nostri dati riguardanti il costo per acquisto, trovando le 2 scatole molto sovrapposte

## Risultati: 
- Costo medio per acquisto: 5,05 $ contro 5,90 $, deviazioni standard 2,12 e 2,80, p = 0,19 (costo d'acquisto);
- conversione: 11,5% contro 9,2%, p = 0,14 (conversione);
- giorni per gruppo: 29 e 30.

## Conclusione: 

Il controllo ha valori leggermente migliori su entrambi gli indicatori, ma nessuna differenza è statisticamente significativa, dunque il test non è significativo (con questi dati non si può stabilire) poiché la differenza è troppo bassa tra le 2 campagne rispetto alla variabilità dei giorni, con pochi dati a disposizione, per rendere l'analisi più affidabile servirebbero più giorni di dati, o un test con utenti assegnati ai gruppi a caso.

## Limiti: 

I limiti dell'analisi sono i seguenti: pochi giorni, unità giornaliera, dati di cui non si conosce l'origine reale o simulata, i giorni non sono del tutto indipendenti, perché le due campagne girano nello stesso periodo e il t-test assume indipendenza.
**LIMITE IMPORTANTE, 
la pagina Kaggle non spiega la differenza pratica tra i metodi o la grafica delle 2 campagne.**

## Come eseguire il file:
- scarica i due CSV dalla pagina Kaggle;
- caricali su Colab o in una cartella di Drive;
- cambia il percorso nella cella di lettura.
