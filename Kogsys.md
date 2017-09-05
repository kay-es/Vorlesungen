# 1. Signalverarbeitung

## 1.2 Faltung
Bei der faltung kann die Funktion, die über die andere geschoben wird, als konstant mit dem entsprechenden Intervallwert gesehen werden. Beispielsweise g(t) = {2 für 0 <= t < 1 | 0 sonst} wird ganze Zeit die 2 genommen, da diese sich ja nicht im Intervall mehr befindet durch das verschieben. Integral wird dann durch Mulitplikation berechnet.

# 2. Klassifikation und Machine Learning
## 2.1 Gauß'sche Normalverteilung
Für jede Person, die einen beschriebenen Versuch durchführt, lässt sich eine spezifische Wahrscheinlichkeitsdichtefunktion beschreiben:
$$
f(x | \mu, \sigma^2) = \frac{1}{\sqrt{2 \pi \sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}
$$

wobei:
- \mu der **Mittelwert** oder die Erwartung der Verteilung ist (aber auch der Median und Mode).
- \sigma ist due **Standardabweichung**
- \sigma^2 ist die **Varianz**

Gausverteilung:
$$
p(x|\omega_1) \tilde{} N(\mu; \sigma^2) 
$$

## 2.2 Maximum Likelihood-Methode

Für den Mittelwert gilt:
$$
\mu_n = \frac{1}{n} \sum_{i=0}^nx_i
$$
Für die Varianz gilt:
$$
\sigma^2_n = \frac{1}{n} \sum_{i=0}^n(x_i- \mu)^2
$$

## 2.3 Bayes-Klassifikator
Posteriori-Wahrscheinlichkeit:
$$
P(\omega_c | x) = frac{p(x|\omega_c)P(\omega_c)}{p(x)}
$$

## 2.4 Fehlerwahrscheinlichkeit
Wahrscheinlichkeitsdichtefunktion:
$$
P_{Fehler}(\theta) = \int_{\theta}^{\infty} p(x|\omega_1)P(\omega_1) dx + \int_{-\infty}^{\theta} p(x|\omega_2)P(\omega_2) dx
$$

Der optimale Schwellwert $\theta_{opt}$ liegt an der Stelle an der sich die Fehlerwahrscheinlichkeitsfunktionen kreuzen. Der richtige Wert kann auch über eine grafische Darstellung am Schnittpunkt der beiden Funktionen abgelesen werden:  
$$
p(x|\omega_1)P(\omega_1) \overset{!}{=} p(x|\omega_2)P(\omega_2)
$$
*Grafisch bestimmen*:

1. Zeichnen eines geeigneten Koordinatensystems
2. $p(x|\omega_1)P(\omega_1) $ einzeichnen und danach $p(x|\omega_2)P(\omega_2)$ 
3. Schnittpunkt grafisch ermitteln => $\theta_{opt}$ 

In Klausur:

- *"Berechnen Sie die minimale Fehlerwahrscheinlichkeit, die durch eine geeignete Wahl des Schwellwertes bei der Klassifikation möglich ist."*
- $P_{Fehler}(\theta) = \int_{b}^{c} p(x|\omega_1)P(\omega_1) dx + \int_{a}^{b} p(x|\omega_2)P(\omega_2) dx  $ 
  - wobei a, b, c die grenzen der form sind die durch den Schnittpunkt entsteht

## 2.5 Berechnung des Kleinsten möglichen Klassifikationsfehler

Die minimale Fehlerwarscheinlichkeit taucht dann auf, wenn der Grenzwert optimal ist: $\theta_{opt}$.

=> Somit müssen wir $P_{Fehler}(\theta_{opt})$ berechnen. Die Standardnormalverteilung lautet: 
$$
\Phi_{0,1}(z) = \frac{1}{\sqrt{2\pi}}\int_{-\infty}^{z}e^{-\frac{1}{2}t^2}dt
$$
Anwendungsbeispiel: 

​	**$Geg.: \theta_{opt} = 1.1\\ $**
$$
\begin{equation} \label{eq1}
\begin{split}
 P_{Fehler}(\theta_{opt}) & = \int_{\theta_{opt}}^{\infty} p(x|\omega_1)P(\omega_1) dx + \int_{-\infty}^{\theta_{opt}} p(x|\omega_2)P(\omega_2) dx \\
& =\frac{3}{5}\int_{1.1}^{\infty} \frac{1}{\sqrt{2\pi}} e^{-\frac{(x+1)^2}{2}} dx + \frac{2}{5}\int_{-\infty}^{1.1} \frac{1}{\sqrt{2\pi}} e^{-\frac{(x-3)^2}{2}} dx \\ 
& = \frac{3}{5}\frac{1}{\sqrt{2\pi}}\int_{1.1+1}^{\infty} e^{-\frac{x^2}{2}} dx + \frac{2}{5} \frac{1}{\sqrt{2\pi}}\int_{-\infty}^{1.1 - 3} e^{-\frac{x^2}{2}} dx \\ 
& =\frac{3}{5}(1-\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{2.1} e^{-\frac{x^2}{2}} dx) + \frac{2}{5}(1- \frac{1}{\sqrt{2\pi}}\int_{-\infty}^{1.9} e^{-\frac{x^2}{2}} dx)\\
& = \frac{3}{5}(1-\Phi(2.1)) + \frac{2}{5}(1- \Phi(1.9)) \\ 
&  \overset{(1)}{\approx} \frac{3}{5}(1-0.98) + \frac{2}{5}(1- 0.97) \\ 
& = \frac{3}{5}\cdot0.02 + \frac{2}{5}\cdot0.03 \\ 
& \approx 0.022
\end{split}
\end{equation}
$$
(1) In Liste unter https://de.wikipedia.org/wiki/Tabelle_Standardnormalverteilung#Fl.C3.A4cheninhalte_unter_dem_Graphen_der_Standardnormalverteilung nachschauen.



Die **Wahrscheinlichkeitsdichtefunktion** ist immer nur eine Schatzung, die der realen Verteilung möglichst nahe kommen soll, sie aber nicht perfekt abbildet. Somit kann die tatsächliche Fehlerrate höher ausfallen als die errechnete wenn zu wenige oder verzerrte Messdaten vorliegen. 

## 2.6 K-Nearest Neighbors

- nicht parametrisch im Gegensatz zu Gauß
- Einfach, häufig ohne Lernschritt

*Algorithmus*:

- Find k closest samples (using some distance measure) 
- decide the class with the largest samples
- Beispiel
  - Euklidischer Abstand

  - K = 1 => Kreis , K = 5 => Kreuz

    ​

## 2.7 Perzeptronen

- Einfacher Perzeptron und linear separierbar 
- ein einfacher Perzeptron ist eine Funktion mit n-Parametern $(x_1,x_2,…,x_n)$
  - $g(x) = w_0 + \sum_{i=1}^{n}w_ix_i$
  - Wird zur Klassifizierung von Paaterns verwendet, die linear separierbar sein sollen???
- Für 2-dimensionale Inputdaten kann das Perzeptron als Linie im Kartesischen Koordinaten System gezeichnet werden
  - $g(x) = w_1x_1+ w_2x_2 + b$



### Klausuren-Fragen

Aufgaben:

- Nach Bayer-Klassifikations-Regel Klasse bestimmen, für die x=… präzidiert ist
  $$
  \begin{equation}
  \begin{split}
  p(x|\omega1)P(\omega1) & <> p(x|\omega2)P(\omega2)\\
  \frac{1}{3}\frac{1}{\sqrt{2\pi}}e^{-\frac{x^2}{2}} & <> \frac{2}{3}\frac{1}{\sqrt{2\pi}}e^{-\frac{(x+1)^2}{2}}\\
  e^{\frac{2x+1}{2}} & <> 2\\
  \end{split}
  \end{equation}
  $$
  Wenn $x=0.5$ ist, dann ist $e > 2$ und somit wird x der Klasse 1 zugeschrieben.

Fragen:

- Welche Methoden gehen von einer zugrundeliegenden Wahrscheinlichkeitsverteilung aus?
  - Gauß'scher Bayer-Klassifikator
- Welche Lernverfahren erfordern vorklassifizierte Trainings-Daten?
  - Fisher-Linear Discriminant
  - Gauß-Klassifikator
- Welche Eigenschaften gelten für einen Autoencoder?
  - unüberwacht
  - Nicht-parametrisch
- Überwachtest und unbewachtes Lernverfahren:
  - Überwacht: Neuronale Netze, k-Nearest Neighbours
  - Unüberwacht: k-means
- Was ist mit dem Begriff "overfitting" gemeint?
  - Durch zu häufige Trainingsiterationen lernt der Klassifikator die Trainingsdaten auswendig. Als Folge davon klassifiziert er die Trainingsdaten sehr gut, versagt allerdings auf ungesehene Daten.
  - *Lösung*: Testen des Klassifikator nach jeder Trainingsiteration auf ungesehene Testdaten. Training abbrechen, sobald die Klassifikationsleistung auf den Testdaten schlechter wird.

###Neuronale Netze

Künstliche Neuronale Netze bestehen aus Neuronen -> Neuronen sind nicht-lineare Funktionen

Wobei $x_j $ die Aktivierung ist: $\sum_i x_i \cdot w_i$ 

Die Komponente, welche für die Nicht-linearität zuständig ist, ist die Aktivierungsfunktion (oder auch Entscheidungsfunktion) der einzelnen Perzeptionen. Für diese wird im Allgemeinen eine nichtlineare Funktion gewählt. Beispiele hierfür sind: Schrittfunktion, Threshold-Logik, logistische Funktion (Auch Sigmoid-Funktion oder Log-Sigmoid-Funktion genannt), Tanz-Funktion (auch Tan-Sigmoid-Funktion genannt) und die Softmax-Funktion.

Wünschenswerte Eigenschaften sind Monotonie und Ableitbarkeit.

Wichtigste Parameter:

- Gewichte
- Schwellwert



#### Fragenkatalog

- Einteilung von Klassifikationen: Welche Art von Klassifikator ist ein Perzeptron?
  - Klasse Perzeptron
    - Ein Perzeptron ist ein statischer, überwachter, nicht-parametrischer und linearer Klassifikator
- Gehören, die in der VL vorgestellten Multi-Layer-Perzeptrons zur selben Klasse wie das Perzeptron?
  - Klasse Multi-Layer-Perzeptron
    - MLPs gehören nicht zur selben Klasse wie einzelne Perzeptrone, da sie nichtlineare Klassengrenzen lernen können und somit statistiche, überwachte, nicht-parametrische und nicht-lineare Klassifikatoren sind. 
- Wie kann die Ausgabe von MLPs statisch interpretiert werden?
  - Die Ausgabe eines MLP kann als A-Posteriori Wahrscheinlichkeit interpretiert werden.

# 3. Grundlagen der Bildverarbeitug

# 3.1 Lochkamera

Berechne Zunächst $\frac{Pixel}{mm}$ indem man Breite und Höhe vom CCD-Chip zu deren CCD-Zellen nimmt und so die Höhe und Breite des Pixels berechnet. Beispiel: CCD-Chip mit 3mm x 4mm Größe und 750 x 1000 CCD-Zellen => Ein Pixel ist $\frac{3 mm}{750} = \frac{4 mm}{1000} = 0,004 mm$ hoch und breit.

###Aufgabe

a) Bei der Aufgabe, dass man den Bildpunkt $p(u,v)$ mit $u, v \in \mathbb{R}$  der linken Kamera, auf den ein gegeber Punkt P(X,Y,Z) abgebildet wird, berechnen soll: 
$$
\left( \begin{array}{c}u\\v\end{array} \right) = \frac{f}{Z}\left( \begin{array}{c}X\\Y\end{array} \right)
$$
b) Linke Kamera liefert irgendeinen Bildpunkt $p_l(u,v)$ (Beispielsweise $p_l(40, -100)$ Pixels). Man soll die Gerade $g_l$ im Koordinatensystem der linken Kamera für alle Punkte berechnen, die sich auf den Bildpunkt $p_l$ abbilden. Das Gleiche für $g_r$ mit gegeben Bildpunkt $p_r$.

