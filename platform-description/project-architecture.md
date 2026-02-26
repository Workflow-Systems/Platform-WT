# Архитектура проекта

## Трехуровневая архитектура WT-программы <a href="#three-tier-architecture-of-wt-program" id="three-tier-architecture-of-wt-program"></a>

Любое приложение, построенное на платформе Workflow Technology, – проще говоря, WT-программа – представляет собой трехуровневое клиент-серверное приложение.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2F8srULVFFx2wydHlUIrl5%2FProject_architecture.png?alt=media&#x26;token=1b689f04-f8df-493b-89d5-4875bd507167" alt=""><figcaption></figcaption></figure>

**Клиентская часть** представляет собой:

* Для десктопной разработки: [приложение Windows](https://learn.microsoft.com/ru-ru/dotnet/desktop/winforms/overview/?view=netdesktop-7.0).
* Для мобильной разработки: [Xamarin](https://learn.microsoft.com/ru-ru/xamarin/get-started/what-is-xamarin)-приложение под iOS и Android.
* Для веб-разработки: [Blazor](https://learn.microsoft.com/ru-ru/aspnet/core/blazor/?view=aspnetcore-7.0)-веб-приложение.

Все три версии клиентских приложений построены на платформе .NET.

Настройки конфигурации приложения Windows вынесены в файл [WorkflowForms.dll.config](https://wfsys.gitbook.io/wt_knowledge_base/platforma-wt/configuration-files/workflowforms.dll.config). Основными настройками являются путь до стартовой формы и IP-адрес и порт расположения серверной части.

**Серверная часть** представляет собой веб-приложение, построенное на платформе .NET, а именно на веб-сервере Kestrel, включенном в ASP.NET Core.

Сервер поддерживает протокол RestWebAPI, что позволяет выстроить общение клиентских приложений и сервера через классические API-запросы.

Настройки сервера разбиты на два файла. В файл [appsettings.json](https://wfsys.gitbook.io/wt_knowledge_base/platforma-wt/configuration-files/appsettings.json) вынесены настройки доступа к базе данных, временной зоной сервера и другие, а в файл [hosting.json](https://wfsys.gitbook.io/wt_knowledge_base/platforma-wt/configuration-files/hosting.json) – IP-адрес и порт сервера.

В качестве **СУБД** по умолчанию используется PostgreSQL – одна из наиболее производительных и популярных СУБД.&#x20;

## Состав элементов архитектуры WT-программы <a href="#elements-of-wt-program-architecture" id="elements-of-wt-program-architecture"></a>

Каждая WT-программа, созданная на базе платформы WT, состоит из элементов:

![](https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FbdDPfA2op7PVFHcvURv2%2FProject_structure-%D0%A1%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0%201.png?alt=media\&token=28d8a68b-be19-4922-a395-ceddef8510f2)

* База данных. В качестве СУБД выступает PostgreSQL;
* Серверная часть Workflow Engine (WE) включает:&#x20;
  * бинарные файлы;
  * xml-файл серверной части с описанием SQL-запросов и прав доступа;
* Клиентские части Workflow Forms (WF), Workflow MobileForms (WMF), Workflow WebForms (WWF) включают:
  * бинарные файлы;
  * xml-файлы форм, файлы ресурсов (картинки, звуки) и файлы шаблонов печатных форм (docx/xlsx).

Бинарные файлы WE, WF, WMF и WWF помимо штатных, платформенных, могут быть кастомными – созданными разработчиками для расширения функциональности платформы в конкретном проекте. Для WF это могут быть кастомные команды или графические элементы форм. А для серверной части это могут быть библиотеки, которые отвечают за взаимодействие со сторонними сервисами. Например, отправка данных в Google Analytics или интеграция со сторонней CRM.

## Технический сценарий работы WT-программы <a href="#script-of-wt-program" id="script-of-wt-program"></a>

Рассмотрим сценарий загрузки данных на форму, например, десктопного приложения:

1. Запуск клиентского приложения WT-программы – транслятора Workflow Forms.
2. Одним из первых действий транслятора Workflow Forms будет чтение файла конфигурации [WorkflowForms.dll.config](https://wfsys.gitbook.io/wt_knowledge_base/platforma-wt/configuration-files/workflowforms.dll.config).
3. Из файла конфигурации среди прочего будут извлечены:\
   \- IP-адрес и порт – где расположена серверная часть WT-программы\
   \- Путь до стартовой клиентской XML-формы
4. Чтение стартовой клиентской XML-формы.
5. После чтения стартовой клиентской XML-формы, в которой среди прочего наверняка будут XML-конструкции [DataConnection](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/dataconnections/primary_dc), будут осуществлены запросы данных с сервера в соответствии с параметрами, указанными в коде DataConnection (к параметрам DataConnection в первую очередь относятся наименования SQL-запросов, результаты которых требуется получить, и параметры, которые следует в них передать перед выполнением). Запросы (чтобы не путать с SQL-запросами, назовем их WF-запросы) будут отправлены на адрес, ранее прочтенный из файла конфигурации, где расположена серверная часть WT-программы.
6. Серверная часть WT-программы – транслятор Workflow Engine – в первую очередь осуществит [аутентификацию](https://wfsys.gitbook.io/wt_knowledge_base/platforma-wt/authentication) пользователя, который к нему обращается.
7. После успешной аутентификации пользователя Workflow Engine определит, на какие именно SQL-запросы аутентифицированный пользователь имеет права, прочитав эти сведения из файла Workflow.xml, из блока [прав доступа](https://wfsys.gitbook.io/wt_knowledge_base/platforma-wt/access-rights).
8. Далее Workflow Engine, извлекая из WF-запроса наименования SQL-запросов, результаты которых требуется получить, сравнит извлеченные имена SQL-запросов с перечнем имен SQL-запросов, на выполнение которых пользователь имеет права – другими словами, авторизует пользователя.
9. После успешной авторизации WorkflowEngine разыменует SQL-запросы, результаты которых требуется получить, – другими словами, по именам SQL-запросов получит их текст, который хранится в серверном XML-файле – Workflow.xml.
10. После разыменования SQL-запросов в их тексты будут вставлены параметры, также переданные в WF-запросе.
11. После подстановки параметров SQL-запросы будут отправлены в БД на выполнение. К тому моменту это будет возможно потому, что транслятор WorkflowEngine сразу после запуска, считывая параметры подключения к БД из конфигурационного файла [appsettings.json](https://wfsys.gitbook.io/wt_knowledge_base/platforma-wt/configuration-files/appsettings.json), осуществляет пробное подключение в БД и впоследствии всегда готов выполнять SQL-запросы к БД.
12. Workflow Engine, получив от БД результаты выполнения SQL-запросов, возвращает их на клиентскую часть в качестве ответа на WF-запрос.
13. Workflow Forms, получив данные, располагает и/или использует их на форме тем или иным образом – в соответствии с логикой, заданной в XML-файле клиентской формы интерфейса.
