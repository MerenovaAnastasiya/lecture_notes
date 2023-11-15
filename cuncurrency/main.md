Программа, которая состоит полностью из потокобезопасных классов может не быть потокобезопсаной.
Понятие потокобезопасного класса применяется только в том случае, если класс инкапсулирует свое состояние.

Ни один набор операций, выполняемый последовательно или конкурентно на экземплярах потокобезопасного класса,
не может привести класс в недопустимое состояние.

**Атомарность**

Атомарная операция — операция, которая либо выполняется целиком, либо не выполняется вовсе(не может быть частично исполнена)
Не атомарная операция в java инкрементирвание i++, тк для того чтобы ее выполнить, необходимо сначала прочитать старое значение, а потом увеличить 
его на единицу. Между чтением и увеличением значения переменная может быть изменена другим потоком.


**Состояние гонки(race condition)**

Ошибка в проектировании многопоточного приложения может привести систему в состояние, при котором последовательность выполнения определенных частей 
кода может привести к различному исходу.


synchronized - создает блок кода, который выполняется в режиме взаимного исключения

happens-before правила:
1. внутри одного потока операции h-b согласно program order.
2. освобождение монитора h-b его заполучению
3. запись в volatile переменную h-b ее чтению
4. Объект, у которого есть final поля можно использовать только после установки значений в эти поля


