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


UNION

Задача: Реализовать операции работы с множествами


    1. Пересечение множеств
    2. Объединение множеств
    3. Вычитание множеств
    4. Симметрическая разность



Определения:

Объединением множеств A и B называется множество

Пересечением множеств A и B называется множество

Разностью множеств A и B называется множество

Симметрической разностью множеств A и B называется множество


Решение

Для решения задачи необходимо определиться с представлением
множеств. В качестве представления выберем списки. Таким образом,
множество из элементов A,B,C будет представлено в виде списка (A B
C). Многоуровневые списки естественным образом представляют множество
множеств.

Определим некоторые ограничения. В первую очередь мы остановимся на
рассмотрении одноуровневых списов, т.е. множеств, состоящих из
элементов. В дальнейшем будет показано, что ограничение не
существенно.

Начнем с объединения множеств. Решением является функция union~ от
двух аргументов a, b, которые представляют два объединяемых
множества. Единственность элемента, его уникальность – вот свойство
множеств, которое требует реализации. Таким образом, решение можно
свести к рекурсивной обработке одного из аргументов на осове слудующих
соображений:

Если a пусто, то вернуть b
Если b пусто, то вернуть a
Если (car a) принадлежит множеству b, то результат:
(cons (car a) (union~ (cdr a) b)
В противном случае результат:
(union~ (cdr a) b)

Прежде чем приняться за реализацию необходимо конкретизировать понятие
“принадлежит” в терминах выбранного предствавления, ограничений и
функционального подхода.

В силу того, что мы ограничились рассмотрением одноуровневых списков,
то (car a) всегда будет элементом, атомом. Тогда понятие
принадлежности можно формализовать как функцию in-predicate от двух
аргументов, первый из которых атом, а второй – одноуровневый спискок,
представляющий множество:



(defun in-predicate (a l)

    (cond

        ((null l) nil) ; элемент не может принадлежать пустому
        множеству

        ((eq a (car l)) t) ; элемент принадлежит множеству, если в нем
        содержится

        (t (in-predicate a (cdr l))) ; продолжаем проверку

    )

)




Тестирование:



> (in-predicate 'a '(b c a))

T

> (in-predicate 'a '(b c d))

NIL




Формализуя, получаем решение:



(defun union~ (a b)

    (cond ((null a) b)

        ((null b) a)

        ((in-predicate (car a) b) (union~ (cdr a) b) )

        (t (cons (car a) (union~ (cdr a) b)))

    )

)




Тестирование:



> (union~ '(a b c) '(b c d))

“Лисп со всех сторон” --- В.А. Потапенко --- vp@green.iis.nsk.su 2

(A B C D)

> (union~ '(a b c) 'nil)

(A B C)

> (union~ 'nil 'nil)

NIL

> (union~ '(a b) '(c d))

(A B C D)

Источник
http://lisp.ru/page.php?id=23


--------
Алгоритм
--------

Если a пусто, то вернуть b
Если b пусто, то вернуть a
Если (car a) принадлежит множеству b, то результат:
(cons (car a) (union~ (cdr a) b)
В противном случае результат:
(union~ (cdr a) b)

-------------------------------------------------------

(defun new-union (a b)
 (if (not b)
      a
      (if (member (car b) a)
        (new-union a (cdr b))
        (new-union (append a (list (car b))) (cdr b)))))

or

(defun new-union (list1 list2)
  (remove-duplicates (flatten (list list1 list2)) :from-end t))

or

определение функции
(defun new-union (list1 list2)
    (remove-duplicates (flatten (list list1 list2)) :from-end t))
NEW-UNION

вызов функции
> (new-union 'a 'b)
(A B)
> (new-union 'a '(b))
(A B)
> (new-union '(a b) '(b c))
(A B C)
> (new-union '(((a))) '(b (c ((d e)) a)))
(A B C D E)

UNION – это функция двух аргументов, оба аргумента “X” и “Y” - списки,
представляющие
множества. Функция вырабатывает новый список, в который входят все
атомы из списков
“Х” и “Y”.

Алгоритм:
Определение тела функции состоит из трех ветвей:
- Если первый аргумент – пустой список,
   то значением является второй аргумент, т.е. можно ничего не
   строить.
- Иначе если “голова” первого аргумента входит во второй аргумент,
   то достаточно объединить хвост первого аргумента со вторым
   аргументом, т.е.
    рекурсивно применяем исходную функцию, редуцируя первый аргумент.
- Иначе “голову” первого аргумента присоединяем к результату
объединения
   редуцированного первого аргумента со вторым аргументом.


алг UNION (список x,y) арг x, y
    нач
       если пусто (x)
          то знач := y
       инес member ( голова (x), y )
          то знач := UNION (хвост (x), y)
       иначе знач := cons (голова (x), UNION (хвост (x), y))
    кон

Источник
http://window.edu.ru/library/pdf2txt/684/41684/18842/page7

INTERSECTION – это функция двух аргументов, оба аргумента “X” и “Y” -
списки,
представляющие множества. Функция вырабатывает новый список, в который
входят атомы
списка “Х”, входящие в список “Y”.

Алгоритм:
Определение тела функции состоит из трех ветвей:
- Если первый аргумент – пустой список,
   то и пересечение - пустой список.
- Иначе если “голова” первого аргумента входит во второй аргумент,
   то “голову” первого аргумента присоединяем к результату пересечения
   редуцированного
    первого аргумента со вторым аргументом.
- Иначе применяем пересечение к редуцированному первому аргументу со
вторым
   аргументом.


алг INTERSECTION (список x,y) арг x, y
    нач
       если пусто (x)
          то знач := Nil
       инес member ( голова (x), y )
          то знач := cons (голова (x), INTERSECTION (хвост (x),
y))
       иначе знач := INTERSECTION (хвост (x), y)
    кон
                                                                                    14


Определяя эти функции на Лиспе, мы используем специальную
псевдо-функцию
DEFUN. Программа выглядит так:



 (DEFUN MEMBER (A X)
;определение проверки входит ли атом в список
     (COND
       ((NULL X)    Nil)
       ((EQ A (CAR X)) T)
       (T        (MEMBER A (CDR X)) )
)    )

(DEFUN UNION (X Y)
;определение объединения двух множеств
     (COND
      ((NULL X) Y)
      ((MEMBER (CAR X) Y) (UNION (CDR X) Y) )
      (T (CONS (CAR X) (UNION (CDR X) Y))) )) )
))

(DEFUN INTERSECTION (X Y)
;определение пересечения двух множеств
         (COND
   ((NULL X) NIL)
   ((MEMBER (CAR X) Y) (CONS (CAR X) (INTERSECTION (CDR
X) Y)) )
   (T (INTERSECTION (CDR X) Y))
))

(INTERSECTION '(A1 A2 A3) '(Al A3 A5))
;тест на пересечение двух множеств
(UNION '(X Y Z) '(U V W X))
;тест на объединение двух множеств


Эта программа предлагает Лисп-системе вычислить пять различных
форм. Первые три
формы сводятся к применению псевдо-функции DEFUN. Значение четвертой
формы - (A1
A3). Значение пятой формы - (Y Z C B D X). Анализ пути, по которому
выполняется
рекурсия, показывает, почему элементы множества появляются именно в
таком порядке.

Псевдо-функция - это функция, которая выполняется ради ее воздействия
на систему, тогда
как обычная функция - ради ее значения. DEFUN заставляет функции стать
определенными и
допустимыми в системе равноправно со встроенными функциями. Ее
значение - имя
определяемой функции, в данном случае - MEMBER, UNION, INTERSECTION.




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


---------
Алгоритм:
---------




