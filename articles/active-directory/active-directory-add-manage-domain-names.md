---
title: "Azure Active Directory에서 사용자 지정 도메인 이름을 aaaManaging | Microsoft Docs"
description: "Azure Active Directory에서 사용자 지정 도메인에 대한 관리 개념 및 관리 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="a5b0d-103">Azure Active Directory에서 사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="a5b0d-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="a5b0d-104">도메인 이름은 다음의 일부로 많은 디렉터리 리소스에 대한 중요한 식별자일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-104">A domain name can be an important identifier for many directory resources, as part of:</span></span>

* <span data-ttu-id="a5b0d-105">사용자 이름 또는 사용자에 대한 전자 메일 주소</span><span class="sxs-lookup"><span data-stu-id="a5b0d-105">A user name or email address for a user</span></span>
* <span data-ttu-id="a5b0d-106">그룹에 대 한 hello 주소</span><span class="sxs-lookup"><span data-stu-id="a5b0d-106">hello address for a group</span></span>
* <span data-ttu-id="a5b0d-107">응용 프로그램에 대 한 hello 앱 ID URI</span><span class="sxs-lookup"><span data-stu-id="a5b0d-107">hello app ID URI for an application</span></span>

<span data-ttu-id="a5b0d-108">Azure Active Directory (Azure AD)에 리소스 toobe hello 리소스가 포함 된 hello 디렉터리에 의해 소유 이미 확인 된 도메인 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-108">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified toobe owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="a5b0d-109">전역 관리자만 Azure AD에서 도메인 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-109">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5b0d-110">Hello를 사용 하 여 Azure AD를 관리 하는 것이 좋습니다 [Azure AD 관리 센터](https://aad.portal.azure.com) hello에서 사용 하는 대신 Azure 포털 hello Azure 클래식 포털이이 문서에서 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-110">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="a5b0d-111">어떻게 toomanage 도메인 이름 hello Azure AD 관리 센터에서 참조 [Azure Active Directory에서 사용자 지정 도메인 이름을 관리](active-directory-domains-manage-azure-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-111">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="a5b0d-112">Azure AD 디렉터리에 대 한 hello 기본 도메인 이름 설정</span><span class="sxs-lookup"><span data-stu-id="a5b0d-112">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="a5b0d-113">디렉터리를 만들면 hello 초기 도메인 이름 예: 'contoso.onmicrosoft.com' 디렉터리에 대 한 hello 기본 도메인 이름 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-113">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name for your directory.</span></span> <span data-ttu-id="a5b0d-114">hello에 새 사용자를 만들 때 hello 주 도메인은 새 사용자에 대 한 기본 도메인 이름을 hello [Azure 클래식 포털](https://manage.windowsazure.com/), 또는 hello Office 365 관리 포털 등 다른 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-114">hello primary domain is hello default domain name for a new user when you create a new user in hello [Azure classic portal](https://manage.windowsazure.com/), or other portals such as hello Office 365 admin portal.</span></span> <span data-ttu-id="a5b0d-115">이 관리자 toocreate 새 포털에서 사용자에 hello에 대 한 hello 프로세스를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-115">This streamlines hello process for an administrator toocreate new users in hello portal.</span></span>

<span data-ttu-id="a5b0d-116">디렉터리에 대 한 toochange hello 주 도메인 이름:</span><span class="sxs-lookup"><span data-stu-id="a5b0d-116">toochange hello primary domain name for your directory:</span></span>

1. <span data-ttu-id="a5b0d-117">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) 사용자 계정과 Azure AD 디렉터리의 전역 관리자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-117">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with a user account that is a global administrator of your Azure AD directory.</span></span>
2. <span data-ttu-id="a5b0d-118">선택 **Active Directory** hello 왼쪽된 탐색 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-118">Select **Active Directory** on hello left navigation bar.</span></span>
3. <span data-ttu-id="a5b0d-119">디렉터리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-119">Open your directory.</span></span>
4. <span data-ttu-id="a5b0d-120">선택 hello **도메인** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-120">Select hello **Domains** tab.</span></span>
5. <span data-ttu-id="a5b0d-121">선택 hello **변경 주** hello 명령 모음에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-121">Select hello **Change primary** button on hello command bar.</span></span>
6. <span data-ttu-id="a5b0d-122">Hello 도메인을 toobe hello 새 주 도메인 디렉터리를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-122">Select hello domain that you want toobe hello new primary domain for your directory.</span></span>

<span data-ttu-id="a5b0d-123">페더레이션 계정이 아닌지 확인 된 사용자 지정 도메인 디렉터리 toobe hello 주 도메인 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-123">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="a5b0d-124">디렉터리에 대 한 hello 주 도메인 변경 hello 사용자 이름에 대 한 모든 기존 사용자가 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-124">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="a5b0d-125">사용자 지정 도메인 이름을 tooyour Azure AD를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-125">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="a5b0d-126">Too900 사용자 지정 도메인 이름 tooeach Azure AD 디렉터리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-126">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="a5b0d-127">프로세스를 너무 hello[추가 사용자 지정 도메인 이름을 추가](active-directory-add-domain.md) hello 첫 번째 사용자 지정 도메인 이름에 대 한 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-127">hello process too[add an additional custom domain name](active-directory-add-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="a5b0d-128">사용자 지정 도메인의 하위 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="a5b0d-128">Add subdomains of a custom domain</span></span>
<span data-ttu-id="a5b0d-129">Tooadd 'europe.contoso.com' tooyour 디렉터리와 같이 세 번째 수준의 도메인 이름, 원하는 경우 먼저 추가 하 고 contoso.com 등의 hello 두 번째 수준 도메인을 확인 합니다. Azure AD에 의해 hello 하위 도메인을 자동으로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-129">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="a5b0d-130">방금 추가한 하위 도메인 hello toosee 확인 되 면 디렉터리의 hello 도메인을 나열 하는 hello 브라우저에서 새로 고침 hello 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-130">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains in your directory.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="a5b0d-131">사용자 지정 도메인 이름에 대 한 hello DNS 등록을 변경 하는 경우 어떤 toodo</span><span class="sxs-lookup"><span data-stu-id="a5b0d-131">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="a5b0d-132">사용자 지정 도메인 이름에 대 한 hello DNS 등록을 변경 하면 toouse을 사용자 지정 도메인 이름을 Azure AD와 자체의 추가 구성 작업 없이 하 고 중단 없이 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-132">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="a5b0d-133">사용자 지정 도메인 이름을 사용 하 여 Office 365, Intune 또는 Azure AD에서 사용자 지정 도메인 이름을 사용 하는 다른 서비스와 이러한 서비스에 대해 toohello 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-133">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="a5b0d-134">사용자 지정 도메인 이름 삭제</span><span class="sxs-lookup"><span data-stu-id="a5b0d-134">Delete a custom domain name</span></span>
<span data-ttu-id="a5b0d-135">조직에는 더 이상 해당 도메인 이름을 사용 하는 경우 또는 다른 Azure AD와 해당 도메인 이름을 toouse을 필요한 경우 Azure AD에서 사용자 지정 도메인을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-135">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="a5b0d-136">사용자 지정 도메인 이름을 toodelete 먼저 확인 해야 디렉터리에 있는 hello 도메인 이름에 사용할 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-136">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="a5b0d-137">다음의 경우 디렉터리에서 도메인 이름을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-137">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="a5b0d-138">모든 사용자에 게 사용자 이름, 전자 메일 주소 또는 hello 도메인 이름을 포함 하는 프록시 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-138">Any user has a user name, email address, or proxy address that include hello domain name.</span></span>
* <span data-ttu-id="a5b0d-139">모든 그룹에 전자 메일 주소 또는 hello 도메인 이름을 포함 하는 프록시 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-139">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="a5b0d-140">Azure AD의 모든 응용 프로그램 ID URI hello 도메인 이름을 포함 하는 응용 프로그램을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-140">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="a5b0d-141">Hello 사용자 지정 도메인 이름을 삭제 하려면 먼저 Azure AD 디렉터리에서 이러한 리소스를 삭제 하거나 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-141">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="a5b0d-142">PowerShell 또는 Graph API toomanage 도메인 이름 사용</span><span class="sxs-lookup"><span data-stu-id="a5b0d-142">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="a5b0d-143">Azure Active Directory의 도메인 이름에 대한 대부분의 관리 작업은 Microsoft PowerShell을 사용하거나 프로그래밍 방식으로 Azure AD Graph API를 사용하여 완료할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5b0d-143">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="a5b0d-144">Azure ad에서 PowerShell toomanage 도메인 이름을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a5b0d-144">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="a5b0d-145">Azure ad에서 Graph API toomanage 도메인 이름을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="a5b0d-145">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="a5b0d-146">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a5b0d-146">Next steps</span></span>
* [<span data-ttu-id="a5b0d-147">Azure AD에서 도메인 이름에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="a5b0d-147">Learn about domain names in Azure AD</span></span>](active-directory-add-domain-concepts.md)
* [<span data-ttu-id="a5b0d-148">사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="a5b0d-148">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)

