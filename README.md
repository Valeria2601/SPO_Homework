[![icon](/data/pixmaps/idbutton.png?raw=true)](https://www.darktable.org/) darktable 
=========

darktable - это приложение для работы с фотографиями с открытым исходным кодом и недеструктивный проявитель сырых изображений - виртуальный световой стол и темная комната для фотографов. Оно хранит ваши цифровые негативы в базе данных, позволяет просматривать их с помощью светового стола с возможностью масштабирования и позволяет обрабатывать необработанные изображения, улучшать их и экспортировать в локальное или удаленное хранилище.

![screenshot_lighttable](https://user-images.githubusercontent.com/45535283/148689197-e53dd75f-32f1-4297-9a0f-a9547fd4e7c7.jpg)

darktable **не** является заменой бесплатной программы Adobe® Lightroom®.

[https://www.darktable.org/](https://www.darktable.org/ "darktable homepage")

## Содержание

1. [Документация](#документация)
2. [Требования](#требования)
   - [Поддерживаемые платформыы](#поддерживаемые-платформы)
   - [Системные требования](#системные-требования)
3. [Установка](#установка)
   - [Последний выпуск](#последний-выпуск)
   - [Версии в разработке](#версии-в-разработке)
4. [Обновление с предыдущих версий](#обновление-с-предыдущих-версий)
5. [Расширения](#расширения)
6. [Сборка](#сборка)
   - [Зависимости](#зависимости)
   - [Исходные файлы](#исходные-файлы)
   - [Подмодули](#подмодули)
   - [Компиляция](#компиляция)
7. [Использование](#использование)
   - [Тестовая/нестабильная версия](#тестоваянестабильная-версия)
   - [Действующая/стабильная версия](#действующаястабильная-версия)
8. [Wiki](#wiki)

Документация
-------------

Руководство пользователя можно найти в репозитории [dtdocs](https://github.com/darktable-org/dtdocs).

Документация Lua API поддерживается в репозитории [luadocs](https://github.com/darktable-org/luadocs).

Требования
------------

### Поддерживаемые платформы

* Linux
* FreeBSD
* NetBSD
* OpenBSD
* Windows 8.1 с [UCRT](https://support.microsoft.com/en-us/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c) и новее
* macOS 13.5 и новее

*Big-endian платформы не поддерживаются.*

*32-битные платформы не имеют официальной поддержки.*

*И darktable, и используемые им библиотеки разработаны на платформе Linux.
Поэтому на других платформах МОЖНО найти дополнительные ошибки, которых нет в версии для Linux.
Кроме того, например, на платформе Windows в настоящее время не реализована поддержка печати.
Поэтому мы рекомендуем, если у вас есть выбор платформы, использовать darktable на Linux.*

### Системные требования

(минимальные / **рекомендуемые**):
* RAM: 4 ГБ / **8 ГБ**
* CPU: Intel Pentium 4 (Core 2 for Windows) / **Intel Core i5 4×2.4 ГГц**
* GPU: none / **Nvidia with 1024 CUDA cores, 4 GB, OpenCL 1.2 compatible**
* Свободное место: 250 МБ / **1 ГБ**

*darktable может работать на легких конфигурациях (даже на Raspberry Pi), но ожидайте, что такие модули, как denoise, local contrast,
contrast equalizer, retouch или liquify будут медленными и непригодными для использования.*

*Наличие GPU не является обязательным, но настоятельно рекомендуется для более плавной работы.
Графические процессоры Nvidia рекомендуются для обеспечения безопасности, поскольку некоторые драйверы AMD ведут себя ненадежно с некоторыми модулями (например, local contrast).*

Установка
----------

Если последний выпуск все еще не доступен в виде предварительно собранного пакета для вашего дистрибутива,
вы можете собрать программное обеспечение самостоятельно, следуя инструкциям [ниже](#сборка).

### Последний выпуск

4.8.1 (stable)

* [Загрузить исполняемый файл для Windows](https://github.com/darktable-org/darktable/releases/download/release-4.8.1/darktable-4.8.1-win64.exe)
* [Загрузить исполняемый файл для macOS на Intel](https://github.com/darktable-org/darktable/releases/download/release-4.8.1/darktable-4.8.1-x86_64.dmg)
* [Загрузить исполняемый файл для macOS на Apple Silicon](https://github.com/darktable-org/darktable/releases/download/release-4.8.1/darktable-4.8.1-arm64.dmg)
* [Загрузить исполняемый файл для macOS 13.5 на Apple Silicon](https://github.com/darktable-org/darktable/releases/download/release-4.8.1/darktable-4.8.1-arm64-13.5.dmg)
* [Загрузить AppImage для Linux](https://github.com/darktable-org/darktable/releases/download/release-4.8.1/darktable-4.8.1-x86_64.AppImage)
* [Дополнительная информация об установке darktable на любой платформе](https://www.darktable.org/install/)

*При использовании предварительно собранного пакета убедитесь, что он содержит поддержку Lua, OpenCL, OpenMP и Colord.
Эти параметры являются необязательными и не помешают запуску darktable, если они отсутствуют,
но их отсутствие ухудшит пользовательский опыт.
Вы можете проверить их наличие, запустив darktable с опцией командной строки `--version`.*

### Версии в разработке

Версии в разработке отражают текущее состояние ветки `master`. Они предназначны для тестирования и, как правило, небезопасны. Смотрите пункт [ниже](#исходные-файлы) для предупреждений о работе с веткой `master`.

* [Бинарные пакеты предоставляются для Linux (AppImage), macOS и Windows каждую ночь.](https://github.com/darktable-org/darktable/releases/tag/nightly)

Обновление с предыдущих версий
----------------------------

При обновлении darktable с более старой версии достаточно установить
новейшую версию. Существующие файлы будут сохранены.

Однако в новых версиях иногда требуется изменить структуру базы данных библиотеки
(содержащей весь список изображений, известных darktable, с историей их редактирования). Если это произойдет
вам будет предложено либо обновить базу данных, либо закрыть программу.

**Переход на новую структуру базы данных/новый релиз означает, что ваши правки (как новые, так и старые)
больше не будут совместимы со старыми версиями darktable.** Обновления являются окончательными.
Новые версии всегда совместимы со старыми версиями, но новые версии обычно
не совместимы со старыми версиями.

darktable автоматически создает резервную копию базы данных библиотеки, когда новая версия вызывает ее обновление
(например, в `~/.config/darktable/library.db-pre-3.0.0`), так что
при необходимости вы можете вернуться к предыдущему выпуску, восстановив эту резервную копию
(просто переименуйте ее в `library.db`).

Вы не сможете открыть новую версию базы данных с помощью версии darktable
которая поддерживает только старую версию базы данных. Это невозможно, потому что старое
приложение не знает, как изменилась схема базы данных, поэтому его код не сможет
работать с ней.

Вы сможете импортировать изображения с файлом XMP sidecar, содержащим более новые версии модулей обработки
или новые модули, но при этом части редактирования изображений будут отброшены, и вы их потеряете.

Если вы планируете регулярно переключаться между двумя версиями, то смотрите детали [ниже](#testunstable-version)
о том как делать это безопасно.

Расширения
--------------------

Расширения и плагины используют язык сценариев Lua и могут быть загружены [здесь](https://github.com/darktable-org/lua-scripts). Поддержка Lua в darktable является опциональной, поэтому убедитесь, что у вас установлен интерпретатор `lua` и файлы его разработки (пакет
`lua-dev` или `lua-devel`, в зависимости от дистрибутива) установлены в вашей системе
при сборке или убедитесь, что используемый вами пакет был собран с этой библиотекой.

Расширения позволяют экспортировать снимки для различных носителей и веб-сайтов, объединять/складывать/смешивать HDR, панорамы или брекетинг фокуса,
применять распознавание лиц на основе искусственного интеллекта, управлять тегами и данными GPS и т. д.

Сборка
--------

### Зависимости

Совместимые компиляторы:
* Clang: 15 и новее
* GCC: 12 и новее
* MinGW-w64: 10 и новее
* XCode: 15.2 и новее

Требуемые зависимости (минимальные версии):
* CMake 3.18
* GTK 3.24.15
* GLib 2.56
* SQLite 3.26
* libcurl 7.56
* Exiv2 0.27.2 *(но, по крайней мере, 0.27.4 с поддержкой ISO BMFF, необходимой для сырого импорта Canon CR3)*
* pugixml 1.5

Требуемые зависимости (без привязки к версии):
* Lensfun *(для автоматической корректировки линз)* (Примечание: alpha 0.3.95 и git master ветки не поддерживаются)
* Little CMS 2

Опциональные зависимости (минимальные версии):
* OpenMP 4.5 *(для многопоточности процессора и векторизации SIMD)*
* LLVM 7 *(для проверки OpenCL во время компиляции)*
* OpenCL 1.2 *(для вычислений с GPU-ускорением)*
* Lua 5.4 *(для скриптов плагинов и расширений)*
* G'MIC 2.7.0 *(для поддержки сжатых LUT-файлов .gmz)*
* libgphoto2 2.5 *(для привязки камеры)*
* Imath 3.1.0 *(для экспорта и ускорения импорта 16-битных TIFF с «половинным» плаванием)*
* libavif 0.9.3 *(для импорта и экспорта AVIF)*
* libheif 1.13.0 *(для импорта HEIF/HEIC/HIF; также для импорта AVIF, если нет libavif)*
* libjxl 0.7.0 *(для импорта и экспорта JPEG XL)*
* WebP 0.3.0 *(для импорта и экспорта WebP)*

Опциональные зависимости (без привязки к версии):
* colord, Xatom *(для получения цветового профиля дисплея системы)*
* PortMidi *(для поддержки MIDI-ввода)*
* SDL2 *(для поддержки ввода с геймпада)*
* CUPS *(для поддержки режима печати)*
* OpenEXR *(для импорта и экспорта EXR)*
* OpenJPEG *(для импорта и экспорта JPEG 2000)*
* GraphicsMagick или ImageMagick *(для импорта изображений в разных форматах)*

Для установки всех зависимостей на Linux-системах вы можете воспользоваться исходными репозиториями вашего дистрибутива
(при условии, что они актуальны):

#### Fedora и RHEL/CentOS

```bash
sudo dnf builddep darktable
```

#### OpenSuse

```bash
sudo zypper si -d darktable
```

#### Ubuntu

```bash
sed -e '/^#\sdeb-src /s/^# *//;t;d' "/etc/apt/sources.list" \
  | sudo tee /etc/apt/sources.list.d/darktable-sources-tmp.list > /dev/null \
  && (
    sudo apt-get update
    sudo apt-get build-dep darktable
  )
sudo rm /etc/apt/sources.list.d/darktable-sources-tmp.list
```

#### Debian

```bash
sudo apt-get build-dep darktable
```

### Исходные файлы

#### Ветка master (нестабильная)

Мастер-ветка содержит последнюю версию исходного кода и предназначена:
* в качестве рабочей базы для разработчиков,
* для бета-тестеров для поиска ошибок,
* для пользователей, готовых пожертвовать стабильностью ради новых возможностей, не дожидаясь следующего релиза.

Мастер-ветка не дает никаких гарантий стабильности и может повредить вашу базу данных и файлы XMP,
привести к потере данных и истории правок или временно нарушить совместимость с предыдущими версиями и коммитами.

Насколько это опасно? В большинстве случаев он достаточно стабилен. Как и при любом другом типе развертывания, ошибки появляются чаще,
но и исправляются быстрее. Иногда, однако, эти ошибки могут приводить к потерям или несоответствиям в истории редактирования ваших фотографий.
Это нормально, если вам не нужно открывать свои правки в будущем.

После создания резервной копии каталога `~/.config/darktable` и файлов sidecar .XMP всех фотографий, которые вы собираетесь открыть
с помощью мастер-ветки, вы можете получить исходный код следующим образом:

```bash
git clone --recurse-submodules --depth 1 https://github.com/darktable-org/darktable.git
cd darktable
```

Смотрите ниже (в "Использование") как начать тестовую установку нестабильной версии без вреда для программы и файлов стабильной версии.

#### Последний стабильный выпуск

4.8.1

Проект darktable выпускает две основные версии каждый год, в дни летнего и зимнего солнцестояний, помеченные четными цифрами (например, 4.2, 4.4, 4.6, 4.8).
Минорные версии помечаются третьей цифрой (например, 4.4.1, 4.4.2) и в основном содержат исправления ошибок и поддержку камер.
Вы можете самостоятельно скомпилировать эти стабильные версии, чтобы получить лучшую производительность для вашего конкретного компьютера:

```bash
git clone --recurse-submodules --depth 1 https://github.com/darktable-org/darktable.git
cd darktable
git fetch --tags
git checkout tags/release-4.8.1
```

### Подмодули

Обратите внимание, что [libxcf](https://github.com/houz/libxcf.git), [OpenCL](https://github.com/KhronosGroup/OpenCL-Headers.git), [RawSpeed](https://github.com/darktable-org/rawspeed), [whereami](https://github.com/gpakosz/whereami) и [LibRaw](https://github.com/LibRaw/LibRaw) отслеживаются через git-подмодули, поэтому после проверки darktable вам необходимо обновить/проверить и подмодули.:

```bash
git submodule update --init
```

### Компиляция

#### Лёгкий способ

ВНИМАНИЕ: Если вы уже собирали darktable, не забудьте предварительно полностью удалить (`rm -R`) директории `build`
и директории `/opt/darktable`, чтобы избежать конфликтов файлов из разных версий. Сообщается о многих странных поведениях и временных
было зарегистрировано множество странных поведений и временных ошибок, которые могут быть связаны с тем, что кэш сборки не может должным образом аннулировать измененные зависимости, поэтому
наиболее безопасным способом является полное удаление ранее собранных двоичных файлов и начало работы с нуля.

darktable предоставляет shell-скрипт, который автоматически позаботится о сборке в Linux и macOS для классических случаев одной командой.

```bash
./build.sh --prefix /opt/darktable --build-type Release --install --sudo
```

Если вы хотите установить тестовую версию наряду с действующей/стабильной, измените префикс установки:

```bash
./build.sh --prefix /opt/darktable-test --build-type Release --install --sudo
```

Это создает программное обеспечение только для вашей архитектуры, с:

* `-O3` уровнем оптимизации,
* поддержкой SSE/AVX, если она обнаружена,
* Поддержка OpenMP (многопоточность и векторизация), если обнаружена,
* Поддержка OpenCL (разгрузка GPU), если обнаружена,
* поддержка сценариев Lua, если обнаружена.

Если вы хотите, чтобы dartkable отображался вместе с другими вашими приложениями, достаточно добавить символическую ссылку:

```bash
ln -s /opt/darktable/share/applications/org.darktable.darktable.desktop /usr/share/applications/org.darktable.darktable.desktop
```

Теперь ваш личный darktable готов к использованию, как и любое другое готовое программное обеспечение.

#### Ручной способ

Кроме того, вы можете использовать ручную сборку для передачи пользовательских аргументов.

##### Linux

```bash
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=/opt/darktable/ ..
cmake --build .
sudo cmake --install .
```

##### macOS

Смотрите инструкции [Homebrew](https://github.com/darktable-org/darktable/blob/master/packaging/macosx/BUILD_hb.txt) или [MacPorts](https://github.com/darktable-org/darktable/blob/master/packaging/macosx/BUILD.txt).

##### Windows

Инструкции можно найти [здесь](https://github.com/darktable-org/darktable/tree/master/packaging/windows).

### Использование

#### Тестовая/нестабильная версия

Чтобы использовать тестовую версию darktable, не повредив файлы и базу данных обычной/стабильной версии, запустите darktable в терминале с помощью команды:

```bash
/opt/darktable-test/bin/darktable --configdir "~/.config/darktable-test"
```

и убедитесь, что вы установили опцию «создавать XMP-файлы» на «никогда» в настройках -> хранилище -> XMP sidecar files. Таким образом,
ваша действующая/стабильная версия будет сохранять свои конфигурационные файлы в `~/.config/darktable`, как обычно,
тестовая/нестабильная будет сохранять в `~/.config/darktable-test`, и обе версии не будут создавать конфликтов баз данных.

#### Действующая/стабильная версия

Просто запустите его из меню приложений рабочего стола или из терминала, запустив `darktable` или `/opt/darktable/bin/darktable`. Если при установке не была создана программа запуска в меню приложений, выполните команду:

```bash
sudo ln -s /opt/darktable/share/applications/org.darktable.darktable.desktop /usr/share/applications/org.darktable.darktable.desktop
```

Конфигурационные файлы darktable можно найти в папке `~/.config/darktable`.
Если при запуске происходят сбои, попробуйте запустить darktable из терминала с отключенным OpenCL с помощью `darktable --disable-opencl`.

Wiki
----

* [GitHub wiki](https://github.com/darktable-org/darktable/wiki "github wiki")
* [Developer wiki](https://github.com/darktable-org/darktable/wiki/Developer's-guide "darktable developer wiki")

