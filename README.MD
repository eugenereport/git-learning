## Титул
## Вивчення Git
## Виконав студент: Прокопенко Євгеній ІПЗ-4.04
## з дисципліни: **"Розробка та програмування координатних систем"**

## Конфігурація середи

Використовуючи наступні git команди, виконаємо встановлення пошти та імені користувача:

> git config --global user.name "deyouare"

> git config --global user.email "deyouare@gmail.com"

Встановимо назву головної гілки за замовчуванням:

> git config --global init.defaultBranch main

Вставновимо правила обробки закінчень файлів:

> git config --global core.autocrlf true

> git config --global core.safecrlf warn

## Стартовий проєкт

#### 1. Створення стартового проєкта

Створимо нову директорію для проєкта, перейдемо до неї та створимо там html файл, наступними командами:

```bash
mkdir work
cd work
touch hello.html
```

Виконаємо ініціалізацію git:

> git init

Додамо файл `hello.html` до репозиторія:

> git add hello.html

Створимо перший коміт доданих файлів з повідомленням `Initial Commit`:

> git commit -m "Initial Commit"

Перевіримо статус репозиторія:

> git status

**Результат:**

![Перевірка гіт статусу](screenshots/1_first_git_status.png)

Поточна гілка — головна, нема файлів для створення комітів.

#### 2. Зміна файлів

Змінимо вміст файла `hello.html`:

```html
<h1>Hello, World!</h1>
```

Перевіримо статус репозиторія:

> git status

**Результат:**

![Перевірка гіт статусу після зміни файла](screenshots/2_git_status_after_change.png)

Git відзначив наявність змін у файлі `hello.html`.

Додамо поточний стан файла до наступного коміту та перевіримо статус репозиторія:

> git add hello.html

> git status

**Результат:**

![Перевірка гіт статусу після додання файлу](screenshots/3_git_status_after_add.png)

Git відзначив готовність `hello.html` до коміту.

Створимо коміт та переглянемо історію проєкта:

> git commit -m "Added h1 tag"

> git log --oneline

**Результат:**

![Перегляд історії комітів](screenshots/4_git_history_check.png)

Можна побачити два наявних коміта з відповідними повідомленнями, що були додані раніше.

#### 3. Отримання старих версій

Перевіримо поточний вміст файлу `hello.html`:

> cat hello.html

**Результат:**

![Перевірка поточного вміста файла hello.html](screenshots/5_hello_html_now.png)

Переключимось на стару версію репозиторію на перший коміт:

> git checkout 40adbfd

Перевіримо поточний вміст файлу `hello.html`:

> cat hello.html

**Результат:**

![Перевірка вміста файла hello.html на першому коміті](screenshots/6_hello_html_before.png)

Як можна побачити, ми повернулись на пусту версію файлу `hello.html`.

Повернемося до останнього коміту:

> git switch main

Знов перевіримо вміст файлу `hello.html`:

> cat hello.html

**Результат:**

![Перевірка вміста файла hello.html після повернення на останній](screenshots/7_hello_html_newest.png)

#### 3. Тагування

Виконаємо тагування комітів:

```bash
git tag v1-beta 40adbfd
git tag v1 edf6419
```

Перевіримо встановлені таги:

> git tag

**Результат:**

![Перевірка виставлених до комітів тегів](screenshots/8_git_tag.png)

Усього було додано два тега: `v1-beta` та `v1`.

#### 4. Скасування запланованих дій

Змінимо файл `hello.html`:

> cat hello.html

**Результат:**

![Нова зміна файла hello.html](screenshots/9_hello_html_new_change.png)

Заплануємо зміну файла до коміту:

> git add hello.html

Перевіримо статус репозиторія:

> git status

**Результат:**

![Статус репозиторія](screenshots/10_git_status.png)

Відмінемо додання файлу `hello.html`:

> git reset HEAD hello.html

Переведемо файл `hello.html` до версії останнього коміту:

> git checkout hello.html

Перевіримо файл `hello.html`:

> cat hello.html

**Результат:**

![Відкат зміни файла hello.html, вміст файлу](screenshots/11_hello_html_reset.png)

#### 5. Відкат коміту

Зробимо зміни до файлу `hello.html` та створимо новий коміт:

```bash
git add hello.html
git commit -m "Oops, bad commit!"
```

Перевіримо результат:

> git log --oneline

**Результат:**

![Список комітів](screenshots/12_git_log.png)

Створимо коміт, який відкатить зміни поточного:

> git revert HEAD

