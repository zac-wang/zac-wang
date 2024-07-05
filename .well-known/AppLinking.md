## App Linking 配置步骤

##### 1、**[创建鸿蒙app](#create-project)**
##### 2、**[修改项目文件module.json5](#edit-project-module.json5)**
##### 3、**[AGC创建项目](#create-agc-project)**
##### 4、**[AGC创建app开发证书相关](#create-agc-app)**

### <h5 id='create-project'>1、创建鸿蒙app</h5>

### <h5 id='edit-project-module.json5'>2、修改项目文件ohos/entry/src/main/module.json5,增加以下内容</h5>

```
{
  "entities": [
    "entity.system.browsable",
  ],
  "actions": [
    "ohos.want.action.viewData",
  ],
  "uris": [
    {
      // scheme须配置为https
      "scheme": "https",
      // host须配置关联的域名
      "host": "zac-wang.github.io",
      // path可选，为了避免匹配到多个应用，建议配置该字段
      "path": "index.html",
    }
  ],
  // domainVerify须设置为true
  "domainVerify": true
}
```

### <h5 id='create-agc-project'>3、AGC创建项目</h5>
去[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/myProject), 
1. 点击“创建项目”
2. 输入项目名,下一步
3. 分析服务,下一步
4. 选择数据处理位置 中国, 点击“开通”,创建完成

### <h5 id='create-agc-cer'>4、AGC创建app开发证书相关</h5>
去[证书、APP ID和Profile](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/harmonyOSDevPlatform/9249519184596237889)
1. 选择APP ID, “新建”
2. 选择HarmonyOS应用,填写你的应用名、包名、分类
3. 所属项目为第3步创建的项目
4. 在开放能力列表中打开: App Linking
5. 点击完成


DevEco Studio 选择构建:生成私钥和证书请求文件
- Key store file:选择New,选择保存地址、输入密码
- 输入Alias
- 输入Countrycode: 86
- Next
- 选择csr保存地址

新增证书
输入证书名称,选择类型,上传生成的csr
点击提交,并下载生成的cer

进入项目,修改工程打包证书为刚才对应的文件、密码

### <h5 id='create-agc-cer'>6、AGC创建applinking</h5>
去[我的项目](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/myProject)选择之前创建的项目
1. 项目设置: 常规: 复制APP ID
2. 替换以下内容中的APP ID,保存为applinking.json
```
{
 "applinking": {
   "apps": [
     {
       "appIdentifier": "APP ID"
     }
   ]
 }
}
```
3. 放在你的服务器.well-known下面,即:https://域名/.well-known/applinking.json


### <h5 id='create-agc-cer'>6、AGC创建applinking</h5>
去[我的项目](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html#/myProject)选择之前创建的项目
1. 选择App Linking, 选择立即开通
2. 创建基础链接, 输入名称、你的服务器域名,点击发布
3. 创建App Linking,无链接前缀 可点击去创建,下一步
4. 深度链接输入你的第一步中 scheme、host、path对应的拼接后的url地址,如果报错去填写配置网址允许清单: ^.*$ ,下一步
5. 设置HarmonyOS链接行为,在浏览器中打开,下一步
6. 跟踪参数和分享标识,默认下一步
7. 勾选显示预览页,点击发布




