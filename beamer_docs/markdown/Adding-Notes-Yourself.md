## Creating Supporting Material

####  19 Adding Notes for Yourself 

A _note_ is text that is intended as a reminder to yourself of what you should say or should keep in mind when presenting a slide. Notes are usually printed out on paper, but with two-screen support they can also be shown on your laptop screen while the main presentation is shown on the projector. 

#####  19.1 Specifying Note Contents¶

To add a note to a slide or a frame, use the \note command. This command can be used both inside and outside frames, but it has quite different behaviors then: Inside frames, \note commands accumulate and append a single note page after the current slide; outside frames each \note directly inserts a single note page with the given parameter as contents. Using the \note command inside frames is usually preferably over using them outside, since only commands issued inside frames profit from the option show only slides with notes. 

Inside a frame, the effect of \note⟨ _text_ ⟩ is the following: When you use it somewhere inside the frame on a specific slide, a note page is created after the slide, containing the ⟨ _text_ ⟩. Since you can add an overlay specification to the \note command, you can specify after which slide the note should be shown. If you use multiple \note commands on one slide, they “accumulate” and are all shown on the same note. 

To make the accumulation of notes more convenient, you can use the \note command with the option [item]. The notes added with this option are accumulated in an enumerate list that follows any text inserted using \note. 

The following example will produce one note page that follows the second slide and has two entries. 
    
    
    \begin{frame}
     \begin{itemize}
     \item<1-> Eggs
     \item<2-> Plants
       \note[item]<2>{Tell joke about plants.}
       \note[item]<2>{Make it short.}
     \item<3-> Animals
     \end{itemize}
    \end{frame}
    

Outside frames, the command \note creates a single note page. It is “independent” of any usage of the \note commands inside the previous frame. If you say \note inside a frame and \note right after it, _two_ note pages are created. 

In the following, the syntax and effects of the \note command _inside_ frames are described: 

`\note`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]{⟨ _note text_ ⟩} 

Effects _inside_ frames:

This command appends the ⟨ _note text_ ⟩ to the note that follows the current slide. Multiple uses of this command on a slide accumulate. If you do not specify an ⟨ _overlay specification_ ⟩, the note will be added to _all_ slides of the current frame. This is often not what you want, so adding a specification like <1> is usually a good idea. 

The following ⟨ _options_ ⟩ may be given: 

  * • item causes the note to be put as an item in a list that is shown at the end of the note page. 




_Example:_ \note<2>{Do not talk longer than 2 minutes about this.}

article

Notes are ignored in article mode.

Next, the syntax and effects of the \note command _outside_ frames are described: 

`\note`[⟨ _options_ ⟩]{⟨ _note text_ ⟩} 

Outside frames, this command creates a note page. This command is _not_ affected by the option show only slides with notes. 

The following ⟨ _options_ ⟩ may be given: 

  * • itemize will enclose the whole note page in an itemize environment. This is just a convenience. 

  * • enumerate will enclose the whole note page in an enumerate environment. 




_Example:_
    
    
    \begin{frame}
    some text
    \end{frame}
    \note{Talk no more than 1 minute.}
    
    \note[enumerate]
    {
    \item Stress this first.
    \item Then this.
    }
    

article

Notes are ignored in article mode.

The following element dictates how the note pages are rendered:

**Beamer-Template/-Color/-Font** note page

This template is used to typeset a note page. The template should contain a mentioning of the insert \insertnote, which will contain the note text. To squeeze more onto note pages you might consider changing the size of the beamer-font note page to something small. The default is \small. 

