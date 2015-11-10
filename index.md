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

## CSS!

~~~ javascript
.menu {
    background: red;
}

.menu__item {
    font-weight: bold;
}

<ul class="menu">
    <li class="menu__item">
        Hello,
    <li>
    <li class="menu__item">
        BEM
    <li>
</ul>
~~~

## CSS?

~~~ javascript
.menu {
    tag: 'ul';
}

.menu__item {
    tag: 'li';
}

<ul class="menu">
    <li class="menu__item">
        Hello,
    <li>
    <li class="menu__item">
        BEM
    <li>
</ul>
~~~

## BEMHTML

~~~ javascript
{
    block: 'menu',
    content: [
        { elem: 'item', content: 'Hello,' },
        { elem: 'item', content: 'BEM' }
    ]
}

block('menu')(
    tag()('ul')
)

block('menu').elem('item')(
    tag()('li')
)
~~~

## Пример подсветки кода на JavaScript

## **Контакты** {#contacts}

<div class="info">
<p class="author">{{ site.author.name }}</p>
<p class="position">{{ site.author.position }}</p>

    <div class="contacts">
        <p class="contacts-left mail">vitkarpov@yandex-team.ru</p>
        <p class="contacts-left contacts-top twitter">@vitkarpov</p>
    </div>
</div>
