## Changing the Way Things Look

####  18 Fonts 

The first subsection introduces the predefined font themes that come with beamer and which make it easy to change the fonts used in a presentation. The next subsection describes further special commands for changing some basic attributes of the fonts used in a presentation. The last subsection explains how you can get a much more fine-grained control over the fonts used for every individual element of a presentation. 

#####  18.1 Font Themes¶

beamer comes with a set of font themes. When you use such a theme, certain fonts are changed as described below. You can use several font themes in concert. For historical reasons, you cannot change all aspects of the fonts used using font themes—in some cases special commands and options are needed, which are described in the next subsection. 

The following font themes only change certain font attributes, they do not choose special font families (although that would also be possible and themes doing just that might be added in the future). Currently, to change the font family, you need to load special packages as explained in the next subsection. 

\usefonttheme{default}

_Example:_

The default font theme installs a sans serif font for all text of the presentation. The default theme installs different font sizes for things like titles or head- and footlines, but does not use boldface or italics for “highlighting.” To change some or all text to a serif font, use the serif theme. 

_Note:_ The command \mathrm will always produce upright (not slanted), serif text and the command \mathsf will always produce upright, sans-serif text. The command \mathbf will produce upright, bold-face, sans-serif or serif text, depending on whether mathsans or mathserif is used. 

To produce an upright, sans-serif or serif text, depending on whether mathsans or mathserif is used, you can use for instance the command \operatorname from the amsmath package. Using this command instead of \mathrm or \mathsf directly will automatically adjust upright mathematical text if you switch from sans-serif to serif or back. 

  * \usefonttheme{professionalfonts}

This font theme does not really change any fonts. Rather, it _suppresses_ certain internal replacements performed by beamer. If you use “professional fonts” (fonts that you buy and that come with a complete set of every symbol in all modes), you do not want beamer to meddle with the fonts you use. beamer normally replaces certain character glyphs in mathematical text by more appropriate versions. For example, beamer will normally replace glyphs such that the italic characters from the main font are used for variables in mathematical text. If your professional font package takes care of this already, beamer’s meddling should be switched off. Note that beamer’s substitution is automatically turned off if one of the following packages is loaded: arevmath, hvmath, kpfonts, lmodern, lucidabr, lucimatx, mathastext, mathpmnt, mathpple, mathtime, mtpro, and mtpro2. It is also turned off when unicode-math is loaded for the use of Unicode math fonts. If your favorite professional font package is not among these, use the professionalfonts theme (and open an issue in our github bug tracker, so that the package can be added). 




\usefonttheme[⟨ _options_ ⟩]{serif}

_Example:_

