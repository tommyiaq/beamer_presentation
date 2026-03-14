## Getting Started

####  2 Installation 

There are different ways of installing the beamer class, depending on your installation and needs. When installing the class, you may have to install some other packages as well as described below. Before installing, you may wish to review the licenses under which the class is distributed, see Section [7](<Licenses-Copyright.html#section-license>). 

Fortunately, most likely your system will already have beamer preinstalled, so you can skip this section. 

#####  2.1 Versions and Dependencies¶

This documentation is part of version 3.71 of the beamer class. beamer needs a reasonably recent version of several standard packages to run and also the following versions of two special packages (later versions should work, but not necessarily): 

  * • pgf.sty version 3.1.7, 

  * • xcolor.sty version 2.00. 




If you use pdflatex, which is optional, you need 

  * • pdflatex version 0.14 or higher. Earlier versions do not work. 




#####  2.2 Installation of Pre-bundled Packages¶

We do not create or manage pre-bundled packages of beamer, but, fortunately, other nice people do. We cannot give detailed instructions on how to install these packages, since we do not manage them, but we _can_ tell you where to find them and we can tell you what these nice people told us on how to install them. If you have a problem with installing, you might wish to have a look at the following first. 

######  2.2.1TeX Live and MacTeX¶

In TeX Live, use the tlmgr tool to install the packages called beamer, pgf, and xcolor. If you have a fairly recent version of TeX Live, and you have done full installation, beamer is included. 

######  2.2.2 MiKTeX and proTeXt¶

For MiKTeX and proTeXt, use the update wizard or package manager to install the (latest versions of the) packages called beamer, pgf, and xcolor. 

######  2.2.3 Linux distributions¶

Most linux distributions provide pre-packaged bundles of TeX Live. It is probably easiest to install a full (or at least recommended) scheme of TeX Live, but if you only want to install beamer: 

  * • Ubuntu/Debian: apt install texlive-latex-recommended

  * • Fedora: dnf install texlive-beamer




#####  2.3 Installation in a texmf Tree¶

If, for whatever reason, you do not wish to use a prebundled package, the “right” way to install beamer is to put it in a so-called texmf tree. In the following, we explain how to do this. 

Obtain the latest source version (ending .tar.gz or .zip) of the beamer package from 
    
    
    https://github.com/josephwright/beamer
    

(most likely, you have already done this). Next, you also need the pgf package and the xcolor packages, which you need to install separately (see their installation instructions). 

The package contains a bunch of files; beamer.cls is one of these files and happens to be the most important one. You now need to put these files in an appropriate texmf tree. 

When you ask TeX to use a certain class or package, it usually looks for the necessary files in so-called texmf trees. These trees are simply huge directories that contain these files. By default, TeX looks for files in three different texmf trees: 

  * • The root texmf tree, which is usually located at /usr/share/texmf/, /usr/local/texlive/texmf/, C:\texmf\, or C:\texlive\texmf\. 

  * • The local texmf tree, which is usually located at /usr/local/share/texmf/,  
/usr/local/texlive/texmf-local/, C:\localtexmf\, or C:\texlive\texmf-local\. 

  * • Your personal texmf tree, which is usually located in your home directory at ~/texmf/ or ~/Library/texmf/. 




You should install the packages either in the local tree or in your personal tree, depending on whether you have write access to the local tree. Installation in the root tree can cause problems, since an update of the whole TeX installation will replace this whole tree. 

Inside whatever texmf directory you have chosen, create the sub-sub-sub-directory 
    
    
    texmf/tex/latex/beamer
    

and place all files of the package in this directory.

Finally, you need to rebuild TeX’s filename database. This is done by running the command texhash or mktexlsr (they are the same). In MiKTeX package manager and TeX Live tlmgr, there is a menu option to do this. 

#####  2.4 Updating the Installation¶

To update your installation from a previous version, simply replace everything in the directory 
    
    
    texmf/tex/latex/beamer
    

with the files of the new version. The easiest way to do this is to first delete the old version and then to proceed as described above. 

Note that if you have two versions installed, one in texmf and other in texmf-local directory, TeX distribution will prefer one in texmf-local directory. This generally allows you to update packages manually without administrator privileges. 

#####  2.5 Testing the Installation¶

To test your installation, copy the file generic-ornate-15min-45min.en.tex from the directory 
    
    
    beamer/doc/solutions/generic-talks
    

to some place where you usually create presentations. Then run the command pdflatex several times on the file and check whether the resulting pdf file looks correct. If so, you are all set. 

#####  2.6 Compatibility with Other Packages and Classes¶

When using certain packages or classes together with the beamer class, extra options or precautions may be necessary. 

\usepackage{AlDraTex}

Graphics created using AlDraTex must be treated like verbatim text. The reason is that DraTex fiddles with catcodes and spaces much like verbatim does. So, in order to insert a picture, either add the fragile option to the frame or use the \defverbatim command to create a box containing the picture. 

\usepackage{alltt}

Text in an alltt environment must be treated like verbatim text. So add the fragile option to frames containing this environment or use \defverbatim. 

\usepackage{amsthm}

This package is automatically loaded since beamer uses it for typesetting theorems. If you do not wish it to be loaded, which can be necessary especially in article mode if the package is incompatible with the document class, you can use the class option noamsthm to suppress its loading. See Section [12.4](<Structuring-Presentation-The-Local-Structure.html#section-theorems>) for more details. 

\usepackage[french]{babel}

When using the french style, certain features that clash with the functionality of the beamer class will be turned off. For example, enumerations are still produced the way the theme dictates, not the way the french style does. 

\usepackage[spanish]{babel}

presentation

When using the spanish style, certain features that clash with the functionality of the beamer class will be turned off. In particular, the special behavior of the pointed brackets < and > is deactivated. 

article

To make the characters < and > active in article mode, pass the option activeospeccharacters to the package beamerbasearticle. This will lead to problems with overlay specifications. 

\usepackage{color}

presentation

The color package is automatically loaded by beamer.cls. This makes it impossible to pass options to color in the preamble of your document in the normal manner. To pass a ⟨ _list of options_ ⟩ to color, you can use the following class option: 

\documentclass[color=⟨ _list of options_ ⟩]{beamer} 

Causes the ⟨ _list of options_ ⟩ to be passed on to the color package. If the ⟨ _list of options_ ⟩ contains more than one option you must enclose it in curly brackets. 

article

The color package is not loaded automatically if beamerarticle is loaded with the noxcolor option. 

\usepackage{colortbl}

presentation

With newer versions of xcolor.sty, you need to pass the option table to xcolor.sty if you wish to use colortbl. See the notes on xcolor below, on how to do this. 

\usepackage{CJK}

presentation

When using the CJK package for using Asian fonts, you must use the class option CJK. 

\usepackage{deluxetable}

presentation

The caption generation facilities of deluxetable are deactivated. Instead, the caption template is used. 

\usepackage{DraTex}

See AlDraTex.

\usepackage{enumerate}

article

This package is loaded automatically in the presentation modes, but not in the article mode. If you use its features, you have to load the package “by hand” in the article mode. 

\documentclass{foils}

If you wish to emulate the foils class using beamer, please see Section [24.3](<How-To-Import-Presentations-Based-on-Other-Packages-Classes.html#section-foiltex>). 

\usepackage[T1,TU]{fontenc}

Use the T1 option _only_ with fonts that have outline fonts available in the T1 encoding like times or the lmodern fonts. In a standard installation standard Computer Modern fonts (the fonts Donald Knuth originally designed and which are used by default) are _not_ available in the T1 encoding. Using this option with them will result in very poor rendering of your presentation when viewed with pdf viewer applications like Acrobat, xpdf, evince or okular. To use the Computer Modern fonts with the T1 encoding, make sure you have installed cm-super package in your TeX distribution, or use Latin Modern fonts provided by lmodern instead. See also Section [18.2.3](<Fonts.html#section-font-encoding>). This applies both to latex+dvips and pdflatex. 

The newest version of LaTeX2ε kernel has introduced TU encoding for xelatex and lualatex. Note that xelatex and lualatex support OpenType fonts, and font encodings work very different compared to pdflatex. Again, see Section [18.2.3](<Fonts.html#section-font-encoding>) for more information. 

\usepackage{fourier}

The package switches to a T1 encoding, but it does not redefine all fonts such that outline fonts (non-bitmapped fonts) are used by default. For example, the sans-serif text and the typewriter text are not replaced. To use outline fonts for these, write \usepackage{lmodern} _before_ including the fourier package. 

\usepackage{HA-prosper}

You cannot use this package with beamer. However, you might try to use the package beamerprosper instead, see Section [24.1](<How-To-Import-Presentations-Based-on-Other-Packages-Classes.html#section-prosper>). 

\usepackage{hyperref}

presentation

The hyperref package is automatically loaded by beamer.cls and certain options are set up. In order to pass additional options to hyperref or to override options, you can use the following class option: 

\documentclass[hyperref=⟨ _list of options_ ⟩]{beamer} 

Causes the ⟨ _list of options_ ⟩ to be passed on to the hyperref package. 

_Example:_ \documentclass[hyperref={bookmarks=false}]{beamer}

Alternatively, you can also use the \hypersetup command. 

article

In the article version, you must include hyperref manually if you want to use it. You can do so by passing option hyperref to beamerarticle. It is not included automatically. 

\usepackage[utf8,utf8x]{inputenc}

presentation

When using Unicode, you may wish to use _some_ of the following class options: 

\documentclass[ucs]{beamer}

Loads the package ucs and passes the correct Unicode options to hyperref. Also, it preloads the Unicode code pages zero and one. 

\documentclass[utf8x]{beamer} 

Same as the option ucs, but also sets the input encoding to utf8x. You could also use the option ucs and say \usepackage[utf8x]{inputenc} in the preamble. This also automatically loads ucs package in most TeX systems. 

If you use a Unicode character outside the first two code pages (which includes the Latin alphabet and the extended Latin alphabet) in a section or subsection heading, you have to use the command \PreloadUnicodePage{⟨ _code page_ ⟩} to give ucs a chance to preload these code pages. You will know that a character has not been preloaded, if you get a message like “Please insert into preamble.” The code page of a character is given by the unicode number of the character divided by 256. 

\documentclass[utf8]{beamer}

This option sets the input encoding to utf8. It’s designed to be used _without_ ucs. It’s the same as saying \usepackage[utf8]{inputenc} in the preamble. 

Note that _none_ of these options apply to lualatex and xelatex, since both support Unicode natively without any extra packages. Most of the time using these options actually harms output quality, so be careful about what you use. If you want to have a document that allows compiling with multiple drivers, take a look at iftex, ifxetex and ifluatex packages. 

article

Passing option utf8 to beamerarticle has the same effect as saying \usepackage[utf8]{inputenc} in the preamble. 

Again, take care if you use lualatex or xelatex. 

\usepackage{listings}

presentation

Note that you must treat lstlisting environments exactly the same way as you would treat verbatim environments. When using \defverbatim that contains a colored lstlisting, use the colored option of \defverbatim. 

_Example:_
    
    
    \usepackage{listings}
    
    \begin{document}
    \defverbatim[colored]\mycode{%
      \begin{lstlisting}[frame=single, emph={cout}, emphstyle={\color{blue}}]
        cout << "Hello world!";
      \end{lstlisting}
      }
    
    \begin{frame}
      \mycode
    \end{frame}
    \end{document}
    

\usepackage{msc}

presentation

Since this package uses pstricks internally, everything that applies to pstricks also applies to msc. 

\usepackage{musixtex}

When using MusiXTeX to typeset musical scores, you have to have ![\\\( \\varepsilon \\\)](beameruserguide-images/9020E760374275D66D6ED67719029778.svg)-TeX extensions enabled. Most modern distributions enable that by default both in pdflatex and latex. However, if you have an older distribution, the document must be compiled with pdfelatex or elatex instead of pdflatex or latex. 

Inside a music environment, the \pause is redefined to match MusiXTeX’s definition (a rest during one quarter of a whole). You can use the \beamerpause command to create overlays in this environment. 

\usepackage{paralist}

presentation

beamer automatically patches list-related commands using beamerpatchparalist package at the beginning of document. Besides, beamer also supports using compactitem and compactenum environments with overlays, just like the usage of enumerate environments: 
    
    
    \begin{compactitem}[<+->][$\bullet$]
      \item Alpha
      \item Bravo
    \end{compactitem}
    

\usepackage{pdfpages}

Commands like \includepdf only work _outside_ frames as they produce pages “by themselves.” 

\usepackage{⟨ _professional font package_ ⟩}

presentation

If you use a professional font package, beamer’s internal redefinition of how variables are typeset may interfere with the font package’s superior way of typesetting them. In this case, you should use the class option professionalfonts to suppress any font substitution. See Section [18.2.2](<Fonts.html#section-substition>) for details. 

\documentclass{prosper}

If you wish to (partly) emulate the prosper class using beamer, please see Section [24.1](<How-To-Import-Presentations-Based-on-Other-Packages-Classes.html#section-prosper>). 

\usepackage{pstricks}

You should add the option xcolor=pst to make xcolor aware of the fact that you are using pstricks. 

\documentclass{seminar}

If you wish to emulate the seminar class using beamer, please see Section [24.2](<How-To-Import-Presentations-Based-on-Other-Packages-Classes.html#section-seminar>). 

\usepackage{texpower}

You cannot use this package with beamer. However, you might try to use the package beamertexpower instead, see Section [24.4](<How-To-Import-Presentations-Based-on-Other-Packages-Classes.html#section-texpower>). 

\usepackage{textpos}

presentation

beamer automatically installs a white background behind everything, unless you install a different background template. Because of this, you must use the overlay option when using textpos, so that it will place boxes _in front of_ everything. Alternatively, you can install an empty background template, but this may result in an incorrect display in certain situations with older versions of the Acrobat Reader. 

\usepackage{ucs}

See \usepackage[utf8,utf8x]{inputenc}. 

\usepackage{xcolor}

presentation

The xcolor package is automatically loaded by beamer.cls. The same applies as to color. 

\documentclass[xcolor=⟨ _list of options_ ⟩]{beamer} 

Causes the ⟨ _list of options_ ⟩ to be passed on to the xcolor package. 

When using beamer together with the pstricks package, be sure to pass the xcolor=pst option to beamer (and hence to xcolor). 

article

The color package is not loaded automatically if beamerarticle is loaded with the noxcolor option. 
