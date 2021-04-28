## Games, classically
### Slide 1

Informal definition: 
> Game theory is the mathematical study of interaction among independent, self-interested
agents.
-- EoGT

Examples:
1. Tic-tac-toe, chess, Monopoly, etc.
2. Economic games (includes/are included in: ecological games)
3. Social dilemmas (PD, 'tragedy of the commons', etc.)
4. Proof theory, model theory, etc.
5. Machine learning
6. _etc._

### Slide 2
Two ways of representing a game:
1. Normal form:
There is a set of players P, and indexed set of _actions_ A : P \to Set, and a utility function u : \Pi A \to P \to R
(PD)
2. Extensive form
There is a set of players P, and a tree representing the unfolding of the game. Nodes are assigned to players and grouped in _information sets_. Branches are called _moves_. _Utility vectors_ are assigned to each leaf.
(PD)

### Slide 3
One can always convert an extensive form game into normal form:
1. Define A p = \Sum_{x \in p's nodes} moves at x
1. Define u(action profile a_1, \ldots, a_n) = u(path a_1, \ldots, a_n) = payoff at the end of the path
The converse is not always possible since normal-form games have too little structural information.

We'll prefer to use extensive form to denote games until we introduce a better one.

### Slide 4
The main goal of a game analysis is to find a _solution_. There are different concepts of what a _solution_ amounts to:

Informal def: a _solution concept_ for a given game is a notion of 'optimal way to play' for all players involved

A 'way to play' for a player is called _strategy_. A strategy is a choice of move at every stage of the game:
\Omega p = \Prod_{x \in p's nodes} moves at x
^ strategies of player p
compare it with
A p = \Sum_{x \in p's nodes} moves at x
Key difference: strategies are a _comprehensive plan of action_: for each _state_ of the game, no matter how unlikely, we plan an _action_.

A choice of strategy for each player is a _strategy profile_
\Sigma = \Prod_{p \in P} \Omega p

### Slide 5
The most important (and general) solution concept is _Nash equilibrium_:

Def. A strategy profile \Sigma is a Nash equilibrium if no player can obtain a higher payoff by unilaterally changing their own strategy:

u_i(s[s_p/s'_p]) \leq u_p(s) for all p

It's not the only one: SGP, ESS, \varepsilon-Nash, trembling hand, etc.
Afaik, all are _refinements_ of Nash.

### Slide 6
Problems with classical game theory:
1. Traditionally, games are treated monolithically: one defines _a_ game (or _the_ game) all at once, and treats reuse/composition only informally.
2. Mathematically quite clunky: it's basically stuck in early 20th century mathematical language
3. Denotations for normal form and extensive form are quite disappointing: normal form is too opaque, extensive form is too... extended

Open games are a proposed improvement to (1)-(3)
1. Defined compositionally, and can be formally and easily composed and mutated
_This includes, most importantly, equilibria_
2. Mathematically more sophisticated (grounded in category theory)
3. Elegantly denoted by string diagrams, hence halfway between normal and extensive form

Follows the ACT tradition of 'opening up' systems: always consider a system as part of an environment which interacts non-trivially

## Open games
### Slide 7
Warning: Open games are compositional structures, hence the single building blocks do not make much sense from a classical standpoint -- you have to put them together to get something meaningful

Informally: an 'atomic' open game is a forest of bushes
(pic)

### Slide 8
First of all, let's model the information flow of a game.
(pic of a tree)
There's two phases in a game
1. The 'play' or 'forward phase': players takes turn and make their own decisions until a leaf is reached
2. The 'coplay' or 'backward phase': payoffs propagate back to player along the tree

The backward phase is done for analysis purposes: we observe how different decisions would bring about different payoffs (_backward induction_)

### Slide 9
A _lens_ models exactly this bidirectional information flow:

(pic of a lens)

Slogan: '_Time flows clockwise_'

Def. Let C be a cartesian category (think: sets & functions). A lens (X,S) \to (Y,R) is a pair of maps
view : X \to Y
update : X \times R \to S

The _view_ is the forward step, the _update_ is the backward step. 

### Slide 10
So a game can be represented naively as a lens (X,S) \to (Y,R) where
...X are 'states of the game'
...Y are 'moves'
...R are 'utilities'
...S are 'coutilities'

In open games we call the forward part of a lens 'play' and backward part 'coplay'

### Slide 11
What's coutility?

> For a given node x in a game, a player’s continuation value (also called
continuation payoff) is the payoff that this player will eventually get
contingent on the path of play passing through node x.
-- Strategy - Watson

The coplay function takes on this job. In classical game theory it's hidden in backward induction.
It doesn't _have to_ be trivial, but it often is.

### Slide 12
Lenses, hence games, can then be composed in at least two ways:

(sequential)

(parallel)

### Slide 13
We can use sequential composition to give a lens a _context_, i.e. an initial _state_ and a _payoff function_

(pic)

Remember: '_time flows clockwise_'

### Slide 14
What's missing?

> What does it mean to say that agents are self-interested? [...] [I]t means that each agent has **[their] own description** of which **states of the world [they like]**—which can include good things happening to other agents—and that **[they act]** in an attempt to bring about these states of the world.
EoGT

Three things:
1. A way for agents to _act in the world_
2. A way for agents to _represent the world_
3. A way for agents to _evaluate the world_

At the moment, agents do not intervene in the unfolding of the game: plays and coplays are fixed 

We need to give a 'steering wheel' to agents:

### Slide 15
Interlude I: the Para construction

Para originates in [backprop as a functor] an has been adopted by this group (Bruno) to represent all sort of stuff. Also Toby Smithe has come up with a Para-like construction, Proxy.

### Slide 16

Def. When C is symmetric monoidal, Para(C) is the category of parametrized morphisms of C:
- objects are the same
- a morphism A -> B is given by a choice of parameter P : C and a choice of morphism P \otimes A \to B in C:

(pic of para morphism)

### Slide 17
Para(C) is again symmetric monoidal:

(pic of seq comp)

(pic of par comp)

and, most importantly, it's a _bicategory_

(pic of 2-cell)

### Slide 18
Now, if our morphisms are `bidirectional', we get an even more interesting picture:

(pic of para optic)

If we peek inside, we can see the new information flow:

(pic of para lens, opened up)

### Slide 19
Idea: if 'games without agency' are lenses, 'games with agency' are parametrized lenses:

- parameters are _strategies_: the ways an agent _acts_ in the world
- coparameters are _'costrategies'_: the ways an agent _represent_ the world

The only piece still missing is ways for agents to _evaluate_ the world.

### Slide 20
Interlude II: selection functions

Def. A _continuation_ on a object X with scalars an object R is a map

K_R(X) = (X \to R) \to R

It's a `generalized quantifier':

Examples: max, min, \exists, \forall
If the ambient category is cartesian closed, K_R defines a monad (the continuation monad)

### Slide 21
Selection functions `realize' quantifiers: 

Def. A _selection function_ on a object X with scalars an object R is a map

J_R(X) = (X \to R) \to X

Examples: argmax, argmin, Hilbert's \varepsilon

If the ambient category is cartesian closed, J_R defines a monad (the continuation monad)

### Slide 22
Notice: often quantifiers can be realized by multiple elements...

(ambiguous max function)

So a better type for selection functions is

(X \to R) \to PX

where P is the powerset monad.

### Slide 23

Also notice:

(X \to R)           \to   P  X
^ costate of (X,R)           ^ state of (X,R)

so we arrive to a general definition:

Def. Let C be a monoidal category. Then the selection functions functor is
given by 
Sel : C \longto \Cat
X \mapsto C(X, I) \to PC(I,X)

(pic of \varepsilon(costate) = state)

The codomain is Cat since this set is ordered by pointwise inclusion:

\varepsilon \leq \varepsilon' \sse \forall k \in C(X,I), \varepsilon(k) \subseteq \varepsilon'(k)

### Slide 24
Sel is a functor because it also acts on morphism by _pushforward_:

(pic from wiki)

Idea: selection functions are a relation between states and costates

### Slide 25
Finally, Sel is _lax monoidal_ with the _Nash product_:

\boxtimes : Sel(X) \times Sel(Y) \to Sel(X \otimes Y)
....

### Slide 26
To see why we call this the Nash product, let's go back to games...

(pic of para optic)

At this point, we only miss one piece of data:
3. A way for agents to _evaluate the world_

Idea: for each player, we pick a selection function
\varepsilon \in Sel(\Omega, \Comega)
to model their preferences

### Slide 27
Now, careful. Recall:

> Game theory is the mathematical study of **interaction** among independent, self-interested
**agents**.
-- EoGT

A game factors in two parts
1. An _arena_, which models the _interaction patterns_ in the game
2. A set of _agents_, i.e. the players, which make _decisions_ at different points of a game

Without (2) a game would be only a _dynamical system_, whose dynamic is fixed.
Instead, in a game agents can vary the dynamics in response to the expected unfolding of the interaction.

### Slide 28

(pic: para optic with arena and agents areas highlighted)

Lenses model dynamical systems (see also: DJM, Spivak, Schultz, Vasilakopoulou, etc.)
Parametrized lenses model cybernetic systems

(Cue: what do parametrized ... parametrized lenses model?)

### Slide 29
Therefore: _agents live in the parametrization direction_
The arena plays the role of a costate to them:

(pic of \top action)

### Slide 30
Finally, if _arenas_ can be defined 'locally' because they are information plumbing, _agents' interests_ can't since they are defined 'globally': an agent might observe and interact with the arena at multiple, causally 'far' points.

We take advantage of the 2-cells in Para(Lens) to handle this:

(pic)

### Slide 31
Great! So an open game is

1. A parametrized lens
(X, S) \nto{(P, P')} (Y,R)
2. A set of players {1, ..., n} represented by a choice of selection function
\varepsilon_i \in Sel(\Omega_i, \Comega_i)
for each
3. A _wiring 2-cell_
w : \Prod_{i \in I} (\Omega_i, \Comega_i) \to (P,P')

Equilibria are given by

eq(x,u) = (\varepsilon_1 \boxtimes \cdots \boxtimes \cdots \varepsilon_n)(w ; (x ; G ; u)^\top)

It can be shown that this definition is compositional in the natural way, and recovers Nash equilibria as an equilibrium concept (which justifies calling \boxtimes _Nash product_)

### Slide 32
This solves long-standing problems with open games:

1. We finally compute ther _right set of Nash equilibria_
2. We can handle situations of imperfect recall
3. We can define internal choice
3. We can even model coalitional games (WIP)

Still a lot to explore.

## Cybernetics
### Slide 33
I struggled to keep this presentation on games, but we believe this framework is actually bound to become the categorical foundation of **cybernetics** (_κυβερνάω_: to govern, to steer):

> Science concerned with the study of systems of any nature which are capable of receiving, storing and processing information so as to use it for control.
-- Kolmogorov

The missing bits are **storage** and **feedback**.

### Slide 34
Intuitively, agents should first act in the arena, then observe the result of their behaviour, then change their action accordingly, until an equilibrium is reached:

(pic of lens with trace)

This answers also the questions: _where do selection functions come from?_ _where do they enter the (literal) picture?_

### Slide 35
Selection functions are obtained as fixpoints of **delayed traces** [paper].
In fact: **every selection function is a fixpoint selection.**

(pic of costate with gradient descent)

This brings together:
1. Learners: they come already with such a mechanism (Gradient Descent)
2. Games: replace equilibria with _best responses_

### Slide 36
Hence a cybernetic system is:
1. A parametrized lens
(X, S) \nto{(P, P')} (Y,R)
2. A set of players {1, ..., n} represented by a choice of _abstract gradient descent lens_
(pic of GD)
for each
3. A _wiring 2-cell_
w : \Prod_{i \in I} (\Omega_i, \Comega_i) \to (P,P')

(pic: costate, agd, traces)

Equilibria for the system are given by

eq(x,u) = fixpoint(GD ; w ; (x ; G ; u)^\top)

Nash is a consequence of the algebra of fixpoints.










