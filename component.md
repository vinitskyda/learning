## Components

1. Компонентами являются только папки и подпапки из `/components`, которые содержат `meta.json`.
2. Если такая папка НЕ содержит `meta.json`, то она компонентом НЕ является.
3. Нельзя подключать часть компонента. 

Ex. `"/components/button/button_ok"` - не компонент, а `"/components/button"` - компонент, так как в `button_ok` нет `meta.json`, а в `button` - есть.
