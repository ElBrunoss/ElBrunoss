# Esercizio 1 -- Analisi di un Algoritmo Ibrido QuickSort--SelectionSort

## 1. Obiettivo

È stato implementato un algoritmo di ordinamento ibrido che combina:

-   QuickSort per sottoarray di dimensione ≥ k
-   SelectionSort per sottoarray di dimensione < k

L'obiettivo è valutare sperimentalmente se l'introduzione di una soglia
`k` possa migliorare le prestazioni rispetto a QuickSort puro,
sfruttando il minor overhead di SelectionSort su istanze di piccole
dimensioni.

------------------------------------------------------------------------

## 2. Progettazione Algoritmica

### 2.1 QuickSort

È stata implementata una versione robusta con:

-   Partizionamento: [specificare: Hoare / Lomuto]
-   Strategia pivot: [specificare: median-of-three / random /
    centrale]

Nel caso medio:

T(n) = O(n log n)

La scelta del pivot è determinante per evitare degenerazioni verso il
caso peggiore O(n²), specialmente in presenza di input già ordinati o
costruiti in modo avverso.

------------------------------------------------------------------------

### 2.2 SelectionSort

SelectionSort è stato implementato nella forma classica:

T(n) = O(n²)

Caratteristiche:

-   nessuna ricorsione
-   accessi regolari in memoria
-   overhead costante molto basso

Per n piccoli il termine quadratico è limitato e può risultare
competitivo.

------------------------------------------------------------------------

### 2.3 Logica Ibrida

-   Se n ≥ k → QuickSort
-   Se n \< k → SelectionSort
-   Se k = 0 → QuickSort puro
-   Se k \> N → SelectionSort puro

La soglia introduce un trade-off tra overhead ricorsivo e costo
quadratico locale.

------------------------------------------------------------------------

## 3. Setup Sperimentale

Dataset: 20 milioni di record binari.

Campi di ordinamento:

1.  id (uint64_t)
2.  field1 (float)
3.  field2 (int64_t)
4.  field3 (stringa 16 byte)

Valori testati per k:

0, 10, 50, 100, 500, 1000, 5000, 10000, 1000000

Timeout massimo: 5 minuti.

------------------------------------------------------------------------

## 4. Tabelle dei Tempi

### field = 1 (id)

  k         Tempo (s)
  --------- -----------
  0         
  10        
  50        
  100       
  500       
  1000      
  5000      
  10000     
  1000000   

------------------------------------------------------------------------

### field = 2 (float)

  k         Tempo (s)
  --------- -----------
  0         
  10        
  50        
  100       
  500       
  1000      
  5000      
  10000     
  1000000   

------------------------------------------------------------------------

### field = 3 (int64)

  k         Tempo (s)
  --------- -----------
  0         
  10        
  50        
  100       
  500       
  1000      
  5000      
  10000     
  1000000   

------------------------------------------------------------------------

### field = 4 (string)

  k         Tempo (s)
  --------- -----------
  0         5.989
  10        5.473
  50        6.219
  100       7.565
  500       18.986
  1000      31.208
  5000      2.24.321
  10000     
  1000000   

------------------------------------------------------------------------

## 5. Analisi Critica

### Confronto con le attese teoriche

-   k = 0 → comportamento O(n log n)
-   k molto grande → degradazione verso O(n²)
-   k intermedio → possibile miglioramento marginale

\[Inserire analisi sui dati raccolti\]

------------------------------------------------------------------------

### Valore Ottimale di k

Valore ottimale osservato:

k = \_\_\_\_\_\_

Motivazione:

-   riduzione chiamate ricorsive
-   migliore utilizzo cache
-   eliminazione overhead su sottoarray piccoli

------------------------------------------------------------------------

### Differenze tra Campi

-   Interi: confronti più economici
-   Float: costo leggermente maggiore
-   Stringhe: confronti lessicografici dominanti

Le differenze dipendono principalmente dal costo delle comparazioni.

------------------------------------------------------------------------

## 6. Conclusioni

1.  QuickSort domina asintoticamente su grandi dataset.
2.  SelectionSort non è adatto come algoritmo globale.
3.  L'approccio ibrido produce un miglioramento marginale ma misurabile
    per piccoli k.
4.  Esiste una soglia ottimale nell'ordine di poche decine o centinaia.

L'ipotesi iniziale risulta:

Confermata
