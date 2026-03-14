## Building a Presentation

####  12 Structuring a Presentation: The Local Structure 

LaTeX provides different commands for structuring text “locally,” for example, via the itemize environment. These environments are also available in the beamer class, although their appearance has been slightly changed. Furthermore, the beamer class also defines some new commands and environments, see below, that may help you to structure your text. 

#####  12.1 Itemizations, Enumerations, and Descriptions¶

There are three predefined environments for creating lists, namely enumerate, itemize, and description. The first two can be nested to depth three, but nesting them to this depth creates totally unreadable slides. 

The \item command is overlay specification-aware. If an overlay specification is provided, the item will only be shown on the specified slides, see the following example. If the \item command is to take an optional argument and an overlay specification, the overlay specification can either come first as in \item<1>[Cat] or come last as in \item[Cat]<1>. 
    
    
    \begin{frame}
     There are three important points:
     \begin{enumerate}
     \item<1-> A first one,
     \item<2-> a second one with a bunch of subpoints,
       \begin{itemize}
       \item first subpoint. (Only shown from second slide on!).
       \item<3-> second subpoint added on third slide.
       \item<4-> third subpoint added on fourth slide.
       \end{itemize}
     \item<5-> and a third one.
     \end{enumerate}
    \end{frame}
    

\begin{itemize}[<⟨ _default overlay specification_ ⟩>]

⟨ _environment contents_ ⟩

\end{itemize}

Used to display a list of items that do not have a special ordering. Inside the environment, use an \item command for each topic. 

If the optional parameter ⟨ _default overlay specification_ ⟩ is given, in every occurrence of an \item command that does not have an overlay specification attached to it, the ⟨ _default overlay specification_ ⟩ is used. By setting this specification to be an incremental overlay specification, see Section [9.6.4](<Creating-Overlays.html#section-incremental>), you can implement, for example, a step-wise uncovering of the items. The ⟨ _default overlay specification_ ⟩ is inherited by subenvironments. Naturally, in a subenvironment you can reset it locally by setting it to <1->. 

_Example:_
    
    
    \begin{itemize}
    \item This is important.
    \item This is also important.
    \end{itemize}
    

_Example:_
    
    
    \begin{itemize}[<+->]
    \item This is shown from the first slide on.
    \item This is shown from the second slide on.
    \item This is shown from the third slide on.
    \item<1-> This is shown from the first slide on.
    \item This is shown from the fourth slide on.
    \end{itemize}
    

_Example:_
    
    
    \begin{itemize}[<+-| alert@+>]
    \item This is shown from the first slide on and alerted on the first slide.
    \item This is shown from the second slide on and alerted on the second slide.
    \item This is shown from the third slide on and alerted on the third slide.
    \end{itemize}
    

_Example:_
    
    
    \newenvironment{mystepwiseitemize}{\begin{itemize}[<+-| alert@+>]}{\end{itemize}}
    

The appearance of an itemize list is governed by several templates. The first template concerns the way the little marker introducing each item is typeset: 

**Parent Beamer-Template** itemize items

This template is a parent template, whose children are itemize item, itemize subitem, and itemize subsubitem. This means that if you use the \setbeamertemplate command on this template, the command is instead called for all of these children (with the same arguments). 

The following template options are predefined:

  * • `[default]` The default item marker is a small triangle colored with the foreground of the beamer-color itemize item (or, for subitems, itemize subitem etc.). Note that these colors will automatically change under certain circumstances such as inside an example block or inside an alertenv environment. 

  * • `[triangle]` Alias for the default. 

  * • `[circle]` Uses little circles (or dots) as item markers. 

  * • `[square]` Uses little squares as item markers. 

  * • `[ball]` Uses little balls as item markers. 




**Beamer-Template/-Color/-Font** itemize item

Color/font parents: `item`

This template (with item instead of items) governs how the marker in front of a first-level item is typeset. “First-level” refers to the level of nesting. See the itemize items template for the ⟨ _options_ ⟩ that may be given. 

When the template is inserted, the beamer-font and -color itemize item is installed. Typically, the font is ignored by the template as some special symbol is drawn anyway, by the font may be important if an optional argument is given to the \item command as in \item[First]. 

The font and color inherit from the item font and color, which are explained at the end of this section. 

**Beamer-Template/-Color/-Font** itemize subitem

Color/font parents: `subitem`

Like itemize item, only for second-level items. An item of an itemize inside an enumerate counts as a second-level item. 

**Beamer-Template/-Color/-Font** itemize subsubitem

Color/font parents: `subsubitem`

Like itemize item, only for third-level items. 

\begin{enumerate}[<⟨ _default overlay specification_ ⟩>][⟨ _mini template_ ⟩]

⟨ _environment contents_ ⟩

\end{enumerate}

Used to display a list of items that are ordered. Inside the environment, use an \item command for each topic. By default, before each item increasing Arabic numbers followed by a dot are printed (as in “1.” and “2.”). This can be changed by specifying a different template, see below. 

The first optional argument ⟨ _default overlay specification_ ⟩ has exactly the same effect as for the itemize environment. It is “detected” by the opening <-sign in the ⟨ _default overlay specification_ ⟩. Thus, if there is only one optional argument and if this argument does not start with <, then it is considered to be a ⟨ _mini template_ ⟩. 

The syntax of the ⟨ _mini template_ ⟩ is the same as the syntax of mini templates in the enumerate package (you do not need to include the enumerate package, this is done automatically). Roughly spoken, the text of the ⟨ _mini template_ ⟩ is printed before each item, but any occurrence of a 1 in the mini template is replaced by the current item number, an occurrence of the letter A is replaced by the ![\\\( i \\\)](beameruserguide-images/D50F79E2E66556E5AE928DD6FF809A89.svg)-th letter of the alphabet (in uppercase) for the ![\\\( i \\\)](beameruserguide-images/D50F79E2E66556E5AE928DD6FF809A89.svg)-th item, and the letters a, i, and I are replaced by the corresponding lowercase letters, lowercase Roman letters, and uppercase Roman letters, respectively. So the mini template (i) would yield the items (i), (ii), (iii), (iv), and so on. The mini template A.) would yield the items A.), B.), C.), D.) and so on. For more details on the possible mini templates, see the documentation of the enumerate package. Note that there is also a template that governs the appearance of the mini template. 

