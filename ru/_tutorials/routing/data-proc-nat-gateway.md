# Настройка сети для {{ dataproc-name }}

В этом руководстве описано создание кластера {{ dataproc-name }} с настройкой подсетей и NAT-шлюза.

## Создайте ресурсы {#deploy-infrastructure}

Вам необходимо создать:

* сеть;
* подсеть;
* NAT-шлюз и таблицу маршрутизации;
* группу безопасности для кластера;
* сервисный аккаунт для кластера;
* бакет, в котором будут храниться зависимости заданий и результаты их выполнения;
* кластер {{ dataproc-name }}.

{% list tabs %}

- Вручную

    1. [Создайте сеть](../../vpc/operations/network-create.md) с именем `data-proc-network`, при создании выключив опцию **Создать подсети**.
    1. В сети `data-proc-network` [создайте подсеть](../../vpc/operations/subnet-create.md) со следующими параметрами:

        * **Имя** — `data-proc-subnet-a`.
        * **Зона** — `{{ region-id }}-a`.
        * **CIDR** — `192.168.1.0/24`.

    1. [Создайте NAT-шлюз](../../vpc/operations/create-nat-gateway.md) и таблицу маршрутизации с именем `data-proc-route-table` в сети `data-proc-network`. Привяжите таблицу к подсети `data-proc-subnet-a`.

    1. В сети `data-proc-network` [создайте группу безопасности](../../vpc/operations/security-group-create.md) с именем `data-proc-security-group` и следующими правилами:

        * По одному правилу для входящего и исходящего служебного трафика:

            * Диапазон портов — `{{ port-any }}`.
            * Протокол — `Любой` (`Any`).
            * Источник — `Группа безопасности`.
            * Группа безопасности — `Текущая` (`Self`).

        * Правило для исходящего HTTPS-трафика:

            * Диапазон портов — `{{ port-https }}`.
            * Протокол — `TCP`.
            * Назначение — `CIDR`.
            * CIDR блоки — `0.0.0.0/0`.

    1. [Создайте сервисный аккаунт](../../iam/operations/sa/create.md) `data-proc-sa` с ролями:

        * [mdb.dataproc.agent](../../iam/concepts/access-control/roles.md#mdb-dataproc-agent);
        * [storage.uploader](../../iam/concepts/access-control/roles.md#storage-uploader);
        * [storage.viewer](../../iam/concepts/access-control/roles.md#storage-viewer).

    1. [Создайте бакет {{ objstorage-full-name }}](../../storage/operations/buckets/create.md).

    1. [Создайте кластер {{ dataproc-name }}](../../data-proc/operations/cluster-create.md) любой подходящей конфигурации со следующими настройками:

        * **Сервисный аккаунт** — `data-proc-sa`.
        * **Формат указания бакета** — `Список`.
        * **Имя бакета** — выберите созданный ранее бакет.
        * **Сеть** — `data-proc-network`.
        * **Группы безопасности** — `data-proc-security-group`.

- С помощью {{ TF }}

    1. Если у вас еще нет {{ TF }}, [установите и настройте](../../tutorials/infrastructure-management/terraform-quickstart.md#install-terraform) его.
    1. [Скачайте файл с настройками провайдера](https://github.com/yandex-cloud/examples/tree/master/tutorials/terraform/provider.tf). Поместите его в отдельную рабочую директорию и [укажите значения параметров](../../tutorials/infrastructure-management/terraform-quickstart.md#configure-provider).
    1. [Скачайте файл конфигурации кластера](https://github.com/yandex-cloud/examples/blob/master/tutorials/terraform/data-proc-nat-gateway.tf) в ту же рабочую директорию.

        В файле описаны:

        * сеть;
        * подсеть;
        * NAT-шлюз и таблица маршрутизации;
        * группы безопасности;
        * сервисный аккаунт для работы с ресурсами кластера;
        * бакет, в котором будут храниться зависимости заданий и результаты их выполнения;
        * кластер {{ dataproc-name }}.

    1. Укажите в файле конфигурации все необходимые параметры.

    1. Выполните команду `terraform init` в рабочей директории с конфигурационными файлами. Эта команда инициализирует провайдер, указанный в конфигурационных файлах, и позволяет работать с ресурсами и источниками данных провайдера.

    1. Проверьте корректность файлов конфигурации {{ TF }} с помощью команды:

        ```bash
        terraform validate
        ```

        Если в файлах конфигурации есть ошибки, {{ TF }} на них укажет.

    1. Создайте необходимую инфраструктуру:

        1. Выполните команду для просмотра планируемых изменений:

            ```bash
            terraform plan
            ```

            Если конфигурации ресурсов описаны верно, в терминале отобразится список изменяемых ресурсов и их параметров. Это проверочный этап: ресурсы не будут изменены.

        1. Если вас устраивают планируемые изменения, внесите их:

            1. Выполните команду:

                ```bash
                terraform apply
                ```

            1. Подтвердите изменение ресурсов.

            1. Дождитесь завершения операции.

    В указанном каталоге будут созданы все требуемые ресурсы. Проверить появление ресурсов и их настройки можно в [консоли управления]({{ link-console-cloud }}).

{% endlist %}

## Удалите созданные ресурсы {#clear-out}

{% list tabs %}

Если созданные ресурсы вам больше не нужны, удалите их:

- Вручную

    1. [Удалите кластер {{ dataproc-name }}](../../data-proc/operations/cluster-delete.md).
    1. Если вы зарезервировали публичные статические IP-адреса, освободите и [удалите их](../../vpc/operations/address-delete.md).
    1. [Удалите подсеть](../../vpc/operations/subnet-delete.md).
    1. Удалите таблицу маршрутизации и NAT-шлюз.
    1. [Удалите сеть](../../vpc/operations/network-delete.md).

- С помощью {{ TF }}

    Чтобы удалить инфраструктуру, [созданную с помощью {{ TF }}](#deploy-infrastructure):

    1. В терминале перейдите в директорию с планом инфраструктуры.

    1. Удалите конфигурационный файл `data-proc-nat-gateway.tf`.

    1. Проверьте корректность файлов конфигурации {{ TF }} с помощью команды:

        ```bash
        terraform validate
        ```

        Если в конфигурационных файлах есть ошибки, {{ TF }} на них укажет.

    1. Подтвердите изменение ресурсов.

        1. Выполните команду для просмотра планируемых изменений:

            ```bash
            terraform plan
            ```

            Если конфигурации ресурсов описаны верно, в терминале отобразится список изменяемых ресурсов и их параметров. Это проверочный этап: ресурсы не будут изменены.

    1. Если вас устраивают планируемые изменения, внесите их:

        1. Выполните команду:

            ```bash
            terraform apply
            ```

        1. Подтвердите изменение ресурсов.

        1. Дождитесь завершения операции.

    Все ресурсы, которые были описаны в конфигурационном файле, будут удалены.

{% endlist %}