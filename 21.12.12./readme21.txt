______________

примеры кодов

______________

***тема Данные***

**ЦИТИРОВАНИЕ**
________________
чтобы Лисп не счел список вызовом функции

CL-USER> '(my 3 "Sons")
(MY 3 "Sons")

CL-USER> '(my 6 "Cats")
(MY 6 "Cats")

CL-USER> '(my very big 8 "Dogs")
(MY VERY BIG 8 "Dogs")

CL-USER> '(my lesson Lisp 21 "Dec 2012")
(MY LESSON LISP 21 "Dec 2012")

CL-USER> '(my NN year in this live "my 2012 year")
(MY NN YEAR IN THIS LIVE "my 2012 year")

CL-USER> '(the list (a b c) has 3 elements)
(THE LIST (A B C) HAS 3 ELEMENTS)

CL-USER> '(this dog (Mary) has 6 puppies)
(THIS DOG (MARY) HAS 6 PUPPIES)

CL-USER> '(the list (1 2 3 4 5 6 7 8 9) has 9 elements)
(THE LIST (1 2 3 4 5 6 7 8 9) HAS 9 ELEMENTS)

CL-USER> '(the Lisp has (functions lists predicates simbols) in
arhitecture)
(THE LISP HAS (FUNCTIONS LISTS PREDICATES SIMBOLS) IN ARHITECTURE)


Построение списка с помощью функции list
ее агументы вычисляются
пример, внутри вызова функции list вычисляется значение функции +

