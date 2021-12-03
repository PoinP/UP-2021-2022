# Семинар седмица 9

## Днес ще научим:
 - Указатели

## Допълнителни ресурси: https://personal.ntu.edu.sg/ehchua/programming/cpp/cp4_pointerreference.html

### Указатели
#### За какво са и за какво ни трябват?
Указателят е променлива, чиято стойност е адресът на друга променлива. Това е едно от най - ценните предимства на езика C++. Чрез него можем директно да променяме стойността която се намира в дадена клетка от паметта. Масивите всъщност също са указатели. Най - важната същност на указателите се крие в това, че съчетавайки ги с функциите създаваме инструменти, чрез които да оперираме над дадените променливи.

#### Синтаксис и семантика:
```c++
<object_type> *<object_name_pointer> = &<object_name_transmitter>;
```
Пример:

```c++
int a = 50;
int *ptr = &a;
```
По този начин казваме следното: създали сме променлива от тип int и сме я инициализирали със стойност 50, след това създаваме променлива от тип указател към int, на която присвояваме адреса на а. Вземането на адрес на дадена променлива се прави чрез &.

Най - важното е да се разбере, че указателите пазят адреса към паметта на това, с което искаме да работим.

Когато сме инициализирали стойност, както в случая по - горе, можем да достъпим стойността на дадения адрес като пишем - *ptr. По този начин казваме "Дай ми това, което се намира на адреса, към който сочи ptr".

![alt tag](https://github.com/GeorgiMinkov/FMI_IS_UP_1_2016/blob/master/week12/MemoryPointer.png)

Пример:
```c++
int a = 50;
int *ptr = &a;

std::cout << *ptr << std::endl; // 50
std::cout << ++*ptr << std::endl; // 51
std::cout << a << std::endl; // 51

```

#### Масиви и указатели
Споменахме, че масивът е указател. Как можем да проверим?
```c++
double arr[5] = { 4, 5, 6, 7.6, 9 };
std::cout << arr << std::endl; // Ще се изпише на конзолата: 0x7ffcd4326470
```
Това е така, защото когато създаваме масив, ние всъщност създаваме указател към първия елемент на масива. Когато пишем arr[index] (еквивалентно е *(arr + index)), казваме дай ми елемента, който се намира на позицията: на първия елемент + отместване

#### Псевдоними и указатели във функции
Когато използваме функции и подаваме аргумент (подаване по стойност), ние всъщност създаваме нова променлива някъде в паметта (виж графиката) и всички промени, които осъществим, се правят върху новата променлива, а не върху променливата, която сме подали.

За да правим промени върху оригиналните променливи, които сме подали, се използват указателите и псевдонимите.

![alt tag](https://github.com/GeorgiMinkov/FMI_IS_UP_1_2016/blob/master/week12/1Diagram.png)

Пример: Искаме да намерим сумата на две числа като използваме трета променлива, в която да се пази резултата. (решавам да не връщам сумата като резултат, а да пазя резултата в предварително създадена променлива)

```c++
// Example program
#include <iostream>

// without reference or pointer => will lose value of sum
void sumWithoutRefOrPointer(int numL, int numR, int sum)
{
    sum = numL + numR;
}

// with reference
void sumIt(int numL, int numR, int &sum)
{
    sum = numL + numR;
}

// with pointer
void sumIt(int numL, int numR, int *sum)
{
    *sum = numL + numR;
}

int main()
{
  int numL = 4, numR = 6, sum = 0;

  sumWithoutRefOrPointer(numL, numR, sum);
  std::cout << "1) " << sum << std::endl; // 0

  sumIt(numL, numR, sum);
  std::cout << "2) " << sum << std::endl; // 10

  sumIt(numL + 1, numR, &sum); // we must put adress of sum
  std::cout << "3) " << sum << std::endl; // 11

  return 0;

}
```

Когато сме подали по стойност (първата функция), правим копие и след края на изпълнение се трие това копие като стойността на sum (това е main) не е променена.
Когато подаваме по референция, ние работим директно в паметта и от там идва и промяната на стойността на променливата sum.
При използването на указател наблюдаваме същото: Вземи адреса на променливата и след това със * казваме влез вътре и промени стойността.