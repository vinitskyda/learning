# Graph changelog

### 18/07/2014
Сейчас имплементация шага в графе выглядит так:

`$$.Script472.prototype.step1__0 = (cb) ->`

С настоящего момента запись без `id` будет синонимом:

`$$.Script.prototype.step1__0 = (cb) ->`

Так тоже работает

vakhov [6:50 PM]
Я старые шаги не трогал, но **`update_script` новые шаги будет вставлять без `id`** - не удивляйтесь, это правильно


### 22/08/2014
Вместо `(s2:comment); (s1)-->(s2);` можно писать `(s2:comment); s1-->s2;`


### 16/09/2014
После вызова функции `click()` теперь помимо `@obj` с объектом, который кликнули,есть `@event` с координатами клика:
`@event.pageX`
`@event.pageY`
(как у jQuery-ого eventObject)