## Changing the Way Things Look  
  
####  16 Inner Themes, Outer Themes, and Templates 

This section discusses the inner and outer themes that are available in beamer. These themes install certain _templates_ for the different elements of a presentation. The template mechanism is explained at the end of the section. 

Before we plunge into the details, let us agree on some terminology for this section. In beamer, an _element_ is part of a presentation that is potentially typeset in some special way. Examples of elements are frame titles, the author’s name, or the footnote sign. The appearance of every element is governed by a _template_ for this element. Appropriate templates are installed by inner and outer themes, where the _inner_ themes only install templates for elements that are typically “inside the main text,” while _outer_ themes install templates for elements “around the main text.” Thus, from the templates’ point of view, there is no real difference between inner and outer themes. 

#####  16.1 Inner Themes¶

An inner theme installs templates that dictate how the following elements are typeset: 

  * • Title and part pages. 

  * • Itemize environments. 

  * • Enumerate environments. 

  * • Description environments. 

  * • Block environments.

  * • Theorem and proof environments. 

  * • Figures and tables.

  * • Footnotes.

  * • Bibliography entries. 




In the following examples, the color themes seahorse and rose are used to show where and how background colors are honored. Furthermore, background colors have been specified for all elements that honor them in the default theme. In the default color theme, all of the large rectangular areas are transparent. 

\useinnertheme{default}

_Example:_

The default element theme is quite sober. The only extravagance is the fact that a little triangle is used in itemize environments instead of the usual dot. 

In some cases the theme will honor background color specifications for elements. For example, if you set the background color for block titles to green, block titles will have a green background. The background specifications are currently honored for the following elements: 

  * • Title, author, institute, and date fields in the title page. 

  * • Block environments, both for the title and for the body. 




This list may increase in the future.

\useinnertheme{circles}

_Example:_

In this theme, itemize and enumerate items start with a small circle. Likewise, entries in the table of contents start with circles. 

\useinnertheme{rectangles}

_Example:_

In this theme, itemize and enumerate items and table of contents entries start with small rectangles. 

\useinnertheme[⟨ _options_ ⟩]{rounded}

_Example:_

In this theme, itemize and enumerate items and table of contents entries start with small balls. If a background is specified for blocks, then the corners of the background rectangles will be rounded off. The following ⟨ _options_ ⟩ may be given: 

  * • shadow adds a shadow to all blocks. 




\useinnertheme{inmargin}

_Example:_

The idea behind this theme is to have “structuring” information on the left and “normal” information on the right. To this end, blocks are redefined such that the block title is shown on the left and the block body is shown on the right. 

The code used to place text in the margin is a bit fragile. You may often need to adjust the spacing “by hand,” so use at your own risk. 

Itemize items are redefined such that they appear on the left. However, only the position is changed by changing some spacing parameters; the code used to draw the items is not changed otherwise. Because of this, you can load another inner theme first and then load this theme afterwards. 

This theme is a “dirty” inner theme since it messes with things that an inner theme should not mess with. In particular, it changes the width of the left sidebar to a large value. However, you can still use it together with most outer themes. 

Using columns inside this theme is problematic. Most of the time, the result will not be what you expect. 

The indicators for the title page can be adjusted by redefining \inserttitleindicator, \insertauthorindicator, \insertinstituteindicator and \insertdateindicator. 

#####  16.2 Outer Themes¶

An outer theme dictates (roughly) the overall layout of frames. It specifies where any navigational elements should go (like a mini table of contents or navigational mini frames) and what they should look like. Typically, an outer theme specifies how the following elements are rendered: 

  * • The head- and footline. 

  * • The sidebars.

  * • The logo.

  * • The frame title.




An outer theme will not specify how things like itemize environments should be rendered—that is the job of an inner theme. 

In the following examples the color theme seahorse is used. Since the default color theme leaves most backgrounds empty, most of the outer themes look too unstructured with the default color theme. 

\useoutertheme{default}

_Example:_

