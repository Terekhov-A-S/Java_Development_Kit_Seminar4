# Java Development Kit (семинары)

![picture for project](https://raw.githubusercontent.com/Terekhov-A-S/Java_Development_Kit_Seminar4/main/src/main/resources/sa.jpg)

## Урок 4. Коллекции


### Задача.

Создать справочник сотрудников.
Необходимо:
Создать класс справочник сотрудников, который содержит внутри коллекцию сотрудников - каждый сотрудник должен иметь следующие атрибуты:
Табельный номер;
Номер телефона;
Имя;
Стаж.
Добавить метод, который ищет сотрудника по стажу (может быть список).
Добавить метод, который возвращает номер телефона сотрудника по имени (может быть список).
Добавить метод, который ищет сотрудника по табельному номеру.
Добавить метод добавление нового сотрудника в справочник.

#### Решение

Создадим класс Employee, геттеры и переопределим возврат значения в строки.

<details>

  <summary>Нажмите, чтобы открыть код</summary>

```java
class Employee {
    private int employeeId;
    private String phoneNumber;
    private String name;
    private int experience;

    public Employee(int employeeId, String phoneNumber, String name, int experience) {
        this.employeeId = employeeId;
        this.phoneNumber = phoneNumber;
        this.name = name;
        this.experience = experience;
    }

    public int getEmployeeId() {
        return employeeId;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }

    public String getName() {
        return name;
    }

    public int getExperience() {
        return experience;
    }

    @Override
    public String toString() {
        return  "табельный номер = " + employeeId +
                ", номер телефона = '" + phoneNumber + '\'' +
                ", имя = '" + name + '\'' +
                ", стаж = " + experience;
    }
}
    
```

</details>

Далее создадим клаас EmployeeDirectory, который будет содержать список сотрудников, а так же методы для возврата необходимой информации.

<details>

  <summary>Нажмите, чтобы открыть код</summary>

```java
class EmployeeDirectory {
    private List<Employee> employees;

    public EmployeeDirectory() {
        this.employees = new ArrayList<>();
    }

    public void addEmployee(Employee employee) {
        employees.add(employee);
    }

    public List<Employee> findEmployeesByExperience(int targetExperience) {
        List<Employee> result = new ArrayList<>();
        for (Employee employee : employees) {
            if (employee.getExperience() == targetExperience) {
                result.add(employee);
            }
        }
        return result;
    }

    public String findPhoneNumberByName(String targetName) {
        for (Employee employee : employees) {
            if (employee.getName().equals(targetName)) {
                return employee.getPhoneNumber();
            }
        }
        return "Сотрудник не найден";
    }

    public Employee findEmployeeByEmployeeId(int targetEmployeeId) {
        for (Employee employee : employees) {
            if (employee.getEmployeeId() == targetEmployeeId) {
                return employee;
            }
        }
        return null;
    }
    
```

</details>

Далее в методе main создадим пустую коллекцию с сотрудниками. После этого воспользуемся методами для добавления новых записей в эту коллекцию, поиском сотрудников по стажу, поиском номера телефона по имени, поиском сотрудников по табельному номеру.

<details>

  <summary>Нажмите, чтобы открыть код</summary>

```java
public static void main(String[] args) {
        EmployeeDirectory directory = new EmployeeDirectory();

        // Добавление новых сотрудников
        directory.addEmployee(new Employee(1, "8(985)863-96-74", "Иванов Николай Петрович", 5));
        directory.addEmployee(new Employee(2, "8(635)878-85-48", "Сидорова Виктория Ивановна", 3));
        directory.addEmployee(new Employee(3, "8(485)125-32-21", "Калмыкова Юлия Сергеевна", 1));
        directory.addEmployee(new Employee(4, "8(519)362-46-31", "Дедков Иван Юрьевич", 10));
        directory.addEmployee(new Employee(5, "8(785)496-49-11", "Симухин Владимир Митрофанович", 7));

        // Поиск сотрудников по стажу
        List<Employee> employeesWithExperience3 = directory.findEmployeesByExperience(3);
        System.out.println("Сотрудники со стажем 3 года: " + employeesWithExperience3);

        // Поиск номера телефона по имени
        String phoneNumberIvanov = directory.findPhoneNumberByName("Иванов Николай Петрович");
        System.out.println("Номер телефона для: 'Иванов Н.П.': " + phoneNumberIvanov);

        // Поиск сотрудника по табельному номеру
        Employee employeeById2 = directory.findEmployeeByEmployeeId(2);
        System.out.println("Информация о сотруднике с табельным номером 2: " + employeeById2);
    }
    
```

</details>


Все работает корректно, согласно задания:

![work is correct](https://raw.githubusercontent.com/Terekhov-A-S/Java_Development_Kit_Seminar4/main/src/main/resources/2024-02-24_18-48-30.png)

---


*Подготовил студент Geek Brains* [**`Терехов Александр`**](https://gb.ru/users/1db43d0f-6c3d-46d1-bf5e-974b49af6f0d), Java_Development_Kit_Seminar4