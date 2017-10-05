---
title: "Azure AD Connect 동기화로 암호 동기화 구현 | Microsoft Docs"
description: "암호 동기화 작동 방식 및 설정 방법에 대한 정보를 제공합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: db9b1578a235be9018fc1985cc75a0a05ee47b3a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="8f856-103">Azure AD Connect 동기화를 사용하여 암호 동기화 구현</span><span class="sxs-lookup"><span data-stu-id="8f856-103">Implement password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="8f856-104">이 문서에서는 온-프레미스 Active Directory 인스턴스에서 클라우드 기반 Azure Active Directory(Azure AD) 인스턴스로 사용자 암호를 동기화하는 데 필요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-104">This article provides information that you need to synchronize your user passwords from an on-premises Active Directory instance to a cloud-based Azure Active Directory (Azure AD) instance.</span></span>

## <a name="what-is-password-synchronization"></a><span data-ttu-id="8f856-105">암호 동기화란 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="8f856-105">What is password synchronization</span></span>
<span data-ttu-id="8f856-106">암호를 잊어버려서 작업을 수행하지 못할 확률은 기억해야 하는 암호의 수와 관련됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-106">The probability that you're blocked from getting your work done due to a forgotten password is related to the number of different passwords you need to remember.</span></span> <span data-ttu-id="8f856-107">기억할 암호가 많을 수록 잊을 확률이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-107">The more passwords you need to remember, the higher the probability to forget one.</span></span> <span data-ttu-id="8f856-108">암호 다시 설정 및 기타 암호 관련 문제에 대한 질문 및 호출은 많은 helpdesk 리소스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-108">Questions and calls about password resets and other password-related issues demand the most helpdesk resources.</span></span>

<span data-ttu-id="8f856-109">암호 동기화는 온-프레미스 Active Directory 인스턴스에서 클라우드 기반 Azure AD 인스턴스로 사용자 암호를 동기화하는 데 사용되는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-109">Password synchronization is a feature used to synchronize user passwords from an on-premises Active Directory instance to a cloud-based Azure AD instance.</span></span>
<span data-ttu-id="8f856-110">이 기능을 사용하여 Office 365, Microsoft Intune, CRM Online 및 Azure Active Directory Domain Services(Azure AD DS)와 같은 Azure AD 서비스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-110">Use this feature to sign in to Azure AD services like Office 365, Microsoft Intune, CRM Online, and Azure Active Directory Domain Services (Azure AD DS).</span></span> <span data-ttu-id="8f856-111">온-프레미스 Active Directory 인스턴스에 로그인하기 위해 사용하는 암호와 동일한 암호를 사용하여 서비스에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-111">You sign in to the service by using the same password you use to sign in to your on-premises Active Directory instance.</span></span>

