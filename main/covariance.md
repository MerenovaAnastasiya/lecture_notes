Ковариантность — перенос наследования исходных типов на производные от них типы
Ковариантность - случай когда более конкретный тип S может быть подставлен вместо более обобщенного типа Т

Контрвариантность — перенос наследования исходных типов на производные от них типы в обратном порядке
Контрвариантность - случай когда более общий тип Т может быть подставлен вместо более конкретного типа S

В Java массивы являются ковариантными, т.о. если метод принимает на вход массив Object, то ему на вход можно передать массив String.

###### Ковариантность типо-безопасна для операций чтения, а контравариантность для операций записи!!!!!

Таким образом, такой код будет безопасным:

    public class TestArray {
        public static void main(String[] args){
            String[] strArray = new String[] {"string1", "string2", "string3"};
            print(strArray);
        }

        public static void print(Object[] objectArray){
            for (Object v : objectArray)
            System.out.print(v + "\n");
        }
    }

Однако! Если попытаться изменить содержимое массива следующим образом:

    public static void print(Object[] objectArray){
        for (Object v : objectArray)
            System.out.print(v + "\n");
            objectArray[0] = 1;
    }

мы получим ошибку ArrayStoreException!!!

