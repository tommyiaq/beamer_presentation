## Building a Presentation

####  9 Creating Overlays 

#####  9.1 The Pause Commands¶

The pause command offers an easy, but not very flexible way of creating frames that are uncovered piecewise. If you say \pause somewhere in a frame, only the text on the frame up to the \pause command is shown on the first slide. On the second slide, everything is shown up to the second \pause, and so forth. You can also use \pause inside environments; its effect will last after the environment. However, taking this to extremes and using \pause deeply within a nested environment may not have the desired result. 

A much more fine-grained control over what is shown on each slide can be attained using overlay specifications, see the next sections. However, for many simple cases the \pause command is sufficient. 

The effect of \pause lasts till the next \pause, \onslide, or the end of the frame. 
    
    
    \begin{frame}
      \begin{itemize}
      \item
        Shown from first slide on.
      \pause
      \item
        Shown from second slide on.
        \begin{itemize}
        \item
          Shown from second slide on.
        \pause
        \item
          Shown from third slide on.
        \end{itemize}
      \item
        Shown from third slide on.
      \pause
      \item
        Shown from fourth slide on.
      \end{itemize}
    
      Shown from fourth slide on.
    
      \begin{itemize}
      \onslide
      \item
        Shown from first slide on.
      \pause
      \item
        Shown from fifth slide on.
      \end{itemize}
    \end{frame}
    

`\pause`[⟨ _number_ ⟩]

This command causes the text following it to be shown only from the next slide on, or, if the optional ⟨ _number_ ⟩ is given, from the slide with the number ⟨ _number_ ⟩. If the optional ⟨ _number_ ⟩ is given, the counter beamerpauses is set to this number. This command uses the \onslide command, internally. This command does _not_ work correctly inside amsmath environments like align and pgf environements like tikzpicture or tcolorbox, since these do really wicked things. 

_Example:_
    
    
    \begin{frame}
      \begin{itemize}
      \item
        A
      \pause
      \item
        B
      \pause
      \item
        C
      \end{itemize}
    \end{frame}
    

article

This command is ignored.

To “unpause” some text, that is, to temporarily suspend pausing, use the command \onslide, see below. 

#####  9.2 The General Concept of Overlay Specifications¶

The approach taken by most presentation classes to overlays is somewhat similar to the above \pause command. These commands get a certain slide number as input and affect the text on the slide following this command in a certain way. For example, prosper’s \FromSlide{2} command causes all text following this command to be shown only from the second slide on. 

The beamer class uses a different approach (though the abovementioned command is also available: \onslide<2-> will have the same effect as \FromSlide{2}, except that \onslide transcends environments; likewise, \pause is internally mapped to a command with an appropriate overlay specification). The idea is to add _overlay specifications_ to certain commands. These specifications are always given in pointed brackets and follow the command “as soon as possible,” though in certain cases beamer also allows overlay specification to be given a little later. In the simplest case, the specification contains just a number. A command with an overlay specification following it will only have “effect” on the slide(s) mentioned in the specification. What exactly “having an effect” means, depends on the command. Consider the following example. 
    
    
    \begin{frame}
      \textbf{This line is bold on all three slides.}
      \textbf<2>{This line is bold only on the second slide.}
      \textbf<3>{This line is bold only on the third slide.}
    \end{frame}
    

For the command \textbf, the overlay specification causes the text to be set in boldface only on the specified slides. On all other slides, the text is set in a normal font. 

For a second example, consider the following frame:
    
    
    \begin{frame}
      \only<1>{This line is inserted only on slide 1.}
      \only<2>{This line is inserted only on slide 2.}
    \end{frame}
    

The command \only, which is introduced by beamer, normally simply inserts its parameter into the current frame. However, if an overlay specification is present, it “throws away” its parameter on slides that are not mentioned. 

