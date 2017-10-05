---
title: "응용 프로그램에 대한 동의를 수행할 때 예기치 않은 오류 | Microsoft Docs"
description: "응용 프로그램에 대한 동의 프로세스 도중 발생할 수 있는 오류 및 사용자가 할 수 있는 조치를 설명합니다."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: fd500fdd4c8642bad96dcf71eebcf1fad461a35f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-error-when-performing-consent-to-an-application"></a><span data-ttu-id="eb9cc-103">응용 프로그램에 대한 동의를 수행할 때 예기치 않은 오류</span><span class="sxs-lookup"><span data-stu-id="eb9cc-103">Unexpected error when performing consent to an application</span></span>

<span data-ttu-id="eb9cc-104">이 문서에서는 응용 프로그램에 대한 동의 프로세스 도중 발생할 수 있는 오류에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-104">This article discusses errors that can occur during the process of consenting to an application.</span></span> <span data-ttu-id="eb9cc-105">오류 메시지를 포함하지 않는 예기치 않은 동의 프롬프트의 문제를 해결하려는 경우 [Azure AD의 인증 시나리오](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-105">If you are Troubleshoot unexpected consent prompts that do not contain any error messages, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span></span>

<span data-ttu-id="eb9cc-106">Azure Active Directory와 통합되는 많은 응용 프로그램을 작동시키기 위해 다른 리소스에 대한 사용 권한이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-106">Many applications that integrate with Azure Active Directory require permissions to access other resources in order to function.</span></span> <span data-ttu-id="eb9cc-107">또한 이러한 리소스가 Azure Active Directory와 통합되면 종종 일반적인 동의 프레임워크를 사용하여 액세스하기 위한 사용 권한을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-107">When these resources are also integrated with Azure Active Directory, permissions to access them is often requested using the common consent framework.</span></span> 

<span data-ttu-id="eb9cc-108">이로 인해 일반적으로 응용 프로그램을 처음 사용하는 경우 발생하지만 응용 프로그램의 후속 사용에도 발생할 수 있는 동의 확인 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-108">This results in a consent prompt being displayed, which generally occurs the first time an application is used but can also occur on a subsequent use of the application.</span></span>

<span data-ttu-id="eb9cc-109">응용 프로그램에 필요한 사용 권한에 대해 동의한 사용자에게는 특정 조건이 true여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-109">Certain conditions must be true for a user to consent to the permissions an application requires.</span></span> <span data-ttu-id="eb9cc-110">이러한 조건이 충족되지 않으면 다양한 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-110">If these conditions are not met, various errors can occur.</span></span> <span data-ttu-id="eb9cc-111">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-111">These include:</span></span>

## <a name="requesting-not-authorized-permissions-error"></a><span data-ttu-id="eb9cc-112">권한 없는 사용 권한 요청 오류</span><span class="sxs-lookup"><span data-stu-id="eb9cc-112">Requesting not authorized permissions error</span></span>
* <span data-ttu-id="eb9cc-113">**AADSTS90093:** &lt;clientAppDisplayName&gt;은 사용 권한이 부여되지 않은 하나 이상의 사용 권한을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-113">**AADSTS90093:** &lt;clientAppDisplayName&gt; is requesting one or more permissions that you are not authorized to grant.</span></span> <span data-ttu-id="eb9cc-114">사용자 대신 이 응용 프로그램에 동의할 수 있는 관리자에게 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-114">Contact an administrator, who can consent to this application on your behalf.</span></span>

<span data-ttu-id="eb9cc-115">이 오류는 회사 관리자가 아닌 사용자가 관리자만이 부여할 수 있는 사용 권한을 요청하는 응용 프로그램을 사용하려고 할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-115">This error occurs when a user who is not a company administrator attempts to use an application that is requesting permissions that only an administrator can grant.</span></span> <span data-ttu-id="eb9cc-116">해당 조직을 대신하여 응용 프로그램에 대한 액세스 권한을 부여하는 관리자가 이 오류를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-116">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="policy-prevents-granting-permissions-error"></a><span data-ttu-id="eb9cc-117">사용 권한 부여를 방지하는 정책 오류</span><span class="sxs-lookup"><span data-stu-id="eb9cc-117">Policy prevents granting permissions error</span></span>
* <span data-ttu-id="eb9cc-118">**AADSTS90093:** &lt;tenantDisplayName&gt;의 관리자는 사용 권한이 요청하는 &lt;앱의 이름&gt;을 부여하지 못하도록 방지하는 정책을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-118">**AADSTS90093:** An administrator of &lt;tenantDisplayName&gt; has set a policy that prevents you from granting &lt;name of app&gt; the permissions it is requesting.</span></span> <span data-ttu-id="eb9cc-119">사용자 대신 이 앱에 대한 권한을 부여할 수 있는 &lt;tenantDisplayName&gt;의 관리자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-119">Contact an administrator of &lt;tenantDisplayName&gt;, who can grant permissions to this app on your behalf.</span></span>

