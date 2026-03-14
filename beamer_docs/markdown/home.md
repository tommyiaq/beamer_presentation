The beamer Document Class 

Manual for Version 3.71

Unofficial HTML Version

This HTML version of the documentation is maintained by Siyu Wu, and is produced with the help of the [lwarp](<https://ctan.org/pkg/lwarp>) package 

Editors of the Beamer documentation: [Till Tantau](<mailto:tantau@users.sourceforge.net>), [Joseph Wright](<mailto:joseph.wright@morningstar2.co.uk>), [Vedran Miletić](<mailto:vmiletic@inf.uniri.hr>)
    
    
    \begin{frame}
      \frametitle{There Is No Largest Prime Number}
      \framesubtitle{The proof uses \textit{reductio ad absurdum}.}
      \begin{theorem}
        There is no largest prime number.
      \end{theorem}
      \begin{proof}
        \begin{enumerate}
        \item<1-| alert@1> Suppose $p$ were the largest prime number.
        \item<2-> Let $q$ be the product of the first $p$ numbers.
        \item<3-> Then $q+1$ is not divisible by any of them.
        \item<1-> Thus $q+1$ is also prime and greater than $p$.\qedhere
        \end{enumerate}
      \end{proof}
    \end{frame}
    