![Azure AD Connect의 정의](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

<span data-ttu-id="8f856-113">암호의 수를 줄여서 사용자는 암호를 하나만 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-113">By reducing the number of passwords, your users need to maintain to just one.</span></span> <span data-ttu-id="8f856-114">암호 동기화를 사용하면 다음을 수행하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-114">Password synchronization helps you to:</span></span>

* <span data-ttu-id="8f856-115">사용자의 생산성 향상.</span><span class="sxs-lookup"><span data-stu-id="8f856-115">Improve the productivity of your users.</span></span>
* <span data-ttu-id="8f856-116">지원 센터 비용 절감.</span><span class="sxs-lookup"><span data-stu-id="8f856-116">Reduce your helpdesk costs.</span></span>  

<span data-ttu-id="8f856-117">또한 [AD FS(Active Directory Federation Services)와 페더레이션](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect)을 사용하도록 선택하는 경우 필요에 따라 AD FS 인프라에 장애가 발생할 경우 백업으로 암호 동기화를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-117">Also, if you decide to use [Federation with Active Directory Federation Services (AD FS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), you can optionally set up password synchronization as a backup in case your AD FS infrastructure fails.</span></span>

<span data-ttu-id="8f856-118">암호 동기화는 Azure AD Connect 동기화를 통한 디렉터리 동기화 기능 구현의 확장판입니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-118">Password synchronization is an extension to the directory synchronization feature implemented by Azure AD Connect sync.</span></span> <span data-ttu-id="8f856-119">사용자 환경에서 암호 동기화를 사용하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-119">To use password synchronization in your environment, you need to:</span></span>

* <span data-ttu-id="8f856-120">Azure AD Connect 설치.</span><span class="sxs-lookup"><span data-stu-id="8f856-120">Install Azure AD Connect.</span></span>  
* <span data-ttu-id="8f856-121">온-프레미스 Active Directory 인스턴스 및 Azure Active Directory 인스턴스 간에 디렉터리 동기화 구성.</span><span class="sxs-lookup"><span data-stu-id="8f856-121">Configure directory synchronization between your on-premises Active Directory instance and your Azure Active Directory instance.</span></span>
* <span data-ttu-id="8f856-122">암호 동기화 사용.</span><span class="sxs-lookup"><span data-stu-id="8f856-122">Enable password synchronization.</span></span>

<span data-ttu-id="8f856-123">자세한 내용은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f856-123">For more details, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8f856-124">FIPS 및 암호 동기화에 대해 구성된 Azure Active Directory Domain Services에 대한 자세한 내용은 문서 뒷부분에 나오는 "암호 동기화 및 FIPS"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f856-124">For more details about Azure Active Directory Domain Services configured for FIPS and password synchronization, see "Password synchronization and FIPS" later in this article.</span></span>
>
>

## <a name="how-password-synchronization-works"></a><span data-ttu-id="8f856-125">암호 동기화 작동 방법</span><span class="sxs-lookup"><span data-stu-id="8f856-125">How password synchronization works</span></span>
<span data-ttu-id="8f856-126">Active Directory 도메인 서비스는 실제 사용자 암호의 해시 값 표현 형태로 암호를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-126">The Active Directory domain service stores passwords in the form of a hash value representation of the actual user password.</span></span> <span data-ttu-id="8f856-127">해시 값은 단방향 수학 함수(*해시 알고리즘*)의 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-127">A hash value is a result of a one-way mathematical function (the *hashing algorithm*).</span></span> <span data-ttu-id="8f856-128">암호의 일반 텍스트 버전에 대한 함수의 결과를 되돌릴 수 있는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-128">There is no method to revert the result of a one-way function to the plain text version of a password.</span></span> <span data-ttu-id="8f856-129">암호 해시를 사용하여 온-프레미스 네트워크에 로그인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-129">You cannot use a password hash to sign in to your on-premises network.</span></span>

<span data-ttu-id="8f856-130">암호를 동기화 하기 위해, Azure AD Connect 동기화는 온-프레미스 Active Directory 인스턴스에서 암호 해시를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-130">To synchronize your password, Azure AD Connect sync extracts your password hash from the on-premises Active Directory instance.</span></span> <span data-ttu-id="8f856-131">Azure Active Directory 인증 서비스로 동기화 되기 전에 암호 해시에 추가적인 보안 처리가 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-131">Extra security processing is applied to the password hash before it is synchronized to the Azure Active Directory authentication service.</span></span> <span data-ttu-id="8f856-132">암호는 각 사용자 기본별로 동기화되고 시간 순서대로 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-132">Passwords are synchronized on a per-user basis and in chronological order.</span></span>

<span data-ttu-id="8f856-133">암호 동기화 과정의 실제 흐름은 DisplayName 또는 전자 메일 주소와 같은 사용자 데이터 동기화와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-133">The actual data flow of the password synchronization process is similar to the synchronization of user data such as DisplayName or Email Addresses.</span></span> <span data-ttu-id="8f856-134">그러나 암호는 다른 특성에 대한 표준 디렉터리 동기화 창보다 더 자주 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-134">However, passwords are synchronized more frequently than the standard directory synchronization window for other attributes.</span></span> <span data-ttu-id="8f856-135">암호 동기화 프로세스는 2분 마다 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-135">The password synchronization process runs every 2 minutes.</span></span> <span data-ttu-id="8f856-136">이 프로세스의 빈도를 수정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-136">You cannot modify the frequency of this process.</span></span> <span data-ttu-id="8f856-137">암호를 동기화할 경우 기존 클라우드 암호를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-137">When you synchronize a password, it overwrites the existing cloud password.</span></span>

<span data-ttu-id="8f856-138">암호 동기화 기능을 사용하도록 처음으로 설정하면 범위 내 모든 사용자 암호에 대한 초기 동기화를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-138">The first time you enable the password synchronization feature, it performs an initial synchronization of the passwords of all in-scope users.</span></span> <span data-ttu-id="8f856-139">동기화할 사용자 암호의 하위 집합을 명시적으로 정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-139">You cannot explicitly define a subset of user passwords that you want to synchronize.</span></span>

<span data-ttu-id="8f856-140">온-프레미스 암호를 변경하면, 업데이트된 암호는 대개 몇 분 내에 동기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-140">When you change an on-premises password, the updated password is synchronized, most often in a matter of minutes.</span></span>
<span data-ttu-id="8f856-141">암호 동기화 기능은 실패한 사용자 암호 동기화를 자동으로 재시도합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-141">The password synchronization feature automatically retries failed synchronization attempts.</span></span> <span data-ttu-id="8f856-142">암호를 동기화하는 동안 오류가 발생하면 이벤트 뷰어에 오류가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-142">If an error occurs during an attempt to synchronize a password, an error is logged in your event viewer.</span></span>

<span data-ttu-id="8f856-143">암호 동기화는 현재 로그인된 사용자에게 아무런 영향도 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-143">The synchronization of a password has no impact on the user  who is currently signed in.</span></span>
<span data-ttu-id="8f856-144">클라우드 서비스에 로그온해 있는 동안, 동기화된 암호가 변경되더라도 현재 클라우드 세션이 즉시 영향을 받지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-144">Your current cloud service session is not immediately affected by a synchronized password change that occurs while you are signed in to a cloud service.</span></span> <span data-ttu-id="8f856-145">하지만, 클라우드 서비스에서 다시 인증을 요구하면 새 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-145">However, when the cloud service requires you to authenticate again, you need to provide your new password.</span></span>

<span data-ttu-id="8f856-146">사용자는 회사 네트워크에 로그인되어 있는지 여부에 관계없이 Azure AD에 인증하려면 회사 자격 증명을 다시 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-146">A user must enter their corporate credentials a second time to authenticate to Azure AD, regardless of whether they're signed in to their corporate network.</span></span> <span data-ttu-id="8f856-147">하지만 사용자가 로그인 시 로그인 유지(KMSI) 확인란을 선택하면 이러한 패턴을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-147">These pattern can be minimized, however, if the user selects the Keep me signed in (KMSI) check box at sign in.</span></span> <span data-ttu-id="8f856-148">이 확인란을 선택하면 짧은 기간 동안 인증을 우회하는 세션 쿠키가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-148">This selection sets a session cookie that bypasses authentication for a short period.</span></span> <span data-ttu-id="8f856-149">KMSI 동작은 Azure AD 관리자가 설정 또는 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-149">KMSI behavior can be enabled or disabled by the Azure AD administrator.</span></span>

> [!NOTE]
> <span data-ttu-id="8f856-150">암호 동기화는 Active Directory의 개체 형식 사용자에만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-150">Password sync is only supported for the object type user in Active Directory.</span></span> <span data-ttu-id="8f856-151">iNetOrgPerson 개체 형식에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-151">It is not supported for the iNetOrgPerson object type.</span></span>

### <a name="detailed-description-of-how-password-synchronization-works"></a><span data-ttu-id="8f856-152">암호 동기화가 작동하는 방법에 대한 자세한 설명</span><span class="sxs-lookup"><span data-stu-id="8f856-152">Detailed description of how password synchronization works</span></span>
<span data-ttu-id="8f856-153">다음은 Active Directory와 Azure AD 간에 암호 동기화가 작동하는 방식에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-153">The following describes in-depth how password synchronization works between Active Directory and Azure AD.</span></span>

![자세한 암호 흐름](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. <span data-ttu-id="8f856-155">2분마다 AD Connect 서버의 암호 동기화 에이전트는 DC 간 데이터 동기화에 사용되는 표준 [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) 복제 프로토콜을 통해 DC에서 저장된 암호 해시(unicodePwd 특성)를 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-155">Every two minutes, the password synchronization agent on the AD Connect server requests stored password hashes (the unicodePwd attribute) from a DC via the standard [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) replication protocol used to synchronize data between DCs.</span></span> <span data-ttu-id="8f856-156">암호 해시를 얻으려면 서비스 계정에 디렉터리 변경 내용 복제 및 모든 디렉터리 변경 내용 복제 AD 권한(설치 시 기본적으로 부여)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-156">The service account must have Replicate Directory Changes and Replicate Directory Changes All AD permissions (granted by default on installation) to obtain the password hashes.</span></span>
2. <span data-ttu-id="8f856-157">전송하기 전에 DC는 RPC 세션 키의 [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) 해시인 키와 솔트를 사용하여 MD4 암호 해시를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-157">Before sending, the DC encrypts the MD4 password hash by using a key that is a [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hash of the RPC session key and a salt.</span></span> <span data-ttu-id="8f856-158">그런 다음 RPC를 통해 암호 동기화 에이전트에 결과를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-158">It then sends the result to the password synchronization agent over RPC.</span></span> <span data-ttu-id="8f856-159">또한 DC는 DC 복제 프로토콜을 사용하여 동기화 에이전트에 솔트를 전달하고, 따라서 에이전트는 봉투(Envelope)를 해독할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-159">The DC also passes the salt to the synchronization agent by using the DC replication protocol, so the agent will be able to decrypt the envelope.</span></span>
3.  <span data-ttu-id="8f856-160">암호 동기화 에이전트는 봉투(Envelope)를 암호화한 후 [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx)와 솔트를 사용하여 수신한 데이터를 원래 MD4 형식으로 해독하는 키를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-160">After the password synchronization agent has the encrypted envelope, it uses [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) and the salt to generate a key to decrypt the received data back to its original MD4 format.</span></span> <span data-ttu-id="8f856-161">암호 동기화 에이전트에는 어떤 경우에도 일반 텍스트 암호에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-161">At no point does the password synchronization agent have access to the clear text password.</span></span> <span data-ttu-id="8f856-162">암호 동기화 에이전트의 MD5 사용은 DC와의 복제 프로토콜 호환성으로 그 용도가 엄격하게 제한되며 DC와 암호 동기화 에이전트 간의 온-프레미스에서만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-162">The password synchronization agent’s use of MD5 is strictly for replication protocol compatibility with the DC, and it is only used on premises between the DC and the password synchronization agent.</span></span>
4.  <span data-ttu-id="8f856-163">암호 동기화 에이전트는 해시를 32바이트 16진수 문자열로 변환한 후 UTF-16 인코딩을 사용하여 이 문자열을 다시 이진으로 변환하는 방법으로 16바이트 이진 암호 해시를 64바이트로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-163">The password synchronization agent expands the 16-byte binary password hash to 64 bytes by first converting the hash to a 32-byte hexadecimal string, then converting this string back into binary with UTF-16 encoding.</span></span>
5.  <span data-ttu-id="8f856-164">암호 동기화 에이전트는 10바이트 길이 솔트로 구성된 솔트를 64비트 이진 파일에 추가하여 원래 해시의 보안을 강화합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-164">The password synchronization agent adds a salt, consisting of a 10-byte length salt, to the 64-byte binary to further protect the original hash.</span></span>
6.  <span data-ttu-id="8f856-165">그런 다음 암호 동기화 에이전트는 MD4 해시와 솔트를 결합하고 [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) 함수에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-165">The password synchronization agent then combines the MD4 hash plus salt, and inputs it into the [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) function.</span></span> <span data-ttu-id="8f856-166">[HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) 키 지정 해시 알고리즘이 1000번 반복하여 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-166">1000 iterations of the [HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) keyed hashing algorithm is used.</span></span> 
7.  <span data-ttu-id="8f856-167">암호 동기화 에이전트는 결과 32바이트 해시를 가져오고, 솔트와 SHA256 반복 횟수를 해시에 연결하고(Azure AD가 사용할 수 있도록), SSL을 통해 Azure AD Connect에서 Azure AD로 문자열을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-167">The password synchronization agent takes the resulting 32-byte hash, concatenates both the salt and the number of SHA256 iterations to it (for use by Azure AD), then transmits the string from Azure AD Connect to Azure AD over SSL.</span></span></br> 
8.  <span data-ttu-id="8f856-168">사용자가 Azure AD에 로그인을 시도하고 암호를 입력하면 암호가 동일한 MD4+salt+PBKDF2+HMAC-SHA256 프로세스를 통해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-168">When a user attempts to sign in to Azure AD and enters their password, the password is run through the same MD4+salt+PBKDF2+HMAC-SHA256 process.</span></span> <span data-ttu-id="8f856-169">결과 해시가 Azure AD에 저장된 해시와 일치하고 사용자가 올바른 암호를 입력하면 해당 사용자가 인증됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-169">If the resulting hash matches the hash stored in Azure AD, the user has entered the correct password and is authenticated.</span></span> 

>[!Note] 
><span data-ttu-id="8f856-170">원래 MD4 해시는 Azure AD로 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-170">The original MD4 hash is not transmitted to Azure AD.</span></span> <span data-ttu-id="8f856-171">대신 원래 MD4 해시의 SHA256 해시가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-171">Instead, the SHA256 hash of the original MD4 hash is transmitted.</span></span> <span data-ttu-id="8f856-172">결과적으로 Azure AD에 저장된 해시를 습득하더라도 온-프레미스 pass-the-hash 공격에 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-172">As a result, if the hash stored in Azure AD is obtained, it cannot be used in an on-premises pass-the-hash attack.</span></span>

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a><span data-ttu-id="8f856-173">암호 동기화가 Azure Active Directory Domain Services와 작동하는 방식</span><span class="sxs-lookup"><span data-stu-id="8f856-173">How password synchronization works with Azure Active Directory Domain Services</span></span>
<span data-ttu-id="8f856-174">암호 동기화 기능을 사용하여 온-프레미스 암호를 [Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md)에 동기화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-174">You can also use the password synchronization feature to synchronize your on-premises passwords to [Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md).</span></span> <span data-ttu-id="8f856-175">이 시나리오에서는 Azure Active Directory Domain Services 인스턴스가 온-프레미스 Active Directory 인스턴스에서 사용할 수 있는 모든 방법을 사용하여 클라우드에서 사용자를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-175">In this scenario, the Azure Active Directory Domain Services instance authenticates your users in the cloud with all the methods available in your on-premises Active Directory instance.</span></span> <span data-ttu-id="8f856-176">이 시나리오의 환경은 온-프레미스 환경에서 ADMT(Active Directory 마이그레이션 도구)를 사용하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-176">The experience of this scenario is similar to using the Active Directory Migration Tool (ADMT) in an on-premises environment.</span></span>

### <a name="security-considerations"></a><span data-ttu-id="8f856-177">보안 고려 사항</span><span class="sxs-lookup"><span data-stu-id="8f856-177">Security considerations</span></span>
<span data-ttu-id="8f856-178">암호를 동기화 할 때, 사용자 암호의 일반 텍스트 버전은 암호 동기화 기능, Azure AD 혹은 다른 어떤 관련 서비스에 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-178">When synchronizing passwords, the plain-text version of your password is not exposed to the password synchronization feature, to Azure AD, or any of the associated services.</span></span>

<span data-ttu-id="8f856-179">사용자 인증은 조직의 고유한 Active Directory 인스턴스가 아닌 Azure AD에 대해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-179">User authentication takes place against Azure AD rather than against the organization's own Active Directory instance.</span></span> <span data-ttu-id="8f856-180">암호 데이터가 어떤 형태로든 프레미스를 벗어난다는 점을 조직에서 염려하는 경우 Azure AD에 저장된 SHA256 암호 데이터, 즉 원래 MD4 해시의 해시가 Active Directory에 저장된 것보다 훨씬 안전하다는 사실을 고려하십시오.</span><span class="sxs-lookup"><span data-stu-id="8f856-180">If your organization has concerns about password data in any form leaving the premises, consider the fact that the SHA256 password data stored in Azure AD--a hash of the original MD4 hash--is significantly more secure than what is stored in Active Directory.</span></span> <span data-ttu-id="8f856-181">뿐만 아니라 이 SHA256 해시는 해독이 불가능하기 때문에 조직의 Active Directory 환경으로 가져와서 pass-the-hash 공격에서 유효한 사용자 암호로 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-181">Further, because this SHA256 hash cannot be decrypted, it cannot be brought back to the organization's Active Directory environment and presented as a valid user password in a pass-the-hash attack.</span></span>





### <a name="password-policy-considerations"></a><span data-ttu-id="8f856-182">암호 정책 고려 사항</span><span class="sxs-lookup"><span data-stu-id="8f856-182">Password policy considerations</span></span>
<span data-ttu-id="8f856-183">암호 동기화를 사용하여 영향을 받는 두 가지 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-183">There are two types of password policies that are affected by enabling password synchronization:</span></span>

* <span data-ttu-id="8f856-184">암호 복잡성 정책</span><span class="sxs-lookup"><span data-stu-id="8f856-184">Password complexity policy</span></span>
* <span data-ttu-id="8f856-185">암호 만료 정책</span><span class="sxs-lookup"><span data-stu-id="8f856-185">Password expiration policy</span></span>

#### <a name="password-complexity-policy"></a><span data-ttu-id="8f856-186">암호 복잡성 정책</span><span class="sxs-lookup"><span data-stu-id="8f856-186">Password complexity policy</span></span>  
<span data-ttu-id="8f856-187">암호 동기화를 사용하는 경우 온-프레미스 Active Directory 인스턴스의 암호 복잡성 정책이 동기화된 사용자에 대한 클라우드의 복잡성 정책을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-187">When password synchronization is enabled, the password complexity policies in your on-premises Active Directory instance override complexity policies in the cloud for synchronized users.</span></span> <span data-ttu-id="8f856-188">온-프레미스 Active Directory 인스턴스의 유효한 모든 암호를 사용하여 Azure AD 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-188">You can use all of the valid passwords from your on-premises Active Directory instance to access Azure AD services.</span></span>

> [!NOTE]
> <span data-ttu-id="8f856-189">클라우드에서 직접 만든 사용자의 암호는 클라우드 내에서 정의된 암호 정책을 계속 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-189">Passwords for users that are created directly in the cloud are still subject to password policies as defined in the cloud.</span></span>

#### <a name="password-expiration-policy"></a><span data-ttu-id="8f856-190">암호 만료 정책</span><span class="sxs-lookup"><span data-stu-id="8f856-190">Password expiration policy</span></span>  
<span data-ttu-id="8f856-191">사용자가 암호 동기화 범위 내에 있을 경우 클라우드 계정 암호는 *사용 기간 제한 없음*으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-191">If a user is in the scope of password synchronization, the cloud account password is set to *Never Expire*.</span></span>

<span data-ttu-id="8f856-192">온-프레미스 환경에서 만료된 동기화된 암호를 사용하여 클라우드 서비스에 계속 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-192">You can continue to sign in to your cloud services by using a synchronized password that is expired in your on-premises environment.</span></span> <span data-ttu-id="8f856-193">클라우드 암호는 온-프레미스 환경에서 다음에 암호를 변경할 때 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-193">Your cloud password is updated the next time you change the password in the on-premises environment.</span></span>

#### <a name="account-expiration"></a><span data-ttu-id="8f856-194">계정 만료</span><span class="sxs-lookup"><span data-stu-id="8f856-194">Account expiration</span></span>
<span data-ttu-id="8f856-195">조직에서 사용자 계정 관리의 일환으로 accountExpires 특성을 사용하는 경우 이 특성이 Azure AD와 동기화되지 않는다는 점에 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-195">If your organization uses the accountExpires attribute as part of user account management, be aware that this attribute is not synchronized to Azure AD.</span></span> <span data-ttu-id="8f856-196">결과적으로 암호 동기화를 위해 구성된 환경의 만료된 Active Directory 계정은 Azure AD에서 계속 활성 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-196">As a result, an expired Active Directory account in an environment configured for password synchronization will still be active in Azure AD.</span></span> <span data-ttu-id="8f856-197">계정이 만료되면 워크플로 작업에서 사용자의 Azure AD 계정을 비활성화하는 PowerShell 스크립트를 트리거하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-197">We recommend that if the account is expired, a workflow action should trigger a PowerShell script that disables the user's Azure AD account.</span></span> <span data-ttu-id="8f856-198">반대로 계정이 켜지면 Azure AD 인스턴스도 켜져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-198">Conversely, when the account is turned on, the Azure AD instance should be turned on.</span></span>

### <a name="overwrite-synchronized-passwords"></a><span data-ttu-id="8f856-199">동기화된 암호 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="8f856-199">Overwrite synchronized passwords</span></span>
<span data-ttu-id="8f856-200">관리자는 Windows PowerShell을 사용하여 사용자 암호를 수동으로 재설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-200">An administrator can manually reset your password by using Windows PowerShell.</span></span>

<span data-ttu-id="8f856-201">이런 경우, 새 암호는 사용자의 동기화된 암호를 재정의하고 클라우드 내에 정의된 모든 암호 정책이 새 암호에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-201">In this case, the new password overrides your synchronized password, and all password policies defined in the cloud are applied to the new password.</span></span>

<span data-ttu-id="8f856-202">사용자가 온-프레미스 암호를 다시 변경하면, 새 암호는 클라우드에 동기화되며, 수동으로 업데이트한 암호를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-202">If you change your on-premises password again, the new password is synchronized to the cloud, and it overrides the manually updated password.</span></span>

<span data-ttu-id="8f856-203">암호 동기화는 로그인된 Azure 사용자에게 아무런 영향도 미치지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-203">The synchronization of a password has no impact on the Azure user who is signed in.</span></span> <span data-ttu-id="8f856-204">클라우드 서비스에 로그온해 있는 동안, 동기화된 암호가 변경되더라도 현재 클라우드 세션이 즉시 영향을 받지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-204">Your current cloud service session is not immediately affected by a synchronized password change that occurs while you're signed in to a cloud service.</span></span> <span data-ttu-id="8f856-205">KMSI는 이런 차이가 나는 기간을 연장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-205">KMSI extends the duration of this difference.</span></span> <span data-ttu-id="8f856-206">클라우드 서비스에서 다시 인증을 요구하면 새 암호를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-206">When the cloud service requires you to authenticate again, you need to provide your new password.</span></span>

### <a name="additional-advantages"></a><span data-ttu-id="8f856-207">추가적인 이점</span><span class="sxs-lookup"><span data-stu-id="8f856-207">Additional advantages</span></span>

- <span data-ttu-id="8f856-208">일반적으로 암호 동기화는 페더레이션 서비스보다 구현에 더 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-208">Generally, password synchronization is simpler to implement than a federation service.</span></span> <span data-ttu-id="8f856-209">추가 서버가 필요 없으며, 사용자를 인증하기 위해 고가용성의 페더레이션 서비스에 의존하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-209">It doesn't require any additional servers, and eliminates dependence on a highly available federation service to authenticate users.</span></span> 
- <span data-ttu-id="8f856-210">페더레이션 외에 암호 동기화를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-210">Password synchronization can also be enabled in addition to federation.</span></span> <span data-ttu-id="8f856-211">페더레이션 서비스에 중단이 발생하는 경우 대체 서비스로 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-211">It may be used as a fallback if your federation service experiences an outage.</span></span>












## <a name="enable-password-synchronization"></a><span data-ttu-id="8f856-212">암호 동기화 사용</span><span class="sxs-lookup"><span data-stu-id="8f856-212">Enable password synchronization</span></span>
<span data-ttu-id="8f856-213">**기본 설정** 옵션을 사용하여 Azure AD Connect를 설치할 경우 암호 동기화를 사용하도록 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-213">When you install Azure AD Connect by using the **Express Settings** option, password synchronization is automatically enabled.</span></span> <span data-ttu-id="8f856-214">자세한 내용은 [기본 설정을 사용하여 Azure AD Connect 시작](active-directory-aadconnect-get-started-express.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f856-214">For more details, see [Getting started with Azure AD Connect using express settings](active-directory-aadconnect-get-started-express.md).</span></span>

<span data-ttu-id="8f856-215">Azure AD Connect를 설치할 때 사용자 지정 설정을 사용하는 경우 사용자 로그인 페이지에서 암호 동기화를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-215">If you use custom settings when you install Azure AD Connect, password synchronization is available on the user sign-in page.</span></span> <span data-ttu-id="8f856-216">자세한 내용은 [Azure AD Connect의 사용자 지정 설치](active-directory-aadconnect-get-started-custom.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f856-216">For more details, see [Custom installation of Azure AD Connect](active-directory-aadconnect-get-started-custom.md).</span></span>

![암호 동기화를 사용하도록 설정](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a><span data-ttu-id="8f856-218">암호 동기화 및 FIPS</span><span class="sxs-lookup"><span data-stu-id="8f856-218">Password synchronization and FIPS</span></span>
<span data-ttu-id="8f856-219">서버가 FIPS(Federal Information Processing Standard)에 따라 잠긴 다음 MD5가 비활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-219">If your server has been locked down according to Federal Information Processing Standard (FIPS), then MD5 is disabled.</span></span>

<span data-ttu-id="8f856-220">**암호 동기화에 MD5를 사용하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="8f856-220">**To enable MD5 for password synchronization, perform the following steps:**</span></span>

1. <span data-ttu-id="8f856-221">%programfiles%\Azure AD Sync\Bin으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-221">Go to %programfiles%\Azure AD Sync\Bin.</span></span>
2. <span data-ttu-id="8f856-222">miiserver.exe.config를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-222">Open miiserver.exe.config.</span></span>
3. <span data-ttu-id="8f856-223">파일의 끝에서 구성/런타임 노드로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-223">Go to the configuration/runtime node at the end of the file.</span></span>
4. <span data-ttu-id="8f856-224">다음 노드를 추가 합니다. `<enforceFIPSPolicy enabled="false"/>`</span><span class="sxs-lookup"><span data-stu-id="8f856-224">Add the following node: `<enforceFIPSPolicy enabled="false"/>`</span></span>
5. <span data-ttu-id="8f856-225">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-225">Save your changes.</span></span>

<span data-ttu-id="8f856-226">참조용으로 다음 조각처럼 보여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f856-226">For reference, this snippet is what it should look like:</span></span>

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

<span data-ttu-id="8f856-227">보안 및 FIPS에 대한 자세한 내용은 [AAD 암호 동기화, 암호화 및 FIPS 준수](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f856-227">For information about security and FIPS, see [AAD Password Sync, encryption and FIPS compliance](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/).</span></span>

## <a name="troubleshoot-password-synchronization"></a><span data-ttu-id="8f856-228">암호 동기화 문제 해결</span><span class="sxs-lookup"><span data-stu-id="8f856-228">Troubleshoot password synchronization</span></span>
<span data-ttu-id="8f856-229">암호 동기화에 문제가 있으면 [암호 동기화 문제 해결](active-directory-aadconnectsync-troubleshoot-password-synchronization.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f856-229">If you have problems with password synchronization, see [Troubleshoot password synchronization](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f856-230">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f856-230">Next steps</span></span>
* [<span data-ttu-id="8f856-231">Azure AD Connect 동기화: 사용자 지정 동기화 옵션</span><span class="sxs-lookup"><span data-stu-id="8f856-231">Azure AD Connect sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="8f856-232">Azure Active Directory와 온-프레미스 ID 통합</span><span class="sxs-lookup"><span data-stu-id="8f856-232">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
