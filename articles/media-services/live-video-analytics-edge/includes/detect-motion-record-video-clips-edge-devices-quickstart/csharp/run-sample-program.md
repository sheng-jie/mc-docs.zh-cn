---
ms.openlocfilehash: 587808df1f2457f9f24738a2cffdddd4064548eb
ms.sourcegitcommit: 2eb5a2f53b4b73b88877e962689a47d903482c18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89413904"
---
1. 通过选择 F5 键启动调试会话。 “终端”窗口会打印一些消息。
1. operations.json 代码调用直接方法 `GraphTopologyList` 和 `GraphInstanceList`。 如果在学完先前的快速入门后清理了资源，则该过程将返回空列表，然后暂停。 按 Enter 键。
    
    ```
    --------------------------------------------------------------------------
    Executing operation GraphTopologyList
    -----------------------  Request: GraphTopologyList  --------------------------------------------------
    {
      "@apiVersion": "1.0"
    }
    ---------------  Response: GraphTopologyList - Status: 200  ---------------
    {
      "value": []
    }
    --------------------------------------------------------------------------
    Executing operation WaitForInput
    Press Enter to continue
    ```
  
  “终端”窗口将显示下一组直接方法调用：  
  
  * 使用前面的 `topologyUrl` 调用 `GraphTopologySet` 
  * 对 `GraphInstanceSet` 的调用，该调用使用以下正文：
  
  ```
  {
    "@apiVersion": "1.0",
    "name": "Sample-Graph",
    "properties": {
      "topologyName": "EVRToFilesOnMotionDetection",
      "description": "Sample graph description",
      "parameters": [
        {
          "name": "rtspUrl",
          "value": "rtsp://rtspsim:554/media/lots_015.mkv"
        },
        {
          "name": "rtspUserName",
          "value": "testuser"
        },
        {
          "name": "rtspPassword",
          "value": "testpassword"
        }
      ]
    }
  }
  ```
    
  * 对 `GraphInstanceActivate` 的调用，用于启动图形实例和视频流。
  * 对 `GraphInstanceList` 的第二次调用，显示图形实例处于正在运行状态。
1. “终端”窗口中的输出会在出现 `Press Enter to continue` 时暂停。 暂时不要选择 Enter。 向上滚动，查看调用的直接方法的 JSON 响应有效负载。
1. 切换到 Visual Studio Code 中的“输出”窗口。 你将看到 IoT Edge 模块上的实时视频分析正发送到 IoT 中心的消息。 本快速入门中的以下部分将讨论这些消息。
1. 媒体图将继续运行并打印结果。 RTSP 模拟器不断循环源视频。 若要停止媒体图，请返回“终端”窗口，并选择 Enter。 

    接下来的一系列调用会清理资源：

    * 调用 `GraphInstanceDeactivate` 停用图形实例。
    * 调用 `GraphInstanceDelete` 删除该实例。
    * 调用 `GraphTopologyDelete` 删除拓扑。
    * 最后一次调用 `GraphTopologyList` 显示该列表现在为空。
