---
title: "Azure RemoteApp으로 모든 장치에서 동일한 Office 365 환경 즐기기 | Microsoft Docs"
description: "Azure RemoteApp을 사용하여 사용자와 Office 365 앱을 공유하는 방법을 알아봅니다."
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
ms.openlocfilehash: 584c781c97097cda3c1455ade05cba8659f11073
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-the-same-office-365-experience-on-any-device-with-azure-remoteapp"></a><span data-ttu-id="256fe-103">Azure RemoteApp으로 모든 장치에서 동일한 Office 365 환경 즐기기</span><span class="sxs-lookup"><span data-stu-id="256fe-103">Get the same Office 365 experience on any device with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="256fe-104">Azure RemoteApp은 2017년 8월 31일에 중단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="256fe-105">자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="256fe-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="256fe-106">이 문서에서는 회사의 모든 장치에서 Office 365를 배포하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-106">This article will cover how to deploy Office 365 on any device in your company.</span></span> <span data-ttu-id="256fe-107">사용자는 Android, Apple 및 Windows에서 동일한 기능과 UI 환경을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-107">Your users can get the same capabilities and UI experience on Android, Apple and Windows.</span></span>

<span data-ttu-id="256fe-108">이를 위해 사용자가 연결할 수 있는 Azure의 확장 가능한 가상 컴퓨터에서 Office 365를 호스트하여 Azure RemoteApp을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-108">We will accomplish this using Azure RemoteApp by hosting Office 365 on scale-able virtual machines in Azure that users can connect to.</span></span> <span data-ttu-id="256fe-109">이 가상 컴퓨터 집합을 "클라우드 컬렉션"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-109">This set of virtual machines we call a "cloud collection".</span></span>

## <a name="create-a-cloud-collection"></a><span data-ttu-id="256fe-110">클라우드 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="256fe-110">Create a cloud collection</span></span>
<span data-ttu-id="256fe-111">먼저 Azure 계정을 만든 후 왼쪽에 있는 링크를 클릭하여 **RemoteApp** 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-111">First after you have created an Azure account, navigate to **RemoteApp** by clicking on the link on the left side.</span></span>
<span data-ttu-id="256fe-112">![Azure 포털에서 Azure RemoteApp 표시](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span><span class="sxs-lookup"><span data-stu-id="256fe-112">![Showing Azure RemoteApp on the Azure Portal](./media/remoteapp-tutorial-o365anywhere/1-menu.png)</span></span>

<span data-ttu-id="256fe-113">그런 다음 아래쪽에서 **새로 만들기** 를 클릭하고 컬렉션을 "빠르게 생성"합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-113">Then continue by clicking **new** on the bottom and "quick creating" a collection.</span></span> <span data-ttu-id="256fe-114">이름, 지역, 구독, 계획 및 Microsoft에서 제공하는 "Office Proffesional 2013" 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-114">Provide a name, the region, the subscription, the plan and the image "Office Proffesional 2013" that we provide.</span></span>
<span data-ttu-id="256fe-115">![만들기 대화 상자](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span><span class="sxs-lookup"><span data-stu-id="256fe-115">![Create Dialog](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)</span></span>

<span data-ttu-id="256fe-116">양식을 완료하면 컬렉션 만들기 프로세스가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-116">Once you finish the form the collection creation process should start.</span></span> <span data-ttu-id="256fe-117">이 작업을 수행하는 데 1시간 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-117">This may take up to an hour or so.</span></span>

![대기](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

<span data-ttu-id="256fe-119">프로세스가 완료되면 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-119">Once the process is done, it will look something like this.</span></span> <span data-ttu-id="256fe-120">**게시** 를 클릭하면 대부분의 Office 응용 프로그램이 이미 게시되어 있음을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-120">If we click **Publishing** we can see that most Office applications have been published for us already.</span></span>
<span data-ttu-id="256fe-121">![만들어진 컬렉션](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span><span class="sxs-lookup"><span data-stu-id="256fe-121">![Collection created](./media/remoteapp-tutorial-o365anywhere/4-done.png)</span></span>

![게시된 앱](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

<span data-ttu-id="256fe-123">여기서 **사용자 액세스**를 클릭하여 이 컬렉션에 액세스할 수 있는 사용자를 더 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-123">At this point you can also add more users that have access to this collection by clicking **User Access**.</span></span>
<span data-ttu-id="256fe-124">![사용자 액세스 구성](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span><span class="sxs-lookup"><span data-stu-id="256fe-124">![Configure user access](./media/remoteapp-tutorial-o365anywhere/6-user.png)</span></span>

<span data-ttu-id="256fe-125">이제 Office 365에 연결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-125">Now let's try out connecting to Office 365!</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="256fe-126">Office 365에 연결</span><span class="sxs-lookup"><span data-stu-id="256fe-126">Connect to Office 365</span></span>
<span data-ttu-id="256fe-127">[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/)을 방문하여 아래로 스크롤을 내린 다음 **클라이언트 다운로드**를 클릭하여 사용하는 장치에 Azure RemoteApp 클라이언트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-127">We'll head over to [https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), scroll down  and click **Download clients** to install the Azure RemoteApp client on the device you're on.</span></span> <span data-ttu-id="256fe-128">아래 스크린샷은 Windows에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-128">The screenshots below are for Windows.</span></span>

<span data-ttu-id="256fe-129">응용 프로그램이 시작되면 Microsoft 계정(이전의 “Live ID”)을 사용하여 로그인하라는 메시지가 표시됩니다. 여기서는 Azure 계정과 동일한 ID를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-129">Once the application starts you'll be asked to sign in with your Microsoft account (formerly called a "Live ID"), use the same one as your Azure account for now.</span></span> <span data-ttu-id="256fe-130">로그인하면 새 초대에 대한 알림이 표시됩니다. 알림을 클릭하면 아래와 같은 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-130">When you're signed in you should see a notification about new invitations, click there and you should see a list like one below.</span></span> <span data-ttu-id="256fe-131">내 Azure 계정 소유자 전자 메일과 일치하는 초대를 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-131">Accept the invitation that matches your Azure account owner email.</span></span>

![새 초대](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

<span data-ttu-id="256fe-133">새 초대가 있는 경우의 모양</span><span class="sxs-lookup"><span data-stu-id="256fe-133">What it looks like when there are new invitations.</span></span>

![응용 프로그램 수락](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

<span data-ttu-id="256fe-135">초대를 수락하면 Azure RemoteApp 클라이언트에 모든 Office 앱이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-135">Once you accept the invitation you should see all the Office apps in the Azure RemoteApp client.</span></span>

![앱 목록](./media/remoteapp-tutorial-o365anywhere/9-work.png)

<span data-ttu-id="256fe-137">응용 프로그램을 클릭하면 Azure 가상 컴퓨터에서 시작되며 사용할 준비가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="256fe-137">When you click on any of these the application should start on the Azure virtual machine and you should be all set!</span></span> <span data-ttu-id="256fe-138">마음껏 즐기세요!</span><span class="sxs-lookup"><span data-stu-id="256fe-138">Enjoy!</span></span>

![시작 중](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

