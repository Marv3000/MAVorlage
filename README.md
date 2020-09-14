# Vorlage Masterarbeit
Die Intention liegt in der Entwicklung einer TeX-Vorlage für die Masterarbeit im Studiengang Master Biometry/Biostatistics an der Universität Heidelberg. Das Ganze nutzt die Project-Umgebung von TeXStudio, lässt sich aber in nahezu jedem vorhandenen TeX-Editor kompilieren (nicht getestet). 

## Struktur der Dokumente
Der Kern der Vorlage ist die Datei `masterarbeit.tex`. Über diese Datei werden alle anderen Einzelteile aufgerufen und eingebunden sowie die zentralen Definitionen hinsichtlich Inhalts-/Tabellen- und Abbildungsverzeichnis aufgerufen. Auch wird hier bereits das Literaturverzeichnis eingebunden. 

### Preamble
Über `\input{preamble.tex}` wird zunächst die Dokumentenklassen -- ich nutze `scrreprt` für die Masterarbeit --  festgelegt sowie die weiteren Optionen und Einstellungen aufgerufen:
```
\documentclass[12pt, a4paper, toc=bibliographynumbered, toc=listoff, english, draft=false]{scrreprt}
\usepackage[amsfonts,amsmath,amsthm}
.
.
.
```
Die jeweiligen Pakete und Optionen können dabei den eigenen Ansprüchen und Erfordernissen entsprechend angepasst werden. 

### Titlepage
Die Titelseite ist den Erfordernissen der Uni bzw. des Instituts basierend auf der Word-Vorlage aus Moodle angepasst. Die Opacity und exakte Positionierung des Logos sowie der einzelnen Überschriften und Autoreninformationen können in der Datei `titlepage.tex` modifiziert werden: 
```
\begin{center}

	\begin{tikzpicture}[remember picture, overlay]
      % Opacity verändert die Durchsichtigkeit des Logos
      % Die Datei HD.png MUSS im Arbeitsordner der Datei gespeichert sein
      % yshift verändert die horizontale Positionierung in Relation zum oberen Rand
	\node[anchor=north, yshift=-12.5mm, opacity=.35]at(current page.north){%
	\pgfimage{HD}};
	\end{tikzpicture}
	
{\LARGE \textbf{Ruprecht-Karls-Universität Heidelberg}}
\end{center}
```
Abstände und Schriftgrößen lassen sich mittels der bekannten Optionen `\Large` (oder `\large` bzw. `\Huge`) anpassen. Abstände habe ich mit `\vspace` eingebaut:
```
\vspace{10em}
\begin{center}
{\large Masterarbeit zur Erlangung des akademisches Grades \\[0.5cm]
\glqq Master of Science in Medical Biometry/Biostatistics\grqq} \\[1.0cm]
{\large A title for a really great piece of research, just the best, really}\\[2.0cm]
{\large vorgelegt von}\\[0.5cm]
{\large Donald J. Trump}\\
\vfill
{\large 20XX}
\end{center}
```
`\glqq` sowie `\grqq` sind für das Setzen von Anführungszeichen (je nach Definition der Kodierung der Zeichen) beim Titel der Arbeit (siehe Moodle-Vorlage) wichtig, können aber je nach Vorliebe auch weggelassen werden.

## Workflow
Die Arbeit am Inhalt erfolgt dann in einzelnen TeX-Files wie beispielsweise `Introduction.tex`:
```
\chapter{Introduction}
Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt 
ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. 
```
Dies wird dann in der Datei `masterarbeit.tex` ziemlich simpel über `\input{Introduction}` eingebunden. Das Referenzieren auf Literaturstellen funktioniert dann genau wie in einem einzelnen Dokument auch über `\cite{}`. TeX wird dann entsprechend des BibTeX-Keys eine Referenz basierend auf den im BibTeX-Eintrag gespeicherten bibliografischen Informationen (diese sind hier im Beispiel in der Datei `expose.bib` abgelegt) im Literaturverzeichnis erstellen. Wie beim Logo muss dazu natürlich a) eine BibTex-Datei vorhanden sein und b) in dieser Datei die Referenz erstellt worden sein. 
