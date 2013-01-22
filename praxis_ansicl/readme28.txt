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


попробуем решить задачу с точками с помощью dotimes

используем функции:
do
format
progn
>

(DO (
      (i 1 (+ i 1))
      (j 1 (+ j 1)))
      ((> j 5) (printline 'ok) (printline 'ok) (printline 'ok))
      (print 'i=) (print i) (prints " ") (print 'j=) (printline j)
)


CL-USER> (defun tochka (b)
           (do ((x 0 (+ x 1)))
               ((>= x b))
             (progn
               (format t "~% x=~A" "."))))
STYLE-WARNING: redefining COMMON-LISP-USER::TOCHKA in DEFUN
TOCHKA
CL-USER> (tochka 6)

 x=.
 x=.
 x=.
 x=.
 x=.
 x=.
NIL


Верная версия

CL-USER> (defun tochka (b)
           (do ((x 0 (+ x 1)))
               ((>= x b))
             (progn
               (format t "." "~% x=~A"))))
;
; caught STYLE-WARNING:
;   Too many arguments (1) to FORMAT ".": uses at most 0.
;   See also:
;     The ANSI Standard, Section 22.3.10.2
;
; compilation unit finished
;   caught 1 STYLE-WARNING condition
STYLE-WARNING: redefining COMMON-LISP-USER::TOCHKA in DEFUN
TOCHKA
CL-USER> (tochka 6)
......
NIL


(b)

предложить определение функции, которая возвращает
количество символов "а" в заданном списке


построение списков - с помощью cons

(cons 'a '(b c d))
(A B C D)

функция, которая возвращает t, если ее аргумент - список
list

новые функции можно определить с помощью defun
принимает три или более аргументов

функция вывода - format
принимает два или более аргументов


CL-USER> (defun our-member (obj lst)
           (if (null lst)
              nil
              (if (eql (car lst) obj)
               obj
               (our-member obj (cdr lst))
               (do ((obj 0 (+ obj 1)))
                   ((= obj a))
                 (progn
                   (format t "a" "~% obj=~A"))))))


; in: DEFUN OUR-MEMBER
;     (IF (EQL (CAR LST) OBJ)
;         OBJ
;         (OUR-MEMBER OBJ (CDR LST))
;         (DO ((OBJ 0 (+ OBJ 1))) ((= OBJ A)) (PROGN (FORMAT T "a" "~% obj=~A"))))
;
; caught ERROR:
;   error while parsing arguments to special form IF:
;     invalid number of elements in
;       ((EQL (CAR LST) OBJ) OBJ (OUR-MEMBER OBJ (CDR LST))
;        (DO ((OBJ 0 #)) ((= OBJ A)) (PROGN (FORMAT T "a" "~% obj=~A"))))
;     to satisfy lambda list
;       (SB-C::TEST SB-C::THEN &OPTIONAL SB-C::ELSE):
;     between 2 and 3 expected, but 4 found

;     (SB-INT:NAMED-LAMBDA OUR-MEMBER
;         (OBJ LST)
;       (BLOCK OUR-MEMBER
;         (IF (NULL LST)
;             NIL
;             (IF (EQL # OBJ)
;                 OBJ
;                 (OUR-MEMBER OBJ #)
;                 (DO # # #)))))
; ==>
;   #'(SB-INT:NAMED-LAMBDA OUR-MEMBER
;         (OBJ LST)
;       (BLOCK OUR-MEMBER
;         (IF (NULL LST)
;             NIL
;             (IF (EQL # OBJ)
;                 OBJ
;                 (OUR-MEMBER OBJ #)
;                 (DO # # #)))))
;
; caught STYLE-WARNING:
;   The variable OBJ is defined but never used.
;
; compilation unit finished
;   caught 1 ERROR condition
;   caught 1 STYLE-WARNING condition
OUR-MEMBER
CL-USER> (our-member 'a '(a b c a d e f a a r t a))


вернул ошибку на данный код:

Execution of a form compiled with errors.
Form:
  (IF (EQL (CAR LST) OBJ)
    OBJ
    (OUR-MEMBER OBJ (CDR LST))
    (DO ((OBJ 0 (+ OBJ 1))) ((= OBJ A)) (PROGN (FORMAT T a ~%
    obj=~A))))
Compile-time error:
  error while parsing arguments to special form IF:
  invalid number of elements in
    ((EQL (CAR LST) OBJ) OBJ (OUR-MEMBER OBJ (CDR LST))
     (DO ((OBJ 0 (+ OBJ 1))) ((= OBJ A)) (PROGN (FORMAT T "a" "~%
     obj=~A"))))
  to satisfy lambda list
    (SB-C::TEST SB-C::THEN &OPTIONAL SB-C::ELSE):
  between 2 and 3 expected, but 4 found
   [Condition of type SB-INT:COMPILED-PROGRAM-ERROR]


Исполнение форме составлен с ошибками.
Форма:
   (IF (EQL (CAR LST) OBJ)
     OBJ
     (OUR-ЧЛЕНОВ OBJ (CDR LST))
     (DO ((OBJ 0 (+ OBJ 1))) ((= OBJ)) (PROGN (FORMAT T ~%
     Объект = ~))))
Ошибка времени компиляции:
   Ошибка при разборе аргументов в специальной форме, ЕСЛИ:
   неверное число элементов в
     ((EQL (CAR LST) OBJ) OBJ (OUR-ЧЛЕНОВ OBJ (CDR LST))
      (DO ((OBJ 0 (+ OBJ 1))) ((= OBJ)) (PROGN (FORMAT T "" "~%
      Объект = ~ "))))
   , чтобы удовлетворить лямбда-список
     (SB-C :: TEST SB-C :: ТОГДА И ДОПОЛНИТЕЛЬНЫЕ SB-C :: ELSE):
   между 2 и 3 ожидали, но 4 найдено

CL-USER> (defun letter (obj lst)
           (if (null lst)
              nil
              (find #\a lst)))


; in: DEFUN LETTER
;     (SB-INT:NAMED-LAMBDA LETTER
;         (OBJ LST)
;       (BLOCK LETTER
;         (IF (NULL LST)
;             NIL
;             (FIND #\a LST))))
; ==>
;   #'(SB-INT:NAMED-LAMBDA LETTER
;         (OBJ LST)
;       (BLOCK LETTER
;         (IF (NULL LST)
;             NIL
;             (FIND #\a LST))))
;
; caught STYLE-WARNING:
;   The variable OBJ is defined but never used.
;
; compilation unit finished
;   caught 1 STYLE-WARNING condition
LETTER
CL-USER> (letter 'a '(a b c d a f r a g a))
NIL

сработало условие пустого списка
редактируем снова

вернул вот такую ошибку:

Value of #\a in (= X #\a) is #\a, not a NUMBER.
   [Condition of type SIMPLE-TYPE-ERROR]

на вот этот код:

CL-USER> (defun letter-a (x lst)
           (if (null lst)
               nil)
               (if (= x #\a)
                   (+ x 1)
                   lst))



; in: DEFUN LETTER-A
;     (= X #\a)
;
; caught WARNING:
;   Constant #\a conflicts with its asserted type NUMBER.
;   See also:
;     The SBCL Manual, Node "Handling of Types"
;
; compilation unit finished
;   caught 1 WARNING condition
STYLE-WARNING: redefining COMMON-LISP-USER::LETTER-A in DEFUN
LETTER-A
CL-USER> (letter-a 0 '(a b a c d a))

вот такая ошибка:

#\a found where a LOOP keyword or LOOP type keyword expected
current LOOP context: COLLECT CHAR #\a.
   [Condition of type SB-INT:COMPILED-PROGRAM-ERROR]

на вот этот код:

CL-USER> (defun letter-a (char lst)
           (if (null lst)
               nil)
               (loop for char across lst collect char #\a))



; in: DEFUN LETTER-A
;     (LOOP FOR CHAR ACROSS LST
;           COLLECT CHAR #\a)
;
; caught ERROR:
;   during macroexpansion of (LOOP FOR CHAR ...). Use *BREAK-ON-SIGNALS* to
;   intercept:
;
;    #\a found where a LOOP keyword or LOOP type keyword expected
;   current LOOP context: COLLECT CHAR #\a.

;     (SB-INT:NAMED-LAMBDA LETTER-A
;         (CHAR LST)
;       (BLOCK LETTER-A
;         (IF (NULL LST)
;             NIL)
;         (LOOP FOR CHAR ACROSS LST
;               COLLECT CHAR #\a)))
; ==>
;   #'(SB-INT:NAMED-LAMBDA LETTER-A
;         (CHAR LST)
;       (BLOCK LETTER-A
;         (IF (NULL LST)
;             NIL)
;         (LOOP FOR CHAR ACROSS LST
;               COLLECT CHAR #\a)))
;
; caught STYLE-WARNING:
;   The variable CHAR is defined but never used.
;
; compilation unit finished
;   caught 1 ERROR condition
;   caught 1 STYLE-WARNING condition
STYLE-WARNING: redefining COMMON-LISP-USER::LETTER-A in DEFUN
LETTER-A
CL-USER> (letter-a #\a '(a b a c d a))


вывести букву а

CL-USER> (format t "a" "~% ~A")
a
NIL


Итерация по списку

(dolist (x '(a b c d e))
        (print x))

A
B
C
D
E
NIL


Два частых варианта использования format

(format t "string") ; напечатает строку в поток вывода
(format nil "string") ; вернёт полученную строку



Исполнит все аргументы, но вернуть значение последнего

(progn 1 2 3)

3


Исполнит все аргументы, но вернуть значение первого

(prog1 1 2 3)

1


Замерить время выполнения участка кода

(defun add-n-squares (n)
  (do ((i 0 (+ i 1))
       (sum 0 (+ sum (* i i))))
    ((> i n) sum)))

(time (add-n-squares 10000))

Evaluation took:
  0.001 seconds of real time
  0.004000 seconds of total run time (0.004000 user, 0.000000 system)
  400.00% CPU
  3,090,464 processor cycles
  212,792 bytes consed

333383335000



Создать хэш-таблицу изначально большого размера.

(defparameter *my-hash* (make-hash-table :size 100000))
; *MY-HASH*
(hash-table-size *my-hash*)
; 100000
(time (dotimes (n 100000) (setf (gethash n *my-hash*) n)))
; Compiling LAMBDA NIL:
; Compiling Top-Level Form:
;
; Evaluation took:
;   0.04 seconds of real time
;   0.04 seconds of user run time
;   0.0 seconds of system run time
;   0 page faults and
;   0 bytes consed.
; NIL




Источник:

http://ru.najomi.org/common-lisp





(defun letter-a (obj lst x)
  (if (null lst)
      nil
      (do (= obj "a")
          (x 0 (+ x 1))
       (princ x))))

разница между рекурсией и итерацией тут
http://www.ctc.msiu.ru/materials/Book/node57.html


рекурсия - способ решения задачи, когда каждый последующий шаг
делается так же, как и предыдущий, но известно, что со следующего шага
задача решается проще, чем с предыдущего.
самовызов

итеративный способ - это решение задачи, когда каждый последующий шаг
не обязательно является упрощённым условием решения предыдущего, но
могут измениться условия выполнения.
цикл

Рекурсия -- это такой способ организации обработки данных, при котором
программа вызывает сама себя непосредственно, либо с помощью других
программ.

Итерация -- способ организации обработки данных, при котором
определенные действия повторяются многократно, не приводя при этом к
рекурсивным вызовам программ.


рекурсия:

(defun p (lst)
  (if (not (null lst))
      (progn
        (print (car lst))
        (p (cdr lst)))))

(p '(a b c d))


итерация:

(defun p2 (lst)
  (do ((i 0))
      ((>= i (length lst)))
    (progn
      (print (nth i lst))
      (setf i (+ i 1)))))

(p2 '(a b c d))


это говорит о том, что и итер и рекус функции так или иначе зациклены
только рекурсив функция зациклена сама на себе, а итерац функция -
просто цикл



Алгоритм для упр 8 (b)

1. Обьявление функции:

(функция имя_функции (список_аргументов_функции)
проверяем список, который задали в списке_аргументов
пуст список или нет
         условие
         используем оператор if
         (условие "если" (тест-выражение)
если тест выражение истино,то возвращаем nil (это then-выражение)
(т.е. да, список пуст)
если тест выражение ложно, то переходим к вычислению else-выражения
в данном случае это будет код
по сравнению букв в списке с буквой а
(так как, скорее всего список будет не из одного элемента,
то для повторного сравнения, нужно будет создать цикл (итерация или
рекурсия)
условия:
если есть совпадение, т.е а=а то нужно запомнить это совпадение,
запишем в созданную локальную переменную цифру 1, и каждый раз при
совпадении а=а мы будем прибавлять единицу в переменную, таким образом
мы сосчитаем все буквы а с списке

если нет совпадения, то мы ничего не прибавляем, просто дальше
сравниваем буквы из списка с буквой а

в конце функции нужно будет вывести на печать результат, который
записался в переменную

2. Вызов функции
---------------------------
более короткий алгоритм

нужна функция, которая считает кол-во "а" в списке
эта функция принимает на вход список, и возвращает кол-во букв "а" в нем
---------------------------------------------------------------------------
1. <список пуст?>
  1.1. да -> возвращаем nil и выходим
  1.2. нет -> выполняем сравнение с буквой "а":

2. <итерация с помощью dolist>
   (dolist (var list &optional result) &body body)

   2.1. буква в списке совпадает с "а"?
   2.2. вводим глобальную переменную с помощью оператора defparameter *glob*
        имя данной локальной переменной *glob* (окружена символами "*")
        2.1.1. да -> увеличиваем переменную *glob* на единицу
               (+ *glob* 1)
        2.1.2. нет -> возвращаемся к пункту 1.2.
3. <печатаем значение глобальной переменной *glob*>
   (format t "*glob*=~A")
----------------------------------------------------------

сначала напечатаем имя функции с параметрами

(defun letter-a (lst)

теперь составим цикл:

(do ((i 0))
      ((>= i (length lst)))
    (progn
      (print (nth i lst))
      (setf i (+ i 1))))

теперь введем локальную переменную, куда можно будет записать итог
подсчета букв а

(let (result 0))

теперь напишем условие, при котором будет выполняться цикл

(if (null lst)
    (let (result 0))
    (char= #\a (length lst)))


вот код:

(defun letter-a (lst)
           (do ((i 0))
               ((>= i (length lst)))
             (progn
               (print (nth i lst))
               (setf i (+ i 1)))
           (if (null lst)
               (lst)
               (char= #\a (length lst)))))

вызов функции:

(letter-a '(#\b #\c #\d #\a #\f #\t #\a #\g #\k #\a))


вернул ошибку:

Value of #1=(LENGTH LST) in
  (CHAR= #\a #1#)
is
  10,
not a
  CHARACTER.
   [Condition of type SIMPLE-TYPE-ERROR]


на вот этот код:

CL-USER> (defun letter-a (lst)
           (let ((result)))
           (do ((i 0))
               ((>= i (length lst)))
             (progn
               (print (nth i lst))
               (setf i (+ i 1)))
           (if (null lst)
               (lst)
               (char= #\a (length lst)))))
; in: DEFUN LETTER-A
;     (LET ((RESULT))
;       )
;
; caught STYLE-WARNING:
;   The variable RESULT is defined but never used.

;     (CHAR= #\a (LENGTH LST))
;
; caught WARNING:
;   Derived type of (LENGTH LST) is
;     (VALUES (MOD 536870909) &OPTIONAL),
;   conflicting with its asserted type
;     CHARACTER.
;   See also:
;     The SBCL Manual, Node "Handling of Types"

; in: DEFUN LETTER-A
;     (LST)
;
; caught STYLE-WARNING:
;   undefined function: LST
;
; compilation unit finished
;   Undefined function:
;     LST
;   caught 1 WARNING condition
;   caught 2 STYLE-WARNING conditions
LETTER-A
CL-USER> (letter-a '(#\b #\c #\d #\a #\f #\t #\a #\g #\k #\a))

#\b


пробуем другой вариант:
будем проверять код по частям:

сначала проверим цикл:

CL-USER> (defun letter-a (lst)
           (do ((i 0))
               ((>= i (length lst)))
             (progn
               (print (nth i lst))
               (setf i (+ i 1)))))

STYLE-WARNING: redefining COMMON-LISP-USER::LETTER-A in DEFUN
LETTER-A
CL-USER> (letter-a '(#/b #/c #/a #/e #/f #/s #/a))

B
C
D
A
E
F
S
A
NIL

nth - это доступ к частям списка, функция, которая помогает получить
элемент с определенным индексом

если убрать (setf i (+ i 1)) вот эту строчку
цикл никогда не закончится

теперь нужно написать часть по сравнению

(char= #/a (nth lst))


отдельные части кода работают:

CL-USER> (defun letter-a (lst)
             (if (null lst)
                 nil
                 (progn
                   (print "Вывод кол-ва встречаемых символов а на
             экран"))))
STYLE-WARNING: redefining COMMON-LISP-USER::LETTER-A in DEFUN
LETTER-A
CL-USER> (letter-a '(a b c s d f c v g))

"Вывод кол-ва встречаемых символов а на экран"
"Вывод кол-ва встречаемых символов а на экран"


(defun letter-a (lst)
           (do ((i 0))
               ((>= i (length lst)))
             (if (null lst)
                 nil
                 (char= #/a nth)
             (progn
               (print (nth i lst))
               (setf i (+ i 1))))))

вернул мне ошибку:

((NULL LST) NIL (CHAR= #\a NTH LST) (PROGN (SETF I (+ I 1))))
  to satisfy lambda list
    (SB-C::TEST SB-C::THEN &OPTIONAL SB-C::ELSE):
  between 2 and 3 expected, but 4 found
   [Condition of type SB-INT:COMPILED-PROGRAM-ERROR]


на вот этот код:

CL-USER> (defun letter-a (lst)
           (let (result i)
             (format t "~%~A" lst)
           (do ((i 0))
               ((>= i (length lst)))
             (if (null lst)
                 nil
                 (char= #\a nth lst)
             (progn
               (setf i (+ i 1)))))))
; in: DEFUN LETTER-A
;     (IF (NULL LST)
;         NIL
;         (CHAR= #\a NTH LST)
;         (PROGN (SETF I (+ I 1))))
;
; caught ERROR:
;   error while parsing arguments to special form IF:
;     invalid number of elements in
;       ((NULL LST) NIL (CHAR= #\a NTH LST) (PROGN (SETF I #)))
;     to satisfy lambda list
;       (SB-C::TEST SB-C::THEN &OPTIONAL SB-C::ELSE):
;     between 2 and 3 expected, but 4 found

;     (LET (RESULT I)
;       (FORMAT T "~%~A" LST)
;       (DO ((I 0))
;           ((>= I (LENGTH LST)))
;         (IF (NULL LST)
;             NIL
;             (CHAR= #\a NTH LST)
;             (PROGN (SETF #)))))
;
; caught STYLE-WARNING:
;   The variable RESULT is defined but never used.
;
; caught STYLE-WARNING:
;   The variable I is defined but never used.
;
; compilation unit finished
;   caught 1 ERROR condition
;   caught 2 STYLE-WARNING conditions
STYLE-WARNING: redefining COMMON-LISP-USER::LETTER-A in DEFUN
LETTER-A
CL-USER> (letter-a '(#\a #\b #\c #\d #\a #\f #\a #\g #\a))

(a b c d a f a g a)


напечатал, вернул мне список, который я ввела в вызове функции

не понимаю, что не так в условии "если":

CL-USER> (defun letter-a (lst)
           (do ((i 0))
               ((>= i (length lst)))
             (if (null lst)
                 nil
                 (char= #\a (nth lst))
                 (progn
                   (setf i (+ i 1)
                         (format t "~% ~A" nth i))))))
; in: DEFUN LETTER-A
;     (IF (NULL LST)
;         NIL
;         (CHAR= #\a (NTH LST))
;         (PROGN
;          (SETF I (+ I 1)
;                (FORMAT T "~% ~A" NTH I))))
;
; caught ERROR:
;   error while parsing arguments to special form IF:
;     invalid number of elements in
;       ((NULL LST) NIL (CHAR= #\a (NTH LST))
;        (PROGN
;         (SETF I #
;               #)))
;     to satisfy lambda list
;       (SB-C::TEST SB-C::THEN &OPTIONAL SB-C::ELSE):
;     between 2 and 3 expected, but 4 found
;
; compilation unit finished
;   caught 1 ERROR condition
STYLE-WARNING: redefining COMMON-LISP-USER::LETTER-A in DEFUN
LETTER-A

продолжение...

CL-USER> (defun letter-a (lst)
           (let ((result 0))
             (do ((i 0))
                 ((>= i (length lst)))
               (if (null lst)
                   nil
                   (if (char= #\a (nth lst))
                       (progn
                         (print (nth i lst))
                         (setf i (+ i 1))))))))
; in: DEFUN LETTER-A
;     (NTH LST)
;
; caught WARNING:
;   The function was called with one argument, but wants exactly two.

;     (LET ((RESULT 0))
;       (DO ((I 0))
;           ((>= I (LENGTH LST)))
;         (IF (NULL LST)
;             NIL
;             (IF (CHAR= #\a #)
;                 (PROGN # #)))))
;
; caught STYLE-WARNING:
;   The variable RESULT is defined but never used.

;     (SB-INT:NAMED-LAMBDA LETTER-A
;         (LST)
;       (BLOCK LETTER-A
;         (LET ((RESULT 0))
;           (DO (#)
;               (#)
;             (IF #
;                 NIL
;                 #)))))
; ==>
;   #'(SB-INT:NAMED-LAMBDA LETTER-A
;         (LST)
;       (BLOCK LETTER-A
;         (LET ((RESULT 0))
;           (DO (#)
;               (#)
;             (IF #
;                 NIL
;                 #)))))
;
; caught STYLE-WARNING:
;   (The function was previously called with two arguments, but wants at most one.)
;
; compilation unit finished
;   caught 1 WARNING condition
;   caught 2 STYLE-WARNING conditions
LETTER-A
CL-USER> (letter-a '(b c d a e f s a))

вернул ошибку:
неверное число аргументов: 1

другой вариант:

CL-USER> (defun letter-a (lst)
           (do ((i 0))
               ((>= i (length lst)))
             (if (null lst)
                 nil
                 (if (count #\a (lst) :test #'equal)
                     (progn
                       (print (nth i lst))
                       (setf i (+ i 1)))))))

; in: DEFUN LETTER-A
;     (LST)
;
; caught STYLE-WARNING:
;   undefined function: LST
;
; compilation unit finished
;   Undefined function:
;     LST
;   caught 1 STYLE-WARNING condition
STYLE-WARNING: redefining COMMON-LISP-USER::LETTER-A in DEFUN
LETTER-A
CL-USER> (letter-a '(#\a #\b #\c #\a #\d #\a))

пишет, что Функция COMMON-LISP-USER :: LST не определено.
надо ее определить

