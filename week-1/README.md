# Проектирование системы, неделя 1.

## Чеклист

[Требования к системе](requirements.md).

- [x] Сделайте [event storming модель](event_storming.md) проекта. 
- [x] Текстом опишите логику по которой сгруппировали команды и события в контексты.
- [x] Сделайте [модель данных](data_model.md) для требуемой системы
- [x] Сделайте [общую модель всех полученных коммуникаций](communication_model.md) в системе
- [x] Выберите подходящую реализацию проекта (монолит или сервисы, как элементы системы связаны между собой).
- [x] Текстом опишите, почему была выбрана именно такая структура, какие варианты рассматривались и по каким причинам было выбрано итоговое решение.
- [x] Если были выбраны сервисы — текстом опишите, почему были выбраны синхронные или асинхронные коммуникации.
- [x] Опишите спорные места и (или) места, которые вам кажутся критичными на данный момент.

## Схема реализации проекта

Поскольку было выделено всего 4 сильно изолированных бизнес-контекста, целесообразно реализовать отдельный (макро)сервис для каждого контекста и, при необходимости,
отдельный сервис рассылки оповещений.  

Это позволит сохранить баланс между низким TTM и изоляцией бизнес-процессов друг от друга, что упростит поддержание системы и релиз новой функциональностив долгосрочной перспективе.

Для упрощения начальной реализации, все коммуникации в системе можно сделать синхронными, допуская потенциальный провал некритичных коммуникаций (например, оповещения).
При условии инкапсуляции реализации коммуникаций на уровне кода, это позволит постепенно переходить на асинхронные коммуникации, когда это потребуется.

## Спорные и критичные места

* Финансовый мониторинг и аудит системы - нет планов предоставления отчётности и каких-либо требований на этот счёт.
* Сервис ставок - насколько тщательно нужно продумывать модель взаимодействия с сервисом, чтобы он не повлиял на основной фунционал системы.
* Состояние услуги - модель статусов, консистентность перехода между статусами.
* Пользователи системы - стоит ли выделить всё, связанное с логином пользователей, в отдельный сервис в дальнейшем.