The default layout theme is the most sober and minimalistic theme around. It will flush left the frame title and it will not install any head- or footlines. However, even this theme honors the background color specified for the frame title. If a color is specified, a bar occupying the whole page width is put behind the frame title. A background color of the frame subtitle is ignored. 

\useoutertheme{infolines}

_Example:_

This theme installs a headline showing the current section and the current subsection. It installs a footline showing the author’s name, the institution, the presentation’s title, the current date, and a frame count. This theme uses only little space. 

The colors used in the headline and footline are drawn from palette primary, palette secondary, and palette tertiary (see Section [17](<Colors.html#section-colors>) for details on how to change these). 

\useoutertheme[⟨ _options_ ⟩]{miniframes}

_Example:_

This theme installs a headline in which a horizontal navigational bar is shown. This bar contains one entry for each section of the presentation. Below each section entry, small circles are shown that represent the different frames in the section. The frames are arranged subsection-wise, that is, there is a line of frames for each subsection. If the class option compress is given, the frames will instead be arranged in a single row for each section. The navigation bars draws its color from section in head/foot. 

Below the navigation bar, a line is put showing the title of the current subsection. The color is drawn from subsection in head/foot. 

At the bottom, two lines are put that contain information such as the author’s name, the institution, or the paper’s title. What is shown exactly is influenced by the ⟨ _options_ ⟩ given. The colors are drawn from the appropriate beamer-colors like author in head/foot. 

At the top and bottom of both the head- and footline and between the navigation bar and the subsection name, separation lines are drawn _if_ the background color of separation line is set. This separation line will have a height of 3pt. You can get even more fine-grained control over the colors of the separation lines by setting appropriate colors like lower separation line head. 

_Note:_ Make sure the document is organized in the section-subsection-frame structure when using miniframes and smoothbars theme. Any frame without a \section or \subsection will bring unpredictable effects in the navigation bar. 

The following ⟨ _options_ ⟩ can be given: 

  * • footline=empty suppresses the footline (default). 

  * • footline=authorinstitute shows the author’s name and the institute in the footline. 

  * • footline=authortitle shows the author’s name and the title in the footline. 

  * • footline=institutetitle shows the institute and the title in the footline. 

  * • footline=authorinstitutetitle shows the author’s name, the institute, and the title in the footline. 

  * • subsection=⟨ _true or false_ ⟩ shows or suppresses line showing the subsection in the headline. It is shown by default. If the document does not use subsections, this option should be set false. 




\useoutertheme[⟨ _options_ ⟩]{smoothbars}

_Example:_

This theme behaves very much like the miniframes theme, at least with respect to the headline. The only differences are that smooth transitions are installed between the background colors of the navigation bar, the (optional) bar for the subsection name, and the background of the frame title. No footline is created. You can get the footlines of the miniframes theme by first loading that theme and then loading the smoothbars theme. 

The following ⟨ _options_ ⟩ can be given: 

  * • subsection=⟨ _true or false_ ⟩ shows or suppresses line showing the subsection in the headline. It is shown by default. 




\useoutertheme[⟨ _options_ ⟩]{sidebar}

_Example:_

In this layout, a sidebar is shown that contains a small table of contents with the current section, subsection, or subsubsection highlighted. The frame title is vertically centered in a rectangular area at the top that always occupies the same amount of space in all frames. Finally, the logo is shown in the “corner” resulting from the sidebar and the frame title rectangle. 

There are several ways of modifying the layout using the ⟨ _options_ ⟩. If you set the width of the sidebar to 0pt, it is not shown, giving you a layout in which the frame title does not “wobble” since it always occupies the same amount of space on all slides. Conversely, if you set the height of the frame title rectangle to 0pt, the rectangular area is not used and the frame title is inserted normally (occupying as much space as needed on each slide). 

The background color of the sidebar is taken from sidebar, the background color of the frame title from frametitle, and the background color of the logo corner from logo. 

The colors of the entries in the table of contents are drawn from the beamer-color section in sidebar and section in sidebar current as well as the corresponding beamer-colors for subsections. If an entry does not fit on a single line it is automatically “linebroken.” 

The following ⟨ _options_ ⟩ may be given: 

  * • height=⟨ _dimension_ ⟩ specifies the height of the frame title rectangle. If it is set to 0pt, no frame title rectangle is created. Instead, the frame title is inserted normally into the frame. The default is 2.5 base line heights of the frame title font. Thus, there is about enough space for a two-line frame title plus a one-line subtitle. 

  * • hideothersubsections causes all subsections except those of the current section to be suppressed in the table of contents. This is useful if you have lots of subsections. 

  * • hideallsubsections causes all subsections to be suppressed in the table of contents. 

  * • left puts the sidebar on the left side. Note that in a left-to-right reading culture this is the side people look first. Note also that this table of contents is usually _not_ the most important part of the frame, so you do not necessarily want people to look at it first. Nevertheless, it is the default. 

  * • right puts the sidebar of the right side. 

  * • width=⟨ _dimension_ ⟩ specifies the width of the sidebar. If it is set to 0pt, it is completely suppressed. The default is 2.5 base line heights of the frame title font. 




\useoutertheme{split}

_Example:_

This theme installs a headline in which, on the left, the sections of the talk are shown and, on the right, the subsections of the current section. If the class option compress has been given, the sections and subsections will be put in one line; normally there is one line per section or subsection. 

The footline shows the author on the left and the talk’s title on the right. 

The colors are taken from palette primary and palette quaternary. 

\useoutertheme{shadow}

_Example:_

This layout theme extends the split theme by putting a horizontal shading behind the frame title and adding a little “shadow” at the bottom of the headline. 

\useoutertheme[⟨ _options_ ⟩]{tree}

_Example:_

In this layout, the headline contains three lines that show the title of the current talk, the current section in this talk, and the current subsection in the section. The colors are drawn from title in head/foot, section in head/foot, and subsection in head/foot. 

In addition, separation lines of height 3pt are shown above and below the three lines _if_ the background of separation line is set. More fine-grained control of the colors of these lines can be gained by setting upper separation line head and lower separation line head. 

The following ⟨ _options_ ⟩ may be given: 

  * • hooks causes little “hooks” to be drawn in front of the section and subsection entries. These are supposed to increase the tree-like appearance. 




\useoutertheme{smoothtree}

_Example:_

This layout is similar to the tree layout. The main difference is that the background colors change smoothly. 

#####  16.3 Changing the Templates Used for Different Elements of a Presentation¶

This section explains how beamer’s template management works. 

######  16.3.1 Overview of Beamer’s Template Management¶

If you only wish to modify the appearance of a single or few elements, you do not need to create a whole new inner or outer theme. Instead, you can modify the appropriate template. 

A template specifies how an element of a presentation is typeset. For example, the frametitle template dictates where the frame title is put, which font is used, and so on. 

As the name suggests, you specify a template by writing the exact LaTeX code you would also use when typesetting a single frame title by hand. Only, instead of the actual title, you use the command \insertframetitle. 

_Example:_ Suppose we would like to have the frame title typeset in red, centered, and boldface. If we were to typeset a single frame title by hand, it might be done like this: 
    
    
    \begin{frame}
      \begin{centering}
        \color{red}
        \textbf{The Title of This Frame.}
        \par
      \end{centering}
    
      Blah, blah.
    \end{frame}
    

In order to typeset the frame title in this way on all slides, in the simplest case we can change the frame title template as follows: 
    
    
    \setbeamertemplate{frametitle}
    {
      \begin{centering}
        \color{red}
        \textbf{\insertframetitle}
        \par
      \end{centering}
    }
    

We can then use the following code to get the desired effect:
    
    
    \begin{frame}
      \frametitle{The Title of This Frame.}
    
      Blah, blah.
    \end{frame}
    

When rendering the frame, beamer will use the code of the frame title template to typeset the frame title and it will replace every occurrence of \insertframetitle by the current frame title. 

We can take this example a step further. It would be nicer if we did not have to “hardwire” the color of the frametitle, but if this color could be specified independently of the code for the template. This way, a color theme could change this color. Since this is a problem that is common to most templates, beamer will automatically setup the beamer-color frametitle when the template frametitle is used. Thus, we can remove the \color{red} command if we set the beamer-color frametitle to red at some point. 
    
    
    \setbeamercolor{frametitle}{fg=red}
    \setbeamertemplate{frametitle}
    {
      \begin{centering}
        \textbf{\insertframetitle}
        \par
      \end{centering}
    }
    

Next, we can also make the font “themable.” Just like the color, the beamer-font frametitle is installed before the frametitle template is typeset. Thus, we should rewrite the code as follows: 
    
    
    \setbeamercolor{frametitle}{fg=red}
    \setbeamerfont{frametitle}{series=\bfseries}
    \setbeamertemplate{frametitle}
    {
      \begin{centering}
        \insertframetitle\par
      \end{centering}
    }
    

Users, themes, or whoever can now easily change the color or font of the frametitle without having to mess with the code used to typeset it. 

article

In article mode, most of the template mechanism is switched off and has no effect. However, a few templates are also available. If this is the case, it is specially indicated. 

Here are a few hints that might be helpful when you wish to set a template: 

  * • Usually, you might wish to copy code from an existing template. The code often takes care of some things that you may not yet have thought about. The default inner and outer themes might be useful starting points. Also, the file beamerbaseauxtemplates.sty contains interesting “auxiliary” templates. 

  * • When copying code from another template and when inserting this code in the preamble of your document (not in another style file), you may have to “switch on” the at-character (@). To do so, add the command \makeatletter before the \setbeamertemplate command and the command \makeatother afterward. 

  * • Most templates having to do with the frame components (headlines, sidebars, etc.) can only be changed in the preamble. Other templates can be changed during the document. 

  * • The height of the headline and footline templates is calculated automatically. This is done by typesetting the templates and then “having a look” at their heights. This recalculation is done right at the beginning of the document, _after_ all packages have been loaded and even _after_ these have executed their \AtBeginDocument initialization. 

  * • Getting the boxes right inside any template is often a bit of a hassle. You may wish to consult the TeX book for the glorious details on “Making Boxes.” If your headline is simple, you might also try putting everything into a pgfpicture environment, which makes the placement easier. 




######  16.3.2 Using Beamer’s Templates¶

As a user of the beamer class you typically do not “use” or “invoke” templates yourself, directly. For example, the frame title template is automatically invoked by beamer somewhere deep inside the frame typesetting process. The same is true of most other templates. However, if, for whatever reason, you wish to invoke a template yourself, you can use the following command. 

`\usebeamertemplate`***{⟨ _element name_ ⟩} 

If none of the stars is given, the text of the ⟨ _element name_ ⟩ is directly inserted at the current position. This text should previously have been specified using the \setbeamertemplate command. No text is inserted if this command has not been called before. 

_Example:_
    
    
    \setbeamertemplate{my template}{correct}
    ...
    Your answer is \usebeamertemplate{my template}.
    

If you add one star, three things happen. First, the template is put inside a TeX-group, thereby limiting most side effects of commands used inside the template. Second, inside this group the beamer-color named ⟨ _element name_ ⟩ is used and the foreground color is selected. Third, the beamer-font ⟨ _element name_ ⟩ is also used. This one-starred version is usually the best version to use. 

If you add a second star, nearly the same happens as with only one star. However, in addition, the color is used with the command \setbeamercolor*. This causes the colors to be reset to the normal text color if no special foreground or background is specified by the beamer-color ⟨ _element name_ ⟩. Thus, in this twice-starred version, the color used for the template is guaranteed to be independent of the color that was currently in use when the template is used. 

Finally, adding a third star will also cause a star to be added to the \setbeamerfont* command. This causes the font used for the template also to be reset to normal text, unless the beamer-font ⟨ _element name_ ⟩ specifies things differently. This three-star version is the “most protected” version available. 

`\ifbeamertemplateempty`{⟨ _beamer template name_ ⟩}{⟨ _executed if empty_ ⟩}{⟨ _executed otherwise_ ⟩} 

This command checks whether a template is defined and set to a non-empty text. If the text is empty or the template is not defined at all, ⟨ _executed if empty_ ⟩ is executed. Otherwise, ⟨ _executed otherwise_ ⟩ is executed. 

`\expandbeamertemplate`{⟨ _beamer template name_ ⟩} 

This command does the same as \usebeamertemplate{⟨ _beamer template name_ ⟩}. The difference is that this command performs a direct expansion and does not scan for a star. This is important inside, for example, an \edef. If you don’t know the difference between \def and \edef, you won’t need this command. 

######  16.3.3 Setting Beamer’s Templates¶

To set a beamer-template, you can use the following command: 

`\setbeamertemplate`{⟨ _element name_ ⟩}[⟨ _predefined option_ ⟩]⟨ _args_ ⟩

In the simplest case, if no ⟨ _predefined option_ ⟩ is given, the ⟨ _args_ ⟩ must be a single argument and the text of the template ⟨ _element name_ ⟩ is setup to be this text. Upon later invocation of the template by the command \usebeamertemplate this text is used. 

_Example:_
    
    
    \setbeamertemplate{answer}{correct}
    ...
    Your answer is \usebeamertemplate*{answer}.
    

If you specify a ⟨ _predefined option_ ⟩, this command behaves slightly differently. In this case, someone has used the command \defbeamertemplate to predefine a template for you. By giving the name of this predefined template as the optional parameter ⟨ _predefined option_ ⟩, you cause the template ⟨ _element name_ ⟩ to be set to this template. 

_Example:_ \setbeamertemplate{bibliography item}[book] causes the bibliography items to become little book icons. This command causes a subsequent call of \usebeamertemplate{bibliography item} to insert the predefined code for inserting a book. 

Some predefined template options take parameters themselves. In such a case, the parameters are given as ⟨ _args_ ⟩. 

_Example:_ The ⟨ _predefined option_ ⟩ grid for the template background takes an optional argument: 
    
    
    \setbeamertemplate{background}[grid][step=1cm]
    

In the example, the second argument in square brackets is the optional argument. 

In the descriptions of elements, if there are possible ⟨ _predefined option_ ⟩, the description shows how the ⟨ _predefined option_ ⟩ can be used together with its arguments, but the \setbeamertemplate{xxxx} is omitted. Thus, the above example would be documented in the description of the background element like this: 

  * • `[grid]`[⟨ _step options_ ⟩] causes a light grid to be … 




`\addtobeamertemplate`{⟨ _element name_ ⟩}{⟨ _pre-text_ ⟩}{⟨ _post-text_ ⟩} 

This command adds the ⟨ _pre-text_ ⟩ before the text that is currently installed as the template ⟨ _element name_ ⟩ and the ⟨ _post-text_ ⟩ after it. This allows you a limited form of modification of existing templates. 

_Example:_ The following commands have the same effect:
    
    
    \setbeamertemplate{my template}{Hello world!}
    
    \setbeamertemplate{my template}{world}
    \addtobeamertemplate{my template}{Hello }{!}
    

If a new template is installed, any additions will be deleted. On the other hand, you can repeatedly use this command to add multiple things. 

`\defbeamertemplate`<⟨ _mode specification_ ⟩>*{⟨ _element name_ ⟩}{⟨ _predefined option_ ⟩}  
[⟨ _argument number_ ⟩][⟨ _default optional argument_ ⟩]{⟨ _predefined text_ ⟩}  
[action]{⟨ _action command_ ⟩}

This command installs a _predefined option_ for the template ⟨ _element name_ ⟩. Once this command has been used, users can access the predefined template using the \setbeamertemplate command. 

_Example:_ \defbeamertemplate{itemize item}{double arrow}{$\Rightarrow$}

After the above command has been invoked, the following two commands will have the same effect: 
    
    
    \setbeamertemplate{itemize item}{$\Rightarrow$}
    \setbeamertemplate{itemize item}[double arrow]
    

Sometimes, a predefined template needs to get an argument when it is installed. Suppose, for example, we want to define a predefined template that draws a square as the itemize item and we want to make this size of this square configurable. In this case, we can specify the ⟨ _argument number_ ⟩ of the predefined option the same way one does for the \newcommand command: 
    
    
    \defbeamertemplate{itemize item}{square}[1]{\hrule width #1 height #1}
    
    %% The following have the same effect:
    \setbeamertemplate{itemize item}[square]{3pt}
    \setbeamertemplate{itemize item}{\hrule width 3pt height 3pt}
    

As for the \newcommand command, you can also specify a ⟨ _default optional argument_ ⟩: 
    
    
    \defbeamertemplate{itemize item}{square}[1][1ex]{\hrule width #1 height #1}
    
    %% The following have the same effect:
    \setbeamertemplate{itemize item}[square][3pt]
    \setbeamertemplate{itemize item}{\hrule width 3pt height 3pt}
    
    %% So do the following:
    \setbeamertemplate{itemize item}[square]
    \setbeamertemplate{itemize item}{\hrule width 1ex height 1ex}
    

The starred version of the command installs the predefined template option, but then immediately calls \setbeamertemplate for this option. This is useful for the default templates. If there are any arguments necessary, these are set to \relax. 

In certain cases, if a predefined template option is chosen, you do not only wish the template text to be installed, but certain extra “actions” must also be taken once. For example, a shading must be defined that should not be redefined every time the shading is used later on. To implement such “actions,” you can use the optional argument ⟨ _action_ ⟩ following the keyword [action]. Thus, after the normal use of the \defbeamertemplate you add the text [action] and then any commands that should be executed once when the ⟨ _predefined option_ ⟩ is selected by the \setbeamertemplate command. 

_Example:_
    
    
    \defbeamertemplate{background canvas}{my shading}[2]
    {
      \pgfuseshading{myshading}% simple enough
    }
    [action]
    {
      \pgfdeclareverticalshading{myshading}{\the\paperwidth}
      {color(0cm)=(#1); color(\the\paperheight)=(#2)}
    }
    ...
    
    \setbeamertemplate{background canvas}[my shading]{red!10}{blue!10}
    %% Defines the shading myshading right here. Subsequent calls to
    %% \usebeamertemplate{background canvas} will yield
    %% ``\pgfuseshading{myshading}''.
    

article

Normally, this command has no effect in article mode. However, if a ⟨ _mode specification_ ⟩ is given, this command is applied for the specified modes. Thus, this command behaves like the \\\ command, which also gets the implicit mode specification <presentation> if no other specification is given. 

_Example:_ \defbeamertemplate{my template}{default}{something} has no effect in article mode. 

_Example:_ \defbeamertemplate<article>{my template}{default}{something} has no effect in presentation modes, but has an effect in article mode. 

_Example:_ \defbeamertemplate<all>{my template}{default}{something} applies to all modes. 

It is often useful to have access to the same template option via different names. For this, you can use the following command to create aliases: 

`\defbeamertemplatealias`{⟨ _element name_ ⟩}{⟨ _new predefined option name_ ⟩}{⟨ _existing predefined option name_ ⟩} 

Causes the two predefined options to have the same effect.

There is no inheritance relation among templates as there is for colors and fonts. This is due to the fact the templates for one element seldom make sense for another. However, sometimes certain elements “behave similarly” and one would like a \setbeamertemplate to apply to a whole set of templates via inheritance. For example, one might want that \setbeamertemplate{items}[circle] causes all items to use the circle option, though the effects for the itemize item as opposed to the itemize subsubitem as opposed to enumerate item must be slightly different. 

The beamer-template mechanism implements a simple form of inheritance via _parent templates_. In element descriptions, parent templates are indicated via a check mark in parentheses. 

`\defbeamertemplateparent`{⟨ _parent template name_ ⟩}[⟨ _predefined option name_ ⟩]{⟨ _child template list_ ⟩}  
[⟨ _argument number_ ⟩][⟨ _default optional argument_ ⟩]{⟨ _arguments for children_ ⟩} 

The effect of this command is that whenever someone calls \setbeamertemplate{⟨ _parent template name_ ⟩}{⟨ _args_ ⟩}, the command \setbeamertemplate{⟨ _child template name_ ⟩}{⟨ _args_ ⟩} is called for each ⟨ _child template name_ ⟩ in the ⟨ _child template list_ ⟩. 

The ⟨ _arguments for children_ ⟩ come into play if the \setbeamertemplate command is called with a predefined option name (not necessarily the same as the ⟨ _predefined option name_ ⟩, we’ll come to that). If \setbeamertemplate is called with some predefined option name, the children are called with the ⟨ _arguments for children_ ⟩ instead. Let’s look at two examples: 

_Example:_ The following is the typical, simple usage:
    
    
    \defbeamertemplateparent{itemize items}{itemize item,itemize subitem,itemize subsubitem}
    {}
    
    %% The following command has the same effect as the three commands below:
    \setbeamertemplate{itemize items}[circle]
    
    \setbeamertemplate{itemize item}[circle] % actually, the ``empty'' argument is added
    \setbeamertemplate{itemize subitem}[circle]
    \setbeamertemplate{itemize subsubitem}[circle]
    

_Example:_ In the following case, an argument is passed to the children: 
    
    
    \defbeamertemplateparent{sections/subsections in toc shaded}
    {section in toc shaded,subsection in toc shaded}[1][20]
    {[#1]}
    
    %% The following command has the same effect as the two commands below:
    \setbeamertemplate{sections/subsections in toc shaded}[default][35]
    
    \setbeamertemplate{section in toc shaded}[default][35]
    \setbeamertemplate{subsection in toc shaded}[default][35]
    
    
    
    %% Again:
    \setbeamertemplate{sections/subsections in toc shaded}[default]
    
    \setbeamertemplate{section in toc shaded}[default][20]
    \setbeamertemplate{subsection in toc shaded}[default][20]
    

In detail, the following happens: When \setbeamertemplate is encountered for a parent template, beamer first checks whether a predefined option follows. If not, a single argument is read and \setbeamertemplate is called for all children for this template. If there is a predefined template option set, beamer evaluates the ⟨ _argument for children_ ⟩. It may contain parameters like #1 or #2. These parameters are filled with the arguments that follow the call of \setbeamertemplate for the parent template. The number of arguments must be the number given as ⟨ _argument number_ ⟩. An optional argument can also be specified in the usual way. Once the ⟨ _arguments for the children_ ⟩ have been computed, \setbeamertemplate is called for all children for the predefined template and with the computed arguments. 

You may wonder what happens when certain predefined options take a certain number of arguments, but another predefined option takes a different number of arguments. In this case, the above-described mechanism cannot differentiate between the predefined options and it is unclear which or even how many arguments should be contained in ⟨ _arguments for children_ ⟩. For this reason, you can give the optional argument ⟨ _predefined option name_ ⟩ when calling \defbeamertemplateparent. If this optional argument is specified, the parenthood of the template applies only to this particular ⟨ _predefined option name_ ⟩. Thus, if someone calls \setbeamertemplate for this ⟨ _predefined option name_ ⟩, the given ⟨ _argument for children_ ⟩ is used. For other predefined option names a possibly different definition is used. You can imaging that leaving out the optional ⟨ _predefined option name_ ⟩ means “this ⟨ _argument for children_ ⟩ applies to all predefined option names that have not been specially defined differently.” 
