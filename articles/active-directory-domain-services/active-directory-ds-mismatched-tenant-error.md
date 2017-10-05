---
title: "기존 Azure AD Domain Services로 관리되는 도메인의 디렉터리 불일치 오류 해결 | Microsoft Docs"
description: "기존 Azure AD Domain Services로 관리되는 도메인의 디렉터리 불일치 문제 이해 및 해결"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 40eb75b7-827e-4d30-af6c-ca3c2af915c7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: 
ms.date: 07/06/2017
ms.author: maheshu
ms.openlocfilehash: ca9ff29f5f91b8d796a29706ab49a82e417d1ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="resolve-mismatched-directory-errors-for-existing-azure-ad-domain-services-managed-domains"></a><span data-ttu-id="f3b41-103">기존 Azure AD Domain Services로 관리되는 도메인의 디렉터리 불일치 문제 해결</span><span class="sxs-lookup"><span data-stu-id="f3b41-103">Resolve mismatched directory errors for existing Azure AD Domain Services managed domains</span></span>
<span data-ttu-id="f3b41-104">Azure 클래식 포털을 사용하여 활성화된 기존의 관리되는 도메인이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-104">You have an existing managed domain that was enabled using the Azure classic portal.</span></span> <span data-ttu-id="f3b41-105">새 Azure Portal로 이동하여 관리되는 도메인을 확인할 때 다음 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-105">When you navigate to the new Azure portal and view the managed domain, you see the following error message:</span></span>

![디렉터리 불일치 오류](.\media\getting-started\mismatched-tenant-error.png)

<span data-ttu-id="f3b41-107">오류가 해결될 때까지 이 관리되는 도메인을 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-107">You cannot administer this managed domain until the error is resolved.</span></span>


## <a name="whats-causing-this-error"></a><span data-ttu-id="f3b41-108">이 오류의 원인</span><span class="sxs-lookup"><span data-stu-id="f3b41-108">What's causing this error?</span></span>
<span data-ttu-id="f3b41-109">이 오류는 관리되는 도메인과 해당 항목이 활성화된 가상 네트워크가 서로 다른 두 Azure AD 테넌트에 속할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-109">This error is caused when your managed domain and the virtual network it is enabled in belong to two different Azure AD tenants.</span></span> <span data-ttu-id="f3b41-110">예를 들어 'contoso.com'이라는 관리되는 도메인이 Contoso의 Azure AD 테넌트에서 활성화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-110">For example, you have a managed domain called 'contoso.com' and it was enabled for Contoso's Azure AD tenant.</span></span> <span data-ttu-id="f3b41-111">그러나 관리되는 도메인이 활성화된 Azure 가상 네트워크는 다른 Azure AD 테넌트인 Fabrikam에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-111">However, the Azure virtual network in which the managed domain was enabled belongs to Fabrikam - a different Azure AD tenant.</span></span>

<span data-ttu-id="f3b41-112">새 Azure Portal(및 특히 Azure AD Domain Services 확장)은 Azure Resource Manager에서 구축됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-112">The new Azure portal (and specifically the Azure AD Domain Services extension) is built on Azure Resource Manager.</span></span> <span data-ttu-id="f3b41-113">최신 Azure Resource Manager 환경에서는 보안을 높이고 역할 기반 액세스 제어(RBAC)를 리소스에 적용하기 위해 특정 제한이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-113">In the modern Azure Resource Manager environment, certain restrictions are enforced to deliver greater security and for roles-based access control (RBAC) to resources.</span></span> <span data-ttu-id="f3b41-114">Azure AD 테넌트에 Azure AD Domain Services를 활성화하는 것은 관리되는 도메인에 자격 증명 해시가 동기화되기 때문에 중요한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-114">Enabling Azure AD Domain Services for an Azure AD tenant is a sensitive operation since it causes credential hashes to be synchronized to the managed domain.</span></span> <span data-ttu-id="f3b41-115">이 작업을 위해서는 사용자가 디렉터리의 테넌트 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-115">This operation requires you to be a tenant admin for the directory.</span></span> <span data-ttu-id="f3b41-116">또한 관리되는 도메인을 활성화한 가상 네트워크에 대해 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-116">Additionally, you must have administrative privileges over the virtual network in which you enable the managed domain.</span></span> <span data-ttu-id="f3b41-117">RBAC 검사가 일관되게 작동하려면 관리되는 도메인과 가상 네트워크가 동일한 Azure AD 테넌트에 속해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-117">For the RBAC checks to work consistently, the managed domain and the virtual network should belong to the same Azure AD tenant.</span></span>

