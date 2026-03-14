## Changing the Way Things Look

####  15 Themes 

#####  15.1 Five Flavors of Themes¶

_Themes_ make it easy to change the appearance of a presentation. The beamer class uses five different kinds of themes: 

Presentation Themes
    

Conceptually, a presentation theme dictates for every single detail of a presentation what it looks like. Thus, choosing a particular presentation theme will setup for, say, the numbers in enumeration what color they have, what color their background has, what font is used to render them, whether a circle or ball or rectangle or whatever is drawn behind them, and so forth. Thus, when you choose a presentation theme, your presentation will look the way someone (the creator of the theme) thought that a presentation should look like. Presentation themes typically only choose a particular color theme, font theme, inner theme, and outer theme that go well together. 

Color Themes
    

A color theme only dictates which colors are used in a presentation. If you have chosen a particular presentation theme and then choose a color theme, only the colors of your presentation will change. A color theme can specify colors in a very detailed way: For example, a color theme can specifically change the colors used to render, say, the border of a button, the background of a button, and the text on a button. 

Font Themes
    

A font theme dictates which fonts or font attributes are used in a presentation. Similar to colors, the font of all text elements used in a presentation can be specified independently. 

Inner Themes
    

An inner theme specifies how certain elements of a presentation are typeset. This includes all elements that are at the “inside” of the frame, that is, that are not part of the headline, footline, or sidebars. This includes all enumerations, itemize environments, block environments, theorem environments, or the table of contents. For example, an inner theme might specify that in an enumeration the number should be typeset without a dot and that a small circle should be shown behind it. The inner theme would _not_ specify what color should be used for the number or the circle (this is the job of the color theme) nor which font should be used (this is the job of the font theme). 

Outer Themes
    

An outer theme specifies what the “outside” or “border” of the presentation slides should look like. It specifies whether there are head- and footlines, what is shown in them, whether there is a sidebar, where the logo goes, where the navigation symbols and bars go, and so on. It also specifies where the frametitle is put and how it is typeset. 

The different themes reside in the five subdirectories theme, color, font, inner, and outer of the directory beamer/themes. Internally, a theme is stored as a normal style file. However, to use a theme, the following special commands should be used: 

`\usetheme`[⟨ _options_ ⟩]{⟨ _name list_ ⟩} 

Installs the presentation theme named ⟨ _name_ ⟩. Currently, the effect of this command is the same as saying \usepackage for the style file named beamertheme⟨ _name_ ⟩.sty for each ⟨ _name_ ⟩ in the ⟨ _name list_ ⟩. 

`\usecolortheme`[⟨ _options_ ⟩]{⟨ _name list_ ⟩} 

Same as \usetheme, only for color themes. Color style files are named beamercolortheme⟨ _name_ ⟩.sty. 

`\usefonttheme`[⟨ _options_ ⟩]{⟨ _name_ ⟩} 

Same as \usetheme, only for font themes. Font style files are named beamerfonttheme⟨ _name_ ⟩.sty. 

`\useinnertheme`[⟨ _options_ ⟩]{⟨ _name_ ⟩} 

Same as \usetheme, only for inner themes. Inner style files are named beamerinnertheme⟨ _name_ ⟩.sty. 

`\useoutertheme`[⟨ _options_ ⟩]{⟨ _name_ ⟩} 

Same as \usetheme, only for outer themes. Outer style files are named beameroutertheme⟨ _name_ ⟩.sty. 

If you do not use any of these commands, a sober _default_ theme is used for all of them. In the following, the presentation themes that come with the beamer class are described. The element, layout, color, and font themes are presented in the following sections. 

#####  15.2 Presentation Themes without Navigation Bars¶

A presentation theme dictates for every single detail of a presentation what it looks like. Normally, having chosen a particular presentation theme, you do not need to specify anything else having to do with the appearance of your presentation—the creator of the theme should have taken care of that for you. However, you still _can_ change things afterward either by using a different color, font, element, or even layout theme; or by changing specific colors, fonts, or templates directly. 

