## Howtos

####  24 How To Import Presentations Based on  
Other Packages and Classes 

The beamer class comes with a number of emulation layers for classes or packages that do not support beamer directly. For example, the package beamerseminar maps some (not all) commands of the seminar class to appropriate beamer commands. This way, individual slides or whole sets of slides that have been prepared for a presentation using seminar can be used inside beamer, provided they are reasonably simple. 

None of the emulation layers is a perfect substitute for the original (emulations seldom are) and it is not intended that they ever will be. If you want/need/prefer the features of another class, use that class for preparing your presentations. The intention of these layers is just to help speed up creating beamer presentations that use parts of old presentations. You can simply copy these parts in verbatim, without having to worry about the subtle differences in syntax. 

A useful effect of using an emulation layer is that you get access to all the features of beamer while using the syntax of another class. For example, you can use the article mode to create a nice article version of a prosper talk. 

#####  24.1 Prosper, HA-Prosper and Powerdot¶

The package beamerprosper maps the commands of the prosper package, developed by Frédéric Goualard, to beamer commands. Also, some commands of the ha-prosper and powerdot packages, developed by Hendri Adriaens, are mapped to beamer commands. _These mappings cannot perfectly emulate all of Prosper!_ Rather, these mappings are intended as an aid when porting parts of presentations created using prosper to beamer. _No styles are implemented that mimic Prosper styles._ Rather, the normal beamer themes must be used (although, one could implement beamer themes that mimics existing prosper styles; we have not done that and do not intend to). 

The workflow for creating a beamer presentation that uses prosper code is the following: 

  * 1. Use the document class beamer, not prosper. Most options passed to prosper do not apply to beamer and should be omitted. 

  * 2. Add a \usepackage{beamerprosper} to start the emulation. 

  * 3. If you add slides relying on ha-prosper, you may wish to add the option framesassubsections to beamerprosper, though we do not recommend it (use the normal \subsection command instead; it gives you more fine-grained control). 

  * 4. If you also copy the title commands, it may be necessary to adjust the content of commands like \title or \author. Note that in prosper the \email command is given outside the \author command, whereas in beamer and also in ha-prosper it is given inside. 

  * 5. When copying slides containing the command \includegraphics, you will almost surely have to adjust its usage. If you use pdfLaTeX to typeset the presentation, than you cannot include PostScript files. You should convert them to .pdf or to .png and adjust any usage of \includegraphics accordingly. 

  * 6. When starting to change things, you can use all of beamer’s commands and even mix them with prosper commands. 




An example can be found in the file beamerexample-prosper.tex. 

