# Группы виртуальных машин

#### Что такое {{ ig-name }}? {#what-is}

{{ ig-name }} — это компонент, с помощью которого можно создавать, эксплуатировать и масштабировать группы однотипных виртуальных машин в инфраструктуре {{ compute-full-name }}.

С {{ ig-name }} вы можете:

- создавать группы с необходимым количеством виртуальных машин и параметрами производительности;
- увеличивать вычислительные мощности по мере необходимости и уменьшать, если нагрузка снизилась.

Вы взаимодействуете с группой виртуальных машин как с единой сущностью в инфраструктуре {{ compute-full-name }}. Благодаря этому вы можете управлять внутренними настройками группы виртуальных машин в соответствии с требованиями вашего приложения.

#### Как рассчитывается стоимость использования групп виртуальных машин? {#ig-cost}

Создание группы виртуальных машин не тарифицируется.

Все остальные услуги {{ yandex-cloud }}, например создание виртуальных машин или выделение внешних IP-адресов, тарифицируются обычным образом.

#### Как не переплатить лишнего? {#not-overpaying}

Чтобы выбрать подходящее вам количество виртуальных машин и платить минимальную стоимость:

- Оцените, сколько потребуется вычислительных ресурсов для вашего сервиса, и посмотрите примеры расчетов и [правила тарификации](../../compute/pricing.md) для {{ compute-full-name }}.
- Старайтесь чаще следить за нагрузкой на сервис в разное время суток.
