## compiler Design Notes
- The machine-language target program produced by a compiler is usually
much faster than an interpreter at mapping inputs to outputs . An interpreter,
however, can usually give better error diagnostics than a compiler, because it
executes the source program statement by statement.
- Java language processors combine compilation and interpreta-
tion, as shown in Fig. 1.4. A Java source program may rst be compiled into
an intermediate form called bytecodes . The bytecodes are then interpreted by a
virtual machine. A bene t of this arrangement is that bytecodes compiled on
one machine can be interpreted on another machine, perhaps across a network.
In order to achieve faster processing of inputs to outputs, some Java compil-
ers, called just-in-time compilers, translate the bytecodes into machine language
immediately before they run the intermediate program to process the input.

 ## LExical analyser
 - It scanneas the source  program into tokens into <tokens-attr,tokens-points>.
 it stores all informations in symbol tables.
 ### syntax analyer
 - It uses the tokens generated by the  lexical analyser to form grammitical tree.

 ### Semantic analyers
 - The semantic analyzer uses the syntax tree and the information in the symbol
table to check the source program for semantic consistency with the language
de nition.
- An important part of semantic analysis is type checking , where the compiler
checks that each operator has matching operands.

## syntax analyser
- LL and LR gram-mars, are expressive enough to describe most of the syntactic constructs in modern programming languages.
- Parsers for the larger class of LR grammars are usually constructed using automated tools.

## Top -down parser

- Top-down parsing can be viewed as the problem of constructing a parse tree for
the input string, starting from the root and creating the nodes of the parse tree
in preorder (depth- rst, as discussed in Section 2.3.4). Equivalently, top-down
parsing can be viewed as nding a leftmost derivation for an input string.

eg: id+id*id;
       G: E->TE'
          E'->+T|e
          T->FT'
          T'->*F|e
          F->(E)|id   
           ---
              `
                            The class of grammars for which we can construct predictive parsers looking
                                k symbols ahead in the input is sometimes called the LL ( k ) class.
1)   E                      `
    /  \
  
   T    E'
   /\  / \ 
       +  T
          /\
         F  T'
         |   / \
             *  F 
         id      |
   F             id
   |
   id

## LL(1)
 - left to right and left recursive left derivation  with 1 look head 
 - LL(1) parsers shouldn't have common first in the E->A/B
 where A/B
 take first of(A) first(B) and do their intersecion .


 ##  Bottom up parser 
###  Handle pruning
-

### Conflicts During Shifts-Reduce Parsing
- There are context free grammar  which shift - reduce parsing cannot be used.

- Every shift-reduce parser for such a grammar can reach a con guration in which
the parser, knowing the entire stack and also the next k input symbols, cannot
decide whether to shift or to reduce (a shift/reduce con ict ), or cannot decide.

### LR Parsers
- The most prevalent type of bottom-up parser today is based on a concept called
LR( k ) parsing; the \L" is for left-to-right scanning of the input, the \R" for
constructing a rightmost derivation in reverse, and the k for the number of
input symbols of lookahead that are used in making parsing decisions. The
cases k = 0 or k = 1 are of practical interest, and we shall only consider LR
parsers with k  1 here. When ( k ) is omitted, k is assumed to be 1
->[drag](E.jpg)


## To determine LR PArsers 
---
 - METHOD:
1. Construct C'={I0,I1,....In}, the collection of sets of LR(1) items for
G 0 .
2. State i of the parser is constructed from I i . The parsing action for state
i is determined as follows.
(a) If [ A -> x a ; b ] is in I i and GOTO ( I i ; a ) = I j , then set ACTION [ i; a ]
to \shift j ." Here a must be a terminal.
(b) If [ A ->  ; a ] is in I i , A 6 = S 0 , then set ACTION [ i; a ] to \reduce
A -> ."
(c) If [ S 0 -> S  ; $] is in I i , then set ACTION [ i; $] to \accept."
If any con icting actions result from the above rules, we say the grammar
is not LR(1). The algorithm fails to produce a parser in this case.