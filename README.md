## Отчет по лабораторной работе № 2

#### № группы: `ПМ-2502`

#### Выполнил: `Загидулина Ева Артуровна`

#### Вариант: `6`

### Cодержание:

- [Задание №1](#задание-№1)
- [Задание №2](#задание-№2)
- [Задание №3](#задание-№3)
- [Задание №4](#задание-№4)

# Лабораторная работа по программированию

## Задание 1: Исследование последовательности

### 1. Условие задачи
<div style="color: gray;">
Последовательность: 2, 2, 8, 24, 32, 720...
Найти закономерность и запрограммировать.
</div>

### 2. Как я поняла задачу
Анализирую последовательность: 2, 2, 8, 24, 32, 720...
Закономерность: 
- Четные позиции (0, 2, 4): 2 в степени (i+1) → 2¹=2, 2³=8, 2⁵=32
- Нечетные позиции (1, 3, 5): факториал (i+1) → 2!=2, 4!=24, 6!=720

### 3. Объяснение алгоритма
1. Для каждого i от 0 до n-1:
   - Если i четное: a[i] = 2ⁱ⁺¹
   - Если i нечетное: a[i] = (i+1)!

### 4. Код на Java
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.print("Введите n: ");
        int n = sc.nextInt();
        
        if (n > 100) {
            System.out.println("n слишком большое");
            return;
        }
        
        long[] a = new long[n];
        
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0) {
                // Четное: 2^(i+1)
                a[i] = (long)Math.pow(2, i+1);
            } else {
                // Нечетное: факториал (i+1)
                long fact = 1;
                for (int j = 1; j <= i+1; j++) {
                    fact *= j;
                }
                a[i] = fact;
            }
        }
        
        // Вывод
        for (int i = 0; i < n; i++) {
            System.out.print(a[i] + " ");
        }
    }
}
```

## Задание 2: Префиксы последовательности

### 1. Условие задачи
<div style="color: gray;">
Найти первый префикс, где разность max-min максимальна.
Вывести длину этого префикса.
</div>

### 2. Как я поняла задачу
Нужно для каждого префикса считать разность между максимальным и минимальным элементом, и найти первый префикс с максимальной такой разностью.

### 3. Объяснение алгоритма
1. Читаем n и массив
2. Бежим по элементам, обновляя min и max
3. Считаем разность для текущего префикса
4. Если разность больше максимальной, запоминаем длину

### 4. Код на Java
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] a = new int[n];
        
        for (int i = 0; i < n; i++) {
            a[i] = sc.nextInt();
        }
        
        int maxDiff = 0;
        int res = 0;
        int minVal = a[0];
        int maxVal = a[0];
        
        for (int i = 0; i < n; i++) {
            if (a[i] < minVal) minVal = a[i];
            if (a[i] > maxVal) maxVal = a[i];
            
            int diff = maxVal - minVal;
            if (diff > maxDiff) {
                maxDiff = diff;
                res = i + 1;
            }
        }
        
        System.out.println(res);
    }
}
```

## Задание 3: Бегун на стадионе

### 1. Условие задачи
<div style="color: gray;">
Бегун бежит по кругу длины L. 
Точки A, B, C нужно посетить.
Вывести номер круга и шага, когда все точки впервые посещены.
</div>

### 2. Как я поняла задачу
Двигаемся по кругу, после каждого шага проверяем, посетили ли точки A, B, C. Старт (0) не считается.

### 3. Объяснение алгоритма
1. Читаем L, A, B, C
2. Читаем шаги до -L*L
3. После каждого шага обновляем позицию
4. Проверяем посещение точек
5. Когда все три посещены - выводим ответ

### 4. Код на Java
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int L = sc.nextInt();
        int A = sc.nextInt();
        int B = sc.nextInt();
        int C = sc.nextInt();
        
        int pos = 0;
        int stepNum = 0;
        int circles = 0;
        boolean va = false, vb = false, vc = false;
        
        while (true) {
            int step = sc.nextInt();
            if (step == -L*L) break;
            
            stepNum++;
            pos = (pos + step) % L;
            if (pos < 0) pos += L;
            
            if (pos == 0 && stepNum > 0) circles++;
            
            if (pos == A) va = true;
            if (pos == B) vb = true;
            if (pos == C) vc = true;
            
            if (va && vb && vc) {
                System.out.println(circles + " " + stepNum);
                return;
            }
        }
        
        System.out.println("NO");
    }
}
```

## Задание 4: Элемент = числу различных

### 1. Условие задачи
<div style="color: gray;">
Найти элемент массива, равный количеству различных элементов.
</div>

### 2. Как я поняла задачу
Нужно посчитать, сколько разных чисел в массиве, и найти элемент с таким значением.

### 3. Объяснение алгоритма
1. Считаем различные элементы
2. Ищем элемент, равный этому количеству

### 4. Код на Java
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();
        int[] a = new int[n];
        
        for (int i = 0; i < n; i++) {
            a[i] = sc.nextInt();
        }
        
        // Считаем различные элементы
        int d = 0;
        for (int i = 0; i < n; i++) {
            boolean found = false;
            for (int j = 0; j < i; j++) {
                if (a[i] == a[j]) {
                    found = true;
                    break;
                }
            }
            if (!found) d++;
        }
        
        // Ищем элемент, равный d
        int res = 0;
        for (int i = 0; i < n; i++) {
            if (a[i] == d) {
                res = a[i];
                break;
            }
        }
        
        System.out.println(res);
    }
}
```
