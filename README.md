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