<span data-ttu-id="f3b41-118">즉 다른 Azure AD 테넌트인 'fabrikam.com'에서 소유한 Azure 구독에 속한 가상 네트워크에서 Azure AD 테넌트 'contoso.com'에 대해 관리되는 도메인을 활성화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-118">In short, you cannot enable a managed domain for an Azure AD tenant 'contoso.com' in a virtual network belonging to an Azure subscription owned by another Azure AD tenant 'fabrikam.com'.</span></span> <span data-ttu-id="f3b41-119">Azure 클래식 포털은 리소스 플랫폼의 맨 위에 구축되지 않으며 그러한 제한을 적용하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-119">The Azure classic portal isn't built on top of the Resource Manager platform and does not enforce such restrictions.</span></span>

<span data-ttu-id="f3b41-120">**유효한 구성**: 이 배포 시나리오에서 Contoso로 관리되는 도메인은 Contoso Azure AD 테넌트에 대해 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-120">**Valid configuration**: In this deployment scenario, the Contoso managed domain is enabled for the Contoso Azure AD tenant.</span></span> <span data-ttu-id="f3b41-121">관리되는 도메인은 Contoso Azure AD 테넌트가 소유한 Azure 구독에 속한 가상 네트워크에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-121">The managed domain is exposed in a virtual network belonging to an Azure subscription owned by the Contoso Azure AD tenant.</span></span> <span data-ttu-id="f3b41-122">따라서 관리되는 도메인과 가상 네트워크 모두 동일한 Azure AD 테넌트에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-122">Therefore, both the managed domain as well as the virtual network belong to the same Azure AD tenant.</span></span> <span data-ttu-id="f3b41-123">이 구성은 유효하며 모두 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-123">This configuration is valid and fully supported.</span></span>

![유효한 테넌트 구성](./media/getting-started/valid-tenant-config.png)

