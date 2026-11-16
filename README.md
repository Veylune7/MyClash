# MyClash

Mihomo（Clash Meta）分流配置，开箱即用。同时提供 **普通版（mihomo 内核）** 和 **FlClash 版（Concord 内核）** 两套文件，按客户端内核二选一，不要混用。

> 基于 [AIsouler/MyClash](https://github.com/AIsouler/MyClash) 二次修改，
> 核心改动：**AI 分组的规则集替换为 [viewer12/OverseasAI.list](https://github.com/viewer12/OverseasAI.list)**，
> 覆盖更全（OpenAI / Claude / Gemini / Copilot / Civitai 等 600+ 条规则）。

## 🚀 快速开始

把下面对应链接填进客户端的「订阅 / 配置 URL」即可。

### 普通版（mihomo 内核：Bettbox、Clash Verge、旧版 FlClash 等）

**全量版**（完整分组：AI / 流媒体 / 游戏 / 电报 / 苹果 / 微软 / 谷歌等）

```
https://raw.githubusercontent.com/Veylune7/MyClash/main/Config/mihomoConfig.yaml
```

**精简版**（保留常用分组，体积更小，低内存设备友好）

```
https://raw.githubusercontent.com/Veylune7/MyClash/main/Config/mihomoConfigLite.yaml
```

### FlClash 版（Concord 内核：新版 FlClash）

先在 FlClash「设置 → 关于 / 核心状态」确认内核：显示 `concord` 用这一套，显示 `mihomo` 用上面的普通版。Concord 版删掉了 Concord 不支持的参数（`path-in-bundle`、`bind-address`、`external-controller`、`external-ui`、`tun.auto-redirect`），其余分组、规则、DNS 与普通版一致。详细说明见 [FlClash（Concord 内核）使用说明](./Docs/FlClashConcord.md)。

**全量版**

```
https://raw.githubusercontent.com/Veylune7/MyClash/main/Config/concordConfig.yaml
```

**精简版**

```
https://raw.githubusercontent.com/Veylune7/MyClash/main/Config/concordConfigLite.yaml
```

> ⚠️ 导入后**必须**在配置里填入自己的机场订阅链接：
> 找到 `proxy-providers` → `provider1` → `url: ''`，把订阅链接填进单引号里。
> 如需添加第二个订阅，复制 `provider1` 整块改名为 `provider2` 即可（文件里有注释示例）。

## 🤖 AI 分组说明

AI 分组默认走「美国」节点（可在策略组里手动切换）。

- **规则源**：[viewer12/OverseasAI.list](https://github.com/viewer12/OverseasAI.list)
- **规则数**：约 618 条（DOMAIN 50 / DOMAIN-SUFFIX 553 / DOMAIN-KEYWORD 11 / IP-CIDR 2 / IP-ASN 2）
- **更新频率**：规则源每天更新，配置每天自动拉取（`interval: 86400`）
- **覆盖范围**：OpenAI、Claude、Anthropic、Gemini、Copilot、Civitai，以及 Stripe、PayPal、Nvidia、JetBrains AI 等
- **技术细节**：`behavior: classical` + `format: text`（该规则集为混合类型文本规则，不能用原来的 `domain` / `mrs` 二进制格式）

## 📱 在 FlClash 中使用

1. 先确认内核（设置 → 关于 / 核心状态）：`concord` 用 FlClash 版链接，`mihomo` 用普通版链接
2. 侧边栏 → 配置 → 右上角 ＋ → **URL**，粘贴对应链接
3. 等待下载完成，点击设为当前配置
4. 点右上角 ✏️ 编辑配置，找到 `proxy-providers.provider1.url`，填入机场订阅链接后保存
5. 回到首页 → 代理 → 选择各分组节点（AI 分组默认美国，可按需切换）

其他 Mihomo 内核客户端（Clash Verge、NekoBox 等）同理：导入普通版 URL → 填订阅 → 选节点。

## 📜 覆写脚本（Bettbox 可视化开关）

直接用上面的 YAML 订阅即可；如果你用 **Bettbox**，还可以挂上覆写脚本，在 App 里一键开关各个服务分组：

**普通版（mihomo）精简版脚本**

```
https://raw.githubusercontent.com/Veylune7/MyClash/main/Script/Script.js
```

**普通版（mihomo）完整版脚本**

```
https://raw.githubusercontent.com/Veylune7/MyClash/main/Script/mihomoScript.js
```

**FlClash 版（Concord）完整版脚本**

```
https://raw.githubusercontent.com/Veylune7/MyClash/main/Script/concordScript.js
```

**FlClash 版（Concord）精简版脚本**

```
https://raw.githubusercontent.com/Veylune7/MyClash/main/Script/concordScriptLite.js
```

用法（Bettbox）：订阅卡片 → 覆写 → 脚本，填入上面对应链接。之后在覆写设置里会出现各服务的可视化开关（AI、GitHub、Google、Telegram 等），关掉某个开关后该分组消失、对应流量回落到默认代理。

两个脚本同样基于上游二次修改：AI 规则集换成 OverseasAI.list，并新增了 GitHub 开关。

## 🔄 与原版的区别

| | 原版 AIsouler/MyClash | 本仓库 |
|---|---|---|
| AI 规则集 | `category-ai-!cn.mrs`（geosite 二进制） | `OverseasAI.list`（classical 文本，规则更多更全） |
| 内核版本 | mihomo + Concord 两套 | 同样两套：普通版（mihomo）+ FlClash 版（Concord），定制一致 |
| 图标 | 原仓库 CDN | 沿用原仓库 CDN（稳定，暂不迁移） |
| 其余分组/规则 | — | 与原版一致，另有 GitHub / 韩国 / 月饼Emby 分组与链式代理（默认关） |

## 🙏 致谢与授权

- 配置框架：[AIsouler/MyClash](https://github.com/AIsouler/MyClash)（MIT License，原作者署名保留，见 [LICENSE](./LICENSE)）
- AI 规则集：[viewer12/OverseasAI.list](https://github.com/viewer12/OverseasAI.list)
- 其他规则源：[appshubcc/bett-rules](https://github.com/appshubcc/bett-rules)

本仓库同样以 MIT 协议发布，可自由使用、修改和分享。
