####  1 Introduction 

beamer is a LaTeX class for creating presentations that are held using a projector, but it can also be used to create transparency slides. Preparing presentations with beamer is different from preparing them with wysiwyg programs like Libre-/OpenOffice.org Impress, Apple Keynote, Calligra Stage or Microsoft PowerPoint. A beamer presentation is created like any other LaTeX document: It has a preamble and a body, the body contains \sections and \subsections, the different slides (called _frames_ in beamer) are put in environments, they are structured using itemize and enumerate environments, and so on. The obvious disadvantage of this approach is that you have to know LaTeX in order to use beamer. The advantage is that if you know LaTeX, you can use your knowledge of LaTeX also when creating a presentation, not only when writing papers. 

#####  1.1 Main Features¶

The list of features supported by beamer is quite long (unfortunately, so is presumably the list of bugs supported by beamer). The most important features, in our opinion, are: 

  * • You can use beamer with pdflatex, latex+dvips and lualatex. beamer documents can also be compiled with xelatex, however the results might show some elements incorrectly and there are other limitations of the engine, which are described in more detail in e.g. <https://www.texdev.net/2024/11/05/engine-news-from-the-latex-project>. latex+dvipdfm isn’t supported (but we accept patches!). 

  * • The standard commands of LaTeX still work. A \tableofcontents will still create a table of contents, \section is still used to create structure, and itemize still creates a list. 

  * • You can easily create overlays and dynamic effects. 

  * • Themes allow you to change the appearance of your presentation to suit your purposes. 

  * • The themes are designed to be usable in practice, they are not just for show. You will not find such nonsense as a green body text on a picture of a green meadow. 

  * • The layout, the colors, and the fonts used in a presentation can easily be changed globally, but you still also have control over the most minute detail. 

  * • A special style file allows you to use the LaTeX-source of a presentation directly in other LaTeX classes like article or book. This makes it easy to create presentations out of lecture notes or lecture notes out of presentations. 

  * • The final output is typically a pdf-file. Viewer applications for this format exist for virtually every platform. When bringing your presentation to a conference on a memory stick, you do not have to worry about which version of the presentation program might be installed there. Also, your presentation is going to look exactly the way it looked on your computer. 




#####  1.2 History¶

Till Tantau created beamer mainly in his spare time. Many other people have helped by sending him emails containing suggestions for improvement or corrections or patches or whole new themes (by now, this amounts to over a thousand emails concerning beamer). Indeed, most of the development was only initiated by feature requests and bug reports. Without this feedback, beamer would still be what it was originally intended to be: a small private collection of macros that make using the seminar class easier. Till created the first version of beamer for his PhD defense presentation in February 2003. A month later, he put the package on ctan at the request of some colleagues. After that, things somehow got out of hand. 

After being unmaintained since 2007, in April 2010 Till handed over the maintenance to Joseph Wright and Vedran Miletić, who are still maintaining it: improving code, fixing bugs, adding new features and helping users. 

#####  1.3 Acknowledgments¶

Till Tantau: _“Where to begin? beamer’s development depends not only on me, but on the feedback I get from other people. Many features have been implemented because someone requested them and I thought that these features would be nice to have and reasonably easy to implement. Other people have given valuable feedback on themes, on the user’s guide, on features of the class, on the internals of the implementation, on special LaTeX features, and on life in general. A small selection of these people includes (in no particular order and I have surely forgotten to name lots of people who really, really deserve being in this list): Carsten (for everything), Birgit (for being the first person to use beamer besides me), Tux (for his silent criticism), Rolf Niepraschk (for showing me how to program LaTeX correctly), Claudio Beccari (for writing part of the documentation on font encodings), Thomas Baumann (for the emacs stuff), Stefan Müller (for not loosing hope), Uwe Kern (for xcolor), Hendri Adriaens (for ha-prosper), Ohura Makoto (for spotting typos). People who have contributed to the themes include Paul Gomme, Manuel Carro, and Marlon Régis Schmitz.”_

