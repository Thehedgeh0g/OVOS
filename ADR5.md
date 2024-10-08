# ADR - [Выбор фреймворка для разработки клиента]

Участники: Лежнин Попов Смаилов

Дата: 25.09.2024

Статус: Code review

## Контекст

- Проблемы и задачи
    - Масштабируемость: С учетом потенциального роста числа пользователей, важно выбрать архитектуру,
      которая сможет поддерживать высокую нагрузку и обеспечивать стабильную работу приложения.
    - Производительность: Игровой процесс требует минимальной задержки, особенно в многопользовательском режиме.
    - Архитектура должна обеспечивать быструю обработку запросов и обновление состояния игры.
    - Разработка и поддержка: Выбранная архитектура должна быть удобной для команды разработчиков,
      обеспечивая легкость в развертывании, тестировании и обновлении приложения.
- Ограничения и предпосылки
    - Технические ограничения: Необходимо учитывать доступные технологии и инструменты, а также уровень квалификации
      команды разработчиков. Например, бессерверные архитектуры могут потребовать знаний в области облачных технологий.
    - Безопасность: При реализации многопользовательского режима важно обеспечить защиту данных пользователей и
      предотвратить мошенничество в игре.
    - Бюджетные ограничения: Разные архитектурные подходы могут иметь различные затраты на внедрение и поддержку.
      Например, серверные решения могут требовать значительных инвестиций в инфраструктуру. Учитывая, что проект
      не имеет выделенного бюджета, наша команда обязана учитывать использование бесплатных или экономически
      эффективных решений, как для разработки, так и для дальнейшего поддержания системы.
    - Пользовательский опыт: Архитектура должна поддерживать функции, которые улучшают взаимодействие с пользователем,
      такие как возможность играть с друзьями или против случайных соперников.
    - Состав команды: В команду входят три разработчика с навыками PHP, JavaScript, Go, C++, SQL и Python.

## Рассматриваемые варианты

- ### Native (Android/iOS/WEB)  
    - Преимущества:  
        - Полный доступ к нативным API платформ, что позволяет реализовывать высокоэффективные приложения с максимальной производительностью.
        - Хороший контроль над интерфейсом и взаимодействием с системой.
        - Возможность полной кастомизации пользовательского опыта на каждой платформе.  
    - Недостатки:  
        - Необходимость разработки отдельных приложений для каждой платформы (Android, iOS, Web), что увеличивает затраты времени и ресурсов.  
        - Сложнее поддерживать кросс-платформенную синхронизацию и поддерживать единую кодовую базу.  
        - Требуются специфические навыки для каждой платформы, что может усложнить процесс разработки для команды.

- ### React  
    - Преимущества:  
        - Широко используемый и поддерживаемый фреймворк с активным сообществом и обширной экосистемой.
        - Обеспечивает компонентный подход к разработке, что упрощает поддержку и масштабируемость клиентской части.
        - Универсальный фреймворк, легко интегрируемый с любыми веб-технологиями.  
    - Недостатки:  
        - Потребность в дополнительных инструментах (например, Redux) для управления состоянием при разработке крупных приложений.
        - Может быть медленнее нативных решений, особенно при работе с графикой и анимациями.
        - Некоторая сложность в настройке и конфигурации проекта для новых разработчиков.

- ### Vue  
    - Преимущества:  
        - Более простой порог вхождения по сравнению с React и Angular.
        - Легкость в интеграции с существующими проектами благодаря модульной структуре.
        - Встроенные инструменты для управления состоянием и маршрутизацией (Vuex и Vue Router).  
    - Недостатки:  
        - Меньшее сообщество и поддержка по сравнению с React, что может ограничивать выбор готовых решений.
        - Ограниченные возможности для сложных и крупных приложений без значительных доработок.
        - Меньшее количество доступных библиотек и инструментов по сравнению с React.

- ### React Native  
    - Преимущества:  
        - Позволяет использовать единый код для разработки приложений на Android и iOS, что снижает затраты на поддержку и разработку.
        - Хорошая производительность для кросс-платформенных приложений, возможность использования нативных модулей.
        - Использование знакомой экосистемы React, что сокращает время обучения команды.  
    - Недостатки:  
        - Меньшая производительность по сравнению с нативными приложениями, особенно при использовании сложной графики или анимации.
        - Ограниченная поддержка специфичных для платформы функций, что может потребовать написания нативного кода.
        - Зависимость от сторонних библиотек, которые могут не поддерживаться или обновляться.

