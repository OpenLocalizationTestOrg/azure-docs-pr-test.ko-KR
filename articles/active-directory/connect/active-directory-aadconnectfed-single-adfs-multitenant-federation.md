---
title: "단일 AD FS를 사용하여 여러 Azure AD를 페더레이션 | Microsoft Docs"
description: "이 문서에서는 하나의 AD FS를 통해 Azure AD를 페더레이션하는 방법에 대해 설명합니다."
keywords: "페더레이션, ADFS, AD FS, 다중 테넌트, 단일 AD FS, 단일 ADFS, 다중 테넌트 페더레이션, 다중 포리스트 ADFS, AAD 연결, 페더레이션, 테넌트 간 페더레이션"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 436bf5905d2b203dc4cceea97f4fb90593df7111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="e628b-104">AD FS의 단일 인스턴스를 사용하여 Azure AD의 여러 인스턴스를 페더레이션</span><span class="sxs-lookup"><span data-stu-id="e628b-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="e628b-105">양방향 트러스트가 있는 경우 하나의 고가용성 AD FS 팜에서 여러 포리스트를 페더레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="e628b-106">이러한 다중 포리스트는 동일한 Azure Active Directory에 해당하거나 그렇지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-106">These multiple forests may or may not correspond to the same Azure Active Directory.</span></span> <span data-ttu-id="e628b-107">이 문서에서는 단일 AD FS 배포와 다른 Azure AD에서 동기화하는 둘 이상의 포리스트 간에 페더레이션을 구성하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-107">This article provides instructions on how to configure federation between a single AD FS deployment and more than one forests that sync to different Azure AD.</span></span>

![단일 AD FS로 다중 테넌트 페더레이션](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="e628b-109">이 시나리오에서는 장치 쓰기 저장 및 자동 장치 연결이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="e628b-110">Azure AD Connect는 단일 Azure AD에서 도메인에 대한 페더레이션을 구성할 수 있으므로 이 시나리오에서 페더레이션을 구성하는 데 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-110">Azure AD Connect cannot be used to configure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="e628b-111">여러 Azure AD를 사용하여 AD FS를 페더레이션하는 단계</span><span class="sxs-lookup"><span data-stu-id="e628b-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="e628b-112">contoso.onmicrosoft.com Azure Active Directory의 contoso.com 도메인은 이미 contoso.com 온-프레미스 Active Directory 환경에 설치된 AD FS 온-프레미스와 통합되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with the AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="e628b-113">fabrikam.com은 fabrikam.onmicrosoft.com Azure Active Directory의 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="e628b-114">1단계: 양방향 트러스트 설정</span><span class="sxs-lookup"><span data-stu-id="e628b-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="e628b-115">contoso.com의 AD FS가 fabrikam.com에서 사용자를 인증하려면 contoso.com과 fabrikam.com 간에 양방향 트러스트 관계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-115">For AD FS in contoso.com to be able to authenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com.</span></span> <span data-ttu-id="e628b-116">이 [문서](https://technet.microsoft.com/library/cc816590.aspx)의 지침에 따라 양방향 트러스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-116">Follow the guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) to create the two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="e628b-117">2단계: contoso.com 페더레이션 설정 수정</span><span class="sxs-lookup"><span data-stu-id="e628b-117">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="e628b-118">AD FS에 페더레이션된 단일 도메인에 대해 설정되는 기본 발급자는 "http://ADFSServiceFQDN/adfs/services/trust"입니다(예: "http://fs.contoso.com/adfs/services/trust").</span><span class="sxs-lookup"><span data-stu-id="e628b-118">The default issuer set for a single domain federated to AD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="e628b-119">Azure Active Directory에는 각 페더레이션 도메인마다 고유한 발급자가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-119">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="e628b-120">동일한 AD FS에서 두 도메인을 페더레이션하므로 Azure Active Directory와 페더레이션하는 각 도메인 AD FS에 대해 고유하도록 발급자 값을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-120">Since the same AD FS is going to federate two domains, the issuer value needs to be modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="e628b-121">AD FS 서버에서 Azure AD PowerShell을 열고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-121">On the AD FS server, open Azure AD PowerShell and perform the following steps:</span></span>
 
<span data-ttu-id="e628b-122">contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain에 대한 페더레이션 설정인 contoso.com 도메인 Connect-MsolService Update가 포함된 Azure Active Directory에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-122">Connect to the Azure Active Directory that contains the domain contoso.com Connect-MsolService Update the federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="e628b-123">도메인 페더레이션 설정의 발급자가 "http://contoso.com/adfs/services/trust"로 변경되고, Azure AD 신뢰 당사자 트러스트에서 UPN 접미사를 기반으로 하는 올바른 issuerId 값을 발급하도록 발급 클레임 규칙이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-123">Issuer in the domain federation setting will be changed to "http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for the Azure AD Relying Party Trust to issue the correct issuerId value based on the UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="e628b-124">3단계: AD FS로 fabrikam.com 페더레이션</span><span class="sxs-lookup"><span data-stu-id="e628b-124">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="e628b-125">Azure AD PowerShell 세션에서 다음 단계를 수행합니다. fabrikam.com 도메인이 포함된 Azure Active Directory에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-125">In Azure AD powershell session perform the following steps: Connect to Azure Active Directory that contains the domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="e628b-126">fabrikam.com 관리되는 도메인을 페더레이션된 도메인으로 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-126">Convert the fabrikam.com managed domain to federated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="e628b-127">위의 작업에서는 동일한 AD FS를 통해 fabrikam.com 도메인을 페더레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-127">The above operation will federate the domain fabrikam.com with the same AD FS.</span></span> <span data-ttu-id="e628b-128">두 도메인 모두에 대해 Get-MsolDomainFederationSettings를 사용하여 도메인 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e628b-128">You can verify the domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e628b-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e628b-129">Next steps</span></span>
[<span data-ttu-id="e628b-130">Active Directory와 Azure Active Directory 연결</span><span class="sxs-lookup"><span data-stu-id="e628b-130">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
