# Як створити *Єдині новини*?
## Зміст
- [Blog post workflow](#blog-post-workflow)
- [RSS](#rss)
***
## Blog post workflow
1. [Blog post workflow](https://github.com/gautamkrishnar/blog-post-workflow) — репозиторій розповідає, як налаштувати виведення останніх постів із блогів чи соціальних спільнот у md-файл. Автор репозиторію має докладні інструкції з інтеграції з Dev.to, Medium, Stackoverflow, Reddit, YouTube та іншими популярними платформами. Але можна скористатися RSS-посиланням та виводити останні пости зі свого блогу. У цій статті розглянемо інструкцію про те, як виводити пости з "Фактами" у свій профіль GitHub. По-перше, у нас вже має бути створений md-файл профілю. По-друге, треба відкрити цей файл і в необхідному місці вставити наступну конструкцію:
```markdown
<!-- BLOG-POST-LIST:START -->
<!-- BLOG-POST-LIST:END -->
```
2. Потім у корені репозиторію треба створити папку  `.github` у ній папку  workflows, а ній файл  `blog-post-workflow.yml`. Повний шлях має виглядати так:  `username/.github/workflows/blog-post-workflow.yml`.
3. Тепер переходимо до створеного yml-файлу і вставляємо наступне, замінюючи посилання в поле  feed-list: на ваше RSS-посилання (можна скопіювати у профілі "Факти" в розділі «Публікації»):
```yaml
name: Latest blog post workflow
on:
  schedule: # Run workflow automatically
    - cron: '0 * * * *' # Runs every hour, on the hour
  workflow_dispatch: # Run workflow manually (without waiting for the cron to be called), through the GitHub Actions Workflow page directly
permissions:
  contents: write # To write the generated contents to the readme

jobs:
  update-readme-with-blog:
    name: Update this repo's README with latest blog posts
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Pull in dev.to posts
        uses: gautamkrishnar/blog-post-workflow@v1
        with:
          feed_list: "https://fakty.ua/rss_feed/ukraine,https://fakty.ua/rss_feed/show-business"
```
***
## RSS
*RSS* — це родина XML-форматів, що використовується для публікації та постачання інформації, що часто змінюється, наприклад, нових записів в блозі, заголовків новин, анонсів статей, зображень, аудіо і відео матеріалів (в стандартизованому форматі). Документ в стандарті RSS (який також інколи називають «стрічкою», «вебстрічкою» або «каналом») складається з повного або часткового тексту і метаданих (дата і авторство).
