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

## CSS, чтобы задать внешний вид

~~~ css
.menu {
    background: red;
}

.menu__item {
    font-weight: bold;
}
~~~

## CSS, чтобы определить разметку?!

~~~ css
.menu {
    tag: 'ul';
}

.menu__item {
    tag: 'li';
}
~~~

## BEMHTML: CSS-way

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
git clone https://github.com/bem-events/beminar-3 beminar-3++
~~~

## Конвертация HTML в BEMJSON

### Если есть HTML, написанный по БЭМ, то можно сконвертировать

~~~ javascript
npm install html2bemjson --save
~~~

## Дотюним сборку

* По аналогии с html2bl, подключим bemjson2bl
* Напишем небольшой gulp-плагин, который позволяет скомпилировать bemjson в html

## **Контакты** {#contacts}

<div class="info">
<p class="author">{{ site.author.name }}</p>
<p class="position">{{ site.author.position }}</p>

    <div class="contacts">
        <p class="contacts-left mail">vitkarpov@yandex-team.ru</p>
        <p class="contacts-left contacts-top twitter">@vitkarpov</p>
    </div>
</div>
