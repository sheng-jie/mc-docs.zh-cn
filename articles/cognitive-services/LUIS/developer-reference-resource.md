---
title: 开发人员资源 - 语言理解
description: SDK、REST API、CLI 用于以编程语言开发语言理解 (LUIS) 应用。 管理 Azure 资源和 LUIS 预测。
ms.topic: reference
origin.date: 05/19/2020
ms.date: 08/04/2020
ms.author: v-johya
ms.custom: devx-track-javascript
ms.openlocfilehash: edb3df4e84ea961c563d6cf31b024bd58aea6bfe
ms.sourcegitcommit: caa18677adb51b5321ad32ae62afcf92ac00b40b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/08/2020
ms.locfileid: "88023362"
---
# <a name="sdk-rest-and-cli-developer-resources-for-language-understanding-luis"></a>用于语言理解 (LUIS) 的 SDK、REST 和 CLI 开发人员资源

SDK、REST API、CLI 用于以编程语言开发语言理解 (LUIS) 应用。 管理 Azure 资源和 LUIS 预测。

## <a name="azure-resource-management"></a>Azure 资源管理

使用 Azure 认知服务的“管理”层来创建、编辑、列出和删除语言理解或认知服务资源。

根据以下工具来查找参考文档：

* [Azure CLI](/cli/cognitiveservices#az-cognitiveservices-list)

* [Azure RM PowerShell](https://docs.microsoft.com/powershell/module/azurerm.cognitiveservices/?view=azurermps-4.4.1#cognitive_services)


## <a name="language-understanding-authoring-and-prediction-requests"></a>语言理解创作和预测请求

可以从需要创建的 Azure 资源访问语言理解服务。 有两个资源：

* 使用**创作**资源进行训练，以便创建、编辑、训练和发布内容。
* 将**预测**用于运行时，以便发送用户的文本并接收预测。

了解 [V3 预测终结点](luis-migration-api-v3.md)。

使用[认知服务示例代码](https://github.com/Azure-Samples/cognitive-services-quickstart-code)，了解并使用最常见的任务。

### <a name="rest-specifications"></a>REST 规范

GitHub 上公开提供 [LUIS REST 规范](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/cognitiveservices/data-plane/LUIS)以及所有 [Azure REST 规范](https://github.com/Azure/azure-rest-api-specs)。

### <a name="rest-apis"></a>REST API

创作终结点 API 和预测终结点 API 都可在 REST API 中使用：

|类型|版本|
|--|--|
|创作|[V2](https://dev.cognitive.azure.cn/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f)<br>[预览 V3](https://dev.cognitive.azure.cn/docs/services/luis-programmatic-apis-v3-0-preview)|
|预测|[V2](https://dev.cognitive.azure.cn/docs/services/5819c76f40a6350ce09de1ac/operations/5819c77140a63516d81aee78)<br>[V3](https://dev.cognitive.azure.cn/docs/services/luis-endpoint-api-v3-0/)|

### <a name="rest-endpoints"></a>REST 终结点

LUIS 目前有 2 种类型的终结点：

* 在训练终结点上进行创作
* 运行时终结点上的查询预测。

|目的|URL|
|--|--|
|在训练终结点上进行 V2 创作|`https://{your-resource-name}.cognitiveservices.azure.cn/luis/api/v2.0/apps/{appID}/`|
|在训练终结点上进行 V3 创作|`https://{your-resource-name}.cognitiveservices.azure.cn/luis/authoring/v3.0-preview/apps/{appID}/`|
|V2 预测 - 运行时终结点上的所有预测|`https://{your-resource-name}.cognitiveservices.azure.cn/luis/v2.0/apps/{appId}?q={q}[&timezoneOffset][&verbose][&spellCheck][&staging][&bing-spell-check-subscription-key][&log]`|
|V3 预测 - 运行时终结点上的版本预测|`https://{your-resource-name}.cognitiveservices.azure.cn/luis/prediction/v3.0/apps/{appId}/versions/{versionId}/predict?query={query}[&verbose][&log][&show-all-intents]`|
|V3 预测 - 运行时终结点上的槽预测|`https://{your-resource-name}.cognitiveservices.azure.cn/luis/prediction/v3.0/apps/{appId}/slots/{slotName}/predict?query={query}[&verbose][&log][&show-all-intents]`|

下表说明了上表中用大括号 `{}` 表示的参数。

|参数|目的|
|--|--|
|`your-resource-name`|Azure 资源名称|
|`q` 或 `query`|从客户端应用程序（如聊天机器人）发送的话语文本|
|`version`|10 字符版本名称|
|`slot`| `production` 或 `staging`|

### <a name="rest-query-string-parameters"></a>REST 查询字符串参数

[!INCLUDE [V3 query params](./includes/v3-prediction-query-params.md)]

## <a name="app-schema"></a>应用架构

[应用架构](app-schema-definition.md)以 `.json` 或 `.lu` 格式导入和导出。

### <a name="language-based-sdks"></a>基于语言的 SDK

|语言 |参考文档|程序包|快速入门|
|--|--|--|--|
|C#|[创作](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.language.luis.authoring?view=azure-dotnet)</br>[预测](https://docs.microsoft.com/dotnet/api/microsoft.azure.cognitiveservices.language.luis.runtime?view=azure-dotnet)|[NuGet 创作](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Language.LUIS.Authoring/)<br>[NuGet 预测](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Language.LUIS.Runtime/)|[创作](sdk-authoring.md?pivots=programming-language-csharp)<br>[查询预测](sdk-query-prediction-endpoint.md?pivots=programming-language-csharp)|
|Go|[创作和预测](https://godoc.org/github.com/Azure/azure-sdk-for-go/services/cognitiveservices/v2.0/luis)|[SDK](https://github.com/Azure/azure-sdk-for-go/tree/master/services/cognitiveservices/v2.0/luis)||
|Java|[创作和预测](https://docs.microsoft.com/java/api/overview/cognitiveservices/client/languageunderstanding?view=azure-java-stable)|[Maven 创作](https://search.maven.org/artifact/com.microsoft.azure.cognitiveservices/azure-cognitiveservices-luis-authoring)<br>[Maven 预测](https://search.maven.org/artifact/com.microsoft.azure.cognitiveservices/azure-cognitiveservices-luis-runtime)|
|Javascript|[创作](https://docs.microsoft.com/javascript/api/@azure/cognitiveservices-luis-authoring/?view=azure-node-latest)<br>[预测](https://docs.microsoft.com/javascript/api/@azure/cognitiveservices-luis-runtime/?view=azure-node-latest)|[NPM 创作](https://www.npmjs.com/package/@azure/cognitiveservices-luis-authoring)<br>[NPM 预测](https://www.npmjs.com/package/@azure/cognitiveservices-luis-runtime)|[创作](sdk-query-prediction-endpoint.md?pivots=programming-language-javascript)<br>[预测](sdk-query-prediction-endpoint.md?pivots=programming-language-javascript)|
|Python|[创作和预测](sdk-authoring.md?pivots=programming-language-python)|[Pip](https://pypi.org/project/azure-cognitiveservices-language-luis/)|[创作](sdk-authoring.md?pivots=programming-language-python)<br>[预测](sdk-query-prediction-endpoint.md?pivots=programming-language-python)|


### <a name="containers"></a>容器

语言理解 (LUIS) 提供一个可提供本地版和包含版应用的[容器](luis-container-howto.md)。

### <a name="export-and-import-formats"></a>导出和导入格式

语言理解提供以 JSON 格式管理应用及其模型的功能，并提供 `.LU` ([LUDown](https://github.com/microsoft/botbuilder-tools/blob/master/packages/Ludown)) 格式以及用于语言理解容器的压缩包。

可以通过 API 和 LUIS 门户导入和导出这些格式。 此门户通过“应用”列表和“版本”列表提供导入和导出功能。

## <a name="workshops"></a>研讨会

* GitHub：（研讨会）[Conversational-AI：使用 LUIS 的 NLU](https://github.com/GlobalAICommunity/Workshop-Conversational-AI)

<!-- Devops not available in mc-->
## <a name="bot-framework-tools"></a>Bot Framework 工具

Bot Framework 在多种语言中以 [SDK](https://github.com/Microsoft/botframework) 形式提供，并通过 [Azure 机器人服务](https://dev.botframework.com/)以服务形式提供。

Bot Framework 提供有助于语言理解的[多种工具](https://github.com/microsoft/botbuilder-tools)，其中包括：

* [LUDown](https://github.com/microsoft/botbuilder-tools/blob/master/packages/Ludown) - 使用 Markdown 文件构建 LUIS 语言理解模型
* [LUIS CLI](https://github.com/microsoft/botbuilder-tools/blob/master/packages/LUIS) - 创建并管理 luis.azure.cn 应用程序
* [Dispatch](https://github.com/microsoft/botbuilder-tools/blob/master/packages/Dispatch)- 管理父应用和子应用
* [LUISGen](https://github.com/microsoft/botbuilder-tools/blob/master/packages/LUISGen) - 为 LUIS 意向和实体自动生成 C#/Typescript 支持类。
* [Bot Framework Emulator](https://github.com/Microsoft/BotFramework-Emulator/releases) - 一款桌面应用程序，可让机器人开发人员测试和调试使用 Bot Framework SDK 构建的机器人。
* [Bot Framework Composer](https://github.com/microsoft/BotFramework-Composer/blob/stable/README.md) - 一个集成开发工具，供开发人员和多学科团队通过 Microsoft Bot Framework 构建机器人和聊天体验
* [Bot Framework 示例](https://github.com/microsoft/botbuilder-samples) - 使用 #C、JavaScript、TypeScript 和 Python 编写
## <a name="next-steps"></a>后续步骤

* 了解常见的 [HTTP 错误代码](luis-reference-response-codes.md)
* 所有 API 和 SDK 的[参考文档](https://docs.azure.cn/index#pivot=sdkstools)
* [Bot Framework](https://github.com/Microsoft/botbuilder-dotnet) 和 [Azure 机器人服务](https://dev.botframework.com/)
* [LUDown](https://github.com/microsoft/botbuilder-tools/blob/master/packages/Ludown)
* [认知容器](../cognitive-services-container-support.md)