When Till started naming the presentation themes, he soon ran out of ideas on how to call them. Instead of giving them more and more cumbersome names, he decided to switch to a different naming convention: Except for two special cases, all presentation themes are named after cities. These cities happen to be cities in which or near which there was a conference or workshop that he attended or that a co-author of his attended. 

All themes listed without author mentioned were developed by Till. If a theme has not been developed by us (that is, if someone else is to blame), this is indicated with the theme. We have sometimes slightly changed or “corrected” submitted themes, but we still list the original authors. 

\usetheme{default}

_Example:_

As the name suggests, this theme is installed by default. It is a sober no-nonsense theme that makes minimal use of color or font variations. This theme is useful for all kinds of talks, except for very long talks. 

\usetheme[headheight=⟨ _head height_ ⟩,footheight=⟨ _foot height_ ⟩]{boxes}

_Example:_

For this theme, you can specify an arbitrary number of templates for the boxes in the headline and in the footline. You can add a template for another box by using the following commands. 

`\addheadbox`{⟨ _beamer color_ ⟩}{⟨ _box template_ ⟩} 

Each time this command is invoked, a new box is added to the head line, with the first added box being shown on the left. All boxes will have the same size. 

The ⟨ _beamer color_ ⟩ will be used to setup the foreground and background colors of the box. 

_Example:_
    
    
    \addheadbox{section in head/foot}{\tiny\quad 1. Box}
    \addheadbox{structure}{\tiny\quad 2. Box}
    

A similar effect as the above commands can be achieved by directly installing a head template that contains two beamercolorboxes: 
    
    
    \setbeamertemplate{headline}
    {\leavevmode
    \begin{beamercolorbox}[width=.5\paperwidth]{section in head/foot}
      \tiny\quad 1. Box
    \end{beamercolorbox}%
    \begin{beamercolorbox}[width=.5\paperwidth]{structure}
      \tiny\quad 2. Box
    \end{beamercolorbox}
    }
    

While being more complicated, the above commands offer more flexibility. 

`\addfootbox`{⟨ _beamer color_ ⟩}{⟨ _box template_ ⟩} 

_Example:_
    
    
    \addfootbox{section in head/foot}{\tiny\quad 1. Box}
    \addfootbox{structure}{\tiny\quad 2. Box}
    

\usetheme[⟨ _options_ ⟩]{Bergen}

_Example:_

A theme based on the inmargin inner theme and the rectangles inner theme. Using this theme is not quite trivial since getting the spacing right can be trickier than with most other themes. Also, this theme goes badly with columns. You may wish to consult the remarks on the inmargin inner theme. 

Bergen is a town in Norway. It hosted iwpec 2004\. 

\usetheme[⟨ _options_ ⟩]{Boadilla}

_Example:_

A theme giving much information in little space. The following ⟨ _options_ ⟩ may be given: 

  * • secheader causes a headline to be inserted showing the current section and subsection. By default, this headline is not shown. 




_Theme author:_ Manuel Carro. Boadilla is a village in the vicinity of Madrid, hosting the University’s Computer Science department. 

\usetheme[⟨ _options_ ⟩]{Madrid}

_Example:_

Like the Boadilla theme, except that stronger colors are used and that the itemize icons are not modified. The same ⟨ _options_ ⟩ as for the Boadilla theme may be given. 

_Theme author:_ Manuel Carro. Madrid is the capital of Spain. 

\usetheme{AnnArbor}

_Example:_

Like Boadilla, but using the colors of the University of Michigan. 

_Theme author:_ Madhusudan Singh. The University of Michigan is located at Ann Arbor. 

\usetheme{CambridgeUS}

_Example:_

Like Boadilla, but using the colors of MIT. 

_Theme author:_ Madhusudan Singh.

\usetheme{EastLansing}

_Example:_

Like Boadilla, but using the colors of Michigan State University. 

_Theme author:_ Alan Munn. Michigan State University is located in East Lansing. 

