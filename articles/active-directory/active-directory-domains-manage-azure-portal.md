---
title: "Azure Active Directory에서 사용자 지정 도메인 이름을 aaaManaging | Microsoft Docs"
description: "Azure Active Directory에서 도메인 이름 관리에 대한 관리 개념 및 방법"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a><span data-ttu-id="06197-103">Azure Active Directory에서 사용자 지정 도메인 이름 관리</span><span class="sxs-lookup"><span data-stu-id="06197-103">Managing custom domain names in your Azure Active Directory</span></span>
<span data-ttu-id="06197-104">도메인 이름이 많은 디렉터리 리소스에 대 한 hello 식별자의 중요 한 부분이: 사용자가 그룹에 대 한 hello 주소의 일부가 사용자 이름이 나 전자 메일 주소의 일부 이며 응용 프로그램에 대 한 hello 앱 ID URI의 일부가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-104">A domain name is an important part of hello identifier for many directory resources: it is part of a user name or email address for a user, part of hello address for a group, and can be part of hello app ID URI for an application.</span></span> <span data-ttu-id="06197-105">Azure Active Directory (Azure AD)에 리소스 hello 리소스가 포함 된 hello 디렉터리가 소유 하 고 이미 확인 된 도메인 이름을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-105">A resource in Azure Active Directory (Azure AD) can include a domain name that is already verified as owned by hello directory that contains hello resource.</span></span> <span data-ttu-id="06197-106">전역 관리자만 Azure AD에서 도메인 관리 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-106">Only a global administrator can perform domain management tasks in Azure AD.</span></span>

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a><span data-ttu-id="06197-107">Azure AD 디렉터리에 대 한 hello 기본 도메인 이름 설정</span><span class="sxs-lookup"><span data-stu-id="06197-107">Set hello primary domain name for your Azure AD directory</span></span>
<span data-ttu-id="06197-108">디렉터리를 만들면 hello 초기 도메인 이름 예: 'contoso.onmicrosoft.com' hello 기본 도메인 이름 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-108">When your directory is created, hello initial domain name, such as ‘contoso.onmicrosoft.com,’ is also hello primary domain name.</span></span> <span data-ttu-id="06197-109">hello 주 도메인은 새 사용자를 만들 때 새 사용자에 대 한 hello 기본 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="06197-109">hello primary domain is hello default domain name for a new user when you create a new user.</span></span> <span data-ttu-id="06197-110">주 도메인 이름을 설정 하는 hello 포털에는 관리자 toocreate 새 사용자에 대 한 hello 프로세스를 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-110">Setting a primary domain name streamlines hello process for an administrator toocreate new users in hello portal.</span></span> <span data-ttu-id="06197-111">toochange hello 주 도메인 이름:</span><span class="sxs-lookup"><span data-stu-id="06197-111">toochange hello primary domain name:</span></span>

