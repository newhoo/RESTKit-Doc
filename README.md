# RESTKit

[简体中文](./README.zh_CN.md)

[RESTKit](https://plugins.jetbrains.com/plugin/14723-restkit) is a powerful toolkit for restful services development.

This plugin is committed to enhancing development efficiency with useful features. From the initial RestfulToolkit and joined common functions of Postman, rich and complete features can greatly improve the efficiency of IDEA development. Free to share with everyone, not for commercial purposes. If you find any problems, please give me feedback.

If this plugin helps, please **🌟 Star** and [Rating](https://plugins.jetbrains.com/plugin/14723-restkit/reviews)! If you have any good idea, please let me know.


## Features
- Restful service automatic scanning and display.
  - Support searching service in Native Search Everywhere. ( use: <kbd>Ctrl \\</kbd> or <kbd>Ctrl Alt N</kbd> )
  - Show restful service structure in tool window.
  - Service and Method jump to each other.
- Powerful HTTP client：
  - Custom parameter format, support placeholder variable, formatted JSON.
  - Environment variable：define/manage/use/export/import, support preset function and script function.
  - Global header：can use with Environment, also support preset function and script function.
  - Parameter library：support display/save/delete in Headers/Params/Body tab.
  - Request script：support pre-request and post-script script.
  - HTTP packet display.
- Request log：save request log whit HTTP packet format.
- Plugin extension：through this, you can scan restful service in other framework.
- Language & Framework：
  - Support Spring MVC / SpringBoot by default.
  - Support Java and Kotlin.
- Other:
  - Java class convert to JSON.
  
 
## Install
- **Using IDE plugin system**

Recommended <kbd>Preferences(Settings)</kbd> > <kbd>Plugins</kbd> > <kbd>Browse repositories...</kbd> > <kbd>find "RESTKit"</kbd> > <kbd>Install Plugin</kbd>

- **Local Install**

Download plugin form <kbd>distributions/RESTKit-x.x.x.zip</kbd>, then <kbd>Preferences(Settings)</kbd> > <kbd>Plugins</kbd> > <kbd>Install Plugin from Disk...</kbd>

## Usage

### RESTKit Tool window
Open project, find and open RESTKit at right window. RESTKit is composed of four parts: **Toolbar**、**service tree**、**http client**.

![tool window](images/tool_window.png)

#### Toolbar
- Refresh: refresh service list when updated.
- Search: search service in search everywhere.
- Filter: filter by HTTP method.
- Scan library: whether scan with library.
- Setting：open setting view.

![](images/toolbar.png)

#### service tree
- Display services by module.
- Navigate to source when double-clicking in the service list.
- Show context menu when right clicking.

![](images/tree.png)

#### HTTP client
- Environment: select the environment variable that has been added. preview current environment when hovering.
- Method: http method, needn't select manually.
- URL: http uri, needn't input manually. support placeholder, e.g. `{{baseUrl}}`.
- Send: send http request one time after clicking.
- Headers tab: request header, needn't input manually. support placeholder and parameter library.
- Params tab: include query/path/form parameter, needn't input manually. support placeholder and parameter library.
- Body tab: body for POST/PUT/PATCH/DELETE, needn't input manually.
- Response tab: display response result. The content may be normal return, exception, or script return by the request script.
- Info tab: display request with http packet format.

![](images/http_client.png)


### Search URL
- Search everywhere: <kbd>Double Shift</kbd> or click **search icon**。
- When selecting item in search everywhere(URL tab), clicking <kbd>Option</kbd> or <kbd>Alt</kbd> helps to jump to service tree item.
- Service tree: support input search when focus on service tree.

![search everywhere](images/search_everywhere.png)


### Common setting
Provide some common settings for the plugin.

![common setting.png](images/common_setting.png)

#### Where: 
- <kbd>Preferences(Settings)</kbd> > <kbd>Other Settings</kbd> > <kbd>RESTKit</kbd>
- <kbd>RESTKit tool window</kbd> > <kbd>toolbar</kbd> > <kbd>setting</kbd> > <kbd>Common Setting</kbd>

#### Supported web framework
support Spring MVC and enabled by default. // todo
默认支持Spring MVC，勾选即启用。若需要支持其他web框架的restful接口扫描，请参考: [RESTKit扩展](#)

#### 请求配置
- 请求超时: 设置请求超时时长，设置时长小于等于0时不超时
- 启用保存请求日志: 默认不启用，保存路径为 `$PROJECT_DIR$/.idea/restkit/logs/*.log`
- 启用参数库: 默认启用。设置后需重新打开当前项目

#### 请求脚本
设置前置/后置请求脚本路径。当输入框为空时，可双击`Label`自动生成脚本，默认生成路径为: `$PROJECT_DIR$/.idea/restkit/xxx-request Script.js`

![](images/script_setting.png)

### 环境变量
- 环境变量表示提前配置的一组或多组变量，包括`字面量变量`、`直接引用变量`、`内置函数变量`和`脚本变量`。
- 可用于URL、Headers、Params、Body和请求脚本等。
- 通过占位符方式来引用环境变量。
- 每个项目的配置独立（Project级别），支持导入导出。

![environment.png](images/environment.png)

#### 设置
- <kbd>Preferences(Settings)</kbd> > <kbd>Other Settings</kbd> > <kbd>RESTKit</kbd> > <kbd>Environment</kbd>
- <kbd>RESTKit tool window</kbd> > <kbd>toolbar</kbd> > <kbd>setting</kbd> > <kbd>Environment Setting</kbd>

#### 添加
1. 点击<kbd>Add</kbd>，输入唯一的环境变量组名，建议使用简短名称，比如`DEV`、`FAT`、`UAT`、`PRE`、`PRO`。
2. 在当前组下的列表中增加/删除/移动变量键值对，可勾选是否启用。
3. 默认会创建`baseUrl: http://localhost:8080`，用于替换URL输入框的`{{baseUrl}}`
4. **VALUE**为字符串，可使用内置函数变量和脚本变量，参见下文说明。

![env_add.png](images/env_add.png)

#### 复制
从当前环境变量复制一份新的环境变量。点击<kbd>Copy</kbd>，输入唯一的环境变量组名，命名不能重复。

#### 删除
删除当前环境变量组及内容，点击<kbd>Delete</kbd>。

#### 导出&导入
1. 点击<kbd>Export</kbd>将本页配置中的环境变量、环境脚本、全局请求头以JSON格式复制到剪切板。
2. 在需要导入环境变量的项目中打开配置页面，点击<kbd>Import</kbd>。导入的环境变量会替换当前已配置的所有内容。
3. 若导出导入过程中出现异常，请参考`Event Log`中的提示。

#### KEY-VALUE规则
KEY、VALUE均为字符串，其中VALUE支持引用变量，支持如下: 
- 直接引用变量: 引用当前环境变量中已存在的键值对，使用方式: `{{KEY}}`
- 内置函数变量: 默认提供了内置函数，使用方式: `{{$functionName}}`
 - `{{$timestamp}}` 当前时间戳，ms
 - `{{$uuid}}` 生成UUID
- 脚本变量: 点击<kbd>Script Variable</kbd>，在弹出框中编辑脚本变量。目前只支持Java语言，编写规则参考注释，无第三方库支持。使用方式: {{$methodName$}}

```java
public class RestKitScript {

    /**
     * Your script method, no param, method name must from {{$methodName$}}.
     * Use pre-request script can be more powerful.
     *
     * @return return value should be String
     */
    public static String methodName() {
        return "";
    }

}
```

#### 全局请求头
配置当前项目中HTTP请求默认附带的请求头。

![](images/global_header.png)


### 参数库
- 参数库是用于保存请求参数的仓库，支持保存Headers、Params和Body等参数。
- 参数库存在多个，**每个参数库和URL、method 唯一绑定**。
- 在对应编辑器右上角有两个图标<kbd>Save</kbd>和<kbd>List</kbd>，分别对应 **保存** 和 **选择** 参数，其中 **选择** 参数的图标会同时展示当前保存过的数量。

![](images/parameter1.png)

#### 保存参数
保存当前编辑好的参数，以便留给将来使用。点击<kbd>Save</kbd>图标，输入唯一的名称。

![](images/parameter_add.png)

#### 选择参数
点击<kbd>List</kbd>图标，可以看到当前URL和method绑定的参数库。

- 鼠标Hover时会预览当前选择的参数
- 单击鼠标左键，当前选择参数会替换对应编辑器的内容

![](images/parameter_list.png)

#### 管理参数
在参数列表中，每一行对应一个<kbd>Setting</kbd>图标，点击可对该参数重命名和删除。

![](images/parameter_setting.png)

#### 清空所有参数
在当前项目中找到文件 `$PROJECT_DIR$/.idea/restkit/RESTKit_ParameterLibrary.xml`，删除即可。


### 请求脚本
在发送HTTP请求前后，可通过脚本对请求的前后内容进行操作，方便使用，如可以替换token、加密请求等。

> Note  
> 该功能使用了Java Nashorn脚本引擎实现，该引擎计划在JDK11后移除，暂无替换实现。

#### 设置脚本路径
参考本文 `通用设置` > `请求脚本`

![](images/script_setting.png)

#### 前置脚本

- 默认生成的前置脚本位于: `$PROJECT_DIR$/.idea/restkit/Pre-request Script.js`

- 使用说明: 
```js
// You can use custom preset object request and environment, attributes are:
// request attributes
// url:         java.lang.String,               request url, can be modified by pre-request script.
// method:      java.lang.String,               request method, can be modified by pre-request script.
// headers:     java.util.Map<String, String>,  request headers, can be modified by pre-request script.
// params:      java.util.Map<String, String>,  request params, can be modified by pre-request script.
// body:        java.lang.String,               request body, can be modified by pre-request script.
//
// environment: java.util.Map<String, String>,  current environment, defined in the Environment setting, readonly.
//
// See more usages in nashorn-users-guide: https://docs.oracle.com/en/java/javase/12/nashorn/nashorn-users-guide.pdf
```

- 示例: 
```js
var env = environment;
var baseUrl = env.baseUrl;
var username = env['username'];

var req = request;
var url = req.url;
var method = req.method;
var headers = req.headers;
var params = req.params;
var body = req.body;

req.url = 'http://httpbin.org/ip';
req.method = 'GET';
req.headers = {
    'x-auth-ts': '' + new Date().valueOf(),
    'x-auth-traceid': '83b557cc-366a-4274-8912-078e71216c51',
};
req.headers['x-auth-token'] = '70309f2cc6a6462497f824e77baa77f9';
req.params = { code: 'ABCD' };
req.params.name = 'JavaNashorn';
req.body = JSON.stringify({ reqBody: 'Hello world!' });
```

#### 后置脚本
- 默认生成的后置脚本位于: `$PROJECT_DIR$/.idea/restkit/Post-request Script.js`

- 使用说明: 
```js
// You can use custom preset object response and environment, attributes are:
// response attributes
// original:    org.apache.http.HttpResponse,   original http response, from http-client 4.4.
// body:        java.lang.String,               response body can be modified by post-request script.
//
// environment: java.util.Map<String, String>,  current environment, defined in the Environment setting, readonly.
//
// See more usages in nashorn-users-guide: https://docs.oracle.com/en/java/javase/12/nashorn/nashorn-users-guide.pdf
```

- 示例: 
```js
var env = environment;
var baseUrl = env.baseUrl;
var username = env['username'];

var resp = response;
var statusCode = resp.original.getStatusLine().getStatusCode();

if (statusCode != 200) {
    resp.body = JSON.stringify({ error: 'error occurred!' });
} else {
    resp.body = JSON.parse(resp.body).origin;
}
```

#### HTTP请求执行过程

![](images/request_flow.png)


### 插件扩展
RESTKit从`2.0.0`版本开始提供了扩展点`io.github.newhoo.restkit.restful.ep.RestfulResolverProvider`。通过扩展点，你可以提供其他web框架restful接口的扫描方式，以实现在本插件中展示多样化的restful接口。

使用示例: 

- plugin.xml
```xml
<idea-plugin>
    ...
    <depends>io.github.newhoo.restkit</depends>

    <extensions defaultExtensionNs="io.github.newhoo.restkit">
        <!-- your restful resolver implementation -->
        <restfulResolver implementation="io.github.newhoo.restkit.ext.jaxrs.JaxrsResolverProvider"/>
    </extensions>
</idea-plugin>
```
- RestfulResolverProvider instance
```java
public class JaxrsResolverProvider implements RestfulResolverProvider {

    @Override
    public RequestResolver createRequestResolver(@NotNull Project project) {
        return project.getComponent(JaxrsResolver.class);
    }
}
```

完整示例请参阅: [RESTKit-JAX-RS](https://github.com/huzunrong/RESTKit-JAX-RS)


### 其他使用

#### Java Method跳转到service tree
光标移到Java中的restful接口，点击`小灯泡`或者按<kbd>⌥ ↩</kbd>

![](images/intention.png)

#### Java类生成JSON
在需要生成的Java类名称上右键，在弹出的上下文菜单中选择 `Convert to JSON`

![](images/convert2json.png)


## 关于
本插件是作者致力于提升开发效率之作，只有实用常用的功能。源于RestfulToolkit，同时参考了Postman的常用功能，免费分享给大家使用，不用于商业用途。个人之力，难免有疏忽，如有使用问题，请反馈于我。

如果你觉得本插件不错，请赏个好评吧，同时也欢迎提供宝贵的建议。🌟Star | [Ratings](https://plugins.jetbrains.com/plugin/14723-restkit/reviews)


## Contact & Feedback
[Issues](https://github.com/huzunrong/RESTKit-Doc/issues) | [Email](mailto:huzunrong@foxmail.com) | [Ratings & Previews](https://plugins.jetbrains.com/plugin/14723-restkit/reviews)

> Note  
> Please provide necessary information when you feedback: IDEA version, plugin version, exception content, recreation way(if can), desire, and etc.


## 支持作者
如果觉得本插件不错，提升了你的开发效率，那么可以请作者喝杯咖啡吧～您的支持是鼓励我前行的动力，非常感谢。

| ![微信](images/pay/wechat.JPG) | ![支付宝](images/pay/alipay.JPG) |
| --- | --- |
| --- | --- |