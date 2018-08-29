GADTs basically allow you to describe richer relations between your data constructors and the type they inhabit.
If you have a parameterized type T with constructors C1 and C2, anytime you receive some t of the type T a, you need to provide code to handle both C1 and C2, because t could be either of these.
Knowing which constructor has been used to build t does not tell you what the parameter a is.
Knowing what concrete parameter has been used for a does not tell you which constructors you're going to find in t.
This is sometimes frustrating when certain parts of your code should really only care some constructors, but the system wants you to care about all of them (or it will complain that you are not exhaustive).
GADTs allow you to constrain, for each constructor of a datatype, the value of parameters in its type. Instead of all the constructors having the same type T a, they can choose to constrain this a. For instance, maybe C1 : T int and C2 : T float. Now this allows two things:
Pattern-matching now unveils information about type parameters (or type indices as we rather call them). For instance, I can write this function:
z : T a -> a
z C1 = 0   (* since we match C1 of type T int, we discover that a = int *)
z C2 = 0.0 (* since we match C2 of type T float, we discover that a = float *re)
Indicating restrictions in the input type allows you to avoid treating irrelevant constructors:
f : T int -> int
f C1 = 42
(* this pattern matching *is* exhaustive *)
Combining these two things gives you great flexibility. Probably the best thing to do is to try and play a bit with it though.
The canonical tutorial is to try and define a small typed language where each element of the language constrains its type. For instance:
IntLiteral :                     term int
Pair       : term a -> term b -> term (a * b)
Fst        : term (a * b)     -> term a
Snd        : term (a * b)     -> term b
and try to write this function:
eval : term a -> a