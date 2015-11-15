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

## Прошедшие вебинары

* Верстаем веб-страницу<br />[https://ru.bem.info/talks/beminar-css-2015/](https://ru.bem.info/talks/beminar-css-2015/)
* ...Сборка и оптимизация<br />[https://ru.bem.info/talks/beminar-build-2015/](https://ru.bem.info/talks/beminar-build-2015/)
* ...Декларативный JavaScript<br />[https://ru.bem.info/talks/beminar-js-2015/](https://ru.bem.info/talks/beminar-js-2015/)

## План вебинара

* Напишем BEMJSON страниц, вместо HTML
* ...Напишем простые BEMHTML шаблоны
* ...Посмотрим на интересные возможности BEMHTML

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

## Хотим застилизовать все элементы меню

* Можно инлайновыми стилями

~~~ javascript
<ul class="menu">
    <li style="background: red;" class="menu__item">
        Hello,
    <li>
    <li style="background: red;" class="menu__item">
        BEM
    <li>
</ul>
~~~

* ...но плохо: хочется написать код один раз, который будет работать для всех элементов списка

## CSS

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

* застилизовали один раз все элементы списка

~~~ css
.menu__item {
    background: red;
}
~~~

## BEMHTML — CSS-way

~~~ css
.menu {
    tag: 'ul';
}

.menu__item {
    tag: 'li';
}
~~~

* как CSS, но для HTML

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
* ...Можно написать такую декларацию на JavaScript
* ...BEMJSON — это описание структуры страницы в терминах БЭМ на JavaScript с зарезервированными полями
* ...BEMJSON компилируется в HTML

## На чем остановились в прошлый раз

* Есть несколько HTML страниц, написанных по БЭМ
* Есть сборка на Gulp
* Есть JavaScript для некоторых блоков

~~~ javascript
git clone https://github.com/bem-events/beminar-3 beminar-4
~~~

## Конвертация HTML в BEMJSON

* Если есть HTML, написанный по БЭМ, то можно сконвертировать автоматически!

~~~ javascript
npm install html2bemjson --save
~~~

## Дотюним сборку

* Список блоков теперь нужно собирать по BEMJSON-декларации, а не HTML-файлу

~~~ javascript
npm install bemjson2bl --save
~~~

* Нужно компилировать BEMJSON в HTML

~~~ javascript
npm install gulp-bemjson2html --save
~~~

## Можно Plain JavaScript прямо в BEMJSON

* ...Array.prototype.map
* ...Какие-то вычисления во время компиляции: Math.random(), Date.now()

## Напишем шаблоны

* tag находится прямо в BEMJSON, это аналог «инлайновых стилей» — надо выносить в шаблоны

~~~ javascript
block('menu')(
    tag()('ul')
)

block('menu').elem('item')(
    tag()('li')
)
~~~

## BEMJSON делаем ближе к предметное области страницы

* Можно абстрагировать структуру страницы в терминах блоков от ее итогового HTML

~~~javascript
{
    block: 'menu',
    content: [
        { url: 'http://yandex.ru', content: 'Яндекс' },
        { url: 'http://bem.info', content: 'БЭМ' }
    ]
}
~~~

* ...полный BEMJSON для content можно сгенерировать на лету, в шаблонах

## Некоторые интересные возможности

* ...Переопределение шаблона на уровне переопределения
* ...Доопределение контента: добавление всевозможных оберток
* ...Разные шаблоны в зависимости от контекста

## Переопределение шаблона на уровне

* На уровне common.blocks

~~~ javascript
block('link')(
    tag('a')
)
~~~

* На уровне potter.blocks

~~~ javascript
block('link')(
    tag('span')
)
~~~

## Доопределение контента: добавление всевозможных оберток

* applyNext() — позволяет получить результат выполнения предыдущего шаблона

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

~~~ css
.menu__item[href] {
    background: green;
}
~~~

* Если в BEMJSON не указан url для ссылки — заменим тег на span, потому что это уже не ссылка в HTML

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
  * ...plain JavaScript — можно динамически генерировать BEMJSON, проводить какие-то вычисления во время компиляции
* ...BEMHTML — декларативные шаблоны. Как CSS, только для «настройки» итогового HTML
    * ...определять теги, общие классы или атрибуты для всех блоков на странице
    * ...доопределять/переопределять шаблоны на уровнях переопределения
    * ...писать разные шаблоны в зависимости от контекста (BEMJSON блока)
    * ...динамически менять BEMJSON, который находится внутри блока

## Полезные ссылки

* Песочница<br />[http://bem.github.io/bem-xjst/](http://bem.github.io/bem-xjst/)
* Документация<br />[https://ru.bem.info/technology/bemhtml/](https://ru.bem.info/technology/bemhtml/)

## **Контакты** {#contacts}

<div class="info">
<p class="author">{{ site.author.name }}</p>
<p class="position">{{ site.author.position }}</p>

    <div class="contacts">
        <p class="contacts-left mail">viktor.s.karpov@yandex.ru</p>
        <p class="contacts-left contacts-top twitter">@vitkarpov</p>
        <p class="contacts-right contacts-top github">vitkarpov</p>
    </div>
</div>
