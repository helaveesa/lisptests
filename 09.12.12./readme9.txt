
1. начну с того, что прочту файл (именно прочту, а не только открою)

Алгоритм по заданию:

Сосчитать все буквы "а" в некотором,заданном тексте.

(let ((in (open "/home/helaveesa/repo/testslisp/09.12.12/text9.txt" :if-does-not-exist nil)))
  (when in
    (loop for line = (read-char in nil)
         while line do (format t "~a~%" line))
    (close in)))

тестируем:
.................

итог тестирования:
все, ок.
; SLIME 2011-08-26
CL-USER> (let ((in (open
"/home/helaveesa/repo/testslisp/09.12.12/text9.txt" :if-does-not-exist
nil)))
             (when in
                   (loop for line = (read-char in nil)
                                 while line do (format t "~a~%" line))
                       (close in)))
NIL
CL-USER>


2. Теперь нужно объявить переменную char, в которую будут заноситься
все случаи встречи с буквой "а"

Ищем как объявить переменную в лисп:

http://lispnik.livejournal.com/9137.html

Имена динамических переменных обрамляются звёздочками по традиции,
чтобы можно по имени переменной понять, является ли она динамической.

Итак, объявляем переменную:
(defvar/defparameter *z* 0)

первоначально присвоим ей значение ноль, так как мы будем считать
буквы а именно в эту переменную, а точку отсчета примем за ноль.


Соединим эти два кода:

(let ((in (open "/home/helaveesa/repo/testslisp/09.12.12/text9.txt" :if-does-not-exist nil)))
  (when in
    (loop for line = (read-char in nil)
         while line do (defparameter *z* 0))
    (close in)))

4. Разберемся с условиями:

Источник:
http://aco.ifmo.ru/~nadinet/html/other/lsp_book/lisp.html#_Toc465260932


(if (= 1 3) "Yes!!" "no.") возвращает "no."

в моем случае:

(if (= char "а") (+ 1 *z*)) записывает единицу в переиенную *z*

5. Соединим наш код:

(let ((in (open "/home/helaveesa/repo/testslisp/09.12.12/text9.txt"
:if-does-not-exist nil)))
  (when in
    (loop for line = (read-char in nil)
         while line do (defparameter *z* 0))
         (if (= char "а") (+ *z* 1))
    (close in)))

тестируем:
...............

итог тестирования:

выдал NIL

CL-USER> (let ((in (open
"/home/helaveesa/repo/testslisp/09.12.12/text9.txt"
                         :if-does-not-exist nil)))
             (when in
                   (loop for line = (read-char in nil)
                                 while line do (defparameter *z* 0))
                            (if (= char "а") (+ *z* 1))
                                (close in)))
; in:
;      LET ((IN
;        (OPEN "/home/helaveesa/repo/testslisp/09.12.12/text9.txt"
;              :IF-DOES-NOT-EXIST NIL)))
;     (= CHAR "а")
;
; caught WARNING:
;   Constant "а" conflicts with its asserted type NUMBER.
;   See also:
;     The SBCL Manual, Node "Handling of Types"

; in:
;      LET ((IN
;        (OPEN "/home/helaveesa/repo/testslisp/09.12.12/text9.txt"
;              :IF-DOES-NOT-EXIST NIL)))
;     (+ *Z* 1)
;
; caught WARNING:
;   undefined variable: *Z*

;     (= CHAR "а")
;
; caught WARNING:
;   undefined variable: CHAR
;
; compilation unit finished
;   Undefined variables:
;     *Z* CHAR
;   caught 3 WARNING conditions
NIL
CL-USER>

и в мини-буфере пишет:

(let bindings &body body)


6.
