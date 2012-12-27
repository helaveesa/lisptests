__________

Введение
__________

Функция, которая принимает число n и возвращает функцию,
которая добавляет n к своему аргументу:
(лексические замыкания)

(defun addn (n)
  #’(lambda (x)
      (+ x n)))

__________

Форма
__________

Вычисление:

специальный оператор quote

> (quote (+ 3 5))
(+ 3 5)

quote берет один аргумент и возвращает его текстовую запись

аналогично, сокращение quote

> ’(+ 3 5)
(+ 3 5)


Данные:

integer - целое число 256
строка - последовательность символов в кавычках
"изучать Лисп это как мотокросс"

символы - слова, преобразуются к верхнему регистру

> ’Artichoke
ARTICHOKE


списки - последовательность из нуля и более элементов,
заключенных в скобки (любой тип, другой список)

чтобы Лисп не счел список вызовом функции
его нужно процитировать

> ’(my 3 "Sons")
(MY 3 "Sons")
> ’(the list (a b c) has 3 elements)
(THE LIST (A B C) HAS 3 ELEMENTS)


функция list
пример,
внутри вызова функции list вычисляется
значение функции +

> (list ’my (+ 2 1) "Sons")
(MY 3 "Sons")


цитирование есть в коде,
тогда нет вычисления, возвращается сама текстовая запись
цитирования нет - производится вычисление, и на входе
дается результат вычисления

> (list ’(+ 2 1) (+ 2 1))
((+ 2 1) 3)

пустой список

> ()
NIL
> nil
NIL




Операции со списками:

построение списков - cons

> (cons ’a ’(b c d))
(A B C D)

> (cons ’a (cons ’b nil))
(A B)

более удобно в данном случае использовать list
> (list ’a ’b)
(A B)


функции для получения элементов списка

car

> (car ’(a b c))
A

cdr

> (cdr ’(a b c))
(B C)


комбинирование car и cdr

> (car (cdr (cdr ’(a b c d))))
C

аналогично, но с помощью функции third

> (third ’(a b c d))
C


Истинность:

истинность - символ t

функция listp возвращает истину, если ее аргумент - список

> (listp ’(a b c))
T

ложь - nil

функция listp вернет ложь, если ее аргумент - НЕ список

> (listp 27)
NIL


условный оператор if
три аргумента:
test
then
else

> (if (listp ’(a b c))
(+ 1 2)
(+ 5 6))
3
> (if (listp 27)
(+ 1 2)
(+ 5 6))
11


истина - символ t
но и все остальное, если это НЕ nil - считается за истину

> (if 27 1 2)
1
истина


логические операторы and и or

> (and t (+ 1 2))
3


Функции:

новые функции можно определить с помощью оператора defun

> (defun our-third (x)
(car (cdr (cdr x))))
OUR-THIRD

далее идет вызов функции, в нашем случае имя функции our-third,

> (our-third ’(a b c d))
C


выражение проверяет, превосходит ли сумма
чисел 1 и 4 чсило 3

> (> (+ 1 4) 3)
T

заменим конкретные числа, переменными
получим функцию, которая делает тоже самое,
что и предыдущее выражение, но для многих чисел

> (defun sum-greater (x y z)
(> (+ x y) z))
SUM-GREATER
> (sum-greater 1 4 3)
T



Рекурсия:

функция вызывающая саму себя и другие функции

функция member проверяет есть ли в списке
какой-либо объект

упрощенная реализация данной функции

(defun our-member (obj lst)
  (if (null lst)
       nil
    (if (eql (car lst) obj)
         lst
         (our-member obj (cdr lst)))))

предикат eql проверяет два аргумента на идентичность
проверяем есть ли obj в списке lst

вызовы:

> (our-member ’b ’(a b c))
(B C)
> (our-member ’z ’(a b c))
NIL


Ввод и вывод:

функция вывода  - format

> (format t "~A plus ~A equals ~A.~%" 2 3 (+ 2 3))
2 plus 3 equals 5.
NIL


функция чтения - read

пример: функция, которая предлагает ввести
любое значение и затем возвращает его

