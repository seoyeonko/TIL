# BEM Naming Convention

CSS class๋ช ๋ฐฉ๋ฒ๋ก  [๐ ref](http://getbem.com/)

- Block - Element - Modifier
- class(.)๋ง์ ์ฌ์ฉ, id(#) ์ฌ์ฉํ์ง ์์

## Block
- ๋๋ฆฝ์ ์ธ ์ปดํฌ๋ํธ     
ex) `header`, `container`, `menu`, `checkbox`, `input`


## Element
- ๋ธ๋ญ์ ์์
- `__` ์ฌ์ฉ: `block__element`   
ex) `menu item`, `list item`, `checkbox`, `caption`, `header title`


## Modifier
- block์ด๋ element์ ์์ฑ 
- `--` ์ฌ์ฉ: `block__element--modifier`, `block--modifier`    
ex) `disabled`, `highlighted`, `checked`, `fixed`, `size big`, `color yellow` 


### Using
```html
<button class="button">
	Normal button
</button>
<button class="button button--state-success">
	Success button
</button>
<button class="button button--state-danger">
	Danger button
</button>
```

```css
.button {
	display: inline-block;
	border-radius: 3px;
	padding: 7px 12px;
	border: 1px solid #D5D5D5;
	background-image: linear-gradient(#EEE, #DDD);
	font: 700 13px/18px Helvetica, arial;
}
.button--state-success {
	color: #FFF;
	background: #569E3D linear-gradient(#79D858, #569E3D) repeat-x;
	border-color: #4A993E;
}
.button--state-danger {
	color: #900;
}
```

## Benefits
- ์ฌ์ฌ์ฉ์ ํตํด css ์ฝ๋ ์์ ์ค์ผ ์ ์์ 
- css ๊ตฌ์กฐ ์ดํด๊ฐ ์ฌ์์ง  
