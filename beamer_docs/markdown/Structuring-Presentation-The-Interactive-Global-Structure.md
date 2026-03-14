## Building a Presentation

####  11 Structuring a Presentation: The Interactive Global Structure 

#####  11.1 Adding Hyperlinks and Buttons¶

To create anticipated nonlinear jumps in your talk structure, you can add hyperlinks to your presentation. A hyperlink is a text (usually rendered as a button) that, when you click on it, jumps the presentation to some other slide. Creating such a button is a three-step process: 

  * 1. You specify a target using the command \hypertarget or (easier) the command \label. In some cases, see below, this step may be skipped. 

  * 2. You render the button using \beamerbutton or a similar command. This will _render_ the button, but clicking it will not yet have any effect. 

  * 3. You put the button inside a \hyperlink command. Now clicking it will jump to the target of the link. 




`\hypertarget`<⟨ _overlay specification_ ⟩>{⟨ _target name_ ⟩}{⟨ _text_ ⟩} 

If the ⟨ _overlay specification_ ⟩ is present, the ⟨ _text_ ⟩ is the target for hyper jumps to ⟨ _target name_ ⟩ only on the specified slide. On all other slides, the text is shown normally. Note that you _must_ add an overlay specification to the \hypertarget command whenever you use it on frames that have multiple slides (otherwise pdflatex rightfully complains that you have defined the same target on different slides). 

_Example:_
    
    
    \begin{frame}
      \begin{itemize}
      \item<1-> First item.
      \item<2-> Second item.
      \item<3-> Third item.
      \end{itemize}
    
      \hyperlink{jumptosecond}{\beamergotobutton{Jump to second slide}}
      \hypertarget<2>{jumptosecond}{}
    \end{frame}
    

article

You must say \usepackage[hyperref]{beamerarticle} or \usepackage{hyperref} in your preamble to use this command in article mode. 

The \label command creates a hypertarget as a side-effect and the label=⟨ _name_ ⟩ option of the \frame command creates a label named ⟨ _name_ ⟩<⟨ _slide number_ ⟩> for each slide of the frame as a side-effect. Thus the above example could be written more easily as: 
    
    
    \begin{frame}[label=threeitems]
      \begin{itemize}
      \item<1-> First item.
      \item<2-> Second item.
      \item<3-> Third item.
      \end{itemize}
    
      \hyperlink{threeitems<2>}{\beamergotobutton{Jump to second slide}}
    \end{frame}
    

The following commands can be used to specify in an abstract way what a button will be used for. 

`\beamerbutton`{⟨ _button text_ ⟩} 

Draws a button with the given ⟨ _button text_ ⟩. 

_Example:_ \hyperlink{somewhere}{\beamerbutton{Go somewhere}}

article

This command (and the following) just insert their argument in article mode. 

**Beamer-Template/-Color/-Font** button

When the \beamerbutton command is called, this template is used to render the button. Inside the template you can use the command \insertbuttontext to insert the argument that was passed to \beamerbutton. 

The following template options are predefined:

  * • `[default]` Typesets the button with rounded corners. The fore- and background of the beamer-color button are used and also the beamer-font button. The border of the button gets the foreground of the beamer-color button border. 




The following inserts are useful for this element:

  * • `\insertbuttontext` inserts the text of the current button. Inside “Goto-Buttons” (see below) this text is prefixed by the insert \insertgotosymbol and similarly for skip and return buttons. 

  * • `\insertgotosymbol` This text is inserted at the beginning of goto buttons. Redefine this command to change the symbol. 

_Example:_ \renewcommand{\insertgotosymbol}{\somearrowcommand}

  * • `\insertskipsymbol` This text is inserted at the beginning of skip buttons. 

  * • `\insertreturnsymbol` This text is inserted at the beginning of return buttons. 




**Beamer-Color** button border

The foreground of this color is used to render the border of buttons. 

`\beamergotobutton`{⟨ _button text_ ⟩} 

Draws a button with the given ⟨ _button text_ ⟩. Before the text, a small symbol (usually a right-pointing arrow) is inserted that indicates that pressing this button will jump to another “area” of the presentation. 

_Example:_ \hyperlink{detour}{\beamergotobutton{Go to detour}}

`\beamerskipbutton`{⟨ _button text_ ⟩} 

The symbol drawn for this button is usually a double right arrow. Use this button if pressing it will skip over a well-defined part of your talk. 

_Example:_
    
    
    \begin{frame}
      \begin{theorem}
        ...
      \end{theorem}
    
      \begin{overprint}
      \onslide<1>
        \hfill\hyperlinkframestartnext{\beamerskipbutton{Skip proof}}
      \onslide<2>
        \begin{proof}
          ...
        \end{proof}
      \end{overprint}
    \end{frame}
    

`\beamerreturnbutton`{⟨ _button text_ ⟩} 

The symbol drawn for this button is usually a left-pointing arrow. Use this button if pressing it will return from a detour. 