<span data-ttu-id="eb9cc-120">회사 관리자가 응용 프로그램에 대해 동의하는 사용자의 기능을 해제한 다음 관리자가 아닌 사용자가 동의를 필요로 하는 응용 프로그램을 사용하려는 경우에 이 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-120">This error occurs when a company administrator turns off the ability for users to consent to applications, then a non-administrator user attempts to use an application that requires consent.</span></span> <span data-ttu-id="eb9cc-121">해당 조직을 대신하여 응용 프로그램에 대한 액세스 권한을 부여하는 관리자가 이 오류를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-121">This error can be resolved by an administrator granting access to the application on behalf of their organization.</span></span>

## <a name="intermittent-problem-error"></a><span data-ttu-id="eb9cc-122">일시적인 문제 오류</span><span class="sxs-lookup"><span data-stu-id="eb9cc-122">Intermittent problem error</span></span>
* <span data-ttu-id="eb9cc-123">**AADSTS90090:** &lt;clientAppDisplayName&gt;에 권한을 부여하려고 시도하는 사용 권한을 기록하는 일시적인 문제가 발생했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-123">**AADSTS90090:** It looks like we encountered an intermittent problem recording the permissions you attempted to grant to &lt;clientAppDisplayName&gt;.</span></span> <span data-ttu-id="eb9cc-124">나중에 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-124">try again later.</span></span>

<span data-ttu-id="eb9cc-125">이 오류는 일시적인 서비스 쪽 문제가 발생했음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-125">This error indicates that an intermittent service side issue has occurred.</span></span> <span data-ttu-id="eb9cc-126">응용 프로그램에 대한 동의하도록 다시 시도하여 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-126">It can be resolved by attempting to consent to the application again.</span></span>

## <a name="resource-not-available-error"></a><span data-ttu-id="eb9cc-127">리소스 사용할 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="eb9cc-127">Resource not available error</span></span>
* <span data-ttu-id="eb9cc-128">**AADSTS65005:** &lt;clientAppDisplayName&gt; 앱은 사용할 수 없는 &lt;resourceAppDisplayName&gt; 리소스에 액세스하는 사용 권한을 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-128">**AADSTS65005:** The app &lt;clientAppDisplayName&gt; requested permissions to access a resource &lt;resourceAppDisplayName&gt; that is not available.</span></span> 

<span data-ttu-id="eb9cc-129">응용 프로그램 개발자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-129">Contact the application developer.</span></span>

##  <a name="resource-not-available-in-tenant-error"></a><span data-ttu-id="eb9cc-130">테넌트에서 리소스 사용할 수 없음 오류</span><span class="sxs-lookup"><span data-stu-id="eb9cc-130">Resource not available in tenant error</span></span>
* <span data-ttu-id="eb9cc-131">**AADSTS65005:** &lt;clientAppDisplayName&gt;은 &lt;tenantDisplayName&gt; 조직에서 사용할 수 없는 &lt;resourceAppDisplayName&gt; 리소스에 대한 액세스 권한을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-131">**AADSTS65005:** &lt;clientAppDisplayName&gt; is requesting access to a resource &lt;resourceAppDisplayName&gt; that is not available in your organization &lt;tenantDisplayName&gt;.</span></span> 

<span data-ttu-id="eb9cc-132">이 리소스를 사용할 수 있도록 하거나 &lt;tenantDisplayName&gt;의 관리자에게 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-132">Ensure that this resource is available or contact an administrator of &lt;tenantDisplayName&gt;.</span></span>

