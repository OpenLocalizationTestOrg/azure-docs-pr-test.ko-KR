---
title: "포털에서 Azure 앱에 대한 ID 만들기 | Microsoft Docs"
description: "Azure Resource Manager에서 리소스에 대한 액세스를 관리하기 위해 역할 기반 액세스 제어와 함께 사용할 수 있는 새 Azure Active Directory 응용 프로그램 및 서비스 주체를 만드는 방법을 설명합니다."
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
ms.openlocfilehash: 5d24fb99e1095d53e5ea547e53b80178d9cb77c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="15ac3-103">포털을 사용하여 리소스에 액세스할 수 있는 Azure Active Directory 응용 프로그램 및 서비스 주체 만들기</span><span class="sxs-lookup"><span data-stu-id="15ac3-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="15ac3-104">리소스를 액세스하거나 수정해야 하는 응용 프로그램이 있는 경우 Azure AD(Active Directory) 응용 프로그램을 설정하고 필수 사용 권한을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-104">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span></span> <span data-ttu-id="15ac3-105">이 방법은 다음의 이유로 사용자 고유의 자격 증명을 사용하여 앱을 실행하는 데 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-105">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="15ac3-106">자체 사용 권한과 다른 앱 ID에 대한 사용 권한을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-106">You can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="15ac3-107">일반적으로 이러한 권한은 정확히 앱 실행에 필요한 것으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-107">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="15ac3-108">책임이 변경되면 앱의 자격 증명을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-108">You do not have to change the app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="15ac3-109">무인 스크립트를 실행할 때 인증서를 사용하여 인증을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-109">You can use a certificate to automate authentication when executing an unattended script.</span></span>

