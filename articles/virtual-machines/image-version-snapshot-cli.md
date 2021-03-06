---
title: CLI - 从共享映像库中的快照或 VHD 创建映像
description: 了解如何使用 Azure CLI 从共享映像库中的快照或 VHD 创建映像。
ms.service: virtual-machines
ms.subservice: imaging
ms.topic: how-to
ms.workload: infrastructure
origin.date: 06/30/2020
author: rockboyfor
ms.date: 08/31/2020
ms.testscope: yes
ms.testdate: 08/31/2020
ms.author: v-yeche
ms.reviewer: akjosh
ms.openlocfilehash: 52f048037ab89da3f2910d8aaec874fc4c5f3d72
ms.sourcegitcommit: daf7317c80f13e459469bbc507786520c8fa6d70
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89046525"
---
<!--Verified successfully from partial-->
# <a name="create-an-image-from-a-vhd-or-snapshot-in-a-shared-image-gallery-using-the-azure-cli"></a>使用 Azure CLI 从共享映像库中的 VHD 或快照创建映像

如果想要将现有快照或 VHD 迁移到共享映像库，可以直接从 VHD 或快照创建共享映像库映像。 测试新映像后，可以删除源 VHD 或快照。 还可以使用 [Azure PowerShell](image-version-snapshot-powershell.md) 从共享映像库中的 VHD 或快照创建映像。

映像库中的映像具有两个组件，我们将在此示例中创建这两个组件：
- “映像定义”包含有关映像及其使用要求的信息。 这包括该映像是 Windows 映像还是 Linux 映像、是专用映像还是通用映像，此外还包括发行说明以及最低和最高内存要求。 它是某种映像类型的定义。 
- 使用共享映像库时，将使用映像版本来创建 VM。 可根据环境的需要创建多个映像版本。 创建 VM 时，将使用该映像版本为 VM 创建新磁盘。 可以多次使用映像版本。

## <a name="before-you-begin"></a>准备阶段

<!--CORRECT ON SCORECARD REQUIREMENT a snapshot-->

若要完成本文中的操作，需要有快照或 VHD。 

如果要包含数据磁盘，则数据磁盘大小不能超过 1 TB。

通过本文进行操作时，请根据需要替换资源名称。

## <a name="find-the-snapshot-or-vhd"></a>查找快照或 VHD 

可以使用 [az snapshot list](https://docs.azure.cn/cli/snapshot?view=azure-cli-latest#az-snapshot-list) 查看资源组中可用的快照列表。 

```azurecli
az snapshot list --query "[].[name, id]" -o tsv
```

还可以使用 VHD 代替快照。 若要获取 VHD，请使用 [az disk list](https://docs.azure.cn/cli/disk?view=azure-cli-latest#az-disk-list)。 

```azurecli
az disk list --query "[].[name, id]" -o tsv
```

获得快照或 VHD 的 ID 后，将其分配给名为 `$source` 的变量，以供以后使用。

可以使用相同的过程获取要包含在映像中的任何数据磁盘。 将其分配给变量，稍后在创建映像版本时会使用这些变量。

## <a name="find-the-gallery"></a>查找库

若要创建映像定义，需要有关映像库的信息。

使用 [az sig list](https://docs.microsoft.com/cli/azure/sig?view=azure-cli-latest#az-sig-list) 列出有关可用映像库的信息。 请记下库的名称及库所在的资源组，以供以后使用。

```azurecli 
az sig list -o table
```

## <a name="create-an-image-definition"></a>创建映像定义

映像定义为映像创建一个逻辑分组。 它们用于管理有关映像的信息。 映像定义名称可能包含大写或小写字母、数字、点、短划线和句点。 

<!--CORRECT ON SCORECARD REQUIREMENT it has / is from-->

创建映像定义时，请确保它包含所有正确信息。 在此示例中，我们假设快照或 VHD 来自正在使用的 VM，并且尚未通用化。 如果 VHD 或快照是从通用 OS 获取的（在 Windows 上运行 Sysprep 或在 Linux 上运行 [waagent](https://github.com/Azure/WALinuxAgent)、`-deprovision` 或 `-deprovision+user` 后），则将 `-OsState` 更改为 `generalized`。 

若要详细了解可为映像定义指定的值，请参阅[映像定义](./linux/shared-image-galleries.md#image-definitions)。

使用 [az sig image-definition create](https://docs.microsoft.com/cli/azure/sig?view=azure-cli-latest#az-sig-image-definition-create) 在库中创建一个映像定义。

在此示例中，映像定义名为 myImageDefinition，适用于[专用化](./linux/shared-image-galleries.md#generalized-and-specialized-images) Linux OS 映像。 若要使用 Windows OS 创建映像的定义，请使用 `--os-type Windows`。 

在此示例中，库名为 myGallery，它位于 myGalleryRG 资源组中，映像定义名称将为 mImageDefinition 。

```azurecli 
resourceGroup=myGalleryRG
gallery=myGallery
imageDef=myImageDefinition
az sig image-definition create \
   --resource-group $resourceGroup \
   --gallery-name $gallery \
   --gallery-image-definition $imageDef \
   --publisher myPublisher \
   --offer myOffer \
   --sku mySKU \
   --os-type Linux \
   --os-state specialized
```

## <a name="create-the-image-version"></a>创建映像版本

使用 [az image gallery create-image-version](https://docs.microsoft.com/cli/azure/sig?view=azure-cli-latest#az-sig-image-version-create) 创建映像版本。 

允许用于映像版本的字符为数字和句点。 数字必须在 32 位整数范围内。 格式：*MajorVersion*.*MinorVersion*.*Patch*。

在此示例中，映像的版本为 *1.0.0*，我们打算使用区域冗余存储在“中国东部”区域创建 1 个副本，在“中国东部 2”区域创建 1 个副本。 选择复制的目标区域时，请记住，还需包含 VHD 或快照的源区域作为复制的目标。

在 `--os-snapshot` 参数中传递快照或 VHD 的 ID。

```azurecli 
az sig image-version create \
   --resource-group $resourceGroup \
   --gallery-name $gallery \
   --gallery-image-definition $imageDef \
   --gallery-image-version 1.0.0 \
   --target-regions "chinaeast=1" "chinaeast2=1=standard_lrs" \
   --replica-count 2 \
   --os-snapshot $source
```

<!--CORRECT ON "chinaeast=1" "chinaeast2=1=standard_lrs"-->

如果要在映像中包含数据磁盘，则需要同时包含设置为 LUN 编号的 `--data-snapshot-luns` 参数和设置为数据磁盘或快照 ID 的 `--data-snapshots` 参数。

> [!NOTE]
> 需等待映像版本彻底生成并复制完毕，然后才能使用同一托管映像来创建另一映像版本。
>

<!--Not Availale on  by adding `--storage-account-type standard_zrs` when you create the image version.-->
<!--Not Available on , or [Zone Redundant Storage](/storage/common/storage-redundancy-zrs) by adding `-StorageAccountType Standard_ZRS`-->

## <a name="next-steps"></a>后续步骤

从[专用映像版本](vm-specialized-image-version-cli.md)创建 VM。

若要了解如何提供购买计划信息，请参阅[创建映像时提供 Azure 市场购买计划信息](marketplace-images.md)。

<!-- Update_Description: new article about image version snapshot cli -->
<!--NEW.date: 08/31/2020-->