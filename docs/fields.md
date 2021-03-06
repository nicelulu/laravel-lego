# Fields

## Text

文本输入框

- 示例 HTML：

```html
<input type="text" name="xx" id="xx" />
```


## Text

```php
$form = Lego::form(new User);
$form->addText('name', 'Your Name')

	// Validation
	->required()
	->unique()
	->rule('numberic') // Laravel Validation rules
	// - 自定义的验证逻辑
	->validator(function ($value) {
		if (is_illegal($value)) {
			return 'this name is illegal';
		}
	})

	// 展示模式
	->readonly()
	->editable() // $ifYouAreAwesome
	->extra('select a nick name')

	// 字段值
	->default('Tom')
	
	// html 属性
	->attr('class', 'text-danger')
	->attr(['class' => 'text-danger', 'data-mask' => '999'])
	// - 修改 Field 上一层的属性，Boostrap 中的 .from-group div
	->container('class', 'text-danger')
	->container(['class' => 'hide'])
	
	// i18n
	->locale('zh-CN') // default App::getLocale()
;
```

## AutoComplete

自动补全输入框

- example usage：

```php
$form = Lego::form(new Book);
$form->addAutoComplete('author.name', 'Author')
	// 自定义补全结果
	->match(function ($keyword) {
		return Author::whereMatch($keyword)
			->limit(10)
			->pluck('name', 'id')
			->all();
	})
;

```

## Datetime

日期时间输入框

- 目标数据示例：`2016-11-11 11:11:11`
- example usage：

```php
$form = Lego::form(new Book);
$form->addDatetime('checked_at', 'Checked At');
```

## Date

日期输入框

- 目标数据示例：`2016-11-11`
- example usage：

```php
$form = Lego::form(new Human);
$form->addDate('birthday', 'Birthday');
```

## Time

- 目标数据示例：`11:11:11`
- example usage：

```php
$form = Lego::form(new Schedule);
$form->addTime('daily_at', 'Select Time');
```

## Textarea

长文本输入框

```php
$form = Lego::form([]);
$form->addTestarea('description', 'Description');
```

## Readonly

只读文本

```php
$form = Lego::form([]);
$form->addTestarea('Description', 'this is description of ...');
```

Email field in <http://getbootstrap.com/css/#forms-controls-static>
