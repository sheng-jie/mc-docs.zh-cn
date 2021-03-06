---
title: 在 Azure AD 权利管理中添加连接的组织 - Azure Active Directory
description: 了解如何允许组织外部的人员请求访问包，以便你可以进行项目协作。
services: active-directory
documentationCenter: ''
author: barclayn
manager: daveba
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to
ms.subservice: compliance
ms.date: 08/25/2020
ms.author: v-junlch
ms.reviewer: mwahl
ms.collection: M365-identity-device-management
ms.openlocfilehash: b53d1091ef2c2a094aedc2059cc99a30f98100d1
ms.sourcegitcommit: b5ea35dcd86ff81a003ac9a7a2c6f373204d111d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88947374"
---
# <a name="add-a-connected-organization-in-azure-ad-entitlement-management"></a>在 Azure AD 权利管理中添加连接的组织

使用 Azure Active Directory (Azure AD) 权利管理，你可以与组织外部的人员进行协作。 如果你经常与外部 Azure AD 目录或域中的用户协作，则可以将其添加为连接的组织。 本文介绍了如何添加连接的组织，以便允许组织外部的用户请求目录中的资源。

## <a name="what-is-a-connected-organization"></a>什么是连接的组织？

连接的组织是与你有关系的外部 Azure AD 目录或域。

例如，假设你在 Woodgrove Bank 工作，想要与两个外部组织协作。 这两个组织具有不同的配置：

- Graphic Design Institute 使用 Azure AD，其用户的用户主体名称以 graphicdesigninstitute.com 结尾。
- Contoso 尚未使用 Azure AD。 Contoso 用户的用户主体名称以 *contoso.com* 结尾。

在这种情况下，你可以配置两个连接的组织。 分别为 Graphic Design Institute 和 Contoso 创建一个连接的组织。 如果随后将两个连接的组织添加到策略，则每个组织中具有与该策略相匹配的用户主体名称的用户都可以请求访问包。 用户主体名称中的域为 *graphicdesigninstitute.com* 的用户将与 Graphic Design Institute 连接组织匹配，这些用户获允提交请求。 用户主体名称中的域为 *contoso.com* 的用户将与 Contoso 连接组织匹配，这些用户获允请求包。 而且，由于 Graphic Design Institute 使用 Azure AD，因此其主体名称与已添加到其租户的[已验证域](../fundamentals/add-custom-domain.md#verify-your-custom-domain-name)匹配的任何用户（例如 graphicdesigninstitute.example）也可以通过使用相同的策略来请求访问包。

![连接的组织示例](./media/entitlement-management-organization/connected-organization-example.png)

Azure AD 目录或域中的用户进行身份验证的方式取决于身份验证类型。 连接的组织的身份验证类型为：

- Azure AD

有关如何添加连接的组织的演示，请观看以下视频：

>[!VIDEO https://www.microsoft.com/videoplayer/embed/RE4dskS]

## <a name="add-a-connected-organization"></a>添加连接的组织

若要将外部 Azure AD 目录或域添加为连接的组织，请按照此部分中的说明进行操作。

**必备角色**：全局管理员或用户管理员 

1. 在 Azure 门户中，依次选择“Azure Active Directory”、“标识监管”。 

1. 在左窗格中，选择“连接的组织”，然后选择“添加连接的组织”。

    ![“添加连接的组织”按钮](./media/entitlement-management-organization/connected-organization.png)

1. 选择“基本信息”选项卡，然后输入组织的显示名称和描述。

    ![“添加连接的组织”基本信息窗格](./media/entitlement-management-organization/organization-basics.png)

1. 选择“目录 + 域”选项卡，然后选择“添加目录 + 域”。

    此时会打开“选择目录 + 域”窗格。

1. 在搜索框中，输入一个域名来搜索 Azure AD 目录或域。 请务必输入整个域名。

1. 验证组织名称和身份验证类型是否正确无误。 用户如何登录取决于身份验证类型。

    ![“选择目录 + 域”窗格](./media/entitlement-management-organization/organization-select-directories-domains.png)

1. 选择“添加”以添加 Azure AD 目录或域。 目前只能为每个连接的组织添加一个 Azure AD 目录或域。

    > [!NOTE]
    > 该 Azure AD 目录或域中的所有用户都可请求此访问包。 这包括来自与该目录关联的所有子域的 Azure AD 中的用户，除非这些域被 Azure AD 企业对企业 (B2B) 允许或拒绝列表阻止。 有关详细信息，请参阅[允许或阻止向特定组织中的 B2B 用户发送邀请](../b2b/allow-deny-list.md)。

1. 添加 Azure AD 目录或域后，选择“选择”。

    组织将显示在列表中。

    ![“目录 + 域”窗格](./media/entitlement-management-organization/organization-directory-domain.png)

1. 选择“发起人”选项卡，然后为此连接的组织添加可选的发起人。

    发起人是已在你的目录中的内部或外部用户，他们是与此连接的组织建立关系的联系点。 内部发起人是你的目录中的成员用户。 外部发起人是来自连接的组织且以前已受邀并已在你的目录中的来宾用户。 当此连接的组织中的用户请求访问此访问包时，可将发起人用作审批者。 若要了解如何将来宾用户邀请到目录，请参阅[在 Azure 门户中添加 Azure Active Directory B2B 协作用户](../b2b/add-users-administrator.md)。

    选择“添加/删除”时，会打开一个窗格，可在其中选择内部或外部发起人。 此窗格显示你的目录中用户和组的未筛选列表。

    ![“发起人”窗格](./media/entitlement-management-organization/organization-sponsors.png)

1. 选择“查看 + 创建”选项卡，查看你的组织设置，然后选择“创建”。 

    ![“查看 + 创建”窗格](./media/entitlement-management-organization/organization-review-create.png)

## <a name="update-a-connected-organization"></a>更新连接的组织 

如果连接的组织更改为其他域、组织名称发生更改，或者你想要更改发起人，则可以按照本部分中的说明更新连接的组织。

**必备角色**：全局管理员、用户管理员或来宾邀请者  

1. 在 Azure 门户中，依次选择“Azure Active Directory”、“标识监管”。 

1. 在左窗格中，选择“连接的组织”，然后选择连接的组织以将其打开。

1. 在连接的组织的概览窗格中，选择“编辑”以更改组织名称或描述。  

1. 在“目录 + 域”窗格中选择“更新目录 + 域”，改为使用其他目录或域。

1. 在“发起人”窗格中选择“添加内部发起人”或“添加外部发起人”，将某个用户添加为发起人。 若要删除某个发起人，请选择该发起人，然后在右窗格中选择“删除”。


## <a name="delete-a-connected-organization"></a>删除连接的组织

如果你与某个外部 Azure AD 目录或域不再有关系，则可以删除该连接的组织。

**必备角色**：全局管理员、用户管理员或来宾邀请者  

1. 在 Azure 门户中，依次选择“Azure Active Directory”、“标识监管”。 

1. 在左窗格中，选择“连接的组织”，然后选择连接的组织以将其打开。

1. 在连接的组织的概览窗格中，选择“删除”以将其删除。

    目前，只有不存在连接的用户时，才能删除连接的组织。

    ![连接的组织的“删除”按钮](./media/entitlement-management-organization/organization-delete.png)

## <a name="next-steps"></a>后续步骤

- [管控外部用户的访问权限](entitlement-management-external-users.md)
- [管控不在目录中的用户的访问权限](entitlement-management-access-package-request-policy.md#for-users-not-in-your-directory)