The following template options are predefined:

  * • `[default]` The default template shows the last slide in the upper right corner and some “hints” that should help you match a note page to the slide that is currently shown. 

  * • `[compress]` The option produces an output that is similar to the default, only more fits onto each note page at the price of legibility. 

  * • `[plain]` Just inserts the note text, no fancy hints. 

  * • `[lined]`[⟨ _number_ ⟩] Instead of printing the note text, this option fills the note page with lines on which the audience can write their own notes on. ⟨ _number_ ⟩ specifies how many lines will be shown, the default is 6 lines. For a more sophisticated interface, the [handoutwithnotes](<https://www.ctan.org/pkg/handoutwithnotes>) package can be used. 




The following two inserts are useful for note pages:

  * • `\insertnote` Inserts the text of the current note into the template. 

  * • `\insertslideintonotes`{⟨ _magnification_ ⟩} Inserts a “mini picture” of the last slide into the current note. The slide will be scaled by the given magnification. 

_Note:_ The backgrounds, headlines, footlines and sidebars will not appear in the slide. 

_Example:_ \insertslideintonotes{0.25}

This will give a mini slide whose width and height are one fourth of the usual size. 




#####  19.2 Specifying Contents for Multiple Notes¶

Sometimes you wish some text to be shown on every note or at least on every note in a long series of notes. To achieve this effect, you can use the following two commands: 

`\AtBeginNote`{⟨ _text_ ⟩} 

The ⟨ _text_ ⟩ will be inserted at the beginning of every note in the scope of the command. To stop the effect, either use \AtBeginNote{} or enclose the area in a TeX group. 

It is advisable to add a \par command or an empty line at the end of the ⟨ _text_ ⟩ since otherwise any note text will directly follow the ⟨ _text_ ⟩ without a line break. 

_Example:_
    
    
    \section{My Section}
    
    \AtBeginNote{Finish this section by 14:35.\par}
    \begin{frame}
      ...
      \note{some note}
    \end{frame}
    \begin{frame}
      ...
      \note{some other note}
    \end{frame}
    \AtBeginNote{}
    

`\AtEndNote`{⟨ _text_ ⟩} 

This command behaves the same way as \AtBeginNote, except that the text is inserted at the end (bottom). You may wish to add a \par at the beginning of ⟨ _text_ ⟩. 

#####  19.3 Specifying Which Notes and Frames Are Shown¶

Since you normally do not wish the notes to be part of your presentation, you must explicitly say so in the preamble if notes should be included in your presentation. You can use the following beamer options for this: 

\setbeameroption{hide notes} 

Notes are not shown. This is the default in a presentation.

\setbeameroption{show notes} 

Include notes in the output file. Normal slides are also included and the note pages are interleaved with them. 

\setbeameroption{show notes on second screen=⟨ _location_ ⟩} 

When this option is given, a two screen version of your talk is created, see Section [22](<Taking-Advantage-Multiple-Screens.html#section-twoscreens>) for further details. The second screen, which is displayed on the right by default, shows your notes. By specifying a different ⟨ _location_ ⟩, you can also place the second screen on the left, bottom, or top. 

_Example:_
    
    
    \documentclass{beamer}
    \setbeameroption{show notes on second screen}
    \begin{document}
    \begin{frame}
      A frame.
      \note{This is shown on the right.}
    \end{frame}
    \end{document}
    

In detail, the following happens: The presentation is typeset normally and shown on the main screen or, to be precise, on pgfpages’s logical page number zero. The second screen (logical screen number one) is initialized to be empty. 

Whenever a note page is to be typeset, either because a frame contained \note commands or because the frame was followed by a \note command, the note page is normally typeset. Then the note page is put on the second screen. Then the whole page is shipped out. (The exact details are bit more complex, but that is what happens, basically.) 

An important effect of this behavior is that a note page _following_ a frame is shown next to this frame. Normally, this is exactly what you want and expect. However, if there are multiple note pages for a single slide only the last one is shown, currently. This may change in the future, so do not rely on this effect. 

_Example:_
    
    
    \begin{frame}
      First frame.
    \end{frame}
    \note{This note is not shown at all (currently).}
    \note{This note is shown together with the first frame.}
    
    \begin{frame}
      Second frame.
      \note{This note is shown together with the second frame.}
    \end{frame}
    
    \begin{frame}
      No note text is shown for this frame.
    \end{frame}
    

If you really need multiple note pages for a single slide, you will have to use something more complicated like this: 
    
    
    \begin{frame}<1-3>
     First frame.
     \note<1>{First page of notes for this frame.}
     \note<2>{Second page of notes for this frame.}
     \note<3>{Third page of notes for this frame.}
    \end{frame}
    

\setbeameroption{show only notes} 

Include only the notes in the output file and suppresses all frames. This option is useful for printing them. If you specify this command, the .aux and .toc files are _not_ updated. So, if you add a section and reTeX your presentation, this will not be reflected in the navigation bars (which you do not see anyway since only notes are output). 

\setbeameroption{show only slides with notes} 

Include only slides in the output file that have an accompanying note page. Slides without notes will be excluded. If you specify this command, the .aux and .toc files are _not_ updated. So, if you add a section and reTeX your presentation, this will not be reflected in the navigation bars. 
