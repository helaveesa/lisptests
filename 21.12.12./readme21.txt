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

CL-USER> (cons 'a '())
(A)

CL-USER> (cons '() 'a)
(NIL . A)

Использование cons и list