_Example:_
    
    
    \begin{enumerate}
    \item This is important.
    \item This is also important.
    \end{enumerate}
    
    \begin{enumerate}[(i)]
    \item First Roman point.
    \item Second Roman point.
    \end{enumerate}
    
    \begin{enumerate}[<+->][(i)]
    \item First Roman point.
    \item Second Roman point, uncovered on second slide.
    \end{enumerate}
    

article

To use the ⟨ _mini template_ ⟩, you have to include the package enumerate. 

**Parent Beamer-Template** enumerate items

Similar to itemize items, this template is a parent template, whose children are enumerate item, enumerate subitem, enumerate subsubitem, and enumerate mini template. These templates govern how the text (the number) of an enumeration is typeset. 

The following template options are predefined:

  * • `[default]` The default enumeration marker uses the scheme 1., 2., 3. for the first level, 1.1, 1.2, 1.3 for the second level and 1.1.1, 1.1.2, 1.1.3 for the third level. 

  * • `[circle]` Places the numbers inside little circles. The colors are taken from item projected or subitem projected or subsubitem projected. 

  * • `[square]` Places the numbers on little squares. 

  * • `[ball]` “Projects” the numbers onto little balls. 




**Beamer-Template/-Color/-Font** enumerate item

This template governs how the number in front of a first-level item is typeset. The level here refers to the level of enumeration nesting only. Thus an enumerate inside an itemize is a first-level enumerate (but it uses the second-level itemize/enumerate body). 

When the template is inserted, the beamer-font and -color enumerate item are installed. 

The following command is useful for this template:

  * • `\insertenumlabel` inserts the current number of the top-level enumeration (as an Arabic number). This insert is also available in the next two templates. 




**Beamer-Template/-Color/-Font** enumerate subitem

Like enumerate item, only for second-level items. 

  * • `\insertsubenumlabel` inserts the current number of the second-level enumeration (as an Arabic number). 




_Example:_
    
    
    \setbeamertemplate{enumerate subitem}{\insertenumlabel-\insertsubenumlabel}
    

**Beamer-Template/-Color/-Font** enumerate subsubitem

Like enumerate item, only for third-level items. 

  * • `\insertsubsubenumlabel` inserts the current number of the third-level enumeration (as an Arabic number). 




**Beamer-Template/-Color/-Font** enumerate mini template

This template is used to typeset the number that arises from a mini template. 

  * • `\insertenumlabel` inserts the current number rendered by this mini template. For example, if the ⟨ _mini template_ ⟩ is (i) and this command is used in the fourth item, \insertenumlabel would yield (iv). 




The following templates govern how the _body_ of an itemize or an enumerate is typeset. 

**Beamer-Template** itemize/enumerate body begin

This template is inserted at the beginning of a first-level itemize or enumerate environment. Furthermore, before this template is inserted, the beamer-font and -color itemize/enumerate body is used. 

**Beamer-Template** itemize/enumerate body end

This template is inserted at the end of a first-level itemize or enumerate environment. 

There exist corresponding templates like itemize/enumerate subbody begin for second- and third-level itemize or enumerates. 

**Parent Beamer-Template** items

This template is a parent template of itemize items and enumerate items. 

_Example:_ \setbeamertemplate{items}[circle] will cause all items in itemize or enumerate environments to become circles (of the appropriate size, color, and font). 

\begin{description}[<⟨ _default overlay specification_ ⟩>][⟨ _long text_ ⟩]

⟨ _environment contents_ ⟩

\end{description}

Like itemize, but used to display a list that explains or defines labels. The width of ⟨ _long text_ ⟩ is used to set the indentation. Normally, you choose the widest label in the description and copy it here. If you do not give this argument, the default width is used, which can be changed using \setbeamersize with the argument description width=⟨ _width_ ⟩. 

As for enumerate, the ⟨ _default overlay specification_ ⟩ is detected by an opening <. The effect is the same as for enumerate and itemize. 

_Example:_
    
    
    \begin{description}
    \item[Lion] King of the savanna.
    \item[Tiger] King of the jungle.
    \end{description}
    
    \begin{description}[longest label]
    \item<1->[short] Some text.
    \item<2->[longest label] Some text.
    \item<3->[long label] Some text.
    \end{description}
    

_Example:_ The following has the same effect as the previous example: 
    
    
    \begin{description}[<+->][longest label]
    \item[short] Some text.
    \item[longest label] Some text.
    \item[long label] Some text.
    \end{description}
    

**Beamer-Template/-Color/-Font** description item

This template is used to typeset the description items. When this template is called, the beamer-font and -color description item are installed. 

The following template options are predefined:

  * • `[default]` By default, the description item text is just inserted without any modification. 




The main insert that is useful inside this template is:

  * • `\insertdescriptionitem` inserts the text of the current description item. 




**Beamer-Template** description body begin

This template is inserted at the beginning of a description environment. Furthermore, before this template is inserted, the beamer-font and -color description body is used. 

**Beamer-Template** description body end

This template is inserted at the end of a description environment. 

In order to simplify changing the color or font of items, the different kinds of items inherit from or just use the following “general” beamer-color and fonts: 

**Beamer-Color/-Font** item

Color parents: `local structure`

Font parents: `structure`

This color/font serves as a parent for the individual items of itemize and enumerate environments, but also for items in the table of contents. Since its color parent is the local structure, a change of that color causes the color of items to change accordingly. 

**Beamer-Color/-Font** item projected

Color/font parents: `item`

This is a special “version” of the item color and font that should be used by templates that render items with text (as in an enumeration) and which “project” this text onto something like a ball or a square or whatever. While the normal item color typically has a transparent background, the item projected typically has a colored background and, say, a white foreground. 

**Beamer-Color/-Font** subitem

Color/font parents: `item`

Same as item for subitems, that is, for items on the second level of indentation. 

**Beamer-Color/-Font** subitem projected

Color/font parents: `item projected`

Same as item projected for subitems, that is, for items on the second level of indentation. 

**Beamer-Color/-Font** subsubitem

Color/font parents: `subitem`

Same as subitem for subsubitems, that is, for items on the third level of indentation. 

**Beamer-Color/-Font** subsubitem projected

Color/font parents: `subitem projected`

Same as subitem projected for subsubitems, that is, for items on the third level of indentation. 

#####  12.2 Highlighting¶

The beamer class predefines commands and environments for highlighting text. Using these commands makes it easy to change the appearance of a document by changing the theme. 

`\structure`<⟨ _overlay specification_ ⟩>{⟨ _text_ ⟩} 

