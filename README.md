\documentclass{article}
\usepackage{tikz}
\usetikzlibrary{shapes.geometric, arrows}

\begin{document}

\tikzstyle{startstop} = [rectangle, rounded corners, minimum width=3cm, minimum height=1cm,text centered, draw=black, fill=red!30]
\tikzstyle{process} = [rectangle, minimum width=3cm, minimum height=1cm, text centered, draw=black, fill=orange!30]
\tikzstyle{decision} = [diamond, minimum width=3cm, minimum height=1cm, text centered, draw=black, fill=green!30]
\tikzstyle{arrow} = [thick,->,>=stealth]

\begin{tikzpicture}[node distance=2cm]

\node (start) [startstop] {Start};
\node (register) [process, below of=start] {Claim Registration};
\node (classify) [process, below of=register] {Claim Classification};
\node (policy) [process, below left of=classify, xshift=-2cm] {Policy Check};
\node (damage) [process, below right of=classify, xshift=2cm] {Damage Check};
\node (invalid) [decision, below of=policy, yshift=-0.5cm] {Insurance Invalid?};
\node (exam) [process, below of=damage] {Claims Examination};
\node (recommend) [process, below of=exam] {Settlement Recommendation};
\node (check) [process, below of=recommend] {Senior Claims Check};
\node (ok) [decision, below left of=check, xshift=-2cm] {Claim OK?};
\node (notify) [process, below of=ok] {Notify Settlement};
\node (repeat) [process, below right of=check, xshift=2cm] {Repeat Examination};

\draw [arrow] (start) -- (register);
\draw [arrow] (register) -- (classify);
\draw [arrow] (classify) -| node[anchor=east] {Simple} (policy);
\draw [arrow] (classify) -| node[anchor=west] {Complex} (damage);
\draw [arrow] (policy) -- (invalid);
\draw [arrow] (invalid) -| node[anchor=east] {Yes} (start);
\draw [arrow] (invalid) |- node[anchor=west] {No} (exam);
\draw [arrow] (exam) -- (recommend);
\draw [arrow] (recommend) -- (check);
\draw [arrow] (check) -| node[anchor=east] {Not OK} (repeat);
\draw [arrow] (check) -| node[anchor=west] {OK} (ok);
\draw [arrow] (ok) -- node[anchor=east] {Yes} (notify);
\draw [arrow] (ok) -| node[anchor=west] {No} (repeat);
\draw [arrow] (repeat) |- (exam);

\end{tikzpicture}

\end{document}

