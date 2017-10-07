---
title: "aaaAzure AD 암호 보안 계층 | Microsoft Docs"
description: "Azure AD가 강력한 암호를 적용하고 사이버 범죄자로부터 사용자 암호를 보호하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: joflore
ms.openlocfilehash: 10d8b600d9f4c02355b2cd8c5dccf8505aaf210d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="a-multi-tiered-approach-tooazure-ad-password-security"></a><span data-ttu-id="cfde3-103">다중 계층 접근 방식 tooAzure AD 암호 보안</span><span class="sxs-lookup"><span data-stu-id="cfde3-103">A multi-tiered approach tooAzure AD password security</span></span>

<span data-ttu-id="cfde3-104">몇 가지 모범 사례를 따르면 사용자 또는 관리자 tooprotect로 Azure Active Directory (Azure AD) 또는 Microsoft 계정에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-104">This article discusses some best practices you can follow as a user or as an administrator tooprotect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="cfde3-105">Azure AD 관리자가 hello 문서의 hello 지침을 사용 하 여 사용자 암호를 재설정할 수 [Azure Active Directory에서 사용자에 대 한 hello 암호 재설정](active-directory-users-reset-password-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-105">Azure AD administrators can reset user passwords using hello guidance in hello article [Reset hello password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="cfde3-106">사용자가 hello 문서의 hello 지침을 사용 하 여 자신의 암호를 재설정할 수 [Azure AD 암호를 잊어 버린 도움말](active-directory-passwords-update-your-own-password.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-106">Users can reset their own password using hello guidance in hello article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="cfde3-107">암호 요구 사항</span><span class="sxs-lookup"><span data-stu-id="cfde3-107">Password requirements</span></span>

<span data-ttu-id="cfde3-108">Azure AD 통합 hello 다음 일반적인 접근 방식을 toosecuring 암호:</span><span class="sxs-lookup"><span data-stu-id="cfde3-108">Azure AD incorporates hello following common approaches toosecuring passwords:</span></span>

* <span data-ttu-id="cfde3-109">암호 길이 요구 사항</span><span class="sxs-lookup"><span data-stu-id="cfde3-109">Password length requirements</span></span>
* <span data-ttu-id="cfde3-110">암호 복잡성 요구 사항</span><span class="sxs-lookup"><span data-stu-id="cfde3-110">Password complexity requirements</span></span>
* <span data-ttu-id="cfde3-111">일반 및 정기적인 암호 만료</span><span class="sxs-lookup"><span data-stu-id="cfde3-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="cfde3-112">Azure Active Directory에서 암호 재설정에 대 한 내용은 hello 항목을 참조 하십시오. [Azure AD 셀프 서비스 암호 재설정에 대 한 IT 전문가 hello](active-directory-passwords.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-112">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="cfde3-113">Azure AD 암호 보호</span><span class="sxs-lookup"><span data-stu-id="cfde3-113">Azure AD password protections</span></span>

<span data-ttu-id="cfde3-114">Azure AD 및 Microsoft 계정 시스템 입증 된 업계를 사용 하 여 hello 포함 하 여 사용자 및 관리자 암호의 보안 보호 tooensure 접근 방식을:</span><span class="sxs-lookup"><span data-stu-id="cfde3-114">Azure AD and hello Microsoft Account System use industry proven approaches tooensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="cfde3-115">동적으로 금지된 암호</span><span class="sxs-lookup"><span data-stu-id="cfde3-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="cfde3-116">스마트 암호 잠금</span><span class="sxs-lookup"><span data-stu-id="cfde3-116">Smart Password Lockout</span></span>

<span data-ttu-id="cfde3-117">현재 조사 결과에 따라 암호 관리에 대 한 내용은 hello 백서를 참조 하십시오. [암호 지침](http://aka.ms/passwordguidance)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-117">For information about password management based on current research, see hello whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="cfde3-118">동적으로 금지된 암호</span><span class="sxs-lookup"><span data-stu-id="cfde3-118">Dynamically banned passwords</span></span>

<span data-ttu-id="cfde3-119">Azure AD 및 Microsoft 계정은 일반적으로 사용되는 암호를 동적으로 금지함으로써 암호 보호를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="cfde3-120">hello Azure ID Id 보호 team 목록 금지 된 암호에서 자주 사용 되는 암호를 선택 하면 사용자가 방지를 정기적으로 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-120">hello Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="cfde3-121">이 서비스가 사용할 수 있는 tooAzure AD와 hello Microsoft 계정 서비스 고객입니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-121">This service is available tooAzure AD and hello Microsoft Account Service customers.</span></span>

<span data-ttu-id="cfde3-122">암호를 만들 때 관리자 tooencourage 사용자 toochoose 암호가 포함 된 구를 문자, 숫자, 문자 또는 단어의 고유한 조합에 대 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-122">When creating passwords, it is important for administrators tooencourage users toochoose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="cfde3-123">이 방법을 사용 하지만 사용자가 tooremember 기 더 쉽도록 거의 없는 toobe 손상 toomake 사용자 암호 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-123">This approach helps toomake user passwords nearly impossible toobe compromised but easier for users tooremember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="cfde3-124">암호 위반</span><span class="sxs-lookup"><span data-stu-id="cfde3-124">Password breaches</span></span>

<span data-ttu-id="cfde3-125">Microsoft에서는 항상 toostay 한 발 사이버 범죄자 앞서 노력 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-125">Microsoft is always working toostay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="cfde3-126">hello Azure AD Identity Protection 팀 일반적으로 사용 되는 암호를 지속적으로 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-126">hello Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="cfde3-127">사이버 범죄자 또한 사용 하 여 유사한 전략 tooinform 작성 등의 공격을 [레인 보우 테이블](https://en.wikipedia.org/wiki/Rainbow_table) 해독 암호 해시에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-127">Cyber-criminals also use similar strategies tooinform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="cfde3-128">Microsoft 분석 하 여 지속적으로 [데이터 침해](https://www.privacyrights.org/data-breaches) toomaintain 실제 해지기 전에 취약 한 암호는 사용 금지 보장 하는 금지 된 암호를 동적으로 업데이트 된 목록을 위협 tooAzure AD 고객 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) toomaintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat tooAzure AD customers.</span></span> <span data-ttu-id="cfde3-129">우리의 현재 보안 노력에 대 한 자세한 내용은 참조 hello [Microsoft 보안 인텔리전스 보고서](https://www.microsoft.com/security/sir/default.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-129">For more information about our current security efforts, see hello [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="cfde3-130">스마트 암호 잠금</span><span class="sxs-lookup"><span data-stu-id="cfde3-130">Smart Password Lockout</span></span>

<span data-ttu-id="cfde3-131">Azure AD에서 잠재적인 사이버 범죄 동안 toohack 사용자 암호를 검색 하는 경우 hello 사용자 계정과를 스마트 암호 잠금 잠급니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-131">When Azure AD detects a potential cyber-criminal trying toohack into a user password, we lock hello user account with Smart Password Lockout.</span></span> <span data-ttu-id="cfde3-132">Azure AD는 설계 되었습니다. 특정 로그인 세션과 연결 된 toodetermine hello 위험 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-132">Azure AD is designed toodetermine hello risk associated with specific login sessions.</span></span> <span data-ttu-id="cfde3-133">Hello 최신 보안 데이터를 사용 하 여 다음 잠금 의미 체계 toostop 사이버 위협 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-133">Then using hello most up-to-date security data, we apply lockout semantics toostop cyber threats.</span></span>

<span data-ttu-id="cfde3-134">Azure AD에서 사용자가 잠겨 경우 비슷한 toohello 순서에 해당 화면에 표시:</span><span class="sxs-lookup"><span data-stu-id="cfde3-134">If a user is locked out of Azure AD, their screen looks similar toohello one that follows:</span></span>

  ![Azure AD에서 차단](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="cfde3-136">다른 Microsoft 계정에 대 한 자신의 화면 표시 순서에 비슷한 toohello:</span><span class="sxs-lookup"><span data-stu-id="cfde3-136">For other Microsoft accounts, their screen looks similar toohello one that follows:</span></span>

  ![Microsoft 계정에서 차단](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="cfde3-138">Azure Active Directory에서 암호 재설정에 대 한 내용은 hello 항목을 참조 하십시오. [Azure AD 셀프 서비스 암호 재설정에 대 한 IT 전문가 hello](active-directory-passwords.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-138">For information about password reset in Azure Active Directory, see hello topic [Azure AD self-service password reset for hello IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="cfde3-139">Azure AD 관리자 인 경우 toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid 프로그램 사용자가 기존 암호를 모두 만들 합니다.</span><span class="sxs-lookup"><span data-stu-id="cfde3-139">If you are an Azure AD administrator, you may want toouse [Windows Hello](https://www.microsoft.com/windows/windows-hello) tooavoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="cfde3-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cfde3-140">Next steps</span></span>

* [<span data-ttu-id="cfde3-141">어떻게 tooupdate 암호</span><span class="sxs-lookup"><span data-stu-id="cfde3-141">How tooupdate your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="cfde3-142">hello Azure id 관리 기본 사항</span><span class="sxs-lookup"><span data-stu-id="cfde3-142">hello fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="cfde3-143">암호 재설정 활동에 대한 보고서</span><span class="sxs-lookup"><span data-stu-id="cfde3-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


