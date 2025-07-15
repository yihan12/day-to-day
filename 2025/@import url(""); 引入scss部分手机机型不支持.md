当你碰到“Cannot load Prettier version from package.json”这个错误，往往是因为Prettier没办法从`package.json`文件里读取到自身版本。下面为你介绍几种可行的解决办法：

1. **检查`package.json`文件**
要保证你的项目里有`package.json`文件，而且其中包含Prettier依赖项。可以通过以下命令来添加Prettier：
```bash
npm install --save-dev prettier
```

2. **重新安装依赖**
有时候依赖项可能会损坏，你可以试着删除`node_modules`目录和`package-lock.json`文件，然后重新安装依赖：
```bash
rm -rf node_modules package-lock.json
npm install
```

3. **明确指定Prettier版本**
在VS Code里，你可以手动指定Prettier的路径。具体操作是在设置（Settings）中搜索“Prettier: Path”，然后填入类似`./node_modules/prettier`这样的路径。

4. **更新VS Code Prettier插件**
要确保你安装的VS Code Prettier插件是最新版本，旧版本的插件可能会和Prettier存在兼容性问题。

5. **验证Prettier安装情况**
你可以通过运行以下命令来确认Prettier是否已经正确安装：
```bash
npx prettier --version
```

要是上述方法都不能解决问题，你可以尝试在项目根目录下创建一个`.prettierrc.json`文件，内容如下：
```json
{}
```
这能够帮助Prettier正确初始化。

如果问题依旧存在，建议你提供更多信息，例如项目结构、`package.json`内容以及你使用的IDE/编辑器等，这样便于进一步排查问题。