## <a name="permissions-mismatch-error"></a><span data-ttu-id="eb9cc-133">권한 불일치 오류</span><span class="sxs-lookup"><span data-stu-id="eb9cc-133">Permissions mismatch error</span></span>
* <span data-ttu-id="eb9cc-134">**AADSTS65005:** 앱이 &lt;resourceAppDisplayName&gt; 리소스에 액세스하기 위한 동의를 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-134">**AADSTS65005:** The app requested consent to access resource &lt;resourceAppDisplayName&gt;.</span></span> <span data-ttu-id="eb9cc-135">앱 등록 중에 앱이 미리 구성된 방법과 일치하지 않기 때문에 이 요청에 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-135">This request failed because it does not match how the app was pre-configured during app registration.</span></span> <span data-ttu-id="eb9cc-136">앱 공급업체에게 문의하세요.**</span><span class="sxs-lookup"><span data-stu-id="eb9cc-136">Contact the app vendor.**</span></span>

<span data-ttu-id="eb9cc-137">사용자가 동의하려는 응용 프로그램이 조직의 디렉터리(테넌트)에서 찾을 수 없는 리소스 응용 프로그램에 액세스하는 사용 권한을 요청하는 경우에 이러한 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-137">These errors all occur when the application a user is trying to consent to is requesting permissions to access a resource application that cannot be found in the organization’s directory (tenant).</span></span> <span data-ttu-id="eb9cc-138">이 오류는 다음과 같은 이유로 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-138">This can occur for several reasons:</span></span>

-   <span data-ttu-id="eb9cc-139">클라이언트 응용 프로그램 개발자가 해당 응용 프로그램을 잘못 구성하여 잘못된 리소스에 대한 액세스 권한을 요청했습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-139">The client application developer has configured their application incorrectly, causing it to request access to an invalid resource.</span></span> <span data-ttu-id="eb9cc-140">이 경우에 응용 프로그램 개발자는 이 문제를 해결하기 위해 클라이언트 응용 프로그램의 구성을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-140">In this case, the application developer must update the configuration of the client application to resolve this issue.</span></span>

-   <span data-ttu-id="eb9cc-141">대상 리소스 응용 프로그램을 나타내는 서비스 주체는 조직에서 존재하지 않거나 이전에 있었지만 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-141">A Service Principal representing the target resource application does not exist in the organization, or existed in the past but has been removed.</span></span> <span data-ttu-id="eb9cc-142">이 문제를 해결하려면 클라이언트 응용 프로그램이 이에 대한 권한을 요청할 수 있도록 조직에서 리소스 응용 프로그램의 서비스 주체를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-142">To resolve this issue, a Service Principal for the resource application must be provisioned in the organization so the client application can request permissions to it.</span></span> <span data-ttu-id="eb9cc-143">다음을 비롯한 다양한 방법으로 응용 프로그램의 종류에 따라 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eb9cc-143">This can happen in an number of ways, depending on the type of application, including:</span></span>

    -   <span data-ttu-id="eb9cc-144">리소스 응용 프로그램의 구독 구입(게시된 Microsoft 응용 프로그램)</span><span class="sxs-lookup"><span data-stu-id="eb9cc-144">Acquiring a subscription for the resource application (Microsoft published applications)</span></span>

    -   <span data-ttu-id="eb9cc-145">리소스 응용 프로그램에 대한 동의</span><span class="sxs-lookup"><span data-stu-id="eb9cc-145">Consenting to the resource application</span></span>

    -   <span data-ttu-id="eb9cc-146">Azure Portal을 통해 응용 프로그램 사용 권한 부여</span><span class="sxs-lookup"><span data-stu-id="eb9cc-146">Granting the application permissions via the Azure Portal</span></span>

    -   <span data-ttu-id="eb9cc-147">Azure AD 응용 프로그램 갤러리의 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="eb9cc-147">Adding the application from the Azure AD Application Gallery</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb9cc-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eb9cc-148">Next steps</span></span> 

[<span data-ttu-id="eb9cc-149">Azure Active Directory에서 앱, 사용 권한 및 동의(v1 끝점)</span><span class="sxs-lookup"><span data-stu-id="eb9cc-149">Apps, permissions, and consent in Azure Active Directory (v1 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[<span data-ttu-id="eb9cc-150">Azure Active Directory의 범위, 사용 권한 및 동의(v2.0 끝점)</span><span class="sxs-lookup"><span data-stu-id="eb9cc-150">Scopes, permissions, and consent in the Azure Active Directory (v2.0 endpoint)</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


