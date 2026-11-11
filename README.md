<div align="center">

<img src="https://capsule-render.vercel.app/api?type=venom&color=0:0d1117,40:0b3d91,100:00599C&height=230&section=header&text=Ivan%20·%20C%2B%2B%20Developer&fontSize=48&fontColor=ffffff&fontAlignY=40&desc=системное%20·%20сетевое%20·%20высоконагруженное&descAlignY=62&descSize=18&animation=fadeIn&stroke=1f6feb&strokeWidth=1" width="100%"/>

<a href="https://github.com/Bananka123321">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=20&duration=2800&pause=800&color=58A6FF&center=true&vCenter=true&multiline=false&width=680&height=40&lines=%3E+TLS+%2B+TCP+%D0%BC%D0%B5%D1%81%D1%81%D0%B5%D0%BD%D0%B4%D0%B6%D0%B5%D1%80+%D1%81+%D0%BD%D1%83%D0%BB%D1%8F+%D0%BD%D0%B0+C%2B%2B20;%3E+%D0%B0%D0%BD%D0%B0%D0%BB%D0%BE%D0%B3+Discord+%D0%BD%D0%B0+%D0%BC%D0%B8%D0%BA%D1%80%D0%BE%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%B0%D1%85;%3E+Kafka+%C2%B7+Kubernetes+%C2%B7+WebSocket+%C2%B7+Redis;%3E+%D0%B8%D1%89%D1%83+%D1%81%D1%82%D0%B0%D0%B6%D0%B8%D1%80%D0%BE%D0%B2%D0%BA%D1%83+C%2B%2B+Backend+%2F+Network" alt="typing"/>
</a>

<br>

<a href="https://t.me/M1CROmash"><img src="https://img.shields.io/badge/Telegram-0d1117?style=for-the-badge&logo=telegram&logoColor=26A5E4"/></a>
<a href="mailto:obuhov.i2007@gmail.com"><img src="https://img.shields.io/badge/Email-0d1117?style=for-the-badge&logo=gmail&logoColor=EA4335"/></a>
<a href="https://habr.com/ru/users/Bananka123321/"><img src="https://img.shields.io/badge/Хабр-0d1117?style=for-the-badge&logo=habr&logoColor=65A3BE"/></a>
<img src="https://komarev.com/ghpvc/?username=Bananka123321&style=for-the-badge&color=0d1117&label=PROFILE+VIEWS" alt="views"/>

</div>

<br>

<table>
<tr>
<td width="58%" valign="top">

### `$ whoami`

```cpp
struct Ivan final {
    std::string_view study  = "ТПУ, 3 курс";
    std::string_view role   = "C++ · системное и сетевое программирование";
    std::string_view os     = "Fedora Linux";

    std::array<std::string_view, 4> loves {
        "многопоточность", "сокеты и протоколы",
        "производительность", "работа с памятью"
    };

    [[nodiscard]] auto looking_for() const noexcept {
        return "удалённая стажировка: C++ Backend / Network";
    }
};
```

</td>
<td width="42%" valign="top">

### `$ cat now.log`

```diff
+ Fortal: C++ WebSocket gateway
+ Ivan-Messenger: передача файлов
+ Kafka, Kubernetes, Redis
+ NAT traversal, STUN / TURN
+ C++20: concepts, ranges,
+        coroutines
- «на моей машине работает»
```

</td>
</tr>
</table>

Люблю понимать, как всё устроено на самом деле, от аллокаций до байтов в TCP-потоке. Довожу задачи до конца: с тестами, CI и релизами.

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🛰️ Fortal: аналог Discord на микросервисах

<a href="https://github.com/Fortal-Chat/Fortal"><img src="https://img.shields.io/badge/github-Fortal--Chat%2FFortal-0d1117?style=for-the-badge&logo=github"/></a>
<img src="https://img.shields.io/badge/status-в_разработке-f0883e?style=for-the-badge"/>
<img src="https://img.shields.io/badge/team-2_dev-1f6feb?style=for-the-badge"/>

Делаем вдвоём с напарником: сообщества, каналы, личные сообщения, потом голос. Архитектура с самого начала рассчитана на нагрузку и горизонтальное масштабирование. Моя зона: **C++ gateway** реального времени и **desktop-клиент на Qt 6**.

```mermaid
flowchart LR
    subgraph Clients
        D["🖥️ Desktop<br/>C++ · Qt 6"]
        A["📱 Android<br/>Kotlin · Compose"]
    end

    N["nginx<br/>HTTPS · балансировка"]

    subgraph K8s["☸️ Kubernetes"]
        G["⚡ Gateway<br/>C++ · WebSocket"]
        S["🧩 API<br/>Kotlin · Ktor"]
        Q[("Kafka<br/>шина событий")]
        R[("Redis<br/>pub/sub · кеш")]
    end

    P[("PostgreSQL<br/>пользователи · сообщества")]
    M[("MongoDB<br/>сообщения")]
    L["🎙️ LiveKit<br/>голос"]

    D & A -->|REST| N --> S
    D & A <-->|WebSocket| N <--> G
    S --> P & M
    S -- события --> Q --> G
    G <--> R
    D & A -.-> L
```

