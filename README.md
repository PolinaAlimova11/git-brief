## Это краткое пособие, как настраивать проект Git
---
Прежде чем приступить к созданию репозитория, необходимо:
* настроить конфигурацию git с именем создателя и с почтой привязки

Для этого необходимо выполнить команду

```
git config --global user.name <name>

git config --global user.email <email>
```

Все навтройки хранятся в файле *.gitconfig*

Для проверки конфигурации вызовете команду:

```
git config --list
```

### Настройка локального репозитория

На локальном компьютере в той папке, которую планируется сделать репозиторием,
необходимо выполнить команду инициализации.

```
git init
```

Если папка была выбрана ошибочно, то чтобы её *"разгитить"* достаточно будет удалить файл .git:


```
rm -rf .git
```

Проверка статуса осуществляется с помощью команды:

```
git status
```

#### Добавление изменений в текущую версию

Далее будет представленна простая инструкция сохранения изменений в локальном репозитории.

1. Необходимо подготовить файлы к их сохранению, а именнно выбрать файлы для отслеживания изменений

```
git add <name_file>
```

Можно также воспользоваться командой:

```
git add --all
```

Эта команда сохраняет изменения, которые необходимо сохранить (выстраивает композицию для *фотографии* гита).

2. Сделать коммит

То есть сохранить изменения и прокомментировать, что за изменения были внесены:

```
git commit -m '<comment>'
```

3. Проверить статус коммитов можно с помощью команды

```
git log
```

### Настройка удаленного репозитория

Для использования полных возможностей Git, можно поделиться собственным репозиторием с другими людьми,
чтобы проводить совместную работу с ними. Для этого необходимо воспользоваться платформой *GitHub*, с
помощью которой можно размещать свои репозитории в открытом доступе.

1. Для начала необходимо настроить связь с сервером GitHub с помощью SSH-ключей. Подробней про данную настройку
можно узнать по [ссылке](https://docs.github.com/ru/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

2. После настройки канала связи можно создать удаленный репозиторий. Для этого необходимо создать его
в своём аккаунте на *GitHub* в разделе репозиториев. Для начала достаточно дать название репозиторию
и настроить доступ к нему (публичный или приватный)

### Связь локального и удаленного репозитория

Чтобы можно было выгружать изменения из локального репозитория в удаленный, необходимо
связать их.

**Связывание** происходит с помощью команды:

```
git remote add <name> <URL>
```

В качестве имени удаленного репозитория выступает *origin* а далее прикрепляется ссылка на удаленный репозиторий, которую можно
скопировать с сайта GitHub.

Например, команда может выглядеть так:

```
git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git
```

Для проверки связи можно использовать команду:

```
git remote -v
```

### Отправляем изменения

Чтобы синхронизировать и связать изменения двух репозиториев, в локальном репозитории необходимо выполнить команду

```
git push
```

Однако в первый раз необходимо указать параметры связи:

```
git push -u origin <branch>
```

В качестве ветки может выступать 'main/master'. В следующие разы уже не нужно будет указывать дополнительные
параметры.

### Хэш и лог

Для каждого *commit* вычисляется хэш: "снимок" автора, даты и файлов в данном
коммите. Он вычисляется по определенному алгоритму, поэтому при индентичном наборе
выходит одна и та же комбинация из цифр и латинских букв. Именно по **хэшу** можно
обратиться к контретному коммиту.

Если воспользоваться командой

```
git log
```

То можно увидеть все коммиты, дату их создания, авторов, комментарий и хэш.
Однако иногда сложно ориентироваться в огромном потоке данных, поэтому есть более сокращенная версия
для чтения и ориентации по коммитам:

```
git log --oneline
```

Данная команда выведет более коротную информацию о коммите: его хэш и название (комментарий).

Чтобы не выводить длинную строчку хэша, он обрезается по алгоритму, который представляет
достаточную длину хэша, чтобы можно было ориентироваться по нему и отыскать данный коммит в
хэш-таблице.

### HEAD файл

В репозитории существует папка *.git*, в которой расположен HEAD файл. В данном файле
хранится информация о последнем коммите, точнее, ссылка на хэш последнего коммита. Если перейти
по ссылке, то можно наткнуться на содержимое файла, в точности совпадающее с хэшем последнего
выполненного коммита.

Если необходимо перейти на последний коммит, то можно использовать не хэш запись, а эквивалент
*HEAD*, который является ссылкой на ссылку к последнему коммиту.

### Статус файла

На протяжении всего существования файла в репозитории, он может проходить несколько стадий.

Если не углубляться в статусы информации файла, то его можно обозначить как:

* untracked - "неотслеживаемый", то есть файл, за чьим изменением git не следит, он просто
существует в папке, не более того

* tracked - "отслеживаемый", тот файл, за чьим жизненным путем внимательно следит система git и сравнивает
с его предыдущими версиями.

Сделать файл *tracked* очень просто - достаточно просто добавить его в отслеживаемые файлы командой

```
git add <name_file>
```

Теперь файл является отслеживаемым, и его изменения нам важны.

Однако не все отслеживаемые файлы отправляются в коммит. Файлы могут быть изменены в ходе разработки, поэтому появляются новуе статусы файла:

* tracked - файл был до этого изменен и добавлен в коммит, обычно, такие
файлы не отображаются в *git log*

* staged - файл подготовлен к отправке в коммит, однако ещё не является "сфотографированным"

* modified - измененный отслеживаемый файл, чьи изменения не подготовили для
коммита.

На примере всё просто:

1. Файл создают в репозитории - он **untracked**

2. Файл добавляют к отслеживанию командой *git add* - он **staged** и **tracked**

3. Производят коммит командой *git commit -m ...* - он уже просто **tracked**

4. В файл вносят изменения - он становится **modified** и **tracked**

5. Файл добавляют к отслеживанию вновь - он **staged** и **tracked**

6. Вспоминаются новые правки, файл изменяется до коммита - теперь файл и **modified**, и **staged**.
Тут всё просто: предыдущая версия добавлена в отслеживание, при этом измененная версия нет. Нужно лишь ещё раз ввести файл в отслеживание.

7. Вновь выполняем добавление *git add <name_file>* - файл **staged** и **tracked**

8. Выполняем коммит - он вновь просто **tracked**

### Сообщения в коммитах

Важным правилом сообщения в коммитах является их информативность. Не правильно комментировать
*"исправлены ошибки"* или *"добавлена фича"*, потому что из-за данных неясностей
придется открывать коммит и просматривать конкретные изменения.

Чтобы быстро ориентироваться, нужно четко прописывать выполненные действия с конкретикой.
К примеру:

* Испарвлена ошибка посторной отправки заказа

* Добавлена функция отслеживания товара

* Исправить №334б добавить график темепратуры

Также существуют общепринятые правила оформления, которые представлены [тут](https://www.conventionalcommits.org/ru/v1.0.0-beta.4/#%D1%81%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F)