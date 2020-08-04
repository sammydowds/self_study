[Original Turing Paper](https://www.cs.virginia.edu/~robins/Turing_Paper_1936.pdf)

## Studying Turing's Earlier Work 

### "On Computable Numbers, With an Application to Entscheidungsproblem"

Definition: A number is computable if its decimal can be written down by a machine. 

#### What is the Entscheidungsproblem?
The problem asks for an algorithm that considers, as input, a statement and answers "Yes" or "No" according to whether the statement is *universally valid*, i.e., valid in every structure satisfying the axioms. 

Definition of Axioms: a statement or propostion which is regarded as being establish, accepted, or self-evidently true. 

#### Back to the Paper 

Sections 1-2 seem to layout how this machine would work, and lays out definitions for what the machine is doing. Section 3 gets into examples. 

##### First example: 
A machine can be constructed to compute the sequence of 010101... . The machine is to have four m-configurations "b", "c", "f", "e" and is capable of printing "0" and "1". 

Table for example (first two columns = Configuration, last two = Behavior): 

| m-config | symbol | operations | final m-config |
| --- | --- | --- | --- |
| b | None | P0, R | c |
| c | None | R | e |
| e | None | P1, R | f |
| f | None | R | b |

*P = Print, R = scans immediately to the right*

[Visualizing The Above Table](https://www.youtube.com/watch?v=dNRDvLACg5Q)





