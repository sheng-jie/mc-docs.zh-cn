---
title: 从 VM 创建映像（预览版）
description: 了解如何使用 Azure PowerShell，在共享映像库中从 Azure 中的现有 VM 创建映像。
author: rockboyfor
ms.topic: how-to
ms.service: virtual-machines
ms.subservice: imaging
ms.workload: infrastructure
origin.date: 05/04/2020
ms.date: 08/31/2020
ms.testscope: yes
ms.testdate: 08/31/2020
ms.author: v-yeche
ms.reviewer: akjosh
ms.openlocfilehash: 1fecddd4260668e6d83223d7f6439c39d1fcfc91
ms.sourcegitcommit: 63a4bc7c501fb6dd54a31d39c87c0e8692ac2eb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89052379"
---
<!--Verified Successfully-->
# <a name="preview-create-an-image-from-a-vm"></a>预览版：从 VM 创建映像

如果要使用现有 VM 生成多个相同的 VM，你可以使用该 VM 在共享映像库中通过 Azure PowerShell 创建映像。 还可以使用 [Azure CLI](image-version-vm-cli.md) 从 VM 创建映像。

你可以使用 Azure PowerShell 从[专用化和通用化](./windows/shared-image-galleries.md#generalized-and-specialized-images) VM 捕获映像。 

映像库中的映像具有两个组件，我们将在此示例中创建这两个组件：
- “映像定义”包含有关映像及其使用要求的信息。 这包括该映像是 Windows 映像还是 Linux 映像、是专用映像还是通用映像，此外还包括发行说明以及最低和最高内存要求。 它是某种映像类型的定义。 
- 使用共享映像库时，将使用映像版本来创建 VM。 可根据环境的需要创建多个映像版本。 创建 VM 时，将使用该映像版本为 VM 创建新磁盘。 可以多次使用映像版本。

## <a name="before-you-begin"></a>准备阶段

若要完成本文中的操作，必须拥有现有的共享映像库，以及 Azure 中现有的 VM 作为源。 

如果 VM 附加了数据磁盘，则数据磁盘大小不能超过 1 TB。

通过本文进行操作时，请根据需要替换资源名称。

## <a name="get-the-gallery"></a>获取库

可以按名称列出所有库和映像定义。 结果的格式是 `gallery\image definition\image version`。

```powershell
Get-AzResource -ResourceType Microsoft.Compute/galleries | Format-Table
```

找到正确的库和映像定义后，为它们创建变量以供稍后使用。 此示例会获取 myResourceGroup 资源组中名为 myGallery 的库 。

```powershell
$gallery = Get-AzGallery `
   -Name myGallery `
   -ResourceGroupName myResourceGroup
```

## <a name="get-the-vm"></a>获取 VM

可以使用 [Get-AzVM](https://docs.microsoft.com/powershell/module/az.compute/get-azvm) 查看资源组中可用的 VM 列表。 了解 VM 的名称及其所在资源组后，可以再次使用 `Get-AzVM` 来获取 VM 对象并将其存储在变量中，供稍后使用。 此示例从“myResourceGroup”资源组获取名为 sourceVM 的 VM，并将其分配给变量 $sourceVm 。 

```powershell
$sourceVm = Get-AzVM `
   -Name sourceVM `
   -ResourceGroupName myResourceGroup
```

在使用 [Stop-AzVM](https://docs.microsoft.com/powershell/module/az.compute/stop-azvm) 创建映像之前，建议停止/解除分配 VM。

```powershell
Stop-AzVM `
   -ResourceGroupName $sourceVm.ResourceGroupName `
   -Name $sourceVm.Name `
   -Force
```

## <a name="create-an-image-definition"></a>创建映像定义 

映像定义为映像创建一个逻辑分组。 它们用于管理有关映像的信息。 映像定义名称可能包含大写或小写字母、数字、点、短划线和句点。 

制作映像定义时，请确保它具有所有正确信息。 如果已通用化 VM（使用适用于 Windows 的 Sysprep，或适用于 Linux 的 waagent -deprovision），则应使用 `-OsState generalized` 创建映像定义。 如果未通用化 VM，请使用 `-OsState specialized` 创建映像定义。

若要详细了解可以为映像定义指定的值，请参阅[映像定义](./windows/shared-image-galleries.md#image-definitions)。

使用 [New-AzGalleryImageDefinition](https://docs.microsoft.com/powershell/module/az.compute/new-azgalleryimageversion) 创建映像定义。 

在此示例中，映像定义名为 myImageDefinition，适用于运行 Windows 的专用化 VM。 若要为使用 Linux 的映像创建定义，请使用 `-OsType Linux`。 

```powershell
$imageDefinition = New-AzGalleryImageDefinition `
   -GalleryName $gallery.Name `
   -ResourceGroupName $gallery.ResourceGroupName `
   -Location $gallery.Location `
   -Name 'myImageDefinition' `
   -OsState specialized `
   -OsType Windows `
   -Publisher 'myPublisher' `
   -Offer 'myOffer' `
   -Sku 'mySKU'
```

## <a name="create-an-image-version"></a>创建映像版本

使用 [New-AzGalleryImageVersion](https://docs.microsoft.com/powershell/module/az.compute/new-azgalleryimageversion) 创建映像版本。 

允许用于映像版本的字符为数字和句点。 数字必须在 32 位整数范围内。 格式：*MajorVersion*.*MinorVersion*.*Patch*。

在此示例中，映像版本为 1.0.0，该版本被复制到中国北部和中国东部数据中心  。 选择复制的目标区域时，请记住，你还需包括源区域作为复制的目标。

若要从 VM 创建映像版本，请对 `-Source` 使用 `$vm.Id.ToString()`。

<!--CORRECT ON Source Central US MAP TO China North, and East US MAP TO China East-->

```powershell
   $region1 = @{Name='China North';ReplicaCount=1}
   $region2 = @{Name='China East';ReplicaCount=2}
   $targetRegions = @($region1,$region2)

$job = $imageVersion = New-AzGalleryImageVersion `
   -GalleryImageDefinitionName $imageDefinition.Name`
   -GalleryImageVersionName '1.0.0' `
   -GalleryName $gallery.Name `
   -ResourceGroupName $gallery.ResourceGroupName `
   -Location $gallery.Location `
   -TargetRegion $targetRegions  `
   -Source $sourceVm.Id.ToString() `
   -PublishingProfileEndOfLifeDate '2020-12-01' `
   -asJob 
```

可能需要一段时间才能将该映像复制到所有目标区域，因此我们创建了作业，以便可以跟踪进度。 要查看作业的进度，请键入 `$job.State`。

```powershell
$job.State
```

> [!NOTE]
> 需等待映像版本彻底生成并复制完毕，然后才能使用同一托管映像来创建另一映像版本。
>
> 创建映像版本时，还可以通过添加 `-StorageAccountType Premium_LRS` 在高级存储中存储映像，或者通过添加 `-StorageAccountType Standard_LRS` 在本地冗余存储中存储映像。
>

<!--CORRECT ON Locally Redundant Storage by adding `-StorageAccountType Standard_LRS`-->

## <a name="next-steps"></a>后续步骤

验证新映像版本正常工作后，即可创建 VM。 从[专用化映像版本](vm-specialized-image-version-powershell.md)或[通用化映像版本](vm-generalized-image-version-powershell.md)创建 VM。

<!--Not Available on For information about how to supply purchase plan information, see [Supply Azure Marketplace purchase plan information when creating images](marketplace-images.md).-->

<!-- Update_Description: update meta properties, wording update, update link -->