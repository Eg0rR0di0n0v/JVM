# JVM

# Задача "Понимание JVM"

## Описание

Просмотрите код ниже и опишите (текстово или с картинками) каждую строку с точки зрения происходящего в JVM

Не забудьте упомянуть про:

- ClassLoader'ы,
- области памяти (стэк (и его фреймы), heap)
- сборщик мусора

## Код для исследования

```java
public class JvmComprehension {
    public static void main(String[] args) {
        int i = 1;                      // 1 во фрейме main создается переменная i типа int со значением 1
        Object o = new Object();        // 2 в куче создается объект типа Object на которую ссылается переменная Object о созданная во фрейме main
        Integer ii = 2;                 // 3 в куче создается объект типа Integer со значением 2, во фрейме main создается переменная ii типа Integer ссылающаяся на созданный объект
        printAll(o, i, ii);             // 4  в стеке создается фрейм printAll с переменными о, i, ii
        System.out.println("finished"); // 7 в стеке создается фрейм println принимающий ссылку типа String на объект из кучи со значением "finished"
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5 В куче создается объект типа Integer со значением 700 на которую ссылается переменная uselessVar типа Integer созданная во фрейме printAll 
        System.out.println(o.toString() + i + ii);  // 6 создается фрейм println с переменными o, i, ii каждый из которых, в свою очередь, создает свой фрейм toString. После завершения методов эти фреймы будут удалены. Результирующая строка будет храниться в куче, на которую будет ссылаться переменная типа String во фрейме println. После завершения метода println фрейм println будет удален. При следующем запуске сборщика мусора объект хранящий результат сложения строк будет удален. После выполнение метода printAll() фреймы с переменными удаляются.
    }
}
```

