---
title: Azure Monitor 中的指标 - Azure 事件中心 | Microsoft Docs
description: 本文介绍如何使用 Azure 监视功能来监视 Azure 事件中心
ms.topic: article
origin.date: 06/23/2020
ms.date: 08/21/2020
ms.author: v-tawe
ms.openlocfilehash: f7f4a1f5be3e460096bd21f17486c0b823549c68
ms.sourcegitcommit: 2e9b16f155455cd5f0641234cfcb304a568765a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88715120"
---
# <a name="azure-event-hubs-metrics-in-azure-monitor"></a>Azure Monitor 中的 Azure 事件中心指标

事件中心指标可提供 Azure 订阅中的事件中心资源状态。 通过多种指标数据集，可在命名空间和实体级别评估事件中心的总体运行状况。 由于它们能够帮助监视事件中心的状态，因此这些统计信息非常重要。 另外，指标也可帮助解决由根本原因造成的问题，而无需联系 Azure 支持。

Azure Monitor 提供了统一的用户界面，可用于监视各种 Azure 服务。 有关详细信息，请参阅 GitHub 上的[在 Microsoft Azure 中进行监视](../azure-monitor/overview.md)和[通过 .NET 检索 Azure Monitor 指标](https://github.com/Azure-Samples/monitor-dotnet-metrics-api)示例。

## <a name="access-metrics"></a>访问指标

Azure Monitor 提供多种访问指标的方法。 可通过 [Azure 门户](https://portal.azure.cn)、Azure Monitor API（REST 和 .Net）与分析解决方案（例如 Log Analytics 和事件中心）访问指标。 有关详细信息，请参阅 [Azure Monitor 收集的监视数据](../azure-monitor/platform/data-platform.md)。

默认情况下，已启用指标，并且可访问最近 30 天的数据。 如需将数据保留更长一段时间，可将指标数据存档到 Azure 存储帐户。 可在 Azure Monitor 的 [诊断设置](../azure-monitor/platform/diagnostic-settings.md) 中完成这种配置。


## <a name="access-metrics-in-the-portal"></a>在门户中访问指标

可在 [Azure 门户](https://portal.azure.cn)中监视一段时间内的指标。 以下示例演示了如何在帐户级别查看成功的请求和传入的请求：

![查看成功的指标][1]

也可以直接通过命名空间来访问指标。 为此，请选择命名空间，然后单击“指标”  。 若要显示筛选到事件中心范围的指标，请选择事件中心，然后单击“指标”  。

对于支持维度的指标，必须使用所需的维度值进行筛选，如以下示例所示：

![使用维度值进行筛选][2]

## <a name="billing"></a>计费

目前，在 Azure Monitor 中可以免费使用指标。 但是，如果使用引入指标数据的其他解决方案，可能就需要收费。 例如，如果将指标数据存档到 Azure 存储帐户，则 Azure 存储会收费。

<!-- Not Available on Log Analytics for advanced analysis -->

以下指标可提供服务运行状况的概述。 

> [!NOTE]
> 我们弃用了多个指标，因为它们已移动到不同的名称下。 这可能会要求你更新引用。 今后将不再支持标有“弃用的”关键字的指标。

所有指标值每隔一分钟发送到 Azure Monitor。 时间粒度定义了提供指标值的时间间隔。 所有事件中心指标所支持的时间间隔为一分钟。

## <a name="request-metrics"></a>请求指标

计算数据量和管理操作请求数。

| 标准名称 | 说明 |
| ------------------- | ----------------- |
| 传入请求数  | 在指定期间内向 Azure 事件中心服务发送的请求数。 <br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName |
| 成功的请求数    | 在指定期间内向 Azure 事件中心服务发送成功的请求数。 <br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName |
| 服务器错误数  | 由于 Azure 事件中心服务发生错误，在指定期间内未处理的请求数。 <br/><br/>单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName |
|用户错误数 |由于存在用户错误，在指定期间内未处理的请求数。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|
|超过配额错误 |超出可用配额的请求数。 有关事件中心配额的详细信息，请参阅[本文](event-hubs-quotas.md)。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|

## <a name="throughput-metrics"></a>吞吐量指标

| 标准名称 | 说明 |
| ------------------- | ----------------- |
|限制的请求数 |由于超出吞吐量单位用量而被限制的请求数。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|

## <a name="message-metrics"></a>消息指标

| 标准名称 | 说明 |
| ------------------- | ----------------- |
|传入消息数 |在指定期间内发送到事件中心的事件或邮件数。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|
|传出消息数 |在指定期间内从事件中心检索的事件或邮件数。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|
|传入字节数 |在指定期间内向 Azure 事件中心服务发送的字节数。<br/><br/> 单元：字节 <br/> 聚合类型：总计 <br/> 维度：EntityName|
|传出字节数 |在指定期间内从 Azure 事件中心服务检索的字节数。<br/><br/> 单元：字节 <br/> 聚合类型：总计 <br/> 维度：EntityName|

## <a name="connection-metrics"></a>连接指标

| 标准名称 | 说明 |
| ------------------- | ----------------- |
|ActiveConnections |命名空间以及实体上的活动连接数。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|
|打开的连接数 |打开的连接数。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|
|关闭的连接数 |关闭的连接数。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|

## <a name="event-hubs-capture-metrics"></a>事件中心捕获指标

当为事件中心启用捕获功能时，即可监视事件中心捕获指标。 以下指标描述了在启用捕获的情况下可监视的内容。

| 标准名称 | 说明 |
| ------------------- | ----------------- |
|捕获积压工作 (backlog) |尚未捕获到所选目标的字节数。<br/><br/> 单元：字节 <br/> 聚合类型：总计 <br/> 维度：EntityName|
|捕获的消息数 |在指定期间内捕获到所选目标的邮件或事件数。<br/><br/> 单位：计数 <br/> 聚合类型：总计 <br/> 维度：EntityName|
|捕获的字节数 |在指定期间内捕获到所选目标的字节数。<br/><br/> 单元：字节 <br/> 聚合类型：总计 <br/> 维度：EntityName|

## <a name="metrics-dimensions"></a>指标维度

Azure 事件中心支持对 Azure Monitor 中的指标使用以下维度。 为指标添加维度是可选的。 如果不添加维度，则指标是在命名空间级别指定的。 

| 标准名称 | 说明 |
| ------------------- | ----------------- |
|EntityName| 事件中心支持命名空间下的事件中心实体。|

## <a name="azure-monitor-integration-with-siem-tools"></a>Azure Monitor 与 SIEM 工具集成
使用 Azure Monitor 将监视数据（活动日志、诊断日志等）路由到事件中心，可以轻松地与安全信息和事件管理 (SIEM) 工具集成。 有关详细信息，请参阅以下文章/博客文章：

<!-- - [Introduction to Azure Log Integration](../security/fundamentals/azure-log-integration-overview.md) -->

- [将 Azure 监视数据流式传输到事件中心以便外部工具使用](../azure-monitor/platform/stream-monitoring-data-event-hubs.md)
- [使用 Azure Monitor 与 SIEM 工具集成](https://azure.microsoft.com/blog/use-azure-monitor-to-integrate-with-siem-tools/)

在 SIEM 工具使用事件中心的日志数据的情况下，如果在指标图中看不到传入消息，或者看到传入消息但看不到传出消息，请按照下列步骤操作：

- 如果**没有传入消息**，则表示 Azure Monitor 服务没有将审核/诊断日志移到事件中心。 在此方案中，通过 Azure Monitor 团队建立支持票证。 
- 如果有传入消息，但**没有传出消息**，则意味着 SIEM 应用程序未读取消息。 请与 SIEM 提供者联系，以确定这些应用程序的事件中心配置是否正确。


## <a name="next-steps"></a>后续步骤

* 请参阅 [Azure 监视概述](../azure-monitor/overview.md)。
* [通过 .NET 检索 Azure Monitor 指标](https://github.com/Azure-Samples/monitor-dotnet-metrics-api)示例。 

有关事件中心的详细信息，请访问以下链接：

- 事件中心入门教程
    - [.NET Core](get-started-dotnet-standard-send-v2.md)
    - [Java](get-started-java-send-v2.md)
    - [Python](get-started-python-send-v2.md)
    - [JavaScript](get-started-java-send-v2.md)
* [事件中心常见问题解答](event-hubs-faq.md)
* [使用事件中心的示例应用程序](https://github.com/Azure/azure-event-hubs/tree/master/samples)

[1]: ./media/event-hubs-metrics-azure-monitor/event-hubs-monitor1.png
[2]: ./media/event-hubs-metrics-azure-monitor/event-hubs-monitor2.png