Overlay specifications can only be written behind certain commands, not every command. Which commands you can use and which effects this will have is explained in the next section. However, it is quite easy to redefine an existing command such that it becomes “overlay specification aware,” see also Section [9.3](<Creating-Overlays.html#section-overlay-commands>). 

The syntax of (basic) overlay specifications is the following: They are comma-separated lists of slides and ranges. Ranges are specified like this: 2-5, which means slide two through to five. The start or the end of a range can be omitted. For example, 3- means “slides three, four, five, and so on” and -5 means the same as 1-5. A complicated example is -3,6-8,10,12-15, which selects the slides 1, 2, 3, 6, 7, 8, 10, 12, 13, 14, and 15. 

#####  9.3 Commands with Overlay Specifications¶

**Important:** Due to the way overlay specifications are implemented, the commands documented here are _all_ fragile even if the LaTeX2ε kernel versions are not. 

For the following commands, adding an overlay specification causes the command to be simply ignored on slides that are not included in the specification: \textbf, \textit, \textmd, \textnormal, \textrm, \textsc, \textsf, \textsl, \texttt, \textup, \emph; \color, \textcolor; \alert, \structure. If a command takes several arguments, like \color, the specification should directly follow the command as in the following example (but there are exceptions to this rule): 
    
    
    \begin{frame}
      \color<2-3>[rgb]{1,0,0} This text is red on slides 2 and 3, otherwise black.
    \end{frame}
    

For the following commands, the effect of an overlay specification is special: 

`\onslide`⟨ _modifier_ ⟩<⟨ _overlay specification_ ⟩>{⟨ _text_ ⟩}

The behavior of this command depends on whether the optional argument ⟨ _text_ ⟩ is given or not (note that the optional argument is given in _normal_ braces, not in square brackets). If present, the ⟨ _modifier_ ⟩ can be either a + or a *. 

If no ⟨ _text_ ⟩ is given, the following happens: All text following this command will only be shown (uncovered) on the specified slides. On non-specified slides, the text still occupies space. If no slides are specified, the following text is always shown. You need not call this command in the same TeX group, its effect transcends block groups. However, this command has a _different_ effect inside an overprint environment, see the description of overprint. 

If the ⟨ _modifier_ ⟩ is +, hidden text will not be treated as covered, but as invisible. The difference is the same as the difference between \uncover and \visible. The modifier * may not be given if no ⟨ _text_ ⟩ argument is present. 

_Example:_
    
    
    \begin{frame}
      Shown on first slide.
      \onslide<2-3>
      Shown on second and third slide.
      \begin{itemize}
      \item
        Still shown on the second and third slide.
      \onslide+<4->
      \item
        Shown from slide 4 on.
      \end{itemize}
      Shown from slide 4 on.
      \onslide
      Shown on all slides.
    \end{frame}
    

If a ⟨ _text_ ⟩ argument is present, \onslide (without a ⟨ _modifier_ ⟩) is mapped to \uncover, \onslide+ is mapped to \visible, and \onslide* is mapped to \only. 

_Example:_
    
    
    \begin{frame}
      \onslide<1>{Same effect as the following command.}
      \uncover<1>{Same effect as the previous command.}
    
      \onslide+<2>{Same effect as the following command.}
      \visible<2>{Same effect as the previous command.}
    
      \onslide*<3>{Same effect as the following command.}
      \only<3>{Same effect as the previous command.}
    \end{frame}
    

`\only`<⟨ _overlay specification_ ⟩>{⟨ _text_ ⟩}<⟨ _overlay specification_ ⟩>

If either ⟨ _overlay specification_ ⟩ is present (though only one may be present), the ⟨ _text_ ⟩ is inserted only into the specified slides. For other slides, the text is simply thrown away. In particular, it occupies no space. 

_Example:_ \only<3->{Text inserted from slide 3 on.}

Since the overlay specification may also be given after the text, you can often use \only to make other commands overlay specification-aware in a simple manner: 

_Example:_
    
    
    \newcommand{\myblue}{\only{\color{blue}}}
    \begin{frame}
      \myblue<2> This text is blue only on slide 2.
    \end{frame}
    

`\uncover`<⟨ _overlay specification_ ⟩>{⟨ _text_ ⟩} 

If the ⟨ _overlay specification_ ⟩ is present, the ⟨ _text_ ⟩ is shown (“uncovered”) only on the specified slides. On other slides, the text still occupies space and it is still typeset, but it is not shown or only shown as if transparent. For details on how to specify whether the text is invisible or just transparent see Section [17.6](<Colors.html#section-transparent>). 

_Example:_ \uncover<3->{Text shown from slide 3 on.}

article

This command has the same effect as \only. 

`\visible`<⟨ _overlay specification_ ⟩>{⟨ _text_ ⟩} 

This command does almost the same as \uncover. The only difference is that if the text is not shown, it is never shown in a transparent way, but rather it is not shown at all. Thus, for this command the transparency settings have no effect. 

_Example:_ \visible<2->{Text shown from slide 2 on.}

article

This command has the same effect as \only. 

`\invisible`<⟨ _overlay specification_ ⟩>{⟨ _text_ ⟩} 

This command is the opposite of \visible. 

_Example:_ \invisible<-2>{Text shown from slide 3 on.}

`\alt`<⟨ _overlay specification_ ⟩>{⟨ _default text_ ⟩}{⟨ _alternative text_ ⟩}<⟨ _overlay specification_ ⟩>

Only one ⟨ _overlay specification_ ⟩ may be given. The default text is shown on the specified slides, otherwise the alternative text. The specification must always be present. 

_Example:_ \alt<2>{On Slide 2}{Not on slide 2.}

Once more, giving the overlay specification at the end is useful when the command is used inside other commands. 

_Example:_ Here is the definition of \uncover: 
    
    
    \newcommand{\uncover}{\alt{\@firstofone}{\makeinvisible}}
    

`\temporal`<⟨ _overlay specification_ ⟩>{⟨ _before slide text_ ⟩}{⟨ _default text_ ⟩}{⟨ _after slide text_ ⟩} 

This command alternates between three different texts, depending on whether the current slide is temporally before the specified slides, is one of the specified slides, or comes after them. If the ⟨ _overlay specification_ ⟩ is not an interval (that is, if it has a “hole”), the “hole” is considered to be part of the before slides. 

_Example:_
    
    
     \temporal<3-4>{Shown on 1, 2}{Shown on 3, 4}{Shown 5, 6, 7, ...}
     \temporal<3,5>{Shown on 1, 2, 4}{Shown on 3, 5}{Shown 6, 7, 8, ...}
    

As a possible application of the \temporal command consider the following example: 

_Example:_
    
    
    \def\colorize<#1>{%
      \temporal<#1>{\color{red!50}}{\color{black}}{\color{black!50}}}
    
    \begin{frame}
      \begin{itemize}
        \colorize<1> \item First item.
        \colorize<2> \item Second item.
        \colorize<3> \item Third item.
        \colorize<4> \item Fourth item.
      \end{itemize}
    \end{frame}
    

`\item`<⟨ _alert specification_ ⟩>[⟨ _item label_ ⟩]<⟨ _alert specification_ ⟩>

presentation

Only one ⟨ _alert specification_ ⟩ may be given. The effect of ⟨ _alert specification_ ⟩ is described in Section [9.6.3](<Creating-Overlays.html#section-action-specifications>). 

_Example:_
    
    
    \begin{frame}
      \begin{itemize}
      \item<1-> First point, shown on all slides.
      \item<2-> Second point, shown on slide 2 and later.
      \item<2-> Third point, also shown on slide 2 and later.
      \item<3-> Fourth point, shown on slide 3.
      \end{itemize}
    \end{frame}
    
    \begin{frame}
      \begin{enumerate}
      \item<3-| alert@3>[0.] A zeroth point, shown at the very end.
      \item<1-| alert@1> The first and main point.
      \item<2-| alert@2> The second point.
      \end{enumerate}
    \end{frame}
    

article

The ⟨ _action specification_ ⟩ is currently completely ignored. 

The related command \bibitem is also overlay specification-aware in the same way as \item. 

`\label`<⟨ _overlay specification_ ⟩>{⟨ _label name_ ⟩} 

If the ⟨ _overlay specification_ ⟩ is present, the label is only inserted on the specified slide. Inserting a label on more than one slide will cause a ‘multiple labels’ warning. _However_ , if no overlay specification is present, the specification is automatically set to just ‘1’ and the label is thus inserted only on the first slide. This is typically the desired behavior since it does not really matter on which slide the label is inserted, _except_ if you use an \only command and _except_ if you wish to use that label as a hyperjump target. Then you need to specify a slide. 

Labels can be used as target of hyperjumps. A convenient way of labelling a frame is to use the label=⟨ _name_ ⟩ option of the frame environment. However, this will cause the whole frame to be kept in memory till the end of the compilation, which may pose a problem. 

_Example:_
    
    
    \begin{frame}
      \begin{align}
        a &= b + c \label{first}\\ % no specification needed
        c &= d + e \label{second}% no specification needed
      \end{align}
    
      Blah blah, \uncover<2>{more blah blah.}
    
      \only<3>{Specification is needed now.\label<3>{mylabel}}
    \end{frame}
    

#####  9.4 Environments with Overlay Specifications¶

Environments can also be equipped with overlay specifications. For most of the predefined environments, see Section [12.3](<Structuring-Presentation-The-Local-Structure.html#predefined>), adding an overlay specification causes the whole environment to be uncovered only on the specified slides. This is useful for showing things incrementally as in the following example. 
    
    
    \begin{frame}
      \frametitle{A Theorem on Infinite Sets}
    
      \begin{theorem}<1->
        There exists an infinite set.
      \end{theorem}
    
      \begin{proof}<3->
        This follows from the axiom of infinity.
      \end{proof}
    
      \begin{example}<2->
        The set of natural numbers is infinite.
      \end{example}
    \end{frame}
    

In the example, the first slide only contains the theorem, on the second slide an example is added, and on the third slide the proof is also shown. 

For each of the basic commands \only, \alt, \visible, \uncover, and \invisible there exists “environment versions” onlyenv, altenv, visibleenv, uncoverenv, and invisibleenv. Except for altenv and onlyenv, these environments do the same as the commands. 

\begin{onlyenv}<⟨ _overlay specification_ ⟩>

⟨ _environment contents_ ⟩

\end{onlyenv}

If the ⟨ _overlay specification_ ⟩ is given, the contents of the environment is inserted into the text only on the specified slides. The difference to \only is, that the text is actually typeset inside a box that is then thrown away, whereas \only immediately throws away its contents. If the text is not “typesettable,” the onlyenv may produce an error where \only would not. 

_Example:_
    
    
    \begin{frame}
      This line is always shown.
      \begin{onlyenv}<2>
        This line is inserted on slide 2.
      \end{onlyenv}
    \end{frame}
    

\begin{altenv}<⟨ _overlay specification_ ⟩>{⟨ _begin text_ ⟩}{⟨ _end text_ ⟩}{⟨ _alternate begin text_ ⟩}{⟨ _alternate end text_ ⟩}<⟨ _overlay specification_ ⟩>

⟨ _environment contents_ ⟩

\end{altenv}

Only one ⟨ _overlay specification_ ⟩ may be given. On the specified slides, ⟨ _begin text_ ⟩ will be inserted at the beginning of the environment and ⟨ _end text_ ⟩ will be inserted at the end. On all other slides, ⟨ _alternate begin text_ ⟩ and ⟨ _alternate end text_ ⟩ will be used. 

_Example:_
    
    
    \begin{frame}
      This
      \begin{altenv}<2>{(}{)}{[}{]}
        word
      \end{altenv}
      is in round brackets on slide 2 and in square brackets on slide 1.
    \end{frame}
    

#####  9.5 Dynamically Changing Text or Images¶

You may sometimes wish to have some part of a frame change dynamically from slide to slide. On each slide of the frame, something different should be shown inside this area. You could achieve the effect of dynamically changing text by giving a list of \only commands like this: 
    
    
      \only<1>{Initial text.}
      \only<2>{Replaced by this on second slide.}
      \only<3>{Replaced again by this on third slide.}
    

The trouble with this approach is that it may lead to slight, but annoying differences in the heights of the lines, which may cause the whole frame to “wobble” from slide to slide. This problem becomes much more severe if the replacement text is several lines long. 

To solve this problem, you can use two environments: overlayarea and overprint. The first is more flexible, but less user-friendly. 

\begin{overlayarea}{⟨ _area width_ ⟩}{⟨ _area height_ ⟩} 

⟨ _environment contents_ ⟩

\end{overlayarea}

Everything within the environment will be placed in a rectangular area of the specified size. The area will have the same size on all slides of a frame, regardless of its actual contents. 

_Example:_
    
    
    \begin{overlayarea}{\textwidth}{3cm}
      \only<1>{Some text for the first slide.\\Possibly several lines long.}
      \only<2>{Replacement on the second slide.}
    \end{overlayarea}
    

\begin{overprint}[⟨ _area width_ ⟩]

⟨ _environment contents_ ⟩

\end{overprint}

The ⟨ _area width_ ⟩ defaults to the text width. Inside the environment, use \onslide commands to specify different things that should be shown for this environment on different slides. The \onslide commands are used like \item commands. Everything within the environment will be placed in a rectangular area of the specified width. The height and depth of the area are chosen large enough to accommodate the largest contents of the area. The overlay specifications of the \onslide commands must be disjoint. This may be a problem for handouts, since, there, all overlay specifications default to 1. If you use the option handout, you can disable all but one \onslide by setting the others to 0. 

_Example:_
    
    
    \begin{overprint}
      \onslide<1| handout:1>
        Some text for the first slide.\\
        Possibly several lines long.
      \onslide<2| handout:0>
        Replacement on the second slide. Suppressed for handout.
    \end{overprint}
    

A similar need for dynamical changes arises when you have, say, a series of pictures named first.pdf, second.pdf, and third.pdf that show different stages of some process. To make a frame that shows these pictures on different slides, the following code might be used: 
    
    
    \begin{frame}
      \frametitle{The Three Process Stages}
    
      \includegraphics<1>{first.pdf}
      \includegraphics<2>{second.pdf}
      \includegraphics<3>{third.pdf}
    \end{frame}
    

The above code uses the fact the beamer makes the \includegraphics command overlay specification-aware. It works nicely, but only if each .pdf file contains the complete graphic to be shown. However, some programs, like xfig, sometimes also produce series of graphics in which each file just contains the _additional_ graphic elements to be shown on the next slide. In this case, the first graphic must be shown not on overlay 1, but from overlay 1 on, and so on. While this is easy to achieve by changing the overlay specification <1> to <1->, the graphics must also be shown _on top of each other_. An easy way to achieve this is to use TeX’s \llap command like this: 
    
    
    \begin{frame}
      \frametitle{The Three Process Stages}
    
      \includegraphics<1->{first.pdf}%
      \llap{\includegraphics<2->{second.pdf}}%
      \llap{\includegraphics<3->{third.pdf}}
    \end{frame}
    

or like this:
    
    
    \begin{frame}
      \frametitle{The Three Process Stages}
    
      \includegraphics{first.pdf}%
      \pause%
      \llap{\includegraphics{second.pdf}}%
      \pause%
      \llap{\includegraphics{third.pdf}}
    \end{frame}
    

A more convenient way is to use the \multiinclude command, see Section [14.1.3](<Animations-Sounds-Slide-Transitions.html#section-xmpmulti>) for details. 

#####  9.6 Advanced Overlay Specifications¶

######  9.6.1 Making Commands and Environments Overlay Specification-Aware¶

This section explains how to define new commands that are overlay specification-aware. Also, it explains how to setup counters correctly that should be increased from frame to frame (like equation numbering), but not from slide to slide. You may wish to skip this section, unless you want to write your own extensions to the beamer class. 

beamer extends the syntax of LaTeX’s standard command \newcommand: 

`\newcommand`<>{⟨ _command name_ ⟩}[⟨ _argument number_ ⟩][⟨ _default optional value_ ⟩]{⟨ _text_ ⟩} 

Declares the new command named ⟨ _command name_ ⟩. The ⟨ _text_ ⟩ should contain the body of this command and it may contain occurrences of parameters like #⟨ _number_ ⟩. Here ⟨ _number_ ⟩ may be between 1 and ⟨ _argument number_ ⟩ ![\\\( +1 \\\)](beameruserguide-images/8AFDC0E110595641EA1329A41E27AA16.svg). The additionally allowed argument is the overlay specification. 

When ⟨ _command name_ ⟩ is used, it will scan as many as ⟨ _argument number_ ⟩ arguments. While scanning them, it will look for an overlay specification, which may be given between any two arguments, before the first argument, or after the last argument. If it finds an overlay specification like <3>, it will call ⟨ _text_ ⟩ with arguments 1 to ⟨ _argument number_ ⟩ set to the normal arguments and the argument number ⟨ _argument number_ ⟩ ![\\\( +1 \\\)](beameruserguide-images/8AFDC0E110595641EA1329A41E27AA16.svg) set to <3> (including the pointed brackets). If no overlay specification is found, the extra argument is empty. 

If the ⟨ _default optional value_ ⟩ is provided, the first argument of ⟨ _command name_ ⟩ is optional. If no optional argument is specified in square brackets, the ⟨ _default optional value_ ⟩ is used. 

_Example:_ The following command will typeset its argument in red on the specified slides: 
    
    
    \newcommand<>{\makered}[1]{{\color#2{red}#1}}
    

_Example:_ Here is beamer’s definition of \emph: 
    
    
    \newcommand<>{\emph}[1]{{\only#2{\itshape}#1}}
    

_Example:_ Here is beamer’s definition of \transdissolve (the command \beamer@dotrans mainly passes its argument to hyperref): 
    
    
    \newcommand<>{\transdissolve}[1][]{\only#2{\beamer@dotrans[#1]{Dissolve}}}
    

`\renewcommand`<>{⟨ _existing command name_ ⟩}[⟨ _argument number_ ⟩][⟨ _default optional value_ ⟩]{⟨ _text_ ⟩} 

Redeclares a command that already exists in the same way as \newcommand<>. Inside ⟨ _text_ ⟩, you can still access to original definitions using the command \beameroriginal, see the example. 

_Example:_ This command is used in beamer to make \hyperlink overlay specification-aware: 
    
    
    \renewcommand<>{\hyperlink}[2]{\only#3{\beameroriginal{\hyperlink}{#1}{#2}}}
    

`\newenvironment`<>{⟨ _environment name_ ⟩}[⟨ _argument number_ ⟩][⟨ _default optional value_ ⟩]  
{⟨ _begin text_ ⟩}{⟨ _end text_ ⟩} 

Declares a new environment that is overlay specification-aware. If this environment is encountered, the same algorithm as for \newcommand<> is used to parse the arguments and the overlay specification. 

Note that, as always, the ⟨ _end text_ ⟩ may not contain any arguments like #1. In particular, you do not have access to the overlay specification. In this case, it is usually a good idea to use altenv environment in the ⟨ _begin text_ ⟩. 

_Example:_ Declare your own action block:
    
    
    \newenvironment<>{myboldblock}[1]{%
      \begin{actionenv}#2%
        \textbf{#1}
        \par}
      {\par%
      \end{actionenv}}
    
    \begin{frame}
      \begin{myboldblock}{A title for the theorem}<2>
        This theorem is shown only on the second slide.
      \end{myboldblock}
    \end{frame}
    

_Example:_ Text in the following environment is bold on specified slides and of normal weight on non-specified slides: 
    
    
    \newenvironment<>{boldornormal}
      {\begin{altenv}#1
        {\begin{bfseries}}{\end{bfseries}}
        {}{}}
      {\end{altenv}}
    

Incidentally, since altenv also accepts its argument at the end, the same effect could have been achieved using just 
    
    
    \newenvironment{boldornormal}
      {\begin{altenv}
        {\begin{bfseries}}{\end{bfseries}}
        {}{}}
      {\end{altenv}}
    

`\renewenvironment`<>{⟨ _existing environment name_ ⟩}[⟨ _argument number_ ⟩][⟨ _default optional value_ ⟩]  
{⟨ _begin text_ ⟩}{⟨ _end text_ ⟩} 

Redefines an existing environment. The original environment is still available under the name original⟨ _existing environment name_ ⟩. 

_Example:_
    
    
    \renewenvironment<>{center}
        {\begin{actionenv}#1\begin{originalcenter}}
        {\end{originalcenter}\end{actionenv}}
    

In a similar way \NewDocumentCommand, \NewDocumentEnvironment etc. can be used to define overlay aware commands and environments. The overlay argument can be specified via d<> (without default value) or D<>{} (with default value) type arguments. 

_Example:_
    
    
    \NewDocumentCommand{\makeblue}{D<>{.-} m}{{\color<#1>{blue}#2}}
    

Note that by using \NewDocumentCommand, \NewDocumentEnvironment etc. the original definition of the command or environment won’t be retained as \beameroriginal{...} or \begin{original...}. 

The following two commands can be used to ensure that a certain counter is automatically reset on subsequent slides of a frame. This is necessary for example for the equation count. You might want this count to be increased from frame to frame, but certainly not from overlay slide to overlay slide. For equation counters and footnote counters (you should not use footnotes), these commands have already been invoked. 

`\resetcounteronoverlays`{⟨ _counter name_ ⟩} 

After you have invoked this command, the value of the specified counter will be the same on all slides of every frame. 

_Example:_ \resetcounteronoverlays{equation}

`\resetcountonoverlays`{⟨ _count register name_ ⟩} 

The same as \resetcounteronoverlays, except that this command should be used with counts that have been created using the TeX primitive \newcount instead of LaTeX’s \definecounter. 

_Example:_
    
    
    \newcount\mycount
    \resetcountonoverlays{mycount}
    

######  9.6.2 Mode Specifications¶

This section is only important if you use beamer’s mode mechanism to create different versions of your presentation. If you are not familiar with beamer’s modes, please skip this section or read Section [21](<Creating-Handouts-Lecture-Notes.html#section-modes>) first. 

In certain cases you may wish to have different overlay specifications to apply to a command in different modes. For example, you might wish a certain text to appear only from the third slide on during your presentation, but in a handout for the audience there should be no third slide and the text should appear already on the second slide. In this case you could write 
    
    
    \only<3| handout:2>{Some text}
    

The vertical bar separates the two different specifications 3 and handout:2. By writing a mode name before a colon, you specify that the following specification only applies to that mode. If no mode is given, as in 3, the mode beamer is automatically added. For this reason, if you write \only<3>{Text} and you are in handout mode, the text will be shown on all slides since there is no restriction specified for handouts and since the 3 is the same as beamer:3. 

It is also possible to give an overlay specification that contains only a mode name (or several, separated by vertical bars): 
    
    
    \only<article>{This text is shown only in article mode.}
    

An overlay specification that does not contain any slide numbers is called a (pure) _mode specification_. If a mode specification is given, all modes that are not mentioned are automatically suppressed. Thus <beamer:1-> means “on all slides in beamer mode and also on all slides in all other modes, since nothing special is specified for them,” whereas <beamer> means “on all slides in beamer mode and not on any other slide.” 

Mode specifications can also be used outside frames as in the following examples: 
    
    
    \section<presentation>{This section exists only in the presentation modes}
    \section<article>{This section exists only in the article mode}
    

Presentation modes include beamer, trans and handout. 

You can also mix pure mode specifications and overlay specifications, although this can get confusing: 
    
    
    \only<article| beamer:1>{Riddle}
    

This will cause the text Riddle to be inserted in article mode and on the first slide of a frame in beamer mode, but not at all in handout or trans mode. (Try to find out how <beamer| beamer:1> differs from <beamer> and from <beamer:1>.) 

As if all this were not already complicated enough, there is another mode that behaves in a special way: the mode second. For this mode a special rule applies: An overlay specification for mode beamer also applies to mode second (but not the other way round). Thus, if we are in mode second, the specification <second:2> means “on slide 2” and <beamer:2> also means “on slide 2”. To get a slide that is typeset in beamer mode, but not in second mode, you can use, <second:0>. 

######  9.6.3 Action Specifications¶

This section also introduces a rather advanced concept. You may also wish to skip it on first reading. 

Some overlay specification-aware commands can handle not only normal overlay specifications, but also so called _action specifications_. In an action specification, the list of slide numbers and ranges is prefixed by ⟨ _action_ ⟩@, where ⟨ _action_ ⟩ is the name of a certain action to be taken on the specified slides: 
    
    
    \item<3-| alert@3> Shown from slide 3 on, alerted on slide 3.
    

In the above example, the \item command, which allows actions to be specified, will uncover the item text from slide three on and it will, additionally, alert this item exactly on slide 3. 

Not all commands can take an action specification. Currently, only \item (though not in article mode currently), \action, the environment actionenv, and the block environments (like block or theorem) handle them. 

By default, the following actions are available:

  * • alert alters the item or block. 

  * • uncover uncovers the item or block (this is the default, if no action is specified). 

  * • only causes the whole item or block to be inserted only on the specified slides. 

  * • visible causes the text to become visible only on the specified slides (the difference between uncover and visible is the same as between \uncover and \visible). 

  * • invisible causes the text to become invisible on the specified slides. 




The rest of this section explains how you can add your own actions and make commands action-specification-aware. You may wish to skip it upon first reading. 

You can easily add your own actions: An action specification like ⟨ _action_ ⟩@⟨ _slide numbers_ ⟩ simply inserts an environment called ⟨ _action_ ⟩env around the \item or parameter of \action with <⟨ _slide numbers_ ⟩> as overlay specification. Thus, by defining a new overlay specification-aware environment named ⟨ _my action name_ ⟩env, you can add your own action: 
    
    
    \newenvironment{checkenv}{\only{\setbeamertemplate{itemize item}{X}}}{}
    

You can then write
    
    
    \item<beamer:check@2> Text.
    

This will change the itemization symbol before Text. to X on slide 2 in beamer mode. The definition of checkenv used the fact that \only also accepts an overlay specification given after its argument. 

The whole action mechanism is based on the following environment: 

\begin{actionenv}<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{actionenv}

This environment extracts all actions from the ⟨ _action specification_ ⟩ for the current mode. For each action of the form ⟨ _action_ ⟩@⟨ _slide numbers_ ⟩, it inserts the following text: \begin{⟨ _action_ ⟩env}<⟨ _slide number_ ⟩> at the beginning of the environment and the text \end{⟨ _action_ ⟩env} at the end. If there are several action specifications, several environments are opened (and closed in the appropriate order). An ⟨ _overlay specification_ ⟩ without an action is promoted to uncover@⟨ _overlay specification_ ⟩. 

If the so called _default overlay specification_ is not empty, it will be used in case no ⟨ _action specification_ ⟩ is given. The default overlay specification is usually just empty, but it may be set either by providing an additional optional argument to the command \frame or to the environments itemize, enumerate, or description (see these for details). Also, the default action specification can be set using the command \beamerdefaultoverlayspecification, see below. 

_Example:_
    
    
    \begin{frame}
      \begin{actionenv}<2-| alert@3-4,6>
        This text is shown the same way as the text below.
      \end{actionenv}
    
      \begin{uncoverenv}<2->
        \begin{alertenv}<3-4,6>
          This text is shown the same way as the text above.
        \end{alertenv}
      \end{uncoverenv}
    \end{frame}
    

`\action`<⟨ _action specification_ ⟩>{⟨ _text_ ⟩} 

This has the same effect as putting ⟨ _text_ ⟩ in an actionenv. 

_Example:_ \action{Could also have used \texttt{\string\alert<2>\char‘\\{\char‘\\}}.}

`\beamerdefaultoverlayspecification`{⟨ _default overlay specification_ ⟩} 

Locally sets the default overlay specification to the given value. This overlay specification will be used in every actionenv environment and every \item that does not have its own overlay specification. The main use of this command is to install an incremental overlay specification like <+-> or <+-| alert@+>, see Section [9.6.4](<Creating-Overlays.html#section-incremental>). 

Usually, the default overlay specification is installed automatically by the optional arguments to \frame, frame, itemize, enumerate, and description. You will only have to use this command if you wish to do funny things. 

If given outside any frame, this command sets the default overlay specification for all following frames for which you do not override the default overlay specification. 

_Example:_ \beamerdefaultoverlayspecification{<+->}

_Example:_ \beamerdefaultoverlayspecification{} clears the default overlay specification. (Actually, it installs the default overlay specification <*>, which just means “always,” but the “portable” way of clearing the default overlay specification is this call.) 

######  9.6.4 Incremental Specifications¶

This section is mostly important for people who have already used overlay specifications a lot and have grown tired of writing things like <1->, <2->, <3->, and so on again and again. You should skip this section on first reading. 

Often you want to have overlay specifications that follow a pattern similar to the following: 
    
    
    \begin{itemize}
    \item<1-> Apple
    \item<2-> Peach
    \item<3-> Plum
    \item<4-> Orange
    \end{itemize}
    

The problem starts if you decide to insert a new fruit, say, at the beginning. In this case, you would have to adjust all of the overlay specifications. Also, if you add a \pause command before the itemize, you would also have to update the overlay specifications. 

beamer offers a special syntax to make creating lists as the one above more “robust.” You can replace it by the following list of _incremental overlay specifications_ : 
    
    
    \begin{itemize}
    \item<+-> Apple
    \item<+-> Peach
    \item<+-> Plum
    \item<+-> Orange
    \end{itemize}
    

The effect of the +-sign is the following: You can use it in any overlay specification at any point where you would usually use a number. If a +-sign is encountered, it is replaced by the current value of the LaTeX counter beamerpauses, which is 1 at the beginning of the frame. Then the counter is increased by 1, though it is only increased once for every overlay specification, even if the specification contains multiple +-signs (they are replaced by the same number). 

In the above example, the first specification is replaced by <1->. Then the second is replaced by <2-> and so forth. We can now easily insert new entries, without having to change anything else. We might also write the following: 
    
    
    \begin{itemize}
    \item<+-| alert@+> Apple
    \item<+-| alert@+> Peach
    \item<+-| alert@+> Plum
    \item<+-| alert@+> Orange
    \end{itemize}
    

This will alert the current item when it is uncovered. For example, the first specification <+-| alert@+> is replaced by <1-| alert@1>, the second is replaced by <2-| alert@2>, and so on. Since the itemize environment also allows you to specify a default overlay specification, see the documentation of that environment, the above example can be written even more economically as follows: 
    
    
    \begin{itemize}[<+-| alert@+>]
    \item Apple
    \item Peach
    \item Plum
    \item Orange
    \end{itemize}
    

The \pause command also updates the counter beamerpauses. You can change this counter yourself using the normal LaTeX commands \setcounter or \addtocounter. 

Any occurrence of a +-sign may be followed by an _offset_ in round brackets. This offset will be added to the value of beamerpauses. Thus, if beamerpauses is 2, then <+(1)-> expands to <3-> and <+(-1)-+> expands to <1-2>. For example 
    
    
    \begin{frame}
    \frametitle{Method 1}
    \begin{itemize}
    \item<2-> Apple
    \item<3-> Peach
    \item<4-> Plum
    \item<5-> Orange
    \end{itemize}
    

and
    
    
    \begin{itemize}[<+(1)->]
    \item Apple
    \item Peach
    \item Plum
    \item Orange
    \end{itemize}
    

are equivalent.

There is another special sign you can use in an overlay specification that behaves similarly to the +-sign: a dot. When you write <.->, a similar thing as in <+-> happens _except_ that the counter beamerpauses is _not_ incremented and _except_ that you get the value of beamerpauses decreased by one. Thus a dot, possibly followed by an offset, just expands to the current value of the counter beamerpauses minus one, possibly offset. This dot notation can be useful in case like the following: 
    
    
    \begin{itemize}[<+->]
    \item Apple
    \item<.-> Peach
    \item Plum
    \item Orange
    \end{itemize}
    

In the example, the second item is shown at the same time as the first one since it does not update the counter. 

In the following example, each time an item is uncovered, the specified text is alerted. When the next item is uncovered, this altering ends. 
    
    
    \begin{itemize}[<+->]
    \item This is \alert<.>{important}.
    \item We want to \alert<.>{highlight} this and \alert<.>{this}.
    \item What is the \alert<.>{matrix}?
    \end{itemize}
    

The expansions of the +-sign and the .-sign are no less than zero. This prevents errors when encountering large negative offsets, for example <+(-7)-> is expanded to <0-> rather than <-6->. 
