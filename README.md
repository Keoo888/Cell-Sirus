<p align="center">
  <img src="https://github.com/user-attachments/assets/cadce527-ec65-4ee6-9579-c47ca7cfcca1" alt="Cell" width="120">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Cell-r277-ff8800?style=for-the-badge&logo=appveyor">
  <img src="https://img.shields.io/badge/WotLK-3.3.5a-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/сервер-Sirus-9b59b6?style=for-the-badge">
</p>

<h1 align="center">Cell — Sirus build</h1>

<p align="center">
  <b>Clean raid frame addon with customizable frames for World of Warcraft 3.3.5a (WotLK).</b><br>
  <i>Backport of Cell r277 to the 3.3.5a client, built for the Sirus server.</i>
</p>

<p align="center">
  <a href="#english">English</a> ·
  <a href="#russian">Русский</a>
</p>

---

<a name="english"></a>
## English

<p align="center">
  <a href="#sirus">What's different for Sirus</a> ·
  <a href="#features">Features</a> ·
  <a href="#commands">Commands</a> ·
  <a href="#installation">Installation</a> ·
  <a href="#license">License</a> ·
  <a href="#credits">Credits</a>
</p>

### About

**Cell** is a clean, powerful raid frame addon inspired by CompactRaid, Grid2,
Aptechka, and VuhDo: solo/party/raid frames, aura indicators, click-castings,
raid debuffs tracking, spell request utilities, and more. This repository is a
**backport of Cell r277** to the **WoW 3.3.5a (WotLK)** client.

<img width="178" height="299" alt="party" src="https://github.com/user-attachments/assets/396180df-9d33-483b-8eae-41d09efab515" />

<a name="sirus"></a>
### What's different for Sirus