_Example:_
    
    
    \begin{frame}<1>[label=mytheorem]
      \begin{theorem}
        ...
      \end{theorem}
    
      \begin{overprint}
      \onslide<1>
        \hfill\hyperlink{mytheorem<2>}{\beamergotobutton{Go to proof details}}
      \onslide<2>
        \begin{proof}
          ...
        \end{proof}
        \hfill\hyperlink{mytheorem<1>}{\beamerreturnbutton{Return}}
      \end{overprint}
    \end{frame}
    \appendix
    \againframe<2>{mytheorem}
    

To make a button “clickable” you must place it in a command like \hyperlink. The command \hyperlink is a standard command of the hyperref package. The beamer class defines a whole bunch of other hyperlink commands that you can also use. 

`\hyperlink`<⟨ _overlay specification_ ⟩>{⟨ _target name_ ⟩}{⟨ _link text_ ⟩}<⟨ _overlay specification_ ⟩>

Only one ⟨ _overlay specification_ ⟩ may be given. The ⟨ _link text_ ⟩ is typeset in the usual way. If you click anywhere on this text, you will jump to the slide on which the \hypertarget command was used with the parameter ⟨ _target name_ ⟩. If an ⟨ _overlay specification_ ⟩ is present, the hyperlink (including the ⟨ _link text_ ⟩) is completely suppressed on the non-specified slides. 

The following commands have a predefined target; otherwise they behave exactly like \hyperlink. In particular, they all also accept an overlay specification and they also accept it at the end, rather than at the beginning. 

`\hyperlinkslideprev`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps one slide back.

`\hyperlinkslidenext`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps one slide forward.

`\hyperlinkframestart`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the first slide of the current frame. 

`\hyperlinkframeend`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the last slide of the current frame. 

`\hyperlinkframestartnext`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the first slide of the next frame.

`\hyperlinkframeendprev`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the last slide of the previous frame. 

The previous four command exist also with “frame” replaced by “subsection” everywhere, and also again with “frame” replaced by “section”. 

`\hyperlinkpresentationstart`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the first slide of the presentation. 

`\hyperlinkpresentationend`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the last slide of the presentation. This _excludes_ the appendix. 

`\hyperlinkappendixstart`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the first slide of the appendix. If there is no appendix, this will jump to the last slide of the document. 

`\hyperlinkappendixend`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the last slide of the appendix.

`\hyperlinkdocumentstart`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the first slide of the presentation. 

`\hyperlinkdocumentend`<⟨ _overlay specification_ ⟩>{⟨ _link text_ ⟩} 

Clicking the text jumps to the last slide of the presentation or, if an appendix is present, to the last slide of the appendix. 

#####  11.2 Repeating a Frame at a Later Point¶

Sometimes you may wish some slides of a frame to be shown in your main talk, but wish some “supplementary” slides of the frame to be shown only in the appendix. In this case, the \againframe command is useful. 

`\againframe`<⟨ _overlay specification_ ⟩>[<⟨ _default overlay specification_ ⟩>][⟨ _options_ ⟩]{⟨ _name_ ⟩} 

presentation

Resumes a frame that was previously created using \frame with the option label=⟨ _name_ ⟩. You must have used this option, just placing a label inside a frame “by hand” is not enough. You can use this command to “continue” a frame that has been interrupted by another frame. The effect of this command is to call the \frame command with the given ⟨ _overlay specification_ ⟩, ⟨ _default overlay specification_ ⟩ (if present), and ⟨ _options_ ⟩ (if present) and with the original frame’s contents. 

_Example:_
    
    
    \begin{frame}<1-2>[label=myframe]
      \begin{itemize}
      \item First subject.
      \item Second subject.
      \item Third subject.
      \end{itemize}
    \end{frame}
    
    \begin{frame}
      Some stuff explaining more on the second matter.
    \end{frame}
    
    \againframe<3>{myframe}
    

The effect of the above code is to create four slides. In the first two, the items 1 and 2 are highlighted. The third slide contains the text “Some stuff explaining more on the second matter.” The fourth slide is identical to the first two slides, except that the third point is now highlighted. 

_Example:_
    
    
    \begin{frame}<1>[label=Cantor]
      \frametitle{Main Theorem}
    
      \begin{Theorem}
        $\alpha < 2^\alpha$ for all ordinals~$\alpha$.
      \end{Theorem}
    
      \begin{overprint}
      \onslide<1>
        \hyperlink{Cantor<2>}{\beamergotobutton{Proof details}}
    
      \onslide<2->
        % this is only shown in the appendix, where this frame is resumed.
        \begin{proof}
          As shown by Cantor, ...
        \end{proof}
    
        \hfill\hyperlink{Cantor<1>}{\beamerreturnbutton{Return}}
      \end{overprint}
    \end{frame}
    
    ...
    \appendix
    
    \againframe<2>{Cantor}
    

