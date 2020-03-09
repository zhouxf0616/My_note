# 最佳配置 支持文件跳转 可能需要下载部分拓展插件。 file peek？ vue 3 snippets? vue peek ? vue ? vetur? path intellisense?javascript code snippets? html snippets ?vue helper ? vue vscode snippets?
{
  "editor.cursorBlinking": "smooth",
  "editor.cursorStyle": "block",
  "workbench.iconTheme": "vscode-icons",
  "editor.fontFamily": "Consolas,Monospace",
  "workbench.colorTheme": "Dracula",
  "editor.wordWrap": "on",
  "vsicons.dontShowNewVersionMessage": true,
  "editor.cursorStyle": "line", //光标为细竖线
  "editor.tabSize": 2, //缩进2个空格
  "vetur.format.defaultFormatterOptions": {
    "prettier": {
      "semi": false, //去掉末尾分号
      "singleQuote": true //将所有双引号改为单引号
    }
  },
  "javascript.format.insertSpaceBeforeFunctionParenthesis": true, //在方括号之间插入空格
  "vetur.format.defaultFormatter.js": "vscode-typescript",
  //配置下vscode支持vue语言
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "html",
    {
      "language": "vue",
      "autoFix": true
    }
  ],
  "window.zoomLevel": 0,
  "terminal.integrated.rendererType": "dom",
  "editor.suggest.snippetsPreventQuickSuggestions": false,
  "files.associations": {
    "*.vue": "html"
  },
  "scm.alwaysShowProviders": true,
  "remote.downloadExtensionsLocally": true,
  "file_peek.activeLanguages": [
    "typescript",
    "javascript",
    "python",
    "vue",
    "html"
  ],
  "file_peek.searchFileExtensions": [
    ".js",
    ".ts",
    ".html",
    ".css",
    ".scss",
    ".vue"
  ],
  "path-intellisense.extensionOnImport": true,
  "vue-peek.supportedLanguages": [
    "vue",
    "javascript"
  ],
  "vue-peek.targetFileExtensions": [
    ".vue",
    ".js"
  ]
}