# Подключение и настройка проекта

## Добавление проекта в редактор <a href="#adding-project-to-editor" id="adding-project-to-editor"></a>

### Добавление проекта <a href="#adding-project" id="adding-project"></a>

Для добавления проекта в редактор перейдем в меню **File -> New -> Workflow Project**.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FWIIh3NlLXyyWTSPOJWt9%2F08.png?alt=media&#x26;token=62ff4ccd-8a1a-4228-97a1-06dd73373bae" alt=""><figcaption></figcaption></figure>

Если в меню нет пункта Workflow Project, то можно выбрать пункт Project и в открывшемся окне выбрать нужный тип проекта:

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

Откроется окно создания нового проекта:

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FyGT7tbvyKA0oKnoce08s%2Fimage.png?alt=media&#x26;token=4f56a02a-7d09-4671-b0f6-acac76ae9c83" alt=""><figcaption></figcaption></figure>

Чтобы добавить существующий проект в редактор, снимем галочку **Use default location** и в поле **Location** укажем путь до папки **..\Template\Projects\1. Template\Forms** учебного проекта.

В поле **Project name** укажем имя проекта, которое будет отображаться в окне Navigator редактора Workflow Editor.

Поле **Project type** указывает редактору тип проекта, а именно схему, которую нужно использовать при работе с файлами проекта. Тип проекта можно будет переключить в процессе работы, через контекстное меню на кнопке **Switch project type**:

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

Жмем Finish, чтобы завершить добавление проекта в редактор.

В окне Project Explorer отображается наш проект, содержащий один файл стартовой формы:

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

### Добавление серверного XML-файла <a href="#adding-server-xml-file" id="adding-server-xml-file"></a>

Добавим к проекту серверный XML-файл. Для этого просто перетащим его из окна Проводника на наш проект в окне Navigator. В открывшемся окне File Operation выбираем пункт Link to files а остальные настройки оставим по умолчанию. Жмем OK.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FALCHWQS5Chrrm1yptqZL%2Fimage.png?alt=media&#x26;token=41d3280b-e9b0-4c93-ac56-6d42f927dbea" alt=""><figcaption></figcaption></figure>

Теперь нам нужно привязать к проекту серверный XML-файл - это необходимо, чтобы редактор мог подсказывать имена SQL-запросов, описанных в этом файле, когда будем создавать загружающие соединения с данными в файлах форм, а так же имена команд, реализованных на стороне сервера.

Сделать это можно в свойствах проекта, для этого перейдем в меню **Project -> Properties**:

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Свойства проекта можно открыть через контекстное меню, кликнув правой кнопкой мыши по имени проекта в окне Project Explorer, и выбрав пункт Properties.
{% endhint %}

И в открывшемся окне свойств проекта в левой части перейдем к секции **Workflow Settings**.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2Fziek7WWRGHTTdmE3EjBa%2Fimage.png?alt=media&#x26;token=ab94c91a-11c9-44e2-b574-50ddea280228" alt=""><figcaption></figcaption></figure>

В правой части окна в блоке Forms так же есть настройка для задания типа проекта.

В блоке Workflows нажмем кнопку Add new workflow.

<figure><img src="../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

* **File**: - имя серверного XML-файла;
* **Name**: имя процесса, с которым связан серверный файл.

В открывшемся окне Workflow жмем кнопку Browse. В новом окне Files видим все файлы в проекте.

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FjgZ7sXwGSraWb6KX9Lvy%2Fimage.png?alt=media&#x26;token=909c8cc4-e295-445a-baf7-2d86b4a4a84b" alt=""><figcaption></figcaption></figure>

Выберем серверный XML-файл и жмем OK. В окне Workflow видим выбранный серверный файл и связанный с ним процесс.

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

Жмем OK.

В окне свойств проекта в таблице добавится серверный файл:

<figure><img src="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M_eBlWEU4C3o2GVEAAr%2Fuploads%2FDyXKVGkEpyi2sAGUHda3%2Fimage.png?alt=media&#x26;token=4756466c-c7d0-45ec-9f8d-11e577fc2dec" alt=""><figcaption></figcaption></figure>

Жмем OK. Теперь серверный XML-файл привязан к проекту.

## Обзор структуры кода <a href="#code-structure-overview" id="code-structure-overview"></a>

В этом разделе кратко рассмотрим основные элементы xml-кода для серверного файла и файлов форм. Подробное описание всех тэгов можно найти в справочнике по серверной части и десктопной части.

{% embed url="https://wfsys.gitbook.io/workflow-forms-syntax/" %}

{% embed url="https://wfsys.gitbook.io/workflow-engine-syntax/" %}

### Серверный xml-файл <a href="#server-xml-file" id="server-xml-file"></a>

Краткий шаблон основных элементов серверной части:

