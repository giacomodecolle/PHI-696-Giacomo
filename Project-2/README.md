# Project 2

# Project 2

Your second project will require you to answer each of the 10 questions below.  You will be expected to open a pull request with your initial answers by the second class meeting, giving you one week to work on these problems. You and your peers will then have one week to work together to refine your respective initial answers, so they are ready for final submission. Once your pull requests have been reviewed and merged to the development branch, I will review them, then merge to the master branch. 

```
Tip #1: Carefully study the Baader, et. al. selections assigned on bisimulation; it is deceptively subtle, and quite powerful. 
Tip #2: Google is still your friend. So is stackexchange...
Tip #3: Work _together_ to solve these problems, even for initial submissions and when you do, document this in github. 
Tip #4: Work together _as a team_. 
```

1. Let V be a vocabulary of ALCI consisting of a role name "P". Interpret part_of as "x is a part of y". Using this role name, define the following formulas in this language:
```Other symbols:∀∃ ⊔ ⊓ ⊧ ⊭ ⊦ ⊬ ⊏ ⊐ ⊑ ⊒ ≡ ¬ → ∨ ∧ ¯ ⊤ ≥ ≤

  (a)  PP that says that x is a proper part of y
  PP ≡ P ⊓ ¬P¯
  This reads something like: a proper part between x and y exists iff 
  x is part of y and it is not the case that the inverse parthood relation ("being a whole of") 
  holds between x and y.
  (b)  iPP that says that y is a proper part of x
  iPP ≡ PP¯
  iPP ≡ ¬P ⊓ P¯
  (c)  iP that says that y has x as part 
  iP ≡ P¯
  (d)  O that says that x overlaps y
  O ≡ ∃iP.(∃P.⊤)
  (e)  D that says that x and y are disjoint 
  D ≡ ¬O
```

2. Use your axioms from question 1 as the basis of an ALCI T-Box. Supplement this T-box with whatever other axioms you like, as well as an A-box, so that you ultimately construct a knowledge base K = (T,A). Provide a _model_ of K. This may be graphical or symbolic or both. 

TBox = {
PP ⊑ P
P ⊑ O
O ⊑ O¯
}

ABox = { 
(Italy, Europe) : P 
Italy : State
(Italy, Italy) : P
(Italy, Europe) : P
(UK, Europe) : ¬ P
UK : State
(UK, UK) : P
(Venice, Italy) : P
(Venice, Venice) : P
(Venice, Italy) : O
(Venice, Europe) : O
Venice : City
(UK, UK) : P
(UK, Italy) : D
(UK, Venice) : D
(London, UK) : P
(London, London) : P
London : City
}

ΔI = {Italy, Europe, UK, Venice, London}

Named Individuals:
EuropeI = E,
ItalyI = I,
VeniceI = V,
UKI = U
LondonI = L

Concept Assignments:
State = {U, I}
City = {V, L}
Sovranational Union = {E}


Role Assignments:
PI = {(I, E), (V, I), (V, E), (V, V), (E, E), (I, I), (L, L), (L, UK), (UK, UK)}
PPI = {(I, E), (V, I), (V, E), (L, UK)}
D = {(L, I), (L, V), (V, UK), (E, UK), (I, UK)}

