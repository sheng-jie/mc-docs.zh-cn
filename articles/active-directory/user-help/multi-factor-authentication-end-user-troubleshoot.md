---
title: 帐户双因素身份验证的常见问题 - Azure AD
description: 双因素身份验证以及工作或学校帐户的一些更常见问题的解决方案。
services: active-directory
author: curtand
manager: daveba
ms.assetid: 8f3aef42-7f66-4656-a7cd-d25a971cb9eb
ms.workload: identity
ms.service: active-directory
ms.subservice: user-help
ms.topic: end-user-help
ms.date: 08/26/2020
ms.author: v-junlch
ms.reviewer: kexia
ms.openlocfilehash: fdc99026b4ed78f537a49f4b7a7a9017f66fca9d
ms.sourcegitcommit: b5ea35dcd86ff81a003ac9a7a2c6f373204d111d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88947095"
---
# <a name="common-problems-with-two-factor-verification-and-your-work-or-school-account"></a>双因素验证以及工作或学校帐户的常见问题

Azure Active Directory (Azure AD) 组织可以启用双重验证 (2FV)。 有一些常见的 2FV 问题，似乎发生得比我们任何一个人预期得都要频繁。 我们编写了这篇文章，以介绍最常见问题的修复方法。

打开 2FV 时，帐户登录需要以下数据的组合：

- 您的用户名
- 你的密码
- 移动设备或手机

2FV 比密码更安全，因为 2FV 需要你知道的密码加上你拥有的设备 。 黑客没有你的实体电话。

![身份验证方法的概念图](../authentication/media/concept-mfa-howitworks/methods.png)

