# Tutor

## Методы, часто использующиеся при программировании карт

 * [play_button](#play_button)
 * [t](#t)
 * [Speaker-методы](#speaker-методы)
   * [speaker](#speaker)
   * [speaker_disabled](#speaker_disabled)
   * [speaker_clear](#speaker_clear)
   * [say](#say)
 * [Keypad-методы](#keypad-методы)
   * [keypad_start](#keypad_start)
   * [keypad_finish](#keypad_finish)
   * [button_ok_toggle](#button_ok_toggle)
   * [prevent_default_init](#prevent_default_init)
   * [prevent_default_destroy](#prevent_default_destroy)


#### `play_button`

Метод, вызывающий кнопку, ознаменующую начало карты.

Пример использования: 

```
@tutor.play_button => cb()
```

Параметры:

```
cb                - callback
opt               - параметры зависят от той play_button, которая подключена к лейауту
```

#### `t`

Метод, возвращающий значение "text" константы, преобразованной, заменяя `$num` на соответствующее значение из массива `args` и заменяя `%num{word1}{word2}{word3}`, в соответствии с правилами языка для числа с номером `num` из массива `args`
en-fr word1-единственное число, word2-множественное число
ru word1 - 1,21,31..., word2 - 2,3,4,22..., word3 - 5,6,7,11...

Пример использования:

```
str = "$1 %1{мальчик съел}{мальчика съели}{мальчиков съели} $2 %2{апельсин}{апельсина}{апельсинов}
args = [1, 1], result = 1 мальчик съел 1 апельсин
args = [1, 5], result = 1 мальчик съел 5 апельсинов
args = [5, 1], result = 5 мальчиков съели 1 апельсин
args = [5, 1], result = 5 мальчиков съели 1 апельсин
args = [3, 3], result = 3 мальчика съели 3 апельсина
```

Параметры:

```
args                   - [label, arg0, arg1, ...]
  * label              - имя константы
  * arg0 etc           - значения для замены
```

### Speaker-методы

[to top](#tutor)

Методы, связанные с динамиком.

#### `speaker`

Добавление внутрь элемента динамика, если проигрывание звука возможно.

Пример использования:

```
если:   @tutor.t("task", @salt.final)
то:     @tutor.speaker(line, size:"m", color:"white", ev:"mousedown", label:"task", option:@salt.final, args:[@salt.final])
или:    @tutor.speaker(line, size:"m", label:"task", option:@salt.final, args:[@salt.final])
или:    @tutor.speaker(line, size:"s", label:"task", option:another_key, args:[@salt.final])
или:    @tutor.speaker(line, label:"task", option:another_key, args:[@salt.final])             # без иконки
если:   @tutor.t("task_all")
то:     @tutor.speaker(line, size:"m", color:"white", ev:"mousedown", label:"task_all")
или:    @tutor.speaker(line, size:"m", label:"task_all")
или:    @tutor.speaker(line, size:"s", label:"task_all")
или:    @tutor.speaker(line, label:"task_all")             # без иконки
```

Параметры:

```
elem_               - dom-элемент
opt                 - хэш
  * size            - размер динамика
                      если не указан  -  иконка не создается
                      если указан     -  допустимые значения: 'm', 's' (для шрифтов >=36px и <36px соответственно)
  * color           - цвет динамика
                      если не указан  - синий
                      если указан     - допустимые значения: "white"
  * ev              - событие, на которое будет вешаться воспроизведение динамика
                      если не указан  - вешается на click
                      если указан     - допустимые значение: 'mousedown' (вешается на mousedown или touchstart)
  * stopPropagation - останавливает всплытие событий
                      если не указан  - всплытие происходит по-умолчанию (false)
                      если указан     - допустимые значение: true
                      (в паре с opt.ev: 'mousedown', например, можно заблочить событие драга при нажатии на speaker)
  label:            - имя константы для проигрывания
  * option:         - ключ; используется, если звуковая константа с вариантами
  * args:           - массив, аргументы для подстановки в label вместо $1, $2, ...
  * arg:            - аргумент для подстановки в label вместо $1 (вместо args:[a1] можно писать arg:a1)
```

#### `speaker_disabled`

Метод, который включает/выключает спикер в зависимости от параметра `disabled`, если `disabled==true`, и включает, если `disabled==false`.

Пример использования:

```
@tutor.speaker_disabled($el, true)
```

Параметры:

```
elem               - {jQuery}, элемент, в который был добавлен динамик
disabled           - {boolean}, если disabled==true - динамик включен, если disabled==false - выключен
```

#### `speaker_clear`

Метод, убирающий с элемента все, что навешивает метод `speaker`.

Пример использования:

```
@tutor.speaker_clear(elem)
```

Параметры:

```
elem_               - {jQuery}, элемент, в который был добавлен динамик
```

#### `say`

Метод проигрывает звук в случае автопроигрывания или сразу вызывает callback.

Пример использования:

```
@tutor.say(@hidden_speaker, =>
  cb()
)
```

Параметры:

```
elem_               - {jQuery}, элемент, в который был добавлен динамик
cb                  - callback
```

### Keypad-методы

[to top](#tutor)

Методы, связанные с вводом с клавиатуры.

#### `keypad_start`

Метод начинает слушать клавиатуру (показывает клавиатуру при необходимости).

Пример использования:

```
@tutor.keypad_start ['button'], (char) => handler(char)
@tutor.keypad_start ['numeric'], (char) => handler(char)
```

Параметры:

```
roles                - какие символы слушать
* opt:
    keypad_ios7      - опции планшетной клавиатуры
callback             - обработчик событий
```

#### `keypad_finish`

Метод заканчивает слушать клавиатуру (скрывает клавиатуру при необходимости).

Пример использования:

```
@tutor.keypad_finish()
```

#### `button_ok_toggle`

Включает/выключает кнопку enter.

Пример использования:

```
@tutor.button_ok_toggle(false)
```

Параметры:

```
disabled           - {boolean}, отвечает за включение/выключение кнопки enter
```

#### `prevent_default_init`

Отменить дефолтное поведение chrome по backspace.

Пример использования:

```
@tutor.prevent_default_init()
```

#### `prevent_default_destroy`

Возвращает дефолтное поведение chrome по backspace, используется только если поведение уже было отменено.

Пример использования:

```
@tutor.prevent_default_destroy()
```
