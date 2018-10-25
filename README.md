
# Описание

Python-пакет, обеспечивающий коммуникацию между Carrier (https://github.com/EduScaled/carrier) и  3th-party приложением

Используемый стек: ```python3.7```

# Установка

1. В вашем виртуальном окружении выполнить комманду ```pip install git+https://github.com/EduScaled/carrier-package```

# Использование

**Раздел будет доработан.**

Пакет представлен тремя основными объектами, а именно ```IncomingMessage```, ```OutgoingMessage``` и ```MessageManager```.

Первые два объекта отвечают, соответственно, за входящие и исходящие сообщения.  Третий объект позволяет обрабатывать полученные и отправлять исходящие сообщения.

```IncomingMessage``` имеет class-method ```create_from_bytes```, который в качестве параметра принимает последовательность байт (предположительно, от входящего http-запроса), который на основе этих данных создает и возвращает объект  ```IncomingMessage```. **Валидации объекта пока не производится, при передачи неверной последовательности приведет вызову ошибки**. С полученным объектом уже можно производить произвольные манипуляции. Предполагается дальнейшая его передача в объект ```MessageManager``` для обработки зарегистрированных в данном объекте обработчиков событий.

```OutgoingMessage``` - объект, содержащий информацию для отправки.
Создается стандартным конструктором, передается два параметра - ```topic``` и ```message``` (**формат передаваемого сообщения пока не определен, предполагается ...**) . Подразумевается, что message - это строка, то есть если это json-объект, то требуется его преобразовать в строку.

```message = OutgoingMessage(topic="<topic>", message="<message>")```

```MessageManager``` - объект, отвечающий за "прослушку" и "отправку" сообщений. Можно создавать несколько инстансов объекта (на разные топики и на разные транспортные приложения).

```to_listen = MessageManager(topics=["<topic>", "<topic>"], host="<host>", port="<port>")```

Таким образом задается объект для "прослушки" переданных топиков от приложения на указанному хосту и порту. 
Для обработки полученных сообщений необходимо зарегистрировать один или несколько т.н. event listener'ов.

```to_listen.register_event_handler(should_handle=<function>, handler=<function>)```. 

Обе функции на вход принимают объект IncomingMessage, первая определяет, реагировать ли на сообщение, вторая - если да, то как.

```

```