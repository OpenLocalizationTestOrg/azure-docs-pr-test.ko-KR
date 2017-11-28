---
title: "Azure AD Connect 동기화: toomanage hello Azure AD 서비스 계정을 어떻게 | Microsoft Docs"
description: "이 항목 toorestore hello Azure AD 서비스 계정 하는 방법을 설명 합니다."
services: active-directory
keywords: "Tooreset hello에 대 한 암호 방법을 Azure AD Connect 동기화 서비스 계정 커넥터 hello AADSTS70002, AADSTS50054,"
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
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="d7189-104">Azure AD Connect 동기화: 어떻게 toomanage hello Azure AD 서비스 계정</span><span class="sxs-lookup"><span data-stu-id="d7189-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="d7189-105">hello 서비스 hello Azure AD 커넥터에서 사용 하는 계정은 무료 toobe 서비스.</span><span class="sxs-lookup"><span data-stu-id="d7189-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="d7189-106">자격 증명 tooreset 해야 할 경우이 항목은 드립니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="d7189-107">예를 들어, 전역 관리자는 실수 PowerShell을 사용 하 여 hello 서비스 계정에 대해 hello 암호 재설정으로 가집니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="d7189-108">Hello 자격 증명 다시 설정</span><span class="sxs-lookup"><span data-stu-id="d7189-108">Reset hello credentials</span></span>
<span data-ttu-id="d7189-109">Azure AD 커넥터 hello에 정의 된 hello 서비스 계정이 tooauthentication 문제 때문에 Azure AD에 연결할 수 없는 경우에 hello 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="d7189-110">Toohello Azure AD Connect 동기화 서버에 로그인 하 고 PowerShell을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="d7189-111">`Add-ADSyncAADServiceAccount`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="d7189-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="d7189-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="d7189-113">Azure AD 전역 관리자 자격 증명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="d7189-114">이 cmdlet는 hello hello 서비스 계정의 암호를 다시 설정 하 고 hello 동기화 엔진 및 Azure AD에서 모두 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="d7189-115">이 단계에서 해결할 수 있다고 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="d7189-115">Known issues these steps can solve</span></span>
<span data-ttu-id="d7189-116">이 섹션은 hello Azure AD 서비스 계정에서 다시 설정 하는 자격 증명으로 수정 된 고객에 의해 보고 된 오류 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="d7189-117">이벤트 6900</span><span class="sxs-lookup"><span data-stu-id="d7189-117">Event 6900</span></span>  
<span data-ttu-id="d7189-118">hello 서버 암호 변경 알림을 처리 하는 동안 예기치 않은 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="d7189-119">AADSTS70002: 자격 증명의 유효성 검사 오류.</span><span class="sxs-lookup"><span data-stu-id="d7189-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="d7189-120">AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS50054: 이전 암호가 인증에 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="d7189-121">이벤트 659</span><span class="sxs-lookup"><span data-stu-id="d7189-121">Event 659</span></span>  
<span data-ttu-id="d7189-122">암호 정책 동기화 구성을 검색하는 도중 오류 발생.</span><span class="sxs-lookup"><span data-stu-id="d7189-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="d7189-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span><span class="sxs-lookup"><span data-stu-id="d7189-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="d7189-124">AADSTS70002: 자격 증명의 유효성 검사 오류.</span><span class="sxs-lookup"><span data-stu-id="d7189-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="d7189-125">AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS50054: 이전 암호가 인증에 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d7189-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7189-126">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d7189-126">Next steps</span></span>
<span data-ttu-id="d7189-127">**개요 항목**</span><span class="sxs-lookup"><span data-stu-id="d7189-127">**Overview topics**</span></span>

* [<span data-ttu-id="d7189-128">Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="d7189-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="d7189-129">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="d7189-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