Перевіримо результат:

> git log --oneline

**Результат:**

![Список комітів після відміни коміту](screenshots/13_git_log_revert.png)

Для видалення зайвих комітів, та відкату до версії `v1`, промаркуємо поточний коміт як `currpoint`:

> git tag currpoint

Перевіримо результат:

> git log --oneline

**Результат:**

![Список комітів після маркування останнього](screenshots/14_git_log_after_new_tag.png)

Повернемося до версії `v1`:

> git reset --hard v1

Перевіримо результат:

> git log --all --oneline

**Результат:**

![Список комітів після ресета](screenshots/15_git_log_after_reset.png)

Згідно до результатів, поточним комітом став коміт з тегом `v1`.

Видалимо тег `currpoint`:

> git tag -d currpoint

Перевіримо результат:

> git log --all --oneline

**Результат:**

![Список комітів після видалення тегу](screenshots/16_git_log_after_delete_tag.png)

Зайві коміти зникли з історії комітів після видалення тегу, який посилався на останній коміт.

#### 6. Зміна останнього коміту

У початок файлу `hello.html` було додано новий рядок з позначенням автора та електронної адреси:

> cat hello.html

**Результат:**

![Вміст файлу hello.html після додання автора та електронної пошти](screenshots/17_hello_html_author.png)

Створимо коміт:

> git add hello.html

> git commit -m "Added copyright statement with email"

Перевіримо результат:

> git log --oneline

**Результат:**

![Список комітів після зміни файла hello.html](screenshots/18_git_log_after_add_author.png)

Виправимо файл `hello.html`, додамо забутий символ `@`:

> cat hello.html

**Результат:**

![Вміст файлу hello.html після виправлення електронної пошти](screenshots/19_hello_html_author.png)

Виконаємо злиття:

> git add hello.html

> git commit --amend -m "Added copyright statement with email"

Перевіримо результат:

> git log --oneline

**Результат:**

![Список комітів після зміни останнього коміта](screenshots/20_git_log_after_ammend.png)

#### 7. Створення гілки

Створімо нову гілку для праці зі стилями:

> git switch -c style

Перевіримо статус репозиторія:

> git status

**Результат:**

![Статус репозиторія після додання нової гілки](screenshots/21_git_status_after_new_branch.png)

Створилася нова гілка `style`, яка стала поточною гілкою.

Створімо новий файл для стилів

> touch style.css

З вмістом:

```css
h1 {
  color: orange;
}
```

Додамо зміни до коміту:

> git add style.css

> git commit -m "Added css stylesheet"

Відповідно змінимо файл `hello.html`:

```html
<!-- Author: Prokopenko Yevhenii (deyouare@gmail.com) -->
<html>
  <head>
    <link type="text/css" rel="stylesheet" media="all" href="style.css" />
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

Додамо зміни до коміту:

> git add hello.html

> git commit -m "Included stylesheet into hello.html"

#### 8. Безпечне перейменування(переміщення) файлів

Змінимо назву файлу `hello.html` на `index.html`: 

> git mv hello.html index.html

Додамо зміни до коміту:

> git add .

> git commit -m "Renamed hello.html"

#### 9. Завантаження репозиторія на github

Додамо посилання на віддалений репозиторій:

> git remote add origin https://github.com/eugenereport/git-learning.git

Завантажимо головну гілку `main` та гілку `style`:

> git push -u origin main

> git push -u origin style

**Результат:**

Перевіримо репозиторій на сайті `https://github.com`.

![Репозиторій на сайті github](screenshots/22_github.png)

**Репозиторій успішно завантажився на сайт github.com!**

## Висновок

Git — це система контролю версій, яка дозволяє відстежувати зміни в коді та координувати роботу в команді. Він потрібен для того, щоб забезпечити ефективне управління змінами у проектах, дозволяючи працювати декільком розробникам над одним проєктом. Git корисний тим, що забезпечує збереження історії змін, дозволяє швидко повернутися до попередніх версій коду, спрощує процес злиття змін та сприяє кращій організації командної роботи.

У ході виконання цієї роботи я підтвердив теоретичний матеріал з теми системи контролю версій Git, а саме: ознайомився з основами створення репозиторія, збереження та маркування змін у файлах, створення гілок, відкат змін та публікацією проєктів у GitHub.

Отриманні знання та навички являють собою основу при розробці програмних систем, безпечної спільної праці у команді над проєктом, яка дозволяє зберігати зміни у проєкті на кожному визначеному етапі будування системи.