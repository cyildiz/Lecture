---
type: lecture-cg
title: "Machine Learning 101"
author: "Carsten Gips (FH Bielefeld)"
weight: 1
readings:
  - key: "Russell2020"
    comment: "Lernen: Abschnitte 19.1 und 19.2"
assignments:
  - topic: sheet05
youtube:
  - id: FliWEXQZhsw
fhmedia:
  - link: "https://www.fh-bielefeld.de/medienportal/m/c871a589c1e95782173b9a3c1efbb79ac38dfb4d871df8b39fd5851562036619df4d6b31cec0b630c1c88ff928bbcb2429ea194e2cc795720fce214367009242"
    name: "Direktlink FH-Medienportal: KI Machine Learning 101"
---


## Was ist Lernen?

\pause

\Large

> Verhaltensänderung eines Agenten in Richtung der Optimierung eines
> Gütefunktionals (Bewertungsfunktion) durch Erfahrung.

\normalsize


::: notes
## Warum Lernen?

*   Nicht alle Situationen vorhersehbar
*   Nicht alle Details modellierbar
*   Lösung oder Lösungsweg unbekannt, nicht explizit programmierbar
*   Data Mining: Entdeckung neuen Wissens durch Analyse der Daten
*   Selbstanpassende Programme

\bigskip

=> Lernen wichtige Eigenschaft lebender Wesen :-)
:::

[[Warum Lernen?]{.bsp}]{.slides}


## Learning Agent

::: center
![](images/learning.png){width="80%"}
:::


## Feedback während des Lernens

*   **Überwachtes Lernen**
    *   Lernen durch Beobachtung
    *   Vorgabe von Beispielen:  Ein- und Ausgabewerte

    => Regression, [Klassifikation]{.alert}

\bigskip

*   **Unüberwachtes Lernen**
    *   Erkennen von Mustern in den Inputdaten, Clustering
    *   Kein Feedback (!)

\bigskip

*   **Reinforcement Lernen**
    *   Bewertung der Aktionen des Agenten am Ende einer Aktionsfolge


[Analogie Lernen beim Kleinkind]{.bsp}

::: notes
**Beispiel Kleinkind**: Lernen von Klassen/Konzepten durch Beispiele

*   Zuerst ist alles "Katze" (Übergeneralisierung)
*   Differenzierung durch Feedback der Umwelt; Erkennung unterschiedlicher Ausprägungen
:::


## Beispiel: Kreditrisiko

*   Bankkunde beantragt Kredit
*   Soll er aus Sicht der Bank den Kredit bekommen?

\smallskip

*   Bankangestellter betrachtet (relevante) Merkmale des Kunden:
    *   Alter, Einkommen, sozialer Status
    *   Kundenhistorie bei der Bank
    *   Höhe des Kredits

\bigskip

*   Bewertung des Kreditrisikos:
    *   **Klassifikation**: Guter oder schlechter Kunde  [(Binäre Entscheidung: 2 Klassen)]{.notes}
    *   **Regression**: Vorhersage Gewinn/Verlust für die Bank  [(Höhe des Gewinns/Verlusts interessant)]{.notes}


## Beispiel: Autoreparatur

*   **Gegeben**: Eigenschaften eines Autos

    => Eigenschaften: Ausprägungen der Merkmale

\bigskip

*   **Gesucht**: Diagnose und Reparaturanleitung

    => Hypothese über den Merkmalen (Funktion $\operatorname{h}$)


## Lernen durch Beobachten: Lernen einer Funktion $\operatorname{f}$

::: notes
Funktionsapproximation: Lernen einer Funktion $\operatorname{f}$ anhand von Beispielen
:::

*   Ein Beispiel ist ein Tupel $(\mathbf{x}, \operatorname{f}(\mathbf{x}))$, etwa
    $$
    (\mathbf{x}, \operatorname{f}(\mathbf{x})) = \left(\begin{array}{ccc}
    O & O & X \\
    . & X & . \\
    X & . & .
    \end{array}, +1\right)
    $$

\bigskip

