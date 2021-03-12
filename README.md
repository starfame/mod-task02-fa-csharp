# МИПиС

## Task 02. Разработка детерминированного конечного автомата (ДКА) на C\#

За основу берем пример реализации ДКА

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace fans
{
  public class State
  {
    public string Name;
    public Dictionary<char, State> Transitions;
    public bool IsAcceptState;
  }
  public class FA
  {
        public static State a = new State()
        {
            Name = "a",
            IsAcceptState = false,
            Transitions = new Dictionary<char, State>()
        };
        public State b = new State()
        {
            Name = "b",
            IsAcceptState = false,
            Transitions = new Dictionary<char, State>()
        };
        public State c = new State()
        {
            Name = "c",
            IsAcceptState = true,
            Transitions = new Dictionary<char, State>()
        };

        State InitialState = a;
        
        public FA()
        {
           a.Transitions['0'] = a;
           a.Transitions['1'] = b;
           b.Transitions['0'] = c;
           b.Transitions['1'] = a;
           c.Transitions['0'] = b;
           c.Transitions['1'] = c;            
        }
        
        public bool? Run(IEnumerable<char> s)
        {
            State current = InitialState;
            foreach (var c in s) // цикл по всем символам 
            {
                current = current.Transitions[c]; // меняем состояние на то, в которое у нас переход
                if (current == null)              // если его нет, возвращаем признак ошибки
                    return null;
                // иначе переходим к следующему
            }
            return current.IsAcceptState;         // результат true если в конце финальное состояние 
        }
  }

  class Program
  {
    static void Main(string[] args)
    {
      String s = "0000010111";
      FA fa = new FA();
      bool? result = fa.Run(s);
      Console.WriteLine(result);
    }
  }
}
```

### Задача №1

> Разработать класс ДКА, который допускает бинарную строку, содержащую ровно один '0' и хотя бы одну '1'. 

Класс должен называться **FA1**

### Задача №2

> Разработать класс ДКА, который допускает бинарную строку, содержащей четное количество символов '0' и четное количество символов '1'.

Класс должен называться **FA2**


### Структура проекта

- **fa/program.cs** - файл с реализацией классов **FA1** и **FA2**
- **fa.Tests/UnitTest1.cs** - файл с модульными тестами.
 
### Список участников/веток

см. репозиторий `mod-branches`

### Алгоритм выполнения работы

Для выполнения работы необходимо:

1. Выполнить *fork* репозитария в свой аккаунт.
1. Выполнить клонирование репозитария из своего аккаунта к себе на локальную машину (`git clone`).
1. Создать ветку **git** с индивидуальным номером (`git branch имя_ветки`).
1. Сделать ветку активной (`git checkout имя`).
1. Необходимо разместить как исходные файлы с решениями задач, поместив **cpp** файлы в **src**, а заголовочные - в **include**. 
1. Добавить файлы в хранилище (`git add`).
1. Выполнить фиксацию изменений (`git commit -m "комментарий"`).
1. Отправить содержимое ветки в свой удаленный репозитарий (`git push origin имя_ветки`).
1. Создать пул-запрос в репозитарий группы и ждать результата от **GitHub Actions**.

