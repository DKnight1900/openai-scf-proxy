# 猴子也能学会的腾讯云函数搭建 OpenAI 国内代理教程

> 优势：免费！比 Cloudflare Worker 简单，支持香港等多地区可选，部署简单，一行代码都不用写，有 QQ、微信账号就能注册，猴子也能学会！
> 
> 劣势：不支持 SSE，用户体验欠佳，但完全能用！

PS：本教程不仅仅针对云函数，你也可以托管在自己的服务器上，或者 Azure 等平台，只要能运行 Node.js 程序即可，参加下方[【自托管】](#自托管)部分。

## 你需要准备什么：

- 一台电脑
- 一个腾讯旗下的账号或者手机号
- 一个脑子

## 教程开始

在 [https://cloud.tencent.com/](https://cloud.tencent.com/) 注册账号

进入云函数控制台：[https://console.cloud.tencent.com/scf/list](https://console.cloud.tencent.com/scf/list)

依次点击【新建】->【从头开始】，然后按照以下配置，**没写出来的就不用管，使用默认设置**

- 函数类型：Web函数
- 函数名称：openai-proxy（也可以随便取个名字）
- 地域：香港（也可以是中国之外的任何国家）
- 运行环境：Nodejs 16.13（或者更高的版本）
- 高级配置:
    - 内存：64M
    - 执行超时时间：900 秒
    - 请求多并发：2 并发
- 日志配置 -> 日志投递：启用（可以选择不开，开的话一个月应该几分钱）
- 函数代码：本地上传zip包（[点我下载 ZIP 包](https://github.com/Ice-Hazymoon/openai-scf-proxy/releases/download/0.0.3/openai-proxy.zip)）

之后点击“完成”按钮，进入【函数管理】，点击【函数代码】，往下拉，找到【访问路径】，这里就是你的代理地址，但需要把 "/release" 部分删除

例如：`https://service-aaaaa.hk.apigw.tencentcs.com/release/`

改为：`https://service-aaaaa.hk.apigw.tencentcs.com/`


## 如何使用

你可以在任何支持配置 OpenAI 代理的软件中使用这个服务，例如在 CatGPT 中配置：

进入：[https://ai.okmiku.com/](https://ai.okmiku.com/)

点击右上角的🔑图标，在接口地址中输入这个地址，点击保存即可

愉快的与 OpenAI 一起冲浪吧~

## 自托管

```
git clone https://github.com/Ice-Hazymoon/openai-scf-proxy
cd openai-scf-proxy
npm install
npm run start
```
## 补充注意事项
- 如果【访问路径】为空，可能是没配置【触发管理】
- 首次使用云函数需要账号授权，另外还需要授权API网关，要不然可能会导致部署失败
- 测试：https://xxxx.hk.apigw.tencentcs.com/v1/completions ，返回提示需要API KEY即为成功
- 部署成功后，你的云函数调用链接最好保密，要不然别人也能调用你的
