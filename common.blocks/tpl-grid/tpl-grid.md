
# Сетка
Используется для создания различных контентных конструкций. Сетка может использоваться как для фиксированных, так и для адаптивных проектов.

Сетка связана с блоком [theme](https://github.com/bemdesign/bem-themes) и обвязкой [tpl-layout](https://github.com/bemdesign/bem-layouts/tree/master/common.blocks/tpl-layout). В соответствии с правилом близости, ширина межколонника (**col-gap**) и высота межстрочника (**row-gap**) высчитываются исходя из значения модификатора **gap** в блоке **theme**. Этому же значению равны охранные поля в элементе **content** в блоке **tpl-layout**. Таким образом межколонник и межстрочник сетки никогда не могут больше охранных полей.

Для простых сеточных конструкций, где блоки равны друг другу — есть модификатор **ratio**. Используя его можно не задавать ширину непосредственным «детям» внутри сетки. Если нужны более сложные конструкции, то рекомендуем использовать модификатор **columns** в связке с элементами **fraction** и явным указанием их ширины.

## Модификаторы

### tpl-grid
| Модификатор | Значение        | Описание                         |
| ----------- | --------------- | -------------------------------- |
| columns     | 10 / 12         | Колличество возможных колонок в сетке |
| col-gap     | none / third / half / two-thirds / full | Относительная ширина межколонника исходя из значения модификатора **gap** в блоке **theme**. |
| row-gap     | none / third / half / two-thirds / full | Относительная высота межстрочника исходя из значения модификатора **gap** в блоке **theme**. |
| ratio       | 1-1 / 1-1-1 / 1-1-1-1 / 1-1-1-1-1 / 1-1-1-1-1-1 | Модификатор для простых конструкций, где её элементы визуально равнозначны. **Не используйте** вместе с модификатором **columns** |


### __fraction

Один элемент сетки. Mobile-first — модификаторы на ширину пишутся в порядке увелечения ширины экранов: col > s-col > m-col > l-col > xl-col. Например элемент на мобильном экране занимает 100% ширины контейнера, на планшете 50%, а начиная с ноутбуков одну треть. Для этого указываем модификаторы **col_12 s-col_6 l-col_4**. Если клиентский адаптив не предполагается на проекте, то рекомендуем использовать только модификатор **col**

| Модификатор | Значение        | Описание                         |
| ----------- | --------------- | -------------------------------- |
| col         | 1 / 2 / 3 / 4 / 5 / 6 / 7 / 8 / 9 / 10 / 11 / 12 | Ширина элемента в колонках |
| s-col       | 1 / 2 / 3 / 4 / 5 / 6 / 7 / 8 / 9 / 10 / 11 / 12 | Ширина элемента в колонках при разрешении экрана равному переменной **screen-s** в блоке **theme** |
| m-col       | 1 / 2 / 3 / 4 / 5 / 6 / 7 / 8 / 9 / 10 / 11 / 12 | Ширина элемента в колонках при разрешении экрана равному переменной **screen-m** в блоке **theme** |
| l-col       | 1 / 2 / 3 / 4 / 5 / 6 / 7 / 8 / 9 / 10 / 11 / 12 | Ширина элемента в колонках при разрешении экрана равному переменной **screen-l** в блоке **theme** |
| xl-col      | 1 / 2 / 3 / 4 / 5 / 6 / 7 / 8 / 9 / 10 / 11 / 12 | Ширина элемента в колонках при разрешении экрана равному переменной **screen-xl** в блоке **theme** |


## Примеры

### Встраивание сетки в обвязку страницы **tpl-layout**
```javascript
{
	block: 'tpl-layout',
	mods: { col: 'fold-100' },
	content: [
		{
			elem: 'col',
			content: [
				{
					block: 'main-menu',
				}
			]
		},
		{
			elem: 'col',
			content: [
				{
					elem: 'panel',
					content: {
						block: 'submenu'
					}
				},
				{
					elem: 'content',
					content: [
						{
							elem: 'container',
							elemMods: { size: 'm', distribute: 'center' },
							content: [
								{
									elem: 'section',
									mix: 'tpl-grid', mods: { ratio: '1-1-1', 'col-gap': 'half', 'row-gap': 'half' },
									content: [
										{ block: 'pt-card', content: '...' },
										{ block: 'pt-card', content: '...' },
										{ block: 'pt-card', content: '...' },
									]
								},
								{
									elem: 'section',
									mix: 'tpl-grid', mods: { columns: '12', 'col-gap': 'half', 'row-gap': 'two-thirds' }
									content: [
										{
											block: 'foo',
											mix: { block: 'tpl-grid', elem: 'fraction', elemMods: { 'col': '6' }}
										},
										{
											block: 'bar',
											mix: { block: 'tpl-grid', elem: 'fraction', elemMods: { 'col': '4' }}
										},
										{
											block: 'baz',
											mix: { block: 'tpl-grid', elem: 'fraction', elemMods: { 'col': '2' }}
										}
									]
								},
							]
						}
					]
				}
			]
		}
	]
}
```

### Клиентский адаптив элементов сетки
```javascript
...
	{
		elem: 'container',
		elemMods: { size: 'm', distribute: 'center' },
		content: [
			{
				elem: 'section',
				mix: 'tpl-grid', mods: { columns: '12', 'col-gap': 'half', 'row-gap': 'two-thirds' }
				content: [
					{
						block: 'foo',
						mix: { block: 'tpl-grid', elem: 'fraction', elemMods: { 'col': '12', 'l-col': '6' }}
					},
					{
						block: 'bar',
						mix: { block: 'tpl-grid', elem: 'fraction', elemMods: { 'col': '6', 's-col': '8', 'l-col': '3', 'xl-col': '4' }}
					},
					{
						block: 'baz',
						mix: { block: 'tpl-grid', elem: 'fraction', elemMods: { 'col': '6', 's-col': '4', 'l-col': '3', 'xl-col': '2' }}
					}
				]
			},
		]
	}
...
```
