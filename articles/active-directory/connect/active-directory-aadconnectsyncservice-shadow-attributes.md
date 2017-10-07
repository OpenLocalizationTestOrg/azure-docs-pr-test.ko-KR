---
title: "aaaAzure AD Connect 동기화 서비스 섀도 특성 | Microsoft Docs"
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
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="565fb-103">Azure AD Connect 동기화 서비스 섀도 특성</span><span class="sxs-lookup"><span data-stu-id="565fb-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="565fb-104">대부분의 특성에 표시 되는 동일한 방식으로 hello Azure AD 온-프레미스 Active Directory에 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-104">Most attributes are represented hello same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="565fb-105">하지만 일부 특성은 몇 가지 특수 한 처리 및 Azure AD에서 특성 값 hello Azure AD Connect 동기화 하는 기능 보다 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-105">But some attributes have some special handling and hello attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="565fb-106">섀도 특성 소개</span><span class="sxs-lookup"><span data-stu-id="565fb-106">Introducing shadow attributes</span></span>
<span data-ttu-id="565fb-107">일부 특성은 Azure AD에서 두 가지로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="565fb-108">Hello 온-프레미스 값과 계산된 된 값이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-108">Both hello on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="565fb-109">이러한 추가 특성을 섀도 특성이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="565fb-110">이 문제를 표시 하는 hello 두 가장 일반적인 특성은 **userPrincipalName** 및 **/ / proxyAddress**합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-110">hello two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="565fb-111">특성 값의 변경 내용이 hello 검증 되지 않은 도메인을 나타내는 이러한 특성에 값이 있을 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-111">hello change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="565fb-112">하지만 hello 동기화 엔진 연결에 값을 읽습니다 hello hello 그림자 특성에 있으므로 해당 관점에서 hello 특성이 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-112">But hello sync engine in Connect reads hello value in hello shadow attribute so from its perspective, hello attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="565fb-113">Hello Azure 포털 또는 PowerShell을 사용 하 여 hello 그림자 특성을 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-113">You cannot see hello shadow attributes using hello Azure portal or with PowerShell.</span></span> <span data-ttu-id="565fb-114">않지만 hello 개념 이해 도움이 됩니다 있습니다 tootroubleshoot 특정 시나리오 hello 특성에 값이 다른 온-프레미스와 클라우드 hello.</span><span class="sxs-lookup"><span data-stu-id="565fb-114">But understanding hello concept helps you tootroubleshoot certain scenarios where hello attribute has different values on-premises and in hello cloud.</span></span>

