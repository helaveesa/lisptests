\\\\\\\\\\\\\\\\\\\\\


readme 4

Алгоритм по заданию:

Сосчитать все буквы "а" в некотором,заданном тексте.

Мои мысли по поводу этого:

1. Подумать)

2. Подумать еще лучше...

2.1. Вспомнить, что такое алгоритм (блок-схема, логика, построение
логических схем)
http://www.lessons-tva.info/edu/e-inf1/e-inf1-4-2.html
http://comp-science.narod.ru/Algor/Algor_For_Site.html
http://einf.gym5cheb.ru/p9aa1.html

3. Вспомнить некоторые команды и функции, операторы языка Lisp

4. Прочитать мои записи

5. Обратиться к литературе "Мир Лиспа"

6. Прочесть необходимые разделы в сети интернет:
http://lisper.ru/pcl/files-and-file-io
http://www.lisp.ru/list.php?c=articles
http://ru.najomi.org/common-lisp
http://www.cardarmy.ru/proekt/lisp/art4.htm
http://restas.lisper.ru/ru/tutorial/pastebin.html
http://www.hardforum.ru/archive/f-142-p-2.html
http://acl.achim.ru/book/get_section/15
http://ru.wikipedia.org/wiki/Common_Lisp
http://www.ibm.com/developerworks/ru/library/j-cb02067/index.html
http://www.cad.dp.ua/kurs/LECTURE5/lecture5.html
http://homelisp.ru/help/lisp.html#u01
http://aco.ifmo.ru/~nadinet/html/other/lsp_book/lisp.html
http://homelisp.ru/help/samples.html
http://lisp.ru/page.php?id=8
http://pcl.catap.ru/doku.php?id=pcl:%D1%82%D1%83%D1%80%D0%B2repl
http://cl-cookbook.sourceforge.net/strings.html#substrings
http://lispnik.livejournal.com/9137.html
http://ru.wikibooks.org/wiki/%CB%E8%F1%EF/%D4%F3%ED%EA%F6%E8%E8
http://lisp.ru/page.php?id=5

7. вот на прочтение чего, я потратила весь день 3 декабря 2012 года,
много интересного, много непонятного

8. Я нашла как:
-вывод на экран того, что напечатано
(setq input (read))

////////////////////////////////
CL-USER> (setq input (read))

; in: SETQ INPUT
; (SETQ INPUT (READ))
;
; caught WARNING:
; undefined variable: INPUT
;
; compilation unit finished
; Undefined variable:
; INPUT
; caught 1 WARNING condition
/////////////////////////////////
ждет ввода

вводим:
mama

выводит:
MAMA

-условия

(if условие то-форма иначе-форма)

например:

(if (> x 0) (setq y (+ y x)) (setq y (- y x)))

