Упражнения по учебнику ANSI Common Lisp

по Главе 2

1 упр
описать, что происходит при вычислении выражений:

выражения:

(a)

(+ (- 5 1) (+ 3 7))

функции + передано два аргумента
эти аргументы это математические выражения:
(- 5 1) и (+ 3 7)
они вычисляются, и передаются функции +,
которая потом сложит числа полученные
после вычислений

(+ 4 10)
14


(b)

(list 1 (+ 2 3))

построение списка с помощью функции list
эта функция имеет аргументы, которые вычисляются

сначала вычисляется функция + во внутренних скобках
итог 5
и этот итог передается в функцию list,
которая стоит список из двух, в данном случае, агументов 1 и 5

(list 1 5)


(с)

(if (listp 1) (+ 1 2) (+ 3 4))

условному оператору if передана функция listp, которая возвращает
истину (T), если ее аргумент список.

проверяем:
CL-USER> (listp 1)
NIL
вернул nil - ложь

еще два параметра 3 и 7 полученные после вычисления функций +

(listp 1) - test-выражение
сначала вычисляется оно, если оно истино, то вычисляется
then-выражение и возвращается его результат
в нашем случае это будет (+ 1 2)
возвращается 3
в противном случае, вычисляется else-выражение

итак, test-выражение ложно, значит вычисляется сразу else-выражение
возвращается значение 7

итог 7

тестируем:

CL-USER> (if (listp 1) (+ 1 2) (+ 3 4))
7

ок, все рассуждения верны


(d)

(list (and (listp 3) t) (+ 1 2))

list - это функция с помощью которой строят списки
and - логический оператор "И"
функция listp, которая возвращает истину (T), если ее аргумент список
t - показывает, что вывод будет отправлен в стандартное место,
принятое по умолчанию (toplevel)
(+ 1 2) - выражение которое вычисляет 1+2=3

вычислим выражение (list (and (listp 3) t) (+ 1 2)):

CL-USER> (list (and (listp 3) t) (+ 1 2))
(NIL 3)

вернул ложь и аргумент 3 в списке

функции, для построения списка передается выражение (+ 1 2)
"И" выражение (listp 3), которое как раз и возвращает ложь, а
t-говорит куда напечатать результат: то есть построенный список


упр 2
составьте с помощью cons
три различных выражения, создающие список (a b c)

cons - функция, с помощью которой строятся списки

CL-USER> (cons 'a '(b c))
(A B C)

