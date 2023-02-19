# J Playground


## Ramblings

#### Testing for Equality
`=` works on items of an array
To compare if 2 pieces of data are equivalent, use the `"Match"` function, `-:`

```j
0 1 2 = 0 0 0
1 0 0

0 1 2 = 0 1 2
1 1 1

0 1 2 -: 0 1 2
```


J maps lots of concepts to numbers.
For example, 

#### Types
noun        =: 0  
adverb      =: 1  
conjunction =: 2  
verb        =: 3  
monad       =: 3  
dyad        =: 4  
*(and defining functions for posterity)*  
def         =: :  
define      =: : 0  

#### Foreign Conjunctions
Apply integer scalar left and right arguments to the conjunction !:  
to produce verbs of the following categories:
0!:   Scripts  
1!:   Files  
2!:   Host  
4!:   Names  
5!:   Representation *(produces an adverb)*  
6!:   Time  
7!:   Space  
8!:   Format  
9!:   Global Parameters  
13!:  Debug  
15!:  Dynamic Link Library  
18!:  Locales  
128!: Miscellaneous

Let's dive into some of these.

##### Scripts 0!: y
- `0!:k y`
  - *k* is 3 digits of 1 or 0
  - `000`             means 'from file or noun','stop on error','silent'
  - `111`             means 'from noun','continue on error', 'display'
  - `0!:110 someNoun` means execute `someNoun`, complete it, and stay silent

And there are 2 special cases for tautologies:
- `0!:2 y`
  - stops if any non-assigned noun result is not all 1
- `0!:3 y`
  - returns a 1 if each non-assigned noun results is all 1, otherwise returns 0


##### Host 2!: y
`2!:0 y`   **HOST** The list `y` is executed by the host system. Example: `2!:0 'echo $PWD'`  
`2!:1 y` **SPAWN** spawns a process but yields `''` instead of waiting for the process to finish. Output is ignored. Example: `2!:1 'nvim'`
`2!:3 y`   **WAIT** Wait for pid `y` to terminate. The result is the status code returned by the process.  
`2!:5 y`  **GETENV**  Result is the shell environment variable named `y` or 0 if it doesn't exist.
`2!:55 y`  **TERMINATE SESSION** `y` is an integer return code  


