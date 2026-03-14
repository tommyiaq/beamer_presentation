## Building a Presentation

####  14 Animations, Sounds, and Slide Transitions 

#####  14.1 Animations¶

######  14.1.1 Including External Animation Files¶

If you have created an animation using some external program (like a renderer), you can use the capabilities of the presentation program (like the Acrobat Reader) to show the animation. Unfortunately, currently there is no portable way of doing this and even the Acrobat Reader does not support this feature on all platforms. 

To include an animation in a presentation, you can use, for example, the package multimedia.sty which is part of the beamer package. You have to include this package explicitly. Despite being distributed as part of the beamer distribution, this package is perfectly self-sufficient and can be used independently of beamer. 

\usepackage{multimedia}

A stand-alone package that implements several commands for including external animation and sound files in a pdf document. The package can be used together with both dvips plus ps2pdf and pdflatex, though the special sound support is available only in pdflatex. 

When including this package, you must also include the hyperref package. The multimedia is one of the few packages that needs to be loaded after hyperref. Since beamer includes hyperref automatically, you need not worry about this when creating a presentation using beamer. 

For including an animation in a pdf file, you can use the command \movie, which is explained below. Depending on the used options, this command will either setup the pdf file such that the viewer application (like the Acrobat Reader) itself will try to play the movie or that an external program will be called. The latter approach, though much less flexible, must be taken if the viewer application is unable to display the movie itself. 

`\movie`[⟨ _options_ ⟩]{⟨ _poster text_ ⟩}{⟨ _movie filename_ ⟩} 

This command will insert the movie with the filename ⟨ _movie filename_ ⟩ into the pdf file. The movie file must reside at some place where the viewer application will be able to find it, which is typically only the directory in which the final pdf file resides. The movie file will _not_ be embedded into the pdf file in the sense that the actual movie data is part of the main.pdf file. The movie file must hence be copied and passed along with the pdf file. (Nevertheless, one often says that the movie is “embedded” in the document, but that just means that one can click on the movie when viewing the document and the movie will start to play.) 

The movie will use a rectangular area whose size is determined either by the width= and height= options or by the size of the ⟨ _poster text_ ⟩. The ⟨ _poster text_ ⟩ can be any TeX text; for example, it might be a \pgfuseimage command or an \includegraphics command or a pgfpicture environment or just plain text. The ⟨ _poster text_ ⟩ is typeset in a box, the box is inserted into the normal text, and the movie rectangle is put exactly over this box. Thus, if the ⟨ _poster text_ ⟩ is an image from the movie, this image will be shown until the movie is started, when it will be exactly replaced by the movie itself. However, there is also a different, sometimes better, way of creating a poster image, namely by using the poster option as explained later on. 

The aspect ratio of the movie will _not_ be corrected automatically if the dimension of the ⟨ _poster text_ ⟩ box does not have the same aspect ratio. Most movies have an aspect ratio of 4:3 or 16:9. 

