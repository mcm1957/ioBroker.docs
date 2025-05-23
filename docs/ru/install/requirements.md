---
title: Требования
lastChanged: 29.05.2024
translatedFrom: de
translatedWarning: Если вы хотите отредактировать этот документ, удалите поле «translationFrom», в противном случае этот документ будет снова автоматически переведен
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/ru/install/requirements.md
hash: HYGYFDXyh3VUuWCaHunNw9O/MK74H6CZJqQPqqYQ7Wg=
---
## Системные требования
| Операционная система | Варианты | Аппаратная среда (например) | Минимальные требования для ioBroker | Рекомендуемые ресурсы для ioBroker (2)

| --------- | --------- | --------- | --------- | --------- |
| [Дистрибутивы Linux](./#de/documentation/install/linux.md) | Рекомендация: Debian, включая соответствующие производные (1) | Raspberry PI, одноплановый компьютер, мини-ПК (например, NUC), оборудование со средой виртуализации | 2 ГБ ОЗУ, 32 ГБ встроенной памяти | >= 4 ГБ (лучше 6–8 ГБ) ОЗУ, >= емкость встроенной памяти 64 ГБ | [докер](./#de/documentation/install/docker.md) | | Мини-ПК (например, NUC), NAS (3) | 2 ГБ ОЗУ, 32 ГБ встроенной памяти | >= 4 ГБ (лучше 6–8 ГБ) ОЗУ, >= емкость встроенной памяти 64 ГБ | [Окна](./#de/documentation/windows.md) | | ПК, мини-ПК (например, NUC)| 4 ГБ ОЗУ, 50 ГБ встроенной памяти (включая ОС) | 8 ГБ ОЗУ, 100 ГБ встроенной памяти (включая ОС) |

(1) Рекомендуется установить ioBroker в дистрибутив Linux на базе Debian/Ubuntu (серверная версия без рабочего стола!). Установка в другом дистрибутиве Linux, как правило, возможна (при условии, что поддерживается действующая версия Node.js), но требует экспертных знаний, поскольку стандартные сценарии установки/обслуживания и инструкции адаптированы для Debian.

(2) Эти значения основаны на опыте типичной средней установки системы ioBroker с ~40 активными адаптерами, Grafana и внешней базой данных.

 (3) Для установки на NAS применяются требования Docker, а также дополнительные ресурсы для собственных задач NAS.

### В целом
- ioBroker можно установить на все системы, где доступен Node.js.
- Требуемая оперативная память и емкость хранилища увеличиваются, если, например, точки данных сохраняются в истории (например, с помощью адаптера истории, который хранит текстовые файлы в системе) или если дополнительно установлены и работают на этом базы данных, такие как Influx или MySQL, или другие приложения. система
- При выборе оборудования обратите внимание на энергопотребление оборудования, так как ioBroker будет работать круглосуточно (работа 24/7). Разница всего в несколько ватт становится заметна в потреблении электроэнергии в течение года.