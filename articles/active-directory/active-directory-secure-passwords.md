---
title: "Azure AD 계층 암호 보안 | Microsoft Docs"
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
ms.openlocfilehash: 32464307ccb082b25538eaa522c1cdedef1ca555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="a-multi-tiered-approach-to-azure-ad-password-security"></a><span data-ttu-id="bf733-103">Azure AD 암호 보호에 대한 다중 계층 접근 방법</span><span class="sxs-lookup"><span data-stu-id="bf733-103">A multi-tiered approach to Azure AD password security</span></span>

<span data-ttu-id="bf733-104">이 문서에서는 Azure AD(Azure Active Directory) 또는 Microsoft 계정을 보호하기 위해 사용자 또는 관리자로서 수행할 수 있는 몇 가지 모범 사례를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-104">This article discusses some best practices you can follow as a user or as an administrator to protect your Azure Active Directory (Azure AD) or Microsoft Account.</span></span>

 > [!NOTE]
 > <span data-ttu-id="bf733-105">Azure AD 관리자는 [Azure Active Directory에서 사용자 암호 재설정](active-directory-users-reset-password-azure-portal.md) 문서의 지침을 사용하여 사용자 암호를 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-105">Azure AD administrators can reset user passwords using the guidance in the article [Reset the password for a user in Azure Active Directory](active-directory-users-reset-password-azure-portal.md).</span></span>
 >
 > <span data-ttu-id="bf733-106">사용자는 [Azure AD 암호를 잊어버렸어요. 도와주세요!](active-directory-passwords-update-your-own-password.md) 문서의 지침을 사용하여 암호를 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-106">Users can reset their own password using the guidance in the article [Help I forgot my Azure AD password](active-directory-passwords-update-your-own-password.md).</span></span>
 >

## <a name="password-requirements"></a><span data-ttu-id="bf733-107">암호 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bf733-107">Password requirements</span></span>

<span data-ttu-id="bf733-108">Azure AD는 암호를 보호하기 위해 다음과 같은 일반적인 접근 방식을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-108">Azure AD incorporates the following common approaches to securing passwords:</span></span>

* <span data-ttu-id="bf733-109">암호 길이 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bf733-109">Password length requirements</span></span>
* <span data-ttu-id="bf733-110">암호 복잡성 요구 사항</span><span class="sxs-lookup"><span data-stu-id="bf733-110">Password complexity requirements</span></span>
* <span data-ttu-id="bf733-111">일반 및 정기적인 암호 만료</span><span class="sxs-lookup"><span data-stu-id="bf733-111">Regular and periodic password expiration</span></span>