<sub>Целевая архитектура. Строим поэтапно: сначала договор API, Docker Compose и PostgreSQL, затем gateway, брокер, выкладка и масштабирование по замерам.</sub>

## 🚀 Другие проекты

<table>
<tr>
<td width="50%" valign="top">

### 💬 [Ivan-Messenger](https://github.com/Bananka123321/Ivan-Messenger)
Мессенджер с шифрованием, написанный с нуля.

- свой сервер на POSIX-сокетах + **OpenSSL TLS**
- **Argon2** для паролей, восстановление сессии без повторного входа
- **PostgreSQL** через пул соединений (libpqxx)
- файлы чанками с докачкой, кеш на клиенте в **SQLite**
- клиент на **Qt 6 / QML** (MVVM): Linux, Windows, Android
- контрактные тесты протокола, **GTest**, релизы через **GitHub Actions**

<img src="https://img.shields.io/badge/C++20-00599C?style=flat-square&logo=cplusplus&logoColor=white"/> <img src="https://img.shields.io/badge/Qt_6-41CD52?style=flat-square&logo=qt&logoColor=white"/> <img src="https://img.shields.io/badge/OpenSSL-721412?style=flat-square&logo=openssl&logoColor=white"/> <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white"/> <img src="https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white"/>

</td>
<td width="50%" valign="top">

### 🚢 [Sea Battle](https://github.com/Bananka123321/Sea_Battle)
Сетевой «Морской бой» для двух игроков.

- сервер с лобби и игровыми сессиями, вход по коду комнаты
- синхронизация состояния игры по TCP
- общий протокол и валидация для клиента и сервера
- Qt 6 Widgets + Qt Multimedia
- Winsock2 / POSIX-сокеты: Windows и Linux

<img src="https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white"/> <img src="https://img.shields.io/badge/Qt_6-41CD52?style=flat-square&logo=qt&logoColor=white"/> <img src="https://img.shields.io/badge/TCP-sockets-30363d?style=flat-square"/>

<sub>вместе с <a href="https://github.com/pomidorchik03">pomidorchik03</a></sub>

</td>
</tr>
</table>

<img src="https://user-images.githubusercontent.com/73097560/115834477-dbab4500-a447-11eb-908a-139a6edaec5c.gif" width="100%">

## 🛠 Стек

<div align="center">

<table>
<tr>
<th>⚙️ Языки и фреймворки</th>
<th>🗄️ Данные</th>
</tr>
<tr>
<td align="center"><img src="https://skillicons.dev/icons?i=cpp,c,qt,kotlin,bash&theme=dark&perline=5"/></td>
<td align="center"><img src="https://skillicons.dev/icons?i=postgres,mongodb,redis,sqlite&theme=dark&perline=4"/></td>
</tr>
<tr>
<th>🌐 Инфраструктура</th>
<th>🧰 Инструменты</th>
</tr>
<tr>
<td align="center"><img src="https://skillicons.dev/icons?i=kafka,docker,kubernetes,nginx,linux&theme=dark&perline=5"/></td>
<td align="center"><img src="https://skillicons.dev/icons?i=cmake,git,github,githubactions,vscode&theme=dark&perline=5"/></td>
</tr>
</table>

<sub>а также OpenSSL · libpqxx · Argon2 · GTest · nlohmann/json · POSIX sockets · WebSocket · LiveKit</sub>

</div>

## 📊 Активность

<div align="center">

<img src="https://streak-stats.demolab.com?user=Bananka123321&theme=tokyonight&hide_border=true&background=0d1117&ring=1f6feb&fire=58A6FF&currStreakLabel=58A6FF&locale=ru" width="49%"/>

<img src="https://github-readme-activity-graph.vercel.app/graph?username=Bananka123321&bg_color=0d1117&color=58a6ff&line=1f6feb&point=ffffff&area=true&area_color=1f6feb&hide_border=true&custom_title=Contribution%20graph" width="100%"/>

</div>

## 🎯 Цель

> Ищу **удалённую стажировку** в C++ Backend / Network разработке. Хочу решать настоящие задачи рядом с сильными инженерами и вырасти в сетевого C++ разработчика, который работает над высоконагруженными системами: мессенджерами, финтехом, трейдингом.

<div align="center">

<br>

<sub><i>«Код читается чаще, чем пишется. Поэтому я стараюсь писать его так, чтобы не стыдно было показать.»</i></sub>

<img src="https://capsule-render.vercel.app/api?type=venom&color=0:00599C,60:0b3d91,100:0d1117&height=120&section=footer" width="100%"/>

</div>
