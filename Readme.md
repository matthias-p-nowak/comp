# Idea

Arithmetic encoding uses a limited fractional number of bits to encode each symbol. 
The alphabet consists of literal symbols, commands to the decoder, and references to stored phrases. 
The alphabet can change dynamically. 

## Symbols and alphabet

Both the encoder and decoder keep a tab on the likelilyhood of symbols.
In principle, they are represented by an empirical distribution. Each symbol has an integer weight.


## How it works

Consider the interval [0,1) to be the root of a tree. 
This interval can be divided according to the weights and total sum of all weights. 
Those are the children of the root, each has its own interval [a,b). 
The length b-a equals the weight of the symbol divided by the total sum of weights.
Each of those intervals can be divided again. 
In this way, an infinite tree can be constructed, each node denoted by an interval [a,b).
The path in the tree corresponds to a sequence of symbols.
If the length of the sequence is known beforehand or there exist an end symbol, 
then one can encode a finite sequence.

### Rational numbers

The usual explanation runs with decimal numbers, where the weights conveniently fit the schema.
A real implementation has to deal with restricted precision.
Either both the encoder and the decoder make the same numerical errors, 
or the intervals are slightly reduced in order to deal with the limited precision.

This implemention uses rational numbers: nominator and denominator.
When those numbers get too big, they need to get smaller again. 

### Intervals

The input and output of bits creates intervals based on fractions with powers of 2. 
The encoded symbols however create fractions with products, each factor being the total sum of weights at that stage.
Hence, the common denominator contains both factors from the binary side and from the symbol side.
