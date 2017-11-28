---
title: "포털에서 Azure 응용 프로그램에 대 한 aaaCreate id | Microsoft Docs"
description: "Toocreate 새 Azure Active Directory 응용 프로그램 및 서비스에서 Azure 리소스 관리자 toomanage hello 역할 기반 액세스 제어를 통해 사용할 수 있는 사용자 tooresources 액세스 방법을 설명 합니다."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="eec50-103">Azure Active Directory 응용 프로그램 및 서비스 사용자 리소스에 액세스할 수 있는 포털 toocreate를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="eec50-103">Use portal toocreate an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="eec50-104">Tooaccess 필요 하거나 리소스를 수정 하는 응용 프로그램을 사용 하는 경우에 Azure AD (Active Directory) 응용 프로그램을 설정 하 고 hello 필요한 사용 권한을 tooit 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-104">When you have an application that needs tooaccess or modify resources, you must set up an Azure Active Directory (AD) application and assign hello required permissions tooit.</span></span> <span data-ttu-id="eec50-105">이 방법은 것이 좋습니다 toorunning hello 앱 자신의 자격 증명 때문에:</span><span class="sxs-lookup"><span data-stu-id="eec50-105">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="eec50-106">자신만 사용 권한을 것과 다른 toohello 응용 프로그램 id 권한을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-106">You can assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="eec50-107">일반적으로 이러한 권한은 제한 된 tooexactly 어떤 hello 앱 toodo 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-107">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="eec50-108">않아도 toochange hello 응용 프로그램의 자격 증명 사용자의 책임을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-108">You do not have toochange hello app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="eec50-109">무인 설치 스크립트를 실행할 때 인증서 tooautomate 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-109">You can use a certificate tooautomate authentication when executing an unattended script.</span></span>