1. <span data-ttu-id="06197-112">Toohello 로그인 [Azure 포털](https://portal.azure.com) hello 디렉터리에 대 한 전역 관리자 인 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-112">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="06197-113">선택 **더 많은 서비스**, 입력 **Azure Active Directory** 에 hello 텍스트 상자를 선택한 후 **Enter**합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-113">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
   
   ![사용자 관리 열기](./media/active-directory-domains-add-azure-portal/user-management.png)
3. <span data-ttu-id="06197-115">Hello에 ***디렉터리 이름*** 블레이드를 **도메인 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-115">On hello ***directory-name*** blade, select **Domain names**.</span></span>
4. <span data-ttu-id="06197-116">Hello에  ***디렉터리 이름* -도메인 이름을** 블레이드, 선택 hello 도메인 이름 toomake hello 주 도메인 이름을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-116">On hello ***directory-name* - Domain names** blade, select hello domain name you would like toomake hello primary domain name.</span></span>
5. <span data-ttu-id="06197-117">Hello에 ***도메인 이름*** 블레이드 (즉, hello 블레이드에서 열리면 hello 제목에 새 도메인 이름을 가진) hello 선택 **기본** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="06197-117">On hello ***domain name*** blade (that is, hello blade that opens that has your new domain name in hello title), select hello **Make primary** command.</span></span> <span data-ttu-id="06197-118">메시지가 표시되면 선택을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-118">Confirm your choice when prompted.</span></span>
   
   ![주 도메인 이름 만들기](./media/active-directory-domains-manage-azure-portal/make-primary.png)

<span data-ttu-id="06197-120">페더레이션 계정이 아닌지 확인 된 사용자 지정 도메인 디렉터리 toobe hello 주 도메인 이름을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-120">You can change hello primary domain name for your directory toobe any verified custom domain that is not federated.</span></span> <span data-ttu-id="06197-121">디렉터리에 대 한 hello 주 도메인 변경 hello 사용자 이름에 대 한 모든 기존 사용자가 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-121">Changing hello primary domain for your directory will not change hello user names for any existing users.</span></span>

## <a name="add-custom-domain-names-tooyour-azure-ad"></a><span data-ttu-id="06197-122">사용자 지정 도메인 이름을 tooyour Azure AD를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-122">Add custom domain names tooyour Azure AD</span></span>
<span data-ttu-id="06197-123">Too900 사용자 지정 도메인 이름 tooeach Azure AD 디렉터리를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-123">You can add up too900 custom domain names tooeach Azure AD directory.</span></span> <span data-ttu-id="06197-124">프로세스를 너무 hello[추가 사용자 지정 도메인 이름을 추가](add-custom-domain.md) hello 첫 번째 사용자 지정 도메인 이름에 대 한 동일 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06197-124">hello process too[add an additional custom domain name](add-custom-domain.md) is hello same for hello first custom domain name.</span></span>

## <a name="add-subdomains-of-a-custom-domain"></a><span data-ttu-id="06197-125">사용자 지정 도메인의 하위 도메인 추가</span><span class="sxs-lookup"><span data-stu-id="06197-125">Add subdomains of a custom domain</span></span>
<span data-ttu-id="06197-126">Tooadd 'europe.contoso.com' tooyour 디렉터리와 같이 세 번째 수준의 도메인 이름, 원하는 경우 먼저 추가 하 고 contoso.com 등의 hello 두 번째 수준 도메인을 확인 합니다. Azure AD에 의해 hello 하위 도메인을 자동으로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06197-126">If you want tooadd a third-level domain name such as ‘europe.contoso.com’ tooyour directory, you should first add and verify hello second-level domain, such as contoso.com. hello subdomain will be automatically verified by Azure AD.</span></span> <span data-ttu-id="06197-127">방금 추가한 하위 도메인 hello toosee 확인 되 면 hello 도메인을 나열 하는 hello 브라우저에서 새로 고침 hello 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="06197-127">toosee that hello subdomain that you just added has been verified, refresh hello page in hello browser that lists hello domains.</span></span>

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a><span data-ttu-id="06197-128">사용자 지정 도메인 이름에 대 한 hello DNS 등록을 변경 하는 경우 어떤 toodo</span><span class="sxs-lookup"><span data-stu-id="06197-128">What toodo if you change hello DNS registrar for your custom domain name</span></span>
<span data-ttu-id="06197-129">사용자 지정 도메인 이름에 대 한 hello DNS 등록을 변경 하면 toouse을 사용자 지정 도메인 이름을 Azure AD와 자체의 추가 구성 작업 없이 하 고 중단 없이 계속할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-129">If you change hello DNS registrar for your custom domain name, you can continue toouse your custom domain name with Azure AD itself without interruption and without additional configuration tasks.</span></span> <span data-ttu-id="06197-130">사용자 지정 도메인 이름을 사용 하 여 Office 365, Intune 또는 Azure AD에서 사용자 지정 도메인 이름을 사용 하는 다른 서비스와 이러한 서비스에 대해 toohello 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="06197-130">If you use your custom domain name with Office 365, Intune, or other services that rely on custom domain names in Azure AD, refer toohello documentation for those services.</span></span>

## <a name="delete-a-custom-domain-name"></a><span data-ttu-id="06197-131">사용자 지정 도메인 이름 삭제</span><span class="sxs-lookup"><span data-stu-id="06197-131">Delete a custom domain name</span></span>
<span data-ttu-id="06197-132">조직에는 더 이상 해당 도메인 이름을 사용 하는 경우 또는 다른 Azure AD와 해당 도메인 이름을 toouse을 필요한 경우 Azure AD에서 사용자 지정 도메인을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-132">You can delete a custom domain name from your Azure AD if your organization no longer uses that domain name, or if you need toouse that domain name with another Azure AD.</span></span>

<span data-ttu-id="06197-133">사용자 지정 도메인 이름을 toodelete 먼저 확인 해야 디렉터리에 있는 hello 도메인 이름에 사용할 합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-133">toodelete a custom domain name, you must first ensure that no resources in your directory rely on hello domain name.</span></span> <span data-ttu-id="06197-134">다음의 경우 디렉터리에서 도메인 이름을 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-134">You can't delete a domain name from your directory if:</span></span>

* <span data-ttu-id="06197-135">모든 사용자에 게 사용자 이름, 전자 메일 주소 또는 hello 도메인 이름을 포함 하는 프록시 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="06197-135">Any user has a user name, email address, or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="06197-136">모든 그룹에 전자 메일 주소 또는 hello 도메인 이름을 포함 하는 프록시 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="06197-136">Any group has an email address or proxy address that includes hello domain name.</span></span>
* <span data-ttu-id="06197-137">Azure AD의 모든 응용 프로그램 ID URI hello 도메인 이름을 포함 하는 응용 프로그램을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-137">Any application in your Azure AD has an app ID URI that includes hello domain name.</span></span>

<span data-ttu-id="06197-138">Hello 사용자 지정 도메인 이름을 삭제 하려면 먼저 Azure AD 디렉터리에서 이러한 리소스를 삭제 하거나 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06197-138">You must change or delete any such resource in your Azure AD directory before you can delete hello custom domain name.</span></span>

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a><span data-ttu-id="06197-139">PowerShell 또는 Graph API toomanage 도메인 이름 사용</span><span class="sxs-lookup"><span data-stu-id="06197-139">Use PowerShell or Graph API toomanage domain names</span></span>
<span data-ttu-id="06197-140">Azure Active Directory의 도메인 이름에 대한 대부분의 관리 작업은 Microsoft PowerShell을 사용하거나 프로그래밍 방식으로 Azure AD Graph API를 사용하여 완료할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06197-140">Most management tasks for domain names in Azure Active Directory can also be completed using Microsoft PowerShell, or programmatically using Azure AD Graph API.</span></span>

* [<span data-ttu-id="06197-141">Azure ad에서 PowerShell toomanage 도메인 이름을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="06197-141">Using PowerShell toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [<span data-ttu-id="06197-142">Azure ad에서 Graph API toomanage 도메인 이름을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="06197-142">Using Graph API toomanage domain names in Azure AD</span></span>](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a><span data-ttu-id="06197-143">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06197-143">Next steps</span></span>
* [<span data-ttu-id="06197-144">사용자 지정 도메인 이름 추가</span><span class="sxs-lookup"><span data-stu-id="06197-144">Add custom domain names</span></span>](add-custom-domain.md)

