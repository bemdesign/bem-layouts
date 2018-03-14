# Обвязка
Используется для формирования общего каркаса страницы. Позволяет создавать различные сплитовые конструкции страницы.

## Модификаторы

### tpl-layout
| Модификатор	 | Значение        | Описание                         |
| ------------ | --------------- | -------------------------------- |
| structure 	| 10-90 / 30-70 / 50-50 / 70-30 / 90-10 / 20-60-20 / fold-25-50-25 / fold-30-70 / fold-50-50 / fold-70-30 / fold-100 / unfold-25-50-25 / unfold-30-70 / unfold-50-50 / unfold-70-30 / unfold-100 	| Конструкции обвязки в различных пропорциях |

Цифры в значениях модификатора опредлеяеют ширину колонки в процентах относительно всей страницы. Значение **fold** — задаёт первой колонке ширину схлопнотого меню, равной переменной **menu-fold** из блока **theme**. **unfold** — задаёт первой колонке ширину развёрнутого меню, равной переменной **menu-unfold** из блока **theme**


### __col
Элемент для разграничения содержимого страницы по выбранному каркасу.

### __panel
Опциональный семантический элемент для меню второго уровня, фильтров, настроек и т.п.

###
Опциональный семантический элемент для заголовка страницы.

### __content
Элемент обеспечивает охранные поля от границы содержимого до края экрана, либо соседнего сплита. Значение охранных полей берётся из модификатора **gap** блока **theme**.

### __container
Элемент для основного контента страницы. Вкладывается в элемент **__content**.

| Модификатор	 | Значение        | Описание                         |
| ------------ | --------------- | -------------------------------- |
| size 	| xs / s / m / full 	| Максимальная ширина контейнера |
| align 	 | center 	 | Распроложение контейнера по горизонтале |

### __section
Элемент для семантического разделения содержимого.



### Примеры

## Обвязка со схлопнутым боковым меню, панелью и заголовком
```javascript
{
	block: 'tpl-layout',
	mods: { structure: 'fold-100' },
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
					elem: 'heading',
					content: {
						block: 'title',
						content: 'Page title'
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
									content: [ ]
								},
								{
									elem: 'section',
									content: [ ]
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

## Обвязка с раскрытым боковым меню, основным контентом и дополнительный боковой секцией
```javascript
{
	block: 'tpl-layout',
	mods: { structure: 'unfold-70-30' },
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
					elem: 'content',
					content: [
						{
							elem: 'container',
							elemMods: { size: 'm', distribute: 'center' },
							content: [
								{
									elem: 'section',
									content: [ ]
								},
								{
									elem: 'section',
									content: [ ]
								},
							]
						}
					]
				}
			]
		},
		{
			elem: 'col',
			content: [
				{
					block: 'aside-widget'
				},
				{
					block: 'banner'
				}
			]
		}
	]
}
```

## Сплит экран в пропорциях 50 на 50
```javascript
{
	block: 'tpl-layout',
	mods: { structure: '50-50' },
	content: [
		{
			elem: 'col',
			content: [
				{
					block: 'pt-form',
					content: []
				}
			]
		},
		{
			elem: 'col',
			content: [
				{
					block: 'promo-image'
				}
			]
		},
	]
}
```