There are, unfortunately, quite a few places where you may run into problems: 

  * • In beamer, the command \PDForPS will do exactly what the name suggests: insert the first argument when run by pdflatex, insert the second argument when run by latex. However, in prosper, the code inserted for the pdf case is actually PostScript code, which is only later converted to pdf by some external program. You will need to adjust this PostScript code such that it works with pdflatex (which is not always possible). 

  * • If you used fine-grained spacing commands, like adding a little horizontal skip here and a big negative vertical skip there, the typesetting of the text may be poor. It may be a good idea to just remove these spacing commands. 

  * • If you use pstricks commands, you will either have to stick to using latex and dvips or will have to work around them using, for example, pgf. Porting lots of pstricks code is bound to be difficult, if you wish to switch over to pdflatex, so be warned. You can read more about that in Section [13](<Graphics.html#section-graphics>) that talks about graphics. 

  * • If the file cannot be compiled because some prosper command is not implemented, you will have to delete this command and try to mimic its behavior using some beamer command. 




\usepackage{beamerprosper}

Include this package in a beamer presentation to get access to prosper commands. Use beamer as the document class, not prosper. Most of the options passed to the class prosper make no sense in beamer, so just delete them. 

This package takes the following options:

  * • framesassubsections causes each frame to create its own subsection with the frame title as subsection name. This behavior mimics ha-prosper’s behavior. In a long talk this will create way too many subsections. 




article

The framesassubsections option has no effect in article mode. 

_Example:_
    
    
    \documentclass[notes]{beamer}
    
    \usepackage[framesassubsections]{beamerprosper}
    
    \title{A Beamer Presentation Using (HA-)Prosper Commands}
    \subtitle{Subtitles Are Also Supported}
    \author{Till Tantau}
    \institution{The Institution is Mapped To Institute}
    
    \begin{document}
    
    \maketitle
    
    \tsectionandpart{Introduction}
    
    \overlays{2}{
    \begin{slide}{About this file}
      \begin{itemstep}
      \item
        This is a beamer presentation.
      \item
        You can use the prosper and the HA-prosper syntax.
      \item
        This is done by mapping prosper and HA-prosper commands to beamer
        commands.
      \item
        The emulation is by no means perfect.
      \end{itemstep}
    \end{slide}
    }
    
    \section{Second Section}
    \subsection{A subsection}
    \begin{frame}
      \frametitle{A frame created using the \texttt{frame} environment.}
    
      \begin{itemize}[<+->]
      \item You can still use the original beamer syntax.
      \item The emulation is intended only to make recycling slides
        easier, not to install a whole new syntax for beamer.
      \end{itemize}
    \end{frame}
    
    \begin{notes}{Notes for these slides}
    My notes for these slides.
    \end{notes}
    \end{document}
    

You can run, for example, pdfLaTeX on the file to get a beamer presentation with overlays. Adding the notes option will also show the notes. Certain commands, like \LeftFoot, are ignored. You can change the theme using the usual commands. You can also use all normal beamer commands and concepts, like overlay-specifications, in the file. You can also create an article version by using the class article and including the package beamerarticle. 

In the following, the effects of prosper commands in beamer are listed. 

`\email`{⟨ _text_ ⟩} 

Simply typesets its argument in typewriter text. Should hence be given _inside_ the \author command. 

`\institution`{⟨ _text_ ⟩} 

This command is mapped to beamer’s \institute command if given _outside_ the \author command, otherwise it typesets its argument in a smaller font. 

`\Logo`(⟨ _x_ ⟩,⟨ _y_ ⟩){⟨ _logo text_ ⟩} 

This is mapped to \logo{⟨ _logo text_ ⟩}. The coordinates are ignored. 

\begin{slide}[⟨ _options_ ⟩]{⟨ _frame title_ ⟩} 

⟨ _environment contents_ ⟩

\end{slide}

Inserts a frame with the fragile=singleslide option set. The ⟨ _frame title_ ⟩ will be enclosed in a \frametitle command. 

The following ⟨ _options_ ⟩ may be given: 

  * • trans=⟨ _prosper transition_ ⟩ installs the specified ⟨ _prosper transition_ ⟩ as the transition effect when showing the slide. 

  * • ⟨ _prosper transition_ ⟩ has the same effect as trans=⟨ _prosper transition_ ⟩. 

  * • toc=⟨ _entry_ ⟩ overrides the subsection table of contents entry created by this slide by ⟨ _entry_ ⟩. Note that a subsection entry is created for a slide only if the framesassubsections options is specified. 

  * • template=⟨ _text_ ⟩ is ignored. 




_Example:_ The following two texts have the same effect:
    
    
    \begin{slide}[trans=Glitter,toc=short]{A Title}
      Hi!
    \end{slide}
    

and
    
    
    \subsection{short} % omitted, if framesassubsections is not specified
    \begin{frame}[fragile=singleslide]
      \transglitter
      \frametitle{A Title}
      Hi!
    \end{frame}
    

`\overlays`{⟨ _number_ ⟩}{⟨ _slide environment_ ⟩} 

This will put the ⟨ _slide environment_ ⟩ into a frame that does not have the fragile option and which can hence contain overlaid text. The ⟨ _number_ ⟩ is ignored since the number of necessary overlays is computed automatically by beamer. 

_Example:_ The following code fragments have the same effect: 
    
    
    \overlays{2}{
    \begin{slide}{A Title}
      \begin{itemstep}
      \item Hi!
      \item Ho!
      \end{itemstep}
    \end{slide}}
    

and
    
    
    \subsection{A Title} % omitted, if framesassubsections is not specified
    \begin{frame}
      \frametitle{A Title}
      \begin{itemstep}
      \item Hi!
      \item Ho!
      \end{itemstep}
    \end{frame}
    

`\fromSlide`{⟨ _slide number_ ⟩}{⟨ _text_ ⟩} 

This is mapped to \uncover<⟨ _slide number_ ⟩->{⟨ _text_ ⟩}. 

`\fromSlide`*{⟨ _slide number_ ⟩}{⟨ _text_ ⟩} 

This is mapped to \only<⟨ _slide number_ ⟩->{⟨ _text_ ⟩}. 

`\onlySlide`{⟨ _slide number_ ⟩}{⟨ _text_ ⟩} 

This is mapped to \uncover<⟨ _slide number_ ⟩>{⟨ _text_ ⟩}. 

`\onlySlide`*{⟨ _slide number_ ⟩}{⟨ _text_ ⟩} 

This is mapped to \only<⟨ _slide number_ ⟩>{⟨ _text_ ⟩}. 

`\untilSlide`{⟨ _slide number_ ⟩}{⟨ _text_ ⟩} 

This is mapped to \uncover<-⟨ _slide number_ ⟩>{⟨ _text_ ⟩}. 

`\untilSlide`*{⟨ _slide number_ ⟩}{⟨ _text_ ⟩} 

This is mapped to \only<-⟨ _slide number_ ⟩>{⟨ _text_ ⟩}. 

`\FromSlide`{⟨ _slide number_ ⟩} 

This is mapped to \onslide<⟨ _slide number_ ⟩->. 

`\OnlySlide`{⟨ _slide number_ ⟩} 

This is mapped to \onslide<⟨ _slide number_ ⟩>. 

`\UntilSlide`{⟨ _slide number_ ⟩} 

This is mapped to \onslide<-⟨ _slide number_ ⟩>. 

`\slideCaption`{⟨ _text_ ⟩} 

This is mapped to \date{⟨ _text_ ⟩}. 

`\fontTitle`{⟨ _text_ ⟩} 

Simply inserts ⟨ _text_ ⟩. 

`\fontText`{⟨ _text_ ⟩} 

Simply inserts ⟨ _text_ ⟩. 

`\PDFtransition`{⟨ _prosper transition_ ⟩} 

Maps the ⟨ _prosper transition_ ⟩ to an appropriate \transxxxx command. 

\begin{Itemize}

⟨ _environment contents_ ⟩

\end{Itemize}

This is mapped to itemize.

\begin{itemstep}

⟨ _environment contents_ ⟩

\end{itemstep}

This is mapped to itemize with the option [<+->]. 

\begin{enumstep}

⟨ _environment contents_ ⟩

\end{enumstep}

This is mapped to enumerate with the option [<+->]. 

`\hiddenitem`

This is mapped to \addtocounter{beamerpauses}{1}. 

`\prosperpart`[⟨ _options_ ⟩]{⟨ _text_ ⟩} 

This command has the same effect as prosper’s \part command. beamer’s normal \part command retains its normal semantics. Thus, you might wish to replace all occurrences of \part by \prosperpart. 

`\tsection`*{⟨ _section name_ ⟩} 

Creates a section named ⟨ _section name_ ⟩. The star, if present, is ignored. 

`\tsectionandpart`*{⟨ _part text_ ⟩} 

Mapped to a \section command followed by a \prosperpart command. 

article

In article mode, no part page is added. 

`\dualslide`[⟨ _x_ ⟩][⟨ _y_ ⟩][⟨ _z_ ⟩]{⟨ _options_ ⟩}{⟨ _left column_ ⟩}{⟨ _right column_ ⟩} 

This command is mapped to a columns environment. The ⟨ _left column_ ⟩ text is shown in the left column, the ⟨ _right column_ ⟩ text is shown in the right column. The options ⟨ _x_ ⟩, ⟨ _y_ ⟩, and ⟨ _z_ ⟩ are ignored. Also, all ⟨ _options_ ⟩ are ignored, except for lcolwidth= and rcolwidth=. These set the width of the left or right column, respectively. 

`\PDForPS`{⟨ _PostScript text_ ⟩}{⟨ _PDF text_ ⟩} 

Inserts either the ⟨ _PostScript text_ ⟩ or the ⟨ _PDF text_ ⟩, depending on whether latex or pdflatex is used. When porting, the ⟨ _PDF text_ ⟩ will most likely be _incorrect_ , since in prosper the ⟨ _PDF text_ ⟩ is actually PostScript text that is later transformed to pdf by some external program. 

If the ⟨ _PDF text_ ⟩ contains an \includegraphics command (which is its usual use), you should change the name of the graphic file that is included to a name ending .pdf, .png, or .jpg. Typically, you will have to convert your graphic to this format. 

`\onlyInPDF`⟨ _PDF text_ ⟩

The ⟨ _PDF text_ ⟩ is only included if pdflatex is used. The same as for the command \PDForPS applies here. 

`\onlyInPS`⟨ _PS text_ ⟩

The ⟨ _PS text_ ⟩ is only included if latex is used. 

\begin{notes}{⟨ _title_ ⟩} 

⟨ _environment contents_ ⟩

\end{notes}

Mapped to \note{\textbf{⟨ _title_ ⟩}⟨ _environment contents_ ⟩} (more or less). 

The following commands are parsed by beamer, but have no effect: 

  * • \myitem, 

  * • \FontTitle, 

  * • \FontText, 

  * • \ColorFoot, 

  * • \DefaultTransition, 

  * • \NoFrenchBabelItemize, 

  * • \TitleSlideNav, 

  * • \NormalSlideNav, 

  * • \HAPsetup, 

  * • \LeftFoot, and 

  * • \RightFoot. 




#####  24.2 Seminar¶

The package beamerseminar maps a subset of the commands of the seminar package to beamer. As for prosper, the emulation cannot be perfect. For example, no portrait slides are supported, no automatic page breaking, the framing of slides is not emulated. Unfortunately, for all frames (slide environments) that contain overlays, you have to put the environment into a frame environment “by hand” and must remove all occurrences of \newslide inside the environment by closing the slide and opening a new one (and then putting these into frame environments). 

The workflow for the migration is the following:

  * 1. Use the document class beamer, not seminar. Most options passed to seminar do not apply to beamer and should be omitted. 

  * 2. If you copy parts of a presentation that is mixed with normal text, add the ignorenonframetext option and place _every_ slide environment inside a frame since beamer will not recognize the \begin{slide} as the beginning of a frame. 

  * 3. Add a \usepackage{beamerseminar} to start the emulation. Add the option accumulated if you wish to create a presentation to be held with a video projector. 

  * 4. Possibly add commands to install themes and templates. 

  * 5. There should not be commands in the preamble having to do with page and slide styles. They do not apply to beamer. 

  * 6. If a \newslide command is used in a slide (or similarly slide*) environment that contains an overlay, you must replace it by a closing \end{slide} and an opening \begin{slide}. 

  * 7. Next, for each slide or slide* environment that contains an overlay, you must place a frame environment around it. You can remove the slide environment (and hence effectively replace it by frame), unless you use the accumulated option. 

  * 8. If you use \section or \subsection commands inside slides, you will have to move them _outside_ the frames. It may then be necessary to add a \frametitle command to the slide. 

  * 9. If you use pdfLaTeX to typeset the presentation, you cannot include PostScript files. You should convert them to .pdf or to .png and adjust any usage of \includegraphics accordingly. 

  * 10. When starting to change things, you can use all of beamer’s commands and even mix them with seminar commands. 




An example can be found in the file beamerexample-seminar.tex. 

There are, unfortunately, numerous places where you may run into problems: 

  * • The whole note management of seminar is so different from beamer’s, that you will have to edit notes “by hand.” In particular, commands like \ifslidesonly and \ifslide may not do exactly what you expect. 

  * • If you use pstricks commands, you will either have to stick to using latex and dvips or will have to work around them using, for example, pgf. Porting lots of pstricks code is bound to be difficult, if you wish to switch over to pdflatex, so be warned. 

  * • If the file cannot be compiled because some seminar command is not implemented, you will have to delete this command and try to mimic its behavior using some beamer command. 




\usepackage{beamerseminar}

Include this package in a beamer presentation to get access to seminar commands. Use beamer as the document class, not seminar. Most of the options passed to the class seminar make no sense in beamer, so just delete them. 

This package takes the following options:

  * • accumulated causes overlays to be accumulated. The original behavior of the seminar package is that in each overlay only the really “new” part of the overlay is shown. This makes sense, if you really print out the overlays on transparencies and then really stack overlays on top of each other. For a presentation with a video projector, you rather want to present an “accumulated” version of the overlays. This is what this option does: When the new material of the ![\\\( i \\\)](beameruserguide-images/D50F79E2E66556E5AE928DD6FF809A89.svg)-th overlay is shown, the material of all previous overlays is also shown. 




_Example:_ The following example is an extract of beamerexample-seminar.tex: 
    
    
    \documentclass[ignorenonframetext]{beamer}
    \usepackage[accumulated]{beamerseminar}
    \usepackage{beamerthemeclassic}
    
    \title{A beamer presentation using seminar commands}
    \author{Till Tantau}
    
    \let\heading=\frametitle
    
    \begin{document}
    
    \begin{frame}
      \maketitle
    \end{frame}
    
    This is some text outside any frame. It will only be shown in the
    article version.
    
    \begin{frame}
      \begin{slide}
        \heading{This is a frame title.}
    
        \begin{enumerate}
          {\overlay1
          \item Overlays are a little tricky in seminar.
            {\overlay2
            \item But it is possible to use them in beamer.
            }
          }
        \end{enumerate}
      \end{slide}
    \end{frame}
    \end{document}
    

You can use all normal beamer commands and concepts, like overlay-specifications, in the file. You can also create an article version by using the class article and including the package beamerarticle. 

In the following, the effects of seminar commands in beamer are listed. 

`\overlay`{⟨ _number_ ⟩} 

Shows the material till the end of the current TeX group only on overlay numbered ![\\\( \\hbox {\\meta {number}}+1 \\\)](beameruserguide-images/57DA1BE2C27ED9FD43860F1C685A8B37.svg) or, if the accumulated option is given, from that overlay on. Usages of this command may be nested (as in seminar). If an \overlay command is given inside another, it temporarily “overrules” the outer one as demonstrated in the following example, where it is assumed that the accumulated option is given. 

_Example:_
    
    
    \begin{frame}
      \begin{slide}
        This is shown from the first slide on.
        {\overlay{2}
          This is shown from the third slide on.
          {\overlay{1}
            This is shown from the second slide on.
          }
          This is shown once more from the third slide on.
        }
      \end{slide}
    \end{frame}
    

\begin{slide}*

⟨ _environment contents_ ⟩

\end{slide}

Mainly installs an \overlay{0} around the ⟨ _environment contents_ ⟩. If the accumulated option is given, this has no effect, but otherwise it will cause the main text of the slide to be shown _only_ on the first slide. This is useful if you really wish to physically place slides on top of each other. 

The starred version does the same as the nonstarred one.

If this command is not issued inside a \frame, it sets up a frame with the fragile=singleframe option set. Thus, this frame will contain only a single slide. 

_Example:_
    
    
    \begin{slide}
      Some text.
    \end{slide}
    
    \frame{
    \begin{slide}
      Some text. And an {\overlay{1} overlay}.
    \end{slide}
    }
    

`\red`

Mapped to \color{red}.

`\blue`

Mapped to \color{blue}.

`\green`

Mapped to \color{green}.

`\ifslide`

True in the presentation modes, false in the article mode. 

`\ifslidesonly`

Same as \ifslide.

`\ifarticle`

False in the presentation modes, true in the article mode. 

`\ifportrait`

Always false.

The following commands are parsed by beamer, but have no effect: 

  * • \ptsize. 




#####  24.3 FoilTeX¶

The package beamerfoils maps a subset of the commands of the foils package to beamer. Since this package defines only few non-standard TeX commands and since beamer implements all the standard commands, the emulation layer is pretty simple. 

A copyright notice: The FoilTeX package has a restricted license. For this reason, no example from the foils package is included in the beamer class. The emulation itself does not use the code of the foils package (rather, it just maps foils commands to beamer commands). For this reason, our understanding is that the _emulation_ offered by the beamer class is “free” and legally so. IBM has a copyright on the foils class, not on the effect the commands of this class have. (At least, that’s our understanding of things.) 

The workflow for the migration is the following:

  * 1. Use the document class beamer, not foils. 

  * 2. Add a \usepackage{beamerfoils} to start the emulation. 

  * 3. Possibly add commands to install themes and templates. 

  * 4. If the command \foilhead is used inside a \frame command or frame environment, it behaves like \frametitle. If it used outside a frame, it will start a new frame (with the allowframebreaks option, thus no overlays are allowed). This frame will persist till the next occurrence of \foilhead or of the new command \endfoil. Note that a \frame command will _not_ end a frame started using \foilhead. 

  * 5. If you rely on automatic frame creation based on \foilhead, you will need to insert an \endfoil before the end of the document to end the last frame. 

  * 6. If you use pdfLaTeX to typeset the presentation, than you cannot include PostScript files. You should convert them to .pdf or to .png and adjust any usage of \includegraphics accordingly. 

  * 7. Sizes of objects are different in beamer, since the scaling is done by the viewer, not by the class. Thus a framebox of size 6 inches will be way too big in a beamer presentation. You will have to manually adjust explicit dimension occurring in a foilTeX presentation. 




\usepackage{beamerfoils}

Include this package in a beamer presentation to get access to foils commands. Use beamer as the document class, not foils. 

_Example:_ In the following example, frames are automatically created. The \endfoil at the end is needed to close the last frame. 
    
    
    \documentclass{beamer}
    \usepackage{beamerfoils}
    
    \begin{document}
    
    \maketitle
    
    \foilhead{First Frame}
    
    This is on the first frame.
    \pagebreak
    This is on the second frame, which is a continuation of the first.
    
    \foilhead{Third Frame}
    
    This is on the third frame.
    
    \endfoil
    \end{document}
    

_Example:_ In this example, frames are manually inserted. No \endfoil is needed. 
    
    
    \documentclass{beamer}
    \usepackage{beamerfoils}
    
    \begin{document}
    
    \frame{\maketitle}
    
    \frame{
    \foilhead{First Frame}
    This is on the first frame.
    }
    
    \frame{
    \foilhead{Second Frame}
    This is on the second frame.
    }
    \end{document}
    

In the following, the effects of foils commands in beamer are listed. 

`\MyLogo`{⟨ _logo text_ ⟩} 

This is mapped to \logo, though the logo is internally stored, such that it can be switched on and off using \LogoOn and \LogoOff. 

`\LogoOn`

Makes the logo visible.

`\LogoOff`

Makes the logo invisible.

`\foilhead`[⟨ _dimension_ ⟩]{⟨ _frame title_ ⟩} 

If used inside a \frame command or frame environment, this is mapped to \frametitle{⟨ _frame title_ ⟩}. If used outside any frames, a new frame is started with the option allowframebreaks. If a frame was previously started using this command, it will be closed before the next frame is started. The ⟨ _dimension_ ⟩ is ignored. 

`\rotatefoilhead`[⟨ _dimension_ ⟩]{⟨ _frame title_ ⟩} 

This command has exactly the same effect as \foilhead. 

`\endfoil`

This is a command that is _not_ available in foils. In beamer, it can be used to end a frame that has automatically been opened using \foildhead. This command must be given before the end of the document if the last frame was opened using \foildhead. 

\begin{boldequation}*

⟨ _environment contents_ ⟩

\end{boldequation}

This is mapped to the equation or the equation* environment, with \boldmath switched on. 

`\FoilTeX`

Typesets the foilTeX name as in the foils package. 

`\bm`{⟨ _text_ ⟩} 

Implemented as in the foils package. 

`\bmstyle`{⟨ _text_ ⟩}{⟨ _more text_ ⟩} 

Implemented as in the foils package. 

The following additional theorem-like environments are predefined: 

  * • Theorem*, 

  * • Lemma*, 

  * • Corollary*, 

  * • Proposition*, and 

  * • Definition*. 




For example, the first is defined using \newtheorem*{Theorem*}{Theorem}. 

The following commands are parsed by beamer, but have no effect: 

  * • \leftheader, 

  * • \rightheader, 

  * • \leftfooter, 

  * • \rightfooter, 

  * • \Restriction, and 

  * • \marginpar. 




#####  24.4TeX Power¶

The package beamertexpower maps a subset of the commands of the texpower package, due to Stephan Lehmke, to beamer. This subset is currently rather small, so a lot of adaptions may be necessary. Note that texpower is not a full class by itself, but a package that needs another class, like seminar or prosper to do the actual typesetting. It may thus be necessary to additionally load an emulation layer for these also. Indeed, it _might_ be possible to directly use texpower inside beamer, but we have not tried that. Perhaps this will be possible in the future. 

Currently, the package beamertexpower mostly just maps the \stepwise and related commands to appropriate beamer commands. The \pause command need not be mapped since it is directly implemented by beamer anyway. 

The workflow for the migration is the following:

  * 1. Replace the document class by beamer. If the document class is seminar or prosper, you can use the above emulation layers, that is, you can include the files beamerseminar or beamerprosper to emulate the class. 

All notes on what to do for the emulation of seminar or prosper also apply here. 

  * 2. Additionally, add \usepackage{beamertexpower} to start the emulation. 




\usepackage{beamertexpower}

Include this package in a beamer presentation to get access to the texpower commands having to do with the \stepwise command. 

A note on the \pause command: Both beamer and texpower implement this command and they have the same semantics; so there is no need to map this command to anything different in beamertexpower. However, a difference is that \pause can be used almost anywhere in beamer, whereas it may only be used in non-nested situations in texpower. Since beamer is only more flexible than texpower here, this will not cause problems when porting. 

In the following, the effect of texpower commands in beamer are listed. 

`\stepwise`{⟨ _text_ ⟩} 

As in texpower, this initiates text in which commands like \step or \switch may be given. Text contained in a \step command will be enclosed in an \only command with the overlay specification <+(1)->. This means that the text of the first \step is inserted from the second slide onward, the text of the second \step is inserted from the third slide onward, and so on. 

`\parstepwise`{⟨ _text_ ⟩} 

Same as \stepwise, only \uncover is used instead of \only when mapping the \step command. 

`\liststepwise`{⟨ _text_ ⟩} 

Same as \stepwise, only an invisible horizontal line is inserted before the ⟨ _text_ ⟩. This is presumably useful for solving some problems related to vertical spacing in texpower. 

`\step`{⟨ _text_ ⟩} 

This is either mapped to \only<+(1)->⟨ _text_ ⟩ or to \uncover<+(1)->⟨ _text_ ⟩, depending on whether this command is used inside a \stepwise environment or inside a \parstepwise environment. 

`\steponce`{⟨ _text_ ⟩} 

This is either mapped to \only<+(1)>⟨ _text_ ⟩ or to \uncover<+(1)>⟨ _text_ ⟩, depending on whether this command is used inside a \stepwise environment or inside a \parstepwise environment. 

`\switch`{⟨ _alternate text_ ⟩}{⟨ _text_ ⟩} 

This is mapped to \alt<+(1)->{⟨ _text_ ⟩}{⟨ _alternate text_ ⟩}. Note that the arguments are swapped. 

`\bstep`{⟨ _text_ ⟩} 

This is always mapped to \uncover<+(1)->⟨ _text_ ⟩. 

`\dstep`

This just advances the counter beamerpauses by one. It has no other effect. 

`\vstep`

Same as \dstep.

`\restep`{⟨ _text_ ⟩} 

Same as \step, but the ⟨ _text_ ⟩ is shown on the same slide as the previous \step command. This is implemented by first decreasing the counter beamerpauses by one before calling \step. 

`\reswitch`{⟨ _alternate text_ ⟩}⟨ _text_ ⟩

Like \restep, only for the \switch command. 

`\rebstep`⟨ _text_ ⟩

Like \restep, only for the \bstep command. 

`\redstep`

This command has no effect.

`\revstep`

This command has no effect.

`\boxedsteps`

Temporarily (for the current TeX group) changes the effect of \step to issue an \uncover, even if used inside a \stepwise environment. 

`\nonboxedsteps`

Temporarily (for the current TeX group) changes the effect of \step to issue an \only, even if used inside a \parstepwise environment. 

`\code`{⟨ _text_ ⟩} 

Typesets the argument using a boldface typewriter font.

`\codeswitch`

Switches to a boldface typewriter font.