\usetheme{Pittsburgh}

_Example:_

A sober theme. The right-flushed frame titles creates an interesting “tension” inside each frame. 

Pittsburgh is a town in the eastern USA. It hosted the second recomb workshop of snps and haplotypes, 2004. 

\usetheme[⟨ _options_ ⟩]{Rochester}

_Example:_

A dominant theme without any navigational elements. It can be made less dominant by using a different color theme. 

The following ⟨ _options_ ⟩ may be given: 

  * • height=⟨ _dimension_ ⟩ sets the height of the frame title bar. 




Rochester is a town in upstate New York, USA. Till visited Rochester in 2001. 

#####  15.3 Presentation Themes with a Tree-Like Navigation Bar¶

\usetheme{Antibes}

_Example:_

A dominant theme with a tree-like navigation at the top. The rectangular elements mirror the rectangular navigation at the top. The theme can be made less dominant by using a different color theme. 

Antibes is a town in the south of France. It hosted stacs 2002\. 

\usetheme{JuanLesPins}

_Example:_

A variation on the Antibes theme that has a much “smoother” appearance. It can be made less dominant by choosing a different color theme. 

Juan–Les–Pins is a cozy village near Antibes. It hosted stacs 2002\. 

\usetheme{Montpellier}

_Example:_

A sober theme giving basic navigational hints. The headline can be made more dominant by using a different color theme. 

Montpellier is in the south of France. It hosted stacs 2004\. 

#####  15.4 Presentation Themes with a Table of Contents Sidebar¶

\usetheme[⟨ _options_ ⟩]{Berkeley}

_Example:_

A dominant theme. If the navigation bar is on the left, it dominates since it is seen first. The height of the frame title is fixed to two and a half lines, thus you should be careful with overly long titles. A logo will be put in the corner area. Rectangular areas dominate the layout. The theme can be made less dominant by using a different color theme. 

By default, the current entry of the table of contents in the sidebar will be highlighted by using a more vibrant color. A good alternative is to highlight the current entry by using a different color for the background of the current point. The color theme sidebartab installs the appropriate colors, so you just have to say 
    
    
    \usecolortheme{sidebartab}
    

This color theme works with all themes that show a table of contents in the sidebar. 

This theme is useful for long talks like lectures that require a table of contents to be visible all the time. 

The following ⟨ _options_ ⟩ may be given: 

  * • hideallsubsections causes only sections to be shown in the sidebar. This is useful, if you need to save space. 

  * • hideothersubsections causes only the subsections of the current section to be shown. This is useful, if you need to save space. 

  * • left puts the sidebar on the left (default). 

  * • right puts the sidebar on the right. 

  * • width=⟨ _dimension_ ⟩ sets the width of the sidebar. If set to zero, no sidebar is created. 




Berkeley is on the western coast of the USA, near San Francisco. Till visited Berkeley for a year in 2004. 

\usetheme[⟨ _options_ ⟩]{PaloAlto}

_Example:_

A variation on the Berkeley theme with less dominance of rectangular areas. The same ⟨ _options_ ⟩ as for the Berkeley theme can be given. 

Palo Alto is also near San Francisco. It hosted the Bay Area Theory Workshop 2004. 

\usetheme[⟨ _options_ ⟩]{Goettingen}

_Example:_

A relatively sober theme useful for a longer talk that demands a sidebar with a full table of contents. The same ⟨ _options_ ⟩ as for the Berkeley theme can be given. 

Göttingen is a town in Germany. It hosted the 42nd Theorietag. 

\usetheme[⟨ _options_ ⟩]{Marburg}

_Example:_

A very dominant variation of the Goettingen theme. The same ⟨ _options_ ⟩ may be given. 

Marburg is a town in Germany. It hosted the 46th Theorietag.

\usetheme[⟨ _options_ ⟩]{Hannover}

_Example:_

In this theme, the sidebar on the left is balanced by right-flushed frame titles. 

