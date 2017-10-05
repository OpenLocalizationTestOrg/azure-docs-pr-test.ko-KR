---
title: "Azure RemoteApp에서 Azure Active Directory 테넌트 변경 | Microsoft Docs"
description: "Azure RemoteApp과 연결된 Azure Active Directory 테넌트를 변경하는 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 7c6c4ded8a11d8399968b2c32aff055d7f3ae5f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-azure-active-directory-tenant-in-azure-remoteapp"></a><span data-ttu-id="e4590-103">Azure RemoteApp에서 Azure Active Directory 테넌트 변경</span><span class="sxs-lookup"><span data-stu-id="e4590-103">Change the Azure Active Directory tenant in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e4590-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="e4590-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="e4590-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="e4590-106">Azure RemoteApp은 Azure AD(Azure Active Directory)를 사용하여 사용자 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-106">Azure RemoteApp uses Azure Active Directory (Azure AD) to allow user access.</span></span> <span data-ttu-id="e4590-107">Azure RemoteApp에서 사용할 수 있는 유일한 Azure AD 테넌트는 Azure 구독과 연결된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-107">The only Azure AD tenant that you can use in Azure RemoteApp is the one associated with the Azure subscription.</span></span> <span data-ttu-id="e4590-108">포털의 **설정** 페이지에서 연결된 구독을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-108">You can view the associated subscription on the **Settings** page in the portal.</span></span> <span data-ttu-id="e4590-109">**구독** 탭에서 **디렉터리** 열을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-109">Look at the **Directory** column on the **Subscriptions** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="e4590-110">성공적으로 변경하려면 먼저 모든 Azure RemoteApp 컬렉션에서 기존 Azure Active Directory 테넌트의 사용자를 모두 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-110">For this change to succeed, first remove all users from the existing Azure Active Directory tenant from all Azure RemoteApp collections.</span></span> <span data-ttu-id="e4590-111">이렇게 하려면 Azure 포털로 이동한 다음 **Azure RemoteApp** 탭으로 이동하여 모든 Azure RemoteApp 컬렉션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-111">To do this, go to the Azure Portal, go to the **Azure RemoteApp** tab and open every Azure RemoteApp collection.</span></span> <span data-ttu-id="e4590-112">**사용자** 탭으로 이동하여 현재 Azure Active Directory 테넌트에 속하는 사용자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-112">Go to the **Users** tab and remove users that belong to your current Azure Active Directory tenant.</span></span> <span data-ttu-id="e4590-113">모든 기존 Azure RemoteApp 컬렉션에 대해 이 작업을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-113">Repeat for all existing Azure RemoteApp collections.</span></span> <span data-ttu-id="e4590-114">이 작업을 수행하지 않으면 컬렉션을 만들거나 패치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-114">Without doing this, you will not be able to create or patch collections.</span></span>
> 
> 

<span data-ttu-id="e4590-115">다른 테넌트를 사용하려는 경우 다음 단계를 사용하여 구독과의 연결을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-115">If you want to use a different tenant, use these steps to change the association with your subscription:</span></span>

1. <span data-ttu-id="e4590-116">포털에서 Azure RemoteApp 컬렉션에 대한 액세스 권한을 부여한 Azure AD 사용자를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-116">In the portal, remove any Azure AD users to which you’ve given access to Azure RemoteApp collections.</span></span> <span data-ttu-id="e4590-117">이 작업 방법에 대한 단계는 위의 참고를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4590-117">(See the note above for steps on how to do this.)</span></span>
2. <span data-ttu-id="e4590-118">서비스 관리자로 Microsoft 계정(이전의 Live ID)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-118">Set a Microsoft account (formerly called a Live ID) as the Service administrator.</span></span> <span data-ttu-id="e4590-119">본인이 서비스 관리자라는 사실을 모르는 경우</span><span class="sxs-lookup"><span data-stu-id="e4590-119">(Don't know if you already are the service admin?</span></span> <span data-ttu-id="e4590-120">**설정 -> 관리자**를 클릭하여 확인합니다. 이제 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-120">You can find out by clicking **Settings -> Administrators**.) Now, here's how you change that:</span></span>
   
   1. <span data-ttu-id="e4590-121">오른쪽 위 모서리에서 사용자를 클릭한 다음 **내 청구서 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-121">Click the user in the upper right corner, and then click **View my bill**.</span></span>
   2. <span data-ttu-id="e4590-122">구독을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-122">Click the subscription.</span></span> <span data-ttu-id="e4590-123">그런 다음 새 페이지에서 아래로 스크롤하여 오른쪽의 **구독 세부 정보 편집** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-123">Then, on the new page, scroll down and click **Edit subscription details** in the right.</span></span> <span data-ttu-id="e4590-124">오른쪽 아래 가운데 쯤에 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-124">(Sort of the middle bottom right, if that helps you find it.)</span></span>
   3. <span data-ttu-id="e4590-125">서비스 관리자가 될 사용자에 Microsoft 계정을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-125">Type the Microsoft account for the user that should be the service admin.</span></span>
3. <span data-ttu-id="e4590-126">이제 포털에서 로그아웃하고 이전 단계에서 지정한 Microsoft 계정으로 다시 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-126">Now, sign out of the portal, and then sign back in with the Microsoft account you specified in the previous step.</span></span>
4. <span data-ttu-id="e4590-127">**새로 만들기 -> App Services -> Active Directory -> 디렉터리 -> 사용자 지정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-127">Click **New -> App Services -> Active Directory -> Directory -> Custom Create**.</span></span>
5. <span data-ttu-id="e4590-128">**디렉터리**에서 **기존 디렉터리 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-128">Under **Directory**, choose **Use existing directory**.</span></span> <span data-ttu-id="e4590-129">이제 포털에서 로그아웃할 것이므로 **로그아웃할 준비가 되었습니다.**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-129">We're going to have to sign you out of the portal now, so choose **I am ready to be signed out now**.</span></span>
6. <span data-ttu-id="e4590-130">추가할 디렉터리의 전역 관리자로 다시 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-130">Sign back into the portal as a global admin of the directory you want to add.</span></span> <span data-ttu-id="e4590-131">아직 전역 관리자가 아니라면 로그인한 다음 다시 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-131">(If you weren't already a global admin, you will be after a round of sign in and then sign out.)</span></span>
7. <span data-ttu-id="e4590-132">로그인할 때 구독에서 기존 AD 테넌트를 사용할지 묻는 메시지가 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-132">You'll be asked when you sign in if you want to use your existing AD tenant with your subscription.</span></span> <span data-ttu-id="e4590-133">**계속**을 클릭한 다음 **지금 로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-133">Click **Continue**, and then click **Sign out now**.</span></span>
8. <span data-ttu-id="e4590-134">다시 로그인하여 **설정 -> 구독**으로 다시 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-134">Sign back in again, and go back to **Settings -> Subscriptions**.</span></span> <span data-ttu-id="e4590-135">구독을 선택한 다음 **디렉터리 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-135">Select your subscription, and then click **Edit Directory**.</span></span> <span data-ttu-id="e4590-136">사용하려는 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-136">Select the Azure AD tenant that you want to use.</span></span>

<span data-ttu-id="e4590-137">이제 새 Azure AD 테넌트를 사용하여 Azure 구독에 대한 액세스를 제어하고 Azure RemoteApp에서 사용자 액세스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4590-137">You can now use the new Azure AD tenant to control access to the Azure subscription and to configure user access in Azure RemoteApp.</span></span>

