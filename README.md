# neuro-modelling-interface
Пользовательский интерфейс для системы нейроморфного моделирования

Искусственные нейронные сети используются во многих областях современной жизни и позволяют решать актуальные, важные и практически значимые задачи, которые зачастую не поддаются решению с помощью классических подходов. Одним из динамично развивающихся направлений в настоящее время является разработка нейроморфных системы на базе мемристоров [1]. Для математического моделирования работы таких систем были разработаны программные средства [2], которые представляют собой вычислительный модуль на С++. Однако, для конечных пользователей-исследователей необходим удобный интерфейс, а для интеграции расчетного модуля в многомасштабные сценарии расчетов [3] необходим программный интерфейс (API). Текущая работа посвящена разработке пользовательского и программного интерфейсов для подобной системы.

Целью работы является анализ деталей реализации программного комплекса, предусматривающего все возможные аспекты взаимодействия с системой нейроморфного моделирования, обладающее гибкостью и расширяемостью для минимизации затрат на поддержку развивающегося функционала модуля. Необходимый для реализации функционал:

1. Корректная обработка и валидация входных данных.

2. В качестве шаблонов для распознавания нейросети дать возможность пользователю интерактивно рисовать пиксельное черно-белое изображение.

3. Возможность пользователю вводить, как параметры нейросети, так и параметры математической модели мемристора.

4. Возможность просматривать промежуточные результаты работы сети в течении ее работы, а также итоговые результаты в наглядном виде (представляя полученные сетью веса градациями серого в пиксельном изображении).

5. Возможность сохранения промежуточных и итоговых результатов работы модуля, импорт и экспорт входных параметров.

6. Воспроизводимость экспериментов. При вводе одних и тех же данных, результат не должен меняться.

В качестве решения всех вышеописанных задач, было предложено разработать веб-приложение, состоящее из трех частей: база данных, серверное приложение, клиентское приложение. Были учтены лучшие практики современной разработки программного обеспечения: использование нереляционных баз данных[4], микросервисной архитектуры[5], современных библиотек разработки веб интерфейсов, а также контейнеризация приложения для стабильного развертывания на сервере.

• Для базы данных было выбрано решение MongoDB за счет простоты конфигурации, легкого масштабирования и взаимодействия с клиентским приложением. База данных будет отвечать за хранение данных по проведенным экспериментам, а также справочников.

• Для реализации серверного приложения был выбран язык Kotlin и библиотека Spring Boot. Язык Kotlin [5] сочетает в себе преимущества Java, но в тоже время обладает большим количеством современных синтаксических конструкций, облегчающих поддержку и сопровождение кода Spring Boot же позволяет быстро и стандартным способом реализовать множество инфраструктурных функций: взаимодействие по HTTP, работу с базой данных, сосредоточившись на реализации бизнес логики. В реализуемом приложении на серверную часть возложена следующие обязанности: принимать HTTP запросы от клиентского приложения, сохранять обрабатываемые данные в базу и отправлять команды на исполнение модулю нейроморфного моделирования посредством протокола SSH.

• Клиентское приложение было решено разрабатывать на языке TypeScript с использованием библиотеки React. TypeScript позволяет писать более надежные приложения, за счет того, что о многих ошибках становится известно еще на стадии компиляции, до непосредственного запуска. React же позволяет строить приложение, разбивая его на составные части – компоненты, которые в последствии удобно переиспользовать. На клиентское приложение возложена обязанность предоставить пользователя максимально интуитивно понятный интерфейс для управления нейроморфной системы.

В рамках данной работы была разработана архитектура и прототип веб-интерфейса, а также реализация интеграции с модулем нейроморфного моделирования.

Литература

[1] Морозов А. Ю., Ревизников Д. Л., Абгарян К. К. Вопросы реализации нейросетевых алгоритмов на мемристорных кроссбарах // Известия высших учебных заведений. Материалы электронной техники, 2019. Т. 22. № 4

[2] Морозов А.Ю., Абгарян К.К., Ревизников Д.Л. Математическое моделирование самообучающейся нейроморфной сети, основанной на наноразмерных мемристивных элементах с 1T1R-кроссбар-архитектурой // Известия высших учебных заведений. Материалы электронной техники. 2020;23(3):186-195.

[3] Абгарян К.К, Гаврилов Е.С. «Интеграционная платформа для многомасштабного моделирования нейроморфных систем», «Информатика и ее применения», том 14, выпуск 2, 2020 г. Стр. 104-110.

[4] Fowler, M., and P. J. Sadalage. 2012. NoSQL distilled: A brief guide to the emerging world of polyglot persistence. Addison-Wesley Professional. 190 p.

[5] Newman, S. 2015. Building microservices. Sebastopol, CA: O'Reilly Media. 282 стр.

[6] Jemerov, D., Isakova, S. Kotlin in Action. Manning, 2017 г., 360 стр.