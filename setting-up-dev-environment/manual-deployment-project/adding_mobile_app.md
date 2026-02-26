# Добавление мобильного приложения

В этой статье рассмотрим, как настроить серверную часть WorkflowEngine, чтобы мобильное приложение могло взаимодействовать с ней.

Процесс добавления мобильного приложения будет рассматриваться относительно учебного проекта, с которым познакомились в статье [Учебный проект](../educational-project.md).

## План <a href="#plan" id="plan"></a>

#### **Этап 1. Подготовка бинарников и форм** <a href="#step-1" id="step-1"></a>

1. В папке с развернутой серверной частью создать папку \MobileBin\Template, в которой будут храниться бинарники для мобильного приложения Template.\
   Например, D:\WorkflowEngine\Template\MobileBin\Template
2. Скопировать бинарники из папки MobileBin [архива](adding_mobile_app.md#archive) в созданную папку \MobileBin\Template.
3. В папке \Template\Projects\1. Template разархивированного учебного проекта создать папку \MobileForms, в которой будут храниться xml-файлы форм мобильного приложения.\
   Например, D:\WT\Projects\Template\Projects\1. Template\MobileForms
4. Скопировать содержимое папки MobileForms из [архива](adding_mobile_app.md#archive) в созданную папку MobileForms.

#### Этап 2. Настройка конфига <a href="#step-2" id="step-2"></a>

1. В файл конфигурации D:\WorkflowEngine\Template\appsettings.json внести правки:
   * В поле MobileFormsFolder проверить, совпадает ли указанный _путь до папки Projects_ с тем, по которому располагается папка с xml-файлами форм мобильного приложения. По умолчанию это папка  \1. Template\MobileForms. При несовпадении указать верный путь.
   * В поле MobileBinaryPath проверить, совпадает ли указанный _путь до папки MobileBin_ с тем, по которому располагается папка с бинарниками. При несовпадении указать верный путь.
2. В файле D:\WorkflowEngine\Template\hosting.json для server.urls необходимо указать _локальный IP-адрес_ сервера, а не localhost. В конфиге клиентской части для desktop тоже нужно изменить адрес сервера с localhost на локальный IP-адрес.

#### Этап 3. Подготовка базы данных <a href="#step-3" id="step-3"></a>

1. В таблицу public.mobile\_app внести правки:
   * В столбце forms\_path проверить, совпадает ли указанный _относительный путь_ до папки, в которой хранятся xml-файлы форм для мобильного приложения. Путь указывается относительно папки, заданной в поле MobileFormsFolder в файле конфигурации. При несовпадении указать верный путь.
   * В столбце bin\_path проверить, совпадает ли указанный _относительный путь_ до папки, в которой хранятся бинарники. Путь указывается относительно папки, заданной в поле MobileBinaryPath в файле конфигурации. При несовпадении указать верный путь.
2. В таблице public.user для пользователя WS\_GUEST проверить хэш пароля. Мобильное приложение по умолчанию подключается под пользователем WS\_GUEST с паролем wsGuestPwd123. Поэтому установите для пользователя WS\_GUEST этот пароль.

{% hint style="warning" %}
Если в таблице public.user для пользователя WS\_GUEST пришлось сменить пароль, то необходимо в файле WorkflowForms.dll.config (конфиг клиентской десктопной части) в поле AnonymousPassword указать пароль wsGuestPwd123, чтобы десктопный клиент продолжал работать с серверной частью.
{% endhint %}

Далее подробнее рассмотрим каждый пункт плана.

При возникновении ошибки в процессе разворачивания проекта вернитесь к этому плану и проверьте каждый его пункт.

## Архив <a href="#archive" id="archive"></a>

Скачайте архив с бинарниками и xml-файлами форм:

{% file src="../../.gitbook/assets/WorkflowMobileForms.zip" %}

Архив содержит две папки:

* MobileBin - папка с бинарниками для мобильных приложений;
* MobileForms - папка с xml-файлами стартовой формы и формы настроек.

## **Подготовка бинарников и форм** <a href="#preparing-binaries-and-forms" id="preparing-binaries-and-forms"></a>

В папке, в которую [развернули серверную часть](https://wfsys.gitbook.io/workflow-technology/setting-up-dev-environment/manual-deployment-project#we-deployment-and-configuration), например, D:\WorkflowEngine\Template, создадим папку MobileBin\Template для бинарников мобильного приложения. В новую папку D:\WorkflowEngine\Template\MobileBin\Template скопируем файлы из папки MobileBin [архива](adding_mobile_app.md#archive_mobile_forms).

В папке \Template\Projects\1. Template [разархивированного учебного проекта](../educational-project.md#project-structure) создадим папку \MobileForms, в которой будут храниться xml-файлы форм мобильного приложения. Например, D:\WT\Projects\Template\Projects\1. Template\MobileForms. Скопируем содержимое папки MobileForms из [архива](adding_mobile_app.md#archive_mobile_forms) в созданную папку MobileForms.

## Настройка конфига <a href="#setting-up-config" id="setting-up-config"></a>

Чтобы мобильное приложение могло взаимодействовать с серверной частью WorkflowEngine, нужно показать серверу, в каких папках лежат бинарники и xml-файлы форм. Зная пути до папок, сервер сможет отдавать файлы мобильным приложениям для скачивания на устройство.

Первым делом в файле конфигурации D:\WorkflowEngine\Template\appsettings.json добавим строки:

```json
"MobileFormsFolder": "D:\\WT\\Projects\\Template\\Projects",
"MobileBinaryPath": "D:\\WorkflowEngine\\Template\\MobileBin",
```

* В поле **MobileFormsFolder** указывается путь до папки Projects, в которой будет происходить поиск папки с xml-файлами форм.&#x20;
* В поле **MobileBinaryPath** указывается путь до папки MobileBin, в которой будут располагаться подпапки с бинарниками.

Для удобства строки можно добавить следом за полями FormsFolder и BinaryPath, которые описывают пути до аналогичных файлов десктопной части.

## Подготовка базы данных <a href="#preparing-the-database" id="preparing-the-database"></a>

#### Регистрация приложения <a href="#app-registration" id="app-registration"></a>

Затем необходимо зарегистрировать мобильное приложение в базе данных, для этого создадим таблицу **public.mobile\_app** и добавим в нее запись:

<figure><img src="../../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

<details>

<summary>SQL-запросы на создание таблицы public.mobile_app и добавление записи</summary>

Создание таблицы:

```sql
CREATE SEQUENCE mobile_app_id_seq;
CREATE TABLE public.mobile_app
(
  mobile_app_id smallint NOT NULL DEFAULT nextval('mobile_app_id_seq'::regclass),
  name character varying NOT NULL,
  title character varying NOT NULL,
  bin_path character varying NOT NULL,
  forms_path character varying NOT NULL,
  start_form_path character varying NOT NULL,
  by_default boolean NOT NULL,
  CONSTRAINT pk_mobile_app_id PRIMARY KEY (mobile_app_id),
  CONSTRAINT un_mobile_app_name UNIQUE (name),
  CONSTRAINT un_mobile_app_bin_path UNIQUE (bin_path),
  CONSTRAINT un_mobile_app_forms_path UNIQUE (forms_path)
);
```

Добавление записи:

```sql
INSERT INTO public.mobile_app(
  name,
  title,
  bin_path,
  forms_path,
  start_form_path,
  by_default
)
VALUES (
  'Template',
  'Template',
  'Template',
  '1. Template\MobileForms',
  'TemplateEmptyStart.xml',
  false
);
```

</details>

Колонка **name** содержит ключ, который совпадает с настройкой MobileAppName в конфиге мобильного приложения. Когда в проекте есть несколько мобильных приложений, то этот ключ помогает серверной части определять, какое приложение запрашивает файлы, и по каким путям их можно найти, чтобы отдать приложению.

Колонка **title** хранит имя проекта, которое будет отображаться в списке выбора типа мобильного приложения. Если в проекте используется несколько приложений, и в настройке MobileAppName в конфиге приложения не указан тип, то при первом запуске приложения пользователь сможет сам выбрать тип из доступных.

Колонка **bin\_path** содержит _относительный путь_ до папки, в которой находятся бинарные файлы мобильного приложения. Путь указывается относительно папки, заданной в поле MobileBinaryPath в файле конфигурации appsettings.json.\
Например, при указанных значениях, сервер будет искать бинарные файлы мобильного приложения в папке D:\WorkflowEngine\Template\MobileBin\Template.

Колонка **forms\_path** содержит _относительный путь_ до папки, в которой хранятся xml-файлы форм для мобильного приложения. Путь указывается относительно папки, заданной в поле MobileFormsFolder в файле конфигурации appsettings.json.\
Например, при указанных значениях, сервер будет искать xml-файлы форм мобильного приложения в папке D:\WT\Projects\Template\Projects\1. Template\MobileForms.

Колонка **start\_form\_path** хранит название файла стартовой формы, который должен находиться в папке из колонки forms\_path.

Колонка **by\_default** определяет приложение по умолчанию. Может быть не больше одного приложения по умолчанию.

#### Гостевая учетка <a href="#ws_guest" id="ws_guest"></a>

Мобильное приложение по умолчанию подключается под пользователем WS\_GUEST с паролем wsGuestPwd123. Поэтому установите для пользователя WS\_GUEST этот пароль, выполнив запрос:

```sql
CREATE EXTENSION pgcrypto;

UPDATE public.user
SET user_password = encode(digest('wsGuestPwd123', 'sha512'), 'hex') 
WHERE user_name = 'WS_GUEST';

DROP EXTENSION pgcrypto;
```

{% hint style="warning" %}
Если в таблице public.user для пользователя WS\_GUEST пришлось сменить пароль, то необходимо в файле WorkflowForms.dll.config (конфиг клиентской десктопной части) в поле AnonymousPassword указать пароль wsGuestPwd123, чтобы десктопный клиент продолжал работать с серверной частью.
{% endhint %}