>[!Important]
>如果你是管理员，可以在 [Azure AD 文档](/active-directory)中详细了解如何创建和管理 Azure AD 环境。
>
>另外，本文内容也只适用于解决工作或学校帐户出现的问题，即由组织提供给你的帐户（例如 alain@contoso.com）。 如果在结合使用双因素验证和个人 Microsoft 帐户（即你为自己创建的帐户，例如 danielle@outlook.com）时遇到问题，请参阅[为你的 Microsoft 帐户启用或禁用双因素验证](https://support.microsoft.com/help/4028586/microsoft-account-turning-two-step-verification-on-or-off)。

## <a name="i-dont-have-my-mobile-device-with-me"></a>我没有随身携带移动设备

这种情况确实会发生。 你把移动设备落在家里了，所以现在无法使用电话来验证你的身份。 你以前可能添加了登录到帐户的备用方法，例如通过你的办公电话登录。 如果是这样，你现在可以使用这种备用方法。 如果你从未添加备用验证方法，可以联系组织的支持人员以寻求帮助。

### <a name="to-sign-in-to-your-work-or-school-account-using-another-verification-method"></a>使用另一种验证方法登录你的工作或学校帐户的具体步骤

1. 正常登录帐户，但选择“双因素验证”页上的“使用另一种方式登录”链接。

    ![更改登录验证方法](./media/multi-factor-authentication-end-user-troubleshoot/two-factor-auth-signin-another-way.png)

    如果没有看到“用其他方法登录”链接，这表示尚未设置其他验证方法。 必须联系管理员，获取登录帐户的帮助。

2. 选择备用验证方法，然后继续进行双因素验证流程。

## <a name="i-lost-my-mobile-device-or-it-was-stolen"></a>我的移动设备丢失或被盗

如果移动设备丢失或被盗，可以执行以下任一操作：

- 使用其他方法登录。
- 请求组织的支持人员清除你的设置。

如果你的电话丢失或被盗，强烈建议你告知组织的支持人员。 支持人员可以对你的帐户进行相应更新。 在你的设置清除后，系统会在你下次登录时提示[注册双因素验证](multi-factor-authentication-end-user-first-time.md)。

## <a name="im-not-receiving-the-verification-code-sent-to-my-mobile-device"></a>我没有收到发送到我的移动设备的验证码

收不到验证码是一个常见问题。 此问题通常与移动设备及其设置相关。 下面是可以尝试的一些操作。

尝试此操作 | 指导信息
--------- | ------------
重启移动设备 | 有时，设备只是需要刷新一下。 重启设备时，将结束所有后台进程和服务。 重启还会关闭设备的核心组件。 重启设备时，将刷新任何服务或组件。
验证安全信息是否正确无误 | 确保你的安全验证方法信息是准确的，特别是你的电话号码。 如果你输入了错误的电话号码，那么所有警报都会发送到这一错误号码。 幸运的是，这名用户无法使用警报执行任何操作，但这也不能帮助你登录帐户。 若要确保你的信息正确无误，请参阅[管理双因素验证方法设置](multi-factor-authentication-end-user-manage-settings.md)一文中的说明。
验证是否已启用通知 | 请确保移动设备启用了通知。 确保允许以下通知模式： <br/><br/> &bull; 电话呼叫 <br/> &bull; 身份验证应用 <br/> &bull; 短信应用 <br/><br/> 请确保这些模式创建在你的设备上可见的警报。
确保设备有信号且已连接 Internet | 确保你的移动设备能够接听电话和接收短信。 让朋友给你打电话和发短信，以确保你都能收到。 如果接不到电话或收不到短信，请先进行检查，确保你的移动设备已开机。 如果设备已开机，但仍未收到呼叫或电话，则可能是网络有问题。 需要与你的提供商联系。 
禁用“请勿打扰” | 确保没有在移动设备上启用“请勿打扰”功能。 在此功能启用后，就会禁止在移动设备上发出通知来提醒你。 若要了解如何禁用此功能，请参阅移动设备的手册。
取消阻止电话号码 | 在美国，Microsoft 语音呼叫的号码如下：+1 (866) 539 4191、+1 (855) 330 8653 和 +1 (877) 668 6536。
检查电池相关设置 | 此操作表面上看起来有点奇怪。 但如果你已设置电池优化来阻止不太常用的应用在后台保持活跃，你的通知系统很可能已经受到了影响。 若要尝试修复此问题，请禁用针对身份验证应用和短信应用的电池优化。 然后再次尝试登录你的帐户。
禁用第三方安全应用 | 某些手机安全应用会阻止来自未知号码的骚扰短信和电话。 此类应用可能会阻止你的手机接收验证码。 请尝试在电话上禁用任何第三方安全应用，然后请求发送另一个验证码。

## <a name="im-not-being-prompted-for-my-second-verification-information"></a>我没有看到提供第二个验证信息的提示

使用你的用户名和密码登录到工作或学校帐户。 接下来，系统会提示你提供其他安全验证信息。 如果未出现提示，则可能尚未设置设备。 必须将移动设备设置为使用特定的附加安全验证方法。

若要确保移动设备已打开且可用，请参阅[管理双重验证方法设置](multi-factor-authentication-end-user-manage-settings.md)一文。 如果你知道自己还没有设置设备或帐户，可以立即按照[为我的帐户设置双重验证](multi-factor-authentication-end-user-first-time.md)一文中的步骤操作。

## <a name="i-have-a-new-phone-number-and-i-want-to-add-it"></a>我有新的电话号码，我想添加它

如果你有了新的电话号码，则需要更新安全验证方法的详细信息。 这让我们可以将验证提示发送到正确的位置。 若要更新验证方法，请按照[更改双重验证方法设置](multi-factor-authentication-end-user-manage-settings.md#add-or-change-your-phone-number)一文中的“添加或更改你的电话号码”部分所述步骤操作。

## <a name="i-have-a-new-mobile-device-and-i-want-to-add-it"></a>我有新的移动设备，我想添加它

如果你有了新的移动设备，需要对其进行设置以允许使用双重验证。 这是一个多步骤的解决方案：

1. 按照[为我的帐户设置双重验证](multi-factor-authentication-end-user-first-time.md)一文中的步骤操作，将设备设置为使用你的帐户。

1. 在“附加安全验证”页中，更新你的帐户和设备信息。 通过删除旧设备并添加新设备来执行更新。 有关详细信息，请参阅[更改双因素验证方法设置](multi-factor-authentication-end-user-manage-settings.md)一文。

## <a name="i-cant-turn-off-two-factor-verification"></a>我无法禁用双重验证

如果你是将双因素验证用于工作或学校帐户（例如 alain@contoso.com），那么这很可能意味着你的组织已决定必须使用这一附加的安全功能。 由于你的组织已决定你必须使用此功能，因此无法单独将其关闭。 不过，如果你是将双因素验证用于个人帐户（如 alain@outlook.com），则可以启用和禁用此功能。 有关如何控制个人帐户的双因素验证的说明，请参阅[为你的 Microsoft 帐户启用或禁用双因素验证](https://support.microsoft.com/help/4028586/microsoft-account-turning-two-step-verification-on-or-off)。

如果无法禁用双因素验证，也可能是因为在组织级别应用了安全默认值。 若要详细了解安全默认值，请参阅[什么是安全默认值？](../fundamentals/concept-fundamentals-security-defaults.md)

## <a name="i-didnt-find-an-answer-to-my-problem"></a>我找不到问题的解答

如果已尝试这些步骤，但仍遇到问题，请联系你组织的支持人员来获取帮助。

## <a name="related-articles"></a>相关文章

- [管理双重验证方法设置](multi-factor-authentication-end-user-manage-settings.md)

- [为我的帐户设置双重验证](multi-factor-authentication-end-user-first-time.md)