-присвоение символу значения
(setq x "value-of-x")
-вывод значения символа
(symbol-value 'x)

-создала файл с расширением .txt, в котором напечатан некоторый текст,
 с которым я буду работать (именно в нем считать кол-во всех букв "а")

-открыть файл можно следующим образом:
(open "/repo/testslisp/04.12.12/text1.txt")

-"для того, чтобы напечатать первую строку файла, вы можете
 комбинировать OPEN, READ-LINE, CLOSE следующим образом:"
(let ((in (open "/some/file/name.txt")))
  (format t "~a~%" (read-line in))
  (close in))

Источник: http://lisper.ru/pcl/files-and-file-io

-создать новый файл можно так:
Создать файл можно так:

(with-open-file (stream "/name_papka1/name_papka2/name_file.txt"
:direction :output)
  (format stream "Какой-то текст."))

Источник: http://lisper.ru/pcl/files-and-file-io

-можно считывать данные из строки или записывать их в строку,
 используя STRING-STREAM, которые вы можете создать функциями
 MAKE-STRING-INPUT-STREAM и MAKE-STRING-OUTPUT-STREAM.

-Макрос WITH-OUTPUT-TO-STRING также связывает вновь созданный
 строковый поток вывода с переменной, вами названной, и затем
 выполняет код в своем теле. После того, как код был выполнен,
 WITH-OUTPUT-TO-STRING вернет значение, которое было бы возвращено
 GET-OUTPUT-STREAM-STRING.

CL-USER> (with-output-to-string (out)
            (format out "hello, world ")
            (format out "~s" (list 1 2 3)))
"hello, world (1 2 3)"

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\




readme 5

1. создала документ (файл), из которого
будет счиываться текст, и осуществляться поиск буквы "а"

2. запустила CL

3. нужно открыть этот файл

   3.1.имя файла "text5.txt"
   3.2. расположение файла
   /home/helaveesa/repo/testslisp/05.12.12/text5.txt
   3.3. функция в CL, которая открывает файл
   3.4.поиск...

   http://www.lispworks.com/documentation/HyperSpec/Front/Contents.htm
   http://www.hardforum.ru/t51494/

   3.5.возможно вот это:

   (with-open-file (stream "/tmp/a.lisp")
     (loop for line = (read-line stream nil nil)
        while line
        count t into count
        finally (format t "File has ~D line~:P.~%" count)))

   Примечание!
   В моем случае читать по символьно, а не всю строку.
   Изучение:
   http://www.mari-el.ru/mmlab/home/lisp/LECTION10/index.html

   Перепишем:
   (with-open-file (stream "/tmp/a.lisp")
     (loop for line = (read-line stream nil nil)
        while line
        count t into count
        finally (format t "File has ~D line~:P.~%" count)))

   *** Что такое stream? ***
   Ответ: "При вводе и выводе информации в Лиспе используется
   понятие потоков - stream"

   Важное дополнение:
   "Для потока определены ИМЯ , операции открытия open операции
   закрытия clouse направления output и input"

   *** Какую функцию использовать? ***
   Ответ: "Для чтения символов из файла будем использовать функцию
   (READ-CHAR <входной поток>)"

   Данная функция позволяет читать печатные символы ( CHAR) из
   файла. В качестве значения получается десятичное представление кода
   символа.

   3.6. надо сменить расширение файла, который буду читать
   смена расширения .txt на .lisp

   3.7. Алгоритм действий:
        -1-использовать функцию для посимвольного ввода информации из
                        файла для ее последующего анализа
        -2-определение функции
                       (setq our-input-stream (open "picture.spl"
   :direction :input))
        -3-надо сменить расширение .lisp на .spl ???
        -4-для чтения именно символа используем
               (read-char our-input-stream)
        -5-будем получать последовательность значений
        43
        43
        43
        45
        45
        45
        10 и т.д.

        т.к. Для восстановления содежимого файла применяется
        перекодировка
        -6-перекодируем
                (setq x (read-char our-input-stream)
        Примечание!
        Чтобы представить информацию без искажений, нужно использовать
        цикл

        (loop (progn (setq x (read-char our-input-stream) )
          (cond (( = x 43) (prin1'+))
               (( = x 45) (prin1 '-))
                (( = x 10 ) (terpri))))))


                После вывода имеем



           ---+++
           +++---

        -7-закрытие входного потока
                    (close our-input-stream)

4.тестируем алгоритм


\\\\\\\\\\\\\\\\\\\\\\\

; SLIME 2011-08-26
CL-USER> (setq our-input-stream (open "text5.lisp" :direction :input))

; in: SETQ OUR-INPUT-STREAM
; (SETQ OUR-INPUT-STREAM (OPEN "text5.lisp" :DIRECTION :INPUT))
;
; caught WARNING:
; undefined variable: OUR-INPUT-STREAM
;
; compilation unit finished
; Undefined variable:
; OUR-INPUT-STREAM
; caught 1 WARNING condition
#<SB-SYS:FD-STREAM for "file
; /home/helaveesa/repo/testslisp/05.12.12./text5.lisp" {B9E4C39}>

\\\\\\\\\\\\\\\\\\\\\\

редактируем:

не работает
:( :( :( :( :( :( :( :( :( :( :( :( :( :( :(

         читаем спец. литературу

         итог:

         изменим файл

        -1- Сформируем файл
        -2- Пусть

        (setq s "авабрт")
        (setq p "бртава"), где s,p - переменные

        -3- Определим поток вывода
         (setq our-output-stream (open "text5.spl" :direction
         :output))

         (princ s our-output-stream) ; записываем первую стороку
         (terpri our-output-stream) ; заканчиваем ее
         (princ p our-output-stream) ; записываем вторую строку
         (terpri our-output-stream) ; заканчиваем файл

        -4- Закрываем файл

        (close our-output-stream)

        -5- В файле теперь находится

        авабрт
        бртава

        -6- Чтение символов из файла

        (READ-CHAR <входной поток>)

        -7- Определим

        (setq our-input-stream (open "picture.spl" :direction :input))

        -8- Для чтения символа используем

        (read-char our-input-stream)

        -9- Тестируем
        ..........................

        -10- Вот, что у меня получилось:

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

CL-USER> (setq s "авабрт")

; in: SETQ S
; (SETQ S "авабрт")
;
; caught WARNING:
; undefined variable: S
;
; compilation unit finished
; Undefined variable:
; S
; caught 1 WARNING condition
"авабрт"
CL-USER> (setq p "бртава")

; in: SETQ P
; (SETQ P "бртава")
;
; caught WARNING:
; undefined variable: P
;
; compilation unit finished
; Undefined variable:
; P
; caught 1 WARNING condition
"бртава"
CL-USER> (setq our-output-stream (open "text5.spl" :direction
; :output))

; in: SETQ OUR-OUTPUT-STREAM
; (SETQ OUR-OUTPUT-STREAM (OPEN "text5.spl" :DIRECTION :OUTPUT))
;
; caught WARNING:
; undefined variable: OUR-OUTPUT-STREAM
;
; compilation unit finished
; Undefined variable:
; OUR-OUTPUT-STREAM
; caught 1 WARNING condition
; Evaluation aborted on #<SB-INT:SIMPLE-FILE-ERROR "~@<~?: ~2I~_~A~:>"
; {AC1EDA1}>.
CL-USER> (setq s "авабрт")

; in: SETQ S
; (SETQ S "авабрт")
;
; caught WARNING:
; undefined variable: S
;
; compilation unit finished
; Undefined variable:
; S
; caught 1 WARNING condition
"авабрт"
CL-USER> (setq p "бртава")

; in: SETQ P
; (SETQ P "бртава")
;
; caught WARNING:
; undefined variable: P
;
; compilation unit finished
; Undefined variable:
; P
; caught 1 WARNING condition
"бртава"
CL-USER> (setq our-output-stream (open "newtext5.spl" :direction
; :output))

; in: SETQ OUR-OUTPUT-STREAM
; (SETQ OUR-OUTPUT-STREAM (OPEN "newtext5.spl" :DIRECTION :OUTPUT))
;
; caught WARNING:
; undefined variable: OUR-OUTPUT-STREAM
;
; compilation unit finished
; Undefined variable:
; OUR-OUTPUT-STREAM
; caught 1 WARNING condition
#<SB-SYS:FD-STREAM for "file
; /home/helaveesa/repo/testslisp/05.12.12./newtext5.spl" {AE9D701}>
CL-USER> (princ s our-output-stream)
"авабрт"
CL-USER> (terpri our-output-stream)
NIL
CL-USER> (princ p our-output-stream)
"бртава"
CL-USER> (terpri our-output-stream)
NIL
CL-USER> (close our-output-stream)
T
CL-USER> (setq our-input-stream (open "newtext5.spl" :direction
; :input))

; in: SETQ OUR-INPUT-STREAM
; (SETQ OUR-INPUT-STREAM (OPEN "newtext5.spl" :DIRECTION :INPUT))
;
; caught WARNING:
; undefined variable: OUR-INPUT-STREAM
;
; compilation unit finished
; Undefined variable:
; OUR-INPUT-STREAM
; caught 1 WARNING condition
#<SB-SYS:FD-STREAM for "file
; /home/helaveesa/repo/testslisp/05.12.12./newtext5.spl" {B0DA5F1}>
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_A
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_VE
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_A
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_BE
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_ER
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_TE
#\Newline
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_BE
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_ER
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_TE
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_A
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_VE
CL-USER> (read-char our-input-stream)
#\CYRILLIC_SMALL_LETTER_A
CL-USER> (read-char our-input-stream)
#\Newline

\\\ конец файла, дальше читать не будет, выдаст ошибку, проверяла \\\

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

6..итог тестирования:
        все символы были выведены на экран

7. полезная ссылка:
   LISP, Чтение и запись в файл
   http://pr0gram.clan.su/publ/razlichnye_stati_o_programmirovanii/lisp_chtenie_i_zapis_v_fajl/1-1-0-47

   -1- исходный код
       (1) (setq
                finp (open "путь к файлу\1.txt" : direction : input)
                     fout (open "путь к файлу\2.txt" : direction :
       output)
           )

           (2) (loop
                (if (not(setq sym(read-char finp))) (return))
                    (if (eq sym #\a) (setq sym #\b))
                        (write-char sym fout)
                 )

                 (3) (close finp)
                     (close fout)


   -2- то, что нужно мне
   (1)

   (setq
        finp (open
        "home/helaveesa/repo/testslisp/05.12.12/text5input.txt" :
        direction : input)
        fout (open
        "home/helaveesa/repo/testslisp/05.12.12/text5output.txt" :
        direction : output))

   (2)
   (loop
        (if (not(setq sym(read-char finp))) (return))
        (if (eq sym #\a) (setq sym #\1))
      (write-char sym fout))

   (3)
   (close finp)
   (close fout)

8. тестируем
.....................

9. итог тестирования:

сбрали весь код:

CL-USER> (setq
          finp (open
          "home/helaveesa/repo/testslisp/05.12.12/text5input.txt" :
          direction : input)
          fout (open
          "home/helaveesa/repo/testslisp/05.12.12/text5output.txt" :
          direction : output)

          (loop
             (if (not(setq sym(read-char finp))) (return))
             (if (eq sym #\a) (setq sym #\1))
             (write-char sym fout)

             (close finp)
             (close fout)))

, где

setq - присвоение переменной какого-либо значения
loop - цикл, можно и самим догадаться

Code:
(if (not(setq sym(read-char finp))) (return))
Читает символ из потока finp пока не дойдёт до конца файла.


Code:
(if (eq sym #\a) (setq sym #\b))
Сравниваем символ на эквивалентность символу a


Code:
(write-char sym fout)
Пишем символ (или изменённый символ) во второй файл, т.е. используем
дескриптор fout


Не забываем закрыть файлы, иначе ничего не выйдет
(close finp)
(close fout)



минибуфер выдает:
illegal terminating character after a colon: #\
незаконное прекращение символа после двоеточия: # \
                                                                                                                                        Line:
                                                                                                                                        2,
                                                                                                                                        Column:
                                                                                                                                        77,
                                                                                                                                        File-Position:
                                                                                                                                        82

Stream: #<SB-IMPL::STRING-INPUT-STREAM {BB6AAB1}>
   [Condition of type SB-INT:SIMPLE-READER-ERROR]

НАДО РАЗБИРАТЬСЯ ЧТО НЕ ТАК!!!


10. Пробуем снова!
Мы так быстро не сдаемся!

(let ((in (open "/home/helaveesa/repo/testslisp/05.12.12/text5.txt"
:if-does-not-exist nil)))
  (when in
    (loop for line = (read-char in nil)
         while line do (format t "~a~%" line))
    (close in)))

11. Тестирование
.......................

12. Итог тестирования:
все ок, минибуфер выдал конец файла, то есть NIL

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

CL-USER> (let ((in (open
"/home/helaveesa/repo/testslisp/05.12.12/text5.txt" :if-does-not-exist
nil)))
             (when in
                   (loop for line = (read-char in nil)
                                 while line do (format t "~a~%" line))
                       (close in)))
NIL

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\

13. снова определим переменные:

Пусть

(setq s "Баллонный гидроаккумулятор получил своё название благодаря
форме")

(setq p "разделителя, отделяющего газ от жидкости: на вид он
напоминает")

(setq z "резиновый баллон или вытянутую грушу, находящуюся в такой же
по форме металлической ёмкости.")



14. Определим поток вывода

(setq our-output-stream (open "new_name_file.spl" :direction :output))

(!!!замечание, этот файл создает сама программа, его не нужно
создавать в
директории (папке) заранее!!! надо только задать имя файла, такое,
какого еще нет, чтобы создался новый файл)

(princ s our-output-stream)
(terpri our-output-stream)
(princ p our-output-stream)
(terpri our-output-stream)
(princ z our-output-stream)
(terpri our-output-stream)


15. Тепрь файл закрывается

(close our-output-stream)

16. Теперь читаем печатные символы ( CHAR) из файла

Определим

(setq our-input-stream (open "name_file.spl" :direction :input))

(!!!примечание, этот файл нужно создать заранее в папке, т.е. этот
файл будет принимающим инфу из предыдущего файла (который output))

Для чтения символа используем

(read-char our-input-stream)

Закрытие входного потока

(close our-input-stream)


17. Тестирование этого алгоритма
..................................

18. Итог тестирования:

выдал ошибку:
end of file on #<SB-SYS:FD-STREAM for "file
/home/helaveesa/repo/testslisp/05.12.12./next..." {CBB1621}>
   [Condition of type END-OF-FILE]

после запроса:
(read-char our-input-stream)


Во избежании ошибок соберем алгоритм вместе:


(setq s "Баллонный гидроаккумулятор получил своё название благодаря
форме")
(setq p "разделителя, отделяющего газ от жидкости: на вид он
напоминает")
(setq z "резиновый баллон или вытянутую грушу, находящуюся в такой же
по форме металлической ёмкости")

(setq our-output-stream (open
"home/helaveesa/repo/testslisp/05.12.12./text.spl" :direction
:output))

      (princ s our-output-stream)
      (terpri our-output-stream)
      (princ p our-output-stream)
      (terpri our-output-stream)
      (princ z our-output-stream)
      (terpri our-output-stream)

(close our-output-stream)

(setq our-input-stream (open
"home/helaveesa/repo/testslisp/05.12.12./text.spl" :direction :input))

(read-char our-input-stream)

(close our-input-stream)

вроде бы как-то так...



итог:

выдал ошибку на строчке:
(setq our-output-stream (open
"home/helaveesa/repo/testslisp/05.12.12./fout5.spl" :direction
:output))

ошибка:
The path
  #P"/home/helaveesa/repo/testslisp/05.12.12./home/hela..."
does not exist.
   [Condition of type SB-INT:SIMPLE-FILE-ERROR]

вопрос, почему???
пишет, что не существует файла по тому пути, который я указываю.




19.Попробую другим способом:

\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\
