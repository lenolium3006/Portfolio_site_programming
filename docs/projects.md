# Проекты



## Командный проект «Библиотека»

### **Описание проекта**

В рамках командной работы был разработан проект для предметной области **«Библиотека»**.

Цель проекта — создание набора классов и структуры базы данных для хранения информации о:

* книгах;
* пользователях;
* библиотеках;
* взаимодействии пользователей с книгами.


### **Что было реализовано**
* Создан Telegram-бот.
* Организована командная разработка проекта.
* Создан общий репозиторий.
* Реализованы основные сущности библиотеки.
* Настроена работа с командами Telegram.
* Подготовлена структура базы данных.
* Исследованы способы хранения графика работы библиотеки.
* Подготовлена документация проекта.
* Использован GitHub Flow для организации работы.

### **Основной функционал Telegram-бота**
Бот поддерживает следующие возможности:
* просмотр списка книг;
* поиск книг;
* вывод информации о библиотеке;
* отображение часов работы;
* добавление книг в избранное;
* взаимодействие пользователя с библиотечной системой.


### **Ссылка на репозиторий**

[https://github.com/schudnaya/telegram_library_bot](https://github.com/schudnaya/telegram_library_bot)


### **Результат работы**

В результате выполнения проекта был разработан Telegram-бот для библиотеки, реализована совместная командная разработка с использованием GitHub  и подготовлена документация по архитектуре проекта.








---
## Основные концепции ООП на Python

### **Описание проекта**

В рамках лабораторной работы была организована командная разработка проекта с использованием системы контроля версий GitHub/GitLab и методологии ветвления GitHub Flow.

Участники команды совместно создали репозиторий, распределили между собой темы и концепции объектно-ориентированного программирования, после чего оформили документацию в формате Markdown.

Каждый участник:

* был добавлен в общий репозиторий;
* работал в собственной ветке;
* оформлял описание выбранной концепции;
* создавал примеры кода на Python;
* оформлял Pull Request для объединения изменений.


### **Организация работы команды**

Работа была распределена между участниками команды следующим образом:

1. Один участник создавал репозиторий и настраивал структуру проекта.
2. Остальные участники получали доступ к репозиторию.
3. Для каждой концепции создавалась отдельная ветка.
4. После завершения работы создавались Pull Request.
5. Изменения проходили проверку и объединялись в основную ветку.

Такой подход позволил:

* избежать конфликтов кода;
* распределить нагрузку;
* контролировать изменения;
* упростить совместную разработку.

### **Наследование**

В рамках командного проекта мной была выбрана тема «Наследование» в объектно-ориентированном программировании.
Для данной концепции было подготовлено:
теоретическое описание;
ключевые особенности наследования;
примеры кода на Python;
описание особенностей реализации наследования в Python;
оформление документации в формате Markdown.

#### Введение
Наследование — это один из ключевых принципов объектно-ориентированного программирования (ООП). Оно позволяет создавать новые классы на основе уже существующих. При этом новый класс автоматически получает свойства и методы родительского класса, а также может добавлять собственные функции и изменять уже существующие.

Основные понятия наследования

Класс, от которого происходит наследование, называется родительским, базовым или суперклассом. Класс, который наследует свойства и методы, называется дочерним, производным или подклассом.

Главная идея наследования заключается в том, чтобы не создавать одинаковый код несколько раз. Программист может один раз описать общие свойства объектов, а затем использовать их в других классах.

#### Зачем нужно наследование

Основная цель наследования — повторное использование кода и упрощение разработки программ. Вместо того чтобы заново описывать одинаковые характеристики для разных объектов, программист создает общий базовый класс и использует его как основу для других классов.

Это делает код:

* более компактным;
* понятным;
* удобным для поддержки;
* легким для расширения.

Наследование особенно полезно при разработке крупных проектов, где существует большое количество похожих объектов.

#### Пример наследования

Например, можно создать базовый класс «Транспорт», в котором будут общие свойства: скорость, цвет, марка и метод движения. Далее от него можно унаследовать классы «Автомобиль», «Мотоцикл» и «Велосипед». Все они будут иметь общие характеристики транспорта, но при этом смогут содержать собственные особенности.

Пример на языке Python:

```python 
class Transport:
    def move(self):
        print("Транспорт движется")

class Car(Transport):
    def signal(self):
        print("Бип-бип!")

car = Car()

car.move()
car.signal()
```

В данном примере класс `Car` наследует метод `move()` от класса `Transport`. Благодаря этому нет необходимости повторно писать одинаковый код.

#### Переопределение методов

Одной из важных особенностей наследования является возможность переопределения методов. Это означает, что дочерний класс может изменить работу метода родительского класса под свои задачи.

Пример:

```python 
class Animal:
    def sound(self):
        print("Животное издает звук")

class Dog(Animal):
    def sound(self):
        print("Собака лает")
```

Здесь класс `Dog` переопределяет метод `sound()`, который был создан в классе `Animal`.

#### Преимущества наследования

Наследование имеет множество преимуществ:

* сокращение объема кода;
* повторное использование уже созданных классов;
* упрощение разработки больших проектов;
* улучшение структуры программы;
* удобство поддержки и обновления кода.

Благодаря наследованию программы становятся более гибкими и удобными для дальнейшего развития.

#### Недостатки наследования

Несмотря на преимущества, неправильное использование наследования может усложнить программу. Если создавать слишком длинные цепочки наследования, код становится трудным для понимания и сопровождения.

Поэтому программист должен грамотно продумывать структуру классов и использовать наследование только там, где это действительно необходимо.

#### Заключение

Наследование широко применяется при создании современных программ, веб-сайтов, мобильных приложений, игр и операционных систем. Практически все крупные программные проекты используют принципы объектно-ориентированного программирования.

Таким образом, наследование является важнейшим механизмом ООП, который позволяет создавать гибкие и удобные программы. Благодаря наследованию код становится более организованным, уменьшается количество повторений, а разработка программного обеспечения становится быстрее и эффективнее.


### Пример кода на Python

```python 
from abc import ABC, abstractmethod

class Employee(ABC):

    company_name = "TechCorp"

    def __init__(self, name, age, salary):
        self.name = name
        self.age = age
        self._salary = salary

    @abstractmethod
    def work(self):
        pass

    def show_info(self):
        print("\n==============================")
        print(f"Компания: {Employee.company_name}")
        print(f"Имя: {self.name}")
        print(f"Возраст: {self.age}")
        print(f"Зарплата: {self._salary} руб.")
        print("==============================")

    def get_salary(self):
        return self._salary

    def increase_salary(self, amount):
        if amount > 0:
            self._salary += amount
            print(f"\nЗарплата увеличена на {amount} руб.")
        else:
            print("\nОшибка: сумма должна быть положительной.")

class Developer(Employee):

    def __init__(self, name, age, salary, programming_language):
        super().__init__(name, age, salary)
        self.programming_language = programming_language

    def work(self):
        print(f"\n{self.name} пишет код на {self.programming_language}.")

    def fix_bug(self):
        print(f"{self.name} исправляет ошибки в программе.")

    def show_info(self):
        super().show_info()
        print(f"Должность: Разработчик")
        print(f"Язык программирования: {self.programming_language}")

class Designer(Employee):

    def __init__(self, name, age, salary, design_tool):
        super().__init__(name, age, salary)
        self.design_tool = design_tool

    def work(self):
        print(f"\n{self.name} создает дизайн в {self.design_tool}.")

    def create_mockup(self):
        print(f"{self.name} разрабатывает макет интерфейса.")

    def show_info(self):
        super().show_info()
        print(f"Должность: Дизайнер")
        print(f"Инструмент: {self.design_tool}")
      
class Manager(Employee):

    def __init__(self, name, age, salary, team_size):
        super().__init__(name, age, salary)
        self.team_size = team_size

    def work(self):
        print(f"\n{self.name} управляет командой.")

    def hold_meeting(self):
        print(f"{self.name} проводит собрание команды.")

    def show_info(self):
        super().show_info()
        print(f"Должность: Менеджер")
        print(f"Количество сотрудников в команде: {self.team_size}")

def company_report(employees):

    print("\n========== ОТЧЕТ КОМПАНИИ ==========")

    total_salary = 0

    for employee in employees:
        employee.show_info()
        employee.work()
        total_salary += employee.get_salary()

    print(f"Общий фонд зарплат: {total_salary} руб.")
  


dev1 = Developer(
    name="Алексей",
    age=25,
    salary=120000,
    programming_language="Python"
)

designer1 = Designer(
    name="Мария",
    age=23,
    salary=90000,
    design_tool="Figma"
)

manager1 = Manager(
    name="Дмитрий",
    age=35,
    salary=150000,
    team_size=8
)


dev1.fix_bug()
designer1.create_mockup()
manager1.hold_meeting()

dev1.increase_salary(10000)

employees = [dev1, designer1, manager1]

company_report(employees)
```


### Пример кода на Java


```java
import java.util.ArrayList;
import java.util.List;

abstract class Employee {
    protected String name;
    protected int age;
    protected double salary;

    public Employee(String name, int age, double salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    // Абстрактный метод (обязателен для переопределения)
    public abstract void work();

    public void showInfo() {
        System.out.println("\n========================");
        System.out.println("Имя: " + name);
        System.out.println("Возраст: " + age);
        System.out.println("Зарплата: " + salary);
    }

    public double getSalary() {
        return salary;
    }

    public void raiseSalary(double amount) {
        if (amount > 0) {
            salary += amount;
            System.out.println(name + " получил повышение на " + amount);
        }
    }
}


class Developer extends Employee {
    private String language;

    public Developer(String name, int age, double salary, String language) {
        super(name, age, salary);
        this.language = language;
    }

    @Override
    public void work() {
        System.out.println(name + " пишет код на " + language);
    }

    public void fixBug() {
        System.out.println(name + " исправляет баги");
    }

    @Override
    public void showInfo() {
        super.showInfo();
        System.out.println("Должность: Разработчик");
        System.out.println("Язык: " + language);
    }
}

class Designer extends Employee {
    private String tool;

    public Designer(String name, int age, double salary, String tool) {
        super(name, age, salary);
        this.tool = tool;
    }

    @Override
    public void work() {
        System.out.println(name + " создаёт дизайн в " + tool);
    }

    public void createMockup() {
        System.out.println(name + " делает макет интерфейса");
    }

    @Override
    public void showInfo() {
        super.showInfo();
        System.out.println("Должность: Дизайнер");
        System.out.println("Инструмент: " + tool);
    }
}


class Manager extends Employee {
    private int teamSize;

    public Manager(String name, int age, double salary, int teamSize) {
        super(name, age, salary);
        this.teamSize = teamSize;
    }

    @Override
    public void work() {
        System.out.println(name + " управляет командой из " + teamSize + " человек");
    }

    public void holdMeeting() {
        System.out.println(name + " проводит собрание");
    }

    @Override
    public void showInfo() {
        super.showInfo();
        System.out.println("Должность: Менеджер");
        System.out.println("Размер команды: " + teamSize);
    }
}

public class Main {
    public static void main(String[] args) {

        List<Employee> employees = new ArrayList<>();

        employees.add(new Developer("Алексей", 25, 120000, "Java"));
        employees.add(new Designer("Мария", 23, 90000, "Figma"));
        employees.add(new Manager("Дмитрий", 35, 150000, 10));

        // Полиморфизм + наследование
        double totalSalary = 0;

        for (Employee e : employees) {
            e.showInfo();
            e.work();
            totalSalary += e.getSalary();
        }

        System.out.println("\n========================");
        System.out.println("Общий фонд зарплат: " + totalSalary);
    }
}
```


### **Ссылка на репозиторий**

```text 
https://github.com/Artomaniia/2ob_POO
```

### **Ссылка на итоговый файл README.md**

```text
https://github.com/Artomaniia/2ob_POO/blob/main/README.md
```

### **Результат работы**

В ходе выполнения лабораторной работы была организована полноценная командная разработка проекта с использованием GitHub Flow, совместной работы через GitHub/GitLab и документирования концепций объектно-ориентированного программирования.