<span data-ttu-id="f3b41-125">**테넌트 구성 불일치**: 이 배포 시나리오에서 Contoso로 관리되는 도메인은 Contoso Azure AD 테넌트에 대해 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-125">**Mismatched tenant configuration**: In this deployment scenario, the Contoso managed domain is enabled for the Contoso Azure AD tenant.</span></span> <span data-ttu-id="f3b41-126">그러나 관리되는 도메인이 Fabrikam Azure AD 테넌트에서 소유한 Azure 구독에 속한 가상 네트워크에 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-126">However, the managed domain is exposed in a virtual network that belongs to an Azure subscription owned by the Fabrikam Azure AD tenant.</span></span> <span data-ttu-id="f3b41-127">따라서 관리되는 도메인과 가상 네트워크는 다른 두 Azure AD 테넌트에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-127">Therefore, the managed domain and the virtual network belong to two different Azure AD tenants.</span></span> <span data-ttu-id="f3b41-128">이 구성은 일치하지 않는 테넌트 구성이며 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-128">This configuration is the mismatched tenant configuration and is not supported.</span></span> <span data-ttu-id="f3b41-129">가상 네트워크를 관리되는 도메인과 동일한 Azure AD 테넌트(즉 Contoso)로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-129">The virtual network must be moved to the same Azure AD tenant (that is, Contoso) as the managed domain.</span></span> <span data-ttu-id="f3b41-130">자세한 내용은 [해결](#resolution) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f3b41-130">See the [Resolution](#resolution) section for details.</span></span>

![테넌트 구성 불일치](./media/getting-started/mismatched-tenant-config.png)

<span data-ttu-id="f3b41-132">따라서 관리되는 도메인과 해당 도메인이 활성화된 가상 네트워크가 서로 다른 두 Azure AD에 속한 경우 이 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-132">Therefore, in scenarios where the managed domain and the virtual network it is enabled in belong to two different Azure AD tenants you see this error.</span></span>

<span data-ttu-id="f3b41-133">리소스 관리자 환경에서 다음과 같은 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-133">The following rules apply in the Resource Manager environment:</span></span>
- <span data-ttu-id="f3b41-134">Azure AD 디렉터리에 여러 Azure 구독이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-134">An Azure AD directory may have multiple Azure subscriptions.</span></span>
- <span data-ttu-id="f3b41-135">한 Azure 구독에는 가상 네트워크와 같은 여러 리소스가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-135">An Azure subscription may have multiple resources such as virtual networks.</span></span>
- <span data-ttu-id="f3b41-136">단일 Azure AD Domain Services로 관리되는 도메인은 Azure AD 디렉터리에 대해 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-136">A single Azure AD Domain Services managed domain is enabled for an Azure AD directory.</span></span>
- <span data-ttu-id="f3b41-137">Azure AD Domain Services로 관리되는 도메인은 동일한 Azure AD 테넌트 안의 Azure 구독 중 하나에 속한 가상 네트워크에서 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-137">An Azure AD Domain Services managed domain can be enabled on a virtual network belonging to any of the Azure subscriptions within the same Azure AD tenant.</span></span>


## <a name="resolution"></a><span data-ttu-id="f3b41-138">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f3b41-138">Resolution</span></span>
<span data-ttu-id="f3b41-139">두 가지 방법으로 디렉터리 불일치 오류를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-139">You have two options to resolve the mismatched directory error.</span></span> <span data-ttu-id="f3b41-140">방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-140">You may:</span></span>

- <span data-ttu-id="f3b41-141">**삭제** 단추를 클릭하여 기존의 관리되는 도메인을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-141">Click the **Delete** button to delete the existing managed domain.</span></span> <span data-ttu-id="f3b41-142">관리되는 도메인과 해당 도메인을 사용할 수 있는 가상 네트워크가 Azure AD 디렉터리에 속하도록 [Azure Portal](https://portal.azure.com)을 사용하여 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-142">Re-create using the [Azure portal](https://portal.azure.com), so that the managed domain and virtual network it is available in belong to the Azure AD directory.</span></span> <span data-ttu-id="f3b41-143">새로 만든 관리되는 도메인, 이전에 삭제된 도메인에 조인한 모든 컴퓨터를 다시 조인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-143">You must join afresh to the newly created managed domain, all machines previously joined to the deleted domain.</span></span>

- <span data-ttu-id="f3b41-144">가상 네트워크가 포함된 Azure 구독을 네트워크 관리되는 도메인이 속한 Azure AD 디렉터리로 이동하려면 Azure 지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="f3b41-144">Contact Azure support to move the Azure subscription containing the virtual network to the Azure AD directory, to which your managed domain belongs.</span></span> <span data-ttu-id="f3b41-145">**새 지원 요청**을 클릭하고 지원 요청의 **세부 정보** 섹션에 **디렉터리 불일치**를 명시합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-145">Click **New support request** and specify **mismatched directory** in the **Details** section of the support request.</span></span> <span data-ttu-id="f3b41-146">오류 메시지에 제공한 정보를 지원 요청의 일부로 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f3b41-146">Include the information provided in the error message as part of the support request.</span></span>


## <a name="related-content"></a><span data-ttu-id="f3b41-147">관련 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="f3b41-147">Related content</span></span>
* [<span data-ttu-id="f3b41-148">Azure AD Domain Services - 시작 가이드</span><span class="sxs-lookup"><span data-stu-id="f3b41-148">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="f3b41-149">문제 해결 가이드 - Azure AD Domain Services </span><span class="sxs-lookup"><span data-stu-id="f3b41-149">Troubleshooting guide - Azure AD Domain Services</span></span>](active-directory-ds-troubleshooting.md)
