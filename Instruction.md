**Инструкция по работе с Git**

**Основы**

Git — это набор консольных утилит, которые отслеживают и фиксируют изменения в файлах.

*Для чего он нужен?*

- Во-первых, чтобы отследить изменения, произошедшие с проектом, со временем.
- Во-вторых он чрезвычайно полезен при одновременной работе нескольких специалистов, над одним проектом.

**Установка**

Введение в Git всегда начинается с установки: [скачайте Git](https://git-scm.com/downloads) для Windows, macOS или Linux и проверьте версию с помощью команды *git --version*.

Далее устанавливаем [Visual Studio Code](https://code.visualstudio.com/)

**Настройка конфигурационного файла**

Первое, что нужно сделать, — настроить имя пользователя и email для идентификации. Эти настройки хранятся в конфигурационном файле.

Вы можете напрямую отредактировать файл .gitconfig в текстовом редакторе или сделать это командой git config --global --edit. Для отдельных полей это:
- git config --global user.name <значение имени>;
- git config --global user.email <значение почты>.
![<Базовая конфигурация>](../GitFolder/Config.png)

Для того, чтобы посмотреть все настройки системы, используйте команду
*git config --list*

Если вы не до конца настроили систему для работы, в начале своего пути - не беда. Git всегда подскажет разработчику, если тот запутался, например:

Команда *git --help* - выводит общую документацию по git
Если введем *git log --help* - он предоставит нам документацию по какой-то определенной команде
Если вы вдруг сделали опечатку - система подскажет вам нужную команду
После выполнения любой команды - отчитается о том, что вы натворили
Также Гит прогнозирует дальнейшие варианты развития событий и всегда направит разработчика, не знающего, куда двигаться дальше
Тут стоит отметить, что подсказывать система будет на английском, но не волнуйтесь, со временем вы изучите несложный алгоритм ее работы и будете разговаривать с ней на одном языке.

**Создаём Git-репозиторий**

Как мы отметили ранее, git хранит свои файлы и историю прямо в папке проекта. Чтобы создать новый репозиторий, нам нужно открыть терминал, зайти в папку нашего проекта и выполнить команду init. Это включит приложение в этой конкретной папке и создаст скрытую директорию .git, где будет храниться история репозитория и настройки.
1. Создайте на рабочем столе папку под названием git_folder.
2. Откройте терминал: Вид > Терминал
3. В терминале ввидите *git init*

**Коммиты**

Основы работы с Git предполагают понимание коммитов. Команда git commit откроет текстовый редактор для ввода сообщения коммита. Также эта команда принимает несколько аргументов:

- -m позволяет написать сообщение вместе с командой, не открывая редактор. Например git commit -m "Пофиксил баг";
- -a переносит все отслеживаемые файлы в область подготовленных файлов и включает их в коммит (позволяет пропустить git add перед коммитом);
- --amend заменяет последний коммит новым изменённым коммитом, что бывает полезно, если вы неправильно набрали сообщение последнего коммита или забыли включить в него какие-то файлы.

Советы для эффективного введения в Git:

- Коммитьте как можно чаще.
Одно изменение — один коммит: не помещайте все не связанные между собой изменения в один коммит, разделите их, чтобы было проще откатиться.
- Формат сообщений: заголовок должен быть в повелительном наклонении, меньше 50 символов в длину и должен логически дополнять фразу this commit will ___(this commit will fix bugs — этот коммит исправит баги). Сообщение должно пояснять, почему был сделан коммит, а сам коммит показывает, что изменилось.
- Если у вас много незначительных изменений, хорошим тоном считается делать небольшие коммиты при разработке, а при добавлении в большой репозиторий объединять их в один коммит.

**Файловая система Git**

![<Структура файловой системы>](../GitFolder/File_System.png)

Git отслеживает файлы в трёх основных разделах:

1. Рабочая директория (файловая система вашего компьютера);
2. Область подготовленных файлов (staging area, хранит содержание следующего коммита);
3. HEAD (последний коммит в репозитории).
Все основные команды по работе с файлами сводятся к пониманию того, как Git управляет этими тремя разделами. Существует распространённое заблуждение, что область подготовленных файлов только хранит изменения. Лучше думать об этих трёх разделах как об отдельных файловых системах, каждая из которых содержит свои копии файлов.

**Просмотр изменений в файловых системах**

Команда *git status* отображает все файлы, которые различаются между тремя разделами. У файлов есть 4 состояния:

1. Неотслеживаемый (untracked) — находится в рабочей директории, но нет ни одной версии в HEAD или в области подготовленных файлов (Git не знает о файле).
2. Изменён (modified) — в рабочей директории есть более новая версия по сравнению с хранящейся в HEAD или в области подготовленных файлов (изменения не находятся в следующем коммите).
3. Подготовлен (staged) — в рабочей директории и области подготовленных файлов есть более новая версия по сравнению с хранящейся в HEAD (готов к коммиту).
4. Без изменений — одна версия файла во всех разделах, т. е. в последнем коммите содержится актуальная версия.
*Примечание: Файл может быть одновременно в состоянии «изменён» и «подготовлен», если версия в рабочей директории новее, чем в области подготовленных файлов, которая в свою очередь новее версии в HEAD.*

Мы можем использовать опцию *-s* для команды *git status*, чтобы получить более компактный вывод (по строке на файл). Если файл не отслеживается, то будет выведено ??; если он был изменён, то его имя будет красным, а если подготовлен — зелёным.

Чтобы посмотреть сами изменения, а не изменённые файлы, можно использовать следующие команды:

git diff — сравнение рабочей директории с областью подготовленных файлов;
git diff --staged — сравнение области подготовленных файлов с HEAD.


Далее всю полезную информацию можно найти по следующим ссылкам:
- [Статья 1](https://tproger.ru/translations/beginner-git-cheatsheet/)
- [Статья 2](https://proglib.io/p/git-for-half-an-hour)
- [Статья 3](https://docs.microsoft.com/ru-ru/contribute/markdown-reference)
