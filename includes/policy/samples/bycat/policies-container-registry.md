---
author: rockboyfor
ms.service: azure-policy
ms.topic: include
origin.date: 05/05/2020
ms.date: 05/29/2020
ms.author: v-yeche
ms.custom: generated
ms.openlocfilehash: 76d70e50aeb6c17b684f32b3b7f63fe75b72251d
ms.sourcegitcommit: be0a8e909fbce6b1b09699a721268f2fc7eb89de
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84199287"
---
|名称 |说明 |效果 |版本 |GitHub |
|---|---|---|---|---|
|[容器注册表应使用客户托管密钥 (CMK) 进行加密](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5b9159ae-1701-4a6f-9a7a-aa9c8ddd0580) |审核未通过客户托管密钥 (CMK) 启用加密的容器注册表。 有关 CMK 加密的详细信息，请访问：[https://aka.ms/acr/CMK](https://aka.ms/acr/CMK)。 |Audit、Disabled |1.0.0-preview |[链接](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Container%20Registry/ACR_CMKEncryptionEnabled_Audit.json)。
|[容器注册表不得允许无限制的网络访问](https://portal.azure.cn/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd0793b48-0edc-4296-a390-4c75d1bdfd71) |审核容器注册表，这些注册表默认情况下未配置任何网络（IP 或 VNET）规则，因此允许所有网络访问。 如果容器注册表至少有一个 IP/防火墙规则或配置了虚拟网络，则会将其视为合规。 有关容器注册表网络规则的详细信息，请访问：[https://aka.ms/acr/vnet](https://aka.ms/acr/vnet)。 |Audit、Disabled |1.0.0-preview |[链接](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Container%20Registry/ACR_NetworkRulesExist_Audit.json)。

<!-- Update_Description: update meta properties, wording update, update link -->