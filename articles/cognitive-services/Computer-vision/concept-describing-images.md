---
title: 描述图像 - 计算机视觉
titleSuffix: Azure Cognitive Services
description: 与计算机视觉 API 的图像描述功能相关的概念。
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: conceptual
origin.date: 02/11/2019
ms.date: 02/27/2019
ms.author: v-junlch
ms.custom: seodec18
ms.openlocfilehash: 6cd3540464c4e61088e560e249207db194555c4f
ms.sourcegitcommit: c1ba5a62f30ac0a3acb337fb77431de6493e6096
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "63860470"
---
# <a name="describe-images-with-human-readable-language"></a>使用人类可读语言描述图像

计算机视觉可以分析图像并生成描述其内容的人工可读的句子。 该算法实际返回基于不同视觉功能的多个描述，且每个描述都有一个可信度分数。 最终输出是按可信度从高到低排列的描述的列表。

## <a name="image-description-example"></a>图像说明示例

以下 JSON 响应表明计算机视觉在基于视觉特征对示例图像进行描述时返回的内容。

![曼哈顿建筑的黑白照片](./Images/bw_buildings.png)

```json
{
    "description": {
        "tags": ["outdoor", "building", "photo", "city", "white", "black", "large", "sitting", "old", "water", "skyscraper", "many", "boat", "river", "group", "street", "people", "field", "tall", "bird", "standing"],
        "captions": [
            {
                "text": "a black and white photo of a city",
                "confidence": 0.95301952483304808
            },
            {
                "text": "a black and white photo of a large city",
                "confidence": 0.94085190563213816
            },
            {
                "text": "a large white building in a city",
                "confidence": 0.93108362931954824
            }
        ]
    },
    "requestId": "b20bfc83-fb25-4b8d-a3f8-b2a1f084b159",
    "metadata": {
        "height": 300,
        "width": 239,
        "format": "Jpeg"
    }
}
```

## <a name="next-steps"></a>后续步骤

了解[标记图像](concept-tagging-images.md)和[对图像进行分类](concept-categorizing-images.md)的概念。

<!-- Update_Description: wording update -->