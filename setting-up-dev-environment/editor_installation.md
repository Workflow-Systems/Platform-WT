# Установка Workflow XML Editor

Для начала скачайте Eclipse с официального [сайта](https://www.eclipse.org/downloads/packages/installer).\
Инструкция по установке плагина WorkflowForms Editor приведена ниже.

## Установка плагина Workflow XML Editor <a href="#installing-plugin" id="installing-plugin"></a>

#### Шаг 1 <a href="#step-1" id="step-1"></a>

Запустим Eclipse. При открытии будет просьба указать папку для **Workspace** - там, где будут храниться настройки Eclipse.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FC6P3jzCj5SOtFutgARLC%2Fimage.png?alt=media&#x26;token=ef517a25-ecce-467e-83b0-e16f0e65638d" alt=""><figcaption></figcaption></figure>

В поле Workspace укажем, например, **D:\WorkflowEditor** и поставим галочку **Use this as the default and do not ask again**. Жмем Launch.

Запустится среда разработки. Закроем окно приветствия.

#### Шаг 2 <a href="#step-2" id="step-2"></a>

Теперь пришло время установить плагин Workflow XML Editor. Для этого выберем пункт меню **Help -> Install New Software**.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2Fo576uE23sXj8copY3mvj%2F01.png?alt=media&#x26;token=a37da824-76ba-4cfa-b43a-2ba75a2f861e" alt=""><figcaption></figcaption></figure>

Откроется окно доступного программного обеспечения:

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

В поле **Work with** укажем адрес **http://update.wfsys.ru:6767**, нажмем Enter.&#x20;

Вероятно, что на этом шаге возникнет сообщение вида:

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Если сообщение о невозможности прочитать репозиторий не получили, то можно переходить к следующему [шагу](editor_installation.md#step-3).

Чтобы исправить эту ошибку, нажмите на кнопку **Manage**, расположенную справа от поля поле Work with:

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

В открывшемся окне в левой части перейдем к секции **Trust**, а в правой откроем вкладку **Authorities**:

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

В правой части окна нажмем кнопку **Add**, чтобы добавить доверенный источник. Откроется окно. в котором укажем наш адрес:

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Нажмем OK и вернемся в предыдущее окно.&#x20;

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

Мы видим, что наш источник добавился в таблицу. Теперь внизу правой части окна необходимо указать правила для протоколов в панели **Protocol Rules**. В выпадающем списке для протокола **http** укажем вариант **Allow**.

Отлично, теперь жмем Apply and Close, чтобы продолжить установку плагина.

#### Шаг 3 <a href="#step-3" id="step-3"></a>

В списке плагинов появится раздел **Uncategorized**, отметим его галочкой.

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Жмем Next. И следуем инструкциям установщика плагина, завершающим действием которого будет перезапуск Eclipse.

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

Согласимся с условиями лицензионного соглашения и нажмем Finish:

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

В процессе установки Eclipse может спросить о доверии к источнику контента:

<figure><img src="../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

Жмем кнопку Trust Selected.

По окончании установки потребуется перезагрузить Eclipse.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2Fq2OB1patkDCW5jsiEftq%2Fimage.png?alt=media&#x26;token=1ba78023-f30a-4d36-96f8-6f90af124e1c" alt=""><figcaption></figcaption></figure>

## Настройка среды разработки <a href="#setting-up-dev-environment" id="setting-up-dev-environment"></a>

### Смена перспективы <a href="#change-of-perspective" id="change-of-perspective"></a>

Сменим перспективу со стандартной Java EE на нашу Workflow Development.&#x20;

В правой верхней части экрана есть кнопка-иконка **Java**. Нажмем на нее правой кнопкой мыши, в появившемся контекстном меню выберем пункт Close.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FKGirFgoYPblevAo769w3%2F05.png?alt=media&#x26;token=e6d1adf2-b45d-42ed-ae45-87b7db80048e" alt=""><figcaption></figcaption></figure>

Там же в правой верхней части экрана будет кнопка-иконка **Open Perspective**. Нажмем на нее.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FmNhDurYr5LhSGHo86r06%2F06.png?alt=media&#x26;token=387a9d71-0e33-41c8-ac6e-e7b311dbdde4" alt=""><figcaption></figcaption></figure>

В открывшемся окне выберем пункт **Workflow Development**:

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2Fae8BbjwL71z4b4tbWMir%2Fimage.png?alt=media&#x26;token=3605caab-c9ba-44ed-9c84-ec283dbac7f2" alt=""><figcaption></figcaption></figure>

Жмем Open.

Мы видим абсолютно чистую среду разработки:

<figure><img src="../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

Первым делом настоим панель Project Explorer, в которой будет отображаться список проектов и их файлов. Для этого выберем в главном меню пункт **Windows-> Show View -> Other**:

<figure><img src="../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

В открывшемся меню в разделе **General** найдем элемент **Project Explorer**:

<figure><img src="../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

Жмем Open и видим, что  появилась новая вкладка:

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

Зажимая левую клавишу мыши по имени вкладки, настоим положение панелей Project Explorer и Outline следующим образом:

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

### Настройка синтаксиса платформы <a href="#setting-up-platform-syntax" id="setting-up-platform-syntax"></a>

Подключим схему wXSD, которая описывает структуры XML-документов в рамках платформы WT. Для этого скачаем архив по ссылке ниже и распакуем его в любое удобное место, например, в папку с установленным Eclipse.

{% file src="../.gitbook/assets/Workflow XML Editor.zip" %}
Workflow XML Editor - wXSD
{% endfile %}

Перейдем к пункту меню **Window -> Preferences**.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FzIYaXnGCmrDuOsAI4T5J%2F03.png?alt=media&#x26;token=b9c4578f-1cff-448f-8daf-06df0db38732" alt=""><figcaption></figcaption></figure>

И в открывшемся окне свойств в левой части перейдем к секции **Workflow Forms Editor**.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FkTLZeYhyqz3ttcOGkoV3%2Fimage.png?alt=media&#x26;token=84de35b3-af9d-4ff3-ab6f-1a2e3df6dc85" alt=""><figcaption></figcaption></figure>

В правой части окна для поля **Scheme file location** укажем абсолютный путь до файла \wXSD\Forms\Form.xml из папки, в которую распаковали ранее скачанный архив. Например, D:\Programms\Eclipse\wXSD\Forms\Form.xml.

Для полей **Mobile** **scheme file location** и **Web scheme file location** укажем пути до файлов Form.xml из папок \wXSD\MobileForm и \wXSD\WebForms соответственно.

Для поля **Workflow scheme file location** укажем абсолютный путь до файла \wXSD\Workflow\Workflow.xml из той же папки.&#x20;

Остальные поля оставим по умолчанию. Жмем Apply.

В этом же окне в левой части перейдем к секции **Workflow Forms Editor -> Content Assist**.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FyIJort0tbBWihIE5VdXM%2Fimage.png?alt=media&#x26;token=d585c07e-0af0-4d1d-84c4-26ba930d7c76" alt=""><figcaption></figcaption></figure>

В правой части окна в таблицах **Default Proposal Categories** и **Content Assist Pages** снимем все галочки кроме "Шаблоны" и "Формы", затем нажмите Apply.

В этом же окне в левой части перейдем к секции **Workflow Forms Editor -> Syntax Coloring**.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2Fww67LgNdI1lxYQEYbXXL%2Fimage.png?alt=media&#x26;token=8617cafa-112e-4077-b096-fefedf3512c9" alt=""><figcaption></figcaption></figure>

В правой части окна нажмем кнопку Restore Defaults (находящуюся внизу окна) и затем нажмем Apply.

Эти настройки будут автоматически применяться ко всем проектам, подключенным к редактору.

### Настройка обновлений <a href="#update-configuration" id="update-configuration"></a>

В этом же окне в левой части перейдем к секции **Install/Update -> Automatic Updates**.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2F6ooTiRYqa4SZIcGB1a1D%2Fimage.png?alt=media&#x26;token=8021e31a-60cd-4d60-89e9-72a2f69910bc" alt=""><figcaption></figcaption></figure>

В правой части окна в группе Update schedule выберем пункт Look for updated each time Eclipse is started.

Жмем Apply and Close.

На этом установка и настройка плагина Workflow XML Editor закончена.

## Обзор редактора <a href="#review-of-editor" id="review-of-editor"></a>

В этом разделе рассмотрим элементы Eclipse, которые используются при работе над проектом в рамках редактора Workflow XML Editor.

Ниже приведен пример редактора с проектом Template, который будем разрабатывать в уроках:

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FyiTqzyqgSm0Xg6EdAP58%2Fimage.png?alt=media&#x26;token=b46b9ecc-1456-4ffc-b2c3-0c33238f3581" alt=""><figcaption></figcaption></figure>

#### Панель **Navigator** <a href="#navigator-panel" id="navigator-panel"></a>

Отображает список проектов и их ресурсов: серверные xml-файлы, xml-файлы форм и файлы строковых ресурсов для поддержки языков интерфейса форм.

#### **Область редактирования** <a href="#editing-area" id="editing-area"></a>

Окно с вкладками, содержащее по одной вкладке на редактируемый файл. На рисунке открыто два редактируемых файла: серверный xml-файл (первая вкладка) и xml-файл стартовой формы (вторая вкладка, активная). Вкладка содержит название редактируемого ресурс - имя файла. Если наведем курсор на вкладку, Eclipse отобразит имя папки проекта и имя самого ресурса. Если ресурс не находится в проекте, его путь отображается перед именем папки.

#### Панель **Outline** <a href="#outline-panel" id="outline-panel"></a>

Единственная вкладка в окне, которая показывает структуру редактируемого файла в активной вкладке. Если щелкнуть по имени элемента в этом окне, xml-код, определяющий это имя, появится на вкладке области редактирования. Поэтому панель Outline - это один из способов навигации по большому файлу, содержащему xml-код.

#### Кнопка **Reload patterns** <a href="#reload-patterns-button" id="reload-patterns-button"></a>

Кнопка используется для быстрой загрузки измененных паттернов в редактор без необходимости перезагружать Eclipse.

#### Кнопка **Switch project type**  <a href="#switch-project-type-button" id="switch-project-type-button"></a>

Кнопка используется для указания типа проекта - Desktop, Mobile, Web. Относительно выбранного типа проекта редактор будет использовать соответствующую схему синтаксиса для проверки кода и подсказок при написании кода.
