## Настраиваем хук пре-коммит для flake8
Можно настроить гит в проекте так, чтобы перед коммитом
происходила проверка линтером flake8
(пакеты здесь ставятся глобально, но можно в venv)

```
sudo pip install flake8
sudo pip install pre-commit
```

в корне проекта сделать файл .pre-commit-config.yaml
в нем базовое содержимое
```
repos:
-   repo: https://github.com/pycqa/flake8
    rev: '7.0.0'
    hooks:
    -   id: flake8

```

затем для установки хука в гит

```
pre-commit install
```

если будет ошибка
```
aaa@aaa-laptop:~/coding/python/flake8-git-test$ pre-commit

```
An error has occurred: InvalidConfigError:\

==> File .pre-commit-config.yaml\

=====> Expected a Config map but got a list\

Check the log at /home/aaa/.cache/pre-commit/pre-commit.log


то выполнить команду
```
pre-commit migrate-config
```

Теперь при коммите в первую очередь будет срабатывать flake8,\
который не даст пройти коммиту, если есть ошибки.

Если при коммите будет сообщение вида

```

git commit -m 'bad commit'

[WARNING] The 'rev' field of repo 'https://github.com/pycqa/flake8' appears to be a mutable reference ...

```

то поможет команда

```

pre-commit autoupdate

```

которая добавит версию Флака в поле rev

Линк:

[flake8-using-hooks](https://flake8.pycqa.org/en/7.0.0/user/using-hooks.html)
```