Beispiel: 

- Gegeben: $p_l = (40, -100)$, $p_r = (-20, -100)$, $f=5 mm$   
- Gesucht: $g_l$, $g_r$

$$
g_l: \vec{x}= \left( \begin{array}{c}X\\Y\\Z\end{array} \right) = \frac{Z}{f} \left( \begin{array}{c}u_l\\v_l\\0\end{array} \right) + \left( \begin{array}{c}0\\0\\Z\end{array} \right) =  \frac{Z}{f} \left( \begin{array}{c}u_l\\v_l\\f\end{array} \right) =  \frac{Z}{5mm} \left( \begin{array}{c}40 Pixel\\-100 Pixel\\5mm\end{array} \right) =  \frac{Z}{5mm} \left( \begin{array}{c}\frac{40pixel}{250 \frac{Pixel}{mm}}\\\frac{-100pixel}{250 \frac{Pixel}{mm}}\\1 mm\end{array} \right) \\
=Z\left( \begin{array}{c}0,032mm\\-0,08mm\\1 mm\end{array} \right)
$$

$$
g_r: \vec{x}= \left( \begin{array}{c}X\\Y\\Z\end{array} \right) = \frac{Z}{f} \left( \begin{array}{c}u_l\\v_l\\0\end{array} \right) + \left( \begin{array}{c}0\\0\\Z\end{array} \right) =  \frac{Z}{f} \left( \begin{array}{c}u_l\\v_l\\f\end{array} \right) =  \frac{Z}{5mm} \left( \begin{array}{c}-20 Pixel\\-100 Pixel\\5mm\end{array} \right) =  \frac{Z}{5mm} \left( \begin{array}{c}\frac{-20pixel}{250 \frac{Pixel}{mm}}\\\frac{-100pixel}{250 \frac{Pixel}{mm}}\\1 mm\end{array} \right) \\
=Z\left( \begin{array}{c}-0,016mm\\-0,08mm\\1 mm\end{array} \right)
$$