The following ⟨ _options_ ⟩ may be given: 

  * • hideallsubsections causes only sections to be shown in the sidebar. This is useful, if you need to save space. 

  * • hideothersubsections causes only the subsections of the current section to be shown. This is useful, if you need to save space. 

  * • width=⟨ _dimension_ ⟩ sets the width of the sidebar. 




Hannover is a town in Germany. It hosted the 48th Theorietag.

#####  15.5 Presentation Themes with a Mini Frame Navigation¶

\usetheme[⟨ _options_ ⟩]{Berlin}

_Example:_

A dominant theme with strong colors and dominating rectangular areas. The head- and footlines give lots of information and leave little space for the actual slide contents. This theme is useful for conferences where the audience is not likely to know the title of the talk or who is presenting it. The theme can be made less dominant by using a different color theme. 

The following ⟨ _options_ ⟩ may be given: 

  * • compress causes the mini frames in the headline to use only a single line. This is useful for saving space. 




Berlin is the capital of Germany.

\usetheme[⟨ _options_ ⟩]{Ilmenau}

_Example:_

A variation on the Berlin theme. The same ⟨ _options_ ⟩ may be given. 

Ilmenau is a town in Germany. It hosted the 40th Theorietag.

\usetheme{Dresden}

_Example:_

A variation on the Berlin theme with a strong separation into navigational stuff at the top/bottom and a sober main text. The same ⟨ _options_ ⟩ may be given. 

Dresden is a town in Germany. It hosted STACS 2001.

\usetheme{Darmstadt}

_Example:_

A theme with a strong separation into a navigational upper part and an informational main part. By using a different color theme, this separation can be lessened. 

Darmstadt is a town in Germany.

\usetheme{Frankfurt}

_Example:_

A variation on the Darmstadt theme that is slightly less cluttered by leaving out the subsection information. 

Frankfurt is a town in Germany.

\usetheme{Singapore}

_Example:_

A not-too-sober theme with navigation that does not dominate.

Singapore is located in south-eastern Asia. It hosted cocoon 2002\. 

\usetheme{Szeged}

_Example:_

A sober theme with a strong dominance of horizontal lines.

Szeged is on the south border of Hungary. It hosted dlt 2003\. 

#####  15.6 Presentation Themes with Section and Subsection Tables¶

\usetheme{Copenhagen}

_Example:_

A not-quite-too-dominant theme. This theme gives compressed information about the current section and subsection at the top and about the title and the author at the bottom. No shadows are used, giving the presentation a “flat” look. The theme can be made less dominant by using a different color theme. 

Copenhagen is the capital of Denmark. It is connected to Malmö by the Øresund bridge. 

\usetheme{Luebeck}

_Example:_

A variation on the Copenhagen theme. 

Lübeck is a town in northern Germany. It hosted the 41st Theorietag. 

\usetheme{Malmoe}

_Example:_

A more sober variation of the Copenhagen theme. 

Malmö is a town in southern Sweden. It hosted fct 2001\. 

\usetheme{Warsaw}

_Example:_

A dominant variation of the Copenhagen theme. 

Warsaw is the capital of Poland. It hosted mfcs 2002\. 

#####  15.7 Presentation Themes Included For Compatibility¶

Earlier versions of beamer included some further themes. These themes are still available for compatibility, though they are now implemented differently (they also mainly install appropriate color, font, inner, and outer themes). However, they may or may not honor color themes and they will not be supported in the future. The following list shows which of the new themes should be used instead of the old themes. (When switching, you may want to use the font theme structurebold with the option onlysmall.) 

.  
---  
Old theme |  Replacement options  
none |  Use compatibility.  
bars |  Try Dresden instead.  
classic |  Try Singapore instead.  
lined |  Try Szeged instead.  
plain |  Try none or Pittsburgh instead.  
sidebar |  Try Goettingen for the light version and Marburg for the dark version.   
shadow |  Try Warsaw instead.  
split |  Try Malmoe instead.  
tree |  Try Montpellier and, for the bars version, Antibes or JuansLesPins. 
