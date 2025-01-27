---
header-includes: |
    \usepackage{graphicx}
    \usepackage{seqsplit}
    \usepackage{fvextra}
    \DefineVerbatimEnvironment{Highlighting}{Verbatim}{breaklines,commandchars=\\\{\}}
    \usepackage{caption}
    \usepackage{subcaption}
    \usepackage{xcolor}
    \usepackage{lscape}

    \usepackage{tabularx}
    \usepackage{booktabs}
    \usepackage{caption}
    \usepackage{geometry}
    \usepackage{xltabular}

---

## Assignment 8: E91 Protocol (Q&A)

### Q1: 

Buonasera Professore,  

Avrei una domanda relativa alla CHSH inequality. Mi scuso per averle inviato la domanda tramite screenshot, ma è stato l’unico modo che ho trovato per rappresentare correttamente le formule presenti nel seguito. Nella foto che aveva condiviso sul canale principale, mostrava la formula di $S$ da utilizzare con una specifica scelta di osservabili, che riporto qui per completezza:  

$$A_1 = Z, \quad A_2 = X$$  

$$B_1 = -\frac{(Z+X)}{\sqrt{2}}, \quad B_2 = \frac{(Z-X)}{\sqrt{2}}$$  

La formula di $S$ indicata è:  
$$S = | \langle A_1 B_1 \rangle - \langle A_1 B_2 \rangle + \langle A_2 B_1 \rangle + \langle A_2 B_2 \rangle |$$  

Calcolando i valori teorici delle expectation rispetto allo stato $|\psi^-\rangle = \frac{1}{\sqrt{2}}(|01\rangle - |10\rangle)$, mi torna che $S$ venga $2\sqrt{2}$. Ho rifatto anche io tutti i calcoli su carta.  

Tuttavia, implementando l’E91 protocol su Qiskit e calcolando sperimentalmente $S$ rispetto allo stesso stato $|\psi^-\rangle$, il valore ottenuto viene diverso da quello teorico. In particolare, noto che $\langle A_1 B_1 \rangle$ e $\langle A_2 B_1 \rangle$ si avvicinano a $-\frac{1}{\sqrt{2}}$, mentre teoricamente dovrebbero essere $+\frac{1}{\sqrt{2}}$.  

Ho analizzato la situazione e osservato quanto segue:  
- Se considero $B_1 = \frac{(Z+X)}{\sqrt{2}}$, cioè senza il segno negativo, i risultati sperimentali rimangono invariati.  
- I circuiti di misura risultanti nei due casi ($B_1$ con e senza il segno negativo) sono identici a parte una fase globale di $\pi$. La fase globale è presente solo nel caso con il segno negativo, ma non dovrebbe influenzare le probabilità di misura perché dovrebbero rimanere invariate.  

Mi chiedo quindi se questa fase globale possa in qualche modo influenzare i risultati delle misure e se devo tenerne conto da qualche parte (ad esempio, invertendo il risultato della misura quando la fase globale è $\pi$).  

A questo punto, per cercare di risolvere il problema, ho deciso di considerare una nuova scelta di osservabili:  
$$A_1 = Z, \quad A_2 = X$$  

$$B_1 = \frac{(Z+X)}{\sqrt{2}}, \quad B_2 = \frac{(Z-X)}{\sqrt{2}}$$  

Questa scelta elimina il segno negativo su $B_1$. Calcolando teoricamente le expectation rispetto a $|\psi^-\rangle$, ottengo:  
$$\langle A_1 B_1 \rangle = -\frac{1}{\sqrt{2}}, \quad \langle A_2 B_1 \rangle = -\frac{1}{\sqrt{2}}, \quad \langle A_2 B_2 \rangle = \frac{1}{\sqrt{2}}, \quad \langle A_1 B_2 \rangle = -\frac{1}{\sqrt{2}}$$  

La formula di $S$, che ho visto che dipende sia dalla scelta degli osservabili che dallo stato considerato per il calcolo delle expectation, diventa:  
$$S = | \langle A_1 B_1 \rangle + \langle A_1 B_2 \rangle + \langle A_2 B_1 \rangle - \langle A_2 B_2 \rangle |$$  

