program → statement program'

program' → statement program'
          | ε

statement → import-statement
           | selection-statement
           | iteration-statement
           | function-definition
           | variable-definition
           | expression-statement

import-statement → "import" identifier import-target ";"

import-target → "." identifier import-target'
import-target' → "." identifier import-target'
                | ε

selection-statement → "if" "(" condition ")" "{" statement "}" else-statement

else-statement → "else" "{" statement "}"
                | "else" if-statement
                | ε

if-statement → "if" "(" condition ")" "{" statement "}" else-statement

iteration-statement → for-loop-statement
                     | foreach-loop-statement

for-loop-statement → "for" "(" for-init-statement for-condition for-expression ")" "{" statement "}"

for-init-statement → ε
                    | init-declaration-statement

for-condition → ε
               | expression

for-expression → ε
                | expression

foreach-loop-statement → "foreach" "(" foreach-variable "in" foreach-collection ")" "{" statement "}"

foreach-variable → data-type identifier foreach-variable'

foreach-variable' → ε
                   | "[" identifier-list "]"

foreach-collection → identifier
                    | expression

function-definition → data-type identifier "(" parameter-list ")" compound-statement

parameter-list → ε
                | parameter-declaration parameter-list'

parameter-list' → "," parameter-declaration parameter-list'
                 | ε

variable-definition → data-type identifier variable-definition'

variable-definition' → "=" initializer
                      | ε

expression-statement → expression ";"

expression → assign-expr expression'

expression' → "," assign-expr expression'
             | ε

assign-expr → conditional-expr assign-expr'

assign-expr' → assign-operator init-clause assign-expr'
              | ε

conditional-expr → logical-or-expr conditional-expr'

conditional-expr' → "?" expression ":" assign-expr conditional-expr'
                   | ε

logical-or-expr → logical-and-expr logical-or-expr'

logical-or-expr' → "||" logical-and-expr logical-or-expr'
                  | ε

logical-and-expr → inclusive-or-expr logical-and-expr'

logical-and-expr' → "&&" inclusive-or-expr logical-and-expr'
                   | ε

inclusive-or-expr → exclusive-or-expr inclusive-or-expr'

inclusive-or-expr' → "|" exclusive-or-expr inclusive-or-expr'
                    | ε

exclusive-or-expr → and-expr exclusive-or-expr'

exclusive-or-expr' → "^" and-expr exclusive-or-expr'
                    | ε

and-expr → equality-expr and-expr'

and-expr' → "&" equality-expr and-expr'
           | ε

equality-expr → relational-expr equality-expr'

equality-expr' → "==" relational-expr equality-expr'
                | "!=" relational-expr equality-expr'
                | ε

relational-expr → shift-expr relational-expr'

relational-expr' → "<" shift-expr relational-expr'
                  | ">" shift-expr relational-expr'
                  | "<=" shift-expr relational-expr'
                  | ">=" shift-expr relational-expr'
                  | ε

shift-expr → add-expr shift-expr'

shift-expr' → "<<" add-expr shift-expr'
             | ">>" add-expr shift-expr'
             | ε

add-expr → mul-expr add-expr'

add-expr' → "+" mul-expr add-expr'
          | "-" mul-expr add-expr'
          | ε

mul-expr → cast-expr mul-expr'

mul-expr' → "*" cast-expr mul-expr'
           | "/" cast-expr mul-expr'
           | "%" cast-expr mul-expr'
           | ε

cast-expr → unary-expr
           | "(" type-id ")" cast-expr

unary-expr → unary-operator postfix-expr
            | postfix-expr

unary-operator → "*"| "&"| "+"| "-"| "!"| "~"

postfix-expr → primary-expr postfix-expr'

postfix-expr' → "(" [ expr-list ] ")" postfix-expr'
               | "." identifier "(" [ expr-list ] ")" postfix-expr'
               | ε

primary-expr → literal
              | identifier
              | "(" expression ")"

literal → integer-literal
         | floating-point-literal
         | char-literal
         | string-literal
         | boolean-literal

integer-literal → decimal-literal

floating-point-literal → digit-seq [ "." digit-seq ]

decimal-literal → nonzero-digit decimal-literal'

decimal-literal' → "'" digit decimal-literal'
                  | ε

nonzero-digit → "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

digit → "0" | nonzero-digit

identifier → nondigit identifier'

identifier' → ε
	    	 | (digit | nondigit) identifier'

nondigit → "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n" | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x" | "y" | "z" | "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J" | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T" | "U" | "V" | "W" | "X" | "Y" | "Z" | "_"

data-type → "i32"
		   | "f32"

type-id → type-spec-seq

type-spec-seq → type-spec type-spec-seq'

type-spec → identifier
           | keyword

init-clause → assign-expr

initializer → "=" init-clause
             | "(" expr-list ")"

expr-list → init-list

init-list → init-clause init-list'

init-list' → "," init-clause init-list'
            | ε

condition → expression
