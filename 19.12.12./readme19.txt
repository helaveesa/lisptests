Начало темы МАССИВЫ

еще один способ хранения данных в Лиспе

пример создания массива 2Х3:

CL-USER> (setf arr (make-array '(2 3) :initial-element nil))


; in: SETF ARR
;     (SETF ARR (MAKE-ARRAY '(2 3) :INITIAL-ELEMENT NIL))
; ==>
;   (SETQ ARR (MAKE-ARRAY '(2 3) :INITIAL-ELEMENT NIL))
;
; caught WARNING:
;   undefined variable: ARR
;
; compilation unit finished
;   Undefined variable:
;     ARR
;   caught 1 WARNING condition


#2A((NIL NIL NIL) (NIL NIL NIL))


получение элемента массива, пользуемся aref
CL-USER> (aref arr 0 0)
NIL

Новое значение переменной нужно записать:
вот как мы это сделаем

CL-USER> (setf (aref arr 0 0) 'b)

B
CL-USER> (aref arr 0 0)
B

Теперь свои примеры потестируем:

создади массив 6Х7

CL-USER> (setf arr (make-array '(6 7) :initial-element nil))

;     (SETF ARR (MAKE-ARRAY '(6 7) :INITIAL-ELEMENT NIL))
; ==>
;   (SETQ ARR (MAKE-ARRAY '(6 7) :INITIAL-ELEMENT NIL))
;
; caught WARNING:
;   undefined variable: ARR
;
; compilation unit finished
;   Undefined variable:
;     ARR
;   caught 1 WARNING condition
#2A((NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL))

все ок

теперь получим один из элементов этого массива
получение элемента массива, пользуемся aref

CL-USER> (aref arr 2 2)
NIL

теперь попробуем везде, где есть NIL записать перепенную

Новое значение переменной нужно записать:
вот как мы это сделаем

CL-USER> (setf (aref arr 0 0) 'a)

A
CL-USER> (aref arr 0 0)
A

и так для каждой ячейки (т.е. пересечение столбцов и строк)
т.е. 0Х0-A
     1Х1-B
     2X2-C
     и так далее

(setf (aref arr 0 0) 'a) - буквально, это звучит так,
присвоим ячейке 0Х0 значение А

CL-USER> (setf (aref arr 0 0) 'a)
A
CL-USER> (aref arr 0 0)
A
CL-USER> (setf (aref arr 1 1) 'b)
B
CL-USER> (aref arr 1 1)
B
CL-USER> (setf (aref arr 2 2) 'c)
C
CL-USER> (aref arr 2 2)
C

теперь создади массив 6Х7
и зададим вместо nil единицу

CL-USER> (setf arr (make-array '(6 7) :initial-element 1))

;     (SETF ARR (MAKE-ARRAY '(6 7) :INITIAL-ELEMENT 1))
; ==>
;   (SETQ ARR (MAKE-ARRAY '(6 7) :INITIAL-ELEMENT 1))
;
; caught WARNING:
;   undefined variable: ARR
;
; compilation unit finished
;   Undefined variable:
;     ARR
;   caught 1 WARNING condition
#2A((1 1 1 1 1 1 1)
    (1 1 1 1 1 1 1)
    (1 1 1 1 1 1 1)
    (1 1 1 1 1 1 1)
    (1 1 1 1 1 1 1)
    (1 1 1 1 1 1 1))

идем дальше

массивы могут быть заданы буквально,
с помощью синтаксиса #na

n - количество размерностей массива

нам надо на выходе получить вот это:

#2A((B NIL NIL) (NIL NIL NIL))

получаем:

CL-USER> (setf arr (make-array '(2 3) :initial-element nil))

;     (SETF ARR (MAKE-ARRAY '(2 3) :INITIAL-ELEMENT NIL))
; ==>
;   (SETQ ARR (MAKE-ARRAY '(2 3) :INITIAL-ELEMENT NIL))
;
; caught WARNING:
;   undefined variable: ARR
;
; compilation unit finished
;   Undefined variable:
;     ARR
;   caught 1 WARNING condition
#2A((NIL NIL NIL) (NIL NIL NIL))
CL-USER> (setf (aref arr 0 0) 'b)
B
CL-USER> (aref arr 0 0)
B

ок, мы получили:

#2A((B NIL NIL) (NIL NIL NIL))

теперь применим глобальную переменную *print-array*
которая будет установлена в t

CL-USER> (setf *print-array* t)
T

ок, работает

теперь получим автоматически то, что мы задавали буквально
т.е. вот эту строчку: #2A((B NIL NIL) (NIL NIL NIL))

CL-USER> arr
#2A((B NIL NIL) (NIL NIL NIL))

набрав arr мы получили строчку #2A((B NIL NIL) (NIL NIL NIL))
автоматически

теперь можно попробовать на своем примере:

-создадим массив 6Х7
-передадим вместо NIL некоторые значения (т.е. A B C)
-и выведем то, что мы записали,
чтобы убедиться, что мы действительно записали эти значения в массив


вот мы создали массив 6Х7

CL-USER> (setf arr (make-array '(6 7) :initial-element nil))

;     (SETF ARR (MAKE-ARRAY '(6 7) :INITIAL-ELEMENT NIL))
; ==>
;   (SETQ ARR (MAKE-ARRAY '(6 7) :INITIAL-ELEMENT NIL))
;
; caught WARNING:
;   undefined variable: ARR
;
; compilation unit finished
;   Undefined variable:
;     ARR
;   caught 1 WARNING condition

вот наш массив
#2A((NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL))

дальше передадим
в ячейки 0Х0
         1Х1
         2Х2
         значения  A B C,
         соответственно

CL-USER> (setf (aref arr 0 0) 'a)
A
CL-USER> (setf (aref arr 1 1) 'b)
B
CL-USER> (setf (aref arr 2 2) 'c)
C

введем глобальную переменную для того, чтобы напечатать наш массив
CL-USER> (setf *print-array* t)
T

ок,функцией arr напечатаем наш массив
CL-USER> arr
#2A((A NIL NIL NIL NIL NIL NIL)
    (NIL B NIL NIL NIL NIL NIL)
    (NIL NIL C NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL))

все верно, ячейке 0Х0 соответствует значение А
           ячейке 1Х1 соответствует значение B
           ячейке 2Х2 соответствует значение C

можно вместо букв и цифр, передавать целые слова:

вот пример:

CL-USER> (setf arr (make-array '(6 7) :initial-element nil))
;
; caught WARNING:
;   undefined variable: ARR
;
; compilation unit finished
;   Undefined variable:
;     ARR
;   caught 1 WARNING condition
#2A((NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL))
CL-USER> (setf (aref arr 0 0) 'mama)
MAMA
CL-USER> (setf (aref arr 0 0) 'papa)
PAPA
CL-USER> (setf (aref arr 0 0) 'mucya)
MUCYA
CL-USER> (setf (aref arr 0 0) 'mama)
MAMA
CL-USER> (setf (aref arr 1 1) 'papa)
PAPA
CL-USER> (setf (aref arr 2 2) 'musya)
MUSYA
CL-USER> (setf (aref arr 3 3) 'me)
ME
CL-USER> (setf (aref arr 4 4) 'boy)
BOY
CL-USER> (setf *print-array* t)
T
CL-USER> arr
#2A((MAMA NIL NIL NIL NIL NIL NIL)
    (NIL PAPA NIL NIL NIL NIL NIL)
    (NIL NIL MUSYA NIL NIL NIL NIL)
    (NIL NIL NIL ME NIL NIL NIL)
    (NIL NIL NIL NIL BOY NIL NIL)
    (NIL NIL NIL NIL NIL NIL NIL))

__________
ВЕКТОР
__________

вектор - это тоже массив, только одномерный,
когда в функцию, которая создает массив
make-array

передается целое число

(setf vec (make-array 4 :initial-element nil))

в данном случае это число 4

CL-USER> (setf vec (make-array 4 :initial-element nil))

; in: SETF VEC
;     (SETF VEC (MAKE-ARRAY 4 :INITIAL-ELEMENT NIL))
; ==>
;   (SETQ VEC (MAKE-ARRAY 4 :INITIAL-ELEMENT NIL))
;
; caught WARNING:
;   undefined variable: VEC
;
; compilation unit finished
;   Undefined variable:
;     VEC
;   caught 1 WARNING condition
#(NIL NIL NIL NIL)

создает и заполняет вектор функция vector
(вполне себе логично)

(vector "a" ’b 3)
#("a" B 3)

или

CL-USER> (vector "lisp" 'v 5)
#("lisp" V 5)

Доступ к элементам вектора
осуществляется, через функцию svref

> (svref vec 0)
NIL

попробуем на своем примере:

???

надо разбираться


_______________

Строки и знаки

________________

CL-USER> (aref "abc" 1)
#\b
CL-USER> (aref "abc" 2)
#\c
CL-USER> (aref "abc" 3)
; Evaluation aborted on #<SB-INT:INVALID-ARRAY-INDEX-ERROR
expected-type: (INTEGER 0 (3)) datum: 3>.
CL-USER> (aref "abc" 0)
#\a
CL-USER> (let ((str (copy-seq "Merlin")))
           (setf (char str 3) #\k)
           str)
"Merkin"
CL-USER> (let ((str (copy-seq "Helen")))
           (setf (char str 0) #\P)
           (setf (char str 1) #\u)
           (setf (char str 2) #\s)
           (setf (char str 3) #\i)
           (setf (char str 4) #\k)
           str)
"Pusik"

CL-USER> (let ((str (copy-seq "Merlin")))
           (setf (char str 1) #\o)
           (setf (char str 2) #\n)
           (setf (char str 3) #\r)
           (setf (char str 4) #\o)
           (setf (char str 5) #\!)
           str)
"Monro!"

___________________

Последовательности
___________________

вернуть все номера букв а в слове fantasia

первая буква а

CL-USER> (position #\a "fantasia")
1

как же вернуть букву а, которая 4 по счету?
(помним, что отсчет начинается с нуля)
ведь если всегда писать так
CL-USER> (position #\a "fantasia")
1
будет всегда возвращаться 1, то есть первая буква а в двнном слове

вот вариант выхода из этого
утановить аргументы по ключу

0-f
 1-a
2-n
3-t
 4-a
5-s
6-i
 7-a

буквы а у нас под номерами 1, 4, и 7
с буквой 1-а мы разобрались, все ок
буква 4-а, вот как мы ее вычислим
эта буква а находится под номером 4, т.е. между 3 и 5
вот мы это и запишем
:start 3 :end 5
начала отсчета от 3, а конец счета 5
выведет номер 4, значит нужную нам букву а

CL-USER> (position #\a "fantasia" :start 3 :end 5)
4

аналогично
только конечный аргумент по ключу можно опустить
CL-USER> (position #\a "fantasia" :start 6)
7