<span data-ttu-id="15ac3-110">이 토픽에서는 포털을 통해 이러한 단계를 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-110">This topic shows you how to perform those steps through the portal.</span></span> <span data-ttu-id="15ac3-111">여기서는 응용 프로그램을 하나의 조직 내에서만 실행하게 되는 단일 테넌트 응용 프로그램을 중점적으로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-111">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="15ac3-112">일반적으로 단일 조직 내에서 실행되는 LOB(기간 업무) 응용 프로그램에 대해 단일 테넌트 응용 프로그램을 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-112">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="15ac3-113">필요한 사용 권한</span><span class="sxs-lookup"><span data-stu-id="15ac3-113">Required permissions</span></span>
<span data-ttu-id="15ac3-114">이 토픽을 완료하려면 Azure AD 테넌트에 응용 프로그램을 등록하고 Azure 구독의 역할에 응용 프로그램을 할당하기 위한 충분한 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-114">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="15ac3-115">이러한 단계를 수행하기 위한 올바른 권한이 있는지 확인해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-115">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="15ac3-116">Azure Active Directory 권한 확인</span><span class="sxs-lookup"><span data-stu-id="15ac3-116">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="15ac3-117">[Azure Portal](https://portal.azure.com)을 통해 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-117">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="15ac3-118">**Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-118">Select **Azure Active Directory**.</span></span>

     ![Azure Active Directory 선택](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="15ac3-120">Azure Active Directory에서 **사용자 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-120">In Azure Active Directory, select **User settings**.</span></span>

     ![사용자 설정 선택](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="15ac3-122">**앱 등록** 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-122">Check the **App registrations** setting.</span></span> <span data-ttu-id="15ac3-123">**예**로 설정된 경우 관리자가 아닌 사용자가 AD 앱을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-123">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="15ac3-124">이 설정에서는 Azure AD 테넌트의 모든 사용자가 앱을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-124">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="15ac3-125">[Azure 구독 권한 확인](#check-azure-subscription-permissions)을 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-125">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![앱 등록 보기](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="15ac3-127">앱 등록 설정이 **아니요**로 설정되어 있으면 관리자만 앱을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-127">If the app registrations setting is set to **No**, only admin users can register apps.</span></span> <span data-ttu-id="15ac3-128">사용자 계정이 Azure AD 테넌트에 대한 관리자인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-128">You need to check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="15ac3-129">빠른 작업에서 **개요** 및 **사용자 찾기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-129">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![사용자 찾기](./media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="15ac3-131">사용자 계정을 검색하고, 찾으면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-131">Search for your account, and select it when you find it.</span></span>

     ![사용자 검색](./media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="15ac3-133">사용자 계정에 대해 **디렉터리 역할**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-133">For your account, select **Directory role**.</span></span> 

     ![디렉터리 역할](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="15ac3-135">Azure AD에서 할당된 디렉터리 역할을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-135">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="15ac3-136">계정이 사용자 역할에 할당되어 있으나 앱 등록 설정(이전 단계)이 관리자로 제한되어 있으면 관리자에게 사용자를 관리자 역할로 할당하거나 사용자가 앱을 등록할 수 있게 설정하도록 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-136">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

     ![역할 보기](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="15ac3-138">Azure 구독 권한 확인</span><span class="sxs-lookup"><span data-stu-id="15ac3-138">Check Azure subscription permissions</span></span>
<span data-ttu-id="15ac3-139">Azure 구독에서 사용자 계정에 AD 앱을 역할에 할당할 수 있는 `Microsoft.Authorization/*/Write` 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-139">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="15ac3-140">이 작업에 대한 권한은 [소유자](../active-directory/role-based-access-built-in-roles.md#owner) 역할 또는 [사용자 액세스 관리자](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) 역할을 통해 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-140">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="15ac3-141">계정이 **참가자** 역할에 할당된 경우 적절한 사용 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-141">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="15ac3-142">서비스 주체를 역할에 할당하려고 하면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-142">You will receive an error when attempting to assign the service principal to a role.</span></span> 

<span data-ttu-id="15ac3-143">Azure 구독 권한을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="15ac3-143">To check your subscription permissions:</span></span>

1. <span data-ttu-id="15ac3-144">이전 단계에서 Azure AD 계정을 아직 확인하지 않은 경우 왼쪽 창에서 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-144">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span></span>

2. <span data-ttu-id="15ac3-145">Azure AD 계정을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-145">Find your Azure AD account.</span></span> <span data-ttu-id="15ac3-146">빠른 작업에서 **개요** 및 **사용자 찾기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-146">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![사용자 찾기](./media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="15ac3-148">사용자 계정을 검색하고, 찾으면 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-148">Search for your account, and select it when you find it.</span></span>

     ![사용자 검색](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="15ac3-150">**Azure 리소스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-150">Select **Azure resources**.</span></span>

     ![리소스 선택](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="15ac3-152">할당된 사용자 역할을 확인하고 AD 앱을 역할에 할당하기 위한 적절한 권한이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-152">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="15ac3-153">이러한 권한이 없으면 구독 관리자에게 사용자 액세스 관리자 역할에 사용자를 추가할 것을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-153">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="15ac3-154">다음 그림에서 사용자에게는 2개의 구독에 대한 소유자 역할이 할당됩니다. 즉, 사용자에게는 적절한 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-154">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![권한 표시](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="15ac3-156">Azure Active Directory 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="15ac3-156">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="15ac3-157">[Azure Portal](https://portal.azure.com)을 통해 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-157">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="15ac3-158">**Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-158">Select **Azure Active Directory**.</span></span>

     ![Azure Active Directory 선택](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="15ac3-160">**앱 등록**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-160">Select **App registrations**.</span></span>   

     ![앱 등록 선택](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="15ac3-162">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-162">Select **Add**.</span></span>

     ![앱 추가](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="15ac3-164">응용 프로그램에 대한 이름 및 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-164">Provide a name and URL for the application.</span></span> <span data-ttu-id="15ac3-165">만들려는 응용 프로그램 유형으로 **웹앱/API** 또는 **네이티브**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-165">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="15ac3-166">값을 설정한 후 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-166">After setting the values, select **Create**.</span></span>

     ![응용 프로그램 이름 지정](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="15ac3-168">응용 프로그램이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-168">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="15ac3-169">응용 프로그램 ID 및 인증 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="15ac3-169">Get application ID and authentication key</span></span>
<span data-ttu-id="15ac3-170">프로그래밍 방식으로 로그인하는 경우 응용 프로그램에 대한 ID 및 인증 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-170">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="15ac3-171">이러한 값을 가져오려면 다음 단계를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-171">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="15ac3-172">Azure Active Directory의 **앱 등록**에서 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-172">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![응용 프로그램 선택](./media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="15ac3-174">**응용 프로그램 ID**를 복사하고 응용 프로그램 코드에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-174">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="15ac3-175">[샘플 응용 프로그램](#sample-applications) 섹션의 응용 프로그램은 이 값을 클라이언트 ID로 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-175">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![클라이언트 ID](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="15ac3-177">인증 키를 생성하려면 **키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-177">To generate an authentication key, select **Keys**.</span></span>

     ![키 선택](./media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="15ac3-179">키에 대한 설명 및 키의 기간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-179">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="15ac3-180">완료되면 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-180">When done, select **Save**.</span></span>

     ![키 저장](./media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="15ac3-182">키를 저장하면 키 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-182">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="15ac3-183">나중에 키를 검색할 수 없으므로 이 값을 복사해둡니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-183">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="15ac3-184">응용 프로그램으로 로그인하려면 응용 프로그램 ID와 함께 키 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-184">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="15ac3-185">응용 프로그램에서 검색할 수 있는 위치에 키 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-185">Store the key value where your application can retrieve it.</span></span>

     ![공유 키](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="15ac3-187">테넌트 ID 가져오기</span><span class="sxs-lookup"><span data-stu-id="15ac3-187">Get tenant ID</span></span>
<span data-ttu-id="15ac3-188">프로그래밍 방식으로 로그인하는 경우 인증 요청과 함께 테넌트 ID를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-188">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="15ac3-189">테넌트 ID를 가져오려면 Azure AD 테넌트에 대한 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-189">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![Azure AD 속성 선택](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="15ac3-191">**디렉터리 ID**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-191">Copy the **Directory ID**.</span></span> <span data-ttu-id="15ac3-192">이 값은 테넌트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-192">This value is your tenant ID.</span></span>

     ![테넌트 ID](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="15ac3-194">응용 프로그램을 역할에 할당</span><span class="sxs-lookup"><span data-stu-id="15ac3-194">Assign application to role</span></span>
<span data-ttu-id="15ac3-195">구독의 리소스에 액세스하려면 역할에 응용 프로그램을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-195">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="15ac3-196">응용 프로그램에 적합한 사용 권한을 나타내는 역할을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-196">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="15ac3-197">사용 가능한 역할에 대해 알아보려면 [RBAC: 기본 제공 역할](../active-directory/role-based-access-built-in-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ac3-197">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="15ac3-198">구독, 리소스 그룹 또는 리소스 수준에서 범위를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-198">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="15ac3-199">권한은 하위 수준의 범위로 상속됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-199">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="15ac3-200">예를 들어 응용 프로그램에 리소스 그룹에 대한 읽기 권한자 역할을 추가하면 응용 프로그램이 리소스 그룹과 그 안에 포함된 모든 리소스를 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-200">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="15ac3-201">응용 프로그램을 할당하려는 범위 수준으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-201">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="15ac3-202">예를 들어 구독 범위에서 역할을 할당하려면 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-202">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="15ac3-203">대신 리소스 그룹 또는 리소스를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-203">You could instead select a resource group or resource.</span></span>

     ![구독 선택](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="15ac3-205">응용 프로그램을 할당할 특정 구독(리소스 그룹 또는 리소스)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-205">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![할당을 위한 구독 선택](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="15ac3-207">**액세스 제어(IAM)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-207">Select **Access Control (IAM)**.</span></span>

     ![액세스 선택](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="15ac3-209">**추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-209">Select **Add**.</span></span>

     ![추가 선택](./media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="15ac3-211">응용 프로그램에 할당할 역할을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-211">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="15ac3-212">다음 이미지에서는 **읽기 권한자** 역할을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-212">The following image shows the **Reader** role.</span></span>

     ![역할 선택](./media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="15ac3-214">응용 프로그램을 검색하고 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-214">Search for your application, and select it.</span></span>

     ![앱 검색](./media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="15ac3-216">**확인**을 선택하여 역할 할당을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-216">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="15ac3-217">목록에서 해당 범위에 대한 역할에 할당된 사용자 목록에 응용 프로그램이 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-217">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="log-in-as-the-application"></a><span data-ttu-id="15ac3-218">응용 프로그램으로 로그인</span><span class="sxs-lookup"><span data-stu-id="15ac3-218">Log in as the application</span></span>

<span data-ttu-id="15ac3-219">응용 프로그램은 이제 Azure Active Directory에 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-219">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="15ac3-220">응용 프로그램으로 로그인하는 데 사용할 ID와 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-220">You have an ID and key to use for signing in as the application.</span></span> <span data-ttu-id="15ac3-221">응용 프로그램은 수행할 수 있는 특정 작업을 제공하는 역할에 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="15ac3-221">The application is assigned to a role that gives it certain actions it can perform.</span></span> <span data-ttu-id="15ac3-222">다른 플랫폼을 통해 응용 프로그램으로 로그인하는 방법에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ac3-222">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="15ac3-223">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15ac3-223">PowerShell</span></span>](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [<span data-ttu-id="15ac3-224">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15ac3-224">Azure CLI</span></span>](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [<span data-ttu-id="15ac3-225">REST (영문)</span><span class="sxs-lookup"><span data-stu-id="15ac3-225">REST</span></span>](/rest/api/#create-the-request)
* [<span data-ttu-id="15ac3-226">.NET</span><span class="sxs-lookup"><span data-stu-id="15ac3-226">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="15ac3-227">Java</span><span class="sxs-lookup"><span data-stu-id="15ac3-227">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="15ac3-228">Node.JS</span><span class="sxs-lookup"><span data-stu-id="15ac3-228">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="15ac3-229">Python</span><span class="sxs-lookup"><span data-stu-id="15ac3-229">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="15ac3-230">Ruby</span><span class="sxs-lookup"><span data-stu-id="15ac3-230">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a><span data-ttu-id="15ac3-231">다음 단계</span><span class="sxs-lookup"><span data-stu-id="15ac3-231">Next steps</span></span>
* <span data-ttu-id="15ac3-232">다중 테넌트 응용 프로그램을 설정하려면 [Azure Resource Manager API를 사용한 권한 부여 개발자 가이드](resource-manager-api-authentication.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ac3-232">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="15ac3-233">보안 정책 지정에 대해 자세히 알아보려면 [Azure 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ac3-233">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  
* <span data-ttu-id="15ac3-234">권한이 부여되거나 사용자에 대해 거부될 수 있는 작업 목록은 [Azure Resource Manager 리소스 공급자 작업](../active-directory/role-based-access-control-resource-provider-operations.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15ac3-234">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