This is a separate branch of the [Cell 3.3.5a backport](https://github.com/Keoo888/Cell-3.3.5-backport).
Everything in the main build is here; on top of it are two Sirus-specific changes.

#### Shield amount is exact

On a stock 3.3.5a client the server cannot report the size of an absorb, so Cell sums
shields itself from the combat log using a list of eight known WotLK spells. Sirus reports
the number directly, including **custom server shields** that are not in that list and
cannot be.

The shield bar now reads the value from the client. It shows absorbs that the standard
build cannot see at all (for example, custom server shields), and the number is the real
one, not an estimate. The separate "Power Word: Shield" indicator still uses the combat
log — the size of a single spell cannot be learned any other way.

#### Server service auras are hidden

Sirus applies permanent debuffs to every player that encode account data: PvE category,
VIP tier, premium, zodiac sign, faction override. They never expire, so in a raid they
would occupy debuff icons all evening and push out real boss mechanics; an aura with a
dispel type would also keep the frame highlighted as "needs dispel".

These auras are now hidden on frames and do not trigger dispel highlights. Three details:

- **Your own debuff blacklist is untouched.** Service auras are kept separately and do
  not appear in the settings — only what you added yourself remains there.
- **The list comes from the client.** A new tier or category added by the server is
  filtered without an addon update.
- **Buffs are unaffected.** Cell does not show "all buffs in a row" — every indicator
  asks about a specific spell, so there is nothing to filter there.

#### If something is wrong

The base is a tested backport; both changes above were written against the Sirus client
and its addons. If a frame looks wrong, open an
[issue](https://github.com/Keoo888/Cell-Sirus/issues) and attach the output of
`/cell debug dump`.

<a name="features"></a>
### Features

#### Layouts

<img width="470" height="441" alt="layout" src="https://github.com/user-attachments/assets/507fd502-ef18-4d37-9c0e-b1dd5d5a1575" />

Fully customizable party and raid frames — size, position, orientation, group
arrangement, and power bars. Auto-switch layouts by spec/role with independent
settings for solo, party, raid, arena, and battleground.

#### Appearance

<img width="470" height="491" alt="appearance" src="https://github.com/user-attachments/assets/1a662292-ca2c-48a9-9e56-a2315507b3d3" />

Textures, colors, alphas, and fonts are all in your hands. Health color by
class or by percentage, customizable background, out-of-range dimming, and full
control over the look of every frame.

#### Indicators

<img width="480" height="441" alt="indicators" src="https://github.com/user-attachments/assets/9c1273be-dc68-40f8-ae17-b53245a5509a" />

Dozens of built-in indicators (health text, aggro bar, shield bar, heal
prediction, dispels, raid icons, and more) plus unlimited custom indicators for
any buff or debuff — icons, bars, rects, texts, colors, and glows.

#### Click-Castings

<img width="399" height="441" alt="click-castings" src="https://github.com/user-attachments/assets/4d7b33d5-f2f2-4666-a5c7-388cef15a672" />

Bind spells, macros, and items directly to mouse clicks on unit frames —
mouseover healing without target switching. Supports keyboard and multi-button
mice, with per-class and per-spec binding profiles.

#### Raid Debuffs

<img width="470" height="441" alt="raiddebuffs" src="https://github.com/user-attachments/assets/dea8a922-1be3-4ddb-890b-03eeba76d6c8" />

Track boss abilities and dangerous debuffs in dungeons and raids with
prioritized, per-instance debuff lists and glow effects. Ships with data for
Classic, TBC, and WotLK instances, fully editable in-game — add a debuff by
spell ID or by name, and the backport finds every matching ID for you.

#### Utilities

Useful raid tools: ready check, countdown, spell/dispel requests, buff tracker,
death report, raid roster window, marks bar, and hiding of default Blizzard
party/raid frames.

#### Spotlight Frame

Extra 15 unit buttons that can be set to Target, Focus, Unit, Tank, and more —
keep the most important units always in sight.

<a name="commands"></a>
### Commands

- `/cell` — show all available commands.
- `/cell opt` — open the options window.
- `/cell unlock`, `/cell lock`, `/cell mover` — show or hide the movers for the marks bar, buff tracker and ready/check buttons (added in the backport; the options button is unavailable in combat).
- `/cell minimap` — show or hide the minimap button (added in the backport; middle-click hides it, and only this command brings it back).
- `/cell healers` — create a "Healers" indicator.
- `/cell rescale` — apply the recommended scale for your resolution.
- `/cell report 0-40` — how many deaths to report per raid fight (`0` — all).
- `/cell reset position`, `layouts`, `clickcastings`, `raiddebuffs`, `snippets`, `all` — reset the matching settings for **every character on the account**.
- `/cell debug dump` — open a diagnostics window whose text can be copied into a bug report (added in the backport).
- `/cell debug h` — list all diagnostic subcommands (added in the backport).
- `/cell debug shims` — show which compatibility globals are owned by other addons (added in the backport).

<a name="installation"></a>
### Installation

1. Download the latest release (or clone this repository).
2. Extract the archive.
3. Move the **Cell** folder into:
   ```
   \Interface\AddOns\
   ```
4. Enable it on the character-select AddOns screen and launch the game. Type `/cell` to open options.

### Compatibility

- Built for **Sirus** on the WoW 3.3.5a client (Interface `30300`).
- For **Warmane** and other servers use the [main Cell backport](https://github.com/Keoo888/Cell-3.3.5-backport); the changes above rely on behaviour a stock 3.3.5a client does not have.
- The addon version is `r277-release`, the same as the main build: both come from one base.
- Coexists with other API backport addons (a standalone `!!!ClassicAPI` and the like): Cell never overwrites globals it does not own. Run `/cell debug shims` to see which addon owns what on your client.

<a name="license"></a>
### License

Cell is distributed under the original Cell license: **All Rights Reserved**;
modifications are permitted for private use only, and the addon name and folder
may not be changed. See [LICENSE.txt](LICENSE.txt). Public redistribution of a
modified build requires the author's explicit permission.

<a name="credits"></a>
### Credits

- Original addon: [enderneko/Cell](https://github.com/enderneko/Cell) — A World of Warcraft raid frame addon
- WotLK 3.3.5a backport: **Keoo**
- Sirus build: **Keoo**
- Discord: https://discord.gg/sKpJbUrsvR

---

<a name="russian"></a>
## Русский

<p align="center">
  <a href="#для-sirus">Что изменено для Sirus</a> ·
  <a href="#возможности">Возможности</a> ·
  <a href="#команды">Команды</a> ·
  <a href="#установка">Установка</a> ·
  <a href="#лицензия">Лицензия</a> ·
  <a href="#благодарности">Благодарности</a>
</p>

### Об аддоне

**Cell** — это аккуратный и мощный аддон рейдовых рамок, вдохновлённый
CompactRaid, Grid2, Aptechka и VuhDo: рамки соло/группы/рейда, индикаторы аур,
клик-касты, отслеживание рейдовых дебаффов, запросы заклинаний и многое другое.
Этот репозиторий — **бэкпорт Cell r277** под клиент **WoW 3.3.5a (WotLK)**.

<img width="178" height="299" alt="party" src="https://github.com/user-attachments/assets/396180df-9d33-483b-8eae-41d09efab515" />

<a name="для-sirus"></a>
### Что изменено для Sirus

Это отдельная ветка [бэкпорта Cell под 3.3.5a](https://github.com/Keoo888/Cell-3.3.5-backport).
Всё, что есть в основной сборке, есть и здесь; сверх того — две правки под этот сервер.

#### Щит на рамке считается точно

На обычном клиенте 3.3.5a сервер не умеет сообщать величину поглощения, поэтому Cell
складывает щиты сам, по боевому логу, по списку из восьми известных вотлковских заклинаний.
Sirus так умеет — и отдаёт готовое число, включая **собственные щиты сервера**, которых в
том списке нет и быть не может.

Полоса щита теперь берёт величину прямо у клиента. На рамке видно поглощение, которого в
обычной сборке не видно вовсе (например от кастомных серверных щитов), и число совпадает с
настоящим, а не с оценкой. Отдельный индикатор «Слово силы: Щит» по-прежнему считает по
боевому логу — величину **одного** заклинания никаким другим способом не узнать.

#### Служебные ауры сервера убраны с рамок

Sirus вешает на каждого игрока постоянные дебаффы, которыми кодирует данные аккаунта:
PvE-категорию, тир VIP, премиум, знак зодиака, подмену фракции. Они не истекают — то есть в
рейде занимали бы иконки дебаффов весь вечер и выталкивали бы настоящие боссовые механики, а
аура с типом рассеивания вдобавок держала бы рамку подсвеченной «нужно снять».

Теперь такие ауры на рамках не показываются и подсветку снятия не зажигают. Три уточнения:

- **Ваш собственный чёрный список дебаффов не тронут.** Служебные ауры живут отдельно и в
  настройках не появляются — там остаётся только то, что вы добавили сами.
- **Список берётся из самого клиента.** Новый тир или новая категория, добавленные сервером,
  отфильтруются без обновления аддона.
- **Баффы не затронуты.** Cell не показывает «все баффы подряд» — каждый индикатор спрашивает
  про конкретное заклинание, поэтому фильтровать там нечего.

#### Если что-то не так

Сама основа — обкатанный бэкпорт; обе правки выше написаны по клиенту Sirus и по его аддонам.
Заметили странность на рамках — заводите
[issue](https://github.com/Keoo888/Cell-Sirus/issues), и приложите вывод `/cell debug dump`.

<a name="возможности"></a>
### Возможности

#### Макеты (Layouts)

<img width="470" height="441" alt="layout" src="https://github.com/user-attachments/assets/507fd502-ef18-4d37-9c0e-b1dd5d5a1575" />

Полностью настраиваемые рамки группы и рейда — размер, позиция, ориентация,
расположение групп и полосы ресурсов. Автопереключение макетов по спеку/роли с
независимыми настройками для соло, группы, рейда, арены и поля боя.

#### Внешний вид (Appearance)

<img width="470" height="491" alt="appearance" src="https://github.com/user-attachments/assets/1a662292-ca2c-48a9-9e56-a2315507b3d3" />

Текстуры, цвета, прозрачность и шрифты — всё в ваших руках. Цвет здоровья по
классу или по проценту, настраиваемый фон, затемнение вне дистанции и полный
контроль над видом каждой рамки.

#### Индикаторы (Indicators)

<img width="480" height="441" alt="indicators" src="https://github.com/user-attachments/assets/9c1273be-dc68-40f8-ae17-b53245a5509a" />

Десятки встроенных индикаторов (текст здоровья, полоса агро, полоса щита,
предсказание лечения, диспелы, рейдовые метки и др.) плюс неограниченные
пользовательские индикаторы для любых баффов и дебаффов — иконки, полосы,
прямоугольники, тексты, цвета и свечения.

#### Клик-касты (Click-Castings)

<img width="399" height="441" alt="click-castings" src="https://github.com/user-attachments/assets/4d7b33d5-f2f2-4666-a5c7-388cef15a672" />

Привязывайте заклинания, макросы и предметы напрямую к кликам мыши по рамкам —
лечение по наведению без смены цели. Поддержка клавиатуры и многокнопочных
мышей, профили привязок для каждого класса и спека.

#### Рейдовые дебаффы (Raid Debuffs)

<img width="470" height="441" alt="raiddebuffs" src="https://github.com/user-attachments/assets/dea8a922-1be3-4ddb-890b-03eeba76d6c8" />

Отслеживайте способности боссов и опасные дебаффы в подземельях и рейдах с
приоритетными списками по каждой локации и эффектами свечения. В комплекте
данные для Classic, TBC и WotLK, полностью редактируемые прямо в игре — дебафф
добавляется по ID заклинания или по названию, бэкпорт сам найдёт все
подходящие ID.

#### Утилиты (Utilities)

Полезные рейдовые инструменты: проверка готовности, отсчёт, запросы
заклинаний/диспела, трекер баффов, отчёт о смерти, окно состава рейда, панель
меток и скрытие стандартных рамок Blizzard.

#### Рамка Spotlight

Дополнительные 15 кнопок юнитов, которые можно настроить на Цель, Фокус, Юнита,
Танка и другое — держите самых важных юнитов всегда на виду.

<a name="команды"></a>
### Команды (Slash Commands)

Введите `/cell` для дополнительной информации.

- `/cell` — показать все доступные команды.
- `/cell opt` — открыть окно настроек.
- `/cell unlock`, `/cell lock`, `/cell mover` — показать или скрыть мувер-рамки панели меток, трекера баффов и кнопок готовности/отсчёта (добавлено в бэкпорте — кнопка в настройках в бою недоступна).
- `/cell minimap` — показать или скрыть кнопку у миникарты (добавлено в бэкпорте — щелчок средней кнопкой по ней прячет её, и вернуть можно только этой командой).
- `/cell healers` — создать индикатор «Healers».
- `/cell rescale` — применить рекомендованный масштаб под ваше разрешение.
- `/cell report 0-40` — сколько смертей сообщать за бой в рейде (`0` — все).
- `/cell reset position`, `layouts`, `clickcastings`, `raiddebuffs`, `snippets`, `all` — сбросить соответствующие настройки у **всех персонажей аккаунта**.
- `/cell debug dump` — открыть окно с диагностикой, которую можно скопировать и вставить в баг-репорт (добавлено в бэкпорте).
- `/cell debug h` — список всех диагностических подкоманд (добавлено в бэкпорте).
- `/cell debug shims` — показать, какие глобалы совместимости заняты другими аддонами (добавлено в бэкпорте).

<a name="установка"></a>
### Установка

1. Скачайте последний релиз (или клонируйте репозиторий).
2. Распакуйте архив.
3. Переместите папку **Cell** в:
   ```
   \Interface\AddOns\
   ```
4. Включите аддон на экране выбора персонажа и запустите игру. Введите `/cell`, чтобы открыть настройки.

### Совместимость

- Собрано под **Sirus** на клиенте WoW 3.3.5a (Interface `30300`).
- Для **Warmane** и других серверов берите [основную сборку](https://github.com/Keoo888/Cell-3.3.5-backport) — правки выше рассчитаны на то, чего на обычном 3.3.5a нет.
- Версия аддона — `r277-release`, как и в основной сборке: обе собраны из одной базы.
- Сосуществует с другими аддонами-бэкпортами API (отдельный `!!!ClassicAPI` и подобные): Cell не перезаписывает чужие глобалы. Команда `/cell debug shims` покажет, какой аддон чем владеет на вашем клиенте.

<a name="лицензия"></a>
### Лицензия

Cell распространяется по оригинальной лицензии Cell: **All Rights Reserved**;
изменения разрешены только для личного использования, имя аддона и папки
менять нельзя. Подробности — в [LICENSE.txt](LICENSE.txt). Публичное
распространение изменённой сборки требует явного разрешения автора.

<a name="благодарности"></a>
### Благодарности

- Оригинальный аддон: [enderneko/Cell](https://github.com/enderneko/Cell) — A World of Warcraft raid frame addon
- Бэкпорт под WotLK 3.3.5a: **Keoo**
- Сборка под Sirus: **Keoo**
- Discord: https://discord.gg/sKpJbUrsvR
