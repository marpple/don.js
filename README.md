# Don.js

Don.js는 jQuery가 지원하는 기능들을 함수형 스타일로 지원합니다.

## Selector

```html
<div class="el1" id="div1">
    <ul>
        <li>1</li>
        <li>2</li>
        <li><ul><li>3-1</li><li>3-2</li></ul></li>
    </ul>
    <div class="el2" id="div2"></div>
</div>
```

```javascript
console.log($('div'));
// (2) [div#div1.el1, div#div2.el2]

console.log($1('div').id);
// div1

console.log($1('.el2').id);
// div2

var div1 = $('div')[0];
console.log($.find(div1, 'li'));
// (5) [li, li, li, li, li]

console.log($.find(div1, '> ul > li'));
// (3) [li, li, li]

_go(div1,
  $.find('> ul > li'),
  console.log);
//  (3) [li, li, li]
```

## DOM Manipulation

```javascript
_go($('#div1'),
    $.find('> ul > li'),
    _map($.html),
    console.log);
// ["1", "2", "<ul><li>3-1</li><li>3-2</li></ul>"]

_go($('#div1'),
  $.find('ul ul li'),
  _map($.html),
  console.log);
// ["3-1", "3-2"]

_go('<li>할일</li>',
    $.el, // create element
    $.addClass('todo'),
    $.appendTo('#todos'));

_go($1('button.done'),
    $.removeAttr('disabled'),
    $.addClass('active'),
    $.text('Click me!'));

_go($('.image'),
    _filter(img => $.width(img) > 500),
    _each($.addClass('big')),
    _map($.attr('src')));
// ["http://....png", "http://....png", "http://....png"]
```

## Events

```javascript
_go('<li>할일 <button class="remove">삭제</button></li>',
  $.el, // create element
  $.addClass('todo'),
  $.on('mouseenter', function(e) {
    $.addClass(e.currentTarget, 'over');
  }),
  $.on('mouseleave', function(e) {
    $.removeClass(e.currentTarget, 'over');
  }),
  $.on('click', 'button', function(e) {
    $.remove(e.delegateTarget);
  }),
  $.appendTo('#todos'));
```
