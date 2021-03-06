---
title: 选择 Azure 数据传输解决方案 | Microsoft Docs
description: 了解如何基于环境中的数据大小和可用网络带宽选择 Azure 数据传输解决方案。
services: storage
author: WenJason
ms.service: storage
ms.subservice: blobs
ms.topic: conceptual
origin.date: 06/03/2019
ms.date: 08/24/2020
ms.author: v-jay
ms.openlocfilehash: 6a2e962d97f8d31a57c42d1311c0b1834fabb434
ms.sourcegitcommit: ecd6bf9cfec695c4e8d47befade8c462b1917cf0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2020
ms.locfileid: "88753422"
---
# <a name="choose-an-azure-solution-for-data-transfer"></a>选择 Azure 数据传输解决方案

本文概述一些常用 Azure 数据传输解决方案。 本文还根据环境中的网络带宽以及打算传输的数据大小提供了建议选项。

## <a name="types-of-data-movement"></a>数据移动的类型

数据传输可以脱机进行或通过网络连接进行。 根据以下因素选择解决方案：

- **数据大小** - 打算进行传输的数据大小，
- **传输频率** - 一次性或定期数据引入，以及
- **网络** - 环境中可用于数据传输的带宽。

数据移动可以是以下类型：

- **使用可发运设备脱机传输** - 在要进行脱机一次性批量数据传输时使用可发运设备。 Azure 会向你寄送磁盘或安全的专用设备。 或者，你可以购买并发运自己的磁盘。 将数据复制到设备，然后将它发运给在其中上传数据的 Azure。  可用于这种情况的选项包括 Data Box Disk 和导入/导出（使用你自己的磁盘）。

- **网络传输** - 通过网络连接将数据传输到 Azure。 这可以通过多种方法来实现。

    - **图形界面** - 如果偶尔仅传输几个文件，并且无需自动执行数据传输，则可以选择图形界面工具（如 Azure 存储资源管理器或 Azure 门户中基于 Web 的浏览工具）。
    - **脚本化或编程传输** - 可以使用我们提供的优化软件工具，或直接调用我们的 REST API/SDK。 可用的可编写脚本工具有 AzCopy、Azure PowerShell 和 Azure CLI。 对于编程接口，请使用用于 .NET、Java、Python、Node/JS、C++、Go、PHP 或 Ruby 的 SDK 之一。
    - **托管数据管道** - 可以设置云管道，以在多个 Azure 服务、本地或这两者的组合之间定期传输文件。 使用 Azure 数据工厂可设置和管理数据管道，以及移动和转换数据以进行分析。

## <a name="selecting-a-data-transfer-solution"></a>选择数据传输解决方案

回答以下问题以帮助选择数据传输解决方案：

- 可用网络带宽是否有限或不存在，并且你要传输大型数据集？
  
    如果是，请参阅：[方案 1：在网络带宽不存在或较低的情况下传输大型数据集](storage-solution-large-dataset-low-network.md)。
- 是否要通过网络传输大型数据集并且具有中等到较高网络带宽？

    如果是，请参阅：[方案 2：在网络带宽中等或较高的情况下传输大型数据集](storage-solution-large-dataset-moderate-high-network.md)。
- 是否偶尔要通过网络仅传输几个文件？

    如果是，请参阅[方案 3：在网络带宽有限或中等的情况下传输小型数据集](storage-solution-small-dataset-low-moderate-network.md)。
- 是否在寻找采用固定时间间隔的时间点数据传输？

    如果是，请使用[方案 4：定期数据传输](storage-solution-periodic-data-transfer.md)中概述的脚本化/编程选项。
- 是否在寻找持续数据传输？

    如果是，请使用[方案 4：定期数据传输](storage-solution-periodic-data-transfer.md)中概述的脚本化/编程选项。

## <a name="data-transfer-feature-in-azure-portal"></a>Azure 门户中的数据传输功能

也可转到 Azure 门户中的 Azure 存储帐户，然后选择“数据传输”功能。 请在环境中提供网络带宽、要传输的数据大小以及数据传输的频率。 将会看到与提供的信息相对应的最佳数据传输解决方案。 

## <a name="next-steps"></a>后续步骤

- [获取 Azure 存储资源管理器简介](https://azure.microsoft.com/resources/videos/introduction-to-microsoft-azure-storage-explorer/)。
- [阅读 AzCopy 概述](/storage/common/storage-use-azcopy-v10)。
- [快速入门：使用 PowerShell 上传、下载和列出 blob](../blobs/storage-quickstart-blobs-powershell.md)
- [快速入门：使用 Azure CLI 创建、下载和列出 blob](../blobs/storage-quickstart-blobs-cli.md)
- 学习内容：

    - [Azure Data Box Disk](/databox/)。
- [了解什么是 Azure 数据工厂](/data-factory/copy-activity-overview)。
- 使用 REST API 传输数据

    - [在 .NET 中](/dotnet/api/overview/storage)
    - [在 Java 中](https://docs.microsoft.com/java/api/overview/azure/storage)