<span data-ttu-id="bf733-112">Azure Active Directory의 암호 재설정에 대한 자세한 내용은 [IT 전문가를 위한 Azure AD 셀프 서비스 암호 재설정](active-directory-passwords.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf733-112">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

## <a name="azure-ad-password-protections"></a><span data-ttu-id="bf733-113">Azure AD 암호 보호</span><span class="sxs-lookup"><span data-stu-id="bf733-113">Azure AD password protections</span></span>

<span data-ttu-id="bf733-114">Azure AD 및 Microsoft 계정 시스템은 사용자 및 관리자 암호를 안전하게 보호하기 위해 다음을 비롯하여 업계에서 증명된 접근 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-114">Azure AD and the Microsoft Account System use industry proven approaches to ensure secure protection of user and administrator passwords including:</span></span>

* <span data-ttu-id="bf733-115">동적으로 금지된 암호</span><span class="sxs-lookup"><span data-stu-id="bf733-115">Dynamically banned passwords</span></span>
* <span data-ttu-id="bf733-116">스마트 암호 잠금</span><span class="sxs-lookup"><span data-stu-id="bf733-116">Smart Password Lockout</span></span>

<span data-ttu-id="bf733-117">현재 연구 결과에 따른 암호 관리에 대한 내용은 [암호 지침](http://aka.ms/passwordguidance) 백서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf733-117">For information about password management based on current research, see the whitepaper [Password Guidance](http://aka.ms/passwordguidance).</span></span>

### <a name="dynamically-banned-passwords"></a><span data-ttu-id="bf733-118">동적으로 금지된 암호</span><span class="sxs-lookup"><span data-stu-id="bf733-118">Dynamically banned passwords</span></span>

<span data-ttu-id="bf733-119">Azure AD 및 Microsoft 계정은 일반적으로 사용되는 암호를 동적으로 금지함으로써 암호 보호를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-119">Azure AD and Microsoft Accounts safeguard password protection by dynamically banning commonly used passwords.</span></span> <span data-ttu-id="bf733-120">Azure AD ID 보호 팀은 금지된 암호 목록을 정기적으로 분석하여 사용자가 자주 사용되는 암호를 선택하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-120">The Azure ID Identity Protection team routinely analyzes banned password lists, preventing users from selecting commonly used passwords.</span></span> <span data-ttu-id="bf733-121">Azure AD 및 Microsoft 계정 서비스 고객은 이 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-121">This service is available to Azure AD and the Microsoft Account Service customers.</span></span>

<span data-ttu-id="bf733-122">암호를 만들 때 관리자는 사용자가 고유한 글자, 숫자, 문자 또는 단어 조합을 포함하는 암호 구문을 선택했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-122">When creating passwords, it is important for administrators to encourage users to choose password phrases that include a unique combination of letters, numbers, characters, or words.</span></span> <span data-ttu-id="bf733-123">이 방법은 사용자 암호가 거의 노출되지 않게 하면서 사용자가 보다 쉽게 기억할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-123">This approach helps to make user passwords nearly impossible to be compromised but easier for users to remember.</span></span>

#### <a name="password-breaches"></a><span data-ttu-id="bf733-124">암호 위반</span><span class="sxs-lookup"><span data-stu-id="bf733-124">Password breaches</span></span>

<span data-ttu-id="bf733-125">Microsoft는 항상 한 발 앞서 사이버 범죄에 대처하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-125">Microsoft is always working to stay one step ahead of cyber-criminals.</span></span>

<span data-ttu-id="bf733-126">Azure AD ID 보호 팀은 일반적으로 사용되는 암호를 지속적으로 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-126">The Azure AD Identity Protection team continually analyzes passwords that are commonly used.</span></span> <span data-ttu-id="bf733-127">사이버 범죄자들도 암호 해시를 공격하는 [레인보우 테이블](https://en.wikipedia.org/wiki/Rainbow_table)을 빌드하는 등 공격을 알리는 데 유사한 전략을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-127">Cyber-criminals also use similar strategies to inform their attacks, such as building a [rainbow table](https://en.wikipedia.org/wiki/Rainbow_table) for cracking password hashes.</span></span>

<span data-ttu-id="bf733-128">Microsoft는 지속적으로 [데이터 위반](https://www.privacyrights.org/data-breaches)을 분석하여 동적으로 업데이트된 차단 암호 목록을 관리합니다. 그러면 취약한 암호가 Azure AD 고객에게 실제 위협이 되기 전에 차단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-128">Microsoft continually analyzes [data breaches](https://www.privacyrights.org/data-breaches) to maintain a dynamically updated banned password list, which ensures that vulnerable passwords are banned before they become a real threat to Azure AD customers.</span></span> <span data-ttu-id="bf733-129">현재 보안 노력에 대한 자세한 내용은 [Microsoft 보안 인텔리전스 보고서](https://www.microsoft.com/security/sir/default.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf733-129">For more information about our current security efforts, see the [Microsoft Security Intelligence Report](https://www.microsoft.com/security/sir/default.aspx).</span></span>

### <a name="smart-password-lockout"></a><span data-ttu-id="bf733-130">스마트 암호 잠금</span><span class="sxs-lookup"><span data-stu-id="bf733-130">Smart Password Lockout</span></span>

<span data-ttu-id="bf733-131">Azure AD에서 사용자 암호를 해킹하려는 잠재적인 사이버 범죄를 감지하면 스마트 암호 잠금을 사용하여 사용자 계정을 잠그게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-131">When Azure AD detects a potential cyber-criminal trying to hack into a user password, we lock the user account with Smart Password Lockout.</span></span> <span data-ttu-id="bf733-132">Azure AD는 특정 로그인 세션과 연결된 위험성을 확인하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-132">Azure AD is designed to determine the risk associated with specific login sessions.</span></span> <span data-ttu-id="bf733-133">그런 후 최신 보안 데이터를 사용하여 잠금 의미 체계를 적용함으로써 사이버 위협을 막을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-133">Then using the most up-to-date security data, we apply lockout semantics to stop cyber threats.</span></span>

<span data-ttu-id="bf733-134">사용자가 Azure AD에서 차단된 경우 해당 화면은 다음과 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-134">If a user is locked out of Azure AD, their screen looks similar to the one that follows:</span></span>

  ![Azure AD에서 차단](./media/active-directory-secure-passwords/locked-out-azuread.png)

<span data-ttu-id="bf733-136">다른 Microsoft 계정의 경우 해당 화면은 다음과 비슷하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-136">For other Microsoft accounts, their screen looks similar to the one that follows:</span></span>

  ![Microsoft 계정에서 차단](./media/active-directory-secure-passwords/locked-out-ms-accounts.png)

<span data-ttu-id="bf733-138">Azure Active Directory의 암호 재설정에 대한 자세한 내용은 [IT 전문가를 위한 Azure AD 셀프 서비스 암호 재설정](active-directory-passwords.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf733-138">For information about password reset in Azure Active Directory, see the topic [Azure AD self-service password reset for the IT professional](active-directory-passwords.md).</span></span>

  >[!NOTE]
  ><span data-ttu-id="bf733-139">Azure AD 관리자인 경우 [Windows Hello](https://www.microsoft.com/windows/windows-hello)를 사용하여 사용자가 기존 암호를 모두 만들지 않도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf733-139">If you are an Azure AD administrator, you may want to use [Windows Hello](https://www.microsoft.com/windows/windows-hello) to avoid having your users create traditional passwords altogether.</span></span>
  >

## <a name="next-steps"></a><span data-ttu-id="bf733-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf733-140">Next steps</span></span>

* [<span data-ttu-id="bf733-141">고유한 암호를 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="bf733-141">How to update your own password</span></span>](active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="bf733-142">Azure ID 관리의 기본 항목</span><span class="sxs-lookup"><span data-stu-id="bf733-142">The fundamentals of Azure identity management</span></span>](fundamentals-identity.md)
* [<span data-ttu-id="bf733-143">암호 재설정 활동에 대한 보고서</span><span class="sxs-lookup"><span data-stu-id="bf733-143">Report on password reset activity</span></span>](active-directory-passwords-reporting.md)