The given text is marked as part of the structure, that is, it is supposed to help the audience see the structure of your presentation. If the ⟨ _overlay specification_ ⟩ is present, the command only has an effect on the specified slides. 

_Example:_ \structure{Paragraph Heading.}

Internally, this command just puts the _text_ inside a structureenv environment. 

article

Structure text is typeset as bold text. This can be changed by modifying the templates. 

**Beamer-Color/-Font** structure

This color/font is used when structured text is typeset, but it is also widely used as a base for many other colors including the headings of blocks, item buttons, and titles. In most color themes, the colors for navigational elements in the headline or the footline are derived from the foreground color of structure. By changing the structure color you can easily change the “basic color” of your presentation, other than the color of normal text. See also the related color local structure and the related font tiny structure. 

Inside the \structure command, the background of the color is ignored, but this is not necessarily true for elements that inherit their color from structure. There is no template structure, use structure begin and structure end instead. 

**Beamer-Color** local structure

This color should be used to typeset structural elements that change their color according to the “local environment.” For example, an item “button” in an itemize environment changes its color according to circumstances. If it is used inside an example block, it should have the example text color; if it is currently “alerted” it should have the alerted text color. This color is setup by certain environments to have the color that should be used to typeset things like item buttons. Since the color used for items, item, inherits from this color by default, items automatically change their color according to the current situation. 

If you write your own environment in which the item buttons and similar structural elements should have a different color, you should change the color local structure inside these environments. 

**Beamer-Font** tiny structure

This special font is used for “tiny” structural text. Basically, this font should be used whenever a structural element uses a tiny font. The idea is that the tiny versions of the structure font often are not suitable. For example, it is often necessary to use a boldface version for them. Also, one might wish to have serif smallcaps structural text, but still retain normal sans-serif tiny structural text. 

\begin{structureenv}<⟨ _overlay specification_ ⟩>

⟨ _environment contents_ ⟩

\end{structureenv}

Environment version of the \structure command. 

**Beamer-Template** structure begin

This text is inserted at the beginning of a structureenv environment. 

The following template options are predefined:

  * • `[default]`

article

The text is typeset in boldface.




**Beamer-Template** structure end

This text is inserted at the end of a structureenv environment. 

`\alert`<⟨ _overlay specification_ ⟩>{⟨ _highlighted text_ ⟩} 

The given text is highlighted, typically by coloring the text red. If the ⟨ _overlay specification_ ⟩ is present, the command only has an effect on the specified slides. 

_Example:_ This is \alert{important}.

Internally, this command just puts the _highlighted text_ inside an alertenv. 

article

Alerted text is typeset as emphasized text. This can be changed by modifying the templates, see below. 

**Beamer-Color/-Font** alerted text

This color/font is used when alerted text is typeset. The background is currently ignored. There is no template alerted text, rather there are templates alerted text begin and alerted text end that are inserted before and after alerted text. 

\begin{alertenv}<⟨ _overlay specification_ ⟩>

⟨ _environment contents_ ⟩

\end{alertenv}

Environment version of the \alert command. 

**Beamer-Template** alerted text begin

This text is inserted at the beginning of an alertenv environment. 

The following template options are predefined:

  * • `[default]`

presentation

This changes the color local structure to alerted text. This causes things like buttons or items to be colored in the same color as the alerted text, which is often visually pleasing. See also the \structure command. 

article

The text is emphasized.




**Beamer-Template** alerted text end

This text is inserted at the end of an alertenv environment. 

#####  12.3 Block Environments¶

The beamer class predefines an environment for typesetting a “block” of text that has a heading. The appearance of blocks can easily be changed using the following template: 

**Parent Beamer-Template** blocks

Changing this parent template changes the templates of normal blocks, alerted blocks, and example blocks. 

_Example:_ \setbeamertemplate{blocks}[default]

_Example:_ \setbeamertemplate{blocks}[rounded][shadow=true]

The following template options are predefined:

  * • `[default]` The default setting typesets the block title on its own line. If a background is specified either for the block title or for the block body, this background color is used as background of the title or body, respectively. For alerted and example blocks, the corresponding beamer-colors and -fonts are used, instead. 

  * • `[rounded]`[⟨ _shadow=true_ ⟩] Makes the blocks “rounded.” This means that the corners of the backgrounds of the blocks are “rounded off.” If the shadow=true option is given, a “shadow” is drawn behind the block. 




\begin{block}<⟨ _action specification_ ⟩>{⟨ _block title_ ⟩}<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{block}

