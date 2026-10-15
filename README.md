# QuantumultX

个人 Quantumult X 分流规则，按服务分类维护。

## Wise 直连

规则文件：[Wise.list](rule/QuantumultX/Wise/Wise.list)

将 `wise.com`、`transferwise.com` 及其子域名设为直连。

### 远程订阅

将本项目的改动推送到 GitHub 的 `main` 分支后，使用以下订阅地址：

```text
https://raw.githubusercontent.com/qimingstar/QuantumultX/main/rule/QuantumultX/Wise/Wise.list
```

在 Quantumult X 配置的 `[filter_remote]` 区段添加以下一行；已有该区段时直接追加内容：

```ini
https://raw.githubusercontent.com/qimingstar/QuantumultX/main/rule/QuantumultX/Wise/Wise.list, tag=Wise直连, force-policy=direct, enabled=true
```

将这条资源放在可能匹配 Wise 的通用代理资源之前，并检查已有本地规则是否抢先匹配。保存配置并更新远程资源，在分流模式下使用。

### 本地添加

也可以直接在现有配置的 `[filter_local]` 区段添加以下规则，并放在通用规则及 `final` 规则之前：

```ini
host-suffix, wise.com, direct
host-suffix, transferwise.com, direct
```

### 验证

打开 Wise App，执行登录、查看账户等常用操作，在 Quantumult X 网络活动日志中确认对应域名命中 `direct`。这些规则按域名匹配；其他第三方域名仍按现有配置处理，需根据实际日志确认是否补充。

## 参考

- [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)：参考分类目录结构。
- [Wise 域名讨论](https://github.com/blackmatrix7/ios_rule_script/discussions/1386)：初始域名范围参考。
- [Quantumult X 官方配置示例](https://github.com/crossutility/Quantumult-X/blob/master/sample.conf)：配置格式参考。
