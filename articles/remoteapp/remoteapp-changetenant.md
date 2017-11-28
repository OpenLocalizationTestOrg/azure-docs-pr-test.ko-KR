---
title: "Azure RemoteApp에서 aaaChange hello Azure Active Directory 테 넌 트 | Microsoft Docs"
description: "Azure RemoteApp과 toochange hello Azure Active Directory 테 넌 트 연결 하는 방식에 대해 알아봅니다"
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
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a><span data-ttu-id="efd5f-103">Azure RemoteApp에서 hello Azure Active Directory 테 넌 트 변경</span><span class="sxs-lookup"><span data-stu-id="efd5f-103">Change hello Azure Active Directory tenant in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="efd5f-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="efd5f-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="efd5f-106">Azure RemoteApp Azure Active Directory (Azure AD) tooallow 사용자 액세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-106">Azure RemoteApp uses Azure Active Directory (Azure AD) tooallow user access.</span></span> <span data-ttu-id="efd5f-107">Azure RemoteApp에 사용할 수 있는 hello만 Azure AD 테 넌 트는 hello hello Azure 구독에 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-107">hello only Azure AD tenant that you can use in Azure RemoteApp is hello one associated with hello Azure subscription.</span></span> <span data-ttu-id="efd5f-108">Hello에 관련 된 hello 구독을 볼 수 있습니다 **설정을** hello 포털의 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-108">You can view hello associated subscription on hello **Settings** page in hello portal.</span></span> <span data-ttu-id="efd5f-109">Hello를 살펴보고 **디렉터리** hello에 대 한 열 **구독** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-109">Look at hello **Directory** column on hello **Subscriptions** tab.</span></span>

> [!NOTE]
> <span data-ttu-id="efd5f-110">이 변경 toosucceed에 대 한 먼저 hello 기존 Azure Active Directory 테 넌 트의 모든 Azure RemoteApp 컬렉션의 모든 사용자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-110">For this change toosucceed, first remove all users from hello existing Azure Active Directory tenant from all Azure RemoteApp collections.</span></span> <span data-ttu-id="efd5f-111">toodo이, 이동 toohello Azure 포털에서 이동 toohello **Azure RemoteApp** 탭 하 고 모든 Azure RemoteApp 컬렉션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-111">toodo this, go toohello Azure Portal, go toohello **Azure RemoteApp** tab and open every Azure RemoteApp collection.</span></span> <span data-ttu-id="efd5f-112">Toohello 이동 **사용자** 탭 및 tooyour 현재 Azure Active Directory 테 넌 트에 속하는 사용자를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-112">Go toohello **Users** tab and remove users that belong tooyour current Azure Active Directory tenant.</span></span> <span data-ttu-id="efd5f-113">모든 기존 Azure RemoteApp 컬렉션에 대해 이 작업을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-113">Repeat for all existing Azure RemoteApp collections.</span></span> <span data-ttu-id="efd5f-114">이 작업을 수행 하지 않고 됩니다 수 toocreate 또는 패치 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-114">Without doing this, you will not be able toocreate or patch collections.</span></span>
> 
> 

<span data-ttu-id="efd5f-115">Toouse 다른 테 넌 트를 원하는 경우 이러한 단계 toochange hello 연결 구독에서 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="efd5f-115">If you want toouse a different tenant, use these steps toochange hello association with your subscription:</span></span>