*   Aufgabe: Baue Hypothese $\operatorname{h}$ auf, so dass $\operatorname{h} \approx \operatorname{f}$.
    *   Benutze dazu Menge von Beispielen => [**Trainingsdaten**]{.alert}.

\bigskip

*   Ziele:
    1.  **Konsistente Hypothese**: Übereinstimmung bei Trainingsdaten
    2.  **Generalisierende Hypothese**: Korrekte Vorhersage bei
        unbekannten Daten

::: notes
*Anmerkung*: Stark vereinfachtes Modell realen Lernens!
:::


## Konstruieren einer konsistenten Hypothese

::: center
![](images/occams1.png){width="60%"}
:::

::: notes
Welcher Zusammenhang ist hier dargestellt? Offenbar eine Art Funktionsverlauf ...
Wir haben für einige x-Werte die zugehörigen y-Werte vorgegeben.
:::


## Konstruieren einer konsistenten Hypothese (cnt.)

::: center
![](images/occams2.png){width="60%"}
:::

::: notes
Die einfachste Approximation wäre eine lineare Funktion. Allerdings werden hierbei
einige Werte mehr oder weniger stark nicht korrekt widergegeben, d.h. man hat einen
relativ hohen (Trainings-) Fehler.
:::


## Konstruieren einer konsistenten Hypothese (cnt.)

::: center
![](images/occams3.png){width="60%"}
:::

::: notes
Die Hyperbel erklärt die Trainingsdaten bis auf den einen Punkt sehr gut.
Die Frage ist, ob dieser eine Punkt zum zu lernenden Zusammenhang gehört
oder ein Ausreißer ist, den man gefahrlos ignorieren kann?
:::


## Konstruieren einer konsistenten Hypothese (cnt.)

::: center
![](images/occams4.png){width="60%"}
:::

::: notes
Die grüne Hypothese ist von allen bisher gezeigten die komplexeste, erklärt
aber alle Datenpunkte. D.h. hier wäre der Trainingsfehler Null. Zwischen den
Trainingsdaten zeigt das Modell eine "glatte" Approximation, d.h. es wird auch
neue Daten, die es beim Training nicht gesehen hat, relativ gut erklären.
(Dabei liegt freilich die Annahme zugrunde, dass alle relevanten Daten in der
Trainingsmenge vorhanden sind, d.h. dass es insbesondere zwischen den Datenpunkten
keine Ausreißer o.ä. gibt.)
:::


## Konstruieren einer konsistenten Hypothese (cnt.)

::: center
![](images/occams5.png){width="60%"}
:::

::: notes
Diese Hypothese erklärt ebenfalls sämtliche Trainingsdaten. Allerdings schwingt
die Funktion zwischen den Daten stark hin und her. Vermutlich entspricht dies
nicht dem zu lernenden Funktionsverlauf. Der Trainingsfehler wäre wie bei der
deutlich einfacheren Hypthese aus dem letzten Schritt Null. Der Generalisierungsfehler
(sprich die Abweichung, wenn man das Modell nach Daten zwischen den Trainingspunkten
fragt) dürfte erheblich höher liegen.

D.h. hier hat das Modell einfach die Trainingsdaten auswendig gelernt, aber nicht
den Zusammenhang zwischen den Daten! Dies ist in der Regel unerwünscht!
:::


## Occam's Razor

\large

**Bevorzuge die einfachste konsistente Hypothese!**

\normalsize

::: notes
1.  Wenn es mehrere mögliche Erklärungen für einen Sachverhalt gibt, ist die
    einfachste Erklärung allen anderen vorzuziehen.
2.  Eine Erklärung ist "einfach", wenn sie möglichst wenige Variablen und
    Annahmen enthält und wenn diese in klaren logischen Beziehungen zueinander
    stehen, aus denen der zu erklärende Sachverhalt logisch folgt.
:::


## Trainingsdaten und Merkmalsvektoren

Lehrer gibt Beispiele vor: Eingabe $\mathbf{x}$ und passende Ausgabe $\operatorname{f}(\mathbf{x})$

\smallskip

