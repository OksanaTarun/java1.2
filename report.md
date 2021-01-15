Отчёт о тестировании Credit Card Number Validator

Краткое описание:

15.01.2021 было проведено функциональное тестирование приложения Credit Card Number Validator.

На тестирование затрачено: 1 час

В результате тестирования выявлены следующие дефекты:

1. https://github.com/OksanaTarun/java1.2/issues/1

Описание процесса тестирования:

В процессе тестирования использовались следующие артефакты:

1. Руководство по установке IntelliJ IDEA - https://github.com/netology-code/javaqa-homeworks/blob/master/intro/idea.md
2. Код -

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

В качестве тестовых данных использовались данные сайта https://www.getcreditcardnumbers.com/ , карты для проверки: Mastercard - 5461662745397305, Visa - 4024007139893498, AmericanExpress - 342206890325707.

- валидные карты - ответ ОК
- невалидные карты - ответ FAIL

Тестирование производилось в следующем окружении:

macOS Mojave 10.14.6
openjdk version "11.0.9.1" 2020-11-04