1. <span data-ttu-id="efd5f-116">Hello 포털에서 모든 Azure AD 사용자가 toowhich 제거 tooAzure RemoteApp 컬렉션 액세스를 부여 하였습니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-116">In hello portal, remove any Azure AD users toowhich you’ve given access tooAzure RemoteApp collections.</span></span> <span data-ttu-id="efd5f-117">(참고 hello 위의 단계에 대 한 방법에 toodo이.)</span><span class="sxs-lookup"><span data-stu-id="efd5f-117">(See hello note above for steps on how toodo this.)</span></span>
2. <span data-ttu-id="efd5f-118">Hello 서비스 관리자로 Microsoft 계정 (이전의 Live ID)를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-118">Set a Microsoft account (formerly called a Live ID) as hello Service administrator.</span></span> <span data-ttu-id="efd5f-119">(모르는 이미 모르는 경우 서비스 admin 님 안녕하세요?</span><span class="sxs-lookup"><span data-stu-id="efd5f-119">(Don't know if you already are hello service admin?</span></span> <span data-ttu-id="efd5f-120">**설정 -> 관리자**를 클릭하여 확인합니다. 이제 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-120">You can find out by clicking **Settings -> Administrators**.) Now, here's how you change that:</span></span>
   
   1. <span data-ttu-id="efd5f-121">Hello 맨 오른쪽 위에 있는 hello 사용자를 클릭 한 다음 클릭 **내 청구서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-121">Click hello user in hello upper right corner, and then click **View my bill**.</span></span>
   2. <span data-ttu-id="efd5f-122">Hello 구독을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-122">Click hello subscription.</span></span> <span data-ttu-id="efd5f-123">그런 다음 hello 새 페이지에서 아래로 스크롤하여 클릭 **구독 세부 정보 편집** hello 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-123">Then, on hello new page, scroll down and click **Edit subscription details** in hello right.</span></span> <span data-ttu-id="efd5f-124">(종류의 경우 해당 오른쪽 가운데 아래 hello 사용 하면 되는 것입니다.)</span><span class="sxs-lookup"><span data-stu-id="efd5f-124">(Sort of hello middle bottom right, if that helps you find it.)</span></span>
   3. <span data-ttu-id="efd5f-125">Hello 서비스 관리자 되어야 하는 hello 사용자에 대 한 hello Microsoft 계정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-125">Type hello Microsoft account for hello user that should be hello service admin.</span></span>
3. <span data-ttu-id="efd5f-126">이제 로그 hello 포털 아웃 한 다음 다시 hello hello 이전 단계에서 지정한 Microsoft 계정으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-126">Now, sign out of hello portal, and then sign back in with hello Microsoft account you specified in hello previous step.</span></span>
4. <span data-ttu-id="efd5f-127">**새로 만들기 -> App Services -> Active Directory -> 디렉터리 -> 사용자 지정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-127">Click **New -> App Services -> Active Directory -> Directory -> Custom Create**.</span></span>
5. <span data-ttu-id="efd5f-128">**디렉터리**에서 **기존 디렉터리 사용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-128">Under **Directory**, choose **Use existing directory**.</span></span> <span data-ttu-id="efd5f-129">여기 toohave toosign hello 포털 이제 부족 하므로 하시 **지금 로그 아웃 준비 toobe 저는**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-129">We're going toohave toosign you out of hello portal now, so choose **I am ready toobe signed out now**.</span></span>
6. <span data-ttu-id="efd5f-130">Hello에 다시 로그인 tooadd 원하는 hello 디렉터리의 전역 관리자로 포털입니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-130">Sign back into hello portal as a global admin of hello directory you want tooadd.</span></span> <span data-ttu-id="efd5f-131">아직 전역 관리자가 아니라면 로그인한 다음 다시 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-131">(If you weren't already a global admin, you will be after a round of sign in and then sign out.)</span></span>
7. <span data-ttu-id="efd5f-132">원하면 toouse 기존 AD 테 넌 트 구독에 로그인 할 때 라는 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-132">You'll be asked when you sign in if you want toouse your existing AD tenant with your subscription.</span></span> <span data-ttu-id="efd5f-133">**계속**을 클릭한 다음 **지금 로그아웃**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-133">Click **Continue**, and then click **Sign out now**.</span></span>
8. <span data-ttu-id="efd5f-134">로그인을 다시 다시 후 너무 돌아가기**설정-> 구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-134">Sign back in again, and go back too**Settings -> Subscriptions**.</span></span> <span data-ttu-id="efd5f-135">구독을 선택한 다음 **디렉터리 편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-135">Select your subscription, and then click **Edit Directory**.</span></span> <span data-ttu-id="efd5f-136">원하는 toouse hello Azure AD 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-136">Select hello Azure AD tenant that you want toouse.</span></span>

<span data-ttu-id="efd5f-137">이제 Azure RemoteApp에서 hello 새 Azure AD 테 넌 트 toocontrol 액세스 toohello Azure 구독 및 tooconfigure 사용자 액세스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="efd5f-137">You can now use hello new Azure AD tenant toocontrol access toohello Azure subscription and tooconfigure user access in Azure RemoteApp.</span></span>