CL-USER> (cons 'a (cons 'b (cons 'c nil)))
(A B C)

???


упр 3
с помощью car и cdr определить функцию,
которая возвращает 4-ый элемент списка

если бы мы взяли список только из четырех аргументов,
мы смогли бы вернуть число 4 без car, пользуясь только cdr
вот пример:

CL-USER> (car '('пантера 'коалла 'пума 'ленивец))
'ПАНТЕРА
CL-USER> (cdr '('пантера 'коалла 'пума 'ленивец))
('КОАЛЛА 'ПУМА 'ЛЕНИВЕЦ)
CL-USER>  (cdr (cdr (cdr '('пантера 'коалла 'пума 'ленивец))))
('ЛЕНИВЕЦ)

поэтому возьмем список из 7 аргументов: (1 2 3 4 5 6 7)
нам нужно вернуть 4

заменим числа на список животных, так будет веселее
нам все еще нужно вернуть ленивца!

('пантера 'коалла 'пума 'ленивец 'гепард 'обезьяна 'рысь)

'(пантера коалла пума ленивец гепард обезьяна рысь)

CL-USER> (car (cdr (cdr (cdr '(пантера коалла пума ленивец гепард обезьяна рысь)))))
ЛЕНИВЕЦ

упр 4
определить функцию,
которая принимает два аргумента и возвращает наибольший из них

выдает ошибку:

invalid number of elements in
    ((LISTP '(X Y)) (> X Y) (MASSAGE MAXIMUM "x") (< X Y)
     (MASSAGE MAXIMUM "y"))
  to satisfy lambda list
    (SB-C::TEST SB-C::THEN &OPTIONAL SB-C::ELSE):
  between 2 and 3 expected, but 5 found
   [Condition of type SB-INT:COMPILED-PROGRAM-ERROR]

на вот этот код:

CL-USER> (defun maximum (x y)
           (if (listp '(x y))
               (> x y)
               (massage maximum "x")
               (< x y)
               (massage maximum "y")))
; in: DEFUN MAXIMUM
;     (IF (LISTP '(X Y))
;         (> X Y)
;         (MASSAGE MAXIMUM "x")
;         (< X Y)
;         (MASSAGE MAXIMUM "y"))
;
; caught ERROR:
;   error while parsing arguments to special form IF:
;     invalid number of elements in
;       ((LISTP '(X Y)) (> X Y) (MASSAGE MAXIMUM "x") (< X Y)
;        (MASSAGE MAXIMUM "y"))
;     to satisfy lambda list
;       (SB-C::TEST SB-C::THEN &OPTIONAL SB-C::ELSE):
;     between 2 and 3 expected, but 5 found

;     (SB-INT:NAMED-LAMBDA MAXIMUM
;         (X Y)
;       (BLOCK MAXIMUM
;         (IF (LISTP '(X Y))
;             (> X Y)
;             (MASSAGE MAXIMUM "x")
;             (< X Y)
;             (MASSAGE MAXIMUM "y"))))
; ==>
;   #'(SB-INT:NAMED-LAMBDA MAXIMUM
;         (X Y)
;       (BLOCK MAXIMUM
;         (IF (LISTP '(X Y))
;             (> X Y)
;             (MASSAGE MAXIMUM "x")
;             (< X Y)
;             (MASSAGE MAXIMUM "y"))))
;
; caught STYLE-WARNING:
;   The variable X is defined but never used.
;
; caught STYLE-WARNING:
;   The variable Y is defined but never used.
;
; compilation unit finished
;   caught 1 ERROR condition
;   caught 2 STYLE-WARNING conditions
STYLE-WARNING: redefining COMMON-LISP-USER::MAXIMUM in DEFUN
MAXIMUM

изменила код в условии:

CL-USER> (defun maximum (x y)
           (if (listp '(x y))
               (> x y)
               (< x y)))
STYLE-WARNING: redefining COMMON-LISP-USER::MAXIMUM in DEFUN
MAXIMUM
CL-USER> (maximum 8 2)
T
CL-USER> (maximum 2 8)
NIL

вот пример кода по возвращению только максимального аргумента

CL-USER> (defun maximum (x y z)
           (if (list '(x y z))
               (> x y z)))
STYLE-WARNING: redefining COMMON-LISP-USER::MAXIMUM in DEFUN
MAXIMUM
CL-USER> (maximum 10 6 2)
T
CL-USER> (maximum 6 10 2)
NIL
CL-USER> (maximum 2 6 10)
NIL


теперь функция работает, но возвращая только истину или ложь,
а мне нужн, чтобы она возвращала максимальное значение (число)

_______________

просто отстраненный пример на работу условного оператора if

CL-USER> (defun test (x y)
           (if (listp '(a b c))
               (+ 1 2)
               (+ 6 6)))
; in: DEFUN TEST
;     (SB-INT:NAMED-LAMBDA TEST
;         (X Y)
;       (BLOCK TEST
;         (IF (LISTP '(A B C))
;             (+ 1 2)
;             (+ 6 6))))
; ==>
;   #'(SB-INT:NAMED-LAMBDA TEST
;         (X Y)
;       (BLOCK TEST
;         (IF (LISTP '(A B C))
;             (+ 1 2)
;             (+ 6 6))))
;
; caught STYLE-WARNING:
;   The variable X is defined but never used.
;
; caught STYLE-WARNING:
;   The variable Y is defined but never used.
;
; compilation unit finished
;   caught 2 STYLE-WARNING conditions
STYLE-WARNING: redefining COMMON-LISP-USER::TEST in DEFUN
TEST
CL-USER> (test 1 2)
3
CL-USER> (test 6 6)
3
CL-USER> (test 5 4)
3

какие бы я числа не подставила в аргументы x и y, будет
возвращен результат выражения (+ 1 2), т.е. 3
т.к. по условию, срабатывает вычисление именно этого выражения,
так как listp проверяет на истину свои аргументы,
если аргументы составляют список - то истина,
если аргументы не составляют список - то ложь

вычисляется тест-выражение: (if (listp '(a b c))
если тест-выражение истино - то вычисляется then-выражение т.е. (+ 1 2)
а оно в нашем примере, истино,вот и вычисляется 1+2=3

_______________________________________________________________________

возвращаясь к упр 4

мне нужно определить функцию, которая принимает ДВА агумента,
пусть это будет x и y

оператор defun может создать функцию, которая как раз и будет
принимать два аргумента

определим новую функцию под именем MAXIMUM

структура оператора defun:
-имя будующей функции, в данном случае как раз MAXIMUM
-список параметров (аргументов) это как раз, то
что функция будет принимать два аргумента (x y), например
-тело функции (выражения 1 или более, то есть то,
что я буду делать с аргументами)

определим функцию:

CL-USER> (defun maximum (x y)
           (> x y))
STYLE-WARNING: redefining COMMON-LISP-USER::MAXIMUM in DEFUN
MAXIMUM

вызов функции MAXIMUM:

CL-USER> (maximum 10 5)
T
CL-USER> (maximum 2 9)
NIL

функция возвращает истину - если X > Y
функция возвращает ложь - если X < Y

в моем случае, возвращается не максимально число,
а истина в случае, когда именно первый аргумент (т.е. X) больше
второго аргумента (т.е. Y)



упр 5

объявляется функция mystery (тайна)
функция имеет два аргумента

(b) (defun mystery (x y)
условие:
если y - пуст, ноль
вернуть - пустой список nil
   (if (null y)
    nil
предикат eql проверяет два аргумента на идентичность
если (car y) есть в списке x
вернуть ноль
 (if (eql (car y) x)
   0
оператор let
вводит новые локальные переменные:
далее, следует выражение, которое вычисляется по порядку

к локальной переменной z прибавляется единица
   (let ((z (mystery x (cdr y))))
     (and z (+ z 1))))))


упр 6
см. коммит

https://github.com/helaveesa/lisptests/commit/6292204ff117bf75819d009a56c7dbc170b188ca


упр 7

определить функцию,
которая проверяет
является ли списком хотя бы один элемент списка

список - последовательность из нуля или более элементов,
заключенных в скобки

чтобы Лисп не счел список вызовом функции - список цитируют

(list '(+ 2 1) (+ 5 4))
((+ 2 1) 9)

функция listp возвращает истину, если ее аргумент - список

если рассматривать объект как список:

CL-USER> (defun search-member (obj lst)
           (if (null nil)
               lst
               (if (eql (car lst) obj)
                   lst
                   (search-member obj (cdr lst)))))
SEARCH-MEMBER
CL-USER> (search-member '(a b c) '(a b c d e f))
(A B C D E F)



упр 8

предложите
итеративное и рекурсивное
определение функции, которая:

(а) печатает кол-во точек, которое равно заданному положительному
целому числу

(в) возвращает кол-во символов а в заданном списке


версия функции (а)

существует макрос ntimes, который вычисляет свое тело n раз

(ntimes 10
                 (princ "."))

вернул ошибку:

The function COMMON-LISP-USER::NTIMES is undefined.
   [Condition of type UNDEFINED-FUNCTION]

просто напечатать точку или другой символ может основная функция
вывода format:

CL-USER> (format t ".")
.
NIL

теперь надо вызвать эту функцию много раз, например 5 раз, чтобы
напечатать 5 точек, для этого обратимся к рекурсии и итерации

для цикла надо использовать do или loop

повторим функцию, которая печатает точку столько раз,
сколько напечатанных точек мы хотим получить

инфoрмация по функции format
http://lisper.ru/pcl/a-few-format-recipes


полезное:
http://homelisp.ru/help/classic_funct.html


DOTIMES
Цикл заданное число раз.

принадлежит к классу FSUBR
Эта функция обеспечивает выполнение блока кода заданное число
раз. Синтаксис вызова функции следующий:


(dotimes (переменная_цикла
          число_повторений
          результат)

         (форма1)
         (форма2)
         …
         (формаn)
)


Вычисление происходит так. Переменная цикла последовательно получает
значения от 0 до значения число_повторений-1. При каждом значении
переменной цикла последовательно вычисляются формы (форма1) -
(формаn). По завершении цикла вычисляется форма-результат и
возвращается в качестве результата DOTIMES. Вот как это выглядит:


(dotimes
   (i 5 t)
      (print 'i=)
      (printline i)
)

i=0
i=1
i=2
i=3
i=4

==> T



Для досрочного выхода из цикла можно использовать функцию RETURN:


(dotimes (i 10 t)

         (print 'i=)
         (printline i)
         (if (= i 7) (return 'ok) nil)
)

i=0
i=1
i=2
i=3
i=4
i=5
i=6
i=7

==> ok



Источник:
http://homelisp.ru/help/classic_funct.html#DOTIMES















