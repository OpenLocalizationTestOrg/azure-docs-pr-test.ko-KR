---
title: "Azure AD Connect 복수 도메인"
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
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="91640-103">Azure AD로 페더레이션에 대한 여러 도메인 지원</span><span class="sxs-lookup"><span data-stu-id="91640-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="91640-104">다음 설명서에서는 Office 365 또는 Azure AD 도메인으로 페더레이션하는 경우 여러 최상위 도메인 및 하위 도메인을 사용하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="91640-105">여러 최상위 도메인 지원</span><span class="sxs-lookup"><span data-stu-id="91640-105">Multiple top-level domain support</span></span>
<span data-ttu-id="91640-106">Azure AD로 여러 최상위 도메인을 페더레이션하려면 하나의 최상위 도메인으로 페더레이션하는 경우 필요하지 않은 몇 가지 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="91640-107">도메인이 Azure AD로 페더레이션되는 경우 Azure의 도메인에서 여러 속성이 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="91640-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="91640-108">중요한 한가지 속성은 IssuerUri입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="91640-109">Azure AD에서 토큰이 연결된 도메인을 식별하는 데 사용되는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="91640-110">URI는 아무 것도 확인할 필요가 없지만 유효한 URI여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="91640-111">기본적으로 Azure AD는 이 값을 온-프레미스 AD FS 구성에서 페더레이션 서비스 식별자의 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="91640-112">페더레이션 서비스 식별자는 페더레이션 서비스를 고유하게 식별하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="91640-113">페더레이션 서비스는 보안 토큰 서비스로 작동하는 AD FS의 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="91640-114">PowerShell 명령 `Get-MsolDomainFederationSettings -DomainName <your domain>`을(를) 사용하여 IssuerUri를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="91640-116">두 개 이상의 최상위 도메인을 추가하려는 경우에 문제가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="91640-117">예를 들어 Azure AD와 온-프레미스 환경 간 페더레이션을 설정했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="91640-118">이 문서의 경우 bmcontoso.com을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="91640-119">두 번째 최상위 도메인 bmfabrikam.com을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![도메인](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="91640-121">bmfabrikam.com 도메인을 페더레이션되도록 변환할 때 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="91640-122">Azure AD가 IssuerURI 속성에서 둘 이상의 도메인에 같은 값을 허용하지 않는 제약 조건을 갖는 것이 이에 대한 이유입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![페더레이션 오류](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="91640-124">SupportMultipleDomain 매개 변수</span><span class="sxs-lookup"><span data-stu-id="91640-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="91640-125">이 문제를 해결하려면 `-SupportMultipleDomain` 매개 변수를 사용하여 수행할 수 있는 다른 IssuerUri를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="91640-126">이 매개 변수는 다음 cmdlet과 함께 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91640-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="91640-127">이 매개 변수를 사용하면 Azure AD가 도메인의 이름에 기반하도록 IssuerUri를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="91640-128">Azure AD의 디렉터리에서 고유합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="91640-129">매개 변수를 사용하여 PowerShell 명령을 성공적으로 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="91640-131">새 bmfabrikam.com 도메인의 설정을 보면 다음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="91640-133">`-SupportMultipleDomain` 은(는) 여전히 adfs.bmcontoso.com의 페더레이션 서비스를 가리키도록 구성된 다른 끝점을 변경하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="91640-134">`-SupportMultipleDomain` 이(가) 수행하는 다른 작업은 AD FS 시스템이 Azure AD에 대해 발급된 토큰에 적절한 발급자 값을 포함하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="91640-135">사용자 UPN의 도메인 부분을 가져오거나 issuerURI 즉, https://{upn suffix}/adfs/services/trust의 도메인으로 이를 설정하여 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="91640-136">따라서 Azure AD 또는 Office 365에 인증하는 동안 사용자 토큰의 IssuerUri 요소는 Azure AD에서 도메인을 찾는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="91640-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="91640-137">일치하는 항목이 없는 경우 인증이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="91640-138">예를 들어 사용자의 UPN를 bsimon@bmcontoso.com, 토큰 AD FS 문제에서 IssuerUri 요소 http://bmcontoso.com/adfs/services/trust로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="91640-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="91640-139">이는 Azure AD 구성에 일치하며 인증이 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="91640-140">다음은 이 논리를 구현하는 사용자 지정된 클레임 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="91640-141">새 것을 추가하거나 이미 추가된 도메인을 변환하려고 하는 경우 SupportMultipleDomain 스위치를 사용하려면 원래 지원하도록 페더레이션된 트러스트를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="91640-142">AD FS와 Azure AD 간의 트러스트를 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="91640-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="91640-143">AD FS와 Azure AD의 인스턴스 간의 페더레이션된 트러스트를 설정하지 않았을 경우 이 트러스트를 다시 만들어야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="91640-144">이는 `-SupportMultipleDomain` 매개 변수 없이 원래 설치될 때 IssuerUri가 기본 값으로 설정되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="91640-145">아래 스크린샷에서는 IssuerUri가 https://adfs.bmcontoso.com/adfs/services/trust로 설정된 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="91640-146">따라서 이제 Azure AD 포털에 새 도메인을 성공적으로 추가한 다음 `Convert-MsolDomaintoFederated -DomainName <your domain>`을(를) 사용하여 변환하려고 하는 경우 다음과 같은 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="91640-148">`-SupportMultipleDomain` 스위치를 추가하려는 경우 다음 오류를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="91640-150">원본 도메인에서 `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` 을(를) 실행하려고 하면 또한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![페더레이션 오류](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="91640-152">아래 단계를 사용하여 추가 최상위 도메인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="91640-153">이미 도메인을 추가하고 `-SupportMultipleDomain` 매개 변수를 사용하지 않은 경우 원본 도메인 제거 및 업데이트에 대한 단계를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="91640-154">최상위 도메인을 아직 추가하지 않은 경우 Azure AD Connect의 PowerShell을 사용하여 도메인을 추가하기 위한 단계를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="91640-155">다음 단계를 사용하여 Microsoft Online 트러스트를 제거하고 원본 도메인을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="91640-156">AD FS 페더레이션 서버에서 **AD FS 관리**</span><span class="sxs-lookup"><span data-stu-id="91640-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="91640-157">왼쪽에서 **트러스트 관계** 및 **신뢰 당사자 트러스트**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="91640-158">오른쪽에서 **Microsoft Office 365 ID 플랫폼** 항목을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="91640-159">![Microsoft 온라인 제거](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="91640-159">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="91640-160">[Windows PowerShell용 Azure Active Directory 모듈](https://msdn.microsoft.com/library/azure/jj151815.aspx)이 설치된 컴퓨터에서 `$cred=Get-Credential`을(를) 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="91640-161">페더레이션하는 Azure AD 도메인에 대한 전역 관리자의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="91640-162">PowerShell에서 `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="91640-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="91640-163">PowerShell에서 `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`을(를) 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="91640-164">원본 도메인에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-164">This is for the original domain.</span></span>  <span data-ttu-id="91640-165">따라서 위의 도메인을 사용하는 것은 `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="91640-166">PowerShell을 사용하여 새 최상위 도메인을 추가하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="91640-167">[Windows PowerShell용 Azure Active Directory 모듈](https://msdn.microsoft.com/library/azure/jj151815.aspx)이 설치된 컴퓨터에서 `$cred=Get-Credential`을(를) 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="91640-168">페더레이션하는 Azure AD 도메인에 대한 전역 관리자의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="91640-169">PowerShell에서 `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="91640-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="91640-170">PowerShell에서 `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="91640-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="91640-171">Azure AD Connect를 사용하여 새 최상위 도메인을 추가하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="91640-172">바탕 화면 또는 시작 메뉴에서 Azure AD Connect 시작</span><span class="sxs-lookup"><span data-stu-id="91640-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="91640-173">"추가 Azure AD 도메인 추가" 선택 ![추가 Azure AD 도메인 추가](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="91640-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="91640-174">Azure AD 및 Active Directory 자격 증명 입력</span><span class="sxs-lookup"><span data-stu-id="91640-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="91640-175">페더레이션에 대해 구성하려는 두 번째 도메인을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="91640-176">![추가 Azure AD 도메인 추가](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="91640-176">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="91640-177">설치 클릭</span><span class="sxs-lookup"><span data-stu-id="91640-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="91640-178">새 최상위 도메인 확인</span><span class="sxs-lookup"><span data-stu-id="91640-178">Verify the new top-level domain</span></span>
<span data-ttu-id="91640-179">PowerShell 명령을 사용하여 `Get-MsolDomainFederationSettings -DomainName <your domain>`업데이트된 IssuerUri를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="91640-180">아래 스크린샷은 페더레이션 설정이 원본 도메인 http://bmcontoso.com/adfs/services/trust에 업데이트된 것을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="91640-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="91640-182">새 도메인의 IssuerUri가 https://bmfabrikam.com/adfs/services/trust에 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="91640-184">하위 도메인에 대한 지원</span><span class="sxs-lookup"><span data-stu-id="91640-184">Support for Sub-domains</span></span>
<span data-ttu-id="91640-185">하위 도메인을 추가할 때 Azure AD가 도메인을 처리하는 방식으로 인해 부모의 설정을 상속합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="91640-186">이는 IssuerUri가 부모와 일치해야 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="91640-187">따라서 예를 들어 bmcontoso.com이 있고 corp.bmcontoso.com을 추가한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="91640-188">즉, corp.bmcontoso.com의 사용자를 위한 IssuerUri는 **http://bmcontoso.com/adfs/services/trust**가 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="91640-189">하지만 Azure AD에 대해 위에서 구현 표준 규칙은 **http://corp.bmcontoso.com/adfs/services/trust**와 같은 발급자를 통해 토큰을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="91640-190">로 발급자를 사용하여 토큰을 생성하고 인증에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="91640-191">하위 도메인에 대한 지원을 활성화하는 방법</span><span class="sxs-lookup"><span data-stu-id="91640-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="91640-192">이를 해결하기 위해 Microsoft 온라인에 대한 AD FS 신뢰 당사자 트러스트를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="91640-193">이를 위해 사용자 지정 클레임 규칙이 사용자 지정 발급자 값을 생성할 때 사용자의 UPN 접미사에서 모든 하위 도메인을 제거하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="91640-194">다음 클레임이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="91640-195">정규식에서 마지막 숫자는 루트 도메인에 있는 상위 도메인 수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="91640-196">여기서 bmcontoso.com이 있으므로 2개의 상위 도메인이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="91640-197">3개의 상위 도메인을 유지해야 한다면(예: corp.bmcontoso.com) 숫자는 3이 되었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="91640-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="91640-198">결과적으로 범위를 나타낼 수 있으며, 항상 최대 도메인 수와 일치하도록 매칭됩니다.</span><span class="sxs-lookup"><span data-stu-id="91640-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="91640-199">"{2,3}"은 2~3개의 도메인(예: bmfabrikam.com 및 corp.bmcontoso.com)이 매칭됩니다.</span><span class="sxs-lookup"><span data-stu-id="91640-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="91640-200">하위 도메인을 지원하기 위해 사용자 지정 클레임을 추가하려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="91640-201">AD FS 관리 열기</span><span class="sxs-lookup"><span data-stu-id="91640-201">Open AD FS Management</span></span>
2. <span data-ttu-id="91640-202">Microsoft 온라인 RP 트러스트를 마우스 오른쪽 단추로 클릭하고 편집 클레임 규칙 선택</span><span class="sxs-lookup"><span data-stu-id="91640-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="91640-203">세 번째 클레임 규칙을 선택하고 ![클레임 편집](./media/active-directory-multiple-domains/sub1.png) 대체</span><span class="sxs-lookup"><span data-stu-id="91640-203">Select the third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="91640-204">현재 클레임을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="91640-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![클레임 바꾸기](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="91640-206">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-206">Click Ok.</span></span>  <span data-ttu-id="91640-207">적용을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-207">Click Apply.</span></span>  <span data-ttu-id="91640-208">확인을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="91640-208">Click Ok.</span></span>  <span data-ttu-id="91640-209">AD FS 관리를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="91640-209">Close AD FS Management.</span></span>

