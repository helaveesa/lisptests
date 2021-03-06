ANSI Common Lisp
_______________________________

dec, 2012

___________

p.19
функция складывающая все числа, меньшие n
        (defun sum (n)
          (let ((s 0))
             (dotimes (i n s)
                 (incf s i))))

, где

defun sunm - объявление функции sum
let - ?
обратимся к источнику:

http://lisp2d.net/rus/teach/h.php

let - Работа с контекстом:предложение let.
LET создаёт локальную связь
Вычисление функции создаёт на время вычисления новые связи для
формальных параметров функции. Новые связи внутри формы можно создать
и с помощью предложения let. Эта структура выглядит так:

(nil let ((m1           {value1})|m1       (m2      {value2})|m2
…)
  form1
  form2 …)

  Предложение let вычисляется так, что сначала динамические переменные
m1, m2, … из первого "аргумента" формы связываются (одновременно) с
соответствующими значениями знач1, знач2, … Затем пошагово вычисляются
значения форм форма1, форма2, … В качестве значения всей формы
возвращается значение последней формы. Как и у функций, после
окончания вычисления связи динамических переменных m1, m2, …
ликвидируются и любые изменения их значений (setq) не будут видны
извне. Например:

>(nil setq  a 2)
nil
>(nil let ((a 0))
  (nil  setq  a 1))
nil
>a
2

  Форма let является на самом деле синтаксическим видоизменением
лямбда-вызова, в которой формальные и фактические параметры помещены
совместно в начале формы:

(nil let ((m1 {a1}) (m2 {a2}) … (mn {an}))
  form1 form2 …)
≡
(nil (lambda
  (m1 m2 … mn)  ; формальный параметр
  form1 form2 …)  ; тело функции
  (nil progn {a1}) (nil progn {a2}) … (nil progn {an}))  ; фактический
параметр

Значения переменным формы let присваиваются одновременно. Это
означает, что значения всех переменных mi вычисляются до того, как
осуществляется связывание с формальными параметрами. Новые связи этих
переменных ещё не действуют в момент вычисления начальных значений
переменных, которые перечислены в форме позднее. Например:

>(nil let ((x 2)  (y  (3  * x)))
  (nil  list  x y)) ; при вычислении y у x нет связи
Error:eval: Symbol x have no value


dotimes - ???

ищем в источнике:
http://it-library.org/articles/?c=8&&a=164

dotimes - DOTIMES можно использовать вместо DO, если надо повторить
вычисления задан-
ное число раз.
Общая форма:
(DOTIMES (var num форма-return) (форма-тело))
var - переменная цикла,
num - форма определяющая число циклов,
форма-return - результат, который должен быть возвращен.
Прежде всего вычисляется num-форма, в результате получается целое
число-count. Затем var меняется от 0 до count (исключая count) и
соответственно каждый раз вычисляется форма-тело. Последним
вычисляется форма-return. Если форма-return отсутствует, возвращается
nil.
Пример:
> (dotimes (x 3)
(print x))
0 - автоматически
1
2
t
> (let ((x nil))
(dotimes (n 5 x)
(setq x (cons n x))))
(4 3 2 1 0)


пример 2:

CL-USER> (dotimes (x 9)                                                 (print x))
                                                                  |0
                                                                  |1
                                                                  |2
                                                                  |3
                                                                  |4
                                                                  |5
                                                                  |6
                                                                  |7
                                                                  |8
                                                                  |NIL


incf - ???

источник:

http://www.cardarmy.ru/proekt/lisp/art3.htm


К числу дополнительных средств, обеспечивающих работу с обобщенными
переменными относятся макросы
getf, remf, incf, decf, push, pop assert, ctypecase и ccase.

При этом все эти макросы должны гарантировать соблюдение ими правил
``очевидной'' семантики: субформы ссылок на обобщенные переменные
оцениваются ровно столько раз, сколько они встречаются в исходных
текстах программы, и оценка производится точно в том же порядке, в
котором они появляются в программе.
В некоторых макросах, использующих ссылки на обобщенные переменные,
таких как shiftf, incf, push, и setf обобщенная переменная
используется как для чтения, так и для записи. Поэтому сохранение
принятого в исходной программе порядка оценки значения и количества
этих оценок оказывается исключительно важным для обеспечения
правильной работы разрабатываемого программного кода.


Расширение этих макросов должно содержать код, который следует
описанным выше правилам. Это достигается путем применения вполне
очевидного решения --- введения временных переменных, связанных с
субформами, адресующими используемые обобщенные переменные. По мере
расширения макроса, когда в дело вступает (если он используется)
оптимизатор, эти временные переменные могут быть исключены, если
оптимизатору удастся доказать, что их отсутствие не оказывает влияние
на генерируемый программный код. Например, нет никакого смысла
помещать во временную переменную значение константы. Точно так же,
переменная или любая форма, которая не имеет никаких побочных
эффектов, так же не нуждается в помещении во временную переменную,
если можно доказать, что ее значение не изменяется при изменении
значений обобщенной переменной.

В большинстве версий Common Lisp реализованы встроенные средства,
осуществляющие такого рода упрощения генерируемого кода.  поскольку
эти средства самостоятельно следят за соблюдением описанных выше
семантических правил, пользователь может не беспокоиться о соблюдении
этих правил, что заметно облегчает жизнь при разработке сложных
программ.

Примером такой оптимизации может служить следующий фрагмент:


(incf (ldb byte-field variable))

*******************************************************************************************************


функция, которая принимает число n и возвращает функцию, которая
лобавляет n к своему аргументу

          (defun addn (n)
             #’(lambda (x)
               (+ x n)))


TESTING:

CL-USER> 1
1
CL-USER> (+ 2 3)
5
CL-USER> (+)
0
CL-USER> (third '(a b c d e f))
C
CL-USER> (third '(a vfvf b vfgf c vfvf d bgbv e jbgvf f))
B
CL-USER> (third '(1 2 3 4 5 6 7))
3
CL-USER> (third '(a b nil d e f))
NIL
CL-USER> (third '(a b () d e f))
NIL
CL-USER> (third '(a b '(c d) e f))
'(C D)
CL-USER> (third '(a b (+ 5 4) d e f))
(+ 5 4)




