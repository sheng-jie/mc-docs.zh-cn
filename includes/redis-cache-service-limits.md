---
author: wesmc7777
ms.service: redis-cache
ms.topic: include
origin.date: 11/09/2018
ms.date: 10/29/2019
ms.author: v-junlch
ms.openlocfilehash: 82e5eb0a0d3c38ebba6b4a6a00792a3fa9dbd558
ms.sourcegitcommit: c1ba5a62f30ac0a3acb337fb77431de6493e6096
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "73083723"
---
| 资源 | 限制 |
| --- | --- |
| 缓存大小 |1.2 TB |
| 数据库 |64 |
| 连接的最大客户端数 |40,000 |
| Azure Redis 缓存副本，用于高可用性 |1 |
| 启用群集的高级缓存中的分片数 |10 |

每个定价层的 Azure Redis 缓存限制和大小都不相同。 若要查看定价层及其关联的大小，请参阅 [Azure Redis 缓存定价](https://www.azure.cn/pricing/details/redis-cache/)。

有关 Azure Redis 缓存配置限制的详细信息，请参阅[默认 Redis 服务器配置](../articles/azure-cache-for-redis/cache-configure.md#default-redis-server-configuration)。

由于 Azure Redis 缓存实例的配置和管理是由 Microsoft 执行的，因此 Azure Redis 缓存并非支持所有 Redis 命令。 有关详细信息，请参阅 [Azure Redis 缓存不支持的 Redis 命令](../articles/azure-cache-for-redis/cache-configure.md#redis-commands-not-supported-in-azure-cache-for-redis)。


