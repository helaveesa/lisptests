
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
(defvar *z* 0)

первоначально присвоим ей значение ноль, так как мы будем считать
буквы а именно в эту переменную, а точку отсчета примем за ноль.


3.

