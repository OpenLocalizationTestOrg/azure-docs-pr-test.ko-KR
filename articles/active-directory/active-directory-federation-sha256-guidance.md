---
title: "Office 365 신뢰 당사자 트러스트에 대한 서명 해시 알고리즘 변경 | Microsoft Docs"
description: "이 페이지에서는 Office 365와의 페더레이션 트러스트에 대한 SHA 알고리즘을 변경하는 방법에 대한 지침을 제공합니다."
keywords: "SHA1,SHA256,O365,페더레이션,aadconnect,adfs,ad fs,sha 변경,페더레이션 트러스트,신뢰 당사자 트러스트"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="0b575-104">Office 365 신뢰 당사자 트러스트에 대한 서명 해시 알고리즘 변경</span><span class="sxs-lookup"><span data-stu-id="0b575-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="0b575-105">개요</span><span class="sxs-lookup"><span data-stu-id="0b575-105">Overview</span></span>
<span data-ttu-id="0b575-106">AD FS(Active Directory Federation Services)는 변조될 수 없음을 확인하도록 해당 토큰을 Microsoft Azure Active Directory에 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="0b575-107">이 서명은 SHA1 또는 SHA256을 기반으로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="0b575-108">이제 Azure Active Directory에서는 SHA256 알고리즘으로 서명된 토큰을 지원하며, 최고 수준의 보안을 위해 토큰 서명 알고리즘을 SHA256으로 설정하도록 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="0b575-109">이 문서에서는 토큰 서명 알고리즘을 보다 안전한 SHA256 수준으로 설정하는 데 필요한 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="0b575-110">Microsoft에서는 SHA1보다 더 안전하지만 SHA1이 여전히 지원되는 옵션이므로 토큰을 서명하는 알고리즘으로 SHA256을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="0b575-111">토큰 서명 알고리즘 변경</span><span class="sxs-lookup"><span data-stu-id="0b575-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="0b575-112">아래의 두 절차 중 하나를 사용하여 서명 알고리즘을 설정한 후 AD FS는 SHA256으로 Office 365 신뢰 당사자 트러스트에 대한 토큰을 서명합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="0b575-113">추가 구성을 변경할 필요가 없으며 이 변경은 Office 365 또는 다른 Azure AD 응용 프로그램에 액세스하는 기능에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="0b575-114">AD FS 관리 콘솔</span><span class="sxs-lookup"><span data-stu-id="0b575-114">AD FS management console</span></span>
1. <span data-ttu-id="0b575-115">기본 AD FS 서버에서 AD FS 관리 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="0b575-116">AD FS 노드를 확장하고 **신뢰 당사자 트러스트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="0b575-117">Office 365/Azure 신뢰 당사자 트러스트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="0b575-118">**고급** 탭을 선택하고 보안 해시 알고리즘 SHA256을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="0b575-119">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-119">Click **OK**.</span></span>

![SHA256 서명 알고리즘--MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="0b575-121">AD FS PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="0b575-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="0b575-122">AD FS 서버에서 관리자 권한으로 PowerShell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="0b575-123">**Set-AdfsRelyingPartyTrust** cmdlet을 사용하여 보안 해시 알고리즘을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b575-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="0b575-124">참조 항목</span><span class="sxs-lookup"><span data-stu-id="0b575-124">Also read</span></span>
* [<span data-ttu-id="0b575-125">Azure AD Connect를 사용하여 Office 365 트러스트 복구</span><span class="sxs-lookup"><span data-stu-id="0b575-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

