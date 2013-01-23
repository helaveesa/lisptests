Упражнения по третьей Главе: Списки

стр. 71

упр. 1.
нарисовать конс-ячейки для списков







упр. 2.
напишите свой вариант функции union,
который сохраняет порядок следования элементов
согласно исходным спискам

(new-union ’(a b c) ’(b a d))
(A B C D)

strukture union

UNION
Define a set to be a list of atoms, such that no atom is ever
repeated, and the order of atoms does not matter. The following
function computes the union of two sets, that is, a third set
containing any atom found in either or both of the two given sets.


(DEFUN UNION (SET1 SET2)

     (COND
       ((NULL SET1)   SET2)

       ((MEMBER (CAR SET1) SET2)   (UNION (CDR SET1) SET2))

       (T   (CONS (CAR SET1) (UNION (CDR SET1) SET2))) ) ) )


CL-USER> (defun new-union (a b)
           (if (not b)
               a
               (if (member (car b) a)
                   (new-union a (cdr b))
                   (new-union (append a (list (car b))) (cdr b)))))
STYLE-WARNING: redefining COMMON-LISP-USER::NEW-UNION in DEFUN
NEW-UNION
CL-USER> (new-union '(5 6) '(7 6))
(5 6 7)

источник:
http://stackoverflow.com/questions/12659236/lisp-function-union
















упр. 3.

напишите функцию, определяющую кол-во повторений
(с точки зр eql)
каждого элемента в заданном списке
и сортирующую из по убыванию встречаемости

(occurrences ’(a b a d a c d c a))
((A . 4) (C . 2) (D . 2) (B . 1))


напишите функцию, определяющую кол-во повторений
(с точки зр eql)
каждого элемента в заданном списке

пример использования eql

(eql (cons 'a nil) (cons 'a nil))
NIL ;;is false.


CL-USER> (eql 'a 'a)
T ;;is true.



[Function]
eql x y

The eql predicate is true if its arguments are eq, or if they are
numbers of the same type with the same value, or if they are character
objects that represent the same character. For example:

(eql 'a 'b) is false.
(eql 'a 'a) is true.
(eql 3 3) is true.
(eql 3 3.0) is false.
(eql 3.0 3.0) is true.
(eql #c(3 -4) #c(3 -4)) is true.
(eql #c(3 -4.0) #c(3 -4)) is false.
(eql (cons 'a 'b) (cons 'a 'c)) is false.
(eql (cons 'a 'b) (cons 'a 'b)) is false.
(eql '(a . b) '(a . b)) might be true or false.
(progn (setq x (cons 'a 'b)) (eql x x)) is true.
(progn (setq x '(a . b)) (eql x x)) is true.
(eql #\A #\A) is true.
(eql "Foo" "Foo") might be true or false.
(eql "Foo" (copy-seq "Foo")) is false.
(eql "FOO" "foo") is false.


Источник
http://www.cs.cmu.edu/Groups/AI/html/cltl/clm/node74.html



сортирование
функция sort

> (sort '(2 1 5 4 6) #'<)
(1 2 4 5 6)
> (sort '(2 1 5 4 6) #'>)
(6 5 4 2 1)

>> (sort '("jeff" "sue" "dave" "andy" "walt") #'string> )
:: ("walt" "sue" "jeff" "dave" "andy")

>> (sort '("jeff" "sue" "dave" "andy" "walt") #'string< )
:: ("andy" "dave" "jeff" "sue" "walt")

Источник:
http://nostoc.stanford.edu/Docs/livetutorials/functions.html

----------------------------------------
ПОЛЕЗНОСТЬ!!!
КРАТКО О ФУНКЦИЯХ LISP

http://homelisp.ru/help/lib_funct.html
------------------------------------------

ошибка:
The function COMMON-LISP-USER::COMPRESS is undefined.

на вот этот код:
CL-USER> (defun povtor (lst)
           (compress '(lst)
                     (sort '(lst) #'<)))
; in: DEFUN POVTOR
;     (SORT '(LST) #'<)
;
; caught WARNING:
;   Destructive function SORT called on constant data.
;   See also:
;     The ANSI Standard, Special Operator QUOTE
;     The ANSI Standard, Section 3.2.2.3

;     (SB-INT:NAMED-LAMBDA POVTOR
;         (LST)
;       (BLOCK POVTOR (COMPRESS '(LST) (SORT '(LST) #'<))))
; ==>
;   #'(SB-INT:NAMED-LAMBDA POVTOR
;         (LST)
;       (BLOCK POVTOR (COMPRESS '(LST) (SORT '(LST) #'<))))
;
; caught STYLE-WARNING:
;   The variable LST is defined but never used.

; in: DEFUN POVTOR
;     (COMPRESS '(LST) (SORT '(LST) #'<))
;
; caught STYLE-WARNING:
;   undefined function: COMPRESS
;
; compilation unit finished
;   Undefined function:
;     COMPRESS
;   caught 1 WARNING condition
;   caught 2 STYLE-WARNING conditions
POVTOR
CL-USER> (povtor '(a b a c d b b c g c d))


иначе

CL-USER> (defun povtor ()
           (compress '(a b a c d e f d b c e f c a b)
                     (sort '(a b a c d e f d b c e f c a b) #'<)))
; in: DEFUN POVTOR
;     (SORT '(A B A C D E F D B C E F ...) #'<)
;
; caught WARNING:
;   Destructive function SORT called on constant data.
;   See also:
;     The ANSI Standard, Special Operator QUOTE
;     The ANSI Standard, Section 3.2.2.3

;     (COMPRESS '(A B A C D E F D B C E F ...)
;      (SORT '(A B A C D E F D B C E F ...) #'<))
;
; caught STYLE-WARNING:
;   undefined function: COMPRESS
;
; compilation unit finished
;   Undefined function:
;     COMPRESS
;   caught 1 WARNING condition
;   caught 1 STYLE-WARNING condition
STYLE-WARNING: redefining COMMON-LISP-USER::POVTOR in DEFUN
POVTOR
CL-USER> (povtor)

выдал ошибку:
The value B is not of type NUMBER.
значение В не относится к типу NUMBER

реализация collect

CL-USER>  (defun collect (x)
            (cond ((null x) nil)
                  (t (append (extr (car x) x)
                             (collect (remove (car x) x))))))
STYLE-WARNING: redefining COMMON-LISP-USER::COLLECT in DEFUN
COLLECT
CL-USER> (collect '(5 1 2 3 1 2 3 1 2 2 3 3 1 1 5))
(5 5 1 1 1 1 1 2 2 2 2 3 3 3 3)


Функция PAIR строит из двух списков список пар (ассоциативный
список). Оба аргумента функции должны быть списками.

(pair '(a b c d) '(1 2 3 4))
==> ((a . 1) (b . 2) (c . 3) (d . 4))


(pair '(a b c d e f) '(1 2 3))
==> ((a . 1) (b . 2) (c . 3) (d) (e) (f))


(pair '(a b c d) '(1 2 3 4 5))
==> ((a . 1) (b . 2) (c . 3) (d . 4))