In this example, the proof details are deferred to a slide in the appendix. Hyperlinks are setup, so that one can jump to the proof and go back. 

article

This command is ignored in article mode. 

#####  11.3 Adding Anticipated Zooming¶

Anticipated zooming is necessary when you have a very complicated graphic that you are not willing to simplify since, indeed, all the complex details merit an explanation. In this case, use the command \framezoom. It allows you to specify that clicking on a certain area of a frame should zoom out this area. You can then explain the details. Clicking on the zoomed out picture will take you back to the original one. 

`\framezoom`<⟨ _button overlay specification_ ⟩><⟨ _zoomed overlay specification_ ⟩>[⟨ _options_ ⟩]  
(⟨ _upper left x_ ⟩,⟨ _upper left y_ ⟩)(⟨ _zoom area width_ ⟩,⟨ _zoom area depth_ ⟩)

This command should be given somewhere at the beginning of a frame. When given, two different things will happen, depending on whether the ⟨ _button overlay specification_ ⟩ applies to the current slide of the frame or whether the ⟨ _zoomed overlay specification_ ⟩ applies. These overlay specifications should not overlap. 

If the ⟨ _button overlay specification_ ⟩ applies, a clickable area is created inside the frame. The size of this area is given by ⟨ _zoom area width_ ⟩ and ⟨ _zoom area depth_ ⟩, which are two normal TeX dimensions (like 1cm or 20pt). The upper left corner of this area is given by ⟨ _upper left x_ ⟩ and ⟨ _upper left y_ ⟩, which are also TeX dimensions. They are measures _relative to the place where the first normal text of a frame would go_. Thus, the location (0pt,0pt) is at the beginning of the normal text (which excludes the headline and also the frame title). 

By default, the button is clickable, but it will not be indicated in any special way. You can draw a border around the button by using the following ⟨ _option_ ⟩: 

  * • border=⟨ _width in pixels_ ⟩ will draw a border around the specified button area. The default width is 1 pixel. The color of this button is the linkbordercolor of hyperref. beamer sets this color to a 50% gray by default.  
To change this, you can use the command \hypersetup{linkbordercolor={⟨ _red_ ⟩ ⟨ _green_ ⟩ ⟨ _blue_ ⟩}}, where ⟨ _red_ ⟩, ⟨ _green_ ⟩, and ⟨ _blue_ ⟩ are values between 0 and 1. 




When you press the button created in this way, the viewer application will hyperjump to the first of the frames specified by the ⟨ _zoomed overlay specification_ ⟩. For the slides to which this overlay specification applies, the following happens: 

The exact same area as the one specified before is “zoomed out” to fill the whole normal text area of the frame. Everything else, including the sidebars, the headlines and footlines, and even the frame title retain their normal size. The zooming is performed in such a way that the whole specified area is completely shown. The aspect ratio is kept correct and the zoomed area will possibly show more than just the specified area if the aspect ratio of this area and the aspect ratio of the available text area do not agree. 

Behind the whole text area (which contains the zoomed area) a big invisible “Back” button is put. Thus clicking anywhere on the text area will jump back to the original (unzoomed) picture. 

You can specify several zoom areas for a single frame. In this case, you should specify different ⟨ _zoomed overlay specification_ ⟩, but you can specify the same ⟨ _button overlay specification_ ⟩. You cannot nest zoomings in the sense that you cannot have a zoom button on a slide that is in some ⟨ _zoomed overlay specification_ ⟩. However, you can have overlapping and even nested ⟨ _button overlay specification_ ⟩. When clicking on an area that belongs to several buttons, the one given last will “win” (it should hence be the smallest one). 

If you do not wish to have the frame title shown on a zoomed slide, you can add an overlay specification to the \frametitle command that simply suppresses the title for the slide. Also, by using the plain option, you can have the zoomed slide fill the whole page. 

_Example:_ A simple case
    
    
    \begin{frame}
      \frametitle{A Complicated Picture}
    
      \framezoom<1><2>(0cm,0cm)(2cm,1.5cm)
      \framezoom<1><3>(1cm,3cm)(2cm,1.5cm)
      \framezoom<1><4>(3cm,2cm)(3cm,2cm)
    
      \pgfimage[height=8cm]{complicatedimagefilename}
    \end{frame}
    

_Example:_ A more complicate case in which the zoomed parts completely fill the frames. 
    
    
    \begin{frame}<1>[label=zooms]
      \frametitle<1>{A Complicated Picture}
    
      \framezoom<1><2>[border](0cm,0cm)(2cm,1.5cm)
      \framezoom<1><3>[border](1cm,3cm)(2cm,1.5cm)
      \framezoom<1><4>[border](3cm,2cm)(3cm,2cm)
    
      \pgfimage[height=8cm]{complicatedimagefilename}
    \end{frame}
    \againframe<2->[plain]{zooms}
    