Joseph Wright: _“Thanks to Till Tantau for the huge development effort in creating beamer. Sincere thanks to Vedran Miletić for taking the lead in continuing development.”_

Vedran Miletić: _“First, I would like to thank Karl Berry and Sanda Bujačić for encouragement, without which I wouldn’t ever be anything but a LaTeX user. I would also like to thank Ana Meštrović, my colleague, who was excited by the prospect of using beamer for preparing class material; Ivona Franković and Marina Rajnović, my students at Department of Informatics, who were the first to hear about LaTeX, beamer and how it can help in preparing class material. I would like to thank Heiko Oberdiek (for hyperref), Johannes Braams (for babel) and Philipp Lehman (for biblatex). Above all, I owe a lot to Till Tantau for developing beamer in the first place and to Joseph Wright for developing siunitx and for helping me develop beamer further.”_

#####  1.4 How to Read this User’s Guide¶

You should start with the first part. If you have not yet installed the package, please read Section [2](<Installation.html#section-installation>) first. If you are new to beamer, you should next read the tutorial in Section [3](<Tutorial-Euclid-Presentation.html#section-tutorial>). When you sit down to create your first real presentation using beamer, read Section [4](<Workflow-For-Creating-Beamer-Presentation.html#section-workflow>) where the technical details of a possible workflow are discussed. If you are still new to creating presentations in general, you might find Section [5](<Guidelines-Creating-Presentations.html#section-guidelines>) helpful, where many guidelines are given on what to do and what not to do. Finally, you should browse through Section [6](<Solution-Templates.html#section-solutions>), where you will find ready-to-use solution templates for creating talks, possibly even in the language you intend to use. 

The second part of this user’s guide goes into the details of all the commands defined in beamer, but it also addresses other technical issues having to do with creating presentations (like how to include graphics or animations). 

The third part explains how you can change the appearance of your presentation easily either using themes or by specifying colors or fonts for specific elements of a presentation (like, say, the font used for the numbers in an enumeration). 

The fourth part talks about handouts and lecture notes, so called “support material”. You will frequently have create some kind of support material to give to your audience during the talk or after it, and this part will explain how to do it using the same source that you created your presentation from. 

The last part contains “howtos,” which are explanations of how to get certain things done using beamer. 

This user’s guide contains descriptions of all “public” commands, environments, and concepts defined by the beamer-class. The following examples show how things are documented. As a general rule, red text is _defined_ , green text is _optional_ , blue text indicates special mode considerations. 

`\somebeamercommand`[⟨ _optional arguments_ ⟩]{⟨ _first argument_ ⟩}{⟨ _second argument_ ⟩} 

Here you will find the explanation of what the command \somebeamercommand does. The green argument(s) is optional. The command of this example takes two parameters. 

_Example:_ \somebeamercommand[opt]{my arg}{xxx}

\begin{somebeamerenvironment}[⟨ _optional arguments_ ⟩]{⟨ _first argument_ ⟩} 

⟨ _environment contents_ ⟩

\end{somebeamerenvironment}

Here you will find the explanation of the effect of the environment somebeamerenvironment. As with commands, the green arguments are optional. 

_Example:_
    
    
    \begin{somebeamerenvironment}{Argument}
      Some text.
    \end{somebeamerenvironment}
    

**Beamer-Template/-Color/-Font** some beamer element

Here you will find an explanation of the template, color, and/or font some beamer element. A “beamer-element” is a concept that is explained in more detail in Section [16](<Inner-Themes-Outer-Themes-Templates.html#section-elements>). Roughly speaking, an _element_ is a part of a presentation that is potentially typeset in some special way. Examples of elements are frame titles, the author’s name, or the footnote sign. For most elements there exists a _template_ , see Section [16](<Inner-Themes-Outer-Themes-Templates.html#section-elements>) once more, and also a beamer-color and a beamer-font. 

For each element, it is indicated whether a template, a beamer-color, and/or a beamer-font of the name some beamer element exist. Typically, all three exist and are employed together when the element needs to be typeset, that is, when the template is inserted the beamer-color and -font are installed first. However, sometimes templates do not have a color or font associated with them (like parent templates). Also, there exist beamer-colors and -fonts that do not have an underlying template. 

Using and changing templates is explained in Section [16.3](<Inner-Themes-Outer-Themes-Templates.html#section-templates>). Here is the essence: To change a template, you can say 
    
    
    \setbeamertemplate{some beamer element}{your definition for this template}
    

Unfortunately, it is not quite trivial to come up with a good definition for some templates. Fortunately, there are often _predefined options_ for a template. These are indicated like this: 

  * • `[rose]` causes a rose be used to render the template. 

  * • `[shamrock]`{⟨ _number of leaves_ ⟩} causes a shamrock with a given number of leaves to be used to render the template. 




You can install such a predefined option like this:
    
    
    \setbeamertemplate{some beamer element}[rose]
    %% Now a rose is used
    
    \setbeamertemplate{some beamer element}[shamrock]{3}
    %% Now a shamrock is used
    

Note that not all templates have predefined options and that not all templates with predefined options allow an additional argument. 

beamer-colors are explained in Section [17](<Colors.html#section-colors>). Here is the essence: To change the foreground of the color to, say, red, use 
    
    
    \setbeamercolor{some beamer element}{fg=red}
    

To change the background to, say, black, use:
    
    
    \setbeamercolor{some beamer element}{bg=black}
    

You can also change them together using fg=red,bg=black. The background will not always be “honoured,” since it is difficult to show a colored background correctly and an extra effort must be made by the templates (while the foreground color is usually used automatically). 

beamer-fonts are explained in Section [18](<Fonts.html#section-fonts>). Here is the essence: To change the size of the font to, say, large, use: 
    
    
    \setbeamerfont{some beamer element}{size=\large}
    

In addition to the size, you can use things like series=\bfseries to set the series, shape=\itshape to change the shape, family=\sffamily to change the family, and you can use them in conjunction. Add a star to the command to first “reset” the font. 

presentation

As next to this paragraph, you will sometimes find the word presentation in blue next to some paragraph. This means that the paragraph applies only when you “normally typeset your presentation using LaTeX or pdfLaTeX.” 

article

Opposed to this, a paragraph with article next to it describes some behavior that is special for the article mode. This special mode is used to create lecture notes out of a presentation (the two can coexist in one file). 

#####  1.5 Getting Help¶

When you need help with beamer, please do the following: 

  * 1. Read the user guide, at least the part that has to do with your problem. 

  * 2. If that does not solve the problem, try searching one of the TeX related question and answer sites like [`tex.stackexchange.com`](<https://tex.stackexchange.com>), [`latex.org`](<https://latex.org/forum/>) or [`topanswers.xyz/tex`](<https://topanswers.xyz/tex>). Perhaps someone has already reported a similar problem and someone has found a solution. 

  * 3. If you find no answers there, or if you are sure you have found a bug in beamer, please report it _via_ [`github.com/josephwright/beamer/issues`](<https://github.com/josephwright/beamer/issues>). 

  * 4. Before you file a bug report, especially a bug report concerning the installation, make sure that this is really a bug. In particular, have a look at the .log file that results when you TeX your files. This .log file should show that all the right files are loaded from the right directories. Nearly all installation problems can be resolved by looking at the .log file. 

If you can, before reporting the bug, retest using latest version of beamer with latest version of TeX Live. This can help isolate bugs from other packages that might affect beamer. 

  * 5. _As a last resort_ you can try emailing authors. We do not mind getting emails, we simply get way too many of them. Because of this, we cannot guarantee that your emails will be answered timely or even at all. Reporting an issue is usually a better approach as they don’t get lost. 



