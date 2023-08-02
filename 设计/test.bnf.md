keyword ::= "import"
    | "i32"
    | "for"
    | "if"
    | "else"
    | "f32"
    | "return"
    | "void"
    | "true"
    | "Yes"
    | "No"
    | "YES"
    | "NO"

operator ::= "`"|"~"|"@"|"#"|"$"|"%"|"^"|"&"|"*"|"("|")"|"<"|">"|"["|"]"|"-"|"="|"+"|"/"|"\"|","|"."|"?"
    | ":"|double_quote|"'"|"+="|"-="|"*="|"/="|"<<"|">>"|"<="|">="|"=>"|"->"|"!"|">>="|"<<="|"&="|"=="
    | "%="|"^="|"|="|"||"|"&&"|";"

digit ::= nonzero-digit|"0"

nondigit ::= "a"|"b"|"c"|"d"|"e"|"f"|"g"|"h"|"i"|"g"|"k"|"l"|"m"|"n"|"o"|"p"|"q"|"r"|"s"|"t"|"u"|"v"|"w"|"x"|"y"|"z"
    | "A"|"B"|"C"|"D"|"E"|"F"|"G"|"H"|"I"|"G"|"K"|"L"|"M"|"N"|"O"|"P"|"Q"|"R"|"S"|"T"|"U"|"V"|"W"|"X"|"Y"|"Z"
    | "_"

identifier ::= id-start identifier'
identifier' ::= id-continue identifier'
              | ε

id-start ::= nondigit

id-continue ::= digit
    | id-start

decimal-literal ::= nonzero-digit decimal-literal'
decimal-literal' ::=  "'" digit decimal-literal'
                  | ε

nonzero-digit ::= "1"|"2"|"3"|"4"|"5"|"6"|"7"|"8"|"9"

name ::= identifier

type-id ::= type-spec-seq

type-spec-seq ::= type-spec
    | type-spec type-spec-seq

type-spec ::= identifier
    | keyword

compound-stmt ::= "{" [stmt-seq] "}"

stmt-seq ::= statement stmt-seq'

stmt-seq' ::= ε
    | stmt-seq statement

statement ::= expr-stmt
    | compound-stmt
    | selection-stmt
    | iteration-stmt
    | jump-stmt
    | decl-stmt

data-type ::= "i32" 
    | "f32" 
    | "void"

expr-stmt ::= [expression] ";"

selection-stmt ::= "if" "(" condition ")" statement selection-stmt'
    
selection-stmt' ::= ε
    | "else" statement
    
iteration-stmt ::= "for" "(" init-stmt [condition] ";" [expression] ")" statement
    
jump-stmt ::= "return" [expression] ";"

decl-stmt ::= decl-spec init-decl-list'; 

init-decl-list' ::= ε
    | "," init-decl-list

decl-spec ::= type-spec

decl-spec-seq ::= decl-spec decl-spec-seq'

decl-spec-seq' ::= ε
    | decl-spec decl-spec-seq'

expression ::= assign-expr expression'

expression' ::= ε
    | "," assign-expr expression'

assign-expr ::= conditional-expr assign-expr'

assign-expr' ::= ε
    | assign-operator init-clause assign-expr'

conditional-expr ::= logical-or-expr conditional-expr'

conditional-expr' ::= ε
    | "?" expression ":" assign-expr conditional-expr'

assign-operator ::= "="
    | "*="
    | "/="
    | "+="
    | "-="

logical-or-expr ::= logical-and-expr logical-or-expr'

logical-or-expr' ::= ε
    | "||" logical-and-expr logical-or-expr'

logical-and-expr ::= inclusive-or-expr logical-and-expr'

logical-and-expr' ::= ε
    | "&&" inclusive-or-expr logical-and-expr'

inclusive-or-expr ::= exclusive-or-expr inclusive-or-expr'

inclusive-or-expr' ::= "|" exclusive-or-expr inclusive-or-expr'
                      | ε

exclusive-or-expr ::= and-expr exclusive-or-expr'

exclusive-or-expr' ::= "^" and-expr exclusive-or-expr'
                      | ε

and-expr ::= equality-expr and-expr'

and-expr' ::= "&" equality-expr and-expr'
            | ε

equality-expr ::= relational-expr equality-expr'

equality-expr' ::= "==" relational-expr equality-expr'
                  | "!=" relational-expr equality-expr'
                  | ε

relational-expr ::= shift-expr relational-expr'

relational-expr' ::= "<" shift-expr relational-expr'
                    | ">" shift-expr relational-expr'
                    | "<=" shift-expr relational-expr'
                    | ">=" shift-expr relational-expr'
                    | ε

shift-expr ::= add-expr shift-expr'

shift-expr' ::= "<<" add-expr shift-expr'
               | ">>" add-expr shift-expr'
               | ε

add-expr ::= mul-expr add-expr'

add-expr' ::= "+" mul-expr add-expr'
            | "-" mul-expr add-expr'
            | ε

mul-expr ::= cast-expr mul-expr'

mul-expr' ::= "*" cast-expr mul-expr'
            | "/" cast-expr mul-expr'
            | "%" cast-expr mul-expr'
            | ε

cast-expr ::= unary-expr
            | "(" type-id ")" cast-expr

unary-expr ::= unary-operator cast-expr
              | postfix-expr

unary-operator ::= "*"
                  | "&"
                  | "+"
                  | "-"
                  | "!"
                  | "~"

init-decl-list ::= init-decl init-decl-list'

init-decl-list' ::= "," init-decl init-decl-list'
                   | ε

init-decl ::= declarator initializer

declarator ::= identifier

initializer ::= "=" init-clause
                | "(" expr-list ")"

expr-list ::= init-list

init-list ::= init-clause init-list'

init-list' ::= "," init-clause init-list'
               | ε

init-clause ::= assign-expr

condition ::= expression
              | decl-spec-seq declarator "=" init-clause

init-stmt ::= expr-stmt
              | decl-stmt

import-target ::= identifier import-target'

import-target' ::= "." identifier import-target'
                  | ε

import ::= "import" import-target ";"

function ::= func-head func-body

func-head ::= data-type identifier "(" param-list ")"

param-list ::= [data-type name param-list']

param-list' ::= "," data-type name param-list'
                | ε

func-body ::= compound-stmt

integer-literal ::= decimal-literal

primary-expr ::= literal
                  | "(" expression ")"
                  | identifier

literal ::= integer-literal
          | char-literal
          | floating-point-literal
          | string-literal
          | boolean-literal

postfix-expr ::= primary-expr postfix-expr'

postfix-expr' ::= "(" expr-list ")" postfix-expr'
                | type-spec "(" expr-list ")" postfix-expr'
                | ε

char-literal ::= "'" (nondigit|digit|"~"|","|"|"|"("|")"|"<"|">"|"{"|"}"
                          |"+"|"-"|"!"|"@"|"#"|"$"|"%"|"^"|"&"|"*"|"="|"\"
                          |"/"|"?"|"."|"`"|":"|" " | "[" | "]") "'"

floating-point-literal ::= digit-seq floating-point-literal'

floating-point-literal' ::= "." digit-seq
                           | ε

digit-seq ::= digit digit-seq'
            | digit-seq' digit

digit-seq' ::= "'" digit digit-seq'
              | ε

string-literal ::= double_quote string-literal' double_quote

string-literal' ::= " " char-literal string-literal'
                   | ε

boolean-literal ::= "false"
                    | "true"
                    | "Yes"
                    | "No"
                    | "YES"
                    | "NO"
