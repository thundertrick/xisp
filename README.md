# Xisp
A simple lisp style language. Easy to be parsed in other languages. Xisp works like a USB memory stick that be easily parsed and embedded in any other language.

## 1. Target
Xisp is developed for sending executable logic across devices, which might be Android or iOS. Xisp is designed short, simple and easy to be parsed. Xisp **only** deals with basic operators and structures. Any complex things should be  implemented by the language who parses Xisp.

## 2. Grammar
~~~
; After a ';', this is comment
(operator, val1, val2, ...) ; returns the result val
~~~
### 2.1 Structures
1. Constants

 ~~~lisp
1, 2, 3... ; Integer
1.2f       ; Float / Double
{1, 2}     ; Array
0/not 0    ; Boolean
"c"        ; Char
"Strings"  ; String
~~~

2. Operators

 ~~~lisp
! ++ -- ~  ; 1 val operator
+-*/%~><   ; 2 val operator
~~~

3. Functions:
 Function name should avoid key words, or xisp will stop running. See more in 2.3 Illegal Usage.
 
 ~~~lisp
 (def, f, (+, a, b))  ; Define a function `f(a, b) -> a + b`
 (f, 1, 2)            ; Returns 3
 ~~~
 
4. OO: `.` and `this` is used to interact with OO languages

 ~~~
 ; with java
 (Log.d, "TAG", this.testStr)
 ~~~
 

### 2.2 Key words & Usages
1. Defination: `def`

 ~~~lisp
	; Example for 'def'
	(def, a)               ; Assign a val named a
	(def, b, 1)            ; Assign a val named b, and init with 1
	(def, f, (+, a, b))    ; Define a function `f(a, b) -> a + b`, note all unassigned val will be treated as inputs for the function
	~~~ 

2. Release: `rls`

 ~~~lisp
	; Example for 'rls'
	(rls, a)    ; Release val a
	(rls, f)    ; Release function f, the name can be used to other things
	~~~

3. Loops: `for`

 ~~~lisp
	; Example for 'for'
	(for,
	  (def, a, 1),  ; a = 1
	  (>, a, 10),   ; if a > 10, stop loop
	  (++, a)       ; a++ in every loop 
	)
	(rls, a)
	~~~

4. Conditions: `if`

 ~~~lisp
	; Example for 'if'
	(if,
	  switch,                     ; if (switch) {
	  (=, switch, (~, switch)),   ;    toggle switch
	  ()                          ; } else { do nothing }
	)
	~~~

5. Exceptions: `try`

 ~~~lisp
 (try,
   (def, def),                          ; Try exp  : Try some dangerous things
   (log, "Error: override key words")   ; Catch exp: Do if something is wrong
 )
 ~~~
 
6. Print: `log`
 
 ~~~lisp
 (log, "hello world") ; print hello world
 ~~~ 

### 2.3 Illegal usages
In all usages in this section, Xisp will stop running and go to the nearest catch exp if avaliable.

1. Override key words:

 ~~~lisp
 (def, def)
 ~~~
 
2. Too less inputs:

 ~~~lisp
 (+, 1)
 ~~~
 
3. Too more inputs:

 ~~~lisp
 (+, 1, 1, 1)
 ~~~
 
4. Undefined val:
 
 ~~~lisp
 (++, a)
 ~~~