# LaTeX - Ein Einstieg für TUDa-Studenten

## Installation von LaTeX

### NixOS

- Mit _Nix_: Man lese https://nixos.wiki/wiki/TexLive.

- Mit _Home-Manager_: Man konfiguriert die Option `programs.texlive` in der `home.nix`

- Mit einer _Nix-Flake_: Hier ist meine [Flake](https://github.com/TonyTheAce/NixTeX) dazu

### Obsolete Linux-Betriebssysteme

Man kann über den Paketmanager meist _TeX Live_ installieren, diese installiert seine Pakete statisch hinzu, sodass
man entweder:

1. Die gesamte Distro (ca. 3GB)

2. Spezifische Pakete und Kollektionen

installieren kann. Für Ansatz 1 ist meist nichts weiter zu tun; Ansatz 2 erfordert manchmal die Nachinstallation
von Paketen.

### Windows

Für Windows kann man zwei verschiedene Distros installieren

- _TeX Live_: Äquivalent zur Linux-Variante. **Achtung**: Man muss eine Perl-Distribution und manche andere 
  Abhängigkeit manuell installieren; diese sind nicht in der Installation enthalten

- _MiKTeX_: Diese Distro kann zur Kompilierzeit jegliche Pakete installieren, dementsprechend dauert es aber 
  entsprechend länger (3x-6x langsamer als _TeX Live_)

Ihre Installation kann mit einem Installer oder mit einem Windows-Paketmanager (wie `scoop`) bewerkstelligt werden.

## Wahl des Texteditors

### (Neo)Vim

Für den besten Texteditor gibt es viele Plugins, mit welchen man Features wie _Autocompile_, _Syntax Highlighting_ und
_Autocomplete_ nachrüsten kann. Damit wird Vim der minimalste und schwierigste Editor von dieser Liste

Man beachte, dass man einen externen PDF-Viewer wie Zathura benötigt. Der Workflow entfaltet seine Stärke am
ehesten mit einem Tiling Window Manager.

### Visual Studio Code

Mit dem Plugin _LaTeX Workshop_ ist VSCode komplett ausgerüstet. Die Editor-Features wie
IntelliSense (Autocompletion) und das intuitive Interface werden mit einem GUI für LaTeX ergänzt. In der Theorie
muss man somit nie mit dem Terminal interagieren.

### TeXMaker und ähnliche

Vom Feature-Set sind spezialisierte LaTeX-Editoren en par mit VSCode, aber als Komplettpaket, in dem Sinne, dass
nichts nachinstalliert werden muss. Im Vergleich sind Rechtschreibprüfung und Fehlermeldungen oftmals besser.

### ShareLaTeX-Instanz der TU Darmstadt

ShareLaTeX ist ein Online-Angebot für LaTeX mit folgenden Eigenheiten:

- Man muss keine LaTeX-Distro installieren; Kompilierung ist Server-seitig (Langsam!)

- Native Zusammenarbeit

- Niedrigschwellig (Nur Internet und Browser notwendig)

## Ressourcen

Unterhalb ist allgemein nützliches Lesematerial:

- Overleaf-Tutorials (https://www.overleaf.com/learn)

- Wikibook (https://en.wikibooks.org/wiki/LaTeX): Ähnlich zu Overleaf.

- LaTeX-Wiki der TU Graz (https://latex.tugraz.at/start): Deutschsprachige Anleitungen

Die folgenden Links sind für spezielle Anwendungszwecke:

- Paketverzeichnis CTAN (https://ctan.org/): Enthält zu (fast) jedem LaTeX-Paket die entsprechende README

- Repo der TUDa-Vorlagen (https://github.com/tudace/tuda_latex_templates): Beinhaltet Anleitung spezifische zu der
  Vorlage innerhalb `./templates`

## Schreibprozess: Hausübungen der Informatik

Für diesen Zweck ist innerhalb `./templates` eine Vorlage enthalten. Man beachte, dass eine `logofile` benötigt wird, 
um zu kompillieren; mit dem folgenden [Link](https://download.hrz.tu-darmstadt.de/protected/ULB/tuda_logo.pdf) wird
diese heruntergeladen (TU-ID notwendig!).

Vorrausgesetzt, man hat alle obigen Anweisungen befolgt, so kann man in der `document`-Umgebung sofort mit der
Erstellung des Dokuments beginnen. Es werden nun _Good practices_ demonstriert.

- **Quelltext-Konventionen:** Es gibt keine offiziellen Stellen, die je Standards für LaTeX-Code festgelegt haben.
  Meiner Erfahrung (ca. 3 Jahre) nach sind aber folgende Dinge empfehlenswert:

    - **Zeilenumbrüche!** Bei manchen mathematischen Ausdrücken kann man logisch mal einen machen, um die
      Lesbarkeit zu erhöhen. Insbesondere beim Beginn einer Umgebung muss ein Umbruch eingefügt sein,
      ähnlich zu Klammern in normalen Programmiersprachen. Das erleichtert auch Zusammenarbeit (_hust hust_)

    - **Whitespaces!** Zwischen mathematischen Zeichen (z.B `\varphi`) sollte ein Leerzeichen gesetzt werden.
      Für manche Umgebungen wie `cases` kann man auch Code einrücken, z.B wie hier

     ```latex
      \[f(x) = \begin{cases}
          x , \ &\mathrm{für} \ x < 1 \\
          x+1 , \ &\mathrm{sonst}
        \end{cases}\]
     ```

- **Codeblöcke**: Um einen zu produzieren, kann man die `lstlisting`-Umgebung des Package `listings` nutzen. Für
  erweiterte Optionen wie Syntax-Highlighting schaut man auf den
  [Overleaf-Guide](https://www.overleaf.com/learn/latex/Code_listing#Using_listings_to_highlight_code).

- **Macros:** Mit `\newcommando{}[]{}` sind Ausdrücke abstrahierbar

### Für mathematische Module

- **Initialisierung:** Mit `\(...\)` oder `$...$` werden mathematische Ausdrücke **im** Text umhüllt; `\[...\]` und
  `$$...$$` sind für Ausdrücke, die in eine eigene Zeile und zentriert gerückt werden sollen. Die Klammern sind
  besser, da diese eindeutig Anfang und Ende angeben, wichtig bei einer hohen Dichte an Mathe-Blöcken

- **Lesbarkeit mathematischer Ausdrücke:** Mit `\displaystyle` können Ausdrücke im Text so gerendert werden, als
  wären sie ein Ausdruck außerhalb:

  - `\sum_{n=0}^{\infty} (a_n)` rendert zu $\sum_{n=0}^{\infty} (a_n)$
  
  - `\displaystyle \sum_{n=0}^{\infty} (a_n)` rendert zu $\displaystyle \sum_{n=0}^{\infty} (a_n)$

  Für Brüche kann man `\dfrac{}{}` ($\dfrac{1}{2}$) anstatt `\frac{}{}` ($\frac{1}{2}$) nutzen. Ob es gut aussieht,
  ist eine andere Frage

- **Temporäre Aufhebung des Mathe-Umgebung:** Man nutzt `\text{...}`. Darin sind wieder alle normalen
  LaTeX-Kommandos erhältlich

- **Beweise:** Innerhalb der `proof`-Umgebung werden Beweisstart und -ende erstellt. Das ist nur Eyecandy.