c) Bestimmen der Koordinatentrafo vom rechten Kamerakoordinatensystem in Weltkoordinatensystem. Danach $g_r$ im Weltkoordinatensystem. Anschließend Schnittpunkt S von $g_l$ mit $g_r$ .



- $g_l$ ist bereits im Weltkoordinatensystem definiert, da das Koordinatensystem der linken Kamera mit dem Weltkoordinatensystem identisch ist.

  - $g_l = l\left( \begin{array}{c}0,032mm\\-0,08mm\\1 mm\end{array} \right)$

- $g_r$ muss ins Weltkoordinatensystem transformiert werden, wobei die Orientierung gleich bleibt. Jedoch ist eine translative Koordinatentransformation notwendig, um die Verschiebung relativ zur linken Kamera zu berücksichtigen
  $$
  f: \mathbb{R}^3 \rightarrow   \mathbb{R}^3 \\
  \vec{x} \rightarrow \vec{x} + \left( \begin{array}{c}100\\0\\0\end{array} \right)
  $$
  Somit ist $g_r: \vec{x} = \left( \begin{array}{c}100\\0\\0\end{array} \right) + \mu \left( \begin{array}{c}-0,016mm\\-0,08mm\\1 mm\end{array} \right)$

  Gleichsetzen der im Weltkoordinatensystem definierten Gerade $g_l$ und $g_r$ ergibt:

$$
\lambda \left( \begin{array}{c}-0,0032mm\\-0,08mm\\1 mm\end{array} \right) = \left( \begin{array}{c}100\\0\\0\end{array} \right) + \mu \left( \begin{array}{c}-0,016mm\\-0,08mm\\1 mm\end{array} \right)
$$

Daraus ergibt sich $\lambda = \mu$  => $\lambda \cdot 0,032 = 100 - 0,016 \cdot \lambda $ => $\lambda \approx 2083,3$ und somit ergibt sich der Schnittpunkt zu:
$$
S =  \left( \begin{array}{c}66,7\\-166,7\\2083,3\end{array} \right)
$$
d) Es kommt zu **Bildrauschen**. Somit wird der Punkt $p'_l$ mit entsprechender Gerade $g'_l$ statt $p_l$ berechnet. 

Antwort:

Das hat zur Folge , dass sich die Geraden $g'_l$ und $g_r$ nicht exakt in einem Punkt schneiden, sondern windschief sind. Der optimal Schnittpunkt S' kann beispielsweise als Mittelpunkt der kürzesten Verbindungsstrecke zweier windschiefer Geraden berechent werden, über die Lösung eines LGS. 

Allgemein gilt:
$$
g_l: \vec{x} = \vec{a} + r\vec{u}\\ g_r: \vec{x} = \vec{b} + s\vec{v}
$$
Gleichsetzen von $g_l$ und $g_r$
$$
\vec{a} + r\vec{u} = \vec{b} + s\vec{v}
$$
=> 
$$
r\vec{u} - s\vec{v} = \vec{b}-\vec{a}
$$
=>
$$
\vec{b} - \vec{a} =  \left( \begin{array}{c}u_1 - v_1\\u_2 - v_2\\u_3 - v_3\end{array} \right) \left( \begin{array}{c}r\\s\end{array} \right)
$$
Mit
$$
A:= \left( \begin{array}{c}u_1 - v_1\\u_2 - v_2\\u_3 - v_3\end{array} \right), \vec{x}:=\left(\begin{array}{c}r\\s\end{array}\right), b :=\vec{b} - \vec{a}
$$
Ist Ax = b ein überbestimmtes LGS, dessen optimale Lösung $x_{opt}$ im Sinne der euklidischen Norm beispielsweise durch Lösung der Normalengleichung $A^TAx_{opt} = A^Tb$ zu   $x_{opt} =(A^TA)^{-1} A^Tb$ berechnet werden kann. Mit $(r_{opt}, s_{opt}) = x_{opt}$ lässt sich der Punkt mit geringstem Abstand zu beiden Geraden berechnen zu:
$$
S' = \frac{a+r_{opt}\cdot u+ b + s_{opt}\cdot v}{2}
$$