<span data-ttu-id="eec50-110">이 항목에서는 방법을 tooperform 하는 것을 단계별로 hello 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-110">This topic shows you how tooperform those steps through hello portal.</span></span> <span data-ttu-id="eec50-111">여기서 hello 응용 프로그램은 한 조직 내에서 의도 한 toorun 단일 테 넌 트 응용 프로그램에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-111">It focuses on a single-tenant application where hello application is intended toorun within only one organization.</span></span> <span data-ttu-id="eec50-112">일반적으로 단일 조직 내에서 실행되는 LOB(기간 업무) 응용 프로그램에 대해 단일 테넌트 응용 프로그램을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="eec50-113">필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="eec50-113">Required permissions</span></span>
<span data-ttu-id="eec50-114">toocomplete이이 항목에서는 Azure AD 테 넌 트와 충분 한 사용 권한을 tooregister 응용 프로그램이 있어야 하 고 Azure 구독에서 hello 응용 프로그램 tooa 역할을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-114">toocomplete this topic, you must have sufficient permissions tooregister an application with your Azure AD tenant, and assign hello application tooa role in your Azure subscription.</span></span> <span data-ttu-id="eec50-115">Hello 적절 한 사용 권한이 tooperform 이러한 단계는 선택 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-115">Let's make sure you have hello right permissions tooperform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="eec50-116">Azure Active Directory 권한 확인</span><span class="sxs-lookup"><span data-stu-id="eec50-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="eec50-117">Hello 통해 Azure 계정 tooyour 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-117">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="eec50-118">**Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-118">Select **Azure Active Directory**.</span></span>

     ![Azure Active Directory 선택](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="eec50-120">Azure Active Directory에서 **사용자 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-120">In Azure Active Directory, select **User settings**.</span></span>

     ![사용자 설정 선택](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="eec50-122">Hello 확인 **앱 등록** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-122">Check hello **App registrations** setting.</span></span> <span data-ttu-id="eec50-123">경우 너무 설정**예**, 관리자가 아닌 사용자가 AD 응용 프로그램을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-123">If set too**Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="eec50-124">이 설정에서는 hello Azure AD 테 넌 트의 모든 사용자는 응용 프로그램을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-124">This setting means any user in hello Azure AD tenant can register an app.</span></span> <span data-ttu-id="eec50-125">너무 진행할 수[확인 Azure 구독 권한을](#check-azure-subscription-permissions)합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-125">You can proceed too[Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![앱 등록 보기](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="eec50-127">Hello 응용 프로그램 등록 설정 너무 설정 되어 있으면**아니요**관리자가 사용자가 앱을 등록할 수만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-127">If hello app registrations setting is set too**No**, only admin users can register apps.</span></span> <span data-ttu-id="eec50-128">계정 hello Azure AD 테 넌 트에 대 한 관리자 인지 toocheck이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-128">You need toocheck whether your account is an admin for hello Azure AD tenant.</span></span> <span data-ttu-id="eec50-129">빠른 작업에서 **개요** 및 **사용자 찾기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![사용자 찾기](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="eec50-131">사용자 계정을 검색하고, 찾으면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-131">Search for your account, and select it when you find it.</span></span>

     ![사용자 검색](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="eec50-133">사용자 계정에 대해 **디렉터리 역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-133">For your account, select **Directory role**.</span></span> 

     ![디렉터리 역할](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="eec50-135">Azure AD에서 할당된 디렉터리 역할을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="eec50-136">Toohello 사용자 역할이 할당 됩니다. 사용자 계정 이지만 hello (이전 단계는 hello)에서 응용 프로그램 등록 설정 제한 tooadmin 사용자 인 경우에 관리자 tooeither 있습니다 tooan 관리자 역할 또는 tooenable 사용자 tooregister 앱 할당 요청.</span><span class="sxs-lookup"><span data-stu-id="eec50-136">If your account is assigned toohello User role, but hello app registration setting (from hello preceding steps) is limited tooadmin users, ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

     ![역할 보기](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="eec50-138">Azure 구독 권한 확인</span><span class="sxs-lookup"><span data-stu-id="eec50-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="eec50-139">Azure 구독에서 계정에 있어야 `Microsoft.Authorization/*/Write` tooassign AD 앱 tooa 역할에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access tooassign an AD app tooa role.</span></span> <span data-ttu-id="eec50-140">이 작업은 hello을 통해 부여 [소유자](../active-directory/role-based-access-built-in-roles.md#owner) 역할 또는 [사용자 액세스 관리자에 게](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-140">This action is granted through hello [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="eec50-141">계정 toohello 지정 되 면 **참가자** 역할을 적절 한 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-141">If your account is assigned toohello **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="eec50-142">Tooassign hello 서비스 보안 주체 tooa 역할을 시도할 때 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-142">You will receive an error when attempting tooassign hello service principal tooa role.</span></span> 

<span data-ttu-id="eec50-143">toocheck 구독 권한을:</span><span class="sxs-lookup"><span data-stu-id="eec50-143">toocheck your subscription permissions:</span></span>

1. <span data-ttu-id="eec50-144">표시 되지 않는 이미 Azure AD 계정에 hello 이전 단계에서에서 선택 **Azure Active Directory** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="eec50-144">If you are not already looking at your Azure AD account from hello preceding steps, select **Azure Active Directory** from hello left pane.</span></span>

2. <span data-ttu-id="eec50-145">Azure AD 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-145">Find your Azure AD account.</span></span> <span data-ttu-id="eec50-146">빠른 작업에서 **개요** 및 **사용자 찾기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![사용자 찾기](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="eec50-148">사용자 계정을 검색하고, 찾으면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-148">Search for your account, and select it when you find it.</span></span>

     ![사용자 검색](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="eec50-150">**Azure 리소스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-150">Select **Azure resources**.</span></span>

     ![리소스 선택](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="eec50-152">할당 된 사용자 역할을 확인 하 고 있으면 적절 한 사용 권한이 tooassign AD 앱 tooa 역할을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-152">View your assigned roles, and determine if you have adequate permissions tooassign an AD app tooa role.</span></span> <span data-ttu-id="eec50-153">그렇지 않은 경우에 구독 관리자 tooadd 요청 tooUser 액세스 관리자에 게 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-153">If not, ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span> <span data-ttu-id="eec50-154">다음 이미지는 hello, hello 사용자는 해당 사용자에 게 권한이 즉 두 개의 구독에 대 한 할당 된 toohello 소유자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-154">In hello following image, hello user is assigned toohello Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![권한 표시](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="eec50-156">Azure Active Directory 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="eec50-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="eec50-157">Hello 통해 Azure 계정 tooyour 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-157">Log in tooyour Azure Account through hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="eec50-158">**Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-158">Select **Azure Active Directory**.</span></span>

     ![Azure Active Directory 선택](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="eec50-160">**앱 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-160">Select **App registrations**.</span></span>   

     ![앱 등록 선택](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="eec50-162">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-162">Select **Add**.</span></span>

     ![앱 추가](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="eec50-164">Hello 응용 프로그램에 대 한 이름 및 URL을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-164">Provide a name and URL for hello application.</span></span> <span data-ttu-id="eec50-165">선택 **웹 응용 프로그램 / API** 또는 **네이티브** 원하는 toocreate hello 유형의 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-165">Select either **Web app / API** or **Native** for hello type of application you want toocreate.</span></span> <span data-ttu-id="eec50-166">Hello 값을 설정한 후 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-166">After setting hello values, select **Create**.</span></span>

     ![응용 프로그램 이름 지정](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="eec50-168">응용 프로그램이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="eec50-169">응용 프로그램 ID 및 인증 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="eec50-169">Get application ID and authentication key</span></span>
<span data-ttu-id="eec50-170">프로그래밍 방식으로 로그인 할 때 응용 프로그램 및 인증 키에 대 한 hello ID 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-170">When programmatically logging in, you need hello ID for your application and an authentication key.</span></span> <span data-ttu-id="eec50-171">tooget 해당 값을 사용 하 여 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-171">tooget those values, use hello following steps:</span></span>

1. <span data-ttu-id="eec50-172">Azure Active Directory의 **앱 등록**에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![응용 프로그램 선택](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="eec50-174">복사 hello **응용 프로그램 ID** 응용 프로그램 코드에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-174">Copy hello **Application ID** and store it in your application code.</span></span> <span data-ttu-id="eec50-175">hello에 대 한 응용 프로그램 hello [샘플 응용 프로그램](#sample-applications) 섹션 toothis 값 hello 클라이언트 id로 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-175">hello applications in hello [sample applications](#sample-applications) section refer toothis value as hello client id.</span></span>

     ![클라이언트 ID](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="eec50-177">인증 키를 toogenerate 선택 **키**합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-177">toogenerate an authentication key, select **Keys**.</span></span>

     ![키 선택](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="eec50-179">Hello 키 및 hello 키에 대 한 기간에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-179">Provide a description of hello key, and a duration for hello key.</span></span> <span data-ttu-id="eec50-180">완료되면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-180">When done, select **Save**.</span></span>

     ![키 저장](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="eec50-182">Hello 키를 저장 한 후 hello hello 키 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-182">After saving hello key, hello value of hello key is displayed.</span></span> <span data-ttu-id="eec50-183">관리자가 아니므로 수 tooretrieve hello 키 나중에이 값을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-183">Copy this value because you are not able tooretrieve hello key later.</span></span> <span data-ttu-id="eec50-184">Hello 응용 프로그램으로의 응용 프로그램 ID toolog hello와 hello 키 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-184">You provide hello key value with hello application ID toolog in as hello application.</span></span> <span data-ttu-id="eec50-185">응용 프로그램 검색할 수 있는 hello 키 값을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-185">Store hello key value where your application can retrieve it.</span></span>

     ![공유 키](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="eec50-187">테넌트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="eec50-187">Get tenant ID</span></span>
<span data-ttu-id="eec50-188">프로그래밍 방식으로 로그인 할 때 인증 요청과 함께 toopass hello 테 넌 트 ID가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-188">When programmatically logging in, you need toopass hello tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="eec50-189">tooget hello 테 넌 트 ID, 선택 **속성** Azure AD 테 넌 트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-189">tooget hello tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Azure AD 속성 선택](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="eec50-191">복사 hello **디렉터리 ID**합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-191">Copy hello **Directory ID**.</span></span> <span data-ttu-id="eec50-192">이 값은 테넌트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-192">This value is your tenant ID.</span></span>

     ![테넌트 ID](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a><span data-ttu-id="eec50-194">응용 프로그램 toorole 할당</span><span class="sxs-lookup"><span data-stu-id="eec50-194">Assign application toorole</span></span>
<span data-ttu-id="eec50-195">구독에서 리소스 tooaccess hello 응용 프로그램 tooa 역할을 할당 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-195">tooaccess resources in your subscription, you must assign hello application tooa role.</span></span> <span data-ttu-id="eec50-196">역할을 나타내는 hello hello 응용 프로그램에 대 한 올바른 권한을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-196">Decide which role represents hello right permissions for hello application.</span></span> <span data-ttu-id="eec50-197">toolearn hello 사용 가능한 역할에 대 한 참조 [RBAC: 역할에 기본 제공](../active-directory/role-based-access-built-in-roles.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-197">toolearn about hello available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="eec50-198">Hello 범위 hello 구독, 리소스 그룹 또는 리소스의 hello 수준에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-198">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="eec50-199">권한은 상속 된 toolower 수준의 범위를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-199">Permissions are inherited toolower levels of scope.</span></span> <span data-ttu-id="eec50-200">예를 들어 있으므로 리소스 그룹에 대 한 응용 프로그램 toohello 읽기 역할 추가 읽을 수 hello 리소스 그룹 및 포함 된 모든 리소스.</span><span class="sxs-lookup"><span data-stu-id="eec50-200">For example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains.</span></span>

1. <span data-ttu-id="eec50-201">Toohello 수준의 tooassign hello 응용 프로그램을 원하는 범위를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-201">Navigate toohello level of scope you wish tooassign hello application to.</span></span> <span data-ttu-id="eec50-202">예를 들어 tooassign hello 구독 범위에서 역할 선택 **구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-202">For example, tooassign a role at hello subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="eec50-203">대신 리소스 그룹 또는 리소스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-203">You could instead select a resource group or resource.</span></span>

     ![구독 선택](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="eec50-205">Hello (리소스 그룹 또는 리소스) 특정 구독 tooassign hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-205">Select hello particular subscription (resource group or resource) tooassign hello application to.</span></span>

     ![할당을 위한 구독 선택](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="eec50-207">**액세스 제어(IAM)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-207">Select **Access Control (IAM)**.</span></span>

     ![액세스 선택](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="eec50-209">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-209">Select **Add**.</span></span>

     ![추가 선택](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="eec50-211">Tooassign toohello 응용 프로그램을 원하는 hello 역할을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-211">Select hello role you wish tooassign toohello application.</span></span> <span data-ttu-id="eec50-212">hello 다음 그림에 나와 hello **판독기** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-212">hello following image shows hello **Reader** role.</span></span>

     ![역할 선택](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="eec50-214">응용 프로그램을 검색하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-214">Search for your application, and select it.</span></span>

     ![앱 검색](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="eec50-216">선택 **확인** toofinish hello 역할을 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-216">Select **OK** toofinish assigning hello role.</span></span> <span data-ttu-id="eec50-217">해당 범위에 대 한 tooa 역할에 할당 된 사용자의 hello 목록에서 응용 프로그램을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-217">You see your application in hello list of users assigned tooa role for that scope.</span></span>

## <a name="log-in-as-hello-application"></a><span data-ttu-id="eec50-218">Hello 응용 프로그램으로 로그인</span><span class="sxs-lookup"><span data-stu-id="eec50-218">Log in as hello application</span></span>

<span data-ttu-id="eec50-219">응용 프로그램은 이제 Azure Active Directory에 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="eec50-220">ID 및 키 toouse hello 응용 프로그램으로 로그인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-220">You have an ID and key toouse for signing in as hello application.</span></span> <span data-ttu-id="eec50-221">hello 응용 프로그램에는 수행할 수 있는 특정 작업을 제공 하는 tooa 역할이 할당 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-221">hello application is assigned tooa role that gives it certain actions it can perform.</span></span> <span data-ttu-id="eec50-222">서로 다른 플랫폼을 통해 응용 프로그램 hello로 로그인 하는 방법에 대 한 정보를 보려면</span><span class="sxs-lookup"><span data-stu-id="eec50-222">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="eec50-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eec50-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="eec50-224">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eec50-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="eec50-225">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="eec50-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="eec50-226">.NET</span><span class="sxs-lookup"><span data-stu-id="eec50-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="eec50-227">Java</span><span class="sxs-lookup"><span data-stu-id="eec50-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="eec50-228">Node.JS</span><span class="sxs-lookup"><span data-stu-id="eec50-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="eec50-229">Python</span><span class="sxs-lookup"><span data-stu-id="eec50-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="eec50-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="eec50-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="eec50-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="eec50-231">Next steps</span></span>
* <span data-ttu-id="eec50-232">다중 테 넌 트 응용 프로그램을 tooset 참조 [hello Azure 리소스 관리자 API가 있는 개발자 가이드 tooauthorization](resource-manager-api-authentication.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-232">tooset up a multi-tenant application, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="eec50-233">보안 정책을 지정 하는 방법에 대 한 toolearn 참조 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-233">toolearn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="eec50-234">목록이 부여 하거나 거부 toousers 수 있는 작업에 대 한 참조 [Azure 리소스 관리자 리소스 공급자 작업](../active-directory/role-based-access-control-resource-provider-operations.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="eec50-234">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
