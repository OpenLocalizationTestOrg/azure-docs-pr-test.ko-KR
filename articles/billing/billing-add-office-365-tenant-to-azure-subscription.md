---
title: "Azure 구독 aaaUse Office 365 테 넌 트 | Microsoft Docs"
description: "자세한 내용은 방법 tooadd Office 365 디렉터리 (테 넌 트) tooan Azure 구독."
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
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="9c15c-103">Office 365 테 넌 트 tooan Azure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="9c15c-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="9c15c-104">Azure 구독에서 hello Office 365 테 넌 트에 액세스할 수 있도록 별도 Azure 및 Office 365 구독을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="9c15c-105">toolink tooAzure hello Azure 서비스 관리자 계정으로 로그인 구독 디렉터리를 추가 하 고 hello Office 365 조직 계정 toohello Azure Active Directory 테 넌 트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="9c15c-106">Azure Active Directory 인스턴스에서 사용자를 위한 Office 365 구독이 필요하거나 Office 365 계정이 있지만 Azure 계정이 없는 경우 [Office 365 계정을 사용하여 Azure에 등록](billing-use-existing-office-365-account-azure-subscription.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9c15c-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="9c15c-107">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="9c15c-107">Before you begin</span></span>
* <span data-ttu-id="9c15c-108">Azure 구독의 서비스 관리자에 게의 hello 자격 증명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="9c15c-109">공동 관리자 계정에이 문서의 hello 단계 중 일부를 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="9c15c-110">toochange 서비스 관리자에 게 참조 [어떻게 tooadd 또는 변경 Azure 관리자 역할](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="9c15c-111">Hello Office 365 테 넌 트의 전역 관리자의 hello 자격 증명이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="9c15c-112">hello Office 365 테 넌 트에 서비스 관리자에 게의 hello 전자 메일 주소 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="9c15c-113">서비스 관리자에 게 전자 메일 주소 hello hello Office 365 테 넌 트의 전역 관리자의 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="9c15c-114">Microsoft 계정과 조직 계정 되는 전자 메일 주소를 사용 하는 경우 일시적으로 변경의 Azure 구독 toouse 서비스 관리자에 게 다른 Microsoft 계정.</span><span class="sxs-lookup"><span data-stu-id="9c15c-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="9c15c-115">Hello에서 Microsoft 계정을 만들 수 있습니다 [Microsoft 계정 등록 페이지로](https://signup.live.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="9c15c-116">Office 365 테 넌 트 tooAzure 구독 연결</span><span class="sxs-lookup"><span data-stu-id="9c15c-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="9c15c-117">tooassociate hello Office 365 테 넌 트 toohello Azure 구독에는 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="9c15c-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="9c15c-118">1 단계: Office 365 테 넌 트 tooyour Azure 구독 추가</span><span class="sxs-lookup"><span data-stu-id="9c15c-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="9c15c-119">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) hello 서비스 관리자 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Azure 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="9c15c-121">Hello 왼쪽된 창에서 선택 **ACTIVE DIRECTORY**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="9c15c-122">Hello Office 365 테 넌 트를 참조 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="9c15c-123">표시, 경우 너무 건너뛸[2 단계: Azure 구독 hello와 관련 된 hello 디렉터리를 변경](#Step2)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Active Directory 항목의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="9c15c-125">**새로 만들기** > **디렉터리** > **사용자 지정 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Azure Active Directory 사용자 지정 만들기의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="9c15c-127">Hello에 **디렉터리 추가** 페이지의 **디렉터리**선택, **기존 디렉터리를 사용 하 여**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="9c15c-128">다음 선택 **지금 로그 아웃 준비 toobe 저는**를 선택 하 고 **완료** ![완료 아이콘](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    !["기존 디렉터리 사용"의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="9c15c-130">로그 아웃, Office 365 테 넌 트의 hello 전역 관리자 자격 증명을 사용 하 여 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Office 365 전역 관리자 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="9c15c-132">**계속**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-132">Select **Continue**.</span></span>
   
    ![확인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="9c15c-134">**지금 로그아웃**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-134">Select **Sign out now**.</span></span>
   
    ![로그아웃의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="9c15c-136">Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) hello 서비스 관리자 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Azure 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="9c15c-138">Hello 대시보드에서 Office 365 테 넌 트에 대해 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![대시보드의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="9c15c-140"><a name="Step2"></a>2 단계: Azure 구독 hello와 연관 된 hello 디렉터리 변경</span><span class="sxs-lookup"><span data-stu-id="9c15c-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="9c15c-141">**설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-141">Select **Settings**.</span></span>
   
    ![Azure 클래식 포털 설정 아이콘의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="9c15c-143">Azure 구독을 선택한 다음 **디렉터리 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Azure 구독 편집 디렉터리의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="9c15c-145">**다음** ![다음 아이콘](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    !["변경 관련된 디렉터리를 hello"의 스크린 샷](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="9c15c-147">영향을 받는 hello 계정을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-147">Review hello affected accounts.</span></span> <span data-ttu-id="9c15c-148">모든 공동 관리자와 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md) hello 기존 리소스 그룹에 할당 된 액세스 권한이 있는 사용자가 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="9c15c-149">만 표시 될 hello 경고 공동 관리자의 hello 제거에 언급 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![공동 관리자 계정 toobe 제거 hello를 보여 주는 스크린 샷](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![제거 하는 예에서는 사용자 계정 toobe 보여 주는 스크린 샷](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="9c15c-152">**완료** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="9c15c-153">3 단계: 공동 관리자 toohello Azure Active Directory 테 넌 트로 Office 365 조직 계정 추가</span><span class="sxs-lookup"><span data-stu-id="9c15c-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="9c15c-154">선택 hello **관리자** 탭을 선택한 다음 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Azure 클래식 포털 설정 관리자 탭의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="9c15c-156">Office 365 테 넌 트의 조직 계정을 입력 hello Azure 구독을 선택한 다음 선택 **완료** ![완료 아이콘](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Azure 공동 관리자 추가 대화 상자의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="9c15c-158">Toohello 돌아가서 **관리자** 탭 합니다. Hello 조직 계정을 공동 관리자로 표시 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![관리자 탭의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="9c15c-160">액세스 tooAzure hello 공동 관리자 계정으로 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="9c15c-161">a.</span><span class="sxs-lookup"><span data-stu-id="9c15c-161">a.</span></span> <span data-ttu-id="9c15c-162">로그 아웃 hello Azure 클래식 포털.</span><span class="sxs-lookup"><span data-stu-id="9c15c-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="9c15c-163">b.</span><span class="sxs-lookup"><span data-stu-id="9c15c-163">b.</span></span> <span data-ttu-id="9c15c-164">열기 hello [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="9c15c-165">c.</span><span class="sxs-lookup"><span data-stu-id="9c15c-165">c.</span></span> <span data-ttu-id="9c15c-166">공동 관리자에 게의 hello 자격 증명을 입력 한 다음 선택 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Azure 로그인 페이지의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="9c15c-168">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="9c15c-168">Need help?</span></span> <span data-ttu-id="9c15c-169">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="9c15c-169">Contact support.</span></span>
<span data-ttu-id="9c15c-170">도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c15c-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


