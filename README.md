# vue-study

## todo-list

Небольшое (SFC) приложение для ведения списка дел.  

Доступные функции:
- добавление новых дел
- вычеркивание выполненных (клик по записи)
- добавление записи с высоким приоритетом (будет отмечена оранжевым цветом)
- новые записи сортируются по времени
- по клику на кнопку Add появляестя форма добавления записи, есть обязательные поля (время, описание) и необязательное (приоритет)
- кнопка Save заблокирована, пока требуемые поля не будут заполнены
- кнопка Cancel отменяет ввод, очищает поля и скрывает форму ввода

Использованные технологии:
- node.js v21.6.1
- vue 3 (Composition API, v-for, v-model, v-on, v-if, v-bind, computed, reactivity)
- JS + html + CSS