- ### Flutter  
    - Преимущества:  
        - Позволяет разрабатывать приложения для Android, iOS и веба с одной кодовой базы.
        - Высокая производительность благодаря использованию графического движка Skia, подходящего для сложных интерфейсов и анимаций.
        - Стабильная поддержка от Google и быстрое развитие экосистемы.  
    - Недостатки:  
        - Относительно новая технология, что может привести к ограниченному количеству доступных библиотек и инструментов.
        - Более высокая сложность в освоении, особенно для разработчиков, привыкших работать с веб-технологиями.
        - Приложения могут занимать больше места из-за встроенного движка и требовать большего объема памяти.
  
- ### Compose Multiplatform  
    - Преимущества:  
        - Единая кодовая база для создания интерфейсов на Android, Desktop и Web с использованием Jetpack Compose.
        - Поддержка нативных API, что позволяет создавать высокопроизводительные приложения с нативным UX.
        - Современный декларативный подход к созданию UI, схожий с React и Flutter.  
    - Недостатки:  
        - Находится в стадии активного развития, что может приводить к нестабильности и ограниченной документации.
        - Ограниченная поддержка платформ, особенно по сравнению с Flutter или React Native.
        - Меньшее количество доступных библиотек и плагинов по сравнению с другими кросс-платформенными фреймворками.

## Решение

Для разработки клиентской части онлайн-версии игры "Шашки" был выбран фреймворк **React**. Это решение обусловлено следующими факторами:
React предоставляет гибкий и компонентный подход к разработке пользовательского интерфейса, что упрощает создание, тестирование и масштабирование приложения. У команды уже есть опыт работы с этим фреймворком, что сократит время на освоение новых технологий и ускорит процесс разработки. React также поддерживает обширную экосистему инструментов и библиотек для веб-разработки.

## Обоснование

React является одним из самых популярных и активно поддерживаемых фреймворков для разработки веб-приложений. Он предлагает модульный подход, что облегчает поддержку кода и улучшает его читаемость. Возможность использования сторонних библиотек и инструментов для управления состоянием, маршрутизации и тестирования позволяет быстрее реализовывать сложные функции и фичи в проекте. Широкая поддержка сообщества React также гарантирует наличие готовых решений и документации для решения возникающих проблем.

## Последствия

### Положительные последствия

- Ускорение разработки благодаря использованию знакомого фреймворка и обширной экосистемы инструментов.
- Простота масштабирования и поддержки кода благодаря компонентной архитектуре.
- Легкость интеграции сторонних библиотек для управления состоянием, маршрутизацией и другими функциями.
- Активное сообщество и регулярные обновления React обеспечивают стабильную работу фреймворка и наличие актуальной документации.

### Oтрицательные последствия

- Возможные проблемы с производительностью при рендеринге сложных компонентов и анимаций, что может потребовать дополнительной оптимизации.
- Необходимость в управлении состоянием при работе с крупными приложениями (например, с использованием Redux или других инструментов).
- Зависимость от экосистемы React, что может привести к проблемам совместимости при использовании специфических библиотек или плагинов.

### Риски

- Риск снижения производительности приложения, если не будут реализованы должные меры по оптимизации рендеринга и обновления компонентов.
- Возможные сложности в интеграции с будущими платформами или сервисами, если потребуется расширение функционала.
- Риск устаревания или прекращения поддержки некоторых сторонних библиотек, используемых в React-проектах, что потребует поиска альтернативных решений.

## Затронутые области

- Клиентская архитектура приложения
- Производительность и отзывчивость пользовательского интерфейса
- Управление состоянием и маршрутизация
- Масштабируемость клиентской части
- Интеграция с серверной частью и сторонними библиотеками

## История

Основные обсуждения, приведшие к выбору React для разработки клиентской части игры "Шашки":  
- Опыт команды: У разработчиков есть значительный опыт работы с React, что сокращает время на освоение фреймворка и ускоряет процесс разработки.  
- Гибкость и компонентный подход: React позволяет легко разделять код на переиспользуемые компоненты, что упрощает разработку и поддержание проекта.  
- Экосистема: React имеет большое количество сторонних библиотек и инструментов, что позволяет быстрее реализовать необходимые функции (например, Redux для управления состоянием, React Router для маршрутизации).  
- Поддержка сообществом: React активно поддерживается разработчиками по всему миру, что гарантирует наличие актуальных решений и регулярных обновлений.  
- Альтернативы: Рассмотренные фреймворки (Vue, Flutter, Native) либо требовали больше ресурсов на освоение, либо не подходили по критериям производительности и гибкости для веб-приложений.

Эти факторы привели к окончательному решению использовать React для клиентской части.
