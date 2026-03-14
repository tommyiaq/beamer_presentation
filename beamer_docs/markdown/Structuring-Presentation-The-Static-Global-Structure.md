## Building a Presentation

####  10 Structuring a Presentation: The Static Global Structure 

This section lists the commands that are used for structuring a presentation “globally” using commands like \section or \part. These commands are used to create a _static_ structure, meaning that the resulting presentation is normally presented one slide after the other in the order the slides occur. Section [11](<Structuring-Presentation-The-Interactive-Global-Structure.html#section-nonlinear>) explains which commands can be used to create the _interactive_ structure. For the interactive structure, you must interact with the presentation program, typically by clicking on hyperlinks, to advance the presentation. 

#####  10.1 Adding a Title Page¶

You can use the \titlepage command to insert a title page into a frame. By default, it will arrange the following elements on the title page: the document title, the authors’ names, their affiliation, a title graphic, and a date. 

`\titlepage`

Inserts the text of a title page into the current frame.

_Example:_ \begin{frame}\titlepage\end{frame}

_Example:_ \begin{frame}[plain]\titlepage\end{frame} for a titlepage that fills the whole frame. 

**Beamer-Template/-Color/-Font** title page

This template is invoked when the \titlepage command is used. 

The following template options are predefined:

  * • `[default]`[⟨ _alignment_ ⟩] The title page is typeset showing the title, followed by the author, their affiliation, the date, and a titlegraphic. If any of these are missing, they are not shown. Except for the titlegraphic, if the beamer-color title, author, institute, or date is defined, respectively, it is used as textcolor for these entries. If a background color is defined for them, a colored bar in the corresponding color is drawn behind them, spanning the text width. The corresponding beamer-fonts are used for these entries. The following templates are used by the title page: 

**Beamer-Template/-Color/-Font** title

**Beamer-Template/-Color/-Font** author

**Beamer-Template/-Color/-Font** institute

**Beamer-Template/-Color/-Font** date

**Beamer-Template** titlegraphic

The ⟨ _alignment_ ⟩ option is passed on the beamercolorbox and can be used, for example, to flush the title page to the left by specifying left here. 




The following commands are useful for this template:

  * • `\insertauthor` inserts a version of the author’s name that is useful for the title page. 

  * • `\insertdate` inserts the date. 

  * • `\insertinstitute` inserts the institute. 

  * • `\inserttitle` inserts a version of the document title that is useful for the title page. 

  * • `\insertsubtitle` inserts a version of the document title that is useful for the title page. 

  * • `\inserttitlegraphic` inserts the title graphic into a template. 




For compatibility with other classes, in article mode the following command is also provided: 

`\maketitle`

presentation

If used inside a frame, it has the same effect as \titlepage. If used outside a frame, it has the same effect as \begin{frame}\titlepage\end{frame}; in other words, a frame is added if necessary. 

Before you invoke the title page command, you must specify all elements you wish to be shown. This is done using the following commands: 

`\title`[⟨ _short title_ ⟩]{⟨ _title_ ⟩} 

The ⟨ _short title_ ⟩ is used in headlines and footlines. Inside the ⟨ _title_ ⟩ line breaks can be inserted using the double-backslash command. 

_Example:_
    
    
    \title{The Beamer Class}
    \title[Short Version]{A Very Long Title\\Over Several Lines}
    

article

The short form is ignored in article mode. 

`\subtitle`[⟨ _short subtitle_ ⟩]{⟨ _subtitle_ ⟩} 

The ⟨ _short subtitle_ ⟩ is not used by default, but is available via the insert \insertshortsubtitle. The subtitle is shown below the title in a smaller font. 

_Example:_
    
    
    \title{The Beamer Class}
    \subtitle{An easily paced introduction with many examples.}
    

article

This command causes the subtitle to be appended to the title with a linebreak and a \normalsize command issued before it. This may or may not be what you would like to happen. 

`\author`[⟨ _short author names_ ⟩]{⟨ _author names_ ⟩} 

The names should be separated using the command \and. In case authors have different affiliations, they should be suffixed by the command \inst with different parameters. 

_Example:_ \author[Hemaspaandra et al.]{L. Hemaspaandra\inst{1} \and T. Tantau\inst{2}}

article

The short form is ignored in article mode. 

`\institute`[⟨ _short institute_ ⟩]{⟨ _institute_ ⟩} 

If more than one institute is given, they should be separated using the command \and and they should be prefixed by the command \inst with different parameters. 

_Example:_
    
    
    \institute[Universities of Rijeka and Berlin]{
      \inst{1}Department of Informatics\\
      University of Rijeka
      \and
      \inst{2}Fakult\"at f\"ur Elektrotechnik und Informatik\\
      Technical University of Berlin}
    

article

The short form is ignored in article mode. The long form is also ignored, except if the document class (like llncs) defines it. 

`\date`[⟨ _short date_ ⟩]{⟨ _date_ ⟩} 

_Example:_ \date{\today} or \date[STACS 2003]{STACS Conference, 2003}. 

article

The short form is ignored in article mode. 

`\titlegraphic`{⟨ _text_ ⟩} 

The ⟨ _text_ ⟩ is shown as title graphic. Typically, a picture environment is used as ⟨ _text_ ⟩. 

_Example:_ \titlegraphic{\pgfuseimage{titlegraphic}}

article

The command is ignored in article mode. 

`\subject`{⟨ _text_ ⟩} 

Enters the ⟨ _text_ ⟩ as the subject text in the pdf document info. It currently has no other effect. 

`\keywords`{⟨ _text_ ⟩} 

Enters the ⟨ _text_ ⟩ as keywords in the pdf document info. It currently has no other effect. 

By default, the \title and \author commands will also insert their arguments into a resulting pdf-file in the document information fields. This may cause problems if you use complicated things like boxes as arguments to these commands. In this case, you might wish to switch off the automatic generation of these entries using the following class option: 

\documentclass[usepdftitle=false]{beamer} 

Suppresses the automatic generation of title and author entries in the pdf document information. 

#####  10.2 Adding Sections and Subsections¶

You can structure your text using the commands \section and \subsection. Unlike standard LaTeX, these commands will not create a heading at the position where you use them. Rather, they will add an entry to the table of contents and also to the navigation bars. 

In order to create a line break in the table of contents (usually not a good idea), you can use the command \breakhere. Note that the standard command \\\ is modified so that it’s no longer robust (see Section 9.3; using \protect\\\ or \newline will also be fine). 

`\section`<⟨ _mode specification_ ⟩>[⟨ _short section name_ ⟩]{⟨ _section name_ ⟩} 

Starts a section. No heading is created. By default the ⟨ _section name_ ⟩ is shown in the table of contents and in the navigation bars; if ⟨ _short section name_ ⟩ is specified, it will be used in the navigation bars instead; if ⟨ _short section name_ ⟩ is explicitly empty, it will not appear in the navigation bars. If a ⟨ _mode specification_ ⟩ is given, the command only has an effect for the specified modes. 

_Example:_ \section[Summary]{Summary of Main Results}

article

The ⟨ _mode specification_ ⟩ allows you to provide an alternate section command in article mode. This is necessary for example if the ⟨ _short section name_ ⟩ is unsuitable for the table of contents: 

_Example:_
    
    
    \section<presentation>[Results]{Results on the Main Problem}
    \section<article>{Results on the Main Problem}
    

**Beamer-Template/-Color/-Font** section in toc

This template is used when a section entry is to be typeset. For the permissible ⟨ _options_ ⟩ see the parent template table of contents. 

The following commands are useful for this template:

  * • `\inserttocsection` inserts the table of contents version of the current section name. 

  * • `\inserttocsectionnumber` inserts the number of the current section (in the table of contents). 




**Beamer-Template/-Color/-Font** section in toc shaded

This template is used instead of the previous one if the section should be shown in a shaded way, because it is not the current section. For the permissible ⟨ _options_ ⟩ see the parent template table of contents. 

`\section`<⟨ _mode specification_ ⟩>*{⟨ _section name_ ⟩} 

Starts a section without an entry in the table of contents. No heading is created, but the ⟨ _section name_ ⟩ is shown in the navigation bar. 

_Example:_ \section*{Outline}

_Example:_ \section<beamer>*{Outline}

`\subsection`<⟨ _mode specification_ ⟩>[⟨ _short subsection name_ ⟩]{⟨ _subsection name_ ⟩} 

This command works the same way as the \section command. 

_Example:_ \subsection[Applications]{Applications to the Reduction of Pollution}

**Beamer-Template/-Color/-Font** subsection in toc

Like section in toc, only for subsection. 

In addition to the inserts for the section in toc template, the following commands are available for this template: 

  * • `\inserttocsubsection` inserts the table of contents version of the current subsection name. 

  * • `\inserttocsubsectionnumber` inserts the number of the current subsection (in the table of contents). 




**Beamer-Template/-Color/-Font** subsection in toc shaded

Like section in toc shaded, only for subsections. 

`\subsection`<⟨ _mode specification_ ⟩>*{⟨ _subsection name_ ⟩} 

Starts a subsection without an entry in the table of contents. No heading is created, but the ⟨ _subsection name_ ⟩ is shown in the navigation bar, _except_ if ⟨ _subsection name_ ⟩ is empty. In this case, neither a table of contents entry nor a navigation bar entry is created, _but_ any frames in this “empty” subsection are shown in the navigation bar. 

_Example:_
    
    
    \section{Summary}
    
      \begin{frame}
        This frame is not shown in the navigation bar
      \end{frame}
    
      \subsection*{}
    
      \begin{frame}
        This frame is shown in the navigation bar, but no subsection entry is shown.
      \end{frame}
    
      \subsection*{A subsection}
    
      \begin{frame}
        Normal frame, shown in navigation bar. The subsection name is
        also shown in the navigation bar, but not in the table of contents.
      \end{frame}
    

`\subsubsection`<⟨ _mode specification_ ⟩>[⟨ _short subsubsection name_ ⟩]{⟨ _subsubsection name_ ⟩} 

This command works the like \subsection. However, subsubsections are supported less well than subsections. For example, in the table of contents subsubsections are always shown with the same shading/hiding parameters as the subsection. 

We _strongly_ discourage the use of subsubsections in presentations. If you do not use them, you will give a better presentation. 

_Example:_ \subsubsection[Applications]{Applications to the Reduction of Pollution}

**Beamer-Template/-Color/-Font** subsubsection in toc

Like subsection in toc, only for subsection. 

In addition to the inserts for the subsection in toc template, the following commands are available for this template: 

  * • `\inserttocsubsubsection` inserts the table of contents version of the current subsubsection name. 

  * • `\inserttocsubsubsectionnumber` inserts the number of the current subsubsection (in the table of contents). 




**Beamer-Template/-Color/-Font** subsubsection in toc shaded

Like subsection in toc shaded, only for subsubsections. 

`\subsubsection`<⟨ _mode specification_ ⟩>*{⟨ _subsubsection name_ ⟩} 

Starts a subsubsection without an entry in the table of contents. No heading is created, but the ⟨ _subsubsection name_ ⟩ is shown in a possible sidebar. 

Often, you may want a certain type of frame to be shown directly after a section or subsection starts. For example, you may wish every subsection to start with a frame showing the table of contents with the current subsection highlighted. To facilitate this, you can use the following commands. 

`\AtBeginSection`[⟨ _special star text_ ⟩]{⟨ _text_ ⟩} 

The given text will be inserted at the beginning of every section. If the ⟨ _special star text_ ⟩ parameter is specified, this text will be used for starred sections instead. Different calls of this command will not “add up” the given texts (like the \AtBeginDocument command does), but will overwrite any previous text. 

_Example:_
    
    
    \AtBeginSection[] % Do nothing for \section*
    {
     \begin{frame}<beamer>
       \frametitle{Outline}
       \tableofcontents[currentsection]
     \end{frame}
    }
    

article

This command has no effect in article mode. 

`\AtBeginSubsection`[⟨ _special star text_ ⟩]{⟨ _text_ ⟩} 

The given text will be inserted at the beginning of every subsection. If the ⟨ _special star text_ ⟩ parameter is specified, this text will be used for starred subsections instead. Different calls of this command will not “add up” the given texts. 

_Example:_
    
    
    \AtBeginSubsection[] % Do nothing for \subsection*
    {
     \begin{frame}<beamer>
       \frametitle{Outline}
       \tableofcontents[currentsection,currentsubsection]
     \end{frame}
    }
    

`\AtBeginSubsubsection`[⟨ _special star text_ ⟩]{⟨ _text_ ⟩} 

Like \AtBeginSubsection, only for subsubsections. 

beamer also provides \sectionpage and \subsectionpage commands, which are used to fill a frame with section or subsection number and title in a stylish way. They are very similar to \partpage command described below. 

`\sectionpage`

This command shows a frame with the section number and title of the current section. 

_Example:_
    
    
    \section{A section}
    
      \begin{frame}
        \sectionpage
      \end{frame}
    
      \begin{frame}
        Some text.
      \end{frame}
    

**Beamer-Template** section page

This template is invoked when the \sectionpage command is used. 

The following template options are predefined:

  * • `[default]`[⟨ _alignment_ ⟩] The section page is typeset showing the current section number and, below, the current section title. The templates 

**Beamer-Color/-Font** section name

and

**Beamer-Color/-Font** section title

are used, including the background color of section title. As for the title page template, the ⟨ _alignment_ ⟩ option is passed on the beamercolorbox. 




The following commands are useful for this template:

  * • `\insertsection` inserts the title of the current section. 

  * • `\insertsectionnumber` inserts the current section number. 




`\subsectionpage`

Works the same way as the \sectionpage. 

**Beamer-Template** subsection page

The following template options are predefined:

  * • `[default]`[⟨ _alignment_ ⟩]

The templates

**Beamer-Color/-Font** subsection name

and

**Beamer-Color/-Font** subsection title

are used, including the background color of subsection title. As for the title page template, the ⟨ _alignment_ ⟩ option is passed on the beamercolorbox. 




The following commands are useful for this template:

  * • `\insertsubsection` inserts the title of the current subsection. 

  * • `\insertsubsectionnumber` inserts the current subsection number. 




#####  10.3 Adding Parts¶

If you give a long talk (like a lecture), you may wish to break up your talk into several parts. Each such part acts like a little “talk of its own” with its own table of contents, its own navigation bars, and so on. Inside one part, the sections and subsections of the other parts are not shown at all. 

To create a new part, use the \part command. All sections and subsections following this command will be “local” to that part. Like the \section and \subsection command, the \part command does not cause any frame or special text to be produced. However, it is often advisable for the start of a new part to use the command \partpage to insert some text into a frame that “advertises” the beginning of a new part. 

`\part`<⟨ _mode specification_ ⟩>[⟨ _short part name_ ⟩]{⟨ _part name_ ⟩} 

Starts a part. The ⟨ _part name_ ⟩ will be shown when the \partpage command is used. The ⟨ _short part name_ ⟩ is not shown anywhere by default, but it is accessible via the command \insertshortpart. 

_Example:_
    
    
    \begin{document}
      \begin{frame}
      \titlepage
      \end{frame}
    
      \section*{Outlines}
      \subsection{Part I: Review of Previous Lecture}
      \begin{frame}
        \frametitle{Outline of Part I}
        \tableofcontents[part=1]
      \end{frame}
      \subsection{Part II: Today's Lecture}
      \begin{frame}
        \frametitle{Outline of Part II}
        \tableofcontents[part=2]
      \end{frame}
    
      \part{Review of Previous Lecture}
      \begin{frame}
        \partpage
      \end{frame}
      \section[Previous Lecture]{Summary of the Previous Lecture}
      \subsection{Topics}
      \begin{frame}...\end{frame}
      \subsection{Learning Objectives}
      \begin{frame}...\end{frame}
    
      \part{Today's Lecture}
      \begin{frame}
        \partpage
      \end{frame}
      \section{Topic A}
      \begin{frame}
        \tableofcontents[currentsection]
      \end{frame}
      \subsection{Foo}
      \begin{frame}...\end{frame}
      \section{Topic B}
      \begin{frame}
        \tableofcontents[currentsection]
      \end{frame}
      \subsection{bar}
      \begin{frame}...\end{frame}
    \end{document}
    

`\partpage`

Works like \titlepage, only that the current part, not the current presentation is “advertised.” 

_Example:_ \begin{frame}\partpage\end{frame}

**Beamer-Template** part page

This template is invoked when the \partpage command is used. 

The following template options are predefined:

  * • `[default]`[⟨ _alignment_ ⟩] The part page is typeset showing the current part number and, below, the current part title. The templates 

**Beamer-Color/-Font** part name

and

**Beamer-Color/-Font** part title

are used, including the background color of part title. As for the title page template, the ⟨ _alignment_ ⟩ option is passed on the beamercolorbox. 




The following commands are useful for this template:

  * • `\insertpart` inserts the current part name. 

  * • `\insertpartnumber` inserts the current part number as an Arabic number into a template. 

  * • `\insertromanpartnumber` inserts the current part number as a Roman number into a template. 




`\AtBeginPart`{⟨ _text_ ⟩} 

The given text will be inserted at the beginning of every part. 

_Example:_
    
    
    \AtBeginPart{
      \begin{frame}
        \partpage
      \end{frame}
    }
    

#####  10.4 Splitting a Course Into Lectures¶

When using beamer with the article mode, you may wish to have the lecture notes of a whole course reside in one file. In this case, only a few frames are actually part of any particular lecture. 

The \lecture command makes it easy to select only a certain set of frames from a file to be presented. This command takes (among other things) a label name. If you say \includeonlylecture with this label name, then only the frames following the corresponding \lecture command are shown. The frames following other \lecture commands are suppressed. 

By default, the \lecture command has no other effect. It does not create any frames or introduce entries in the table of contents. However, you can use \AtBeginLecture to have beamer insert, say, a title page at the beginning of (each) lecture. 

`\lecture`[⟨ _short lecture name_ ⟩]{⟨ _lecture name_ ⟩}{⟨ _lecture label_ ⟩} 

Starts a lecture. The ⟨ _lecture name_ ⟩ will be available via the \insertlecture command. The ⟨ _short lecture name_ ⟩ is available via the \insertshortlecture command. 

_Example:_
    
    
    \begin{document}
    \lecture{Vector Spaces}{week 1}
    
    \section{Introduction}
    ...
    \section{Summary}
    
    \lecture{Scalar Products}{week 2}
    
    \section{Introduction}
    ...
    \section{Summary}
    
    \end{document}
    

article

This command has no effect in article mode. 

`\includeonlylecture`⟨ _lecture label_ ⟩

Causes all \frame, frame, \section, \subsection, and \part commands following a \lecture command to be suppressed, except if the lecture’s label matches the ⟨ _lecture label_ ⟩. Frames before any \lecture commands are always included. This command should be given in the preamble. 

_Example:_ \includeonlylecture{week 1}

article

This command has no effect in article mode. 

`\AtBeginLecture`{⟨ _text_ ⟩} 

The given text will be inserted at the beginning of every lecture. 

_Example:_
    
    
    \AtBeginLecture{
      \begin{frame}
        \Large Today's Lecture: \insertlecture
      \end{frame}
    }
    

article

This command has no effect in article mode. 

#####  10.5 Adding a Table of Contents¶

You can create a table of contents using the command \tableofcontents. Unlike the normal LaTeX table of contents command, this command takes an optional parameter in square brackets that can be used to create certain special effects. 

`\tableofcontents`[⟨ _comma-separated option list_ ⟩]

Inserts a table of contents into the current frame.

_Example:_
    
    
    \section*{Outline}
    \begin{frame}
      \tableofcontents
    \end{frame}
    
    \section{Introduction}
    \begin{frame}
      \tableofcontents[currentsection]
    \end{frame}
    \subsection{Why?}
    \begin{frame}...\end{frame}
    \begin{frame}...\end{frame}
    \subsection{Where?}
    \begin{frame}...\end{frame}
    
    \section{Results}
    \begin{frame}
      \tableofcontents[currentsection]
    \end{frame}
    \subsection{Because}
    \begin{frame}...\end{frame}
    \subsection{Here}
    \begin{frame}...\end{frame}
    

The following options can be given:

  * • currentsection causes all sections but the current to be shown in a semi-transparent way. Also, all subsections but those in the current section are shown in the semi-transparent way. This command is a shorthand for specifying the following options: 
        
        sectionstyle=show/shaded,subsectionstyle=show/show/shaded
        

  * • currentsubsection causes all subsections but the current subsection in the current section to be shown in a semi-transparent way. This command is a shorthand for specifying the option subsectionstyle=show/shaded. 

  * • firstsection=⟨ _section number_ ⟩ specifies which section should be numbered as section “1.” This is useful if you have a first section (like an overview section) that should not receive a number. Section numbers are not shown by default. To show them, you must install a different table of contents templates. 

  * • hideallsubsections causes all subsections to be hidden. This command is a shorthand for specifying the option subsectionstyle=hide. 

  * • hideothersubsections causes the subsections of sections other than the current one to be hidden. This command is a shorthand for specifying the option subsectionstyle=show/show/hide. 

  * • lastsection=⟨ _section number_ ⟩ similar to firstsection, this option specifies which section should be the last numbered section. This is useful if you have unnumbered sections at the end, like a summary or outlook. Section numbers are not shown by default. To show them, you must install a different table of contents templates. 

  * • part=⟨ _part number_ ⟩ causes the table of contents of part ⟨ _part number_ ⟩ to be shown, instead of the table of contents of the current part (which is the default). This option can be combined with the other options, although combining it with the current option obviously makes no sense. 

  * • pausesections causes a \pause command to be issued before each section. This is useful if you wish to show the table of contents in an incremental way. 

  * • pausesubsections causes a \pause command to be issued before each subsection. 

  * • sections={⟨ _overlay specification_ ⟩} causes only the sections mentioned in the ⟨ _overlay specification_ ⟩ to be shown. For example, sections={<2-4| handout:0>} causes only the second, third, and fourth section to be shown in the normal version, nothing to be shown in the handout version, and everything to be shown in all other versions. For convenience, if you omit the pointed brackets, the specification is assumed to apply to all versions. Thus sections={2-4} causes sections two, three, and four to be shown in all versions. 

  * • sectionstyle=⟨ _style for current section_ ⟩/⟨ _style for other sections_ ⟩ specifies how sections should be displayed. Allowed ⟨ _styles_ ⟩ are show, shaded, and hide. The first will show the section title normally, the second will show it in a semi-transparent way, and the third will completely suppress it. You can also omit the second style, in which case the first is used for all sections (this is not really useful). 

  * • subsectionstyle=⟨ _style for current subsection_ ⟩/⟨ _style for other subsections in current section_ ⟩/  
⟨ _style for subsections in other sections_ ⟩ specifies how subsections should be displayed. The same styles as for the sectionstyle option may be given. You can omit the last style, in which case the second also applies to the last, and you can omit the last two, in which case the first applies to all. 

_Example:_ subsectionstyle=shaded causes all subsections to be shaded. 

_Example:_ subsectionstyle=hide causes all subsections to be hidden. 

_Example:_ subsectionstyle=show/shaded causes all subsections but the current subsection in the current section to be shown in a semi-transparent way. 

_Example:_ subsectionstyle=show/show/hide causes all subsections outside the current section to be suppressed. 

_Example:_ subsectionstyle=show/shaded/hide causes all subsections outside the current section to be suppressed and only the current subsection in the current section to be highlighted. 

  * • subsubsectionstyle=⟨ _style for current subsubsection_ ⟩/⟨ _style for other subsubsections in current subsection_ ⟩/  
⟨ _style for subsubsections in other subsections in current section_ ⟩/⟨ _style for subsubsections in other subsections in other sections_ ⟩ specifies how subsubsections should be displayed. The same styles as for the sectionstyle option may be given. You can omit styles from the end of the list, in which case the last given style will also be applied to the omitted styles. This option operates in an analogous manner to subsectionstyle. 




The last examples are useful if you do not wish to show too many details when presenting the talk outline. 

article

The options are ignored in article mode. 

**Parent Beamer-Template** sections/subsections in toc

This is a parent template, whose children are section in toc and subsection in toc. This means that if you use the \setbeamertemplate command on this template, the command is instead called for both of these children (with the same arguments). 

The following template options are predefined:

  * • `[default]` In the default setting, the sections and subsections are typeset using the fonts and colors section in toc and subsection in toc, though the background colors are ignored. The subsections are indented. 

  * • `[sections numbered]` Similar to the default setting, but the section numbers are also shown. The subsections are not numbered. 

  * • `[subsections numbered]` This time, the subsections are numbered, but not the sections. Nevertheless, since the subsections are “fully numbered” as in “1.2” or “3.2,” if every section has at least one subsection, the section numbered will not really be missed. 

  * • `[circle]` Draws little circles before the sections. Inside the circles the section number is shown. The beamer-font and color section number projected is used for typesetting the circles, that is, the circle gets the background color and the text inside the circle the foreground color. 

  * • `[square]` Similar to the circle option, except that small squares are used instead of circles. Small, unnumbered squares are shown in front of the subsections. 

  * • `[ball]` Like square, the only difference being the balls are used instead of squares. 

  * • `[ball unnumbered]` Similar to ball, except that no numbering is used. This option makes the table of contents look more like an itemize. 




If none of the above options suits you, you have to change the templates section in toc and subsection in toc directly. 

**Parent Beamer-Template** sections/subsections in toc shaded

A parent template with children section in toc shaded and subsection in toc shaded. They are used to render section and subsection entries when they are currently shaded; like all non-current subsections in \tableofcontents[currentsubsection]. 

The following template options are predefined:

  * • `[default]`[⟨ _opaqueness_ ⟩] In the default setting, the templates section in toc shaded and subsection in toc shaded just show whatever the nonshaded versions of these templates show, but only ⟨ _opaqueness_ ⟩% opaque. The default is 20%. 

_Example:_ \setbeamertemplate{section in toc shaded}[default][50] makes dimmed entries 50% transparent. 




#####  10.6 Adding a Bibliography¶

You can use the bibliography environment and the \cite commands of LaTeX in a beamer presentation. You will typically have to typeset your bibliography items partly “by hand.” Nevertheless, you _can_ use bibtex to create a “first approximation” of the bibliography. Copy the content of the file main.bbl into your presentation. If you are not familiar with bibtex, you may wish to consult its documentation. It is a powerful tool for creating high-quality citations. 

Using bibtex or your editor, place your bibliographic references in the environment thebibliography. This (standard LaTeX) environment takes one parameter, which should be the longest \bibitem label in the following list of bibliographic entries. 

\begin{thebibliography}{⟨ _longest label text_ ⟩} 

⟨ _environment contents_ ⟩

\end{thebibliography}

Inserts a bibliography into the current frame. The ⟨ _longest label text_ ⟩ is used to determine the indentation of the list. However, several predefined options for the typesetting of the bibliography ignore this parameter since they replace the references by a symbol. 

Inside the environment, use a (standard LaTeX) \bibitem command for each reference item. Inside each item, use a (standard LaTeX) \newblock command to separate the authors’ names, the title, the book/journal reference, and any notes. Each of these commands may introduce a new line or color or other formatting, as specified by the template for bibliographies. 

The environment must be placed inside a frame. If the bibliography does not fit on one frame, you should split it (create a new frame and a second thebibliography environment) or use the allowframebreaks option. Even better, you should reconsider whether it is a good idea to present so many references. 

_Example:_
    
    
    \begin{frame}
      \frametitle{For Further Reading}
    
      \begin{thebibliography}{Dijkstra, 1982}
      \bibitem[Salomaa, 1973]{Salomaa1973}
        A.~Salomaa.
        \newblock {\em Formal Languages}.
        \newblock Academic Press, 1973.
    
      \bibitem[Dijkstra, 1982]{Dijkstra1982}
        E.~Dijkstra.
        \newblock Smoothsort, an alternative for sorting in situ.
        \newblock {\em Science of Computer Programming}, 1(3):223--233, 1982.
      \end{thebibliography}
    \end{frame}
    

Four templates govern the appearance of the author, title, journal, and note text. These author templates are inserted before the first block of the entry (the first block is all text before the first occurrence of a \newblock command). The title template is inserted before the second block (the text between the first and second occurrence of \newblock). Likewise for the journal and note templates. 

The templates are inserted _before_ the blocks and you do not have access to the blocks themselves via insert commands. The corresponding beamer-color and -font are also installed before the blocks. 

**Beamer-Template/-Color/-Font** bibliography entry author

This template is inserted before the author of a bibliography entry. The color and font are also installed. Note that the effect of this template will persist until the end of the bibliography item or until one of the following templates undo the effect. 

By default, this template does nothing. The default color is the structure color. 

**Beamer-Template/-Color/-Font** bibliography entry title

This template is inserted before the title of a bibliography entry (more precisely, it is inserted after the first occurrence of the \newblock command). By default, this template starts a new paragraph, causing a line break. The default color is the normal text color. 

**Beamer-Template/-Color/-Font** bibliography entry location

This template is inserted before the journal of a bibliography entry (the second \newblock). By default, this template starts a new paragraph. The default color is a slightly transparent version of the structure color. 

**Beamer-Template/-Color/-Font** bibliography entry note

This template is inserted before any note text at the end of a bibliography entry (it is inserted before the third \newblock). By default, this template starts a new paragraph. The default color is the same as for the journal. 

`\bibitem`<⟨ _overlay specification_ ⟩>[⟨ _citation text_ ⟩]{⟨ _label name_ ⟩} 

The ⟨ _citation text_ ⟩ is inserted into the text when the item is cited using \cite{⟨ _label name_ ⟩} in the main presentation text. For a beamer presentation, this should usually be as long as possible. 

Use \newblock commands to separate the authors’s names, the title, the book/journal reference, and any notes. If the ⟨ _overlay specification_ ⟩ is present, the entry will only be shown on the specified slides. 

_Example:_
    
    
    \bibitem[Dijkstra, 1982]{Dijkstra1982}
      E.~Dijkstra.
      \newblock Smoothsort, an alternative for sorting in situ.
      \newblock {\em Science of Computer Programming}, 1(3):223--233, 1982.
    

**Beamer-Template/-Color/-Font** bibliography item

Color/font parents: `item`

This template is used to render the bibliography item. Unlike normal LaTeX, the default template for the bibliography does not repeat the citation text (like “[Dijkstra, 1982]”) before each item in the bibliography. Instead, a cute, small article symbol is drawn. The rationale is that the audience will not be able to remember any abbreviated citation texts till the end of the talk. 

The following template options are predefined:

  * • `[default]` Draws a cute little article icon as the reference. Use this for journal articles, parts of books (like conference proceedings), or technical reports. 

  * • `[article]` Alias for the default. 

  * • `[book]` Draws a cute little book icon as the reference. Use this for, well, books. 

  * • `[online]` Draws a cute little globe icon as the reference. Use this for websites and the like. 

  * • `[triangle]` Draws a triangle as the reference. This is more in keeping with the standard itemize items. 

  * • `[text]` Uses the reference text (like “[Dijkstra, 1982]”) as the reference text. Be sure you know what you are doing if you use this. 




The following insert is useful for the template:

  * • `\insertbiblabel` inserts the current citation label. 




#####  10.7 Adding an Appendix¶

You can add an appendix to your talk by using the \appendix command. You should put frames and perhaps whole subsections into the appendix that you do not intend to show during your presentation, but which might be useful to answer a question. The \appendix command essentially just starts a new part named \appendixname. However, it also sets up certain hyperlinks. Like other parts, the appendix is kept separate from your actual talk. 

`\appendix`<⟨ _mode specification_ ⟩>

Starts the appendix in the specified modes. All frames, all \subsection commands, and all \section commands used after this command will not be shown as part of the normal navigation bars. 

_Example:_
    
    
    \begin{document}
    \begin{frame}
      \titlepage
    \end{frame}
    \section*{Outline}
    \begin{frame}
      \tableofcontents
    \end{frame}
    \section{Main Text}
    \begin{frame}
      Some text
    \end{frame}
    \section*{Summary}
    \begin{frame}
      Summary text
    \end{frame}
    
    \appendix
    \section{\appendixname}
    \begin{frame}
      \tableofcontents
    \end{frame}
    \subsection{Additional material}
    \begin{frame}
      Details
    \end{frame}
    \begin{frame}
      Text omitted in main talk.
    \end{frame}
    \subsection{Even more additional material}
    \begin{frame}
      More details
    \end{frame}
    \end{document}
    
