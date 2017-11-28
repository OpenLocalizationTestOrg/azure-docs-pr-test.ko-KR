---
title: "aaaGet hello Azure RemoteApp과 함께 모든 장치에서 동일한 Office 365 환경 | Microsoft Docs"
description: "자세한 내용은 방법 tooshare Azure RemoteApp을 사용 하 여 사용자와 Office 365 앱."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="98ccb-103">동일한 get hello Azure RemoteApp과 함께 모든 장치에서 제공 되는 Office 365</span><span class="sxs-lookup"><span data-stu-id="98ccb-103">Get hello same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="98ccb-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="98ccb-105">읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="98ccb-106">이 문서에서는 설명 하는 방법을 회사의 모든 장치에서 Office 365 toodeploy 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-106">This article will cover how toodeploy Office 365 on any device in your company.</span></span> <span data-ttu-id="98ccb-107">사용자가 hello 동일한 기능을 가져올 수 있습니다 및 Android, 사과 및 Windows에서 UI 경험 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-107">Your users can get hello same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="98ccb-108">이를 위해 사용자가 연결할 수 있는 Azure의 확장 가능한 가상 컴퓨터에서 Office 365를 호스트하여 Azure RemoteApp을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="98ccb-109">이 가상 컴퓨터 집합을 "클라우드 컬렉션"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="98ccb-110">클라우드 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="98ccb-110">Create a cloud collection</span></span>
<span data-ttu-id="98ccb-111">처음 Azure 계정을 만든 후 이동 너무**RemoteApp** hello 왼쪽의 hello 링크를 클릭 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-111">First after you have created an Azure account, navigate too**RemoteApp** by clicking on hello link on hello left side.</span></span>
<span data-ttu-id="98ccb-112">![Hello Azure 포털에서 Azure RemoteApp 표시](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="98ccb-112">![Showing Azure RemoteApp on hello Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="98ccb-113">다음을 클릭 하 여 계속 **새** hello 아래쪽과 "빠른 만들기"에 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-113">Then continue by clicking **new** on hello bottom and "quick creating" a collection.</span></span> <span data-ttu-id="98ccb-114">이름, hello 지역, hello 구독, hello 계획 및 제공 하는 hello 이미지 "Office Proffesional 2013"를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-114">Provide a name, hello region, hello subscription, hello plan and hello image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="98ccb-115">![만들기 대화 상자](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="98ccb-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="98ccb-116">완료 되 면 hello 양식 hello 컬렉션 생성 프로세스를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-116">Once you finish hello form hello collection creation process should start.</span></span> <span data-ttu-id="98ccb-117">tooan 시간 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-117">This may take up tooan hour or so.</span></span>

![대기](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="98ccb-119">Hello 프로세스를 완료 한 후 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-119">Once hello process is done, it will look something like this.</span></span> <span data-ttu-id="98ccb-120">**게시** 를 클릭하면 대부분의 Office 응용 프로그램이 이미 게시되어 있음을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="98ccb-121">![만들어진 컬렉션](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="98ccb-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![게시된 앱](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="98ccb-123">이 시점에서 추가할 수도 있습니다를 클릭 하 여 액세스 toothis 컬렉션에 있는 더 많은 사용자가 **사용자 액세스**합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-123">At this point you can also add more users that have access toothis collection by clicking **User Access**.</span></span>
<span data-ttu-id="98ccb-124">![사용자 액세스 구성](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="98ccb-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="98ccb-125">이제 tooOffice 365 연결 시험해 보겠습니다!</span><span class="sxs-lookup"><span data-stu-id="98ccb-125">Now let's try out connecting tooOffice 365!</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="98ccb-126">TooOffice 365 연결</span><span class="sxs-lookup"><span data-stu-id="98ccb-126">Connect tooOffice 365</span></span>
<span data-ttu-id="98ccb-127">통해 너무 head 합니다 म[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), 아래로 스크롤하여 클릭 **클라이언트를 다운로드할** 하 고 hello 장치의 tooinstall hello Azure RemoteApp 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-127">We'll head over too[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** tooinstall hello Azure RemoteApp client on hello device you're on.</span></span> <span data-ttu-id="98ccb-128">Windows hello 스크린 샷을 아래 됩니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-128">hello screenshots below are for Windows.</span></span>

<span data-ttu-id="98ccb-129">Hello 응용 프로그램 시작 되 면 만들라는 메시지가 toosign Microsoft 계정 (이전의 "Live ID")으로, 사용 하 여 hello 지금은 동일한 Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="98ccb-129">Once hello application starts you'll be asked toosign in with your Microsoft account (formerly called a "Live ID"), use hello same one as your Azure account for now.</span></span> <span data-ttu-id="98ccb-130">로그인하면 새 초대에 대한 알림이 표시됩니다. 알림을 클릭하면 아래와 같은 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="98ccb-131">Azure 계정 소유자 전자 메일을 일치 하는 hello 초대를 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-131">Accept hello invitation that matches your Azure account owner email.</span></span>

![새 초대](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="98ccb-133">새 초대가 있는 경우의 모양</span><span class="sxs-lookup"><span data-stu-id="98ccb-133">What it looks like when there are new invitations.</span></span>

![응용 프로그램 수락](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="98ccb-135">Hello 초대를 수락 되 면 모든 hello Office 앱 hello Azure RemoteApp 클라이언트에 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="98ccb-135">Once you accept hello invitation you should see all hello Office apps in hello Azure RemoteApp client.</span></span>

![앱 목록](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="98ccb-137">이러한 hello 응용 프로그램 중 하나를 클릭 해야 hello에 Azure 가상 컴퓨터를 시작 하 고 모두 설정 해야 합니다.!</span><span class="sxs-lookup"><span data-stu-id="98ccb-137">When you click on any of these hello application should start on hello Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="98ccb-138">마음껏 즐기세요!</span><span class="sxs-lookup"><span data-stu-id="98ccb-138">Enjoy!</span></span>

![시작 중](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