3. Translate the following first-order logic axioms into ALCI: 
```
(a) ∀x∃y∀z(R(x,y) ∧ R(x,z) ∧ R(y,z))
∃R.(∀R.⊤) ⊓ ∀R.⊤
(b) ∃x∀y∃z(R(x,y) ∧ R(x,z) ∧ R(y,z))
∃R¯.(∃R.⊤) ⊓ ∃R.⊤
Given that DL has an implicit universal quantifier at the beginning, here we decided 
to start from y as subject of the formula, which is universally quantified.
Our strategy to deal with this problem is to address the universal quantifier by inversing
the R(x,y) relation. Since we want x and z to be successors of y,
we have to write the first relation R(x,y) in an inverse format (i.e. R¯). 
(c) ∀y(R(x, y) → ∃x(R(y, x) ∧ ∀y(R(x, y) → A(y))))
∀R.∃R.∀R.A
(d) (∀y)(R(x, y) → A(y)) ∧ (∃y)(R(x, y) ∧ B(y))
(∀R.A) ⊓ (∃R.B)
```
4. Provide an interpretation I<sub>1</sub> for ALC and an interpretation I<sub>2</sub> for ALCN - each distinct from any interpretation covered in class so far - and construct a bisimulation that demonstrates ALCN is more expressive than ALC. Use the [mermaid syntax](https://github.com/mermaid-js/mermaid) of markdown to provide a graphical representation of your work. 


ΔI1 = {Dr. Beverley, PHI 697, PHI 329, Tuesday Workshop}

Named IndividualsI:
Dr. BeverleyI = B
PHI 697I = 697
PHI 329I = 329
Tuesday WorkshopI = W

Role Assignments:
t = {(B, 697), (B, 329), (B, W)}


ΔI2 = {Dr. Beverley, PHI 697, PHI 329}

Named IndividualsI:
Dr. BeverleyI2 = B2
PHI2 697I = 697-2
PHI 329I = 329-2

Role Assignments:
t2 = {(B2, 697-2),  (B, 329-2)}

Bisimulation:

ρ = {(B, B2), (697, 697-2), (329, 329-2)}

So B is bisimilar to B2. But we can distinguish them in ALCN by defining the role m as
≥2 ∃t.⊤
in I1
≥1 ∃t2.⊤
in I2

![Alt text] (https://mermaid.ink/img/pako:eNqNjzELwjAQhf9KuEWFOrSC0g4OUhcnQTfjcCSnKTaJxFQpbf-7KXUQB_VNx_F9PF4DwkqCDE6lfQiFzrN9zg0LyePDxirDVnQnV9ZHNp0uWesJhaJby9bxeKuKebqY_IcnPT5L0gHn5mUl363RZ8sv_q0GItDkNBYy7Gt6n4NXpIlDFk6J7sKBmy5wWHm7q42AzLuKIqiuEj3lBZ4d6uHZPQFU2F5C?type=png)](https://mermaid.live/edit#pako:eNqNjzELwjAQhf9KuEWFOrSC0g4OUhcnQTfjcCSnKTaJxFQpbf-7KXUQB_VNx_F9PF4DwkqCDE6lfQiFzrN9zg0LyePDxirDVnQnV9ZHNp0uWesJhaJby9bxeKuKebqY_IcnPT5L0gHn5mUl363RZ8sv_q0GItDkNBYy7Gt6n4NXpIlDFk6J7sKBmy5wWHm7q42AzLuKIqiuEj3lBZ4d6uHZPQFU2F5C)

5. Provide an interpretation I<sub>1</sub> for ALC and an interpretation I<sub>2</sub> for ALCN - each distinct from any interpretation covered in class so far - and construct a bisimulation that _does not_ demonstrate ALCN is more expressive than ALC. Use the [mermaid syntax](https://github.com/mermaid-js/mermaid) of markdown to provide a graphical representation of your work. 

ΔI1 = {Dr. Beverley, PHI 697, PHI 329, Tuesday Workshop}

Named IndividualsI:
Dr. BeverleyI = B
PHI 697I = 697
PHI 329I = 329


Role Assignments:
t = {(B, 697), (B, 329)}


ΔI2 = {Dr. Beverley, PHI 697, PHI 329}

Named IndividualsI:
Dr. BeverleyI2 = B2
PHI2 697I = 697-2
PHI 329I = 329-2


Role Assignments:
t2 = {(B2, 697-2),  (B, 329-2)}

Bisimulation:

ρ = {(B, B2), (697, 697-2), (329, 329-2)}

So B is bisimilar to B2. The ALCN definitions are
≥1 ∃m.⊤
in I1
≥1 ∃m2.⊤
in I2

6. Explain the difference - using natural language - between the description logic expressions:
  ```
  (a) ∃r.C and ∀r.C
  The first one reads: there is a thing r-related to all xs, and this thing falls under concept C
  The second one reads: if there is a thing r-related to all xs, this thing falls under concept C
  (b) ∃r-.C and ∀r-.C
  The first one reads: there is a thing r-related to all xs, and this thing falls under the reverse of concept C
  The second one reads: if there is a thing r-related to all xs, this thing falls under the reverse of concept C
  (c) <=nr and <=nr.C
  The first one reads: role r connects all the xs to no more than n elements.
  The second one reads: role r connects all the xs to no more than n elements, and they fall under concept C.
  (d) ∃r-.C and ∃r-.{a} 
  The first one reads: for all xs, there is at least a thing y, which is C-reverse related to it, and which falls under concept C.
  The second one reads: for all xs, there is element a, which is C-reverse related to it.
```

7. There is a delightfully helpful subreddit called "ELI5" which stands for something like "explain it like I'm 5" where users post conceptually challenging questions and other users attempt to provide explanations in simple, jargon-free, terms that presumably a 5 year-old could understand. Using this as a model, explain the _finite model property_. Be sure to provide a simple example and explain when the property might be important, and when it is not so important. 

The finite model property means that if you want to prove something in a game or puzzle, 
you don't have to use too many toys or blocks,just a few of them will be enough. 
This makes it easier to solve the game or puzzle and saves time.
Suppose you have a game with two toy animals, a cat and a dog. The rules of the game are 
that the cat is always hungry, and the dog is always friendly. You want to prove that 
if the cat is hungry, then the dog is not hungry.
One way to prove this would be to use all the possible combinations of hunger and friendliness 
for the cat and the dog, which would require an infinite number of possibilities. 
But because the game has the finite model property.

8. Following up on the preceding , explain the _tree model property_. Be sure to provide a simple example and explain when the property might be important, and when it is not so important. 

Imagine you have a toy with lots of buttons and levers. When you press a button or pull a lever,
the toy changes in some way. The finite tree model is like a picture of all the different ways 
the toy can change.
Each picture shows the toy in a different state, with some buttons and levers pressed and 
others not pressed. The lines between the pictures show how the toy changes when you press a 
button or pull a lever.
By looking at all the pictures together, you can see all the different ways the toy can change, 
and how it changes from one state to another. This can help you understand how the toy works 
and how to use it.

An example:Imagine you're playing a game where you have to guess a number between 1 and 10.
The game will tell you if your guess is too high or too low, and you have to keep guessing
until you get the right answer.
We can represent this game as a finite tree model. The starting point is when you make your 
first guess, which is like the "root" of the tree. Depending on whether your guess is too high 
or too low, the tree branches off into two different paths.
If your guess is too high, you go down one path where you make a lower guess. 
If your guess is too low, you go down the other path where you make a higher guess. 
This branching continues until you finally guess the right number, which is like reaching
a "leaf" node in the tree.
By using the finite tree model to represent the guessing game, we can see all 
the different possible paths that the game can take, and how the game progresses 
from one guess to the next.
In the same way, the finite tree model helps people understand how programs and processes 
work by showing all the different ways they can change and how they change from one state to 
another.


9. Open the Protege editor and create object properties for each of the role names that 
you constructed in question 1. You should have at least 6 object properties.
Assert in the editor that P is a sub-property of O, that P is transitive, 
and that O is symmetric. Next, add individuals - a, b, c - 
to the file and assert that c is part of a and that c overlaps b. 
Running the reasoner should reveal - highlighted in yellow if you select the individual c - 
that c overlaps a. Using the discussion in the selections from chapter 4 of the Baader,
et. al. text as a guide, explain how the tableau algorithm is generating this inference. 






10. Following up on your work in question 9, adjust/add/remove/etc. object properties
and individuals in your Protege file so that when you run a reasoner in Protege, you return 
the following consequences: 
```
  (a) a is a proper part of b and disjoint from e
  (b) a overlaps c
  (c) a is part of b, b is part of f, and a is part of f
  (e) There are no parts between a and g in common
```
