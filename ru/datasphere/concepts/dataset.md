# Датасеты в {{ ml-platform-name }}

_Датасет в {{ ml-platform-name }}_ — это механизм хранения информации, который предоставляет быстрый доступ к большим объемам данных. Датасеты позволяют хранить до 4 ТБ, при этом доступ к данным будет быстрее, чем к основному хранилищу проекта.

{% note tip %}

Чем больше выделенный для датасета [диск](../../compute/concepts/disk.md), тем выше скорость чтения данных.

{% endnote %}

Создание и наполнение датасета происходит во время инициализации. После инициализации датасет нельзя изменить, он будет доступен только для чтения. Если вы хотите добавить файлы в датасет, создайте его заново.

Датасеты не включены в основное хранилище проекта и [тарифицируются](../pricing.md#prices-datasets) отдельно.

Как и другими ресурсами, датасетами можно [делиться](../operations/data/dataset.md#share) в сообществе, чтобы использовать данные в нескольких проектах.

При активации в проекте диск с датасетом монитуется к хранилищу проекта. Файлы активированного датасета можно читать как локальные файлы хранилища проекта по пути `/home/jupyter/mnt/datasets/<имя датасета>`.

Одновременно в проекте может быть активировано до 3 датасетов. Вы можете активировать и деактивировать датасеты проекта прямо во время работы без перезагрузки проекта. Все ограничения {{ ml-platform-name }} см. в разделе [{#T}](limits.md).

## Информация о датасете как ресурсе {#info}

О каждом датасете хранится следующая информация:

* имя;
* статус подключения к проекту;
* имя пользователя, создавшего датасет;
* дата создания датасета в формате в [UTC](https://ru.wikipedia.org/wiki/Всемирное_координированное_время), например `18 июля 2022 г., 14:23`.

Чтобы посмотреть подробную информацию о датасете, нажмите на его название в списке датасетов проекта. На вкладке **Обзор** конкретного датасета можно увидеть:

* [зону доступности](../../overview/concepts/geo-scope.md), в которой хранится датасет;
* размер;
* код инициализации.

#### См. также {#see-also}

* [{#T}](../operations/data/dataset.md)
