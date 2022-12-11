# Oleg Yakubovich

---

## Contacts
* __Location:__ Minsk, Belarus
* __Email:__ olegyakubovich777@gmail.com
* __Phone:__ +375(25)6981195
* __GitHub:__ [Kinglifes](https://github.com/Kinglifes)

---

## About Me
Interest in programming appeared in high school. He successfully entered the MIU Institute for the specialty of programming, was expelled from the end of the 3rd year for failing the exam in higher mathematics. Unfortunately, I could not recover, because. the specialty was changed and there was too much academic difference. Later he was engaged in activities not related to programming, but he always did it for himself. I made the final decision to move into the IT field this spring. To do this, I went to courses, where I study until now.

---

## Skills
* HTML5, CSS3
* JavaScript Basics
* Java Basics
* Phyton Basics
* C# Basics
* Visual Studio, Visual Studio Code
* Git
* Figma

---

## Code example
I haven’t done tasks on codewars yet, so I’ll throw off an example of code from my work in C#.

In the task, it was necessary to create a repository with workers without using "List". One of the project files:
```
struct Repository
    {
        private Worker[] workers;
        private string path;
        int index;

        public Repository(string Path)
        {
            this.path = Path;
            this.index = 0;
            this.workers = new Worker[1];
            
        }

        private void Resize(bool Flag)
        {
            if (Flag)
            {
                Array.Resize(ref this.workers, this.workers.Length * 2);
            }
        }

        public void Add(Worker ConcreteWorker)
        {
            this.Resize(index >= this.workers.Length);
            this.workers[index] = ConcreteWorker;
            this.index++;
        }

        /// <summary>
        /// Метод меню выбора
        /// </summary>
        public void Options() 
        {
            Console.WriteLine("Пожалуйста сделайте свой выбор:");
            Console.WriteLine("1. Просмотреть запись.\n" +
                              "2. Создать запись.\n" +
                              "3. Удалить запись.\n" +
                              "4. Редактировать запись.\n" +
                              "5. Загрузка записей в выбранном диапазоне дат.\n" +
                              "6. Сортировка по возрастанию и убыванию дат.\n" +
                              "0. Выход.");
            int option = int.Parse(Console.ReadLine());
            switch (option)
            {
                case 1:
                    PrintToConsole();
                    break;
                case 2:
                    Save();
                    break;
                case 3:
                    Delete(ref workers);
                    break;
                case 4:
                    Redaction(ref workers);
                    break;
                case 5:
                    LoadForDate(workers);
                    break;
                case 6:
                    DataSort(ref workers);
                    break;
                case 0:
                    Console.WriteLine("Работа завершена.");
                    Console.ReadKey();
                    break;

                default:
                    Console.WriteLine("Пожалуйста, введите корректное значение.");
                    Options();
                    break;
            }
            ContinueOrExit();
        }

        /// <summary>
        /// Метод завершения или продолжения работы
        /// </summary>
        public void ContinueOrExit() 
        {
            Console.WriteLine("Хотите продолжить? (д/н):");
            string coe = Console.ReadLine();
            if (coe != "д" && coe != "н")
            {
                Console.WriteLine("Введите корректный символ.");
                ContinueOrExit();
            }
            else {
                if (coe == "д")
                {
                    Options();
                }
                else
                {
                    Console.WriteLine("Работа завершена.");
                    Console.ReadKey();
                }
            }
        }

        /// <summary>
        /// метод сохранения данных
        /// </summary>
        /// <param name="Path"></param>
        public void Save() 
        {
            Worker worker = new Worker();
            string temp = String.Empty;
            using (StreamWriter streamWriter = new StreamWriter(this.path))
            {
                File.AppendAllText(path, temp);
                worker.ID = Convert.ToString(this.index + 1) + "#";

                worker.Data = DateTime.Now.ToShortTimeString() + "#";


                Console.WriteLine("Введите ФИО сотрудника: ");
                worker.FullName = Console.ReadLine() + "#";

                Console.WriteLine("Введите возраст сотрудника: ");
                worker.Year = Console.ReadLine() + "#";

                Console.WriteLine("Введите рост сотрудника: ");
                worker.Height = Console.ReadLine() + "#";

                Console.WriteLine("Введите дату рождения сотрудника: ");
                worker.BirthDay = Console.ReadLine() + "#";

                Console.WriteLine("Введите место рождения сотрудника: ");
                worker.BirthPlace = Console.ReadLine() + "#";
                Add(worker);
                File.WriteAllText(path, string.Join("\n", workers));
            }
        }

        /// <summary>
        /// метод вывода в консоль
        /// </summary>
        public void PrintToConsole()
        {
            File.Create(path);
            using (StreamReader streamReader = new StreamReader(this.path))
            {
                File.Create(path);
                while (!streamReader.EndOfStream)
                {
                    string[] line = streamReader.ReadLine().Split('#');
                    for (int i = 0; i < line.Length; i++)
                    {
                        Console.WriteLine(line[i] + " ");
                    }
                    Console.Write("\n");
                }

               
            }
        }

        public void Delete(ref Worker[] workers)
        {
            
            Console.Write("Введите ID сотрудника которого хотите удалить: ");
            int x = int.Parse(Console.ReadLine());
            Worker[] newWorkers = new Worker[workers.Length - 1];
            for (int i = 0; i < x - 1; i++)
            {
                newWorkers[i] = workers[i];
                
            }

            for (int i = x; i < workers.Length; i++)
            {
                newWorkers[i - 1] = workers[i];
            }

            workers = newWorkers;
            for(int i = x; i < workers.Length; i++)
            {
                string id = workers[i].ID;
                int id1 = int.Parse(id);
                workers[i].ID = Convert.ToString(id1 - 1);
            }
            File.WriteAllText(path, string.Join("\n", workers));
            
        }

        public void Redaction(ref Worker[] workers)
        {
            Console.WriteLine("Введите ID сотрудника для редактирования: ");
            int id1 = int.Parse(Console.ReadLine());
            Worker worker = workers[id1 - 1];
            Console.WriteLine("Сделайте выбор: ");
            Console.WriteLine("0. Редактировать всю запись.\n" +
                              "1. Редактировать ФИО.\n" +
                              "2. Редактировать возраст.\n" +
                              "3. Редактировать рост.\n" +
                              "4. Редактировать дату рождения.\n" +
                              "5. Редактировать место рождения.");
            int x = int.Parse(Console.ReadLine());
            switch (x)
            {
                case 0:
                    Console.WriteLine("Введите ФИО сотрудника: ");
                    workers[id1 - 1].FullName = Console.ReadLine();

                    Console.WriteLine("Введите возраст сотрудника: ");
                    workers[id1 - 1].Year = Console.ReadLine();

                    Console.WriteLine("Введите рост сотрудника: ");
                    workers[id1 - 1].Height = Console.ReadLine();

                    Console.WriteLine("Введите дату рождения сотрудника: ");
                    workers[id1 - 1].BirthDay = Console.ReadLine();

                    Console.WriteLine("Введите место рождения сотрудника: ");
                    workers[id1 - 1].BirthPlace = Console.ReadLine();

                    File.WriteAllText(path, string.Join("\n", workers));
                    break;
                case 1:
                    Console.WriteLine("Введите ФИО сотрудника: ");
                    workers[id1 - 1].FullName = Console.ReadLine();
                    File.WriteAllText(path, string.Join("\n", workers));
                    break;
                case 2:
                    Console.WriteLine("Введите возраст сотрудника: ");
                    workers[id1 - 1].Year = Console.ReadLine();
                    File.WriteAllText(path, string.Join("\n", workers));
                    break;
                case 3:
                    Console.WriteLine("Введите рост сотрудника: ");
                    workers[id1 - 1].Height = Console.ReadLine();
                    File.WriteAllText(path, string.Join("\n", workers));
                    break;
                case 4:
                    Console.WriteLine("Введите дату рождения сотрудника: ");
                    workers[id1 - 1].BirthDay = Console.ReadLine();
                    File.WriteAllText(path, string.Join("\n", workers));
                    break;
                case 5:
                    Console.WriteLine("Введите место рождения сотрудника: ");
                    workers[id1 - 1].BirthPlace = Console.ReadLine();
                    File.WriteAllText(path, string.Join("\n", workers));
                    break;
                default:
                    Console.WriteLine("Введите корректное число");
                    Redaction(ref workers);
                    break;
            }
        }

        public void LoadForDate(Worker[] workers)
        {
            Console.WriteLine("Выберите с какой даты по какую(включительно)," +
                " вывести информацию.");
            Console.WriteLine("С какой даты начать: ");
            Console.Write("Введите число: ");
            int d = int.Parse(Console.ReadLine());
            Console.Write("Введите месяц: ");
            int m = int.Parse(Console.ReadLine());
            Console.Write("Введите год: ");
            int y = int.Parse(Console.ReadLine());
            string from = new DateTime(y, m, d).ToShortTimeString();
            
            Console.WriteLine("По какаю дату: ");
            Console.Write("Введите число: ");
            int d1 = int.Parse(Console.ReadLine());
            Console.Write("Введите месяц: ");
            int m1 = int.Parse(Console.ReadLine());
            Console.Write("Введите год: ");
            int y1 = int.Parse(Console.ReadLine());
            string to = new DateTime(y1, m1, d1).ToShortTimeString();

            int fromIndex = 0;
            int toIndex = 0;
            for (int i = 0; i < workers.Length; i++)
            {
                if (workers[i].Data == from)
                {
                    fromIndex = i;
                }
                if (workers[i].Data == to)
                {
                    toIndex = i;
                }
            }
            File.OpenWrite(path);
            using (StreamReader streamReader = new StreamReader(this.path))
            {
                File.Create(path);
                while (!streamReader.EndOfStream)
                {
                    string[] line = streamReader.ReadLine().Split('#');
                    for (int i = fromIndex; i <= toIndex; i++)
                    {
                        Console.WriteLine(line[i] + " ");
                    }
                    Console.Write("\n");
                }
            }
        }

        public void DataSort(ref Worker[] workers)
        {
            Console.WriteLine("Остсортировать даты по возростанию(в) или убыванию(у):");
            Console.Write("Выберите (в/у): ");
            string sort = Console.ReadLine();
            switch (sort)
            {
                case "в":
                    workers = workers.OrderBy(w => w.Data).ToArray();
                    break;
                case "у":
                    workers = workers.OrderByDescending(w => w.Data).ToArray();
                    break;
                default:
                    Console.WriteLine("Введите корректный символ.");
                    DataSort(ref workers);
                    break;
            }
            File.WriteAllText(path, string.Join("\n", workers));
        }
    } 
```

---

## Courses
* __SkillBox:__  game development (in progress)
![SkillBox](img/scrinSkillbox.png)
* __Stepik:__
![Stepik](img/scrinStepik.png)

---

## Languages
* English - Beginer (I write all the text using google translate). (In Progress)
* Russian - Native