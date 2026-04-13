# DemonMarket

这是我维护的 DemonMarket 分支，当前主要目标是修复高版本 Paper/Spigot 环境下的兼容性问题，而不是重复整理原项目的完整功能说明。

## 我修改了什么

### 修复 1.21.1 打开收购列表时报错

在 Paper 1.21.1 上，旧版 `worth.yml` 中的部分材质名会触发类似下面的异常：

```text
java.lang.IllegalArgumentException: WATER isn't an item
```

这次修复的内容主要包括：

- 调整 `PluginUtil.getItem()` 的材质解析逻辑，避免把 `WATER`、`LAVA` 这类已经不是可直接创建 `ItemStack` 的材质继续当作物品使用
- 为旧配置中的历史材质名增加兼容映射，例如 `WATER`、`STATIONARYWATER`、`LAVA`、`STATIONARYLAVA`
- 增加回归测试，确保旧材质名在后续改动里不会再次导致 1.21.1 崩溃

## 当前适用场景

如果你正在使用这个 fork，主要是为了解决：

- Paper 1.21.1 启动或打开 GUI 时的物品兼容问题
- 老版本配置文件迁移到新版本服务端后的材质解析报错

## 构建说明

本地验证使用的是 `JDK 17`：

```bash
mvn -q -Dtest=PluginUtilCompatibilityTest test
mvn -q -DskipTests package
```

产物默认在：

```text
target/DemonMarket-1.7.jar
```

## 上游项目

原作者项目地址：

- [Tining123/DemonMarket](https://github.com/Tining123/DemonMarket)

如果你想查看插件原始介绍、功能说明、命令、配置项和历史文档，请直接参考原作者仓库。这个 fork 的 README 主要只记录我额外做过的修复和维护内容。
