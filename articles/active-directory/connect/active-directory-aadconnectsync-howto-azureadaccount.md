---
title: "Azure AD Connect 동기화: Azure AD 서비스 계정을 관리하는 방법 | Microsoft Docs"
description: "이 항목은 Azure AD 서비스 계정을 복원하는 방법을 설명합니다."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, Azure AD Connect 동기화 커넥터 서비스 계정의 암호를 재설정하는 방법"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8e9e8192ee4fcb636b5be91d2616acbc9120c8c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="b7180-104">Azure AD Connect 동기화: Azure AD 서비스 계정을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="b7180-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="b7180-105">Azure AD Connector가 사용하는 서비스 계정은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="b7180-106">자격 증명을 재설정해야 할 경우 이 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b7180-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="b7180-107">예를 들어 전역 관리자가 PowerShell을 사용하여 실수로 서비스 계정의 암호를 재설정한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="b7180-108">자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="b7180-108">Reset the credentials</span></span>
<span data-ttu-id="b7180-109">인증 문제로 인해 Azure AD Connector에서 정의된 서비스 계정으로 Azure AD에 연결할 수 없다면 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="b7180-110">Azure AD Connect 동기화 서버에 로그인하고 PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="b7180-111">`Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="b7180-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="b7180-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="b7180-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="b7180-113">Azure AD 전역 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="b7180-114">이 cmdlet은 서비스 계정의 암호를 재설정하고 Azure AD와 동기화 엔진에서 암호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="b7180-115">이 단계에서 해결할 수 있다고 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="b7180-115">Known issues these steps can solve</span></span>
<span data-ttu-id="b7180-116">이 섹션은 Azure AD 서비스 계정에서 다시 설정된 자격 증명에 의해 수정된 고객이 보고한 오류 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="b7180-117">이벤트 6900</span><span class="sxs-lookup"><span data-stu-id="b7180-117">Event 6900</span></span>  
<span data-ttu-id="b7180-118">서버가 암호 변경 알림을 처리하는 동안 예기치 않은 오류가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="b7180-119">AADSTS70002: 자격 증명의 유효성 검사 오류.</span><span class="sxs-lookup"><span data-stu-id="b7180-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="b7180-120">AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS50054: 이전 암호가 인증에 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="b7180-121">이벤트 659</span><span class="sxs-lookup"><span data-stu-id="b7180-121">Event 659</span></span>  
<span data-ttu-id="b7180-122">암호 정책 동기화 구성을 검색하는 도중 오류 발생.</span><span class="sxs-lookup"><span data-stu-id="b7180-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="b7180-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="b7180-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="b7180-124">AADSTS70002: 자격 증명의 유효성 검사 오류.</span><span class="sxs-lookup"><span data-stu-id="b7180-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="b7180-125">AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS50054: 이전 암호가 인증에 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b7180-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7180-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b7180-126">Next steps</span></span>
<span data-ttu-id="b7180-127">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="b7180-127">**Overview topics**</span></span>

* [<span data-ttu-id="b7180-128">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b7180-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="b7180-129">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="b7180-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