(defun askem (string)
  (format t "~A" string)
  (read))

вызов:

> (askem "How old are you? ")
How old are you? 29
29


Переменные:

оператор let
позволяет ввести новые переменные (локальные)

> (let ((x 1) (y 2))
(+ x y))
3


(defun ask-number ()
  (format t "Please enter a number. ")
  (let ((val (read)))
    (if (numberp val)
        val
        (ask-number))))


вызов:

> (ask-number)
Please enter a number. a
Please enter a number. (no hum)
Please enter a number. 52
52


создание глобальной переменной

> (defparameter *glob* 99)
*GLOB*

задание констант

(defconstant limit (+ *glob* 1))


узнать, чему соответствует имя глобальной переменной или константе
предикат boundp

> (boundp ’*glob*)
T



Присваивание:

оператор setf (для любых типов)

> (setf *glob* 98)
98

> (let ((n 10))
(setf n 2)
n)
2

> (setf x (list ’a ’b ’c))
(A B C)

> (setf (car x) ’n)
N
> x
(N B C)


(setf a b
      c d
      e f)
эквивалентно
(setf a b)
(setf c d)
(setf e f)

создание глобальных переменных
оператор defparameter



Функциональное программирование:

функция remove принимает список и объект
и возвращает новый список, состоящий из тез же элементов
что  предыдущий за исключением этого объекта

> (setf lst ’(c a r a t))
(C A R A T)
> (remove ’a lst)
(C R T)
исходный список не тронут
> lst
(C A R A T)

чтобы действительно удалить а из списка x
(setf x (remove ’a x))



Итерация:

функция печатает квадраты целых чисел от start до end

(defun show-squares (start end)
  (do ((i start (+ i 1)))
      ((> i end) ’done)
     (format t "~A ~A~%" i (* i i))))

вызов

> (show-squares 2 5)
2 4
3 9
4 16
5 25
DONE

макрос do - основной итерационный оператор в CL

функция, которая определяет длину списка

(defun our-length (lst)
  (let ((len 0))
    (dolist (obj lst)
      (setf len (+ len 1)))
len))

рекурсивная версия этой функции

(defun our-length (lst)
  (if (null lst)
      0
      (+ (our-length (cdr lst)) 1)))



Функции как объекты:

дать имя функции с помощью оператора function

> (function +)
#<Compiled-Function + 17BA4E>
эквивалентно
> #’+
#<Compiled-Function + 17BA4E>

функция может служить аргументом
это функция apply

