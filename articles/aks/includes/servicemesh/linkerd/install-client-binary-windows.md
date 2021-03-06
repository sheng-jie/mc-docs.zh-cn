---
author: rockboyfor
ms.topic: include
origin.date: 10/09/2019
ms.date: 05/25/2020
ms.author: v-yeche
ms.openlocfilehash: 306c332b81c9db4daf70505eacf733f3ae3579d3
ms.sourcegitcommit: 7e6b94bbaeaddb854beed616aaeba6584b9316d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83735566"
---
## <a name="download-and-install-the-linkerd-linkerd-client-binary"></a>下载并安装 Linkerd linkerd 客户端二进制文件

在 Windows 上基于 PowerShell 的 shell 中，使用 `Invoke-WebRequest` 下载 Linkerd 发行版，如下所示：

```powershell
# Specify the Linkerd version that will be leveraged throughout these instructions
$LINKERD_VERSION="stable-2.6.0"

# Enforce TLS 1.2
[Net.ServicePointManager]::SecurityProtocol = "tls12"
$ProgressPreference = 'SilentlyContinue'; Invoke-WebRequest -URI "https://github.com/linkerd/linkerd2/releases/download/$LINKERD_VERSION/linkerd2-cli-$LINKERD_VERSION-windows.exe" -OutFile "linkerd2-cli-$LINKERD_VERSION-windows.exe"
```

`linkerd` 客户端二进制文件在客户端计算机上运行，用来与 Linkerd 服务网格交互。 在 Windows 上基于 PowerShell 的 shell 中使用以下命令安装 Linkerd `linkerd` 客户端二进制文件。 这些命令可将 `linkerd` 客户端二进制文件复制到某个 Linkerd 文件夹，然后你就可以通过 `PATH` 将其设置为立即可用（在当前 shell 中）和永久可用（跨 shell 重启）。 不需要提升的（管理员）特权即可运行这些命令，不需重启 shell。

```powershell
# Copy linkerd.exe to C:\Linkerd
New-Item -ItemType Directory -Force -Path "C:\Linkerd"
Copy-Item -Path ".\linkerd2-cli-$LINKERD_VERSION-windows.exe" -Destination "C:\Linkerd\linkerd.exe"

# Add C:\Linkerd to PATH. 
# Make the new PATH permanently available for the current User
$USER_PATH = [environment]::GetEnvironmentVariable("PATH", "User") + ";C:\Linkerd\"
[environment]::SetEnvironmentVariable("PATH", $USER_PATH, "User")
# Make the new PATH immediately available in the current shell
$env:PATH += ";C:\Linkerd\"
```

<!-- Update_Description: update meta properties, wording update, update link -->