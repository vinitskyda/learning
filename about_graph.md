## Конспект Slack от 2014.06.25

Давайте я немного расскажу как устроена работа с графом на системном уровне (edited)

Alexey Vakhov [13:59]
там нет никакой магии

Alexey Vakhov [14:00]
Если в мете скрипта появляется мета-файл графа, то система подключает графовый компилятор

Alexey Vakhov [14:00]
https://github.com/uchiru/content/tree/master/viewer/lib/graph

Alexey Vakhov [14:00]
он лежит здесь

Alexey Vakhov [14:00]
состоит из цепочки всяких парсеров

Alexey Vakhov [14:00]
https://github.com/uchiru/content/blob/master/viewer/lib/graph_compiler.rb#L20-L33

Alexey Vakhov [14:01]
граф из плейн-текста укладывается в иерархическую структуру nodes + edges

Alexey Vakhov [14:01]
у каждого узла соответвенном могут быть внутренности

Alexey Vakhov [14:01]
тоже в виде nodes + edjes

Alexey Vakhov [14:02]
далее граф переводится в кофе скрипт

Alexey Vakhov [14:02]
https://github.com/uchiru/content/tree/master/viewer/lib/graph/templates  - вот здесь лежат темплейты

Alexey Vakhov [14:02]
если вы посмотрите js готовой карточки, то для каждого скрипта вы все эти темплейты увидите

Alexey Vakhov [14:03]
https://github.com/uchiru/content/blob/master/viewer/lib/graph/templates/run.coffee.erb
в этом темплейте для скрипта создается конструктор (поэтому его писать и ненужно), заготовки для SBS. Чтобы скрипт получился полностью совместимым с существующей системой

Alexey Vakhov [14:03]
и всякие вспомогательные методы

Alexey Vakhov [14:03]
https://github.com/uchiru/content/blob/master/viewer/lib/graph/templates/step.coffee.erb

Alexey Vakhov [14:03]
это ключевой метод

Alexey Vakhov [14:04]
для шага step0 в классе скрипта создается метод __graph_step0

Alexey Vakhov [14:04]
который проверяет существует ли метод step0 и его вызывает с колбеком

Alexey Vakhov [14:05]
дальше колбек в зависимости от связей которые  были в изначальном графе переходит в следующее состояние

Alexey Vakhov [14:05]
имплементации шагов вызываются с помощью `call` подменяя this

Alexey Vakhov [14:06]
для каждого "процесса" создается frame с состоянием, на форках состяние клонируется, и поэтому каждая ветвь форка работает со своим this

Alexey Vakhov [14:06]
например системный метод `click` реализован как обычный шаг с _on_term

Alexey Vakhov [14:06]
https://github.com/uchiru/content/blob/master/viewer/lib/graph/templates/click.coffee.erb

Alexey Vakhov [14:06]
и так далее

Alexey Vakhov [14:07]
код весь там, можно поизучать тому, кому интересно

Alexey Vakhov [14:07]
Код сложный, так как колбечную модель мы переводим в мультитредовую. Это нельзя сделать просто мне кажется.
