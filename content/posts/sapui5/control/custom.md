---
title: "SapUI5: Control - контрол из контролов"
description: "Путевые заметки и набитые шишки.."
date: 2018-03-05T19:13:36+04:00
tags: ["sapui5 control", "заметки"]
categories: [sapui5]
draft: false
---
Путевые заметки и набитые шишки...

# Не теряйте родителей

Если контрол создается через new то незабудьте указать родителя.

```
this.button = new Button(
this.setParent(this); // не забудьте указать родителя
```
Стоит учесть что если добавить контрол в агрегат то родитель изменится, причем некоторые контролы при этом выбросят исключение.

# Пробрасываем binding
Часто требуется пробросить биндинг на внутрение контролы. Сделать это переопределением методов ``_bindProperty`` и ``_bindAggregation``
```
_bindProperty: function (sName, oBindingInfo) {
  if (sName === 'value') {
    this.button.bindProperty('text', oBindingInfo);
  }
  
  // не забудте вызвать базовый
  Control.prototype._bindProperty.call(this, sName, oBindingInfo);
},
```
Выглядит как хак но это используется в самом SapUI5
[пример из ListBase](https://github.com/SAP/openui5/blob/f8c120bb2515aa20ba313fa3439c66aa61060ef3/src/sap.m/src/sap/m/ListBase.js#L573)

# RTL языки
Не стоит забывать что есть языки которые пишутся справа налево.
``sap.ui.getCore().getConfiguration().getRTL()`` позволяет получит RTL-ли текущий язык.
```
  if (!sap.ui.getCore().getConfiguration().getRTL()) {
    oRm.write('<div style="float:right">');
  } else {
    oRm.write('<div style="float:left">');
  }
```

Еще один не маловажный пункт, не стоит забывать про тег [bdi](https://developer.mozilla.org/ru/docs/Web/HTML/Element/bdi). Он нужен если в RTL текcте есть вставки LTR языка (наприме данные из базы: название городов, имена, фамилии). Каждый браузер производит разворот написания по своему :(

Например: 
На английском:``Template: (Test) Welcome message`` будет после переключения локали на Arabic ``القالب: (Test) Welcome message``

При этом отобразится это по разному:

* Chrome: ``Test) Welcome message (:القالب``
* FireFox: ``Welcome message (Test) :القالب``
