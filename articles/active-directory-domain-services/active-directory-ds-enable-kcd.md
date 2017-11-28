---
title: "Azure Active Directory Domain Services: Kerberos 제한 위임 활성화 | Microsoft Docs"
description: "Azure Active Directory Domain Services 관리되는 도메인에서 Kerberos 제한 위임 활성화"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a><span data-ttu-id="c07e2-103">관리되는 도메인에서 Kerberos 제한 위임(KCD) 구성</span><span class="sxs-lookup"><span data-stu-id="c07e2-103">Configure kerberos constrained delegation (KCD) on a managed domain</span></span>
<span data-ttu-id="c07e2-104">대부분의 응용 프로그램에는 hello 사용자의 hello 컨텍스트에서 tooaccess 리소스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-104">Many applications need tooaccess resources in hello context of hello user.</span></span> <span data-ttu-id="c07e2-105">Active Directory는 이 사용 사례가 가능한 Kerberos 위임이라고 하는 메커니즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-105">Active Directory supports a mechanism called Kerberos delegation, which enables this use-case.</span></span> <span data-ttu-id="c07e2-106">또한 hello 사용자의 hello 컨텍스트에서 특정 리소스에 액세스할 수 있도록 위임을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-106">Further, you can restrict delegation so that only specific resources can be accessed in hello context of hello user.</span></span> <span data-ttu-id="c07e2-107">Azure AD Domain Services 관리되는 도메인은 더 안전하게 잠겨 있으므로 기존의 Active Directory 도메인과는 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-107">Azure AD Domain Services managed domains are different from traditional Active Directory domains since they are more securely locked down.</span></span>

<span data-ttu-id="c07e2-108">이 문서에서는 tooconfigure kerberos 제한 된 하는 Azure AD 도메인 서비스 관리 되는 도메인에 위임 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-108">This article shows you how tooconfigure kerberos constrained delegation on an Azure AD Domain Services managed domain.</span></span>

## <a name="kerberos-constrained-delegation-kcd"></a><span data-ttu-id="c07e2-109">Kerberos 제한 위임(KCD)</span><span class="sxs-lookup"><span data-stu-id="c07e2-109">Kerberos constrained delegation (KCD)</span></span>
<span data-ttu-id="c07e2-110">Kerberos 위임 계정 tooimpersonate 다른 보안 주체 (사용자)와 같은 tooaccess 리소스가 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-110">Kerberos delegation enables an account tooimpersonate another security principal (such as a user) tooaccess resources.</span></span> <span data-ttu-id="c07e2-111">웹 응용 프로그램을 사용자의 hello 컨텍스트에서 백 엔드 웹 API에 액세스 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-111">Consider a web application that accesses a back-end web API in hello context of a user.</span></span> <span data-ttu-id="c07e2-112">이 예제에서는 hello (hello 컨텍스트의 서비스 계정 또는 컴퓨터/시스템 계정에서 실행) 하는 웹 응용 프로그램 사용자를 가장 hello hello 리소스 (백 엔드 웹 API)에 액세스할 때.</span><span class="sxs-lookup"><span data-stu-id="c07e2-112">In this example, hello web application (running in hello context of a service account or a computer/machine account) impersonates hello user when accessing hello resource (back-end web API).</span></span> <span data-ttu-id="c07e2-113">Kerberos 위임을 안전 하지 않으므로 hello 계정을 가장 하는 리소스 hello hello 사용자의 hello 컨텍스트에서 액세스할 수를 제한 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-113">Kerberos delegation is insecure since it does not restrict hello resources hello impersonating account can access in hello context of hello user.</span></span>

<span data-ttu-id="c07e2-114">Kerberos 제한 위임 KCD ()는 서비스/리소스 toowhich hello에 대 한 지정된 서버 hello 사용자를 대신 하 여 작업할 수 있는 hello를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-114">Kerberos constrained delegation (KCD) restricts hello services/resources toowhich hello specified server can act on hello behalf of a user.</span></span> <span data-ttu-id="c07e2-115">기존의 KCD는 서비스에 대 한 도메인 관리자 권한이 tooconfigure 도메인 계정에 필요 하 고 hello 계정 tooa 단일 도메인을 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-115">Traditional KCD requires domain administrator privileges tooconfigure a domain account for a service and it restricts hello account tooa single domain.</span></span>

<span data-ttu-id="c07e2-116">또한 기존의 KCD에는 이것과 관련된 몇 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-116">Traditional KCD also has a few issues associated with it.</span></span> <span data-ttu-id="c07e2-117">도메인 관리자에 게 hello 서비스를 구성한 이전 운영 체제, 서비스 관리자에 게 없는 유용한 방법은 tooknow 되는 프런트 엔드 서비스 이들이 소유 toohello 리소스 서비스로 위임 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-117">In earlier operating systems where hello domain administrator configured hello service, hello service administrator had no useful way tooknow which front-end services delegated toohello resource services they owned.</span></span> <span data-ttu-id="c07e2-118">와 tooa 리소스 서비스로 위임 될 수 있는 프런트 엔드 서비스에 잠재적 공격 지점이 표현 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-118">And any front-end service that could delegate tooa resource service represented a potential attack point.</span></span> <span data-ttu-id="c07e2-119">프런트 엔드 서비스를 호스팅하는 서버의 보안이 손상 된, 되었으며 구성된 toodelegate tooresource 서비스 하는 경우 리소스 서비스 hello도 손상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-119">If a server that hosted a front-end service was compromised, and it was configured toodelegate tooresource services, hello resource services could also be compromised.</span></span>

