### 前言

>多人开发vue项目,代码风格形式不一
>
>vscode保存代码，自动按照eslint规范格式化代码设置（vscode最新版配置）

### vscode插件

首先vscode需要装一些vscode插件

ESLint、Vetur、Prettier-Code formatter、GitLens-Git supercharged

### 配置settings.json

打开settings.json，贴上配置，注意自己原有的vscode主题和字体等不要替换掉

打开方式

#### 方式一:

1)文件 ------.>【首选项】---------->【设置】

2）搜索emmet.include;

3）在settings.json下的【工作区设置】中添加

#### 方式二:

Ctrl + P 搜索settings.json

### 贴上如下配置

```javascript
{
  "window.zoomLevel": 0,
  "diffEditor.ignoreTrimWhitespace": false,
  "workbench.colorTheme": "One Monokai",
  "editor.fontSize": 14,
  "workbench.editor.enablePreview": true, //预览模式关闭
  "editor.formatOnSave": true, // #每次保存的时候自动格式化
  // 自动修复
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true,
  },
  "eslint.enable": true, //是否开启vscode的eslint
  // vscode默认启用了根据文件类型自动设置tabsize的选项
  "editor.detectIndentation": false,
  // 重新设定tabsize
  "editor.tabSize": 2,
  //  #去掉代码结尾的分号 
  "prettier.semi": false,
  //  #使用单引号替代双引号 
  "prettier.singleQuote": true,  
  //  #让prettier使用eslint的代码格式进行校验 
  "prettier.eslintIntegration": true,
  "javascript.preferences.quoteStyle": "double",
  "typescript.preferences.quoteStyle": "double",
  //  #让函数(名)和后面的括号之间加个空格
  "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
  // 配置 ESLint 检查的文件类型
  "eslint.validate": [
    "javascript",
    "vue",
    "html"
  ],
  "eslint.options": { //指定vscode的eslint所处理的文件的后缀
    "extensions": [
      ".js",
      ".vue",
      ".ts",
      ".tsx"
    ]
  }, 
  "git.enableSmartCommit": true,
  "editor.quickSuggestions": {
    "strings": true
  },
  //一定要在vutur.defaultFormatterOptions参数中设置，单独修改prettier扩展的设置是无法解决这个问题的，因为perttier默认忽略了vue文件（事实上从忽略列表移除vue也不能解决这个问题）
  "vetur.format.defaultFormatterOptions": {
    "prettier": {
      "semi": false, // 格式化不加分号
      "singleQuote": true, // 格式化以单引号为主
    },
    "js-beautify-html": {
      // force-aligned | force-expand-multiline vue html代码格式化
      "wrap_attributes": "force-aligned",//"auto","force-expand-multiline"
      "wrap_line_length": 200,
      "wrap_width_line": false,
      "semi": false,
      "singleQuote": true,
    },
    "prettyhtml": {
      "printWidth": 100,
      "singleQuote": false,
      "wrapAttributes": false,
      "sortAttributes": true
    },
  },
  "vetur.format.defaultFormatter.html": "js-beautify-html",
  "vetur.format.defaultFormatter.js": "prettier",
  "[vue]": {
    "editor.defaultFormatter": "octref.vetur"
  },
  "javascript.updateImportsOnFileMove.enabled": "never",
  "javascript.implicitProjectConfig.experimentalDecorators": true,
  "workbench.editor.showTabs": true,
  "gitlens.advanced.messages": {
        "suppressCommitHasNoPreviousCommitWarning": false,
        "suppressCommitNotFoundWarning": false,
        "suppressFileNotUnderSourceControlWarning": false,
        "suppressGitVersionWarning": false,
        "suppressLineUncommittedWarning": false,
        "suppressNoRepositoryWarning": false,
        "suppressResultsExplorerNotice": false,
        "suppressShowKeyBindingsNotice": true,
        "suppressUpdateNotice": false,
        "suppressWelcomeNotice": true
    },
    "gitlens.keymap": "alternate",
    "git.enableSmartCommit": true,
    "gitlens.historyExplorer.enabled": true,
    "gitlens.views.fileHistory.enabled": true,
    "gitlens.views.lineHistory.enabled": true,
}
```
