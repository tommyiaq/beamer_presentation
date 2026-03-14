## Getting Started

####  4 Workflow For Creating a Beamer Presentation 

This section presents a possible workflow for creating a beamer presentation and possibly a handout to go along with it. Technical questions are addressed, like which programs to call with which parameters. 

#####  4.1 Step One: Setup the Files¶

presentation

It is advisable that you create a folder for each presentation. Even though your presentation will usually reside in a single file, TeX produces so many extra files that things can easily get very confusing otherwise. The folder’s name should ideally start with the date of your talk in ISO format (like 2003-12-25 for a Christmas talk), followed by some reminder text of what the talk is all about. Putting the date at the front in this format causes your presentation folders to be listed nicely when you have several of them residing in one directory. If you use an extra directory for each presentation, you can call your main file main.tex. 

To create an initial main.tex file for your talk, copy an existing file from the beamer/doc/solutions directory and adapt it to your needs. A list of possible beamer solutions that contain templates for presentation TeX-files can be found below. 

If you wish your talk to reside in the same file as some different, non-presentation article version of your text, it is advisable to setup a more elaborate file scheme. See Section [21.2.2](<Creating-Handouts-Lecture-Notes.html#section-article-version-workflow>) for details. 

#####  4.2 Step Two: Structure Your Presentation¶

The next step is to fill the presentation file with \section and \subsection to create a preliminary outline. You’ll find some hints on how to create a good outline in Section [5.1](<Guidelines-Creating-Presentations.html#section-structure-guidelines>). 

Put \section and \subsection commands into the (more or less empty) main file. Do not create any frames until you have a first working version of a possible table of contents. The file might look like this: 
    
    
    \documentclass{beamer}
    %% This is the file main.tex
    
    \usetheme{Berlin}
    
    \title{Example Presentation Created with the Beamer Package}
    \author{Till Tantau}
    \date{\today}
    
    \begin{document}
    
    \begin{frame}
      \titlepage
    \end{frame}
    
    
    
    \section*{Outline}
    \begin{frame}
      \tableofcontents
    \end{frame}
    
    \section{Introduction}
    \subsection{Overview of the Beamer Class}
    \subsection{Overview of Similar Classes}
    
    \section{Usage}
    \subsection{...}
    \subsection{...}
    
    \section{Examples}
    \subsection{...}
    \subsection{...}
    
    \begin{frame}
    \end{frame} % to enforce entries in the table of contents
    
    \end{document}
    

The empty frame at the end (which should be deleted later) ensures that the sections and subsections are actually part of the table of contents. This frame is necessary since a \section or \subsection command following the last page of a document has no effect. 

#####  4.3 Step Three: Creating a PDF or PostScript File¶

presentation

Once a first version of the structure is finished, you should try to create a first PDF or PostScript file of your (still empty) talk to ensure that everything is working properly. This file will only contain the title page and the table of contents. 

######  4.3.1 Creating PDF¶

presentation

To create a PDF version of this file, run the program pdflatex on main.tex at least twice. You need to run it twice, so that TeX can create the table of contents. (It may even be necessary to run it more often since all sorts of auxiliary files are created.) In the following example, the greater-than-sign is the prompt. 
    
    
    > pdflatex main.tex
        ... lots of output ...
    > pdflatex main.tex
        ... lots of output ...
    

Alternatively, you can use lualatex or xelatex instead of pdflatex in above commands. 

You can next use a program like the Acrobat Reader, xpdf, evince or okular to view the resulting presentation. 
    
    
    > acroread main.pdf
    

######  4.3.2 Creating PostScript¶

presentation

To create a PostScript version, you should first ascertain that the hyperref package (which is automatically loaded by the beamer class) uses the option dvips or some compatible option, see the documentation of the hyperref package for details. Whether this is the case depends on the contents of your local hyperref.cfg file. You can enforce the usage of this option by passing dvips or a compatible option to the beamer class (write \documentclass[dvips]{beamer}), which will pass this option on to the hyperref package. 

You can then run latex twice, followed by dvips. 
    
    
    > latex main.tex
        ... lots of output ...
    > latex main.tex
        ... lots of output ...
    > dvips -P pdf main.dvi
    

The option (-P pdf) tells dvips to use Type 1 outline fonts instead of the usual Type 3 bitmap fonts. You may wish to omit this option if there is a problem with it. 

You can convert a PostScript file to a pdf file using
    
    
    > ps2pdf main.ps main.pdf
    

######  4.3.3 Ways of Improving Compilation Speed¶

While working on your presentation, it may sometimes be useful to TeX your .tex file quickly and have the presentation contain only the most important information. This is especially true if you have a slow machine. In this case, you can do several things to speed up the compilation. First, you can use the draft class option. 

\documentclass[draft]{beamer}

Causes the headlines, footlines, and sidebars to be replaced by gray rectangles (their sizes are still computed, though). Many other packages, including pgf and hyperref, also “speed up” when this option is given. 

Second, you can use the following command:

`\includeonlyframes`{⟨ _frame label list_ ⟩} 

This command behaves a little bit like the \includeonly command: Only the frames mentioned in the list are included. All other frames are suppressed. Nevertheless, the section and subsection commands are still executed, so that you still have the correct navigation bars. By labeling the current frame as, say, current and then saying \includeonlyframes{current}, you can work on a single frame quickly. 

The ⟨ _frame label list_ ⟩ is a comma-separated list (without spaces) of the names of frames that have been labeled. To label a frame, you must pass the option label=⟨ _name_ ⟩ to the \frame command or frame environment. 

_Example:_
    
    
    \includeonlyframes{example1,example3}
    
    \begin{frame}[label=example1]
    This frame will be included.
    \end{frame}
    
    \begin{frame}[label=example2]
    This frame will not be included.
    \end{frame}
    
    \begin{frame}
    This frame will not be included.
    \end{frame}
    
    \againframe{example1} % Will be included
    

#####  4.4 Step Four: Create Frames¶

Once the table of contents looks satisfactory, start creating frames for your presentation by adding frame environments. You’ll find guidelines on what to put on a frame in Section [5.1.3](<Guidelines-Creating-Presentations.html#section-frame-guidelines>). 

#####  4.5 Step Five: Test Your Presentation¶

_Always_ test your presentation. For this, you should vocalize or subvocalize your talk in a quiet environment. Typically, this will show that your talk is too long. You should then remove parts of the presentation, such that it fits into the allotted time slot. Do _not_ attempt to talk faster in order to squeeze the talk into the given amount of time. You are almost sure to lose your audience this way. 

Do not try to create the “perfect” presentation immediately. Rather, test and retest the talk and modify it as needed. 

#####  4.6 Step Six: Create a Handout¶

######  4.6.1 Creating the Handout¶

Once your talk is fixed, you can create a handout, if this seems appropriate. For this, you can use the class option handout as explained in Section [21.1](<Creating-Handouts-Lecture-Notes.html#handout>). Typically, you might wish to put several handout slides on one page, see below on how to do this easily. 

You may also wish to create an article version of your talk. An “article version” of your presentation is a normal TeX text typeset using, for example, the document class article or perhaps llncs or a similar document class. The beamer class offers facilities to have this version coexist with your presentation version in one file and to share code. Also, you can include slides of your presentation as figures in your article version. Details on how to setup the article version can be found in Section [21.2](<Creating-Handouts-Lecture-Notes.html#section-article>). 

######  4.6.2 Printing the Handout¶

The easiest way to print a presentation is to use Acrobat Reader with the option “expand small pages to paper size” form the printer dialog enabled. This is necessary, because slides are by default only 128mm by 96mm large. 

For the PostScript version and for printing multiple slides on a single page this simple approach does not work. In such cases you can use the pgfpages package, which works directly with pdflatex, lualatex, xelatex and latex plus dvips. Note however _that this package destroys hyperlinks_. This is due to fundamental flaws in the pdf-specification and it is not likely to change. 

The pgfpages can do all sorts of tricks with pages. The most important one for printing beamer slides is the following command: 
    
    
    \usepackage{pgfpages}
    \pgfpagesuselayout{resize to}[a4paper,border shrink=5mm,landscape]
    

This says “Resize all pages to landscape A4 pages, no matter what their original size was, but shrink the pages by 5mm, so that there is a bit of a border around everything.” Naturally, instead of a4paper you can also use letterpaper or any of the other standard paper sizes. For further options and details see the documentation of pgfpages. 

The second thing you might wish to do is to put several slides on a single page. This can be done as follows: 
    
    
    \usepackage{pgfpages}
    \pgfpagesuselayout{2 on 1}[a4paper,border shrink=5mm]
    

This says “Put two pages on one page and then resize everything so that it fits on A4 paper.” Note that this time we do not need landscape as the resulting page is, after all, not in landscape mode. 

Instead of 2 on 1 you can also use 4 on 1, but then with landscape once more, and also 8 on 1 and even 16 on 1 to get a grand (though unreadable) overview. 

If you put several slides on one page and if these slides normally have a white background, it may be useful to write the following in your preamble: 
    
    
    \mode<handout>{\setbeamercolor{background canvas}{bg=black!5}}
    

This will cause the slides of the handout version to have a very light gray background. This makes it easy to discern the slides’ border if several slides are put on one page. 