CL-USER> (list 'my (+ 2 1) "Sons")

(MY 3 "Sons")

CL-USER> (list 'my (+ 1 1) "Cats: Tupa and Musiya")

(MY 2 "Cats: Tupa and Musiya")


Связь между выражениями и списками
(именно в этом помогает цитирование)

если список цитируется - то результат вычисления будет этот список
если список НЕ цитируется - то результатом вычисления, будет чтение
самого кода и будут вычисленные значения этого кода

цитируется

CL-USER> (list 'my "(+ 2 1) Sons")
(MY "(+ 2 1) Sons")

в данном случае выражение (+ 2 1) цитируется,
поэтому самого вычисления (т.е. функции сложения) не происходит

НЕ цитируется

CL-USER> (list 'my (+ 2 1) "Sons")
(MY 3 "Sons")

в данном случае выражение (+ 2 1) НЕ цитируется,
потому просиходит чтение кода, что говорит программе
вычислить (т.е.выполнить функцию сложения) выражение (+ 2 1),
т.е. сложить два числа 2 и 1 (2+1=3)

_____________________

**операции со СПИСКАМИ**

_____________________

построить список можно с помощью cons
данная функция имеет два аргумента

общий вид cons:

(cons se1 se2)

примеры:

CL-USER> (cons 'a '(b c d))
(A B C D)

CL-USER> (cons '(a b c) '(e f g))
((A B C) E F G)

CL-USER> (cons 'a 'b)
(A . B)

CL-USER> (cons '(a nil) '(b nil))
((A NIL) B NIL)

CL-USER> (cons '(a b) '( c d f))
((A B) C D F)

CL-USER> (cons '(a b c) 'd)
((A B C) . D)

CL-USER> (cons '(a b c) '(d))
((A B C) D)

CL-USER> (cons '(a) '(b c d))
((A) B C D)

CL-USER> (cons '((a) (b)) '((c) (d)))
(((A) (B)) (C) (D))

CL-USER> (cons '(a) '((b) (c) (d)))
((A) (B) (C) (D))

CL-USER> (cons '(1) '(2 3 4))
((1) 2 3 4)

CL-USER> (cons '(pasha) '(lesha))
((PASHA) LESHA)

CL-USER> (cons '(pasha (+ 2 3)) '(lesha (+ 5 10)))
((PASHA (+ 2 3)) LESHA (+ 5 10))

CL-USER> (cons '(pasha (kate)) '(lesha (darina)))
((PASHA (KATE)) LESHA (DARINA))


Создадим список из одного аргумента и пустого списка
с помощью функции cons

CL-USER> (cons 'a '(nil))
(A NIL)

CL-USER> (cons 'a nil)
(A)

CL-USER> (cons 'a '())
(A)

CL-USER> (cons '() 'a)
(NIL . A)




Использование cons и list

функция cons - строит списки, если ее второй агумент список,
то она возвращает новый список, с первым аргументом, добавляя его в
начало
т.е. (cons 'a '(b c d))
вернет (A B C D)
'a - первый аргумент
'(b c d) - второй аргумент функции cons
следовательно,
функция взяла первый аргумент 'a  и положила его в начало списка (b c
d),
создав этим новый список (a b c d)


функция list - для создания списков
более я ничего не могу о ней сказать


CL-USER> (cons 'a (cons 'b nil))
(A B)

но так очень долго,
можно короче и быстрее,
с помощью функции list:

CL-USER> (list 'a 'b)
(A B)

CL-USER> (list 'a 'b 'c)
(A B C)

CL-USER> (list 'af 'bc 'de)
(AF BC DE)

CL-USER> (list 'pasha 'lesha 'vadim)
(PASHA LESHA VADIM)

CL-USER> (list 'pasha '(kate) 'lesha '(sam) 'vadim '(gala))
(PASHA (KATE) LESHA (SAM) VADIM (GALA))

CL-USER> (list '(pasha (kate)) '(lesha (sam)) '(vadim gala))
((PASHA (KATE)) (LESHA (SAM)) (VADIM GALA))



_________________

Истинность
_________________

Истина - true, сокращенно самовычисляемый символ t (T)

функция listp возвращает истину (т.е. T) если ее аргумент является
списком

CL-USER> (listp '(a b c))
T

функция вернула истину

CL-USER> (listp '(1 2 3))
T

функция listp вернет ложь (т.е. NIL),
если ее аргумент НЕ будет являться списком

CL-USER> (listp "this is lie")
NIL


_____________________

Условный рператор if
_____________________

if принимает три аргумента:

1-test
2-then "то"
3-else "иначе"

напишем алгоритм условия словами:

первое выражение вступает в силу,
выражение test - если функция listp вернет истину, так как
ее аргумент это список
"ТО" (второй аргумент вступил в силу, т.е. then), вызываем функцию +
и складываем два числа 1 и 2
и выдаем получившееся число т.е. 3 (т.к. 1+2=3)
"иначе" (третий аргумент вступил в силу, т.е. else),
вызываем функцию +
и складываем два числа 5 и 6
и выдаем получившийся результат т.е. 11 (т.к. 5+6=11)


теперь напишем все это в код:
test-выражение
> (if (listp ’(a b c))
вернется истина, т.к. '(a b c) - это список
далее выполняется
then-выражение
т.к. истина, то вычисляем (+ 1 2)
(+ 1 2)
else-вырадение НЕ будет выполняться, т.к. истина
(+ 5 6))
итог выполнения test, then и else -выражений
3

вторая часть алгоритма:
test-выражение
> (if (listp 27)
истина НЕ вернется, т.к. 27 - это НЕ список
далее выполняется
then-выражение
НО, оно не выполнится т.к. НЕ истина
(+ 1 2)
значит, далее выполняется
else-выражение "иначе" - т.е. иначе чем истина,
а иначе, чем истина - это НЕ истина
т.к. НЕ истина, то вычисляем (+ 5 6)
(+ 5 6))
итог выполнения test, then и else -выражений
11


___________________________________

Ввод и вывод (!!!и выход и вход!!!)

___________________________________

функция ВЫВОДА format
принимает 2 и более аргументов
общий вид функции в словах:
первый аргумент говорит куда напечатать вводимую инфу
второй аргумент - это строковый шаблон
третий аргумент и прочие аргументы - это объекты, которые
будут вставляться в нужные позиции заданного (вторым аргументом)
шаблона

пример кода:

> (format t "~A plus ~A equals ~A.~%" 2 3 (+ 2 3))
2 plus 3 equals 5.
NIL

функция ВЫВОДА (ИЛИ ЧТЕНИЯ) read
считыватель
вот пример функции, которая предлагает ввести любое значение и затем
возвращает его

(defun askem (string)
(format t "~A" string)
(read))
> (askem "How old are you? ")
машина автоматически выдает вопрос (печатается зеленым цветом/другим цветом)
How old are you? кто-то вводит с клавиатуры ответ: 29
машина возвращает этот ответ
29


_____________

Присваивание
_____________

> (let ((n 10))
(setf n 2)
n)
2


let - оператор, который вводит новые переменные (локальные переменные)
инструкция к оператору let , которая содержит имя переменной и
соответствующее ей выражение
следовательно,
(n 10) - имя переменной, а
(setf n 2)
n) - выражение, которое соответствует имени переменной (n 10)
в общем это инструкция по выполнению действий над переменными

setf - это оператор присваивания значений, может присваивать значения
переменным любых типов
следовательно,
(setf n 2)
n) - это значит, присвоить переменной n значение 2 и вернуть это
значение n,
что и происходит, если взглянуть на код:

> (let ((n 10))
(setf n 2)
n)
2



__________________________________

Документация на глобальные функции
___________________________________

CL-USER> (documentation 'defun 'function)
"Define a function at top level."

CL-USER> (documentation 'setf 'function)
"Takes pairs of arguments like SETQ. The first is a place and the
second
  is the value that is supposed to go into that place. Returns the
  last
  value. The place argument may be any of the access forms for which
  SETF
  knows a corresponding setting form."

CL-USER> (documentation 'listp 'function)
"Return true if OBJECT is a LIST, and NIL otherwise."

CL-USER> (documentation '+ 'function)
"Return the sum of its arguments. With no args, returns 0."

CL-USER> (documentation '- 'function)
"Subtract the second and all subsequent arguments from the first;
  or with one argument, negate the first argument."

CL-USER> (documentation 'list 'function)
"Return constructs and returns a list of its arguments."

CL-USER> (documentation 'cons 'function)
"Return a list with SE1 as the CAR and SE2 as the CDR."

CL-USER> (documentation 'car 'function)
"Return the 1st object in a list."
CL-USER> (documentation 'cdr 'function)
"Return all but the first object in a list."
CL-USER> (documentation 'and 'function)
NIL
CL-USER> (documentation 'member 'function)
"Return the tail of LIST beginning with first element satisfying EQLity,
   :TEST, or :TEST-NOT with the given ITEM."
CL-USER> (documentation 'eql 'function)
NIL
CL-USER> (documentation 'format 'function)
"Provides various facilities for formatting output.
  CONTROL-STRING contains a string to be output, possibly with embedded
  directives, which are flagged with the escape character \"~\". Directives
  generally expand into additional text to be output, usually consuming one
  or more of the FORMAT-ARGUMENTS in the process. A few useful directives
  are:
        ~A or ~nA   Prints one argument as if by PRINC
        ~S or ~nS   Prints one argument as if by PRIN1
        ~D or ~nD   Prints one argument as a decimal integer
        ~%          Does a TERPRI
        ~&          Does a FRESH-LINE
  where n is the width of the field in which the object is printed.

  DESTINATION controls where the result will go. If DESTINATION is T, then
  the output is sent to the standard output stream. If it is NIL, then the
  output is returned in a string as the value of the call. Otherwise,
  DESTINATION must be a stream to which the output will be sent.

  Example:   (FORMAT NIL \"The answer is ~D.\" 10) => \"The answer is 10.\"

  FORMAT has many additional capabilities not described here. Consult the
  manual for details."


CL-USER> (documentation 'read 'function)
"Read the next Lisp value from STREAM, and return it."
CL-USER> (documentation 'let 'function)
"LET ({(var [value]) | var}*) declaration* form*

During evaluation of the FORMS, bind the VARS to the result of evaluating the
VALUE forms. The variables are bound in parallel after all of the VALUES forms
have been evaluated."
CL-USER> (documentation 'numberp 'function)
"Return true if OBJECT is a NUMBER, and NIL otherwise."
CL-USER> (documentation 'defparameter 'function)
"Define a parameter that is not normally changed by the program,
  but that may be changed without causing an error. Declare the
  variable special and sets its value to VAL, overwriting any
  previous value. The third argument is an optional documentation
  string for the parameter."
CL-USER> (documentation 'defconstant 'function)
"Define a global constant, saying that the value is constant and may be
  compiled into code. If the variable already has a value, and this is not
  EQL to the new value, the code is not portable (undefined behavior). The
  third argument is an optional documentation string for the variable."
CL-USER> (documentation 'boundp 'function)
"Return non-NIL if SYMBOL is bound to a value."
CL-USER> (documentation 'remove 'function)
"Return a copy of SEQUENCE with elements satisfying the test (default is
   EQL) with ITEM removed."
CL-USER> (documentation 'do 'function)
"DO ({(Var [Init] [Step])}*) (Test Exit-Form*) Declaration* Form*
  Iteration construct. Each Var is initialized in parallel to the value of the
  specified Init form. On subsequent iterations, the Vars are assigned the
  value of the Step form (if any) in parallel. The Test is evaluated before
  each evaluation of the body Forms. When the Test is true, the Exit-Forms
  are evaluated as a PROGN, with the result being the value of the DO. A block
  named NIL is established around the entire expansion, allowing RETURN to be
  used as an alternate exit mechanism."
CL-USER> (documentation 'dolist 'function)
NIL
CL-USER> (documentation 'mapc 'function)
"Apply FUNCTION to successive elements of lists. Return the second argument."
CL-USER> (documentation 'progn 'function)
"PROGN form*

Evaluates each FORM in order, returning the values of the last form. With no
forms, returns NIL."
CL-USER> (documentation 'function 'function)
"FUNCTION name

Return the lexically apparent definition of the function NAME. NAME may also
be a lambda expression."
CL-USER> (documentation 'apple 'function)
NIL

CL-USER> (documentation 'funcall 'function)
"Call FUNCTION with the given ARGUMENTS."
CL-USER> (documentation 'lambda 'function)
NIL
CL-USER> (documentation 'typep 'function)
"Is OBJECT of type TYPE?"
CL-USER> (documentation 'consp 'function)
"Return true if OBJECT is a CONS, and NIL otherwise."
CL-USER> (documentation 'nil 'function)
NIL
CL-USER> (documentation 'equal 'function)
"Return T if X and Y are EQL or if they are structured components whose
elements are EQUAL. Strings and bit-vectors are EQUAL if they are the same
length and have identical components. Other arrays must be EQ to be EQUAL."
CL-USER> (documentation 'copy-list 'function)
"Return a new list which is EQUAL to LIST. LIST may be improper."
CL-USER> (documentation 'append 'function)
"Construct a new list by concatenating the list arguments"
CL-USER> (documentation 'compress 'function)
NIL
CL-USER> (documentation 'compr 'function)
NIL
CL-USER> (documentation 'load 'function)
"Load the file given by FILESPEC into the Lisp environment, returning
   T on success."
CL-USER> (documentation 'nth 'function)
"Return the nth object in a list where the car is the zero-th element."
CL-USER> (documentation 'nthcdr 'function)
"Performs the cdr function n times on a list."
CL-USER> (documentation 'zerop 'function)
"Is this number zero?"
CL-USER> (documentation 'last 'function)
"Return the last N conses (not the last element!) of a list."
CL-USER> (documentation 'mapcar 'function)
"Apply FUNCTION to successive elements of LIST. Return list of FUNCTION
   return values."
CL-USER> (documentation 'maplist 'function)
"Apply FUNCTION to successive CDRs of list. Return list of results."
CL-USER> (documentation 'copy 'function)
NIL
CL-USER> (documentation 'copy-tree 'function)
"Recursively copy trees of conses."
CL-USER> (documentation 'substitute 'function)
"Return a sequence of the same kind as SEQUENCE with the same elements,
  except that all elements equal to OLD are replaced with NEW."
CL-USER> (documentation 'len 'function)
NIL
CL-USER> (documentation 'member-if 'function)
"Return tail of LIST beginning with first element satisfying TEST."
CL-USER> (documentation 'adjoin 'function)
"Add ITEM to LIST unless it is already a member"
CL-USER> (documentation 'length 'function)
"Return an integer that is the length of SEQUENCE."
CL-USER> (documentation 'subseq 'function)
"Return a copy of a subsequence of SEQUENCE starting with element number
   START and continuing to the end of SEQUENCE or the optional END."
CL-USER> (documentation 'reverse 'function)
"Return a new sequence containing the same elements but in reverse order."
CL-USER> (documentation 'mirror 'function)
NIL
CL-USER> (documentation 'sort 'function)
"Destructively sort SEQUENCE. PREDICATE should return non-NIL if
   ARG1 is to precede ARG2."
CL-USER> (documentation 'every 'function)
"Apply PREDICATE to the 0-indexed elements of the sequences, then
   possibly to those with index 1, and so on. Return NIL as soon
   as any invocation of PREDICATE returns NIL, or T if every invocation
   is non-NIL."
CL-USER> (documentation 'some 'function)
"Apply PREDICATE to the 0-indexed elements of the sequences, then
   possibly to those with index 1, and so on. Return the first
   non-NIL value encountered, or NIL if the end of any sequence is
   reached."

















