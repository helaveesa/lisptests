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


