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