##### Transformation des Weltkoordinatensystems in Kamerakoordinatensystem:

$p_w$  ist in Weltkoordinatensystem =>

$p_c = R\cdot p_w + t$  wobei R die Rotation und t die Translation ist.



#### Kontrastanpassung

a) Berechnen des Ergebnisbild nach ausführung einer Spreizung für die Bildmatrix B.

- Wenn sowohl die Intensität 0 als auch 255 vorhanden ist macht die Spreizung nichts und B' = B.

b) Histogramm H(x)

- Einfach Häufigkeiten der Intensitäten
- akkumulierte Histogramm $H_a(x)$ 
- Quantil $H_q(p) = H_a(x) \ge p \cdot H_a(q)$ wobei q der höchste Wert ist, den $H_a(x)$ annehmen kann.
- $I'(u,v) = aI(u,v) + b$ wobei $a = \frac{q}{H_q(p_{max}) - H_q(p_{min})}$ und $b = \frac{q\cdot H_q(p_{min})}{H_q(p_{max}) - H_q(p_{min})}$ 



c) Ergebnisbild nach Ausführung eines Histogrammausgleichs auf B:

- $H_n(x) = \frac{hösteIntensität}{H_a(hösteIntensität)} \cdot H_a(x)$  

####Filter

 Zeigen dass Filtermatrix Approximation eines Gauß-Filters mit $\sigma$ ist: 

- Formel für Gaußfilter heraussuchen
  $$
  \begin{pmatrix}
  (x-1,y-1) & (x-1,y) & (x-1,y+1)\\
  (x,y-1) & (x,y) & (x,y+1) \\
  (x+1,y-1) & (x+1,y) & (x+1,y+1) \\
  \end{pmatrix}
  $$
  Beim Tiefpassfilter muss die Summe der Einträge 1 betragen.





## Morphologische Operatoren

Basis-Operatoren:

- **Dilatation**: Aufblasen des Objektes, vergrößert Pixel zu größeren Bereichen
- **Erosion**: Schrumpfen des Objektes, entfernt vereinzelte Pixel und schwach zusammenhängende Pixelgruppen

- Öffnen-Operation: Zuerst Erosion und anschließend Dilatation verwenden
- Schließen-Operation: Zuerst 

## Hough-Transformation

- Ziel: Erkennung gerader Linien im Bild
- Ansatz: Stelle Linie durch Normalenvektor(Länge, Winkel) in Polarkoordinaten dar(Sinus/Kosinus)
- $r = x \cdot \cos(\theta) + y \cdot \sin(\theta)$ 
- Vorgehen
1. Man wählt eines der r = ... Gleichungen und setzt $\theta$ ein z.B. $\frac{\pi}{4}$
2. Danach erhält man ein r (z.B.: $r = \sin(\theta) = \sin(\frac{\pi}{4}) = \frac{1}{\sqrt(2)}$). Gleiches für $\cos(\theta)$ ($ = \frac{1}{\sqrt(2)}$).
3. Als nächstes stellt man den Vektor auf: $ g =   \left( \begin{array}{c}\frac{1}{\sqrt(2)}\\\frac{1}{\sqrt(2)}\end{array} \right)\left( \begin{array}{c}x\\ y\end{array} \right) = r (=\frac{1}{\sqrt(2)})$

