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