Despite the name, a movie may consist only of sound with no images. In this case, the ⟨ _poster text_ ⟩ might be a symbol representing the sound. There is also a different, dedicated command for including sounds in a pdf file, see the \sound command in Section [14.2](<Animations-Sounds-Slide-Transitions.html#section-sound>). 

Unless further options are given, the movie will start only when the user clicks on it. Whether the viewer application can actually display the movie depends on the application and the version. For example, the Acrobat Reader up to version 5 does not seem to be able to display any movies or sounds on Linux. On the other hand, the Acrobat Reader Version 6 on MacOS is able to display anything that QuickTime can display, which is just about everything. Embedding movies in a pdf document is provided for by the pdf standard and is not a peculiarity of the Acrobat Reader. In particular, one might expect other viewers like xpdf and poppler-based viewers (Okular, Evince) to support embedded movies in the future. 

_Example:_ \movie{\pgfuseimage{myposterimage}}{mymovie.avi}

_Example:_ \movie[width=3cm,height=2cm,poster]{}{mymovie.mpg}

If your viewer application is not able to render your movie, but some external application is, you must use the externalviewer option. This will ask the viewer application to launch an application for showing the movie instead of displaying it itself. Since this application is started in a new window, this is not nearly as nice as having the movie displayed directly by the viewer (unless you use evil trickery to suppress the frame of the viewer application). Which application is chosen is left to the discretion of the viewer application, which tries to make its choice according to the extension of the ⟨ _movie filename_ ⟩ and according to some mapping table for mapping extensions to viewer applications. How this mapping table can be modified depends on the viewer application, please see the release notes of your viewer. 

The following ⟨ _options_ ⟩ may be given: 

  * • autostart. Causes the movie to start playing immediately when the page is shown. At most one movie can be started in this way. The viewer application will typically be able to show at most one movie at the same time anyway. When the page is no longer shown, the movie immediately stops. This can be a problem if you use the \movie command to include a sound that should be played on after the page has been closed. In this case, the \sound command must be used. 

  * • borderwidth=⟨ _T eX dimension_⟩. Causes a border of thickness ⟨ _T eX dimension_⟩ to be drawn around the movie. Some versions of the Acrobat Reader seem to have a bug and do not display this border if is smaller than 0.5bp (about 0.51pt). 

  * • depth=⟨ _T eX dimension_⟩. Overrides the depth of the ⟨ _poster text_ ⟩ box and sets it to the given dimension. 

  * • duration=⟨ _time_ ⟩s. Specifies in seconds how long the movie should be shown. The ⟨ _time_ ⟩ may be a fractional value and must be followed by the letter s. For example, duration=1.5s will show the movie for one and a half seconds. In conjunction with the start option, you can “cut out” a part of a movie for display. 

  * • externalviewer. As explained above, this causes an external application to be launched for displaying the movie in a separate window. Most options, like duration or loop, have no effect since they are not passed along to the viewer application. 

  * • height=⟨ _T eX dimension_⟩. Overrides the height of the ⟨ _poster text_ ⟩ box and sets it to the given dimension. 

  * • label=⟨ _movie label_ ⟩. Assigns a label to the movie such that it can later be referenced by the command \hyperlinkmovie, which can be used to stop the movie or to show a different part of it. The ⟨ _movie label_ ⟩ is not a normal label. It should not be too fancy, since it is inserted literally into the pdf code. In particular, it should not contain closing parentheses. 

  * • loop. Causes the movie to start again when the end has been reached. Normally, the movie just stops at the end. 

  * • once. Causes the movie to just stop at the end. This is the default. 

  * • open. Causes the player to stay open when the movie has finished. 

  * • palindrome. Causes the movie to start playing backwards when the end has been reached, and to start playing forward once more when the beginning is reached, and so on. 

  * • poster. Asks the viewer application to show the first image of the movie when the movie is not playing. Normally, nothing is shown when the movie is not playing (and thus the box containing the ⟨ _poster text_ ⟩ is shown). For a movie that does not have any images (but sound) or for movies with an uninformative first image this option is not so useful. 

  * • repeat is the same as loop. 

  * • showcontrols=⟨ _true or false_ ⟩. Causes a control bar to be displayed below the movie while it is playing. Instead of showcontrols=true you can also just say showcontrols. By default, no control bar is shown. 

  * • start=⟨ _time_ ⟩s. Causes the first ⟨ _time_ ⟩ seconds of the movie to be skipped. For example, start=10s,duration=5s will show seconds 10 to 15 of the movie, when you play the movie. 

  * • width=⟨ _T eXdimension_⟩ works like the height option, only for the width of the poster box. 




_Example:_ The following example creates a “background sound” for the slide. 
    
    
    \movie[autostart]{}{test.wav}
    

_Example:_ A movie with two extra buttons for showing different parts of the movie. 
    
    
    \movie[label=cells,width=4cm,height=3cm,poster,showcontrols,duration=5s]{}{cells.avi}
    
    \hyperlinkmovie[start=5s,duration=7s]{cells}{\beamerbutton{Show the middle stage}}
    
    \hyperlinkmovie[start=12s,duration=5s]{cells}{\beamerbutton{Show the late stage}}
    

A movie can serve as the destination of a special kind of hyperlink, namely a hyperlink introduced using the following command: 

`\hyperlinkmovie`[⟨ _options_ ⟩]{⟨ _movie label_ ⟩}{⟨ _text_ ⟩} 

Causes the ⟨ _text_ ⟩ to become a movie hyperlink. When you click on the ⟨ _text_ ⟩, the movie with the label ⟨ _movie label_ ⟩ will start to play (or stop or pause or resume, depending on the ⟨ _options_ ⟩). The movie must be on the same page as the hyperlink. 

The following ⟨ _options_ ⟩ may be given, many of which are the same as for the \movie command; if a different option is given for the link than for the movie itself, the option for the link takes precedence: 

  * • duration=⟨ _time_ ⟩s. As for \movie, this causes the movie to be played only for the given number of seconds. 

  * • loop and repeat. As for \movie, this causes the movie to loop. 

  * • once. As for \movie, this causes the movie to played only once. 

  * • palindrome. As for \movie, this causes the movie to be played forth and back. 

  * • pause. Causes the playback of the movie to be paused, if the movie was currently playing. If not, nothing happens. 

  * • play. Causes the movie to be played from whatever start position is specified. If the movie is already playing, it will be stopped and restarted at the starting position. This is the default. 

  * • resume. Resumes playback of the movie, if it has previously been paused. If has not been paused, but not started or is already playing, nothing happens. 

  * • showcontrols=⟨ _true or false_ ⟩. As for \movie, this causes a control bar to be shown or not shown during playback. 

  * • start=⟨ _time_ ⟩s. As for \movie, this causes the given number of seconds to be skipped at the beginning of the movie if play is used to start the movie. 

  * • stop. Causes the playback of the movie to be stopped. 




######  14.1.2 Animations Created by Showing Slides in Rapid Succession¶

You can create an animation in a portable way by using the overlay commands of the beamer package to create a series of slides that, when shown in rapid succession, present an animation. This is a flexible approach, but such animations will typically be rather static since it will take some time to advance from one slide to the next. This approach is mostly useful for animations where you want to explain each “picture” of the animation. When you advance slides “by hand,” that is, by pressing a forward button, it typically takes at least a second for the next slide to show. 

More “lively” animations can be created by relying on a capability of the viewer program. Some programs support showing slides only for a certain number of seconds during a presentation (for the Acrobat Reader this works only in full-screen mode). By setting the number of seconds to zero, you can create a rapid succession of slides. 

To facilitate the creation of animations using this feature, the following commands can be used: \animate and \animatevalue. 

`\animate`<⟨ _overlay specification_ ⟩>

The slides specified by ⟨ _overlay specification_ ⟩ will be shown as quickly as possible. 

_Example:_
    
    
    \begin{frame}
      \frametitle{A Five Slide Animation}
      \animate<2-4>
    
      The first slide is shown normally. When the second slide is shown
      (presumably after pressing a forward key), the second, third, and
      fourth slides ``flash by.'' At the end, the content of the fifth
      slide is shown.
    
      ... code for creating an animation with five slides ...
    \end{frame}
    

article

This command is ignored in article mode. 

`\animatevalue`<⟨ _start slide_ ⟩-⟨ _end slide_ ⟩> {⟨ _name_ ⟩}{⟨ _start value_ ⟩}{⟨ _end value_ ⟩} 

The ⟨ _name_ ⟩ must be the name of a counter or a dimension. It will be varied between two values. For the slides in the specified range, the counter or dimension is set to an interpolated value that depends on the current slide number. On slides before the ⟨ _start slide_ ⟩, the counter or dimension is set to ⟨ _start value_ ⟩; on the slides after the ⟨ _end slide_ ⟩ it is set to ⟨ _end value_ ⟩. 

_Example:_
    
    
    \newcount\opaqueness
    \begin{frame}
      \animate<2-10>
      \animatevalue<1-10>{\opaqueness}{100}{0}
      \begin{colormixin}{\the\opaqueness!averagebackgroundcolor}
        \frametitle{Fadeout Frame}
    
        This text (and all other frame content) will fade out when the
        second slide is shown. This even works with
        {\color{green!90!black}colored} \alert{text}.
      \end{colormixin}
    \end{frame}
    
    \newcount\opaqueness
    \newdimen\offset
    \begin{frame}
      \frametitle{Flying Theorems (You Really Shouldn't!)}
    
      \animate<2-14>
    
      \animatevalue<1-15>{\opaqueness}{100}{0}
      \animatevalue<1-15>{\offset}{0cm}{-5cm}
      \begin{colormixin}{\the\opaqueness!averagebackgroundcolor}
      \hskip\offset
        \begin{minipage}{\textwidth}
          \begin{theorem}
            This theorem flies out.
          \end{theorem}
        \end{minipage}
      \end{colormixin}
    
      \animatevalue<1-15>{\opaqueness}{0}{100}
      \animatevalue<1-15>{\offset}{-5cm}{0cm}
      \begin{colormixin}{\the\opaqueness!averagebackgroundcolor}
      \hskip\offset
        \begin{minipage}{\textwidth}
          \begin{theorem}
            This theorem flies in.
          \end{theorem}
        \end{minipage}
      \end{colormixin}
    \end{frame}
    

article

This command is ignored in article mode. 

If your animation “graphics” reside in individual external graphic files, you might also consider using the \multiinclude command, which is explained in Section [14.1.3](<Animations-Sounds-Slide-Transitions.html#section-mpmulti>), together with \animate. For example, you might create an animation like this, assuming you have created graphic files named animation.1 through to animation.10: 
    
    
    \begin{frame}
      \animate<2-9>
      \multiinclude[start=1]{animation}
    \end{frame}
    

######  14.1.3 Including External Animations Residing in Multiple Image Files¶

Some animations reside in external files in the following way: For each stage of the animation there is an image file containing an image for this stage. You can include such a series of images conveniently by using the style mpmulti.sty from the ppower4 package. This style, written by Klaus Guntermann, introduces a command called \multiinclude that takes the base name of a graphic file like mygraphic and will then search for files called mygraphic.0, mygraphic.1, and so on, till no more files are found. It will then include these graphics files using the \includegraphics command, but will put these graphics “on top of each other.” Furthermore, and this is the important part, it inserts a \pause command after each graphic. This command is defined in the ppower4 package and has the same effect as the \pause command of beamer. For this reason, both ppower4 and also beamer will first display the basic graphic and will then additionally show the next graphic on each slide. 

If you try to use mpmulti.sty directly, you will run into the problem that it includes a file called pause.sty, which is part of the ppower4 package. 

You might also consider using the style xmpmulti.sty that comes with beamer. This file is mainly identical to mpmulti, except for two differences: First, it does not include pause.sty, a style that conceptually clashes with beamer, although beamer contains a workaround that sidesteps the problem. Second, it extends the \multiinclude command by allowing a special default overlay specification to be given. The effect of this is explained below. 

\usepackage{xmpmulti}

Defines the command \multiinclude. The code of this package is due to Klaus Guntermann with some additions of mine. It can be used together with beamer and with ppower4, i. e., it can be used as a replacement for mpmulti if the pause package is also included in a ppower4-presentation. 

`\multiinclude`[<⟨ _default overlay specification_ ⟩>][⟨ _options_ ⟩]{⟨ _base file name_ ⟩} 

Except for the possibility of specifying a ⟨ _default overlay specification_ ⟩, this command is identical to the \multiinclude command from the ppower4 package. 

If no overlay specification is given, the command will search for files called ⟨ _base file name_ ⟩.⟨ _number_ ⟩ for increasing numbers ⟨ _number_ ⟩, starting with zero. As long as it finds these files, it issues an \includegraphics command on them. The files following the first one are put “on top” of the first one. Between any two invocations of \includegraphics, a \pause command is inserted. You can modify this behavior in different ways by given suitable ⟨ _options_ ⟩, see below. 

_Example:_ Assume that MetaPost has created files called gra.0, gra.1, and gra.2. You can then create frame consisting of three slides that incrementally show the graphic as follows: 
    
    
    \begin{frame}
      \multiinclude{gra}
    \end{frame}
    

The effect of providing a ⟨ _default overlay specification_ ⟩ is the following: First, no \pause command is inserted between graphics. Instead, each graphic is surrounded by an actionenv environment with the overlay specification set to ⟨ _default overlay specification_ ⟩. 

_Example:_ You can create the same effect as in the previous example using \multiinclude[<+->]{gra}. 

_Example:_ For a more interesting usage of the ⟨ _default overlay specification_ ⟩, consider the following usage: 
    
    
    \multiinclude[]{gra}
    

This will always paint the most recently added part of the graphic in red (assuming you do not use special colors in the graphic itself). 

_Example:_ In order to have each graphic completely _replace_ the previous one, you could use \multiinclude[<+>]{gra}. 

The following ⟨ _options_ ⟩ may be given (these are the same as for the original command from the ppower4 package): 

  * • pause=⟨ _command_ ⟩ replaces the default pausing command \pause by ⟨ _command_ ⟩. If a ⟨ _default overlay specification_ ⟩ is given, the default pausing command is empty; otherwise it is \pause. Note that commands like \pauselevel are not available in \beamer. 

  * • graphics=⟨ _options_ ⟩ passes the ⟨ _options_ ⟩ to the \includegraphics command. 

_Example:_ \multiinclude[graphics={height=5cm}]{gra}

  * • format=⟨ _extension_ ⟩ will cause the file names for which we search change from ⟨ _base file name_ ⟩.⟨ _number_ ⟩ to ⟨ _base file name_ ⟩-⟨ _number_ ⟩.⟨ _extension_ ⟩. Note the change from the dot to a hyphen. This option allows you to include, say, .jpg files. 

  * • start=⟨ _number_ ⟩ specifies the start ⟨ _number_ ⟩. The default is zero. 

  * • end=⟨ _number_ ⟩ specifies the end ⟨ _number_ ⟩. The default is infinity. 




Note that, if you do not use the format= option, the \includegraphics command will be somewhat at a loss in which format your graphic file actually is. After all, it ends with the cryptic “format suffix” .0 or .1. You can tell \includegraphics that any file having a suffix it knows nothing about is actually in format, say, .mps, using the following command: 
    
    
    \DeclareGraphicsRule{*}{mps}{*}{}
    

#####  14.2 Sounds¶

You can include sounds in a presentation. Such sound can be played when you open a slide or when a certain button is clicked. The commands for including sounds are defined in the package multimedia, which is introduced in Section [14.1.1](<Animations-Sounds-Slide-Transitions.html#section-multimedia>). 

As was already pointed out in Section [14.1.1](<Animations-Sounds-Slide-Transitions.html#section-multimedia>), a sound can be included in a pdf presentation by treating it as a movie and using the \movie command. While this is perfectly sufficient in most cases, there are two cases where this approach is not satisfactory: 

  * 1. When a page is closed, any playing movie is immediately stopped. Thus, you cannot use the \movie command to create sounds that persist for a longer time. 

  * 2. You cannot play two movies at the same time. 




The pdf specification introduces special sound objects, which are treated quite differently from movie objects. You can create a sound object using the command \sound, which is somewhat similar to \movie. There also exists a \hyperlinksound command, which is similar to \hyperlinkmovie. While it is conceptually better to use \sound for sounds, there are a number of things to consider before using it: 

  * • Several sounds _can_ be played at the same time. In particular, it is possible to play a general sound in parallel to a (hopefully silent) movie. 

  * • A sound playback _can_ persist after the current page is closed (though it need not). 

  * • The data of a sound file _can_ be completely embedded in a pdf file, obliterating the need to “carry around” other files. 

  * • The sound objects do _not_ work together with dvips and ps2pdf. They only work with pdflatex. 

  * • There is much less control over what part of a sound should be played. In particular, no control bar is shown and you can specify neither the start time nor the duration. 

  * • A bug in some versions of the Acrobat Reader makes it necessary to provide very exact details on the encoding of the sound file. You have to provide the sampling rate, the number of channels (mono or stereo), the number of bits per sample, and the sample encoding method (raw, signed, Alaw or ![\\\( \\mu \\\)](beameruserguide-images/5A119483F03DE4CFBEF70D8746405861.svg)law). If you do not know this data or provide it incorrectly, the sound will be played incorrectly. 

  * • It seems that you can only include uncompressed sound data, which can easily become huge. This is not required by the specification, but some versions of Acrobat Reader are unable to play any compressed data. Data formats that _do_ work are .aif and .au. 




`\sound`[⟨ _options_ ⟩]{⟨ _sound poster text_ ⟩}{⟨ _sound filename_ ⟩} 

This command will insert the sound with the filename ⟨ _sound filename_ ⟩ into the pdf file. As for \movie, the file must be accessible when the sound is to be played. Unlike \movie, you can however use the option inlinesound to actually embed the sound data in the pdf file. 

Also as for a movie, the ⟨ _sound poster text_ ⟩ will be be put in a box that, when clicked on, will start playing the movie. However, you might also leave this box empty and only use the autostart option. Once playback of a sound has started, it can only be stopped by starting the playback of a different sound or by use of the \hyperlinkmute command. 

The supported sound formats depend on the viewer application. Some versions of Acrobat Reader support .aif and .au. Sometimes you also need to specify information like the sampling rate, even though this information could be extracted from the sound file and even though the pdf standard specifies that the viewer application should do so. In this regard, some versions of Acrobat Reader seem to be non-standard-conforming. 

This command only works together with pdflatex. If you use dvips, the poster is still shown, but clicking it has no effect and no sound is embedded in any way. 

_Example:_ \sound[autostart,samplingrate=22050]{}{applause.au}

The following ⟨ _options_ ⟩ may be given: 

  * • autostart. Causes the sound to start playing immediately when the page is shown. 

  * • automute. Causes all sounds to be muted when the current page is left. 

  * • bitspersample=⟨ _8 or 16_ ⟩. Specifies the number of bits per sample in the sound file. If this number is 16, this option need not be specified. 

  * • channels=⟨ _1 or 2_ ⟩. Specifies whether the sound is mono or stereo. If the sound is mono, this option need not be specified. 

  * • depth=⟨ _T eX dimension_⟩. Overrides the depth of the ⟨ _sound poster text_ ⟩ box and sets it to the given dimension. 

  * • encoding=⟨ _method_ ⟩. Specifies the encoding method, which may be Raw, Signed, muLaw, or ALaw. If the method is muLaw, this option need not be specified. 

  * • externalviewer causes an external application to be launched for playing the sound. Most options, like loop, have no effect since they are not passed along to the external application. 

  * • height=⟨ _T eX dimension_⟩. Overrides the height of the ⟨ _sound poster text_ ⟩ box and sets it to the given dimension. 

  * • inlinesound causes the sound data to be stored directly in the pdf-file. 

  * • label=⟨ _sound label_ ⟩. Assigns a label to the sound such that it can later be referenced by the command \hyperlinksound, which can be used to start a sound. The ⟨ _sound label_ ⟩ is not a normal label. 

  * • loop or repeat. Causes the sound to start again when the end has been reached. 

  * • mixsound=⟨ _true or false_ ⟩. If set to true, the sound is played in addition to any sound that is already playing. If set to false all other sounds (though not sound from movies) are stopped before the sound is played. The default is false. 

  * • samplingrate=⟨ _number_ ⟩. Specifies the number of samples per second in the sound file. If this number is 44100, this option need not be specified. 

  * • width=⟨ _T eX dimension_⟩ works like the height option, only for the width of the poster box. 




_Example:_ The following example creates a “background sound” for the slide, assuming that applause.au is encoded correctly (44100 samples per second, mono, ![\\\( \\mu \\\)](beameruserguide-images/5A119483F03DE4CFBEF70D8746405861.svg)law encoded, 16 bits per sample). 
    
    
    \sound[autostart]{}{applause.au}
    

Just like movies, sounds can also serve as destinations of special sound hyperlinks. 

`\hyperlinksound`[⟨ _options_ ⟩]{⟨ _sound label_ ⟩}{⟨ _text_ ⟩} 

Causes the ⟨ _text_ ⟩ to become a sound hyperlink. When you click on the ⟨ _text_ ⟩, the sound with the label ⟨ _sound label_ ⟩ will start to play. 

The following ⟨ _options_ ⟩ may be given: 

  * • loop or repeat. Causes the sound to start again when the end has been reached. 

  * • mixsound=⟨ _true or false_ ⟩. If set to true, the sound is played in addition to any sound that is already playing. If set to false all other sounds (though not sound from movies) are stopped before the sound is played. The default is false. 




Since there is no direct way of stopping the playback of a sound, the following command is useful: 

`\hyperlinkmute`{⟨ _text_ ⟩} 

Causes the ⟨ _text_ ⟩ to become a hyperlink that, when clicked, stops the playback of all sounds. 

#####  14.3 Slide Transitions¶

pdf in general, and the Acrobat Reader in particular, offer a standardized way of defining _slide transitions_. Such a transition is a visual effect that is used to show the slide. For example, instead of just showing the slide immediately, whatever was shown before might slowly “dissolve” and be replaced by the slide’s content. 

There are a number of commands that can be used to specify what effect should be used when the current slide is presented. Consider the following example: 
    
    
    \begin{frame}
      \pgfuseimage{youngboy}
    \end{frame}
    \begin{frame}
      \transdissolve
      \pgfuseimage{man}
    \end{frame}
    

The command \transdissolve causes the slide of the second frame to be shown in a “dissolved way.” Note that the dissolving is a property of the second frame, not of the first one. We could have placed the command anywhere on the frame. 

The transition commands are overlay-specification-aware. We could collapse the two frames into one frame like this: 
    
    
    \begin{frame}
      \only<1>{\pgfuseimage{youngboy}}
      \only<2>{\pgfuseimage{man}}
      \transdissolve<2>
    \end{frame}
    

This states that on the first slide the young boy should be shown, on the second slide the old man should be shown, and when the second slide is shown, it should be shown in a “dissolved way.” 

In the following, the different commands for creating transitional effects are listed. All of them take an optional argument that may contain a list of ⟨ _key_ ⟩=⟨ _value_ ⟩ pairs. The following options are possible: 

  * • duration=⟨ _seconds_ ⟩. Specifies the number of ⟨ _seconds_ ⟩ the transition effect needs. Default is one second, but often a shorter one (like 0.2 seconds) is more appropriate. Viewer applications, especially Acrobat, may interpret this option in slightly strange ways. 

  * • direction=⟨ _degree_ ⟩. For “directed” effects, this option specifies the effect’s direction. Allowed values are 0, 90, 180, 270, and for the glitter effect also 315. 




article

All of these commands are ignored in article mode. 

`\transblindshorizontal`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide as if horizontal blinds were pulled away.

_Example:_ \transblindshorizontal

`\transblindsvertical`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide as if vertical blinds were pulled away.

_Example:_ \transblindsvertical<2,3>

`\transboxin`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by moving to the center from all four sides.

_Example:_ \transboxin<1>

`\transboxout`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by showing more and more of a rectangular area that is centered on the slide center. 

_Example:_ \transboxout

`\transcover`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by covering the content that was shown before.

_Example:_ \transcover

`\transdissolve`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by slowly dissolving what was shown before.

_Example:_ \transdissolve[duration=0.2]

`\transfade`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by slowly fading what was shown before.

_Example:_ \transfade

`\transfly`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by letting the new content fly in before removing the old slide. 

_Example:_ \transfly[direction=180]

`\transglitter`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide with a glitter effect that sweeps in the specified direction. 

_Example:_ \transglitter<2-3>[direction=90]

`\transpush`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by pushing what was shown before off the screen using the new content. 

_Example:_ \transpush

`\transreplace`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Replace the previous slide directly (default behaviour).

`\transsplitverticalin`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by sweeping two vertical lines from the sides inward. 

_Example:_ \transsplitverticalin

`\transsplitverticalout`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by sweeping two vertical lines from the center outward. 

_Example:_ \transsplitverticalout

`\transsplithorizontalin`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by sweeping two horizontal lines from the sides inward. 

_Example:_ \transsplithorizontalin

`\transsplithorizontalout`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by sweeping two horizontal lines from the center outward. 

_Example:_ \transsplithorizontalout

`\transwipe`<⟨ _overlay specification_ ⟩>[⟨ _options_ ⟩]

Show the slide by sweeping a single line in the specified direction, thereby “wiping out” the previous contents. 

_Example:_ \transwipe[direction=90]

You can also specify how _long_ a given slide should be shown, using the following overlay-specification-aware command: 

`\transduration`<⟨ _overlay specification_ ⟩>{⟨ _number of seconds_ ⟩} 

In full screen mode, show the slide for ⟨ _number of seconds_ ⟩. If zero is specified, the slide is shown as short as possible. This can be used to create interesting pseudo-animations. 

_Example:_ \transduration<2>{1} Notice that the _duration_ of a slide transition is entire separate from the _type_ of transition which takes place. Most notably, to cancel an existing auto-advance you need to use 

_Example:_ \transduration{} possibly with an overlay specification. 
