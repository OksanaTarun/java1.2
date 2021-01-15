# Отчёт о тестировании Credit Card Number Validator

## Краткое описание

15.01.2021 было проведено функциональное тестирование приложения Credit Card Number Validator.

На тестирование затрачено: 2 часа

В результате тестирования выявлены следующие дефекты:
* <a href="https://github.com/OksanaTarun/java1.2/issues/1">Ответ FAIL при вводе данных карт American Express</a>
* <a href="https://github.com/OksanaTarun/java1.2/issues/2">Ответ FAIL при вводе данных карт Diners Club</a>

## Описание процесса тестирования

В процессе тестирования использовались следующие артефакты:
* <a href="https://github.com/netology-code/javaqa-homeworks/blob/master/intro/idea.md">Руководство по установке IntelliJ IDEA</a>
* код: 
  
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

В качестве тестовых данных использовались данные карт American Express, Diners Club, Discover, MasterCard, Visa с <a href="https://www.getcreditcardnumbers.com/">сайта</a>:
* валидные карты - ответ ОК
* невалидные карты - ответ FAIL

Тестирование производилось в следующем окружении:
* macOS Mojave 10.14.6
* openjdk version "11.0.9.1" 2020-11-04
