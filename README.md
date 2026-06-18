# API 余额查询样板

这个项目复刻了 `https://cx.chr1.com/` 的核心做法，并已内置为预言家 API 站：`https://api.yuyanjia.top`。

前端收令牌，后端用这个令牌去内置 API 服务查询余额和调用明细。令牌不会写入前端文件，也不会打印到后端日志里。

目标站的公开代码里使用的是：

- `GET /v1/dashboard/billing/subscription`
- `GET /v1/dashboard/billing/usage?start_date=...&end_date=...`
- `GET /api/log/token`

目标站把接口服务写成了 `https://api.chr1.com`。这里已经换成了 `https://api.yuyanjia.top`。

## 运行

```powershell
npm.cmd start
```

然后打开：

```text
http://localhost:4173
```

默认会连接 `https://api.yuyanjia.top`。请输入你自己的预言家 API 令牌查询。

宝塔如果只有 Node `v14.17.6`，也可以直接选这个稳定版运行。

## 改成别的接口服务

以后如果要临时换接口服务，PowerShell 里这样启动：

```powershell
$env:BASE_URLS_JSON='{"备用接口服务":"https://api.your-domain.com"}'
npm.cmd start
```

多个服务也可以：

```powershell
$env:BASE_URLS_JSON='{"预言家 API站":"https://api.yuyanjia.top","备用服务":"https://backup.your-domain.com"}'
npm.cmd start
```

## 安全注意

- 不要把用户令牌写进前端代码。
- 不要在后端日志里打印令牌。
- 不要把这个工具配置成任意 URL 都能查，避免被人拿去探测你的内网。
- 如果你要查官方 OpenAI 组织用量，现行官方接口更偏向 Admin Key + Usage/Costs API，例如 `GET /v1/organization/costs` 和 `GET /v1/organization/usage/completions`。那和目标站这种旧式余额接口不是同一套东西。
