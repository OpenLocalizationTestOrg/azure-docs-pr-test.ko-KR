---
title: "Azure 관리자 구독 역할 추가 또는 변경 | Microsoft Docs"
description: "Azure 공동 관리자, 서비스 관리자 및 계정 관리자를 추가 또는 변경하는 방법에 대해 설명합니다."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: da5995535d42ed52772cb09e0f4da51bbf878748
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-the-subscription-or-services"></a><span data-ttu-id="5e2bb-103">구독 또는 서비스를 관리하는 Azure 관리자 역할 추가 또는 변경</span><span class="sxs-lookup"><span data-stu-id="5e2bb-103">Add or change Azure administrator roles that manage the subscription or services</span></span>
<span data-ttu-id="5e2bb-104">구독에서 사용되는 Azure 구독을 관리하거나 Azure 서비스를 관리하는 Azure 관리자를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-104">You can change the Azure administrator that manages your Azure subscription or manages the Azure services used in your subscription.</span></span> <span data-ttu-id="5e2bb-105">Azure 청구 정보를 보고 구독을 관리하려면 [계정 센터](https://account.windowsazure.com/Home/Index)에 계정 관리자로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-105">To view Azure billing information and manage subscriptions, you must sign in to the [Account Center](https://account.windowsazure.com/Home/Index) as the Account Administrator.</span></span> 

## <a name="add-an-admin-for-a-subscription"></a><span data-ttu-id="5e2bb-106">구독에 대한 관리자 추가</span><span class="sxs-lookup"><span data-stu-id="5e2bb-106">Add an admin for a subscription</span></span>
<span data-ttu-id="5e2bb-107">Azure Portal 또는 Azure 클래식 포털에서 Azure 관리자를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-107">You can add an Azure administrator in the Azure portal or in the Azure classic portal.</span></span>

<span data-ttu-id="5e2bb-108">**Azure Portal**</span><span class="sxs-lookup"><span data-stu-id="5e2bb-108">**Azure portal**</span></span>

<span data-ttu-id="5e2bb-109">Azure Portal에서 누군가를 구독의 관리자로 추가하려면 그 사용자에게 소유자 역할을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-109">To add someone as an admin for a subscription in the Azure portal, you give them the owner role.</span></span> <span data-ttu-id="5e2bb-110">소유자 역할은 할당된 구독의 리소스만 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-110">The owner role can only manage the resources in the subscription that you assigned.</span></span> <span data-ttu-id="5e2bb-111">이 역할에는 다른 구독에 대한 액세스 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-111">It doesn't have access privilege to other subscriptions.</span></span> <span data-ttu-id="5e2bb-112">[Azure Portal](https://portal.azure.com)을 통해 추가한 소유자는 [Azure 클래식 포털](https://manage.windowsazure.com)에서 서비스를 관리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-112">The owners you add through the [Azure portal](https://portal.azure.com) can't manage resource in the [Azure classic portal](https://manage.windowsazure.com).</span></span>

1. <span data-ttu-id="5e2bb-113">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-113">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5e2bb-114">허브 메뉴에서 **구독** > *관리자가 액세스할 구독*에서 서비스를 관리할 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-114">On the Hub menu, select **Subscription** > *the subscription that you want the admin to access*.</span></span>

    ![선택한 구독을 보여 주는 스크린샷](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. <span data-ttu-id="5e2bb-116">구독 블레이드에서 **액세스 제어(IAM)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-116">In the subscription blade, select **Access control (IAM)**.</span></span>
4. <span data-ttu-id="5e2bb-117">**추가** > **역할** > **소유자**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-117">Select **Add** > **Role** > **Owner**.</span></span> <span data-ttu-id="5e2bb-118">소유자로 추가하려는 사용자의 메일 주소를 입력하고 사용자를 선택한 후 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-118">Type the email address of the user you want to add as owner, select the user, and then select **Save**.</span></span>

    ![선택한 소유자 역할을 보여 주는 스크린샷](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. <span data-ttu-id="5e2bb-120">소유자 계정을 공동 관리자로 추가하려는 경우 **액세스 제어(IAM)** 페이지에서 사용자를 마우스 오른쪽 단추로 클릭한 다음 **공동 관리자로 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-120">If you want to add the owner account as co-administrator, in the  **Access control (IAM)** page, right-click the user and then select **Add as co-administrator**.</span></span> <span data-ttu-id="5e2bb-121">이 기능은 이제 [Azure 미리 보기 포털](https://preview.portal.azure.com/)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-121">This feature is now available on [Azure preview portal](https://preview.portal.azure.com/).</span></span> 

     ![공동 관리자를 추가하는 스크린샷](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    ><span data-ttu-id="5e2bb-123">[Azure 클래식 포털](https://manage.windowsazure.com/)에서 Azure 서비스를 관리해야 하는 경우 "소유자" 사용자를 공동 관리자로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-123">You will need to add the "Owner" user as co-administrator if the user needs to manage the Azure services in [Azure classic portal](https://manage.windowsazure.com/).</span></span>

    <span data-ttu-id="5e2bb-124">공동 관리자 권한을 제거하려면 "공동 관리자" 사용자를 마우스 오른쪽 단추로 클릭한 다음 **공동 관리자 제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-124">To remove the co-administrator permission, right-click the "co-administrator" user and then select **Remove co-administrator**.</span></span>

    ![공동 관리자를 제거하는 스크린샷](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


<span data-ttu-id="5e2bb-126">**Azure 클래식 포털**</span><span class="sxs-lookup"><span data-stu-id="5e2bb-126">**Azure classic portal**</span></span>

1. <span data-ttu-id="5e2bb-127">[Azure 클래식 포털](https://manage.windowsazure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-127">Sign in to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="5e2bb-128">탐색 창에서 **설정**> **관리자**> **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-128">In the navigation pane, select **Settings**> **Administrators**> **Add**.</span></span> </br>

    ![추가 단추를 찾는 방법을 보여 주는 스크린샷](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. <span data-ttu-id="5e2bb-130">공동 관리자로 추가하려는 사람의 메일 주소를 입력한 다음 공동 관리자가 액세스하기를 원하는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-130">Type the email address of the person you want to add as Co-administrator and then select the subscription that you want the Co-administrator to access.</span></span></br>

    ![<span data-ttu-id="5e2bb-131">선택한 구독을 보여 주는 스크린샷</span><span class="sxs-lookup"><span data-stu-id="5e2bb-131">Screenshot that shows a subscription selected</span></span> ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

<span data-ttu-id="5e2bb-132">다음 메일 주소를 공동 관리자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-132">The following email address can be added as a Co-Administrator:</span></span>

* <span data-ttu-id="5e2bb-133">**Microsoft 계정**(이전 Windows Live ID)</span><span class="sxs-lookup"><span data-stu-id="5e2bb-133">**Microsoft Account** (formerly Windows Live ID)</span></span> </br>
  <span data-ttu-id="5e2bb-134">Microsoft 계정을 사용하여 Outlook(Hotmail), Skype(MSN), OneDrive, Windows Phone 및 Xbox LIVE와 같은 모든 소비자 지향 Microsoft 제품 및 클라우드 서비스에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-134">You can use a Microsoft Account to sign in to all consumer-oriented Microsoft products and cloud services, such as Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone, and Xbox LIVE.</span></span>
* <span data-ttu-id="5e2bb-135">**Organizational account**</span><span class="sxs-lookup"><span data-stu-id="5e2bb-135">**Organizational account**</span></span></br>
  <span data-ttu-id="5e2bb-136">조직 계정은 Azure Active Directory에 만들어지는 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-136">An organizational account is an account that is created under Azure Active Directory.</span></span> <span data-ttu-id="5e2bb-137">조직 계정 주소 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-137">The organizational account address has this format:</span></span>

    <span data-ttu-id="5e2bb-138">user@&lt;도메인&gt;.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="5e2bb-138">user@&lt;your domain&gt;.onmicrosoft.com</span></span>

## <a name="change-service-administrator-for-a-subscription"></a><span data-ttu-id="5e2bb-139">구독에 대한 서비스 관리자 변경</span><span class="sxs-lookup"><span data-stu-id="5e2bb-139">Change Service Administrator for a subscription</span></span>
<span data-ttu-id="5e2bb-140">계정 관리자만 구독에 대한 서비스 관리자를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-140">Only the Account Administrator can change the Service Administrator for a subscription.</span></span>

1. <span data-ttu-id="5e2bb-141">[Azure 계정 센터](https://account.windowsazure.com/subscriptions)에 계정 관리자를 사용하여 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-141">Sign in to [Azure Account Center](https://account.windowsazure.com/subscriptions) by using the Account Administrator.</span></span>
2. <span data-ttu-id="5e2bb-142">변경하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-142">Select the subscription you want to change.</span></span>
3. <span data-ttu-id="5e2bb-143">오른쪽에서 **구독 세부 사항 편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-143">On the right side, select **Edit subscription** details.</span></span> </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. <span data-ttu-id="5e2bb-145">**서비스 관리자** 상자에서 새 서비스 관리자의 메일 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-145">In the **SERVICE ADMINISTRATOR** box, enter the email address of the new Service Administrator.</span></span> </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-the-account-administrator"></a><span data-ttu-id="5e2bb-147">계정 관리자 변경</span><span class="sxs-lookup"><span data-stu-id="5e2bb-147">Change the Account Administrator</span></span>
<span data-ttu-id="5e2bb-148">Azure 계정의 소유권을 다른 계정에 양도하려면 [Azure 구독의 소유권 양도](billing-subscription-transfer.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-148">To transfer ownership of the Azure account to another account, see [Transferring Ownership of an Azure subscription](billing-subscription-transfer.md).</span></span>

<span data-ttu-id="5e2bb-149">계정 관리자의 전자 메일 주소를 삭제하거나 이름을 변경하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-149">We strongly recommend that you don't delete or rename the Account Administrator's email address.</span></span> <span data-ttu-id="5e2bb-150">Azure 계정에서 예기치 않은 또는 원하지 않는 동작이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-150">You may see unexpected and undesirable behavior with the Azure account.</span></span> <span data-ttu-id="5e2bb-151">해당 계정을 사용하여 Azure에 로그인하거나 해당 계정을 변경하거나 해당 계정을 사용하여 리소스를 관리할 수 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-151">You may not be able sign-in to Azure with that account, make changes to the account, or manage resources with that account.</span></span> 

## <a name="check-the-account-administrator-of-the-subscription"></a><span data-ttu-id="5e2bb-152">구독의 계정 관리자 확인</span><span class="sxs-lookup"><span data-stu-id="5e2bb-152">Check the Account Administrator of the subscription</span></span>
<span data-ttu-id="5e2bb-153">구독에 대한 계정 관리자를 잘 모를 경우 다음 단계를 사용하여 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-153">If you're not sure who the account administrator is for your subscription, use the following steps to find out.</span></span>

  1. <span data-ttu-id="5e2bb-154">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
  2. <span data-ttu-id="5e2bb-155">허브 메뉴에서 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-155">On the Hub menu, select **Subscription**.</span></span>
  3. <span data-ttu-id="5e2bb-156">확인하려는 구독을 선택한 다음 **설정**에서 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-156">Select the subscription you want to check, and then look under **Settings**.</span></span>
  4. <span data-ttu-id="5e2bb-157">**속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-157">Select **Properties**.</span></span> <span data-ttu-id="5e2bb-158">구독의 계정 관리자는 **계정 관리자** 상자에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-158">The account administrator of the subscription is displayed in the **Account Admin** box.</span></span>  

## <a name="types-of-azure-admin-accounts"></a><span data-ttu-id="5e2bb-159">Azure 관리자 계정 유형</span><span class="sxs-lookup"><span data-stu-id="5e2bb-159">Types of Azure admin accounts</span></span>
 <span data-ttu-id="5e2bb-160">계정 관리자, 서비스 관리자 및 공동 관리자가 Microsoft Azure에서 세 가지 유형의 관리자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-160">Account Administrator, Service Administrator, and Co-administrator are the three kinds of administrator roles in Microsoft Azure.</span></span> <span data-ttu-id="5e2bb-161">다음 표에서는 이러한 세 가지 관리 역할의 차이점을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-161">The following table describes the difference between these three administrative roles.</span></span>

| <span data-ttu-id="5e2bb-162">관리 역할</span><span class="sxs-lookup"><span data-stu-id="5e2bb-162">Administrative role</span></span> | <span data-ttu-id="5e2bb-163">제한</span><span class="sxs-lookup"><span data-stu-id="5e2bb-163">Limit</span></span> | <span data-ttu-id="5e2bb-164">설명</span><span class="sxs-lookup"><span data-stu-id="5e2bb-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5e2bb-165">계정 관리자(AA)</span><span class="sxs-lookup"><span data-stu-id="5e2bb-165">Account Administrator (AA)</span></span> |<span data-ttu-id="5e2bb-166">Azure 계정당 1개</span><span class="sxs-lookup"><span data-stu-id="5e2bb-166">1 per Azure account</span></span> |<span data-ttu-id="5e2bb-167">Azure 구독을 등록했거나 구입했고, [계정 센터](https://account.windowsazure.com/Home/Index) 에 액세스하여 다양한 관리 작업을 수행할 권한이 부여된 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-167">This is the person who signed up for or bought Azure subscriptions, and is authorized to access the [Account Center](https://account.windowsazure.com/Home/Index) and perform various management tasks.</span></span> <span data-ttu-id="5e2bb-168">이러한 관리 작업에는 구독 만들기, 구독 취소, 구독에 대한 대금 청구 변경 및 서비스 관리자 변경이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-168">These include being able to create subscriptions, cancel subscriptions, change the billing for a subscription, and change the Service Administrator.</span></span> |
| <span data-ttu-id="5e2bb-169">서비스 관리자(SA)</span><span class="sxs-lookup"><span data-stu-id="5e2bb-169">Service Administrator (SA)</span></span> |<span data-ttu-id="5e2bb-170">Azure 구독당 1개</span><span class="sxs-lookup"><span data-stu-id="5e2bb-170">1 per Azure subscription</span></span> |<span data-ttu-id="5e2bb-171">이 역할은 [Azure 포털](https://portal.azure.com)에서 서비스를 관리할 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-171">This role is authorized to manage services in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5e2bb-172">기본적으로 새 구독의 경우 계정 관리자가 서비스 관리자이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-172">By default, for a new subscription, the Account Administrator is also the Service Administrator.</span></span> |
| <span data-ttu-id="5e2bb-173">[Azure 클래식 포털](https://manage.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="5e2bb-173">Co-administrator (CA) in the [Azure classic portal](https://manage.windowsazure.com)</span></span> |<span data-ttu-id="5e2bb-174">구독당 200</span><span class="sxs-lookup"><span data-stu-id="5e2bb-174">200 per subscription</span></span> |<span data-ttu-id="5e2bb-175">서비스 관리자와 동일한 액세스 권한이 있지만 Azure 디렉터리에 대한 구독의 연결을 변경할 수는 없는 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-175">This role has the same access privileges as the Service Administrator, but can’t change the association of subscriptions to Azure directories.</span></span> |

<span data-ttu-id="5e2bb-176">Azure Active Directory RBAC(역할 기반 액세스 제어)를 사용하면 사용자를 여러 역할에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-176">Azure Active Directory Role-based Access Control (RBAC) allows users to be added to multiple roles.</span></span> <span data-ttu-id="5e2bb-177">자세한 내용은 [Azure Active Directory 역할 기반 액세스 제어](../active-directory/role-based-access-control-configure.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-177">For more information, see [Azure Active Directory Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

## <a name="limitations-and-restrictions-for-admin-accounts"></a><span data-ttu-id="5e2bb-178">관리자 계정에 대한 제한 사항</span><span class="sxs-lookup"><span data-stu-id="5e2bb-178">Limitations and restrictions for admin accounts</span></span>
* <span data-ttu-id="5e2bb-179">구독은 각각 Azure AD 디렉터리(기본 디렉터리라고도 함)와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-179">Each subscription is associated with an Azure AD directory (also known as the Default Directory).</span></span> <span data-ttu-id="5e2bb-180">구독이 연결된 기본 디렉터리를 찾으려면 [Azure 클래식 포털](https://manage.windowsazure.com/)로 이동하여 **설정** > **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-180">To find the Default Directory the subscription is associated with, go to the [Azure classic portal](https://manage.windowsazure.com/), select **Settings** > **Subscriptions**.</span></span> <span data-ttu-id="5e2bb-181">구독 ID를 확인하여 기본 디렉터리를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-181">Check the subscription ID to find the Default Directory.</span></span>
* <span data-ttu-id="5e2bb-182">Microsoft 계정으로 로그인하는 경우 다른 Microsoft 계정 또는 기본 디렉터리 내의 사용자를 공동 관리자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-182">If you are signed in with a Microsoft Account, you can only add other Microsoft Accounts or users within the Default Directory as Co-Administrator.</span></span>
* <span data-ttu-id="5e2bb-183">조직 계정으로 로그인하는 경우 해당 조직의 다른 조직 계정을 공동 관리자로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-183">If you are signed in with an organizational account, you can add other organizational accounts in your organization as Co-Administrator.</span></span> <span data-ttu-id="5e2bb-184">예를 들어 abby@contoso.com은 bob@contoso.com을 서비스 관리자 또는 공동 관리자로 추가할 수 있지만 john@notcontoso.com이 기본 디렉터리에 있지 않으면 john@notcontoso.com은 추가할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-184">For example, abby@contoso.com can add bob@contoso.com as Service Administrator or Co-Administrator, but can't add john@notcontoso.com unless john@notcontoso.com is in Default Directory.</span></span> <span data-ttu-id="5e2bb-185">조직 계정을 사용하여 로그인한 사용자는 Microsoft 계정 사용자를 서비스 관리자 또는 공동 관리자로 계속해서 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-185">Users signed in with organizational accounts can continue to add Microsoft Account users as Service Administrator or Co-Administrator.</span></span>
* <span data-ttu-id="5e2bb-186">이제 조직 계정으로 Azure에 로그인할 수 있으므로 서비스 관리자 및 공동 관리자 계정 요구 사항이 다음과 같이 변경되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-186">Now that it is possible to sign in to Azure with an organizational account, here are the changes to Service Administrator and Co-administrator account requirements:</span></span>

  | <span data-ttu-id="5e2bb-187">로그인 방법</span><span class="sxs-lookup"><span data-stu-id="5e2bb-187">Sign in Method</span></span> | <span data-ttu-id="5e2bb-188">기본 디렉터리 내에서 Microsoft 계정 또는 사용자를 CA 또는 SA로 추가하나요?</span><span class="sxs-lookup"><span data-stu-id="5e2bb-188">Add Microsoft Account or users within Default Directory as CA or SA?</span></span> | <span data-ttu-id="5e2bb-189">동일한 조직의 조직 계정을 CA 또는 SA로 추가하나요?</span><span class="sxs-lookup"><span data-stu-id="5e2bb-189">Add organizational account in the same organization as CA or SA?</span></span> | <span data-ttu-id="5e2bb-190">다른 조직의 조직 계정을 CA 또는 SA로 추가하나요?</span><span class="sxs-lookup"><span data-stu-id="5e2bb-190">Add organizational account in different organization as CA or SA?</span></span> |
  | --- | --- | --- | --- |
  |  <span data-ttu-id="5e2bb-191">Microsoft 계정</span><span class="sxs-lookup"><span data-stu-id="5e2bb-191">Microsoft Account</span></span> |<span data-ttu-id="5e2bb-192">예</span><span class="sxs-lookup"><span data-stu-id="5e2bb-192">Yes</span></span> |<span data-ttu-id="5e2bb-193">아니요</span><span class="sxs-lookup"><span data-stu-id="5e2bb-193">No</span></span> |<span data-ttu-id="5e2bb-194">아니요</span><span class="sxs-lookup"><span data-stu-id="5e2bb-194">No</span></span> |
  |  <span data-ttu-id="5e2bb-195">조직 계정</span><span class="sxs-lookup"><span data-stu-id="5e2bb-195">Organizational Account</span></span> |<span data-ttu-id="5e2bb-196">예</span><span class="sxs-lookup"><span data-stu-id="5e2bb-196">Yes</span></span> |<span data-ttu-id="5e2bb-197">예</span><span class="sxs-lookup"><span data-stu-id="5e2bb-197">Yes</span></span> |<span data-ttu-id="5e2bb-198">아니요</span><span class="sxs-lookup"><span data-stu-id="5e2bb-198">No</span></span> |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a><span data-ttu-id="5e2bb-199">리소스 액세스 제어 및 Active Directory에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="5e2bb-199">Learn more about resource access control and Active Directory</span></span>
* <span data-ttu-id="5e2bb-200">Microsoft Azure에서 리소스 액세스를 제어하는 방법에 대해 자세히 알아보려면 [Azure의 리소스 액세스 이해](../active-directory/active-directory-understanding-resource-access.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-200">To learn more about how resource access is controlled in Microsoft Azure, see [Understanding resource access in Azure](../active-directory/active-directory-understanding-resource-access.md).</span></span>
* <span data-ttu-id="5e2bb-201">Azure Active Directory에 대한 자세한 내용은 [Azure 구독을 Azure Active Directory에 연결하는 방법](../active-directory/active-directory-how-subscriptions-associated-directory.md) 및 [Azure Active Directory에서 관리자 역할 할당](../active-directory/active-directory-assign-admin-roles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-201">For more information about Azure Active Directory, see [How Azure subscriptions are associated with Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) and [Assigning administrator roles in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="5e2bb-202">도움이 필요하세요?</span><span class="sxs-lookup"><span data-stu-id="5e2bb-202">Need help?</span></span> <span data-ttu-id="5e2bb-203">지원에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-203">Contact support.</span></span>
<span data-ttu-id="5e2bb-204">다른 도움이 필요한 경우 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)하여 문제를 신속하게 해결하세요.</span><span class="sxs-lookup"><span data-stu-id="5e2bb-204">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
