# GLOSSARY-MAP 格式

仓库有多个上下文时，根目录放 `GLOSSARY-MAP.md`，指出各上下文所在位置及其相互关系。

## 结构

```
# 术语表地图（Glossary Map）

## 上下文
- [上下文名](./路径/GLOSSARY.md): 一句职责

## 关系
- **上下文A → 上下文B**：交互描述（谁发出/消费什么事件、共享什么类型）
```

示例（仅示格式，内容不得沿用）：
- [订单（Ordering）](./src/ordering/GLOSSARY.md): 接收并跟踪客户订单
- [履约（Fulfillment）](./src/fulfillment/GLOSSARY.md): 管理仓库拣货与发货
- **订单 → 履约**：订单发出 `OrderPlaced` 事件；履约消费它开始拣货
- **订单 ↔ 计费**：共享 `CustomerId` 与 `Money` 类型

## 规则

1. 上下文清单：名称链接到该上下文自己的 GLOSSARY.md，附一句职责。
2. 关系：描述两两间的真实交互（事件流/共享类型/依赖方向），不写空泛的「相关」。
3. 示例仅示格式，内容来自当前项目。
