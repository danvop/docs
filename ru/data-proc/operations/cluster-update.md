# Изменение кластера

После создания кластера вы можете изменить его дополнительные настройки.

{% list tabs %}

* Консоль управления

    1. Перейдите на страницу каталога и выберите сервис **{{ dataproc-name }}**.
    1. Выберите кластер и нажмите кнопку **Изменить кластер** на панели сверху.
    1. Измените дополнительные настройки кластера:

        **Защита от удаления** — управляет защитой кластера от непреднамеренного удаления пользователем.

        Включенная защита не помешает подключиться к кластеру вручную и удалить данные.

    1. Нажмите кнопку **Сохранить изменения**.

* CLI

    {% include [cli-install](../../_includes/cli-install.md) %}

    {% include [default-catalogue](../../_includes/default-catalogue.md) %}

    1. Посмотрите описание команды CLI для изменения кластера:

        ```bash
        yc dataproc cluster update --help
        ```

    1. Чтобы защитить кластер от непреднамеренного удаления пользователем вашего облака, задайте значение `true` для параметра `--deletion-protection`:

        ```bash
        yc dataproc cluster update <идентификатор или имя кластера> \
           --deletion-protection=<защита от удаления кластера: true или false>
        ```

        Включенная защита не помешает подключиться к кластеру вручную и удалить данные.

        Идентификатор и имя кластера можно получить со [списком кластеров в каталоге](./cluster-list.md#list).

{% endlist %}