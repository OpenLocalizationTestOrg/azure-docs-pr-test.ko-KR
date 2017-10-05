---
title: "Azure 구독과 Office 365 테넌트 사용 | Microsoft Docs"
description: "Azure 구독에 Office 365 디렉터리(테넌트)를 추가하는 방법을 알아봅니다."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: 7affb4a83cdb8ababef60e786a3c824e7477ed68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a><span data-ttu-id="5b737-103">Azure 구독에 Office 365 테넌트 연결</span><span class="sxs-lookup"><span data-stu-id="5b737-103">Associate an Office 365 tenant to an Azure subscription</span></span>
<span data-ttu-id="5b737-104">Azure 구독에서 Office 365 테넌트에 액세스할 수 있도록 별도 Azure 및 Office 365 구독을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-104">Link your separate Azure and Office 365 subscriptions so that you can access the Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="5b737-105">구독을 연결하려면 Azure 서비스 관리자 계정으로 Azure에 로그인하고 디렉터리를 추가한 다음 Azure Active Directory 테넌트에 Office 365 조직 계정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-105">To link your subscriptions, sign in to Azure with the Azure service administrator account, add a directory, and add the Office 365 organizational accounts to the Azure Active Directory tenant.</span></span>

<span data-ttu-id="5b737-106">Azure Active Directory 인스턴스에서 사용자를 위한 Office 365 구독이 필요하거나 Office 365 계정이 있지만 Azure 계정이 없는 경우 [Office 365 계정을 사용하여 Azure에 등록](billing-use-existing-office-365-account-azure-subscription.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b737-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="5b737-107">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="5b737-107">Before you begin</span></span>
* <span data-ttu-id="5b737-108">Azure 구독 서비스 관리자의 자격 증명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-108">You must have the credentials of the Azure subscription service administrator.</span></span> <span data-ttu-id="5b737-109">공동 관리자 계정은 이 문서의 단계 중 일부를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-109">Co-administrator accounts can't do some of the steps in this article.</span></span> <span data-ttu-id="5b737-110">서비스 관리자를 변경하려면 [Azure 관리자 역할을 추가 또는 변경하는 방법](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5b737-110">To change your service administrator, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="5b737-111">Office 365 테넌트 전역 관리자의 자격 증명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-111">You must have the credentials of a global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="5b737-112">서비스 관리자의 전자 메일 주소가 Office 365 테넌트에 있지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-112">The email address of the service administrator must not be in the Office 365 tenant.</span></span>
* <span data-ttu-id="5b737-113">서비스 관리자의 전자 메일 주소가 Office 365 전역 관리자의 전자 메일 주소와 일치하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-113">The email address of the service administrator must not match that of any global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="5b737-114">Microsoft 계정이며 조직 계정인 전자 메일 주소를 사용하는 경우 Azure 구독의 서비스 관리자를 일시적으로 변경하여 다른 Microsoft 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change the service administrator of your Azure subscription to use another Microsoft account.</span></span> <span data-ttu-id="5b737-115">[Microsoft 계정 등록 페이지](https://signup.live.com/)에서 Microsoft 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-115">You can create a Microsoft account at the [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-to-azure-subscription"></a><span data-ttu-id="5b737-116">Azure 구독에 Office 365 테넌트 연결</span><span class="sxs-lookup"><span data-stu-id="5b737-116">Link Office 365 tenant to Azure subscription</span></span>
<span data-ttu-id="5b737-117">Azure 구독에 Office 365 테넌트를 연결하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-117">To associate the Office 365 tenant to the Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a><span data-ttu-id="5b737-118">1단계: Azure 구독에 Office 365 테넌트 추가</span><span class="sxs-lookup"><span data-stu-id="5b737-118">Step 1: Add Office 365 tenant to your Azure subscription</span></span>

1. <span data-ttu-id="5b737-119">서비스 관리자 자격 증명을 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-119">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>

    ![Azure 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="5b737-121">왼쪽 창에서 **ACTIVE DIRECTORY**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-121">In the left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="5b737-122">Office 365 테넌트가 표시되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-122">You shouldn't see the Office 365 tenant.</span></span> <span data-ttu-id="5b737-123">표시되는 경우 [2단계: Azure 구독과 연결된 디렉터리 변경](#Step2)으로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-123">If you see it, skip to [Step 2: Change the directory associated with the Azure subscription](#Step2).</span></span>
   
   ![Active Directory 항목의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="5b737-125">**새로 만들기** > **디렉터리** > **사용자 지정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Azure Active Directory 사용자 지정 만들기의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="5b737-127">**디렉터리 추가** 페이지의 **디렉터리**아래에서 **기존 디렉터리 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-127">On the **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="5b737-128">그런 다음 **로그아웃할 준비가 되었습니다**를 선택하고 **완료** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-128">Then select **I am ready to be signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    !["기존 디렉터리 사용"의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="5b737-130">로그인한 후에 Office 365 테넌트 전역 관리자의 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-130">After you are signed out, sign in with the global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Office 365 전역 관리자 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="5b737-132">**계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-132">Select **Continue**.</span></span>
   
    ![확인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="5b737-134">**지금 로그아웃**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-134">Select **Sign out now**.</span></span>
   
    ![로그아웃의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="5b737-136">서비스 관리자 자격 증명을 사용하여 [Azure 클래식 포털](https://manage.windowsazure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>
   
    ![Azure 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="5b737-138">대시보드에서 Office 365 테넌트가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-138">You should see your Office 365 tenant in the dashboard.</span></span>
   
    ![대시보드의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="5b737-140"><a name="Step2"></a>2단계: Azure 구독과 연결된 디렉터리 변경</span><span class="sxs-lookup"><span data-stu-id="5b737-140"><a name="Step2"></a>Step 2: Change the directory associated with the Azure subscription</span></span>
   
1. <span data-ttu-id="5b737-141">**설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-141">Select **Settings**.</span></span>
   
    ![Azure 클래식 포털 설정 아이콘의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="5b737-143">Azure 구독을 선택한 다음 **디렉터리 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Azure 구독 편집 디렉터리의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="5b737-145">**다음** ![다음 아이콘](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    !["연결된 디렉터리 변경"의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="5b737-147">영향을 받는 계정을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-147">Review the affected accounts.</span></span> <span data-ttu-id="5b737-148">또한 기존 리소스 그룹에 할당된 액세스 권한이 있는 모든 공동 관리자 및 [RBAC(역할 기반 액세스 제어)](../active-directory/role-based-access-control-configure.md) 사용자도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in the existing resource groups are removed.</span></span> <span data-ttu-id="5b737-149">받은 경고에서는 공동 관리자를 제거하라는 메시지만을 언급합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-149">The warning you receive only mentions the removal of co-administrators.</span></span>
      
    ![제거할 공동 관리자 계정을 보여 주는 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![제거할 예제 사용자 계정을 보여 주는 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="5b737-152">**완료** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a><span data-ttu-id="5b737-153">3단계: Office 365 조직 계정을 Azure Active Directory 테넌트에 공동 관리자로 추가</span><span class="sxs-lookup"><span data-stu-id="5b737-153">Step 3: Add your Office 365 organizational accounts as co-administrators to the Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="5b737-154">**관리자** 탭을 선택한 다음 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-154">Select the **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Azure 클래식 포털 설정 관리자 탭의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="5b737-156">Office 365 테넌트의 조직 계정을 입력하고 Azure 구독을 선택한 다음 **완료** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-156">Enter an organizational account of your Office 365 tenant, select the Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Azure 공동 관리자 추가 대화 상자의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="5b737-158">**관리자** 탭으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-158">Go back to the **ADMINISTRATORS** tab.</span></span> <span data-ttu-id="5b737-159">공동 관리자 권한으로 표시된 조직 계정을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-159">You should see the organizational account displayed as co-administrator.</span></span>
   
    ![관리자 탭의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="5b737-161">공동 관리자 계정을 사용하여 Azure에 대한 액세스를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-161">Test access to Azure with the co-administrator account.</span></span>
   
    <span data-ttu-id="5b737-162">a.</span><span class="sxs-lookup"><span data-stu-id="5b737-162">a.</span></span> <span data-ttu-id="5b737-163">Azure 클래식 포털에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-163">Sign out of the Azure classic portal.</span></span>
   
    <span data-ttu-id="5b737-164">b.</span><span class="sxs-lookup"><span data-stu-id="5b737-164">b.</span></span> <span data-ttu-id="5b737-165">[Azure 포털](https://portal.azure.com/)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-165">Open the [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="5b737-166">c.</span><span class="sxs-lookup"><span data-stu-id="5b737-166">c.</span></span> <span data-ttu-id="5b737-167">공동 관리자의 자격 증명을 입력한 다음 **로그인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5b737-167">Enter the credentials of the co-administrator, and then select **Sign in**.</span></span>
   
    ![Azure 로그인 페이지의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="5b737-169">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="5b737-169">Need help?</span></span> <span data-ttu-id="5b737-170">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5b737-170">Contact support.</span></span>
<span data-ttu-id="5b737-171">다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="5b737-171">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>


