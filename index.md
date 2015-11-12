---

layout: default

---

# Яндекс

## **{{ site.presentation.title }}** {#cover}

<div class="s">
    <div class="service">{{ site.presentation.service }}</div>
</div>

{% if site.presentation.nda %}
<div class="nda"></div>
{% endif %}

<div class="info">
	<p class="author">{{ site.author.name }}, <br/> {{ site.author.position }}</p>
</div>

## BEMHTML
{:.section}

### Декларативный, как CSS

## Пример

### Простой список

~~~ javascript
<ul class="menu">
    <li class="menu__item">
        Hello,
    <li>
    <li class="menu__item">
        BEM
    <li>
</ul>
~~~

## CSS

* Определяет внешний вид для всех блоков меню на странице — удобно

~~~ css
.menu {
    background: red;
}
~~~

* Но, что если...

~~~ css
.menu {
    tag: 'ul';
}
~~~

## BEMHTML — CSS-way

~~~ javascript
block('menu')(
    tag()('ul')
)

block('menu').elem('item')(
    tag()('li')
)
~~~

## Что нужно для реализации такого интерфейса?

* ...Нужна декларация страницы
* ...Можно написать такую декларацию в формате JSON
* ...BEMJSON — JSON специального вида, который позволяет описать страницу в терминах блоков, элементов и модификаторов
* ...BEMJSON компилируется в HTML

## На чем остановились в прошлый раз

* Есть HTML страниц, написанный по БЭМ
* Есть сборка на Gulp
* Есть javascript для некоторых блоков

~~~ javascript
git clone https://github.com/bem-events/beminar-3 beminar-4
~~~

## Конвертация HTML в BEMJSON

* Если есть HTML, написанный по БЭМ, то можно сконвертировать!

~~~ javascript
npm install html2bemjson --save
~~~

## Дотюним сборку

* Список блоков теперь нужно собирать по bemjson-декларации, а не html-файлу

~~~ javascript
npm install bemjson2bl --save
~~~

* Нужно компилировать bemjson в html

~~~ javascript
npm install gulp-bemjson2html --save
~~~

## Можно Plain Javascript прямо в BEMJSON

* ...Array.prototype.map
* ...Какие-то вычисления во время компиляции: Math.random(), Date.now()

## Напишем простые шаблоны

* tag находится прямо в bemjson, это аналог «инлайновых стилей» — надо выносить в шаблоны

~~~ javascript
block('menu')(
    tag()('ul')
)

block('menu').elem('item')(
    tag()('li')
)
~~~

## Некоторые интересные возможности

* ...Переопределение шаблона на уровне переопределения
* ...Доопределение контента: добавление всевозможных оберток
* ...Разные шаблоны в зависимости от контекста

## Переопределение шаблона на уровне

### На уровне common.blocks

~~~ javascript
block('link')(
    tag('a')
)
~~~

### На уровне potter.blocks

~~~ javascript
block('link')(
    tag('span')
)
~~~

## Доопределение контента: добавление всевозможных оберток

### applyNext() — позволяет получить результат выполнения предыдущего шаблона

~~~ javascript
block('page')(
    content()(function() {
        return {
            elem: 'inner',
            content: applyNext()
        }
    })
)
~~~

## Разные шаблоны в зависимости от контекста

### Если в BEMJSON не указан url для ссылки — заменим тег на span, потому что это уже не ссылка

~~~ javascript
block('link')(
    tag('a')
)

block('link').match(function() { return !this.ctx.url; })(
    tag('span')
)
~~~

## В итоге

* ...BEMJSON позволяет описать страницу в терминах БЭМ
  * ...plain javascript — можно динамически генерировать bemjson, проводить какие-то вычисления во время компиляции
* ...BEMHTML — декларативные шаблоны. Как CSS, только для «настройки» итогового html
    * ...определять теги, общие классы или атрибуты для **всех блоков на странице**
    * ...доопределять/переопределять шаблоны на уровнях переопределения
    * ...писать разные шаблоны в зависимости от контекста (bemjson блока)
    * ...динамически менять bemjson, который находится внутри блока: обертки

## **Контакты** {#contacts}

<div class="info">
<p class="author">{{ site.author.name }}</p>
<p class="position">{{ site.author.position }}</p>

    <div class="contacts">
        <p class="contacts-left mail">vitkarpov@yandex-team.ru</p>
        <p class="contacts-left contacts-top twitter">@vitkarpov</p>
    </div>
</div>