This theme causes all text to be typeset using the default serif font (except if you specify certain ⟨ _options_ ⟩). You might wish to consult Section [5.6.2](<Guidelines-Creating-Presentations.html#section-guidelines-serif>) on whether you should use serif fonts. 

The following ⟨ _options_ ⟩ may be given: 

  * • stillsansserifmath causes mathematical text still to be typeset using sans serif. This option only makes sense if you also use the stillsansseriftext option since sans serif math inside serif text looks silly. 

  * • stillsansserifsmall will cause “small” text to be still typeset using sans serif. This refers to the text in the headline, footline, and sidebars. Using this option is often advisable since small text is often easier to read in sans serif. 

  * • stillsansseriflarge will cause “large” text like the presentation title or the frame title to be still typeset using sans serif. Sans serif titles with serif text are a popular combination in typography. 

  * • stillsansseriftext will cause normal text (none of the above three) to be still typeset using sans serif. If you use this option, you should most likely also use the first two. However, by not using stillsansseriflarge, you get a serif (possibly italic) title over a sans serif text. This can be an interesting visual effect. Naturally, “interesting typographic effect” can mean “terrible typographic effect” if you choose the wrong fonts combinations or sizes. You’ll need some typographic experience to judge this correctly. If in doubt, try asking someone who should know. 

  * • onlymath is a short-cut for selecting all of the above options except for the first. Thus, using this option causes only mathematical text to by typeset using a serif font. Recall that, by default, mathematical formulas are also typeset using sans-serif letters. In most cases, this is visually the most pleasing and easily readable way of typesetting mathematical formulas if the surrounding text is typeset using sans serif. However, in mathematical texts the font used to render, say, a variable is sometimes used to differentiate between different meanings of this variable. In such case, it may be necessary to typeset mathematical text using serif letters. Also, if you have a lot of mathematical text, the audience may be quicker to “parse” it if it is typeset the way people usually read mathematical text: in a serif font. 




\usefonttheme[⟨ _options_ ⟩]{structurebold}

_Example:_

This font theme will cause titles and text in the headlines, footlines, and sidebars to be typeset in a bold font. 

The following ⟨ _options_ ⟩ may be given: 

  * • onlysmall will cause only “small” text to be typeset in bold. More precisely, only the text in the headline, footline, and sidebars is changed to be typeset in bold. Large titles are not affected. 

  * • onlylarge will cause only “large” text to be typeset in bold. These are the main title, frame titles, and section entries in the table of contents. 




As pointed out in Section [5.6.1](<Guidelines-Creating-Presentations.html#section-sizes>), you should use this theme (possibly with the onlysmall option) if your font is not scaled down properly or for light-on-dark text. 

The normal themes do not install this theme by default, while the old compatibility themes do. Since you can reload the theme once it has been loaded, you cannot use this theme with the old compatibility themes to set also titles to a bold font. 

\usefonttheme[⟨ _options_ ⟩]{structureitalicserif}

_Example:_

This theme is similarly as the structurebold font theme, but where structurebold makes text bold, this theme typesets it in italics and in the standard serif font. The same ⟨ _options_ ⟩ as for the structurebold theme are supported. See Section [5.6.3](<Guidelines-Creating-Presentations.html#section-italics>) for the pros and cons of using italics. 

\usefonttheme[⟨ _options_ ⟩]{structuresmallcapsserif}

_Example:_

Again, this theme does exactly the same as the structurebold font theme, only this time text is set using small caps and a serif font. The same ⟨ _options_ ⟩ as for the structurebold theme are supported. See Section [5.6.3](<Guidelines-Creating-Presentations.html#section-smallcaps>) for the pros and cons of using small caps. 

#####  18.2 Font Changes Made Without Using Font Themes¶

While most font decisions can be made using font themes, for historical reasons some changes can only be made using class options or by loading special packages. These options are explained in the following. Possibly, these options will be replaced by themes in the future. 

######  18.2.1 Choosing a Font Size for Normal Text¶

As pointed out in Section [5.6.1](<Guidelines-Creating-Presentations.html#section-sizes>), measuring the default font size in points is not really a good idea for presentations. Nevertheless, beamer does just that, setting the default font size to 11pt as usual. This may seem ridiculously small, but the actual size of each frame size is by default just 128mm by 96mm and the viewer application enlarges the font. By specifying a default font size smaller than 11pt you can put more onto each slide, by specifying a larger font size you can fit on less. 

To specify the font size, you can use the following class options: 

\documentclass[8pt]{beamer}

This is way too small. Requires that the package extsizes is installed. 

\documentclass[9pt]{beamer}

This is also too small. Requires that the package extsizes is installed. 

\documentclass[10pt]{beamer}

If you really need to fit more onto each frame, use this option. Works without extsizes. 

\documentclass[smaller]{beamer} 

Same as the 10pt option.

\documentclass[11pt]{beamer}

The default font size. You need not specify this option.

\documentclass[12pt]{beamer}

Makes all fonts a little bigger, which makes the text more readable. The downside is that less fits onto each frame. 

\documentclass[bigger]{beamer}

Same as the 12pt option.

\documentclass[14pt]{beamer}

Makes all fonts somewhat bigger. Requires extsizes to be installed. 

\documentclass[17pt]{beamer}

This is about the default size of PowerPoint and OpenOffice.org Impress. Requires extsizes to be installed. 

\documentclass[20pt]{beamer}

This is really huge. Requires extsizes to be installed. 

######  18.2.2 Choosing a Font Family¶

By default, beamer uses the Computer Modern fonts. To change this, you can use one of the prepared packages of LaTeX’s font mechanism. For example, to change to Times/Helvetica, simply add 
    
    
    \usepackage{mathptmx}
    \usepackage{helvet}
    

in your preamble. Note that if you do not use the serif font theme, Helvetica (not Times) will be selected as the text font. 

There may be many other fonts available on your installation. Typically, at least some of the following packages should be available: arev, avant, bookman, chancery, charter, euler, helvet, lmodern, mathtime, mathptm, mathptmx, newcent, palatino, pifont, utopia. 

######  18.2.3 Choosing a Font Encodings¶

The same font can come in different encodings, which are (very roughly spoken) the ways the characters of a text are mapped to glyphs (the actual shape of a particular character in a particular font at a particular size). In TeX two encodings are often used with Latin characters: the T1 encoding and the OT1 encoding (old T1 encoding). 

Conceptually, the newer T1 encoding is preferable over the old OT1 encoding. For example, hyphenation of words containing umlauts (like the famous German word Fräulein) will work only if you use the T1 encoding. Unfortunately, the EC fonts, that is, the T1-encoded Computer Modern fonts, are distributed on small installations just as MetaFont sources and only have bitmap renditions of each glyph. For this reason, using the T1-encoded EC fonts on such small installations will produce pdf files that render poorly. 

TeX Live (cross-platform; replaced older `teTeX` for unix/Linux) and MiKTeX (for Windows platforms) can be installed with different levels of completeness. Concerning the Computer Modern fonts, the following packages can be installed: cm-super fonts, lmodern (Latin Modern) fonts, and lgc fonts, the latter containing the Latin, Greek, and Cyrillic alphabets. Concerning other fonts, the txfonts and pxfonts are two extended sets of the Times and the Palatino PostScript fonts, both packages containing extended sets of mathematical glyphs. Most other standard PostScript fonts are also available in T1 encoding. 

Among the packages that make available the Computer Modern fonts in the T1 encoding, the package lmodern may be suggested. If you use lmodern, several extra fonts become available (like a sans-serif boldface math) and extra symbols (like proper guillemots). 

To select the T1 encoding, use \usepackage[T1]{fontenc}. Thus, if you have the LM fonts installed, you could write 
    
    
    \usepackage[T1]{fontenc}
    \usepackage{lmodern}
    

to get beautiful outline fonts and correct hyphenation. Note, however, that certain older versions of the LM bundle did not include correct glyphs for ligatures like “fi,” which may cause trouble. Double check that all ligatures are displayed correctly and, if not, update your installation. 

Everything mentioned above applies to pdflatex and latex+dvips. Unlike those engines, xelatex and lualatex support OpenType fonts, and that means that you can use system fonts in your documents relatively easy. Details will eventually be documented in this manual. For now, you can take a look at the documentation for the fontspec package which supports both engines. Also, note that when you use lualatex or xelatex with TU encoding, respectively, by default you get OpenType Latin Modern fonts. 

#####  18.3 Changing the Fonts Used for Different Elements of a Presentation¶

This section explains how beamer’s font management works. 

######  18.3.1 Overview of Beamer’s Font Management¶

beamer’s font mechanism is somewhat similar to beamer’s color mechanism, but not quite the same. Similar to colors, every beamer element, like the frame titles, the document title, the footnotes, and so on has a certain beamer-font. Similar to colors, on the one hand you can specify the font of each element individually; on the other hand fonts also use inheritance, thereby making it easy to globally change the fonts used for, say, “titlelike things” or for “itemizelike things.” 

While a beamer-color has a certain foreground and a certain background, either of which may be empty, a beamer-font has a size, a shape, a series, and a family, each of which may be empty. The inheritance relation among beamer-fonts is not necessarily the same as between beamer-colors, though we have tried to match them whenever possible. 

Multiple inheritance plays a more important rule for fonts than it does for colors. A font might inherit the attributes of two different fonts. If one of them specifies that the font should be, say, boldface and the other specifies that the font should be, say, large, then the child font will be both large and bold. 

As for fonts, the description of the font used for an element is given after the description of the element. 

######  18.3.2 Using Beamer’s Fonts¶

To use a beamer-font, you can use the command \usebeamerfont. Inside the templates for elements, this command will (typically) have already been called for you, so you will only seldomly have to use this command. 

`\usebeamerfont`*{⟨ _beamer-font name_ ⟩} 

This command changes the current font to the font specified by the ⟨ _beamer-font name_ ⟩. The ⟨ _beamer-font name_ ⟩ can be a not-too-fancyful text and may contain spaces. Typical examples are frametitle or section in toc or My Font 1. beamer-fonts can have (and should) have the same name as beamer-templates and beamer-colors. 

_Example:_ \usebeamerfont{frametitle} In the unstarred version of this command, the font is changed according to the attributes specified in the ⟨ _beamer-font name_ ⟩, but unspecified attributes remain unchanged. For example, if the font specifies that the font should be “bold,” but specifies nothing else, and if the current font is large, then \usebeamerfont causes the current font to become large and bold. 

In the starred version of this command, the font is first reset before the font’s attributes are applied. Thus, in the above example of a beamer-font having only the attribute “boldface” set, saying \usebeamerfont* will _always_ cause the current font to become a normal-shape, bold, default-family font (the font size won’t be reset). 

######  18.3.3 Setting Beamer’s Fonts¶

As for beamer-colors, there exists a central command for setting and changing beamer-fonts. 

`\setbeamerfont`*{⟨ _beamer-font name_ ⟩}{⟨ _attributes_ ⟩} 

This command sets or resets certain attributes of the beamer-font ⟨ _beamer-font name_ ⟩. In the unstarred version, this command just adds those attributes that have not been mentioned in a previous call and overwrites those that have been mentioned. Thus, the following two command blocks have the same effect: 

_Example:_
    
    
    \setbeamerfont{frametitle}{size=\large}
    \setbeamerfont{frametitle}{series=\bfseries}
    
    \setbeamerfont{frametitle}{size=\large,series=\bfseries}
    

In the starred version, the font attributes are first completely reset, that is, set to be empty. 

The following ⟨ _attributes_ ⟩ may be given: 

  * • size=⟨ _size command_ ⟩ sets the size attribute of the beamer font. The ⟨ _size command_ ⟩ should be a normal LaTeX-command used for setting the font size or it should be empty. Useful commands include \tiny, \scriptsize, \footnotesize, \small, \normalsize, \large, \Large, \huge, and \Huge. beamer also introduces the two font sizes \Tiny and \TINY for _really_ small text. But you should know _exactly_ what you are doing if you use them. You have been warned. 

Note that there is a difference between specifying an empty command and specifying \normalsize: Making the size attribute “empty” means that the font size should not be changed when this font is used, while specifying \normalsize means that the size should be set to the normal size whenever this font is used. 

  * • size*={⟨ _size in pt_ ⟩}{⟨ _baselineskip_ ⟩} sets the size attribute of the font to the given ⟨ _size in pt_ ⟩ and the baseline skip to the given value. Note that, depending on what kind of font you use, not all font sizes may be available. Also, certain font sizes are much less desirable than other ones; the standard commands take care of choosing appropriate sizes for you. Do not use this option unless you have a good reason. This command has the same effect as size={\fontsize{⟨ _size in pt_ ⟩}{⟨ _baselineskip_ ⟩}}. 

  * • shape=⟨ _shape command_ ⟩ sets the shape attribute of the font. The command should be a command like \itshape, \slshape, \scshape, or \upshape. 

  * • shape*={⟨ _shape attribute abbreviation_ ⟩} sets the shape attribute of the font using the LaTeX’s abbreviations for attributes. This command has the same effect as shape={\fontshape{⟨ _shape attributes abbreviation_ ⟩}}. 

  * • series=⟨ _series command_ ⟩ sets the “series” attribute of the font. The command should be a command like \bfseries. 

  * • series*={⟨ _series attribute abbreviation_ ⟩} has the same effect as series={\fontseries{⟨ _series attributes abbreviation_ ⟩}}. 

  * • family=⟨ _family command_ ⟩ sets the font family attribute. The command should be a LaTeX-font command like \rmfamily or \sffamily. 

  * • family*={⟨ _family name_ ⟩} sets the font family attribute to the given ⟨ _family name_ ⟩. The command has the same effect as family={\fontfamily{⟨ _family name_ ⟩}}. The ⟨ _family name_ ⟩ is, normally, a somewhat cryptic abbreviation of a font family name that installed somewhere on the system. For example, the ⟨ _family name_ ⟩ for Times happens to be ptm. No one can remember these names, so it’s perfectly normal if you have to look them up laboriously. 

  * • parent={⟨ _parent list_ ⟩} specifies a list of parent fonts. When the beamer-font is used, the parents are used first. Thus, any font attributes set by one of the parents is inherited by the beamer-font, except if this attribute is overwritten by the font. 




_Example:_
    
    
    \setbeamerfont{parent A}{size=\large}
    \setbeamerfont{parent B}{series=\bfseries}
    \setbeamerfont{child}{parent={parent A, parent B},size=\small}
    
    \normalfont
    This text is in a normal font.
    \usebeamerfont{parent A}
    This text is large.
    \usebeamerfont{parent B}
    This text is large and bold.
    \usebeamerfont{parent B}
    This text is still large and bold.
    \usebeamerfont*{parent B}
    This text is only bold, but not large.
    \usebeamerfont{child}
    This text is small and bold.
    