## Prüfungsfragen-Theorie

### 1 Grundlagen der Bildverarbeitung

- Nennen Sie einen Kantenfilter und geben Sie dessen Filtermatrix an.

  - Sobel-X oder Prewitt-X-Filter

    - Sobel-X

    $$
    \begin{pmatrix}
    -1 & 0 &1\\
    -2 & 0 & 2 \\
    -1 & 0 & 1 \\
    \end{pmatrix}
    $$

    - Prewitt-X
      $$
      \begin{pmatrix}
      -1 & 0 & 1\\
      -1 & 0 & 1\\
      -1 & 0 & 1 \\
      \end{pmatrix}
      $$

- Welche Mindesgröße sollte die Filtermatrix eines Gauß-Filters mit Varianz $\sigma^2 = 1.5^2$ besitzen, um eine ausreichende Approximation zu erreichen?

  - ​

# Allgemeine Fragen

### Signalverarbeitung



###Logik

- Wie ist **Logik** formal definiert? Nenne alle 5 Bestandteile.
  - L = {Symbolmenge, Belegungsmenge, Syntax, Semantik, Folgerungsoperator $\models$ } 


- Wozu dient ein Voronoi-Diagramm in der Bahnenplanung?
  - Das Voronoi-Diagramm teil den Raum so in Flächen ein, dass jedes Hindernis in genau einer Fläche enthalten ist. Die Fläche enthält alle Punkte, für die dieses Hindernis das nächstgelegene ist. In der Bahnplanung wird es eingesetzt um maximalen Abstand zu Hindernissen zu halten, indem man sich entlang der Voronoi-Linien bewegt.
- Was ist das Umweltmodell eines Kognitiven Systems
  - Das Umweltmodell eines kognitiven Systems bildet die reale Umwelt auf eine innere Repräsentation ab.
- Welche Darstelungsmöglichkeiten gibt es für Objekte der realen Welt? Welche dieser Möglichkeiten eignen sich zur Abstandsberechnung zwischen den Objekten?
  - Objekte können als **Kantenmodelle, Oberflächenmodelle** oder **Volumenmodelle** dargestellt werden.
  - **Oberflächenmodelle** und **Volumenmodelle** sind zur Abstandsberechnung geeignet
- Wie ist eine Horn-Klausel definiert
  - Eine Horn-Klausel ist eine Disjunktion von Literalen, von denen höchstens eines positiv ist. Beispiel:  $(\neg P \vee \neg Q \vee R  )$ bzw. $(P \wedge Q) \Longrightarrow R$ 
- Wie sind die Knoten und Kanten eines Sichtgraphen definiert?
  - Knoten entsprechen Ecken der Hindernisse. Eine Kante zwischen zwei Knoten A und B existieren genau dann, wenn die zu Knoten B gehörige Ecke von der zu  Knoten A gehörige Ecke aus sichtbar ist.
- Was muss für die Heuristik in einem A*-Algo gelten?
  - Die Heuristik darf Distanzen unter- aber nicht überschätzen
- Wieso ist der Einsatz von Heuristiken bei vielen Planungsproblemen sinnvoll oder notwendig?
  - Durch eine Heuristik kann der Suchraum reduziert werden und die Suche somit beschleunigt werden.
- Auch beim A*-Algorithmus wird eine Heuristik verwendet. An welcher Stelle?
  - Die Heurisitk im A*-Algorithmus wird bei der Entscheidung, welcher Knoten als nächstes expandiert wird, verwendet. Sie schätzt hierbei die Kosten zum Ziel, die mit den Kosten des zurückgelegten Weges addiert werden.
- Welche Eigenschaft muss sie hierbei erfüllen, damit der A*-Algorithmus den kürzesten Weg zum Ziel tatsächlich finden kann?
  - Sie muss optimistisch sein, d.h. sie darf die tatsächlichen Kosten, die zum Ziel führen, unterschätzen, aber nicht überschätzen.

