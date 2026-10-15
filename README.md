# QuantumultX

个人 Quantumult X 分流规则，按服务分类维护。

## Bank 银行直连

规则文件：[Bank.list](rule/QuantumultX/Bank/Bank.list)

将以下域名及其子域名设为直连：

| 服务 | 域名 |
|---|---|
| Wise | `wise.com`、`transferwise.com` |
| iFAST Global Bank | `ifastgb.com` |
| FSM Global（iFAST 集团投资平台） | `fsm.global`、`fundsupermart.com` |

Wise 的 `api.wise.com`、`api-mtls.transferwise.com` 已由上述后缀规则覆盖。

### 远程订阅

将本项目的改动推送到 GitHub 的 `main` 分支后，使用以下订阅地址：

```text
https://raw.githubusercontent.com/qimingstar/QuantumultX/main/rule/QuantumultX/Bank/Bank.list
```

在 Quantumult X 配置的 `[filter_remote]` 区段添加以下一行；已有该区段时直接追加内容：

```ini
https://raw.githubusercontent.com/qimingstar/QuantumultX/main/rule/QuantumultX/Bank/Bank.list, tag=Bank直连, force-policy=direct, enabled=true
```

将这条资源放在可能匹配这些银行服务的通用代理资源之前，并检查已有本地规则是否抢先匹配。保存配置并更新远程资源，在分流模式下使用。

### 从旧 Wise 订阅迁移

将手机上原有资源地址中的 `Wise/Wise.list` 改为 `Bank/Bank.list`，名称改为 `Bank直连`，然后更新资源，应加载 5 条规则。旧 Wise 地址保留相同内容以兼容已有订阅；不必同时添加两个资源。

### 本地添加

也可以直接在现有配置的 `[filter_local]` 区段添加以下规则，并放在通用规则及 `final` 规则之前：

```ini
host-suffix, wise.com, direct
host-suffix, transferwise.com, direct
host-suffix, ifastgb.com, direct
host-suffix, fsm.global, direct
host-suffix, fundsupermart.com, direct
```

### 验证

打开 Wise 和 iFAST GB App，执行登录、查看账户等常用操作，在 Quantumult X 网络活动日志中确认对应域名命中 `direct`。这些规则按域名匹配；其他第三方域名仍按现有配置处理，需根据实际日志确认是否补充。

## 参考

- [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)：参考分类目录结构。
- [Wise 域名讨论](https://github.com/blackmatrix7/ios_rule_script/discussions/1386)：初始域名范围参考。
- [Quantumult X 官方配置示例](https://github.com/crossutility/Quantumult-X/blob/master/sample.conf)：配置格式参考。

- [Wise 官方 API 环境说明](https://docs.wise.com/guides/developer)：生产 API 域名依据。
- [iFAST Global Bank 官网](https://www.ifastgb.com/)：银行官方域名依据。

当前规则面向日常银行访问。Wise 开发测试沙箱不纳入该集合；第三方身份验证、客服等域名根据手机网络活动日志逐项确认后补充。

- [FSM Global 官网](https://fsm.global/)：iFAST 集团归属说明。
- [iFAST 集团业务页面](https://www.ifastcorp.com/ifastcorp/business/business-divisions.tpl)：FSM Global 与 Fundsupermart 平台依据。
