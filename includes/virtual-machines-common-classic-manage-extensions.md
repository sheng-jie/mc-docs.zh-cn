---
author: rockboyfor
ms.service: virtual-machines
ms.topic: include
origin.date: 10/26/2018
ms.date: 11/26/2018
ms.author: v-yeche
ms.openlocfilehash: cb02503037e21fdab8e7177e8a69bb6d9f85c9a3
ms.sourcegitcommit: 59db70ef3ed61538666fd1071dcf8d03864f10a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2018
ms.locfileid: "52676131"
---
## <a name="using-vm-extensions"></a>使用 VM 扩展
Azure VM 扩展实现了可帮助其他程序在 Azure VM 上正常工作的行为或功能（例如，**WebDeployForVSDevTest** 扩展允许 Visual Studio 在 Azure VM 上对解决方案进行 Web 部署），或为用户提供与 VM 交互的功能以支持其他某种行为（例如，用户可以使用 VM 访问扩展从 PowerShell、Azure CLI 和 REST 客户端重置或修改 Azure VM 上的远程访问值）。

> [!IMPORTANT]
> 有关这些扩展按它们支持的功能列出的完整列表，请参阅 [Azure VM 扩展和功能](../articles/virtual-machines/windows/extensions-features.md?toc=%2fvirtual-machines%2fwindows%2ftoc.json)。 由于每个 VM 扩展都支持特定功能，因此使用扩展具体可以和不可以执行哪些操作取决于该扩展。 因此，在修改 VM 之前，请确保已阅读要使用的 VM 扩展的相关文档。 不支持删除某些 VM 扩展；其他 VM 扩展具有可设置以从根本上更改 VM 行为的属性。
> 
> 

最常见的任务是：

1. 查找可用扩展
2. 更新已加载的扩展
3. 添加扩展
4. 删除扩展

## <a name="find-available-extensions"></a>查找可用扩展
可以使用以下项查找扩展和扩展信息：

* PowerShell
* Azure 跨平台命令行接口 (Azure CLI)
* 服务管理 REST API

### <a name="azure-powershell"></a>Azure PowerShell
某些扩展使用特定于它们的 PowerShell cmdlet，因此从 PowerShell 进行配置可能更容易；但以下 cmdlet 适用于所有 VM 扩展。

可以使用以下 cmdlet 获取有关可用扩展的信息：

* 对于 Web 角色或辅助角色的实例，可以使用 [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet。
* 对于虚拟机的实例，可以使用 [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet。

   例如，以下代码示例显示如何使用 PowerShell 列出 **IaaSDiagnostics** 扩展的信息。

        PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics

        Publisher                   : Microsoft.Azure.Diagnostics
        ExtensionName               : IaaSDiagnostics
        Version                     : 1.2
        Label                       : Microsoft Monitoring Agent Diagnostics
        Description                 : Microsoft Monitoring Agent Extension
        PublicConfigurationSchema   :
        PrivateConfigurationSchema  :
        IsInternalExtension         : False
        SampleConfig                :
        ReplicationCompleted        : True
        Eula                        :
        PrivacyUri                  :
        HomepageUri                 :
        IsJsonExtension             : True
        DisallowMajorVersionUpgrade : False
        SupportedOS                 :
        PublishedDate               :
        CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a>Azure 命令行界面 (Azure CLI)
某些扩展使用特定于它们的 Azure CLI 命令（Docker VM 扩展就是一个例子），这可能会使其配置更容易；但以下命令适用于所有 VM 扩展。

可以使用 **azure vm extension list** 命令获取有关可用扩展的信息，并使用 **--json** 选项显示有关一个或多个扩展的所有可用信息。 如果不使用扩展名称，该命令将返回所有可用扩展的 JSON 描述。

例如，以下代码示例显示如何使用 Azure CLI **azure vm extension list** 命令列出 **IaaSDiagnostics** 扩展的信息，并使用 **--json** 选项返回完整信息。

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]

### <a name="service-management-rest-apis"></a>服务管理 REST API
可以使用以下 REST API 获取有关可用扩展的信息：

* 对于 Web 角色或辅助角色的实例，可以使用[列出可用扩展](https://msdn.microsoft.com/library/dn169559.aspx)操作。 若要列出可用扩展的版本，可以使用[列出扩展版本](https://msdn.microsoft.com/library/dn495437.aspx)。
* 对于虚拟机的实例，可以使用[列出资源扩展](https://msdn.microsoft.com/library/dn495441.aspx)操作。 若要列出可用扩展的版本，可以使用[列出资源扩展版本](https://msdn.microsoft.com/library/dn495440.aspx)。

## <a name="add-update-or-disable-extensions"></a>添加、更新或禁用扩展
扩展可以在创建实例时添加，也可以将它们添加到正在运行的实例。 可以更新、禁用或删除扩展。 可以通过使用 Azure PowerShell cmdlet 或使用服务管理 REST API 操作来执行这些操作。 需要使用参数才能安装和设置某些扩展。 扩展支持公共参数和私有参数。

### <a name="azure-powershell"></a>Azure PowerShell
使用 Azure PowerShell cmdlet 是添加和更新扩展的最简单方法。 使用扩展 cmdlet 时，将为用户完成大部分扩展配置。 有时，可能需要以编程方式添加扩展。 当需要这样做时，必须提供扩展的配置。

可以使用以下 cmdlet 来了解扩展是否需要配置公共参数和私有参数：

* 对于 Web 角色或辅助角色的实例，可以使用 **Get-AzureServiceAvailableExtension** cmdlet。
* 对于虚拟机的实例，可以使用 **Get-AzureVMAvailableExtension** cmdlet。

### <a name="service-management-rest-apis"></a>服务管理 REST API
使用 REST API 检索可用扩展的列表时，会收到有关如何配置扩展的信息。 返回的信息可能显示由公共架构和私有架构表示的参数信息。 公共参数值在实例查询中返回。 不返回私有参数值。

可以使用以下 REST API 来了解扩展是否需要配置公共参数和私有参数：

* 对于 Web 角色或辅助角色的实例，**PublicConfigurationSchema** 和 **PrivateConfigurationSchema** 元素包含[列出可用扩展](https://msdn.microsoft.com/library/dn169559.aspx)操作的响应中的信息。
* 对于虚拟机的实例，**PublicConfigurationSchema** 和 **PrivateConfigurationSchema** 元素包含[列出资源扩展](https://msdn.microsoft.com/library/dn495441.aspx)操作的响应中的信息。

> [!NOTE]
> 扩展也可以使用通过 JSON 定义的配置。 使用这些类型的扩展时，仅使用 **SampleConfig** 元素。
> 
>

<!-- Update_Description: update meta properties -->