> [!NOTE]
> <span data-ttu-id="c07e2-120">Azure AD Domain Services 관리되는 도메인에서 도메인 관리자 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-120">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="c07e2-121">따라서 **관리되는 도메인에 기존 KCD를 구성할 수 없습니다**.</span><span class="sxs-lookup"><span data-stu-id="c07e2-121">Therefore, **traditional KCD cannot be configured on a managed domain**.</span></span> <span data-ttu-id="c07e2-122">이 문서에 설명된 대로 리소스 기반 KCD를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-122">Use resource-based KCD as described in this article.</span></span> <span data-ttu-id="c07e2-123">또한 이 메커니즘은 더 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-123">This mechanism is also more secure.</span></span>
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a><span data-ttu-id="c07e2-124">리소스 기반 Kerberos 제한 위임</span><span class="sxs-lookup"><span data-stu-id="c07e2-124">Resource-based kerberos constrained delegation</span></span>
<span data-ttu-id="c07e2-125">Windows Server 2012 R2 및 Windows Server 2012의 hello 서비스에 대 한 hello 기능 tooconfigure 제한 된 위임에서 도메인 관리자 toohello 서비스 관리자에 게 이전 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-125">In Windows Server 2012 R2 and Windows Server 2012, hello ability tooconfigure constrained delegation for hello service has been transferred from hello domain administrator toohello service administrator.</span></span> <span data-ttu-id="c07e2-126">이러한 방식으로 백 엔드 서비스 관리자에 게 허용 하거나 프런트 엔드 서비스를 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-126">In this way, hello back-end service administrator can allow or deny front-end services.</span></span> <span data-ttu-id="c07e2-127">이 모델은 **리소스 기반 Kerberos 제한 위임**으로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-127">This model is known as **resource-based kerberos constrained delegation**.</span></span>

<span data-ttu-id="c07e2-128">리소스 기반 KCD는 PowerShell을 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-128">Resource-based KCD is configured using PowerShell.</span></span> <span data-ttu-id="c07e2-129">Hello Set-adcomputer 또는 컴퓨터 계정이 나 사용자 계정/서비스 계정의 계정을 가장 하는 hello 인지에 따라 Set-aduser cmdlet를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-129">You use hello Set-ADComputer or Set-ADUser cmdlets, depending on whether hello impersonating account is a computer account or a user account/service account.</span></span>

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a><span data-ttu-id="c07e2-130">관리되는 도메인에서 컴퓨터 계정에 대한 리소스 기반 KCD 구성</span><span class="sxs-lookup"><span data-stu-id="c07e2-130">Configure resource-based KCD for a computer account on a managed domain</span></span>
<span data-ttu-id="c07e2-131">Hello 컴퓨터에서 실행 되는 웹 응용 프로그램 사용 한다고 가정 ' contoso100-webapp.contoso100.com'.</span><span class="sxs-lookup"><span data-stu-id="c07e2-131">Assume you have a web app running on hello computer 'contoso100-webapp.contoso100.com'.</span></span> <span data-ttu-id="c07e2-132">필요한 tooaccess hello 리소스 (에서 실행 되는 web API ' contoso100-api.contoso100.com') 도메인 사용자의 hello 컨텍스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-132">It needs tooaccess hello resource (a web API running on 'contoso100-api.contoso100.com') in hello context of domain users.</span></span> <span data-ttu-id="c07e2-133">이 시나리오에서 리소스 기반 KCD를 설정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-133">Here's how you would set up resource-based KCD for this scenario.</span></span>

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a><span data-ttu-id="c07e2-134">관리되는 도메인에서 사용자 계정에 대한 리소스 기반 KCD 구성</span><span class="sxs-lookup"><span data-stu-id="c07e2-134">Configure resource-based KCD for a user account on a managed domain</span></span>
<span data-ttu-id="c07e2-135">서비스 계정 'appsvc'으로 실행 되는 웹 앱이 있는 도메인 사용자의 hello 컨텍스트에서 tooaccess hello 리소스 ('backendsvc'-서비스 계정으로 실행 하는 웹 API) 필요한 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-135">Assume you have a web app running as a service account 'appsvc' and it needs tooaccess hello resource (a web API running as a service account - 'backendsvc') in hello context of domain users.</span></span> <span data-ttu-id="c07e2-136">이 시나리오에서 리소스 기반 KCD를 설정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c07e2-136">Here's how you would set up resource-based KCD for this scenario.</span></span>

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a><span data-ttu-id="c07e2-137">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="c07e2-137">Related Content</span></span>
* [<span data-ttu-id="c07e2-138">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="c07e2-138">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="c07e2-139">Kerberos 제한 위임 개요</span><span class="sxs-lookup"><span data-stu-id="c07e2-139">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
