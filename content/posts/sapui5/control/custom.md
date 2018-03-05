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
Стоит учесть что если добавить контрол в агреган то родитель изменится, причем некоторые контролы при этом выбросыт исключение.

# Пробрасываем binding
Часто требуется пробросить биндинг на внутрение контролы. Сделать это переопределением методов ``_bindProperty`` и ``_bindAggregation``
```
_bindProperty: function (sName, oBindingInfo) {
      if (sName === 'value') {
        this.button.bindProperty('text', oBindingInfo);
      }
      
      Control.prototype._bindProperty.call(this, sName, oBindingInfo); // не забудте вызвать базовый
    },
```
Выглядит как хак но это используется в самом SapUI5
[пример из ListBase](https://github.com/SAP/openui5/blob/f8c120bb2515aa20ba313fa3439c66aa61060ef3/src/sap.m/src/sap/m/ListBase.js#L573)