```xml
<?xml version="1.0"?>
<Workflow Schema="">
  <SqlQueries>
    <SqlQuery Name="">
      <Text></Text>
    </SqlQuery>
  </SqlQueries>

  <AccessPoints>
    <AccessPoint Name="" />
  </AccessPoints>

  <Permissions>
    <Permission Name="">
      <AccessPoint Name="" />
      <SqlQuery Name="" />
    </Permission>
  </Permissions>
  
  <Roles>
    <Role Name="">
      <Permissions></Permissions>
    </Role>
  </Roles>

  <Groups>
    <Group Name="">
      <Roles></Roles>
    </Group>
  </Groups>
</Workflow>
```

Необязательный тэг [`<SqlQueries>`](https://wfsys.gitbook.io/workflow-engine-syntax/workflow_engine/sql_queries) - список тэгов [`<SqlQuery>`](https://wfsys.gitbook.io/workflow-engine-syntax/workflow_engine/sql_queries/sql_query), каждый из которых описывает SQL-запрос на получение или изменение данных, хранящихся в базе данных. Один тэг `<SqlQuery>` может содержать последовательность SQL-запросов, которые будут выполняться в рамках одной транзакции.

{% hint style="info" %}
Транзакция - набор операций по работе с базой данных, объединенных в одну атомарную единицу. Если транзакция выполнена успешно, все модификации данных, сделанные в течение транзакции, принимаются и сохраняются в базе данных. Если в результате выполнения транзакции происходят ошибки и должна быть произведена отмена или выполнен откат, все модификации данных будут отменены.
{% endhint %}

Необязательный тэг [\<AccessPoints>](https://wfsys.gitbook.io/workflow-engine-syntax/workflow_engine/access_points) - список точек доступа, которые предоставляют пользователям доступ к элементам форм.

Необязательный тэг [\<Permissions>](https://wfsys.gitbook.io/workflow-engine-syntax/workflow_engine/permissions) - список разрешений на выполнение запросов и команд, а так же точек доступа.

Необязательный тэг [`<Roles>`](https://wfsys.gitbook.io/workflow-engine-syntax/workflow_engine/roles) - список ролей, представляющих наборы разрешений.

Необязательный тэг [`<Groups>`](https://wfsys.gitbook.io/workflow-engine-syntax/workflow_engine/groups) - список групп пользователей с наборами ролей.

### Xml-файл формы <a href="#form-xml-file" id="form-xml-file"></a>

Краткий шаблон основных элементов xml-файла форм десктопного приложения:

```xml
<?xml version="1.0"?>
<Form Name="" Width="" Height="" BackColor="" StartPosition="" StatusBar="">
  <Parameters>
    <Parameter Name=""></Parameter>
  </Parameters>

  <Appearance>
    <Colors>
      <Color Name="" Red="" Green="" Blue="" Alpha="" />
    </Colors>
    <FontStyles>
      <FontStyle Name="" Font="" Size="" />
    </FontStyles>
  </Appearance>

  <DataConnections></DataConnections>

  <Conditions>
    <Condition Name="" Type="" Assembly="Conditions" />
  </Conditions>

  <Commands>
    <Command Name="" Type="" Assembly="Commands" />
  </Commands>
  
  <Executions>
    <Execution>
      <ConditionExpression></ConditionExpression>
      <Commands></Commands>
    </Execution>
  </Executions>

  <MyObjects>
    <MyObject Name="" Type="" Assembly="BaseControls">
      <Top></Top>
      <Left></Left>
      <Height></Height>
      <Width></Width>
    </MyObject>
  </MyObjects>
</Form>
```

Корневым элементом файла является тэг [`<Form>`](https://wfsys.gitbook.io/workflow-forms-syntax/#attributes_form), его атрибуты описывают основные свойства формы.

Необязательный тэг [`<Parameters>`](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/parameters) - список параметров формы, с помощью которых можно передавать данные между формами или хранить промежуточные расчеты на самой форме.

Необязательный тэг [`<Appearance>`](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/appearance) - список шрифтов и цветов для графических элементов формы.

Необязательный тэг [`<DataConnections>`](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/dataconnections) - список соединений с данными для загрузки данных с сервера или сохранения данных на сервере.

Необязательный тэг [`<Conditions>`](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/conditions) - список событийных условий (например, [CellDoubleClickCondition](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/conditions/event_condition/cell_double_click_condition) или [FormLoadedCondition](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/conditions/event_condition/form_loaded_condition)) и условий сравнений (например, [EqualCondition ](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/conditions/comparison_condition/equal_condition)или [IsNullOrEmptyCondition](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/conditions/comparison_condition/is_null_or_empty_condition)).

Необязательный тэг [`<Commands>`](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/commands) - список команд, выполняемых на стороне клиента.

Необязательный тэг [`<Executions>`](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/executions) - конструкции выполнения команд по&#x20;

Необязательный тэг [`<MyObjects>`](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/objects) - список объектов формы, таких как поля ввода ([TextBox](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/objects/textbox) и [NumericBox](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/objects/numericbox)), таблицы ([DatabaseTable](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/objects/databasetable)) или переменных ([Variable](https://wfsys.gitbook.io/workflow-forms-syntax/workflow_forms/objects/variable)).



Чтобы отключить следование структуры кода в окне Outline за кодом в окне редактирования, можно кликнуть по кнопке **View Menu** и в контекстном меню отключим **Link with Editor**:

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>
