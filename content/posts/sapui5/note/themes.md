title: "Заметки: SapUI5: Загадка с темой beliz"
description: ""
tags: ["sapui5 control", "заметки"]
categories: [sapui5]
draft: false
---

# Начало загадки

Если взять SDK с [http://openui5.org](http://openui5.org),
то мы имеем стиль :
```
html.sap-desktop .sapMIBar.sapMFooter-CTX {
    background-color: #ffffff;
    border-top: 1px solid #ebebeb;
}
html.sap-desktop .sapContrast .sapMIBar.sapMFooter-CTX,html.sap-desktop .sapContrast.sapMIBar.sapMFooter-CTX {
    background-color: #2f3c48;
    border-top: 1px solid #475b6d;
}
```

А если собрать самому из исходников с github (`grunt build`):

```
html.sap-desktop .sapMIBar.sapMFooter-CTX {
  background-color: #2f3c48;
  border-top: 1px solid #475b6d;
}
```
Цвет конечно правильный в обоих случаях но это интерестно `как так?`

Причем в `less` файлах этого раздвоения нет и более того если собрать `less` без плагина `less-openui5`. Мы получим:
```
html.sap-desktop .sapMIBar.sapMFooter-CTX {
    background-color: #ffffff;
    border-top: 1px solid #ebebeb;
}
```

# Maven vs grunt-openui5

[scope.js](https://github.com/SAP/less-openui5/blob/master/lib/scope.js) и
[diff.js](https://github.com/SAP/less-openui5/blob/master/lib/diff.js)

`.theming`
```
{
  "sEntity": "Theme",
  "sId": "sap_belize",
  "oExtends": "base",
  "sVendor": "SAP",
  "aBundled": ["sap_belize_plus"],
  "mCssScopes": {
    "library": {
      "sBaseFile": "library",
      "sEmbeddingMethod": "APPEND",
      "aScopes": [
        {
          "sLabel": "Contrast",
          "sSelector": "sapContrast",
          "sEmbeddedFile": "sap_belize_plus.library",
          "sEmbeddedCompareFile": "library",
          "sThemeIdSuffix": "Contrast",
          "sThemability": "PUBLIC",
          "aThemabilityFilter": [
            "Color"
          ],
          "rExcludeSelector": "\\.sapContrastPlus\\W"
        }
      ]
    }
  }
}
```
