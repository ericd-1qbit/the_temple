\section{Paper Notes - Why does deep and cheap learning work so well?}

1608.08225

Deep Learning in AI is as well understood as learning in the human brain. We

know that certain protocols result in fantastic results in certain tasks, just

like we know that training the human brain with particular methods results in a

specific skill set. But why that is, is not well understood.

  

At the core of the majority of ML algorithm lies the task of approximating an

arbitrary function, i.e. learning a data distribution following some kind of

structure. This gives three main aspects to shed light on:

\begin{itemize}

  \item[Expressibility] Which class of functions can the algorithm represent?

  \item[Efficiency] Which ressources (ressources, free parameters,...) are

        required to represent the a given function? How does this compare to the

        space of overall available arrangements in that class of functions?

  \item[Learnability] How quickly can my algorithm learn the function

        approximation?

\end{itemize}

  

Core question in this paper \emph{How is a NN able to learn and approximate

functions efficiently, if the space of possible functions is exponentially

large?}.

Awesome example: Classifiying pictures with Megapixels into cat or dog

categories. Assume each pixel can take 256 values. This gives a possibility of

$256^{1000000}$ pictures! For each picture, we would like to get a probability

of how cat/dog-like the content is. But this means that we have an arbitray

function covering $256^{1000000}$ probabilites!! A much much greater number than

atoms in the universe ($10^{78}$). But NN usually require only millions of

parameters to approximate this well... Hence the term "cheap".\\

In rough terms, the NN break the available exponential space of parameters down

from $v^n$ to $v\times n$ for $v$ being values and $n$ being the number of

inputs. The NN will only work well on a tiny fraction of the exponential input,

but it turns out that laws of physics ensure that this is the fraction we are

interested in, as the input we are interested in is also just the tiny fraction

of all available inputs. The argument is then, that these subset are very

similar, allowing efficient work on these subsets only.\par

Notation: $p(x|y)$ is a prediction problem - given the class $y$, how do $x$

look like, i.e. what is the pdf. $p(y|x)$ is a classification problem - which

class does a given set of $x$ belong to?

It is natural to understand that $p(x|y)$ would come with simplifications. The

class of cat picture exhibits a certain set of characteristics about $x$ which

reduces the relevant space by much. Generally speaking these characteristics

could be symmetries, localities, polynomial functional dependencies etc.

It's harder to understand how $p(y|x)$ with $y=cat$ would simplify, or how we

could apply generic rules to that...

Steps in paper: 

- reformulate $p(y|x)$ with bayes theorem

- Then do a translation of information theory terms into physics terms!

  introduce hamiltonians.

- End up with an Boltzmann-form expression.
- - introduce shortened notation

- rewrite Bayes theorem in softmax notation

- investigate which Hamiltonians can be approximated. 

- ML and physics focus on Hamiltonians which are symmetric and sparse and often

  of low-order polynomial complexity

- show that one can approximate multiplication efficiently with small nr of

  neurons

- repeated multiplication and addition then approximates any hamiltonian  in

  taylor expansion

- ML and physics focus on Hamiltonians which are symmetric and sparse and often

  of low-order polynomial complexity

- examples of hamiltonians indeed only range up to small dimensionality! SM

  Hamiltonian has dimensionality of 4, for example.

- locality argument stating that for physical systems only local, neighbouring

  connections have effect

- symmetries like rotational invariance and others reduces number of parameters

  

\paragraph{What causes deep learning to improve performance?} Or in other words,

what underlying structure of data distributions in the real world cause an

imporvement in NN performance when additional layers are added?

The papers argument involves the hierarchical underlying structure in any

generative process. This follows a Markovian Chain - the state of a system is

determined by its causal predecessor state alone and a transition matrix between

the states. This is iterative.

THe argument then is, that a NN with multiple layers can approximate any

hierarchical structure which can be decomposed. These are ubiquitous in the

physical world, everythiong can be seen from a hierarchical standpoint and

decomposed intop simpler substructures. Each of these substructures can be

approximated by the layers in the NN.

  

\subsection{Questions}

\begin{itemize}

  \item Where does "Deep" start in Machine learning?

  \item Why is $p(y|x)$ much harder to understand/assign 

  \item Where does divident in Equ. (1) come from? This is an expression for

        $p(x)$. Is that what's called marginalisation?

  \item What exactly does the locality argument state? Couldn't one create a

        counterexample in some image recognition case eg?

  \item What's a Markov Chain?

  \item How is that locality argument anything really? Relation to ML? even in

        physical world: Would it not be possible to have a macro effect from

        non-local influences?

\end{itemize}

\subsection{Insights}

\begin{itemize}

  \item 

\end{itemize}