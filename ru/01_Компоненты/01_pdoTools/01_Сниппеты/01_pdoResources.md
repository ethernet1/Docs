Сниппет предназначен для вывода списка ресурсов. Является продвинутой заменой для getResources: обладает всеми его возможностями, но лишен недостатков.

Умеет правильно сортировать ТВ параметры, присоединять таблицы при выборке, включать и исключать категории из разных контекстов и еще много чего.

## Параметры
### Параметры выборки ресурсов
Эти параметры определяют, какие ресурсы появятся в генерируемом списке.

Название | Описание | По умолчанию
---|---|---
**&parents** | Список родителей, через запятую, для поиска результатов. Если поставить 0 — выборка не ограничивается. Если id родителя начинается с дефиса, он и его потомки исключаются из выборки. |  Текущий ресурс
**&depth** | Глубина поиска дочерних ресурсов от родителя. | 10
**&resources** | Список ресурсов, через запятую, для вывода в результатах. Если id ресурса начинается с дефиса, этот ресурс исключается из выборки. |
**&context** | Ограничение выборки по контексту ресурсов. |
**&where** | Массив дополнительных параметров выборки, закодированный в JSON.
**&showHidden** | Показывать ресурсы, скрытые в меню. | 1
**&showUnpublished** | Показывать неопубликованные ресурсы. | 0
**&showDeleted** | Показывать удалённые ресурсы. | 0
**&hideContainers** | Отключает вывод контейнеров, то есть, ресурсов с isfolder = 1. | 0
**&select** | Список полей для выборки, через запятую. Можно указывать JSON строку с массивом, например **{"modResource":"id,pagetitle,content"}**.
**&sortby** | Любое поле ресурса для сортировки, включая ТВ параметр, если он указан в параметре «**&includeTVs**». Можно указывать JSON строку с массивом нескольких полей. Для случайно сортировки укажите «**RAND()**» | pagetitle
**&sortdir** | Направление сортировки: по убыванию или возрастанию. | ASC
**&limit** | Ограничение количества результатов выборки. Можно использовать «0». | 0
**&offset** | Пропуск результатов от начала. | 0
**&first** | Номер первой итерации вывода результатов. | 1
**&last** | Номер последней итерации вывода результатов. | Автоматически, по формуле (total + first — 1)
**&loadModels** | Список компонентов, через запятую, чьи модели нужно загрузить для построения запроса. Например: «**&loadModels=\`ms2gallery,msearch2\`**». |
**&tvFilters** | Список фильтров по ТВ, с разделителями AND и OR. Разделитель, указанный в параметре "&tvFiltersOrDelimiter" представляет логическое условие OR и по нему условия группируются в первую очередь. Внутри каждой группы вы можете задать список значений, разделив их «**&tvFiltersAndDelimiter**». Поиск значений может проводиться в каком-то конкретном ТВ, если он указан («**myTV==value**»), или в любом («**value**»). Пример вызова: «**&tvFilters=\`filter2==one,filter1==bar%&#124;&#124;filter1==foo\`**». Обратите внимание: фильтрация использует оператор LIKE и знак "%" является метасимволом. И еще: Поиск идёт по значениям, которые физически находятся в БД, то есть, сюда не подставляются значения по умолчанию из настроек ТВ. 
**&tvFiltersAndDelimiter** | Разделитель для условий AND в параметре «**&tvFilters**». | ","
**&tvFiltersOrDelimiter** | Разделитель для условий OR в параметре «**&&tvFilters**». | "||"

### Параметры шаблонов
Эти параметры устанавливают чанки, которые содержат шаблоны для генерации списка, то есть отвечают за внешний вид.

Название | Описание
---|---
**&returnIds** | Установите значение «1», чтобы вернуть строку со списком id ресурсов, вместо оформленных результатов. Все указанные шаблоны игнорируются.
**&tpl** | Имя чанка для оформления ресурса. Если не указан, то содержимое полей ресурса будет распечатано на экран.
**&tplFirst** | Имя чанка для первого ресурса в результатах. 
**&tplLast** | Имя чанка для последнего ресурса в результатах.
**&tplOdd** | Имя чанка для каждого второго ресурса.
**&tplWrapper** | Чанк-обёртка, для заворачивания всех результатов. Понимает один плейсхолдер: `[[+output]]`. Не работает вместе с параметром «**&toSeparatePlaceholders**».
**&wrapIfEmpty** | Включает вывод чанка-обертки (**&tplWrapper**) даже если результатов нет. | 
**&tplCondition** | Поле ресурса, из которого будет получено значение для выбора чанка по условию в «**&conditionalTpls**».
**&tplOperator** | Необязательный оператор для проведения сравнения поля ресурса в «**&tplCondition**» с массивом значений и чанков в «**&conditionalTpls**».
**&conditionalTpls** | JSON строка с массивом, у которого в ключах указано то, с чем будет сравниваться «tplCondition», а в значениях — чанки, которые будут использованы для вывода, если сравнение будет успешно. Оператор сравнения указывается в «**&tplOperator**». Для операторов типа «**isempty**» можно использовать массив без ключей.
**&outputSeparator** | Необязательная строка для разделения результатов работы.

### Параметры результатов
Эти параметры дополнительно определяют, какие данные и каким способом будут выводиться.

Название | Описание | По умолчанию
---|---|---
**&fastMode** | Быстрый режим обработки чанков. Все необработанные теги (условия, сниппеты и т.п.) будут вырезаны. | 0
**&idx** | Вы можете указать стартовый номер итерации вывода результатов. |
**&totalVar** | Имя плейсхолдера для сохранения общего количества результатов. | total
**&includeContent** | Включаем поле «*content*» в выборку. | 0
**&includeTVs** | Список ТВ параметров для выборки, через запятую. Например: «**action,time**» дадут плейсхолдеры `[[+action]]` и `[[+time]]`. |
**&prepareTVs** | Список ТВ параметров, которые нужно подготовить перед выводом. | «1», что означает подготовку всех ТВ, указанных в "&includeTVs"
**&processTVs** | Список ТВ параметров, которые нужно обработать перед выводом. Если установить в «1», будут обработаны все ТВ, указанные в «**&includeTVs=``**». |
**&tvPrefix** | Префикс для ТВ параметров. | tv
**&scheme** | Схема формирования url, передаётся в modX::makeUrl(). | -1 (относительно site_url)
**&useWeblinkUrl** | Генерировать ссылку с учетом класса ресурса. | 
**&toPlaceholder** | Если не пусто, сниппет сохранит все данные в плейсхолдер с этим именем, вместо вывода не экран. | 
**&toSeparatePlaceholders** | Если вы укажете слово в этом параметре, то ВСЕ результаты будут выставлены в разные плейсхолдеры, начинающиеся с этого слова и заканчивающиеся порядковым номером строки, от нуля. Например, указав в параметре «myPl», вы получите плейсхолдеры `[[+myPl0]]`, `[[+myPl1]]` и т.д. |
**&showLog** | Показывать дополнительную информацию о работе сниппета. Только для авторизованных в контекте «mgr». | 0

## Примеры
Простейший вывод списка дочерних ресурсов документа с идентификатором 1:
```
[[pdoResources?
	&parents=`1`
	&depth=`0`
	&tpl=`ListRowTpl`
]]
```

Если используется дополнительное поле image, то вызов изменится следующим образом:
```
[[pdoResources?
	&parents=`1`
	&depth=`0`
	&tpl=`ListRowTpl`
	&includeTVs=`image`
]]
```

В чанке **ListRowTpl** за это поле будет отвечать плейсхолдер `[[+tv.image]]`

