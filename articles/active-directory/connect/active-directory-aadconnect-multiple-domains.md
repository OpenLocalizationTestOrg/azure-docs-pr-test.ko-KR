---
title: "여러 도메인 aaaAzure AD 연결"
description: "이 문서에는 O365 및 Azure AD를 사용하여 여러 최상위 도메인을 설정하고 구성하는 방법이 설명되어 있습니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="828dd-103">Azure AD로 페더레이션에 대한 여러 도메인 지원</span><span class="sxs-lookup"><span data-stu-id="828dd-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="828dd-104">hello 다음 문서는 방법을 제공 toouse 여러 최상위 도메인 및 하위 도메인을 Office 365 또는 Azure AD 도메인을 페더레이션 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="828dd-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="828dd-105">여러 최상위 도메인 지원</span><span class="sxs-lookup"><span data-stu-id="828dd-105">Multiple top-level domain support</span></span>
<span data-ttu-id="828dd-106">Azure AD로 여러 최상위 도메인을 페더레이션하려면 하나의 최상위 도메인으로 페더레이션하는 경우 필요하지 않은 몇 가지 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="828dd-107">도메인은 Azure AD와 페더레이션 하는 경우 Azure의 hello 도메인에 여러 속성이 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="828dd-108">중요한 한가지 속성은 IssuerUri입니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="828dd-109">이 사용 되는 URI는 토큰 hello hello 도메인으로 Azure AD tooidentify와 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="828dd-110">hello URI tooresolve tooanything 필요 하지 않습니다 되지만 유효한 URI 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="828dd-111">기본적으로 Azure AD이 값을 설정 toohello hello 페더레이션 서비스 식별자의 온-프레미스에서 AD FS 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="828dd-112">hello 페더레이션 서비스 식별자는 페더레이션 서비스를 고유 하 게 식별 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="828dd-113">hello 페더레이션 서비스는 hello 보안 토큰 서비스와 AD FS에서 작동 하의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="828dd-114">Hello PowerShell 명령을 사용 하 여 자세한 IssuerUri 수 `Get-MsolDomainFederationSettings -DomainName <your domain>`합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="828dd-116">문제에는 여러 개의 최상위 도메인 tooadd 원하는 경우 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="828dd-117">예를 들어 Azure AD와 온-프레미스 환경 간 페더레이션을 설정했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="828dd-118">이 문서의 경우 bmcontoso.com을 사용합니다.  두 번째 최상위 도메인 bmfabrikam.com을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![도메인](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="828dd-120">회원님께 우리의 bmfabrikam.com 도메인 toobe 페더레이션 tooconvert 때에서는 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="828dd-121">hello 이유는 Azure AD에 hello IssuerUri 속성 toohave hello 같은 둘 이상의 도메인에 대 한 값을 허용 하지 않는 제약 조건이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![페더레이션 오류](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="828dd-123">SupportMultipleDomain 매개 변수</span><span class="sxs-lookup"><span data-stu-id="828dd-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="828dd-124">tooworkaround이 tooadd hello를 사용 하 여 변환을 수행할 수 있는 다른 IssuerUri 필요 `-SupportMultipleDomain` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="828dd-125">이 매개 변수는 cmdlet을 다음 hello로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="828dd-126">이 매개 변수는 hello 도메인의 hello 이름에 따라이 있도록 IssuerUri hello를 구성 하는 Azure AD를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="828dd-127">Azure AD의 디렉터리에서 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="828dd-128">Hello 매개 변수를 사용 하 여 hello PowerShell 명령 toocomplete를 성공적으로 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="828dd-130">새 bmfabrikam.com 도메인의 hello 설정을 있습니다 보고 hello 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="828dd-132">`-SupportMultipleDomain` hello 바뀌지 않으면 있는 다른 끝점 adfs.bmcontoso.com에서 여전히 toopoint tooour 페더레이션 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="828dd-133">또 다른 주의 사항은 `-SupportMultipleDomain` 않습니다는 hello AD FS 시스템에 Azure AD에 대 한 발급 된 토큰에서 적절 한 발급자 값 hello 포함 되도록 보장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="828dd-134">이렇게 하기 hello 사용자 UPN hello 도메인 부분을 가져오고이 hello IssuerUri, 즉, https://{upn 접미사의에서 hello 도메인으로 설정 하 여} / adfs/services/신뢰 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="828dd-135">따라서 인증 tooAzure AD 또는 Office 365 중 hello IssuerUri hello 사용자의 토큰 요소가 사용 되는 toolocate hello 도메인 Azure AD에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="828dd-136">일치 하는 항목이 없는 경우 hello 인증이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="828dd-137">예를 들어 사용자의 UPN를 bsimon@bmcontoso.com, toohttp://bmcontoso.com/adfs/services/trust hello IssuerUri 요소 hello 토큰 AD FS 문제에 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="828dd-138">Hello Azure AD 구성 일치시킬지 및 인증에 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="828dd-139">hello 다음은이 논리를 구현 하는 hello 사용자 지정된 클레임 규칙:</span><span class="sxs-lookup"><span data-stu-id="828dd-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="828dd-140">순서 toouse hello-SupportMultipleDomain 새 tooadd 시도할 때 전환 하거나 이미 변환 추가 도메인, toohave 해야 페더레이션된 트러스트 toosupport 설정으로 원래 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="828dd-141">AD FS와 Azure AD 간의 tooupdate hello 신뢰 하는 방법</span><span class="sxs-lookup"><span data-stu-id="828dd-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="828dd-142">Toore 해야 AD FS와 Azure AD의 사용자 인스턴스 간의 hello 페더레이션 트러스트를 설정 하지 않았을 경우-이 트러스트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="828dd-143">되었을 때 원래 hello 없이 설정 때문에 이것이 `-SupportMultipleDomain` 매개 변수를 hello IssuerUri hello 기본 값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="828dd-144">Hello에서 아래 스크린샷 hello IssuerUri toohttps://adfs.bmcontoso.com/adfs/services/trust 설정 되어 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="828dd-145">이제 hello Azure AD 포털에서 새 도메인을 성공적으로 추가 하 고 다음 tooconvert를 시도 하는 경우 사용 하 여 `Convert-MsolDomaintoFederated -DomainName <your domain>`를 얻을 수 있는 hello 다음 오류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="828dd-147">Tooadd hello를 시도 하면 `-SupportMultipleDomain` 스위치 hello 다음 오류가 수신 됩니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="828dd-149">Toorun 할지를 `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` hello에 원래 도메인에서 오류가 발생도 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="828dd-151">Tooadd 추가 최상위 도메인 아래 hello 단계를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="828dd-152">이미 도메인을 추가 하 고 hello를 사용 하지 않은 경우 `-SupportMultipleDomain` 매개 변수 제거 하 고 원래 도메인을 업데이트 하기 위한 hello 단계부터 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="828dd-153">최상위 도메인을 추가 하지 않은 경우 PowerShell의 Azure AD Connect를 사용 하 여 도메인을 추가 하는 단계 hello로 시작할 수 아직.</span><span class="sxs-lookup"><span data-stu-id="828dd-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="828dd-154">다음 단계 tooremove hello Microsoft Online 신뢰 hello를 사용 하 고 원래 도메인을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="828dd-155">AD FS 페더레이션 서버에서 **AD FS 관리**</span><span class="sxs-lookup"><span data-stu-id="828dd-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="828dd-156">Hello 왼쪽의 확장 **트러스트 관계** 및 **신뢰 당사자 트러스트**</span><span class="sxs-lookup"><span data-stu-id="828dd-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="828dd-157">오른쪽 hello에서 삭제 hello **Microsoft Office 365 Id 플랫폼** 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="828dd-158">![Microsoft 온라인 제거](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="828dd-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="828dd-159">가 있는 컴퓨터에서 [Azure Active Directory에 대 한 Windows PowerShell 모듈](https://msdn.microsoft.com/library/azure/jj151815.aspx) 설치 hello 다음 실행: `$cred=Get-Credential`합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="828dd-160">Hello Azure AD 도메인을 페더레이션 하는 hello 사용자 이름 및 전역 관리자의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="828dd-161">PowerShell에서 `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="828dd-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="828dd-162">PowerShell에서 `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="828dd-163">이 hello 원래 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-163">This is for hello original domain.</span></span>  <span data-ttu-id="828dd-164">따라서 hello를 사용 하 여는 것이 도메인 위에:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="828dd-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="828dd-165">다음 단계 tooadd hello 새 최상위 도메인 PowerShell을 사용 하 여 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="828dd-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="828dd-166">가 있는 컴퓨터에서 [Azure Active Directory에 대 한 Windows PowerShell 모듈](https://msdn.microsoft.com/library/azure/jj151815.aspx) 설치 hello 다음 실행: `$cred=Get-Credential`합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="828dd-167">Hello Azure AD 도메인을 페더레이션 하는 hello 사용자 이름 및 전역 관리자의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="828dd-168">PowerShell에서 `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="828dd-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="828dd-169">PowerShell에서 `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="828dd-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="828dd-170">다음 단계 tooadd hello 새 최상위 도메인 Azure AD Connect를 사용 하 여 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="828dd-171">시작 메뉴 또는 hello 바탕 화면에서 Azure AD Connect 시작</span><span class="sxs-lookup"><span data-stu-id="828dd-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="828dd-172">"추가 Azure AD 도메인 추가" 선택 ![추가 Azure AD 도메인 추가](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="828dd-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="828dd-173">Azure AD 및 Active Directory 자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="828dd-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="828dd-174">페더레이션에 대 한 tooconfigure 원하는 hello 두 번째 도메인을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="828dd-175">![추가 Azure AD 도메인 추가](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="828dd-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="828dd-176">설치 클릭</span><span class="sxs-lookup"><span data-stu-id="828dd-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="828dd-177">Hello 새 최상위 도메인 확인</span><span class="sxs-lookup"><span data-stu-id="828dd-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="828dd-178">Hello PowerShell 명령을 사용 하 여 `Get-MsolDomainFederationSettings -DomainName <your domain>`볼 수 있습니다 hello IssuerUri를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="828dd-179">hello 아래 스크린샷은 우리의 원래 도메인 http://bmcontoso.com/adfs/services/trust에 업데이트 된 hello 페더레이션 설정</span><span class="sxs-lookup"><span data-stu-id="828dd-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="828dd-181">새 도메인에서 IssuerUri hello toohttps://bmfabrikam.com/adfs/services/trust 설정 되었는지</span><span class="sxs-lookup"><span data-stu-id="828dd-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="828dd-183">하위 도메인에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="828dd-183">Support for Sub-domains</span></span>
<span data-ttu-id="828dd-184">하위 도메인을 추가 하면 hello 인해 방식으로 Azure AD 처리 도메인, 일부 알림의 hello 상위 hello 설정을 상속 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="828dd-185">즉, 해당 hello IssuerUri toomatch hello 부모 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="828dd-186">따라서 예를 들어 bmcontoso.com이 있고 corp.bmcontoso.com을 추가한다고 가정합니다.  즉, 해당 hello IssuerUri corp.bmcontoso.com에서 필요성이 toobe에 대 한 **http://bmcontoso.com/adfs/services/trust 합니다.**</span><span class="sxs-lookup"><span data-stu-id="828dd-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="828dd-187">하지만 Azure AD에 대 한 위의 hello 표준 규칙 구현으로 발급자와 토큰을 생성 합니다 **http://corp.bmcontoso.com/adfs/services/trust 합니다.**</span><span class="sxs-lookup"><span data-stu-id="828dd-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="828dd-188">hello 도메인의 필수 값 일치 하지는 않으며 인증이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="828dd-189">하위 도메인에 대 한 tooenable를 지 원하는 방법</span><span class="sxs-lookup"><span data-stu-id="828dd-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="828dd-190">이 hello 주위 순서 toowork AD FS 신뢰 당사자 트러스트에 대 한 Microsoft Online toobe 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="828dd-191">toodo이 hello 사용자 지정 하는 발급자 값을 생성할 때 모든 하위 도메인에서 hello 사용자의 UPN 접미사를 제거 하는 것을 사용자 지정 클레임 규칙을 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="828dd-192">hello 클레임 다음이 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="828dd-193">hello 정규식의 마지막 번호 hello hello 루트 도메인에 부모 도메인을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="828dd-194">여기서 bmcontoso.com이 있으므로 2개의 상위 도메인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="828dd-195">도메인 상위 3 개의 toobe 유지 된 경우 (즉,: corp.bmcontoso.com), hello 수 있었을 세 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="828dd-196">Eventualy 범위를 표시할 수 있습니다 하는 경우 일치 하는 hello toomatch hello 최대값인 도메인 수행 항상 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="828dd-197">"{" (2, 3} 두 toothree 도메인 일치 합니다 (예:: bmfabrikam.com 및 corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="828dd-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="828dd-198">다음 단계 tooadd hello 사용자 지정 클레임 toosupport 하위 도메인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="828dd-199">AD FS 관리 열기</span><span class="sxs-lookup"><span data-stu-id="828dd-199">Open AD FS Management</span></span>
2. <span data-ttu-id="828dd-200">Microsoft 온라인 RP trust hello를 마우스 오른쪽 단추로 클릭 하 고 편집 하는 클레임 규칙 선택</span><span class="sxs-lookup"><span data-stu-id="828dd-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="828dd-201">Hello 세 번째 클레임 규칙을 선택 하 고 대체 ![편집 클레임](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="828dd-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="828dd-202">Hello 현재 클레임을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![클레임 바꾸기](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="828dd-204">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-204">Click Ok.</span></span>  <span data-ttu-id="828dd-205">적용을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-205">Click Apply.</span></span>  <span data-ttu-id="828dd-206">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-206">Click Ok.</span></span>  <span data-ttu-id="828dd-207">AD FS 관리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="828dd-207">Close AD FS Management.</span></span>

