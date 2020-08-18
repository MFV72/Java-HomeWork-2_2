# Отчёт о тестировании Java-кода для проверки валидности номеров карт

## Краткое описание

18.08.2020 - было проведено тестирование Java-кода для проверки валидности номеров пластиковых карт.

На тестирование затрачено: <1 час>

## В результате тестирования дефектов не выявлено.

## Описание процесса тестирования

Для тестирования кода было установлено приложение IntelliJ IDEA согласно [Инструкции по установке](https://github.com/netology-code/javaqa-homeworks/blob/master/intro/idea.md)

Далее в IntelliJ IDEA был создан новый проект и в этот проект был вставлен тестируемый Java-код.
Для проверки корректности работы кода использовались тестовые номера кредитных карт с [сайта](https://www.freeformatter.com/credit-card-number-generator-validator.html).
Номера карт поочередно вводились в 4 строку кода:
```
    "String number = "5351719427810741";
```
 Приложение принимает 16-значное цифровое значение без пробелов и тире и выдает результат проверки в консоли  **"Result is OK"**. При попытке ввести символы, пробелы приложение выдает сообщение : **Result is FAIL**

В качестве тестовых данных использовались:
* [Инструкция по установке IntelliJ IDEA](https://github.com/netology-code/javaqa-homeworks/blob/master/intro/idea.md)
* Java-код
```
public class Main {
  public static void main(String[] args) {
    // TODO: подставлять номер карты нужно сюда между двойными кавычками, без пробелов
    String number = "5351719427810741";
    System.out.println(String.format("Result is %s", isValidCardNumber(number) ? "OK" : "FAIL"));
  }

  public static boolean isValidCardNumber(String number) {
    if (number == null) {
      return false;
    }

    if (number.length() != 16) {
      return false;
    }

    long result = 0;
    for (int i = 0; i < number.length(); i++) {
      int digit;
      try {
        digit = Integer.parseInt(number.charAt(i) + "");
      } catch (NumberFormatException e) {
        return false;
      }

      if (i % 2 == 0) {
        digit *= 2;
        if (digit > 9) {
          digit -= 9;
        }
      }
      result += digit;
    }

    return (result != 0) && (result % 10 == 0);
  }
}
```


Тестирование производилось в следующем окружении:
* <Windows 7 Максимальная 64bit>
* <Java 11 (OpenJDK11), version "11.0.8" 2020-07-14>
* <IntelliJ IDEA 2020.2 (Community Edition) Build #IC-202.6397.94, built on July 27, 2020>