> (apply #’+ ’(1 2 3))
6
> (+ 1 2 3)
6

> (apply #’+ 1 2 ’(3 4 5))
15


Функция funcall делает тоже самое, что apply,
но не требует, чтобы аргументы были упакованы в список

> (funcall #’+ 1 2 3)
6

Создание функции и определение ее с помощью макроса defun

Лямбда-выражение, представляющее функцию,
которая складывает два числа и возвращает их сумму

(lambda (x y)
(+ x y))

вызов

> ((lambda (x) (+ x 100)) 1)
101

добавляя к этому выражению function т.е. #'
плучим функцию

> (funcall #’(lambda (x) (+ x 100))
1)
101




Типы:

функция typep определяет, принадлежит ли ее первый аргумент к типу,
который задается вторым аргументом

> (typep 27 ’integer)
T

типы:
fixnum, integer, rational, real, number, atom и t



3 глава

Списки

ячейки:

ячейка cons (пара указателей на car и cdr)

использование cons:

> (setf x (cons ’a nil))
(A)

вызов

> (car x)
A
> (cdr x)
NIL



список из нескольких элементов, получим цепочку ячеек

> (setf y (list ’a ’b ’c))
(A B C)

вызов cdr
> (cdr y)
(B C)


элементами списка могут быть другие списки

> (setf z (list ’a (list ’b ’c) ’d))
(A (B C) D)

вызов
> (car (cdr z))
(B C)



проверка, является ли объект cons-ячейкой - функция consp
определим listp так

(defun out-listp (x)
(or (null x) (consp x)))

определим предикат atom

(defun our-atom (x) (not (consp x)))




Равенство

> (eql (cons ’a nil) (cons ’a nil))
NIL

> (setf x (cons ’a nil))
(A)

> (eql x x)
T


для проверки идентичности списков (и др. объектов)
используют предикат equal

> (equal x (cons ’a nil))
T
два одинаково выглядящих объекта равны,
с точки зрения equal


определим функцию equal

(defun our-equal (x y)
  (or (eql x y)
      (and (consp x)
           (consp y)
           (our-equal (car x) (car y))
           (our-equal (cdr x) (cdr y)))))


Две переменные указывают на один и тот же список

> (setf x ’(a b c))
(A B C)

> (setf y x)
(A B C)


эти две переменные будут одинаковы с точки жрения equal

> (eql x y)
T



Построение списков

функция copy-list принимает список и возвращает его копию

> (setf x ’(a b c)
y (copy-list x))
(A B C)

определи функцию copy-list

(defun our-copy-list (lst)
  (if (atom lst)
      lst
      (cons (car lst) (our-copy-list (cdr lst)))))


функция append еще одна по работе со списками
она склеивает между собой произвольн кол-во списков

> (append ’(a b) ’(c d) ’(e))
(A B C D E)

копирует все аргументы, за исключением последнего



ПРИМЕР
СЖАТИЕ

пример простого механизма сжатия списков

функция compress принимает список из атомов и возвращает его
сжатое представление

> (compress ’(1 1 1 0 1 0 0 0 0 1))
((3 1) 0 1 (4 0) 1)


кодирование повторов: сжатие

(defun compress (x)
  (if (consp x)
      (compr (car x) 1 (cdr x))
      x))


(defun compr (elt n lst)
  (if (null lst)
      (list (n-elts elt n))
      (let ((next (car lst)))
        (if (eql next elt)
            (compr elt (+ n 1) (cdr lst))
            (cons (n-elts elt n)
                  (compr next 1 (cdr lst)))))))


(defun n-elts (elt n)
  (if (> n 1)
      (list n elt)
      elt))



реконструирование сжатого списка
функция uncompress

> (uncompress ’((3 1) 0 1 (4 0) 1))
(1 1 1 0 1 0 0 0 0 1)



list-of функция, которая выполняется рекурсвино, копируя атомы и
раскрывая списки

> (list-of 3 ’ho)
(HO HO HO)
это сделает лучше функция make-list


кодирование повторов: декодирование

(defun uncompress (lst)
  (if (null lst)
      nil
      (let ((elt (car lst))
            (rest (uncompress (cdr lst))))
        (if (consp elt)
            (append (apply #’list-of elt)
                    rest)
            (cons elt rest)))))


(defun list-of (n elt)
  (if (zerop n)
      nil
      (cons elt (list-of (- n 1) elt))))



загрузка программ или файлов

(load "compress.lisp")




Доступ

вызов функции nth

> (nth 0 ’(a b c))
A

для получения n-ого хвоста списка
нужна функция nthcdr

вызов функции nthcdr

> (nthcdr 2 ’(a b c))
(C)

функции nthcdr и nth ведут свой отсчет от нуля

определим nthcdr

(defun our-nthcdr (n lst)
  (if (zerop n)
      lst
      (our-nthcdr (- n 1) (cdr lst))))


функция zerop проверяет, равен ли нулю ее аргумент

функция last возвращает последную cons-ячейку списка
> (last ’(a b c))
(C)




Отображающие функции

функция mapcar - вызывает заданную функцию поэлементно
для одного или нескольких списков и возвращает список результатов

> (mapcar #’(lambda (x) (+ x 10))
’(1 2 3))
(11 12 13)
> (mapcar #’list
’(a b c)
’(1 2 3 4))
((A 1) (B 2) (C 3))


похожим образом действует maplist
применяет функцию последовательно к cdr списка
начиная со всего списка целиком

> (maplist #’(lambda (x) x)
’(a b c))
((A B C) (B C) (C))



Деревья

функции для работы с деревьями

функция copy-tree - принимает дерево и возвращает его копию

определим такую функцию:

(defun our-copy-tree (tr)
  (if (atom tr)
      tr
      (cons (our-copy-tree (car tr))
      (our-copy-tree (cdr tr)))))

copy-tree копирует еще и car


список:
(and (integerp x) (zerop (mod x 2)))

хотим заменить x на y

функция substitute заменяет элементы последовательности

> (substitute ’y ’x ’(and (integerp x) (zerop (mod x 2))))
(AND (INTEGERP X) (ZEROP (MOD X 2)))


функция subst работает с деревьями, то что нам и надо

> (subst ’y ’x ’(and (integerp x) (zerop (mod x 2))))
(AND (INTEGERP Y) (ZEROP (MOD Y 2)))


Определим функцию subst

(defun our-subst (new old tree)
  (if (eql tree old)
      new
       (if (atom tree)
           tree
           (cons (our-subst new old (car tree))
           (our-subst new old (cdr tree))))))





Рекурсия


рекурсивная функция для определения длины списка

(defun len (lst)
  (if (null lst)
      0
      (+ (len (cdr lst)) 1)))



Множества

чтобы проверить, принадлежит ли элемент множеству,
задаваемому списком, используем
функцию member

> (member ’b ’(a b c))
(B C)

аргументы по ключу
сравнение

> (member ’(a) ’((a) (z)) :test #’equal)
((A) (Z))

> (member ’a ’((a b) (c d)) :key #’car)
((A B) (C D))

аргументы по ключу в произвольном порядке

> (member 2 ’((1) (2)) :key #’car :test #’equal)
((2))
> (member 2 ’((1) (2)) :test #’equal :key #’car)
((2))


member-if - позволяет найти элемент, удовлетворяющий
произвольному предикату, например oddp

oddp - вернет истину, когда аргумент нечетен

> (member-if #’oddp ’(2 3 4))
(3 4)


определение функции member-if

(defun our-member-if (fn lst)
  (and (consp lst)
       (if (funcall fn (car lst)
           lst
           (our-member-if fn (cdr lst)))))



функция adjoin - условный cons
она присоединяет заданный элемент к списку, но
только если его еще нет в списке

> (adjoin ’b ’(a b c))
(A B C)
> (adjoin ’z ’(a b c))
(Z A B C)



функции union, intersection, set-difference

объединение, пересечение, дополнение

> (union ’(a b c) ’(c b s))
(A C B S)
> (intersection ’(a b c) ’(b b c))
(B C)
> (set-difference ’(a b c d e) ’(b e))
(A C D)



Последовательности

length - определяет длину последовательности

> (length ’(a b c))
3


subseq - скопирует часть последовательности

> (subseq ’(a b c d) 1 2)
(B)
> (subseq ’(a b c d) 1)
(B C D)


функция reverse - вернет последовательность в обратном порядке
с ее помощью можно искать палиндромы
> (reverse ’(a b c))
(C B A)

палиндромы

(a b b a)
обратный порядок этого списка
(a b b a)
аналогичен


Используя
length, subseq и reverse

определим функцию mirror?

(defun mirror? (s)
  (let ((len (length s)))
    (and (evenp len)
         (let ((mid (/ len 2)))
           (equal (subseq s 0 mid)
                  (reverse (subseq s mid)))))))

вызов

> (mirror? ’(a b b a))
T


функция mirror? - определяет, является ли список таким палиндромом

sort - для сортировки последовательностей

> (sort ’(0 2 1 3 8) #’>)
(8 3 2 1 0)


Используя sort и nth заишем функцию, которая принимает целое число n
и возвращает n-ый элемент в порядке убывания

(defun nthmost (n lst)
  (nth (- n 1)
       (sort (copy-list lst) #’>)))

вызов

> (nthmost 2 ’(0 2 1 3 8))
3



функции every и some применяют предикат к одной
или нескольким последовательностям

> (every #’oddp ’(1 3 5))
T
> (some #’evenp ’(1 2 3))
T
> (every #’> ’(1 3 5) ’(0 2 4))
T




Стопка (стек)






























