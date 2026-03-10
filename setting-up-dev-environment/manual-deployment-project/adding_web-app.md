# Добавление web-приложения

В этой статье рассмотрим, как настроить сервер, чтобы можно было взаимодействовать с web-приложением через браузер.

Процесс добавления web-приложения будет рассматриваться относительно учебного проекта, с которым познакомились в статье [Учебный проект](../educational-project.md).

## План <a href="#plan" id="plan"></a>

#### **Этап 1. Подготовка бинарников** <a href="#step-1" id="step-1"></a>

1. В папке с развернутой серверной частью создать папку \Web, в которой будут храниться бинарники для web-приложения.\
   Например, D:\WorkflowEngine\Template\Web.
2. Скопировать стандартный конфигурационный файлы appsettings.json из папки config [архива](adding_web-app.md#archive) в папку D:\WorkflowEngine\Template\Web.
3. Скопировать бинарники из папки bin [архива](adding_web-app.md#archive) в созданную папку \Web.
4. Скопировать файл \_start.bat из [архива](adding_web-app.md#we-archive) в папку D:\WorkflowEngine\Template\Web.
5. Для удобства запуска серверной части создать ярлык на файл D:\WorkflowEngine\Template\Web\\\_start.bat, переименовав его (например, в Template WEB).

#### Этап 2. Настройка конфига <a href="#step-2" id="step-2"></a>

В файл конфигурации D:\WorkflowEngine\Template\Web\appsettings.json внести правки:

* В поле ServerUrl проверить, совпадает ли указанный адрес с тем, на котором запущена серверная часть WT-приложения. При несовпадении указать верный путь.
* В поле HostUrl указать адрес и порт, на котором будет запущено web-приложение.
* В поле XmlFolder проверить, совпадает ли указанный путь до папки WebForms с тем, по которому располагается папка с xml-файлами форм web-приложения. По умолчанию это папка  \1. Template\WebForms. При несовпадении указать верный путь.
* В полях AnonymousUserName и AnonymousPassword прописать WS\_GUEST и 123 соответственно. В базе данных в таблице public.user для пользователя WS\_GUEST проверить хэш пароля.

Далее подробнее рассмотрим каждый пункт плана.

При возникновении ошибки в процессе разворачивания проекта вернитесь к этому плану и проверьте каждый его пункт.

## Архив <a href="#archive" id="archive"></a>

Скачайте бинарники нужной разрядности:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>WorkflowWebForms_x64.zip</td><td></td></tr><tr><td>WorkflowWebForms_x86.zip</td><td></td></tr></tbody></table>

Независимо от разрядности структура папок и файлов будет одинаковая. Основные элементы архивов:

<figure><img src="../../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

Web-приложение построено на базе .Net Core 6.0, что позволяет сделать его портативным. Поэтому в папке **bin** лежат все необходимые dll-файлы, чтобы на клиентском сервере не приходилось отдельно устанавливать .NET Core SDK.

В папке **config** лежит конфигурационный файл [appsettings.json](https://wfsys.gitbook.io/wt-knowledge-base/platform-wt/configuration-files/web/appsettings-json), хранящий настройки доступа к web-приложению и адрес серверной части.

Файл **\_start.bat** запускает наше web-приложение.

### Разворачивание и настройка <a href="#deployment-and-configuration" id="deployment-and-configuration"></a>

## **Подготовка бинарников и форм** <a href="#preparing-binaries-and-forms" id="preparing-binaries-and-forms"></a>

В папке, в которую [развернули серверную часть](https://wfsys.gitbook.io/workflow-technology/setting-up-dev-environment/manual-deployment-project#we-deployment-and-configuration), например, D:\WorkflowEngine\Template, создадим папку Web для бинарников web-приложения. В новую папку D:\WorkflowEngine\Template\Web скопируем файлы из папки WebBin [архива](adding_web-app.md#archive_mobile_forms).

В папке \Template\Projects\1. Template [разархивированного учебного проекта](../educational-project.md#project-structure) создадим папку \WebForms, в которой будут храниться xml-файлы форм web-приложения. Например, D:\WT\Projects\Template\Projects\1. Template\WebForms. Скопируем содержимое папки WebForms из [архива](adding_web-app.md#archive_mobile_forms) в созданную папку WebForms.

В папке \Template\Projects\1. Template разархивированного учебного проекта создадим папку \Web, в которой будет храниться razor-приложение для сборки исполнительного файла web-приложения. Например, D:\WT\Projects\Template\Projects\1. Template\Web. Скопируем содержимое папки WebApp из [архива](adding_web-app.md#archive) в созданную папку Web.

## Настройка конфига <a href="#setting-up-config" id="setting-up-config"></a>

Чтобы мобильное приложение могло взаимодействовать с серверной частью WorkflowEngine, нужно показать серверу, в каких папках лежат бинарники и xml-файлы форм. Зная пути до папок, сервер сможет отдавать файлы мобильным приложениям для скачивания на устройство.

В файл конфигурации web-приложения D:\WorkflowEngine\Template\Web\appsettings.json внесем правки:

```json
"ServerUrl": "http://localhost:49707",
"HostUrl": "http://localhost:49708",
"XmlFolder": "D:\\WT\\Projects\\Template\\Projects\\1. Template\\WebForms",
```

* В поле **ServerUrl** указывается IP-адрес (или доменное имя) и порт серверной части WT-приложения, к которой будет обращаться web-приложение. Этот адрес указывали в файле _D:\WorkflowEngine\Template\hosting.json_ в поле **server.urls**
* В поле **HostUrl** указывается IP-адрес (или доменное имя) и порт, на котором будет запущено web-приложения и доступно для работы в браузере.
* В поле **XmlFolder** указывается путь до папки WebForms с xml-файлами форм web-приложения.
* В полях AnonymousUserName и AnonymousPassword прописать WS\_GUEST и 123 соответственно. В базе данных в таблице public.user для пользователя WS\_GUEST проверить хэш пароля.

Если необходимо для пользователя WS\_GUEST изменить пароль в базе данных, выполним запрос:

```sql
CREATE EXTENSION pgcrypto;

UPDATE public.user
SET user_password = encode(digest('new_password', 'sha512'), 'hex') 
WHERE user_name = 'WS_GUEST';

DROP EXTENSION pgcrypto;
```

Этот же пароль необходимо указать и в файле конфига.

## Структура проекта <a href="#project-structure" id="project-structure"></a>