Questa formula coincide anche con quella riportata su Wikipedia: (Tsirelson's bound) https://en.wikipedia.org/wiki/Tsirelson%27s_bound  

Con questa scelta, sperimentalmente ottengo valori di $S$ vicini a $2\sqrt{2}$, coerenti con la teoria.  

Un'ulteriore domanda riguarda il fatto che teoricamente $S$ dovrebbe sempre essere $\leq 2\sqrt{2}$, ma noto che i valori ottenuti sperimentalmente variano tra diverse esecuzioni: in alcuni casi sono inferiori a $2\sqrt{2}$, ma altre volte superiori. Questo comportamento è normale?  

In conclusione, le chiedo:  
1. Posso considerare la nuova scelta di osservabili e formula di $S$ per proseguire con il progetto?  
2. Oppure, vuole che utilizzi la sua scelta iniziale e devo indagare ulteriormente sulle discrepanze tra risultati teorici e sperimentali?  

La ringrazio in anticipo Professore per l’attenzione e il supporto.

Cordiali saluti, $\\$
Giovanni Ligato


### A1:
La questione è piuttosto delicata. Riguardo alla nuova scelta di osservabili e alla formula di $S$, il Professore ha detto che vanno bene. Ha aggiunto che, se non riesco a individuare la causa per cui sperimentalmente non ottengo i risultati attesi con la scelta iniziale, posso procedere utilizzando la nuova scelta. Inoltre, mi ha suggerito di provare con un nuovo stato, $|\psi^+\rangle$, per verificare cosa accade in quel caso con gli osservabili e la formula di $S$ presentati nelle slide del corso.

Per quanto riguarda il punto, più semplice, relativo alla possibilità che i risultati sperimentali superino il limite teorico di $2\sqrt{2}$, il Professore ha spiegato che ciò è normale. Questo fenomeno deriva dalla statistica e dal fatto che sto effettuando un campionamento. Di conseguenza, è normale che tra diverse esecuzioni i risultati possano variare, risultando a volte superiori o inferiori a $2\sqrt{2}$. La soluzione proposta è calcolare un intervallo di confidenza per $S$ su diverse esecuzioni e verificare se esso include il valore teorico di $2\sqrt{2}$.

---

### Q2:

Buonasera Professore,  

Tra ieri e oggi ho approfondito il problema seguendo i suoi suggerimenti. Di seguito le descrivo nel dettaglio i passi che ho seguito e i risultati che ho ottenuto.  

**1. Stato $|\psi^+\rangle$:**  
Come primo passo, ho considerato lo stato $|\psi^+\rangle$ invece di $|\psi^-\rangle$. Per semplicità, ho generato $|\psi^+\rangle$ utilizzando un Bell gate con in ingresso $|01\rangle$, per essere sicuro di avere il controllo su ogni cosa. Ho considerato gli osservabili presentati nelle slide del protocollo E91, ovvero:  

$$A_1 = Z, \quad A_2 = X, \quad A_3 = \frac{(Z+X)}{\sqrt{2}}  $$  
$$B_1 = Z, \quad B_2 = \frac{(Z-X)}{\sqrt{2}}, \quad B_3 = \frac{(Z+X)}{\sqrt{2}}  $$  

In particolare:  

- Le configurazioni $A_1B_1$ e $A_3B_3$ vengono usate per misurare nella stessa base e ottenere i valori anti-correlati per la generazione della chiave condivisa tra Alice e Bob.  
- Le altre combinazioni ($A_1B_2$, $A_1B_3$, $A_2B_2$, $A_2B_3$) sono utilizzate per il calcolo del valore di $S$.  

Con $|\psi^-\rangle$, nel passo di generazione della chiave condivisa, tutto funzionava come previsto: le misure di Alice e Bob erano anti-correlate, e la chiave risultava identica (essendo nel caso ideale).  

**2. Problema con lo stato $|\psi^+\rangle$:**  
Passando a $|\psi^+\rangle$, ho riscontrato che la chiave ottenuta da Alice e Bob era diversa, in particolare si aveno problemi quando la configurazione scelta dai due era $A_3B_3$. Nonostante numerose verifiche sul circuito e sulla corretta implementazione dell’unitaria che mappa gli autovalori dell'osservabile negli stati della base standard, ottenevo i seguenti risultati su 1000 esecuzioni del circuito:  
```
{'11': 234, '10': 244, '00': 243, '01': 279}
```  
In questo caso, i risultati non erano anti-correlati, ma tutti e quattro gli outcome si presentavano con probabilità circa uguali a $\frac{1}{4}$.  

Il circuito utilizzato per la configurazione $A_3B_3$ è riportato in Figura \ref{fig:Q2_r1}.

\begin{figure}[h!]
    \centering
    \includegraphics[width=1.0\textwidth]{resources/Q2_r1.png}
    \caption{Circuito nel caso di scelta $A_3B_3$ degli osservabili e stato $|\psi^+\rangle$}
    \label{fig:Q2_r1}
\end{figure} 

Per chiarire definitivamente la situazione, ho svolto tutti i calcoli teorici a mano. I dettagli sono riportati nelle Figure \ref{fig:Q2_sheet1} e \ref{fig:Q2_sheet2}.

\begin{figure}
    \centering
    \includegraphics[width=0.85\textwidth]{resources/Q2_sheet1.jpg}
    \caption{Calcoli teorici con $|\psi^+\rangle$ (1)}
    \label{fig:Q2_sheet1}
\end{figure}

\begin{figure}
    \centering
    \includegraphics[width=1.0\textwidth]{resources/Q2_sheet2.jpg}
    \caption{Calcoli teorici con $|\psi^+\rangle$ (2)}
    \label{fig:Q2_sheet2}
\end{figure}

I risultati teorici confermano quanto ottenuto sperimentalmente con Qiskit.  

**3. Verifica con lo stato $|\psi^-\rangle$:**  
Sono tornato quindi a considerare $|\psi^-\rangle$, con la stessa scelta di osservabili. Usando il Bell gate con in ingresso $|11\rangle$, ottenevo:  
```
{'10': 498, '01': 502}
```  
Qui, come atteso, i risultati erano perfettamente anti-correlati con probabilità $\frac{1}{2}$. Anche in questo caso, i calcoli teorici confermano i risultati sperimentali (Figura \ref{fig:Q2_sheet3}).

\begin{figure}
    \centering
    \includegraphics[width=1.0\textwidth]{resources/Q2_sheet3.jpg}
    \caption{Calcoli teorici con $|\psi^-\rangle$}
    \label{fig:Q2_sheet3}
\end{figure}

Il circuito utilizzato per questa configurazione è riportato in Figura \ref{fig:Q2_r2}.

\begin{figure}
    \centering
    \includegraphics[width=1.0\textwidth]{resources/Q2_r2.png}
    \caption{Circuito nel caso di scelta $A_3B_3$ degli osservabili e stato $|\psi^-\rangle$}
    \label{fig:Q2_r2}
\end{figure}

Quindi, la conclusione a cui sono giunto è che per la corretta esecuzione del protocollo E91 bisogna considerare lo stato $|\psi^-\rangle$ e non $|\psi^+\rangle$.

**4. Test del valore di $S$:**  
A questo punto sono passato a verificare cosa succedesse ad $S$ con lo stato $|\psi^+\rangle$. La formula che sono andato a considerare è quella presentata nelle slide, ovvero:
$$S = | \langle A_1 B_2 \rangle + \langle A_1 B_3 \rangle + \langle A_2 B_2 \rangle - \langle A_2 B_3 \rangle |  $$  

Gli osservabili a cui faccio riferimento sono sempre quelli delle slide, che ho riportato per completezza all'inizio. I risultati che ottengo sperimentalmente sono coerenti con quelli della teoria, presentati anche da lei.

```
<A1B2> = -0.709, <A1B3> = -0.697, <A2B2> = -0.746, <A2B3> = 0.661  
CHSH correlation value: 2.813  
```  

Anche in questo caso ho provato a fare un ulteriore test, aggiungendo un segno negativo a $B_3$, cioè considerando $B_3 = -\frac{(Z+X)}{\sqrt{2}}$.

I risultati sperimentali che si ottengono sono identici, come se la fase globale di $\pi$ che viene aggiunta, non modificando le probabilità di misura, dovesse essere presa in considerazione in qualche modo, magari invertendo il risultato della misura (o non saprei in che altro modo).

Perciò, credo (perché non mi viene altro in mente) che sia proprio quella fase globale che in qualche modo, venendo trascurata, porti a risultati sperimentali diversi da quelli attesi. A questo punto quindi, come mi ha suggerito anche lei, per continuare il progetto utilizzerò la nuova scelta di osservabili e la formula per $S$ proposti alla fine del mio precedente messaggio.

La ringrazio moltissimo Professore per i consigli e il supporto. Mi scuso per la lunghezza del messagio, ma ho preferito darle una visione completa per poter spiegare al meglio il problema e le mie osservazioni.

Cordiali Saluti, $\\$
Giovanni Ligato
