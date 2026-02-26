# Развертывание проекта

В этой статье рассмотрим ручное разворачивание учебного проекта, с которым познакомились в статье [Учебный проект](../educational-project.md).

Для начала скачайте любую платформу для администрирования и разработки для PostgreSQL. В этой статье и учебном проекте будем использовать pgAdmin 3. Последнюю версию платформы можете скачать с официального [сайта](https://www.pgadmin.org/). Кроме того, в пакет установки PostgreSQL уже входит pgAdmin 4. Скачать последнюю версию PostgreSQL можно с официального [сайта](https://www.postgresql.org/download/). В статье [Установка PostgreSQL](installing_postgresql.md) приведена полная инструкция по установке сервера базы данных.

## План развертывания проекта <a href="#project-deployment-plan" id="project-deployment-plan"></a>

#### **Этап 1. Восстановление БД** <a href="#step-1" id="step-1"></a>

1. [Создать новую БД](./#create-database) (например, template\_project) и [восстановить резервную копию](./#restore-backup) из файла Template\Development\database\create\create.backup.
2. В таблице public.workflow\_type в столбце path проверить, совпадает ли указанный путь до xml-файла серверной части с путем, куда были развернуты исходники проекта. При несовпадении указать абсолютный путь до файла Template\Projects\1. Template\Workflow\Template.xml.

#### Этап 2. Восстановление серверной части <a href="#step-2" id="step-2"></a>

1. Создать папку в которую будет восстанавливаться серверная часть. Например, D:\WorkflowEngine\Template.
2. Скопировать стандартные конфигурационные файлы hosting.json и appsettings.json из папки config [архива](./#we-archive) в новую папку D:\WorkflowEngine\Template
3. В файл D:\WorkflowEngine\Template\appsettings.json внести правки:
   * В поле Database проверить, совпадает ли указанное имя базы данных с именем созданной ранее базой данных. При несовпадении указать верное имя базы данных.
   * В поле ServerPort проверить, совпадает ли указанный порт сервера баз данных с портом в приложении СУБД. При несовпадении указать верный порт.
   * В поле Password указать пароль, который задали при установке PostgreSQL.
4. В файле D:\WorkflowEngine\Template\hosting.json указать порт, который еще не используется на локальном компьютере.
5. Скопировать штатные бинарники из папки bin [архива](./#we-archive) в папку D:\WorkflowEngine\Template.
6. Скопировать файл \_start.bat из [архива](./#we-archive) в папку D:\WorkflowEngine\Template.
7. Для удобства запуска серверной части создать ярлык на файл D:\WorkflowEngine\Template\\\_start.bat, переименовав его (например, в Template SRV).

#### Этап 3. Восстановление клиентской части <a href="#step-3" id="step-3"></a>

1. Создать папку в которую будет восстанавливаться клиентская часть. Например, D:\WorkflowForms\Template.
2. Скопировать стандартный конфигурационный файл WorkflowForms.dll.config из папки config [архива](./#wf-archive) в новую папку D:\WorkflowForms\Template.
3. В файл D:\WorkflowForms\Template\WorkflowForms.dll.config внести правки:
   * В поле ServerUrl указать IP-адрес и порт серверной части, как они прописаны в файле hosting.json (например, http://localhost:49707).
   * В поле StartFormFileName проверить, совпадает ли указанный путь до стартовой формы проекта с путем, куда были развернуты исходники проекта. При несовпадении указать абсолютный путь до файла Template\Projects\1. Template\Forms\TemplateStart.xml.
   * В полях UseSourceCache и CheckBinaryFiles указать значение False.
   * В поле AnonymousLogin указать значение True, тем самым включив учетку входа - WS\_GUEST.
   * В полях AnonymousUserName и AnonymousPassword прописать WS\_GUEST и 123 соответственно.
4. Скопировать штатные бинарники из папки bin [архива](./#wf-archive) в папку D:\WorkflowForms\Template.
5. Для удобства запуска клиентской части создать ярлык на файл D:\WorkflowForms\Template\WorkflowForms.exe, переименовав его (например, в "Template CLI").

Далее подробнее рассмотрим каждый пункт плана.

При возникновении ошибки в процессе разворачивания проекта вернитесь к этому плану и проверьте каждый его пункт. Часто ошибки возникают, если при установке PostgreSQL указали свой пароль и забыли исправить пароль в файле конфигурации серверной части - _appsettings.json._ Вторая возможная причина ошибки в том, что при разворачивании серверной части, архив распаковали в папку, которая отличается от пути указанного в базе данных, или при разворачивании клиентской части забыли изменить путь до стартовой формы.

## База данных <a href="#database" id="database"></a>

{% hint style="info" %}
В статье [Установка PostgreSQL](installing_postgresql.md) в разделе [pgAdmin 4](installing_postgresql.md#pgadmin-4) приведена инструкция по созданию базы данных и восстановлению бэкапа базы.
{% endhint %}

### Создание базы данных <a href="#create-database" id="create-database"></a>

Перейдем в программу pgAdmin III для управления СУБД PostgreSQL. В окне **Браузер объектов (Object browser)**  разверните дерево **Серверы (Servers)** и правой кнопкой мыши кликните по узлу **Базы данных (Databases)** и в появившемся меню выберем пункт **Новая база данных... (New Database...)**.

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

После этого отобразится окно для создания базы данных. Введем имя нашей базы данных, например, **template\_project**. Этого достаточно, чтобы создать базу данных с настройками по умолчанию.

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

Жмем OK.

### Восстановление бэкапа базы данных <a href="#restore-backup" id="restore-backup"></a>

В окне **Браузер объектов (Object browser)** раскройте узел **Базы данных (Databases)** и выберите ранее созданную базу данных, нажмите по ней правой кнопкой мыши и в появившемся контекстном меню выберете пункт **Восстановить… (Restore...)**.

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

Откроется окно восстановления базы, где вы можете задать параметры восстановления, в частности выбрать файл резервной копии.

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

На вкладке **Файл (File Options)** укажите путь до файла **create.backup** в папке проекта. Оставьте все параметры восстановления как есть и нажмите **Восстановить (Restore)**. Запустится процесс восстановления базы данных.  После того, как процесс по восстановлению будет удачно завершен, нажмите **Завершено (Done)**.

<figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure>

Обновите состояние базы данных, выбрав в окне **Браузер объектов (Object browser)** узел базы данных и нажав клавишу **F5**.

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>Описание структуры базы данных</summary>

Как видно на рисунке выше, база данных проекта имеет две схемы:&#x20;

* **public**: содержит системные таблицы, общие для всех бизнес-процессов в клиентском решении;
* **template**: содержит системные и дополнительные таблицы, необходимые для отдельного бизнес-процесса.

#### Схема public <a href="#scheme-public" id="scheme-public"></a>

Таблица **public.about** содержит описание текущей версии проекта.

Таблица **public.file** содержит список всех файлов, загруженных на сервер. Файлы хранятся в папке, определенной настройкой Storages веб-сервера, описанной в файле appsettings.json.

Таблица **public.language** содержит описание поддерживаемых языков.

Таблица **public.load\_mode** содержит описание режимов загрузки данных в [DataConnection](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/dataconnections/primary_dc).

Таблица **public.schedule** содержит данные о последнем запуске задач, описанных в серверном xml-файле.

Таблица **public.strings** содержит строковые ресурсы для поддерживаемых языков.

Таблица **public.time\_zone\_info** и **public.timezone\_intervals** содержат описание и правила часовых поясов.

Таблица **public.user** содержит общий список пользователей системы.

Таблица **public.user\_form\_info** содержит пользовательские настройки графического интерфейса

Таблица **public.workflow\_type** содержит список всех процессов системы и путей до серверных xml-файлов, связанных с ними.

#### Схема template <a href="#scheme-template" id="scheme-template"></a>

Таблица **template.group** содержит список групп пользователей данного процесса.

Таблица **template.group\_group** содержит соответствия групп пользователей между собой в данном процессе.

Таблица **template.permission** и **template.group\_permission** содержат описание динамических прав доступа. Права доступа подробно рассмотрим на одном из уроков.

Таблица **template.update** содержит информацию о выполнении запросов в данном процессе. Подробную информацию о том, какие запросы будут зарегистрированы в данной таблице, можно найти в описании [UpdateSqlQuery](https://wfsys.gitbook.io/ws-syntax/workflow_engine/sql_queries/update_sql_query).

Таблица **template.user** содержит список пользователей данного процесса.

Таблица **template.user\_group** содержит соответствия пользователей и групп данного процесса.

</details>

### Последние настройки базы данных <a href="#latest-database-settings" id="latest-database-settings"></a>

После восстановления бэкапа необходимо в таблице **public.workflow\_type** в поле **path** поправить путь до серверного xml-файла, связанного с каждым процессом. В учебном проекте только один процесс **Template**. И для него нужно указать абсолютный путь до файла Template\Projects\1. Template\Workflow\Template.xml.

## Серверная часть <a href="#server" id="server"></a>

### Архив <a href="#we-archive" id="we-archive"></a>

Скачайте бинарники нужной разрядности:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>WorkflowEngine_v3_x64.zip</td><td></td><td></td><td><a href="https://wfsys.ru/download/WorkflowEngine_v3_x64.zip">https://wfsys.ru/download/WorkflowEngine_v3_x64.zip</a></td></tr><tr><td>WorkflowEngine_v3_x86.zip</td><td></td><td></td><td><a href="https://wfsys.ru/download/WorkflowEngine_v3_x86.zip">https://wfsys.ru/download/WorkflowEngine_v3_x86.zip</a></td></tr></tbody></table>

Независимо от разрядности структура папок и файлов будет одинаковая. Основные элементы архивов:

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

Как говорилось ранее, серверная часть построена на базе .Net Core 3.1, что позволило сделать ее портативной. Поэтому в папке **bin** лежат все необходимые dll-файлы, чтобы на клиентском сервере не приходилось отдельно устанавливать .NET Core SDK.

Так же в папке bin лежит папка **WorkflowEngineUpdateService**, которая содержит dll-файлы и файлы конфигурации для службы обновления серверной части.

В папке **config** лежат конфигурационные файлы:&#x20;

* [appsettings.json](https://wfsys.gitbook.io/wt-knowledge-base/platforma-wt/configuration-files/appsettings.json) - настройки доступа к базе данных, временной зоной сервера и другие;&#x20;
* [hosting.json](https://wfsys.gitbook.io/wt-knowledge-base/platforma-wt/configuration-files/hosting.json) - IP-адрес и порт сервера.

Файл **\_start.bat** запускает наше web-приложение.

### Разворачивание и настройка <a href="#we-deployment-and-configuration" id="we-deployment-and-configuration"></a>

Первым делом создадим папку в которую будем восстанавливать серверную часть. Например, D:\WorkflowEngine\Template.

Скопируем стандартные конфигурационные файлы **hosting.json** и **appsettings.json** из папки config ранее скачанного архива в D:\WorkflowEngine\Template.

В файле _D:\WorkflowEngine\Template\appsettings.json_ необходимо указать настройки доступа к нашей базе данных. Они описаны в объекте Database. В поле **Database** заменим workflow\_technology на имя нашей базы данных, **template\_project**. B поле **ServerPort** укажем порт, на котором развернут сервер PostgreSQL. Например, **5434**. А в поле **Password** укажем пароль, который задали для сервера базы данных при установке - так сервер WT-приложения будет иметь доступ к базе данных и сможет выполнять запросы.

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

Для настроек **HelpDesk** и **Update** в полях Enabled укажем значение **false**, чтобы сервер учебного проекта не пытался проверять обновления на общем сервере обновлений:

```json
"WorkflowServer": {
  "ServerUrl": "http://lic.wfsys.ru:7070",
  "WorkflowEngineUpdateService": {
    "Name": "WorkflowEngineUpdateService",
    "Port": 9090
  },
  "HelpDesk": {
    "Enabled": false
  },
  "Update": {
    "Enabled": false
  }
}
```

В файле _D:\WorkflowEngine\Template\hosting.json_ для **server.urls** укажем IP-адрес и порт сервера. Т.к. мы разворачиваем проект на своем компьютере, то в качестве IP-адреса оставим localhost. А вот порт нужно указать такой, который еще не используется на локальном компьютере. Например, http://localhost:49707

Скопируем штатные бинарники из папки bin ранее скачанного архива в D:\WorkflowEngine\Template. Необходимо копировать _содержимое папки bin_, а не ее саму.

Так же в папку D:\WorkflowEngine\Template скопируем файл \_start.bat - он нужен для запуска сервера, чтобы не приходилось каждый раз писать команду в командной строке. Для удобства запуска серверной части создадим ярлык на этот файл, переименовав его (например, в "Template SRV").

Запустим наш сервер, кликнув по файлу \_start.bat или по ярлыку на этот файл.

<figure><img src="../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

Отлично! Сервер успешно работает.

{% hint style="success" %}
При первом запуске сервера, может появиться сообщение об отсутствии файла лицензии. Это нормально. Позже сервер приложения зарегистрируется на сервере лицензирования и получит необходимый файл. И если все прошло отлично, то при повторном запуске сервера, такого сообщения уже не будет.
{% endhint %}

{% hint style="info" %}
Сообщения об ошибках на стороне сервера или форм будут регистрироваться в журнале событий Windows. Чтобы создать такой журнал, запустите powershell с правами администратора. И в командной строке выполните команду:

`New-EventLog -Source 'Workflow Engine', 'Workflow Forms' -LogName 'Workflow Technology'`

Просмотреть журнал событий можно выполнив **Панель управления ->** **Администрирование** **-> Просмотр событий** или выполнив поиск в меню "Пуск". В открывшемся окне в левой части развернуть узел **Журналы приложений и служб** и найти созданный журнал событий "Workflow Technology".
{% endhint %}

## Клиентская часть <a href="#client" id="client"></a>

### Архив <a href="#wf-archive" id="wf-archive"></a>

Скачайте бинарники нужной разрядности:

<table data-card-size="large" data-view="cards" data-full-width="false"><thead><tr><th></th><th data-hidden></th><th data-hidden></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>WorkflowForms_v3_x64.zip</td><td></td><td></td><td><a href="https://wfsys.ru/download/WorkflowForms_v3_x64.zip">https://wfsys.ru/download/WorkflowForms_v3_x64.zip</a></td></tr><tr><td>WorkflowForms_v3_x86.zip</td><td></td><td></td><td><a href="https://wfsys.ru/download/WorkflowForms_v3_x86.zip">https://wfsys.ru/download/WorkflowForms_v3_x86.zip</a></td></tr></tbody></table>

Независимо от разрядности структура папок и файлов будет одинаковая. Основные элементы архивов:

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

Как говорилось ранее, клиентская часть построена на базе .Net Core 3.1, что позволило сделать ее портативной. Поэтому в папке **bin** лежат все необходимые файлы, чтобы на клиентских машинах не приходилось отдельно устанавливать .NET Core SDK.

Так же в папке bin есть две подпапки Updater и UpdateService. В папке **Updater**  хранится все необходимое для подпрограммы, которая будет обновлять xml-файлы клиентской части. Папка **UpdateService** содержит dll-файлы и файлы конфигурации для службы обновления исполняемых файлов клиентской части.

В папке **config** лежит файл конфигурации клиентской части - [WorkflowForms.dll.config](https://wfsys.gitbook.io/wt-knowledge-base/platforma-wt/configuration-files/workflowforms.dll.config).

### Разворачивание и настройка <a href="#wf-deployment-and-configuration" id="wf-deployment-and-configuration"></a>

Создадим папку в которую будем восстанавливать клиентскую часть. Например, D:\WorkflowForms\Template.

Скопируем стандартный конфигурационный файл WorkflowForms.dll.config из папки config ранее скачанного архива в D:\WorkflowForms\Template.

В файл конфигурации внесем следующие правки:

* для StartFormFileName укажем абсолютный путь до стартовой формы в папке проекта, которую скачали в начале этой статьи. Например, D:\WT\Projects\Template\Projects\1. Template\Forms\TemplateStart.xml;
* т.к. клиентская и серверная части у нас стоят на одном компьютере, то настройки UseSourceCache и CheckBinaryFiles можно выключить, указав им значение False;
* для AppDataFolder оставим значение по умолчанию, оно все равно не будет использоваться;
* для AnonymousUserName и AnonymousPassword прописать WS\_GUEST и 123 соответственно;
* для ServerUrl укажем IP-адрес и порт сервера, как они прописаны в файле hosting.json. Например, http://localhost:49707.

Скопируем штатные бинарники из папки bin ранее скачанного архива в D:\WorkflowForms\Template.

На файл D:\WorkflowForms\Template\WorkflowForms.exe создайте ярлык и для удобства переименуйте его (например, в Template CLI).

Запустите клиентское приложение и убедитесь, что стартовая форма успешно загружается.

{% hint style="info" %}
Чтобы учебный проект использовать как заготовку для реальных проектов необходимо:

1. В именах xml-файлов форм и серверной части заменить _Template_ на имя бизнес-процесса;
2. В таблице **public.workflow\_type** изменить содержимое полей **name**,  **title**, **path** и **forms\_path**;
3. Переименовать схему **template**;
4. Исправить путь до стартовой формы в файле **WorkflowForms.dll.config**
{% endhint %}