*   Ausgabe: typischerweise Skalar (Funktionswert oder Klasse) \newline
    => Beispiel: Bewertung eines Spielstandes bei TicTacToe

\smallskip

*   Eingabe: (Beschreibung des) Objekt(s) oder Situation, die zur Ausgabe gehört \newline
    => Beispiel: Spielstand bei TicTacToe

\bigskip
\bigskip

**Merkmalsvektoren**:

*   Zusammenfassen der [relevanten Merkmale]{.alert} zu [Vektoren]{.alert}


## Beispiel: Schwimmen im See

Beschreibung der Faktoren, wann ich im See schwimmen möchte:

1.  Scheint die Sonne?
2.  Wie warm ist das Wasser?
3.  Wie warm ist die Luft?

\bigskip

*   Trainingsbeispiel:
    *   Eingabe: Merkmalsvektor `(sonnig, warm, warm)`
    *   Ausgabe: Klasse `ja`

::: notes
Dabei wird davon ausgegangen, dass jeder Faktor (jedes Merkmal) an einer bestimmten
Stelle im Merkmalsvektor aufgeführt ist. Beispielsweise gehört das `sonnig` zur
Frage "Scheint die Sonne", `warm` jeweils zur Wasser- und zur Lufttemperatur.

Damit hat man in einem Vektor eine Situation komplett beschrieben, d.h. einen Zustand
der Welt mit den relevanten Dingen beschrieben. Diesem Zustand kann man beispielsweise
ein Label (Klasse) verpassen, hier in diesem Fall "ja, in dieser Welt möchte ich
schwimmen".

Die Trainingsmenge baut sich dann beim überwachten Lernen aus vielen solcher Paare
(Merkmalsvektor, Klasse) auf, und die Algorithmen sollen diese Zuordnung lernen, d.h.
ein Modell für diese Daten erzeugen, welches die Daten gut erklärt und darüber hinaus
für neue Daten aus der selben Datenquelle gute Vorhersagen macht.
:::


## Trainingsdaten -- Merkmalsvektoren

**Generell**: Merkmalsvektor für Objekt $v$:
$$
    \mathbf{x}(v) = (x_1, x_2, \ldots, x_n)
$$

*   $n$ Merkmale (Attribute)
*   Attribut $x_t$ hat $m_t$ mögliche Ausprägungen
*   Ausprägung von $v$ bzgl. $x_t$: $\quad x_t(v) = i \quad$ (mit $i = 1 \ldots m_t$)

::: notes
*Anmerkung*: Stellen Sie sich den Merkmalsvektor \mathbf{x} vielleicht wie
einen Konstruktor einer Klasse `x` vor: Die einzelnen Attribute $x_t$ sind
die Parameter, aus denen der Merkmalsvektor aufgebaut ist/wird. Jedes der
Attribute hat einen Typ und damit eine bestimmte Anzahl erlaubter Werte
("Ausprägungen") ...
:::

\bigskip
\bigskip

**Trainingsbeispiel**:

*   Tupel aus Merkmalsvektor und zugehöriger Klasse: $\left(\mathbf{x}(v), k\right)$

[[Analogie Konstruktor Klasse $x$]{.bsp}]{.slides}


## Wrap-Up

*   Lernen ist Verhaltensänderung, Ziel: Optimierung einer Gütefunktion
    *   Aufbau einer Hypothese, die beobachtete Daten erklären soll
    *   Arten: Überwachtes Lernen, Unüberwachtes Lernen, Reinforcement Lernen

\smallskip

*   Merkmalsvektoren gruppieren Eigenschaften des Problems bzw. der Objekte
*   Trainingsdaten: Beispielobjekte (durch Merkmalsvektoren beschrieben) plus Vorgabe vom Lehrer







<!-- DO NOT REMOVE - THIS IS A LAST SLIDE TO INDICATE THE LICENSE AND POSSIBLE EXCEPTIONS (IMAGES, ...). -->
::: slides
## LICENSE
![](https://licensebuttons.net/l/by-sa/4.0/88x31.png)

Unless otherwise noted, this work is licensed under CC BY-SA 4.0.
:::