Only one ⟨ _action specification_ ⟩ may be given. Inserts a block, like a definition or a theorem, with the title ⟨ _block title_ ⟩. If the ⟨ _action specification_ ⟩ is present, the given actions are taken on the specified slides, see Section [9.6.3](<Creating-Overlays.html#section-action-specifications>). In the example, the definition is shown only from slide 3 onward. 

_Example:_
    
    
    \begin{block}<3->{Definition}
      A \alert{set} consists of elements.
    \end{block}
    

article

The block name is typeset in bold.

**Beamer-Template** block begin

This template is inserted at the beginning of a block before the ⟨ _environment contents_ ⟩. Inside this template, the block title can be accessed via the following insert: 

  * • `\insertblocktitle` Inserts the ⟨ _block title_ ⟩ into the template. 




When the template starts, no special color or font is installed (for somewhat complicated reasons). Thus, this template should install the correct colors and fonts for the title and the body itself. 

**Beamer-Template** block end

This template is inserted at the end of a block.

**Beamer-Color/-Font** block title

This beamer-color/-font should be used to typeset the title of the block. Since neither the color nor the font are setup automatically, the template block begin must do so itself. 

The default block template and also the rounded version honor the background of this color. 

**Beamer-Color/-Font** block body

This beamer-color/-font should be used to typeset the body of the block, that is, the ⟨ _environment contents_ ⟩. As for block title, the color and font must be setup by the template block begin. 

\begin{alertblock}<⟨ _action specification_ ⟩>{⟨ _block title_ ⟩}<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{alertblock}

Inserts a block whose title is highlighting. Behaves like the block environment otherwise. 

_Example:_
    
    
     \begin{alertblock}{Wrong Theorem}
       $1=2$.
     \end{alertblock}
    

article

The block name is typeset in bold and is emphasized.

**Beamer-Template** block alerted begin

Same applies as for normal blocks.

**Beamer-Template** block alerted end

Same applies as for normal blocks.

**Beamer-Color/-Font** block title alerted

Same applies as for normal blocks.

**Beamer-Color/-Font** block body alerted

Same applies as for normal blocks.

\begin{exampleblock}<⟨ _action specification_ ⟩>{⟨ _block title_ ⟩}<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{exampleblock}

Inserts a block that is supposed to be an example. Behaves like the block environment otherwise. 

_Example:_ In the following example, the block is completely suppressed on the first slide (it does not even occupy any space). 
    
    
     \begin{exampleblock}{Example}<only@2->
       The set $\{1,2,3,5\}$ has four elements.
     \end{exampleblock}
    

article

The block name is typeset in italics.

**Beamer-Template** block example begin

Same applies as for normal blocks.

**Beamer-Template** block example end

Same applies as for normal blocks.

**Beamer-Color/-Font** block title example

Same applies as for normal blocks.

**Beamer-Color/-Font** block body example

Same applies as for normal blocks.

#####  12.4 Theorem Environments¶

The beamer class predefines several environments, like theorem or definition or proof, that you can use to typeset things like, well, theorems, definitions, or proofs. The complete list is the following: theorem, Theorem, corollary, Corollary, definition, Definition, definitions, fact, example, Example, examples, Examples, lemma, Lemma, problem, Problem, proof, Proof, and solution. 

The following German block environments are also predefined: Problem, Loesung, Definition, Satz, Beweis, Folgerung, Lemma, Fakt, Theorem, Beispiel, and Beispiele. 

Here is a typical example on how to use them:
    
    
    \begin{frame}
     \frametitle{A Theorem on Infinite Sets}
    
     \begin{theorem}<1->
       There exists an infinite set.
     \end{theorem}
    
     \begin{proof}<2->
       This follows from the axiom of infinity.
     \end{proof}
    
     \begin{example}<3->[Natural Numbers]
       The set of natural numbers is infinite.
     \end{example}
    \end{frame}
    

In the following, only the English versions are discussed. The German ones behave analogously. 

\begin{theorem}<⟨ _action specification_ ⟩>[⟨ _additional text_ ⟩]<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{theorem}

Inserts a theorem. Only one ⟨ _action specification_ ⟩ may be given. If present, the ⟨ _additional text_ ⟩ is shown behind the word “Theorem” in rounded brackets (although this can be changed by the template). 

The appearance of the theorem is governed by the templates theorem begin and theorem end, see their description later on for details on how to change these. Every theorem is put into a block environment, thus the templates for blocks also apply. 

The theorem style (a concept from amsthm) used for this environment is plain. In this style, the body of a theorem should be typeset in italics. The head of the theorem should be typeset in a bold font, but this is usually overruled by the templates. 

If the option envcountsect is given either as class option in one of the presentation modes or as an option to the package beamerarticle in article mode, then the numbering of the theorems is local to each section with the section number prefixing the theorem number; otherwise they are numbered consecutively throughout the presentation or article. We recommend using this option in article mode. 

By default, no theorem numbers are shown in the presentation modes. 

_Example:_
    
    
    \begin{theorem}[Kummer, 1992]
     If $\#^_A^n$ is $n$-enumerable, then $A$ is recursive.
    \end{theorem}
    
    \begin{theorem}<2->[Tantau, 2002]
     If $\#_A^2$ is $2$-fa-enumerable, then $A$ is regular.
    \end{theorem}
    

The environments corollary, fact, and lemma behave exactly the same way. 

\documentclass[envcountsect]{beamer} 

Causes theorems, definitions, and so on to be numbered locally to each section. Thus, the first theorem of the second section would be Theorem 2.1 (assuming that there are no definitions, lemmas, or corollaries earlier in the section). 

\begin{definition}<⟨ _action specification_ ⟩>[⟨ _additional text_ ⟩]<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{definition}

Behaves like the theorem environment, except that the theorem style definition is used. In this style, the body of a theorem is typeset in an upright font. 

The environment definitions behaves exactly the same way. 

\begin{example}<⟨ _action specification_ ⟩>[⟨ _additional text_ ⟩]<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{example}

Behaves like the theorem environment, except that the theorem style example is used. A side-effect of using this theorem style is that the ⟨ _environment contents_ ⟩ is put in an exampleblock instead of a block. 

The environment examples behaves exactly the same way. 

presentation

The default template for typesetting theorems suppresses the theorem number, even if this number is “available” for typesetting (which it is by default in all predefined environments; but if you define your own environment using \newtheorem* no number will be available). 

article

In article mode, theorems are automatically numbered. By specifying the class option envcountsect, theorems will be numbered locally to each section, which is usually a good idea, except for very short articles. 

\begin{proof}<⟨ _action specification_ ⟩>[⟨ _proof name_ ⟩]<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{proof}

Typesets a proof. If the optional ⟨ _proof name_ ⟩ is given, it completely replaces the word “Proof.” This is different from normal theorems, where the optional argument is shown in brackets. 

At the end of the proof, a \qed symbol is shown, except if you say \qedhere earlier in the proof (this is exactly as in amsthm). The default \qed symbol is an open square. To completely suppress the symbol, write \def\qedsymbol{} in your preamble. To get a closed square, say 
    
    
    \setbeamertemplate{qed symbol}{\vrule width1.5ex height1.5ex depth0pt}
    

If you use babel and a different language, the text “Proof” is replaced by whatever is appropriate in the selected language. 

_Example:_
    
    
    \begin{proof}<2->[Sketch of proof]
     Suppose ...
    \end{proof}
    

**Beamer-Template/-Color/-Font** qed symbol

The symbol is shown at the end of every proof.

You can define new environments using the following command:

`\newtheorem`*{⟨ _environment name_ ⟩}[⟨ _numbered same as_ ⟩]{⟨ _head text_ ⟩}[⟨ _number within_ ⟩]

This command is used exactly the same way as in the amsthm package (as a matter of fact, it is the command from that package). For example, the two optional arguments, ⟨ _numbered same as_ ⟩ and ⟨ _number within_ ⟩, are mutually exclusive; see the documentation of amsthm for details. The only difference is that environments declared using this command are overlay specification-aware in beamer and that, when typeset, are typeset according to beamer’s templates. 

article

Environments declared using this command are also overlay specification-aware in article mode. 

_Example:_ \newtheorem{observation}[theorem]{Observation}

You can also use amsthm’s command \newtheoremstyle to define new theorem styles. Note that the default template for theorems will ignore any head font setting, but will honor the body font setting. 

If you wish to define the environments like theorem differently (for example, have it numbered within each subsection), you can use the following class option to disable the definition of the predefined environments: 

\documentclass[notheorems]{beamer} 

Switches off the definition of default blocks like theorem, but still loads amsthm and makes theorems overlay specification-aware. 

The option is also available as a package option for beamerarticle and has the same effect. 

article

In the article version, the package amsthm sometimes clashes with the document class. In this case you can use the following option, which is once more available as a class option for beamer and as a package option for beamerarticle, to switch off the loading of amsthm altogether. 

\documentclass[noamsthm]{beamer} 

Does not load amsthm and also not amsmath. Environments like theorem or proof will not be available. 

\documentclass[noamssymb]{beamer} 

Does not load amssymb. This option is mainly intended for users who are loading specialist font packages. Note that \blacktriangleright needs to be defined if itemize environments are in use. 

\documentclass[leqno]{beamer}

Place equation numbers on the left.

\documentclass[fleqn]{beamer}

Position equations at a fixed indent from the left margin rather than centered in the text column. 

**Parent Beamer-Template** theorems

This template is a parent of theorem begin and theorem end, see the first for a detailed discussion of how the theorem templates are set. 

_Example:_ \setbeamertemplate{theorems}[numbered]

The following template options are predefined:

  * • `[default]` By default, theorems are typeset as follows: The font specification for the body is honored, the font specification for the head is ignored. No theorem number is printed. 

  * • `[normal font]` Like the default, except all font specifications for the body are ignored. Thus, the fonts are used that are normally used for blocks. 

  * • `[numbered]` This option is like the default, except that the theorem number is printed for environments that are numbered. 

  * • `[ams style]` This causes theorems to be put in a block or exampleblock, but to be otherwise typeset as is normally done in amsthm. Thus the head font and body font depend on the setting for the theorem to be typeset and theorems are numbered. 




**Beamer-Template** theorem begin

Whenever an environment declared using the command \newtheorem is to be typeset, this template is inserted at the beginning and the template theorem end at the end. If there is an overlay specification when an environment like theorem is used, this overlay specification will directly follow the ⟨ _block beginning template_ ⟩ upon invocation. This is even true if there was an optional argument to the theorem environment. This optional argument is available via the insert \inserttheoremaddition. 

Numerous inserts are available in this template, see below.

Before the template starts, the font is set to the body font prescribed by the environment to be typeset. 

_Example:_ The following typesets theorems like amsthm: 
    
    
    \setbeamertemplate{theorem begin}
    {%
      \begin{\inserttheoremblockenv}
      {%
        \inserttheoremheadfont
        \inserttheoremname
        \inserttheoremnumber
        \ifx\inserttheoremaddition\@empty\else\ (\inserttheoremaddition)\fi%
        \inserttheorempunctuation
      }%
    }
    \setbeamertemplate{theorem end}{\end{\inserttheoremblockenv}}
    

_Example:_ In the following example, all font “suggestions” for the environment are suppressed or ignored; and the theorem number is suppressed. 
    
    
    \setbeamertemplate{theorem begin}
    {%
      \normalfont% ignore body font
      \begin{\inserttheoremblockenv}
      {%
        \inserttheoremname
        \ifx\inserttheoremaddition\@empty\else\ (\inserttheoremaddition)\fi%
      }%
    }
    \setbeamertemplate{theorem end}{\end{\inserttheoremblockenv}}
    

The following inserts are available inside this template:

  * • `\inserttheoremblockenv` This will normally expand to block, but if a theorem that has theorem style example is typeset, it will expand to exampleblock. Thus you can use this insert to decide which environment should be used when typesetting the theorem. 

  * • `\inserttheoremheadfont` This will expand to a font changing command that switches to the font to be used in the head of the theorem. By not inserting it, you can ignore the head font. 

  * • `\inserttheoremname` This will expand to the name of the environment to be typeset (like “Theorem” or “Corollary”). 

  * • `\inserttheoremnumber` This will expand to the number of the current theorem preceded by a space or to nothing, if the current theorem does not have a number. 

  * • `\inserttheoremaddition` This will expand to the optional argument given to the environment or will be empty, if there was no optional argument. 

  * • `\inserttheorempunctuation` This will expand to the punctuation character for the current environment. This is usually a period. 




**Beamer-Template** theorem end

Inserted at the end of a theorem.

**Beamer-Template** proof begin

Inserted at the beginning of a proof environment. This template behaves like a normal block begin template by default. 

  * • `\insertproofname` This will expand to the proof name, followed by a period most of the time. 




**Beamer-Template** proof end

Inserted at the end of a proof environment. 

#####  12.5 Framed and Boxed Text¶

In order to draw a frame (a rectangle) around some text, you can use LaTeX’s standard command \fbox and also \frame (inside a beamer frame, the \frame command changes its meaning to the normal LaTeX \frame command). More frame types are offered by the package fancybox, which defines the following commands: \shadowbox, \doublebox, \ovalbox, and \Ovalbox. Please consult the LaTeX Companion for details on how to use these commands. 

The beamer class also defines two environments for creating colored boxes. 

\begin{beamercolorbox}[⟨ _options_ ⟩]{⟨ _beamer color_ ⟩} 

⟨ _environment contents_ ⟩

\end{beamercolorbox}

This environment can be used to conveniently typeset some text using some beamer-color. Basically, the following two command blocks do the same: 
    
    
    \begin{beamercolorbox}{beamer color}
      Text
    \end{beamercolorbox}
    
    {
        \usebeamercolor{beamer color}
        \colorbox{bg}{
          \color{fg}
          Text
        }
    }
    

In other words, the environment installs the ⟨ _beamer color_ ⟩ and uses the background for the background of the box and the foreground for the text inside the box. However, in reality, numerous ⟨ _options_ ⟩ can be given to specify in much greater detail how the box is rendered. 

If the background color of ⟨ _beamer color_ ⟩ is empty, no background is drawn behind the text, that is, the background is “transparent.” 

This command is used extensively by the default inner and outer themes for typesetting the headlines and footlines. It is not really intended to be used in normal frames (for example, it is not available inside article mode). You should prefer using structuring elements like blocks or theorems that automatically insert colored boxes as needed. 

_Example:_ The following example could be used to typeset a headline with two lines, the first showing the document title, the second showing the author’s name: 
    
    
    \begin{beamercolorbox}[ht=2.5ex,dp=1ex,center]{title in head/foot}
      \usebeamerfont{title in head/foot}
      \insertshorttitle
    \end{beamercolorbox}%
    \begin{beamercolorbox}[ht=2.5ex,dp=1ex,center]{author in head/foot}
      \usebeamerfont{author in head/foot}
      \insertshortauthor
    \end{beamercolorbox}
    

_Example:_ Typesetting a postit:
    
    
    \setbeamercolor{postit}{fg=black,bg=yellow}
    \begin{beamercolorbox}[sep=1em,wd=5cm]{postit}
      Place me somewhere!
    \end{beamercolorbox}
    

The following ⟨ _options_ ⟩ can be given: 

  * • wd={⟨ _width_ ⟩} sets the width of the box. This command has two effects: First, TeX’s \hsize is set to ⟨ _width_ ⟩. Second, after the box has been typeset, its width is set to ⟨ _width_ ⟩ (no matter what it actually turned out to be). Since setting the \hsize does not automatically change some of LaTeX’s linewidth dimensions, you should consider using a minipage inside this environment if you fool around with the width. 

If the width is larger than the normal text width, as specified by the value of \textwidth, the width of the resulting box is reset to the width \textwidth, but intelligent negative skips are inserted at the left and right end of the box. The net effect of this is that you can use a width larger than the text width for a box and can insert the resulting box directly into normal text without getting annoying warnings and having the box positioned sensibly. 

  * • dp={⟨ _depth_ ⟩} sets the depth of the box, overriding the real depth of the box. The box is first typeset normally, then the depth is changed afterwards. This option is useful for creating boxes that have guaranteed size. 

If the option is not given, the box has its “natural” depth, which results from the typesetting. For example, a box containing only the letter “a” will have a different depth from a box containing only the letter “g.” 

  * • ht=⟨ _height_ ⟩ sets the height of the box, overriding the real height. Note that the “height” does not include the depth (see, for example, the TeX-book for details). If you want a one-line box that always has the same size, setting the height to 2.25ex and the depth to 1ex is usually a good option. 

  * • left causes the text inside the box to be typeset left-aligned and with a (radically) ragged right border. This is the default. To get a better ragged right border, use the rightskip option. Note that this will override any leftskip or rightskip setting. 

  * • right causes the text to be right-aligned with a (radically) ragged left border. Note that this will override any leftskip or rightskip setting. 

  * • center centers the text inside the box. Note that this will override any leftskip or rightskip setting. 

  * • leftskip=⟨ _left skip_ ⟩ installs the ⟨ _left skip_ ⟩ inside the box as the left skip. TeX’s left skip is a glue that is inserted at the left end of every line. See the TeX-book for details. Note that this will override any left, center or right setting. 

  * • rightskip=⟨ _right skip_ ⟩ install the ⟨ _right skip_ ⟩. To get a good ragged right border, try, say, \rightskip=0pt plus 4em. Note that this will override any left, center or right setting. 

  * • sep=⟨ _dimension_ ⟩ sets the size of extra space around the text. This space is added “inside the box,” which means that if you specify a sep of 1cm and insert the box normally into the vertical list, then the left border of the box will be aligned with the left border of the slide text, while the left border of the text inside the box will be 1cm to the right of this left border. Likewise, the text inside the box will stop 1cm before the right border of the normal text. 

  * • colsep=⟨ _dimension_ ⟩ sets the extra “color separation space” around the text. This space behaves the same way as the space added by sep, only this space is only inserted if the box has a colored background, that is, if the background of the ⟨ _beamer color_ ⟩ is not empty. This command can be used together with sep, the effects accumulate. 

  * • colsep*=⟨ _dimension_ ⟩ sets an extra color separation space around the text that is _horizontally outside the box_. This means that if the box has a background, this background will protrude by ⟨ _dimension_ ⟩ to the left and right of the text, but this protruding background will not be taken into consideration by TeX for typesetting purposes. 

A typical example usage of this option arises when you insert a box with a colored background in the middle of normal text. In this case, if the background color is set, you would like a background to be drawn behind the text _and_ you would like a certain extra space around this text (the background should not stop immediately at the borders of the text, this looks silly) _and_ you would like the normal text always to be at the same horizontal position, independently of whether a background is present or not. In this case, using colsep*=4pt is a good option. 

  * • shadow=⟨ _true or false_ ⟩ draws a shadow behind the box. Currently, this option only has an effect if used together with the rounded option, but that may change. 

  * • rounded=⟨ _true or false_ ⟩ causes the borders of the box to be rounded off if there is a background installed. This command internally calls beamerboxesrounded. In this case, colsep* option will have no effect. 

  * • ignorebg causes the background color of the ⟨ _beamer color_ ⟩ to be ignored, that is, to be treated as if it were set to “transparent” or “empty.” 

  * • vmode causes TeX to be in vertical mode when the box starts. Normally, TeX will be in horizontal mode at the start of the box (a \leavevmode is inserted automatically at the beginning of the box unless this option is given). Only TeXperts need this option, so, if you use it, you will probably know what you are doing anyway. 




\begin{beamerboxesrounded}[⟨ _options_ ⟩]{⟨ _head_ ⟩} 

⟨ _environment contents_ ⟩

\end{beamerboxesrounded}

The text inside the environment is framed by a rectangular area with rounded corners. For the large rectangular area, the beamer-color specified with the lower option is used. Its background is used for the background, its foreground for the foreground. If the ⟨ _head_ ⟩ is not empty, ⟨ _head_ ⟩ is drawn in the upper part of the box using the beamer-color specified with the upper option for the fore- and background. The following options can be given: 

  * • lower=⟨ _beamer color_ ⟩ sets the beamer-color to be used for the lower (main) part of the box. Its background is used for the background, its foreground for the foreground of the main part of the box. If either is empty, the current background or foreground is used. The box will never be transparent. 

  * • upper=⟨ _beamer color_ ⟩ sets the beamer-color used for the upper (head) part of the box. It is only used if the ⟨ _head_ ⟩ is not empty. 

  * • width=⟨ _dimension_ ⟩ causes the width of the text inside the box to be the specified ⟨ _dimension_ ⟩. By default, the \textwidth is used. Note that the box will protrude 4pt to the left and right. 

  * • shadow=⟨ _true or false_ ⟩. If set to true, a shadow will be drawn. 




If no ⟨ _head_ ⟩ is given, the head part is completely suppressed. 

_Example:_
    
    
    \begin{beamerboxesrounded}[upper=block head,lower=block body,shadow=true]{Theorem}
      $A = B$.
    \end{beamerboxesrounded}
    

article

This environment is not available in article mode. 

#####  12.6 Figures and Tables¶

You can use the standard LaTeX environments figure and table much the same way you would normally use them. However, any placement specification will be ignored. Figures and tables are immediately inserted where the environments start. If there are too many of them to fit on the frame, you must manually split them among additional frames or use the allowframebreaks option. 

_Example:_
    
    
    \begin{frame}
      \begin{figure}
        \pgfuseimage{myfigure}
        \caption{This caption is placed below the figure.}
      \end{figure}
    
      \begin{figure}
        \caption{This caption is placed above the figure.}
        \pgfuseimage{myotherfigure}
      \end{figure}
    \end{frame}
    

**Beamer-Template/-Color/-Font** caption

This template is used to render the caption.

The following template options are predefined:

  * • `[default]` typesets the caption name (a word like “Figure” or “Abbildung” or “Table,” depending on whether a table or figure is typeset and depending on the currently installed language) before the caption text. No number is printed, since these make little sense in a normal presentation. 

  * • `[numbered]` adds the figure or table number to the caption. Use this option only if your audience has a printed handout or printed lecture notes that follow the same numbering. 

  * • `[caption name own line]` As the name suggests, this option puts the caption name (like “Figure”) on its own line. 




Inside the template, you can use the following inserts:

  * • `\insertcaption` Inserts the text of the current caption. 

  * • `\insertcaptionname` Inserts the name of the current caption. This word is either “Table” or “Figure” or, if the babel package is used, some translation thereof. 

  * • `\insertcaptionnumber` Inserts the number of the current figure or table. 




**Beamer-Color/-Font** caption name

These beamer-color and -font are used to typeset the caption name (a word like “Figure”). The caption template must directly “use” them, they are not installed automatically by the \insertcaptionname command. 

**Beamer-Template** caption label separator

This template is inserted between caption name and caption text. 

The following template options are predefined:

  * • `[default]` Typesets the colon followed by the space. 

  * • `[none]` Typesets no separator. 

  * • `[colon]` Alias for the default. 

  * • `[period]` Typesets the period followed by the space. 

  * • `[space]` Typesets the space. 

  * • `[quad]` Typesets the \quad followed by the space. 

  * • `[endash]` Typesets the en-dash surrounded by spaces ( \-- ). 




#####  12.7 Splitting a Frame into Multiple Columns¶

The beamer class offers several commands and environments for splitting (perhaps only part of) a frame into multiple columns. These commands have nothing to do with LaTeX’s commands for creating columns. Columns are especially useful for placing a graphic next to a description/explanation. 

The main environment for creating columns is called columns. Inside this environment, you can either place several column environments, each of which creates a new column, or use the \column command to create new columns. 

\begin{columns}<⟨ _action specification_ ⟩>[⟨ _options_ ⟩]

⟨ _environment contents_ ⟩

\end{columns}

A multi-column area. If the ⟨ _action specification_ ⟩ is present, the given actions are taken on the specified slides, see Section [9.6.3](<Creating-Overlays.html#section-action-specifications>). Inside the environment you should place only column environments or \column commands (see below). The following ⟨ _options_ ⟩ may be given: 

  * • b will cause the bottom lines of the columns to be vertically aligned. 

  * • c will cause the columns to be centered vertically relative to each other. Default, unless the global option t is used. 

  * • onlytextwidth is the same as totalwidth=\textwidth. This option can also be set for the whole document with the onlytextwidth class option: 

\documentclass[onlytextwidth]{beamer} 

  * • t will cause the first lines of the columns to be aligned. Default if global option t is used. 

  * • T is similar to the t option, but T aligns the tops of the first lines while t aligns the so-called baselines of the first lines. If strange things seem to happen in conjunction with the t option (for example if a graphic suddenly “drops down” with the t option instead of “going up”), try using this option instead. 

  * • totalwidth=⟨ _width_ ⟩ will cause the columns to occupy not the whole page width, but only ⟨ _width_ ⟩, all told. Note that this means that any margins are ignored. 




_Example:_
    
    
    \begin{columns}[t]
      \begin{column}{5cm}
        Two\\lines.
      \end{column}
      \begin{column}{5cm}
        One line (but aligned).
      \end{column}
    \end{columns}
    

_Example:_
    
    
    \begin{columns}[t]
      \column{5cm}
        Two\\lines.
    
      \column[T]{5cm}
        \includegraphics[height=3cm]{mygraphic.jpg}
    \end{columns}
    

article

This environment is ignored in article mode. 

To create a column, you can either use the column environment or the \column command. 

\begin{column}<⟨ _action specification_ ⟩>[⟨ _placement_ ⟩]{⟨ _column width_ ⟩} 

⟨ _environment contents_ ⟩

\end{column}

Creates a single column of width ⟨ _column width_ ⟩. If the ⟨ _action specification_ ⟩ is present, the given actions are taken on the specified slides, see Section [9.6.3](<Creating-Overlays.html#section-action-specifications>). The vertical placement of the enclosing columns environment can be overruled by specifying a specific ⟨ _placement_ ⟩ (t and T for the two top modes, c for centered, and b for bottom). 

_Example:_ The following code has the same effect as the above examples: 
    
    
    \begin{columns}
      \begin{column}[t]{5cm}
        Two\\lines.
      \end{column}
      \begin{column}[t]{5cm}
        One line (but aligned).
      \end{column}
    \end{columns}
    

article

This command is ignored in article mode. 

`\column`<⟨ _action specification_ ⟩>[⟨ _placement_ ⟩]{⟨ _column width_ ⟩} 

Starts a single column. The parameters and options are the same as for the column environment. The column automatically ends with the next occurrence of \column or of a column environment or of the end of the current columns environment. 

_Example:_
    
    
    \begin{columns}
      \column[t]{5cm}
        Two\\lines.
      \column[t]{5cm}
        One line (but aligned).
    \end{columns}
    

article

This command is ignored in article mode. 

#####  12.8 Positioning Text and Graphics Absolutely¶

Normally, beamer uses TeX’s normal typesetting mechanism to position text and graphics on the page. In certain situation you may instead wish a certain text or graphic to appear at a page position that is specified _absolutely_. This means that the position is specified relative to the upper left corner of the slide. 

The package textpos provides several commands for positioning text absolutely and it works together with beamer. When using this package, you will typically have to specify the options overlay and perhaps absolute. For details on how to use the package, please see its documentation. 

Another package to conveniently position elements at specific positions on the frame is Ti _k_ Z. Besides the possibility to manually chose coordinates, this also allows to position elements in respect to the page: 

_Example:_
    
    
    \usepackage{tikz}
    
    \begin{frame}
      \tikz[remember picture, overlay] \node at (3.1415,1) {I'm here};
    
      \tikz[remember picture, overlay] \node at (current page.center) {I'm the centre of the frame!};
    \end{frame}
    

#####  12.9 Verbatim and Fragile Text¶

If you wish to use a {verbatim} environment in a frame, you have to add the option [fragile] to the {frame} environment. The \end{frame} must be alone on a single line (except for any leading whitespace). Using this option will cause the frame contents to be written to an external file and then read back. See the description of the {frame} environment for more details. 

You must also use the [fragile] option for frames that include any “fragile” text, which is any text that is not “interpreted the way text is usually interpreted by TeX.” For example, if you use a package that (locally) redefined the meaning of, say, the character &, you must use this option. 

Inside {verbatim} environments you obviously cannot use commands like \alert<2> to highlight part of code since the text is written in, well, verbatim. There are several good packages like alltt or listings that allow you to circumvent this problem. For simple cases, the following environment can be used, which is defined by beamer: 

\begin{semiverbatim}

⟨ _environment contents_ ⟩

\end{semiverbatim}

The text inside this environment is typeset like verbatim text. However, the characters \, {, and } retain their meaning. Thus, you can say things like 
    
    
    \alert<1->{std::cout << "AT&T likes 100% performance";}
    

To typeset the three characters \, {, and } you can use the commands \\\ (which is redefined inside this environment—you do not need it anyway), \\{, and \\}. Thus in order to get typeset “\alert<1>{X}” you can write \\\alert<1>\\{X\\}. 

#####  12.10 Abstract¶

The {abstract} environment is overlay specification-aware in beamer: 

\begin{abstract}<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{abstract}

You can use this environment to typeset an abstract.

**Beamer-Color/-Font** abstract

These beamer-color and -font are used to typeset the abstract. If a background color is set, this background color is used as background for the whole abstract by default. 

**Beamer-Template/-Color/-Font** abstract title

Color parents: `titlelike`

This template is used for the title. By default, this inserts the word \abstractname, centered. The background color is ignored. 

**Beamer-Template** abstract begin

This template is inserted at the very beginning of the abstract, before the abstract title and the ⟨ _environment contents_ ⟩ is inserted. 

**Beamer-Template** abstract end

This template is inserted at the end of the abstract, after the ⟨ _environment contents_ ⟩. 

#####  12.11 Verse, Quotations, Quotes¶

LaTeX defines three environments for typesetting quotations and verses: verse, quotation, and quote. These environments are also available in the beamer class, where they are overlay specification-aware. If an overlay specification is given, the verse or quotation is shown only on the specified slides and is covered otherwise. The difference between a quotation and a quote is that the first has paragraph indentation, whereas the second hasn’t. 

You can change the font and color used for these by changing the beamer-colors and -fonts listed below. Unlike the standard LaTeX environments, the default font theme typesets a verse in an italic serif font, quotations and quotes are typeset using an italic font (whether serif or sans-serif depends on the standard document font). 

\begin{verse}<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{verse}

You can use this environment to typeset a verse.

**Beamer-Color/-Font** verse

These beamer-color and -font are used to typeset the verse. If a background color is set, this background color is used as background for the whole abstract. The default font is italic serif. 

**Beamer-Template** verse begin

This template is inserted at the beginning of the verse.

**Beamer-Template** verse end

This template is inserted at the end of the verse.

\begin{quotation}<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{quotation}

Use this environment to typeset multi-paragraph quotations. Think again, before presenting multi-paragraph quotations. 

**Beamer-Color/-Font** quotation

These beamer-color and -font are used to typeset the quotation. 

**Beamer-Template** quotation begin

This template is inserted at the beginning of the quotation. 

**Beamer-Template** quotation end

This template is inserted at the end of the quotation.

\begin{quote}<⟨ _action specification_ ⟩>

⟨ _environment contents_ ⟩

\end{quote}

Use this environment to typeset a single-paragraph quotation.

**Beamer-Color/-Font** quote

These beamer-color and -font are used to typeset the quote. 

**Beamer-Template** quote begin

This template is inserted at the beginning of the quote.

**Beamer-Template** quote end

This template is inserted at the end of the quote.

#####  12.12 Footnotes¶

First a word of warning: Using footnotes is usually not a good idea. They disrupt the flow of reading. 

You can use the usual \footnote command. It has been augmented to take an additional option, for placing footnotes at the frame bottom instead of at the bottom of the current minipage. 

`\footnote`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]{⟨ _text_ ⟩} 

Inserts a footnote into the current frame. Footnotes will always be shown at the bottom of the current frame; they will never be “moved” to other frames. As usual, one can give a number as ⟨ _options_ ⟩, which will cause the footnote to use that number. The beamer class adds one additional option: 

  * • frame causes the footnote to be shown at the bottom of the frame. This is normally the default behavior anyway, but in minipages and certain blocks it makes a difference. In a minipage, the footnote is usually shown as part of the minipage rather than as part of the frame. 




If an ⟨ _overlay specification_ ⟩ is given, this causes the footnote ⟨ _text_ ⟩ to be shown only on the specified slides. The footnote symbol in the text is shown on all slides. 

_Example:_ \footnote{On a fast machine.}

_Example:_ \footnote[frame,2]{Not proved.}

_Example:_ \footnote<.->{Der Spiegel, 4/04, S.~90.}

article

In article mode, footnotes are typeset as usual. The frame option has no effect, which means in a minipage the footnote is shown as part of it. 

**Beamer-Template/-Color/-Font** footnote

This template will be used to render the footnote. Inside this template, the following two inserts can be used: 

  * • `\insertfootnotetext` Inserts the current footnote text. 

  * • `\insertfootnotemark` Inserts the current footnote mark (like a raised number). This mark is computed automatically. 




**Beamer-Color/-Font** footnote mark

This beamer-color/-font is used when rendering the footnote mark, both in the text and at the beginning of the footnote itself. 
