---
title: Azure ExpressRoute 的安全控制
description: 用于评估 Azure ExpressRoute 的安全控制的清单
services: expressroute
ms.service: expressroute
documentationcenter: ''
author: msmbaldwin
manager: barbkess
ms.topic: conceptual
origin.date: 06/05/2019
ms.date: 10/08/2019
ms.author: v-yiso
ms.openlocfilehash: b0a14c5480eb9734f5ec9f2a4cdb02aa75e6a535
ms.sourcegitcommit: 2e9b16f155455cd5f0641234cfcb304a568765a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88715134"
---
# <a name="security-controls-for-azure-expressroute"></a>Azure ExpressRoute 的安全控制

本文介绍 Azure ExpressRoute 中内置的安全控制。

[!INCLUDE [Security controls Header](../../includes/security-controls-header.md)]

## <a name="network"></a>网络

| 安全控制 | Yes/No | 注释 |
|---|---|--|
| 服务终结点支持| 不适用 |  |
| VNet 注入支持| 不适用 | |
| 网络隔离和防火墙支持| 是 | 每个客户都包含在自己的路由域中，并通过隧道连接到自己的 VNet |
| 强制隧道支持| 不适用 | 通过边界网关协议 (BGP)。 |

## <a name="monitoring--logging"></a>监视和日志记录

| 安全控制 | Yes/No | 注释|
|---|---|--|
| Azure 监视支持（Log Analytics、App Insights 等）| 是 | 请参阅 [ExpressRoute 监视、指标和警报](expressroute-monitoring-metrics-alerts.md)。|
| 控制和管理平面日志记录和审核| 是 |  |
| 数据平面日志记录和审核| 否 |   |

## <a name="identity"></a>标识

| 安全控制 | Yes/No | 注释|
|---|---|--|
| 身份验证| 是 | 用于 Microsoft 的网关 (GWM)（控制器）的服务帐户；用于开发和操作的实时 (JIT) 访问。 |
| 授权|  是 |用于 Microsoft 的网关 (GWM)（控制器）的服务帐户；用于开发和操作的实时 (JIT) 访问。 |

## <a name="data-protection"></a>数据保护

| 安全控制 | Yes/No | 注释 |
|---|---|--|
| 服务器端静态加密：Microsoft 管理的密钥 |  不适用 | ExpressRoute 不存储客户数据。 |
| 服务器端静态加密：客户管理的密钥 (BYOK) | 不适用 |  |
| 列级加密（Azure 数据服务）| 空值 | |
| 传输中加密（例如 ExpressRoute 加密、VNet 中加密，以及 VNet-VNet 加密）| 否 | |
| 加密的 API 调用| 是 | 通过 [Azure 资源管理器](../azure-resource-manager/index.yml)和 HTTPS。 |


## <a name="configuration-management"></a>配置管理

| 安全控制 | Yes/No | 注释|
|---|---|--|
| 配置管理支持（配置的版本控制等）| 是 | 通过网络资源提供程序 (NRP)。 |

## <a name="next-steps"></a>后续步骤

- 详细了解[跨 Azure 服务的内置安全控制](../security/fundamentals/security-controls.md)。