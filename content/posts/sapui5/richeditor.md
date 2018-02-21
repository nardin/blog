---
title: "SapUI5: rich text editor"
description: "sap.ui.richtexteditor - это обертка tinymce 3 или tinymce 4. Не является частью OpenUI5."
tags: []
date: 2018-02-19T19:13:36+04:00
categories: [sapui5]
draft: false
---

# Общее описание
sap.ui.richtexteditor - это обертка tinymce 3 или tinymce 4. Не является частью OpenUI5.

Тип задается свойством ``editorType`` у молчанию ``TinyMCE`` но я рекомендовал бы использовать ``TinyMCE4`` ([Список допустимых значений](https://sapui5.hana.ondemand.com/#/api/sap.ui.richtexteditor.EditorType/overview))

SAP обычно дает четкие указания когда какой контрол использовать, по сути richtexteditor не разрешено использовать с модулем ``sap.m`` но для декстопов сделано исключение: 
[диаграма совместимости](https://sapui5.hana.ondemand.com/#/topic/363cd16eba1f45babe3f661f321a7820)

![TinyMCE](/images/posts/sapui5/richeditor/tmc3.png)

![TinyMCE 4](/images/posts/sapui5/richeditor/tmc4.png)


# Custom Toolbar
С версии 1.48 появилась возможность использовать ``Custom Toolbar`` по сути это Toolbar написаный на SapUI5 и синхронизующий свое состояние и состояние редактора. (В версии до 1.54 не синхронизуютра Images и Links)

![TinyMCE 4](/images/posts/sapui5/richeditor/custom.png)

# Полезные ссылки
* [API Reference](https://sapui5.hana.ondemand.com/#/api/sap.ui.richtexteditor)
* [TinyMCE](https://www.tinymce.com/)
