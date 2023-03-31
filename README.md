# Понимание JVM

Рассмотрим данный по заданию код пошагово:
    
    public class JvmComprehension {

        public static void main(String[] args) {
            int i = 1;                      
            Object o = new Object();        
            Integer ii = 2;                 
            printAll(o, i, ii);             
            System.out.println("finished"); 
        }

        private static void printAll(Object o, int i, Integer ii) {
            Integer uselessVar = 700;                  
            System.out.println(o.toString() + i + ii);  
        }
    }

## Пошаговый разбор кода:

    public class JvmComprehension {

JVM просит загрузить класс JvmComprehension через систему загрузчиков классов - ClassLoader.
В итоге операции класс JvmComprehension помещается в Metaspace.

        public static void main(String[] args) {

В стеке создаётся фрейм метода main. JVM просит загрузить класс String. Класс String помещается в Metaspace. Происходит выделение памяти в куче, создаётся объект типа String[], заполняя выделенную память, после чего в стек фрейма main кладётся переменная args типа String[] и ей присваивается ссылка на созданный в куче объект.

            int i = 1;

В стек фрейма main кладётся переменная i типа int и ей присваивается значение 1.

            Object o = new Object();

Происходит выделение памяти в куче, создаётся объект типа Object, заполняя выделенную память, после чего в стек фрейма main кладётся переменная o типа Object и ей присваивается ссылка на созданный в куче объект.

            Integer ii = 2;

JVM просит загрузить класс Integer. В итоге операции класс Integer помещается в Metaspace. Происходит выделение памяти в куче, создаётся объект типа Integer, заполняя выделенную память, после чего в стек фрейма main кладётся переменная ii типа Integer и ей присваивается ссылка на созданный в куче объект, в поле value этого объекта записывается значение 2.

            printAll(o, i, ii);

В стеке создаётся фрейм метода printAll.

        private static void printAll(Object o, int i, Integer ii) {

Происходит выделение памяти в куче для создания объектов типа Object и Integer. В стек фрейма printAll кладутся переменные: o типа Object, i типа int, ii типа Integer, где им присваиваются значения аргументов или ссылок, переданных при вызове метода.

        Integer uselessVar = 700;

Происходит выделение памяти в куче, создаётся объект типа Integer, заполняя выделенную память, после чего в стек фрейма printAll кладётся переменная uselessVar типа Integer и ей присваивается ссылка на созданный в куче объект, а в поле value этого объекта записывается значение 700.

        System.out.println(o.toString() + i + ii);

В стеке создаётся фрейм метода println. В стек фрейма println кладётся переменная x типа String
В стеке создаётся фрейм метода toString.
Переменной x присваивается результат конкатенации.
После завершения метода printAll garbage collector может очистить память в куче, если программе понадобится больше ресурсов, т.к. объектам Object o и Integer ii будет не на что ссылаться из-за закрытия фрейма метода printAll.


            System.out.println("finished");

В стеке создаётся фрейм метода println. Происходит выделение памяти в куче, создаётся объект типа String. В стек фрейма println кладётся переменная x типа String, где ей присваивается значение.