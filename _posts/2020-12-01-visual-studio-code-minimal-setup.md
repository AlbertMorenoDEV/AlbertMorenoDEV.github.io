---
layout: post
title: "Visual Studio Code minimal setup"
categories: code
---

* Theme: [Material Theme Palenight High Contrast](https://marketplace.visualstudio.com/items?itemName=Equinusocio.vsc-material-theme)
* Font: [JetBrains Mono](https://www.jetbrains.com/lp/mono/)
* Settings:
```
{
    "files.autoSave": "onFocusChange",
    "go.useLanguageServer": true,
    "editor.minimap.enabled": false,
    "editor.renderWhitespace": "none",
    "editor.renderIndentGuides": false,
    "editor.renderLineHighlight": "none",
    "editor.overviewRulerBorder": false,
    "editor.hideCursorInOverviewRuler": true,
    "editor.folding": false,
    "editor.occurrencesHighlight": false,
    "editor.matchBrackets": false,
    "editor.glyphMargin": false,
    "explorer.openEditors.visible": 0, // see the opened files with ⌘ + ⌥ + Tab
    "workbench.activityBar.visible": false,
    "workbench.editor.showIcons": false,
    "workbench.editor.tabCloseButton": "off",
    "workbench.statusBar.visible": false,
    "indenticator.color.dark": "rgba(255,255,255,.1)",
    "workbench.colorCustomizations": {},
    "editor.fontFamily": "JetBrains Mono, Menlo, Monaco, 'Courier New', monospace",
    "editor.fontSize": 14,
    "workbench.colorTheme": "Material Theme Palenight High Contrast",
    "workbench.iconTheme": "eq-material-theme-icons-palenight",
    "workbench.editor.showTabs": false
}
```
* Extensions:
    * [Indenticator](https://marketplace.visualstudio.com/items?itemName=SirTori.indenticator) to highlight only the current indent depth
    * [Subtle Match Brackets](https://marketplace.visualstudio.com/items?itemName=rafamel.subtle-brackets) to underline matching brackets (instead of a border)