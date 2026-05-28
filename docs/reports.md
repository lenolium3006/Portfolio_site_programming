# Доклады 


## Паттерн Factory (Фабрика) в Python

[Кликабельная ссылка на gist](https://gist.github.com/lenolium3006/54b969e9e5bac3fc48c7824da35f43ac)

### **1. Определение и назначение**

Паттерн **Factory (Фабрика)** относится к порождающим (creational) паттернам проектирования и предназначен для **инкапсуляции процесса создания объектов**.

Основная идея данного паттерна заключается в том, что создание объектов происходит **не напрямую через конструктор класса**, а через специальный метод или класс — фабрику.

Это позволяет:

* скрыть детали создания объектов;
* уменьшить зависимость кода от конкретных классов;
* повысить гибкость и расширяемость системы.


### **2. Аналогия: пиццерия как модель фабрики**

Для наглядного понимания рассмотрим аналогию с пиццерией.

Клиент оформляет заказ, указывая тип пиццы, например, «Пепперони» или «Маргарита». При этом он не участвует в процессе приготовления и не взаимодействует с кухней напрямую. Все этапы — от подбора ингредиентов до выпекания — выполняются поваром.

В данной аналогии:

Product - пицца 
ConcreteProduct - конкретная пицца
Creator - идея кухни
ConcreteCreator - повар, который готовит конкретную пиццу

Таким образом, клиенту необходимо лишь указать желаемый тип продукта, а вся логика его создания скрыта внутри фабрики.


### **3. Основные компоненты паттерна**

Паттерн Factory включает в себя следующие элементы:

| Компонент паттерна  | Назначение                                                                                                           |
| ------------------- | --------------------------------------------------------------- 
| **Product**         | Общий интерфейс или базовый класс для всех создаваемых объектов 
| **ConcreteProduct** | Конкретные реализации продукта                                  
| **Creator**         | Класс с фабричным методом, который объявляет создание объектов  
| **ConcreteCreator** | Класс, который реально создаёт конкретный объект                


Такое разделение позволяет изолировать код создания объектов от кода их использования.

<img width="480" height="298" alt="image" src="https://refactoring.guru/images/patterns/diagrams/factory-method/structure-indexed-2x.png?id=c794e4f2d05013fb176464a1d1a5d7ab" />


### **4. Пример реализации на Python**

#### **4.1 Реализация без использования паттерна**

```python
class Dog:
    def speak(self):
        return "Гав"

class Cat:
    def speak(self):
        return "Мяу"

animal_type = "dog"

if animal_type == "dog":
    animal = Dog()
elif animal_type == "cat":
    animal = Cat()

print(animal.speak())
```

Недостатки данного подхода:

* наличие условных конструкций (`if/elif`);
* сложность масштабирования;
* высокая зависимость от конкретных классов.

#### **4.2 Реализация с использованием паттерна Factory**

```python
# Базовый класс (Product)
class Animal:
    def speak(self):
        pass

# Конкретные классы (ConcreteProduct)
class Dog(Animal):
    def speak(self):
        return "Гав"

class Cat(Animal):
    def speak(self):
        return "Мяу"

# Фабрика (Factory)
class AnimalFactory:
    @staticmethod
    def create_animal(animal_type):
        if animal_type == "dog":
            return Dog()
        elif animal_type == "cat":
            return Cat()
        else:
            raise ValueError("Неизвестный тип животного")

# Использование
animal = AnimalFactory.create_animal("dog")
print(animal.speak())
```

В данной реализации:

* логика создания объектов сосредоточена в одном месте;
* клиентский код не зависит от конкретных классов;
* добавление новых типов объектов требует минимальных изменений.



### **5. Преимущества и недостатки**

#### **Преимущества:**

* инкапсуляция процесса создания объектов;
* снижение связности (loose coupling);
* упрощение расширения системы;
* улучшение читаемости и структуры кода.

#### **Недостатки:**

* увеличение количества классов;
* усложнение архитектуры при простых задачах;
* необходимость дополнительного уровня абстракции.



### **6. Когда применять паттерн**

#### **Рекомендуется использовать, если:**

* система должна работать с различными типами объектов;
* тип создаваемого объекта определяется во время выполнения;
* необходимо упростить добавление новых классов.

#### **Не рекомендуется использовать, если:**

* создаётся небольшое количество объектов;
* логика создания объектов является простой;
* использование фабрики приводит к излишнему усложнению кода.

### **7. Пример применения**

```
from abc import ABC, abstractmethod


#Product (Уведомление)

class Notification(ABC):
    @abstractmethod
    def send(self, message):
        raise NotImplementedError



# ConcreteProduct

class EmailNotification(Notification):
    def send(self, message):
        return f"Отправка Email: {message}"


class SMSNotification(Notification):
    def send(self, message):
        return f"Отправка SMS: {message}"


class PushNotification(Notification):
    def send(self, message):
        return f"Push-уведомление: {message}"



# Creator
class NotificationService(ABC):

    def notify(self, message):
        # общий алгоритм
        notification = self.create_notification()
        result = notification.send(message)
        print(result)

    @abstractmethod
    def create_notification(self):
        raise NotImplementedError



#ConcreteCreator

class EmailService(NotificationService):
    def create_notification(self):
        return EmailNotification()


class SMSService(NotificationService):
    def create_notification(self):
        return SMSNotification()


class PushService(NotificationService):
    def create_notification(self):
        return PushNotification()



# Использование

service = EmailService()
service.notify("Привет!")

service = SMSService()
service.notify("Код подтверждения")

service = PushService()
service.notify("Новое сообщение")
```


### **8. Заключение**

Паттерн **Factory** является эффективным инструментом для организации процесса создания объектов. Он позволяет отделить логику создания от логики использования, что делает систему более гибкой, масштабируемой и удобной для сопровождения.

Таким образом, применение данного паттерна особенно оправдано в тех случаях, когда программа должна поддерживать множество вариантов объектов и легко адаптироваться к изменениям.



---

## Наследование в ООП

[Кликабельная ссылка на репозиторий](https://github.com/Artomaniia/2ob_POO/tree/concept/Inheritance/Inheritance/Examples)


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
