---
title: "Azure AD Connect 동기화 서비스 섀도 특성 | Microsoft Docs"
description: "Azure AD Connect 동기화 서비스에서 섀도 특성이 작동하는 방식을 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 0b6a7f22d744480a40a878c979986cdd7667109c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="3d4f2-103">Azure AD Connect 동기화 서비스 섀도 특성</span><span class="sxs-lookup"><span data-stu-id="3d4f2-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="3d4f2-104">대부분의 특성은 온-프레미스 Active Directory에 있을 때와 동일한 방식으로 Azure AD에 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="3d4f2-105">하지만 일부 특성은 조작 방법이 특별하며 Azure AD의 특성 값이 Azure AD Connect가 동기화하는 값과 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="3d4f2-106">섀도 특성 소개</span><span class="sxs-lookup"><span data-stu-id="3d4f2-106">Introducing shadow attributes</span></span>
<span data-ttu-id="3d4f2-107">일부 특성은 Azure AD에서 두 가지로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="3d4f2-108">온-프레미스 값과 계산된 값이 모두 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-108">Both the on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="3d4f2-109">이러한 추가 특성을 섀도 특성이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="3d4f2-110">이 동작을 볼 수 있는 가장 일반적인 특성 두 개는 **userPrincipalName** 및 **proxyAddress**입니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="3d4f2-111">이러한 특성에 확인되지 않은 도메인을 나타내는 값이 있으면 특성 값의 변화가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="3d4f2-112">하지만 Connect의 동기화 엔진이 섀도 특성의 값을 읽기 때문에 이러한 관점에서 Azure AD에 의해 해당 특성이 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="3d4f2-113">Azure Portal 또는 PowerShell을 사용하여 섀도 특성을 볼 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span></span> <span data-ttu-id="3d4f2-114">하지만 개념을 이해하면 온-프레미스와 클라우드의 특성 값이 서로 다른 시나리오를 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span></span>

<span data-ttu-id="3d4f2-115">이 동작을 보다 정확하게 이해하려면 Fabrikam의 예를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-115">To better understand the behavior, look at this example from Fabrikam:</span></span>  
![도메인](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="3d4f2-117">온-프레미스 Active Directory에 UPN 접미사가 여러 개 있지만 확인된 것은 하나뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="3d4f2-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3d4f2-118">userPrincipalName</span></span>
<span data-ttu-id="3d4f2-119">사용자는 유효성이 확인되지 않은 도메인에서 다음과 같은 특성 값을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-119">A user has the following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="3d4f2-120">특성</span><span class="sxs-lookup"><span data-stu-id="3d4f2-120">Attribute</span></span> | <span data-ttu-id="3d4f2-121">값</span><span class="sxs-lookup"><span data-stu-id="3d4f2-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d4f2-122">온-프레미스 userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3d4f2-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="3d4f2-123">Azure AD shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3d4f2-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="3d4f2-124">Azure AD userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="3d4f2-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="3d4f2-125">userPrincipalName 특성은 PowerShell을 사용할 때 표시되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-125">The userPrincipalName attribute is the value you see when using PowerShell.</span></span>

<span data-ttu-id="3d4f2-126">실제 온-프레미스 특성 값이 Azure AD에 저장되므로 사용자가 fabrikam.com domain을 확인할 때 Azure AD는 shadowUserPrincipalName의 값으로 userPrincipalName 특성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span></span> <span data-ttu-id="3d4f2-127">사용자는 이러한 값을 업데이트하기 위해 Azure AD Connect의 변경 내용을 동기화할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="3d4f2-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="3d4f2-128">proxyAddresses</span></span>
<span data-ttu-id="3d4f2-129">proxyAddresses에서도 확인된 도메인만 포함하기 위한 동일한 프로세스가 발생하지만 몇 가지 추가 논리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="3d4f2-130">확인된 도메인 검사가 사서함 사용자에 대해서만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-130">The check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="3d4f2-131">메일이 활성화된 사용자 또는 연락처는 다른 Exchange 조직의 사용자를 나타내며 고객은 proxyAddresses의 값을 이러한 개체에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span></span>

<span data-ttu-id="3d4f2-132">사서함 사용자의 경우 온-프레미스 또는 Exchange Online에서 확인된 도메인의 값만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="3d4f2-133">다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-133">It could look like this:</span></span>

| <span data-ttu-id="3d4f2-134">특성</span><span class="sxs-lookup"><span data-stu-id="3d4f2-134">Attribute</span></span> | <span data-ttu-id="3d4f2-135">값</span><span class="sxs-lookup"><span data-stu-id="3d4f2-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="3d4f2-136">온-프레미스 proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="3d4f2-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="3d4f2-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="3d4f2-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="3d4f2-138">이 경우 해당 도메인이 확인되지 않았기 때문에 **smtp:abbie.spencer@fabrikam.com**이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="3d4f2-139">하지만 Exchange가 **SIP:abbie.spencer@fabrikamonline.com**을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span></span> <span data-ttu-id="3d4f2-140">Fabrikam은 Lync/Skype 온-프레미스를 사용하지 않지만 Azure AD와 Exchange Online은 그에 대한 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="3d4f2-141">proxyAddresses에 대한 이 논리를 **ProxyCalc**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span></span> <span data-ttu-id="3d4f2-142">다음과 같은 경우 사용자에 대한 모든 변경 내용과 함께 ProxyCalc가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-142">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="3d4f2-143">사용자가 Exchange를 사용하도록 허가되지 않은 경우에도 Exchange Online을 포함하는 서비스 계획이 사용자에게 할당되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span></span> <span data-ttu-id="3d4f2-144">사용자에게 Office E3 SKU가 할당되었지만 SharePoint Online만 할당된 경우를 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="3d4f2-145">사서함이 계속 온-프레미스에 있는 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-145">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="3d4f2-146">msExchRecipientTypeDetails 특성에 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-146">The attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="3d4f2-147">사용자가 proxyAddresses 또는 userPrincipalName을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-147">You make a change to proxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="3d4f2-148">ProxyCalc는 사용자에 대한 변경 내용을 처리하는 데 다소 시간이 걸릴 수 있으며 Azure AD Connect 내보내기 프로세스와 동기화되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="3d4f2-149">ProxyCalc 논리에는 이 토픽에서 설명하지 않은 고급 시나리오를 위한 몇 가지 추가 동작이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="3d4f2-150">이 토픽은 동작의 이해를 돕기 위해 제공되었을 뿐, 모든 내부 논리를 설명하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-150">This topic is provided for you to understand the behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="3d4f2-151">격리된 특성 값</span><span class="sxs-lookup"><span data-stu-id="3d4f2-151">Quarantined attribute values</span></span>
<span data-ttu-id="3d4f2-152">중복된 특성 값이 있는 경우에도 섀도 특성이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-152">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="3d4f2-153">자세한 내용은 참조 [중복 특성 복원력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d4f2-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3d4f2-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3d4f2-154">See also</span></span>
* [<span data-ttu-id="3d4f2-155">Azure AD Connect 동기화</span><span class="sxs-lookup"><span data-stu-id="3d4f2-155">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="3d4f2-156">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="3d4f2-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