<span data-ttu-id="565fb-115">toobetter는 hello 동작 이해를 Fabrikam에서이 예제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-115">toobetter understand hello behavior, look at this example from Fabrikam:</span></span>  
![도메인](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="565fb-117">온-프레미스 Active Directory에 UPN 접미사가 여러 개 있지만 확인된 것은 하나뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="565fb-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="565fb-118">userPrincipalName</span></span>
<span data-ttu-id="565fb-119">사용자가 다음 검증 되지 않은 도메인의 특성 값에는 hello:</span><span class="sxs-lookup"><span data-stu-id="565fb-119">A user has hello following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="565fb-120">특성</span><span class="sxs-lookup"><span data-stu-id="565fb-120">Attribute</span></span> | <span data-ttu-id="565fb-121">값</span><span class="sxs-lookup"><span data-stu-id="565fb-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="565fb-122">온-프레미스 userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="565fb-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="565fb-123">Azure AD shadowUserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="565fb-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="565fb-124">Azure AD userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="565fb-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="565fb-125">hello userPrincipalName 특성은 PowerShell을 사용 하는 경우 참조 하는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-125">hello userPrincipalName attribute is hello value you see when using PowerShell.</span></span>

<span data-ttu-id="565fb-126">Hello 실제 온-프레미스 특성 값은 hello fabrikam.com 도메인을 확인 하기는 경우 Azure AD에 저장 되므로 Azure AD는 hello userPrincipalName 특성 hello shadowUserPrincipalName의 hello 값으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-126">Since hello real on-premises attribute value is stored in Azure AD, when you verify hello fabrikam.com domain, Azure AD updates hello userPrincipalName attribute with hello value from hello shadowUserPrincipalName.</span></span> <span data-ttu-id="565fb-127">없는 toosynchronize 이러한 값 toobe 업데이트에 대 한 Azure AD Connect의 변경 내용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-127">You do not have toosynchronize any changes from Azure AD Connect for these values toobe updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="565fb-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="565fb-128">proxyAddresses</span></span>
<span data-ttu-id="565fb-129">hello 일부 추가 논리가 하면서도 proxyAddresses에 대 한 동일한 프로세스만 확인 된 도메인을 포함 하는 데에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-129">hello same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="565fb-130">사서함 사용자에 대 한 확인 된 도메인에 대 한 hello 확인만 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-130">hello check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="565fb-131">메일 사용이 가능한 사용자 또는 연락처 Exchange 조직의 다른 사용자 나타내고 proxyAddresses toothese 개체의 모든 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses toothese objects.</span></span>

<span data-ttu-id="565fb-132">사서함 사용자의 경우 온-프레미스 또는 Exchange Online에서 확인된 도메인의 값만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="565fb-133">다음과 같이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-133">It could look like this:</span></span>

| <span data-ttu-id="565fb-134">특성</span><span class="sxs-lookup"><span data-stu-id="565fb-134">Attribute</span></span> | <span data-ttu-id="565fb-135">값</span><span class="sxs-lookup"><span data-stu-id="565fb-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="565fb-136">온-프레미스 proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="565fb-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="565fb-137">Exchange Online proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="565fb-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="565fb-138">이 경우 해당 도메인이 확인되지 않았기 때문에 **smtp:abbie.spencer@fabrikam.com**이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="565fb-139">하지만 Exchange가 **SIP:abbie.spencer@fabrikamonline.com**을 추가했습니다. Fabrikam은 Lync/Skype 온-프레미스를 사용하지 않지만 Azure AD와 Exchange Online은 그에 대한 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="565fb-140">ProxyAddresses에 대 한이 논리는 참조 된 tooas **ProxyCalc**합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-140">This logic for proxyAddresses is referred tooas **ProxyCalc**.</span></span> <span data-ttu-id="565fb-141">다음과 같은 경우 사용자에 대한 모든 변경 내용과 함께 ProxyCalc가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-141">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="565fb-142">hello 사용자 hello 사용자가 Exchange에 사용 허가 되지 않더라도 Exchange Online을 포함 하는 서비스 계획을 할당 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-142">hello user has been assigned a service plan that includes Exchange Online even if hello user was not licensed for Exchange.</span></span> <span data-ttu-id="565fb-143">예를 들어 hello 사용자가 할당 하는 경우 Office E3 SKU hello 있지만 SharePoint Online 할당만 합니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-143">For example, if hello user is assigned hello Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="565fb-144">사서함이 계속 온-프레미스에 있는 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-144">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="565fb-145">hello 특성 msExchRecipientTypeDetails 값을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-145">hello attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="565fb-146">변경 tooproxyAddresses 또는 userPrincipalName 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-146">You make a change tooproxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="565fb-147">ProxyCalc는 사용자에 몇 시간 tooprocess 변경 걸릴 수 있습니다 하 고 hello Azure AD Connect 내보내기 프로세스 동기화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-147">ProxyCalc might take some time tooprocess a change on a user and is not synchronous with hello Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="565fb-148">hello ProxyCalc 논리는이 항목에서 설명 하지는 고급 시나리오에 대 한 몇 가지 추가적인 동작에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-148">hello ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="565fb-149">이 항목에는 toounderstand hello 동작을 위해 모든 내부 논리를 설명 하지 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-149">This topic is provided for you toounderstand hello behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="565fb-150">격리된 특성 값</span><span class="sxs-lookup"><span data-stu-id="565fb-150">Quarantined attribute values</span></span>
<span data-ttu-id="565fb-151">중복된 특성 값이 있는 경우에도 섀도 특성이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="565fb-151">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="565fb-152">자세한 내용은 참조 [중복 특성 복원력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="565fb-152">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="565fb-153">참고 항목</span><span class="sxs-lookup"><span data-stu-id="565fb-153">See also</span></span>
* [<span data-ttu-id="565fb-154">Azure AD Connect 동기화</span><span class="sxs-lookup"><span data-stu-id="565fb-154">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="565fb-155">[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="565fb-155">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
