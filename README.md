# spatialDataStorageSystemAPI
Первый эксперимент на джаве

### Сервис
Подсистема организации хранения пространственных данных предназначена для хранения пространственных данных и обеспечения доступа к этим данным для других подсистем, входящих в состав комплексной информационной системы по управлению документами.

Подсистема выполняет следующие функций:
1. Создать слой
2. Удалить слой
3. Сохранить данные: точка, линия, полигон
4. Удалить данные: точка, линия, полигон
5. Получить перечень слоёв
6. Получить объекты слоя
7. Получить стили слоя
8. Сохранить данные из GeoJSON-а

Подсистема взаимодействует с подсистемой ГИС-интерфейса пользователя, подсистемой пакетной загрузки файлов, подсистемой мониторинга системы.

+ Используемый сервер: Apache Tomcat/9.0.54
+ Используемый язык: Java
+ Используемый фреймворк: Spring Boot
+ Сборка: Maven

Подсистема организации хранения пространственных данных имеет сервис-ориентированную архитектуру.

Для обращения к подсистеме организации хранения пространственных данных необходимо отправить запрос с указанием API функции и передать соответствующие параметры.

| **Название функции**       | **URL API функции**                | **Параметры** | **Тело запроса**  | **Метод** |
| :--------------------: |--------------------------------| ----------|:---------------------------:| -----|
|      Создать слой      | http://localhost:8080/createLayer/{layerName}    | {layerName} |-    | POST |
|      Удалить слой      | http://localhost:8080/deleteLayer/{layerId} |   {layerId} |- |   POST |
| Сохранить данные: точка, линия, полигон  | http://localhost:8080/addObject/{layerId} |    {layerId} |GeoJSON | POST |
| Удалить данные: точка, линия, полигон  |http://localhost:8080/deleteObject/{objectId}| {objectId}|- | POST|
| Получить перечень слоёв  | http://localhost:8080/layers |-|-| GET|
| Получить объекты слоя  | http://localhost:8080/layerObjects/{layerId} | {layerId} |-|GET|
| Получить стили слоя  |http://localhost:8080/layer_styles/{layerId}| {layerId} |-| GET |
| Сохранить данные из GeoJSON-а  | http://localhost:8080/saveData | - |GeoJSON|POST|

### БД

В качестве информационной составляющей используется СУБД PostgreSQL 13. 

Для работы с пространственными данными используется расширение PostGIS.

Реализована физическая модель в соответствии с проектированием. 

В базе данных 3 таблицы: geometry_objects (объекты), layers (слои), styles (стили).

Таблица geometry_objects (объекты) содержит 3 поля: id – идентификатор объекта, data – данные объекта, layer_id – идентификатор слоя, на котором находится объект.
Таблица layers (слои) содержит 2 поля: id – идентификатор слоя, name – название слоя.
Таблица styles (стили) содержит 2 поля: id – идентификатор слоя, к которому относится стиль, color – цвет.

Всё очень просто (даже слишком)

![Бд](https://github.com/artyommm/spatialDataStorageSystemAPI/blob/master/Рисунок1.png)
