# This is the way 

## Общая структура пути

1. **База: фундамент AppSec и модель угроз**
2. **Web & API Security (сердце Application Security)**
3. **Secure SDLC: как встроить безопасность в разработку**
4. **Инфраструктура вокруг приложения: Docker, CI/CD, Cloud Sec**
5. **Углубление: код-ревью, языкоспецифичные баги (JS/Node/Go/etc.)**
6. **Портфолио, сертификации, позиционирование**

---

## Блок 1. Фундамент AppSec

**Что выучить:**

* Базовые модели:

  * CIA triad (Confidentiality / Integrity / Availability)
  * STRIDE, DREAD (для threat modeling)
* Типы атак:

  * Injection, XSS, CSRF, IDOR, SSRF, RCE, LFI/RFI, auth & session issues
* Основные стандарты:

  * OWASP Top 10 (Web, API)
  * OWASP ASVS 

**Практика:**

* Сделать шпаргалку по OWASP Top 10:
  для каждой уязвимости - *"что это, где бывает, как предотвратить"*.
* Разобрать 3–5 реальных инцидентов (отчеты bug bounty / write-up’ы) и для каждого ответить:

  * где была ошибка в дизайне/коде,
  * как это можно поймать на этапе разработки.

---

## Блок 2. Web & API Security

**По URL/фиче видеть потенциальные векторы атаки**.

**Теория:**

* Архитектура веб-приложения:

  * клиент → API → БД, кеши, очередь, сторонние сервисы.
* Auth / Session:

  * JWT, cookies, refresh-токены, session fixation, brute-force, rate-limits.
* Типовые уязвимости Web:

  * Injection (SQL, NoSQL, LDAP, template, etc.)
  * XSS (reflected, stored, DOM)
  * CSRF
  * IDOR/BOLA (broken object level authorization)
  * SSRF
  * insecure file upload
* API-специфика:

  * Broken Object Level Authorization (BOLA)
  * Mass Assignment
  * Overly permissive CORS
  * Rate limiting / abuse

**Практика:**

* Платформы:

  * PortSwigger Web Security Academy
  * HackTheBox / TryHackMe - именно web/app-направление.
* Минимум:

  * пройти упражнения по XSS, SQLi/NoSQLi, IDOR, auth-bypass, SSRF.
* Взять **свой реальный проект** (или тестовый pet-project) и:

  * нарисовать схему компонентов,
  * выписать все точки входа (эндпоинты, формы, вебхуки),
  * для каждой точки входа сделать список возможных атак.

---

## Блок 3. Secure SDLC: как встроить безопасность в разработку

**Делать продукт безопаснее системно**.

**Что изучить:**

* Secure SDLC:

  * где в процессе появляются security-активности: требования, дизайн, разработка, тестирование, деплой.
* Практики:

  * Threat Modeling (минимум STRIDE по ключевым фичам)
  * Security code review
  * SAST / DAST / SCA:

    * что такое и чем отличаются;
    * где в CI их ставить;
    * что можно реально автоматизировать.
* Политики:

  * как формировать password policies, account lockout, 2FA, session timeout,
  * как документировать security-решения (RFC/ADR).

**Практика:**

* Взять одну фичу (например, "регистрация/логин/восстановление пароля") и:

  * сделать threat model (схема + STRIDE/what can go wrong);
  * выписать mitigation для каждой угрозы.
* Настроить **минимальный secure SDLC** на своем/тестовом проекте:

  * линтеры + pre-commit hooks,
  * SAST (например, semgrep) в CI,
  * SCA (проверка зависимостей),
  * простейший DAST по staging-URL.

---

## Блок 4. Инфраструктура вокруг приложения

**Docker, Kubernetes, CI/CD, cloud**

**Что выучить:**

* Docker / K8s Security:

  * минимальные образы, rootless, capabilities, seccomp, сетевые политики,
  * секреты: где и как хранить (env, vault, K8s secrets).
* CI/CD:

  * где могут украсть токены, секреты, артефакты,
  * типичные баги: plain-text секреты, shared runners, insecure artifact download.
* Cloud (AWS/Azure/GCP или тот стек, с которым ты работаешь):

  * IAM-роли, least privilege,
  * типовые misconfiguration (public bucket, открытые security groups и т.п.).

**Практика:**

* Взять свой стэк и:

  * сделать **ревью Dockerfile** в своих проектах на предмет:

    * ненужных пакетов,
    * работы под root,
    * утечки секретов в image.
  * оформить чек-лист CI/CD-безопасности для своей инфраструктуры.
* Поднять уязвимый контейнер/кластер (например, Damn Vulnerable Docker / Kubernetes) и поиграться.

---

## Блок 5. Углубление: языкоспецифичные баги и code review

### "Посмотри код, безопасно ли?"

Фокус на **тех языках, которые ты реально используешь** (JS/TS, Node, Go, Python, Java, C++).

**Что изучить:**

* Языкоспецифичные уязвимости:

  * для Node.js: prototype pollution, опасные eval/Function, шаблонизаторы, express-misconfig;
  * для Go: инъекции в SQL/ORM/templating, unsafe fmt, path traversal через `filepath.Join` и т.п.;
  * работа с криптографией: правильные libs, алгоритмы, хранение ключей.
* Secure coding guidelines:

  * OWASP Cheat Sheets по конкретным темам (Auth, Input Validation, Logging, etc.).

**Практика:**

* Взять 1–2 open-source проекта на твоем основном языке и:

  * сделать им **мини-code review с фокусом на безопасность**,
  * оформить findings в виде короткого отчета (это уже элемент портфолио).
* Настроить semgrep/sonarqube/CodeQL на свой репозиторий и **разобраться с находками**: что реально баг, а что нет.

---

## Блок 6. Портфолио, сертификации и выход на рынок (параллельно с Блоками 3–5)

Важно не только уметь, но и **уметь показать**, что ты это умеешь.

**Что сделать:**

1. **Портфолио:**

   * 2–3 мини-отчета по security-ревью своих/чужих проектов (как для клиента).
   * 1 пример внедрения secure SDLC / CI (описание до/после + что именно ты сделал).
   * 1–2 write-up’а по найденным уязвимостям (пусть даже в учебных лабах).

2. **Open source / community:**

   * контрибьют в security-cheat-sheet, правила для semgrep, или issue с багом безопасности в open-source.

3. **Сертификации (по желанию):**

   * стартово: eJPT/eWPT / eWPTX или аналоги (если хочется формальной галочки),
   * позже: OSWE, CSSLP, GIAC GWEB/GWAPT - уже под senior-уровень.

     > Software Engineer → Application Security Engineer
     > с упором на: secure SDLC, web/API security, threat modeling, CI/CD security.

---

## Как этим пользоваться на практике

Чтобы не утонуть:

1. Выбери **горизонт 3–4 месяцев** и сделай план:

   * Месяц 1: Блок 1 + половина Блока 2
   * Месяц 2: конец Блока 2 + Блок 3
   * Месяц 3: Блок 4 + старт Блока 5
   * Месяц 4: добиваешь Блок 5 + собираешь портфолио (Блок 6).

2. Для каждой недели сформулируй:

   * 1–2 темы (например: XSS + CSRF),
   * 2–3 практических задания (конкретные упражнения/лабы).

3. Держи **один трек теории и один трек практики** всегда параллельно:

   * читаешь/смотришь → сразу ищешь руками, как это ломается/чинился бы.

---
