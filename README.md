#Заголовок1


_курсивный текст_
**жирный шрфт**
~~зачеркнутый текст~~
----


##Заголовок2
1. первая строка
2. вторая строка
----


###Ссылки
* [Яндекс](https://www.yandex.ru)
* [Яндекс](https://www.yandex.ru "Я Яндекс")
----

####Код
```bash
ls -la
```
```
mkdir my_project
cd my_project
git init
```


##### Заголовок5
**HEAD** -- это голова.
**Коммит** -- это всему голова.
Внутри HEAD — ссылка на служебный файл: refs/heads/master (или refs/heads/main в зависимости от названия ветки). Если заглянуть в этот файл, можно увидеть хеш последнего коммита.
```
$ cat refs/heads/master # взяли ссылку из файла HEAD
# внутри хеш
e007f5035f113f9abca78fe2149c593959da5eb7

$ git log 
# сверяем с хешем последнего коммита
commit e007f5035f113f9abca78fe2149c593959da5eb7
Author: John Doe <johndoe@example.com>
Date:   Tue Mar 28 00:26:53 2023 +0300

    Добавить амбиций в список дел

... # другие коммиты
```
Когда вы делаете коммит, Git обновляет refs/heads/master — записывает в него хеш последнего коммита. Получается, что HEAD тоже обновляется, так как ссылается на refs/heads/master.

**Статусы** untracked/tracked, staged и modified
untracked (англ. «неотслеживаемый»)
staged (англ. «подготовленный»)
tracked (англ. «отслеживаемый»)
modified (англ. «изменённый»)

1. Файл только что создали. Git про него ещё ничего не знает. Состояние: untracked.
2. Файл добавили в staging area с помощью git add. Состояние: staged (+ tracked).
	Возможно, изменили файл ещё раз. Состояния: staged, modified (+ tracked).
	Обратите внимание: staged и modified у одного файла, но у разных его версий.
	Ещё раз выполнили git add. Состояние: staged (+ tracked).
3. Сделали коммит с помощью git commit. Состояние: tracked.
4.  Изменили файл. Состояние: modified (+ tracked).
5. Снова добавили в staging area с помощью git add. Состояния: staged (+ tracked).
6. Сделали коммит. Состояния: tracked.
7. Повторили пункты 

```mermaid
graph LR;
  untracked -- "git add" --> staged;
  modified  -- "git add" --> staged;
  staged    -- "git commit"     --> tracked/comitted;
  tracked/comitted -- "изменения"     --> modified;
  staged  -- "изменения"   --> modified;

%% стрелка без текста для примера: 
  A --> B;
``` 
###### Заголовок6

1. Команда git restore --staged <file> переведёт файл из staged обратно в modified или untracked.
2. Команда git reset --hard <commit hash> «откатит» историю до коммита с хешем <hash>. Более поздние коммиты потеряются!
3. Команда git restore <file> «откатит» изменения в файле до последней сохранённой (в коммите или в staging) версии.
