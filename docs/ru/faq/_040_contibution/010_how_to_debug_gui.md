---
translatedFrom: de
translatedWarning: Если вы хотите отредактировать этот документ, удалите поле «translationFrom», в противном случае этот документ будет снова автоматически переведен
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/ru/faq/_040_contibution/010_how_to_debug_gui.md
title: без заголовка
hash: eh141K6ZgUBSAOs1s5Ypj/mn6GJoohoZ3t/LHHuvcd0=
---
## Сообщать об ошибках в графическом интерфейсе пользователя
ioBroker имеет множество графических интерфейсов, написанных на JavaScript.

Многие интерфейсы в настоящее время разрабатываются с помощью ReactJS.
Если в таком интерфейсе возникает ошибка, или реакция зависает, или сайт ведет себя непредвиденно, то можно и нужно сообщить об ошибке.

Для этого вам нужно открыть консоль браузера и найти там сообщения об ошибках.
Консоль браузера отличается в каждом браузере, но в большинстве браузеров консоль находится в режиме разработчика, а режим разработчика обычно доступен по нажатию F12 (Chrome, Firefox, Edge).

Важно **сначала открыть консоль браузера, затем перезагрузить страницу (F5)*, а затем выполнить действия, вызвавшие ошибку.

Вот как выглядит консоль браузера в Chrome: ![Консоль браузера в Chrome](../../../de/faq/_040_contibution/media/010_browser_console.png)

Вот как выглядит сообщение об ошибке, если консоль открывается после загрузки страницы: ![Ошибки без источников](../../../de/faq/_040_contibution/media/010_browser_without_sources.png)

И вот так, если консоль открывается до загрузки страницы: ![Ошибки с источниками](../../../de/faq/_040_contibution/media/010_browser_with_sources.png)

Как вы могли заметить, он показывает имя файла и номер строки, в которой возникает ошибка.

С помощью этой информации (вместе с номером версии адаптера) мы можем воспроизвести или исправить ошибку.