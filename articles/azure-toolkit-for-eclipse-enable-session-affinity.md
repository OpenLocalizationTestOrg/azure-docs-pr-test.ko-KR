---
title: "Eclipse 용 Azure 도구 키트 hello aaaEnable 세션 선호도 사용 하 여"
description: "어떻게 Eclipse 용 Azure 도구 키트를 사용 하 여 tooenable 세션 선호도 hello에 대해 알아봅니다."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="13304-103">세션 선호도 사용</span><span class="sxs-lookup"><span data-stu-id="13304-103">Enable Session Affinity</span></span>
<span data-ttu-id="13304-104">Hello Azure Toolkit for Eclipse 내에서 "고정 세션", 역할 또는 HTTP 세션 선호도 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="13304-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="13304-105">hello 다음 그림에 나와 hello **부하 분산** 속성 대화 상자 사용 tooenable hello 세션 선호도 기능:</span><span class="sxs-lookup"><span data-stu-id="13304-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="13304-106">사용자의 역할에 대 한 tooenable 세션 선호도</span><span class="sxs-lookup"><span data-stu-id="13304-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="13304-107">Eclipse의 프로젝트 탐색기에서 hello 역할을 마우스 오른쪽 단추로 클릭 합니다. **Azure**, 클릭 하 고 **부하 분산**합니다.</span><span class="sxs-lookup"><span data-stu-id="13304-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="13304-108">Hello에 **WorkerRole1 부하 분산에 대 한 속성** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="13304-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="13304-109">a.</span><span class="sxs-lookup"><span data-stu-id="13304-109">a.</span></span> <span data-ttu-id="13304-110">**Enable HTTP session affinity (sticky sessions) for this role**</span><span class="sxs-lookup"><span data-stu-id="13304-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="13304-111">b.</span><span class="sxs-lookup"><span data-stu-id="13304-111">b.</span></span> <span data-ttu-id="13304-112">에 대 한 **입력 끝점 toouse**, 예를 들어 한 입력된 끝점 toouse 선택 **http (공용: 80, 개인: 8080)**합니다.</span><span class="sxs-lookup"><span data-stu-id="13304-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="13304-113">응용 프로그램은 이 끝점을 해당 HTTP 끝점으로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="13304-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="13304-114">사용자의 역할에 대 한 여러 끝점을 설정할 수 있지만 둘 중 하나만 toosupport를 선택할 수 있습니다 고정 세션입니다.</span><span class="sxs-lookup"><span data-stu-id="13304-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="13304-115">c.</span><span class="sxs-lookup"><span data-stu-id="13304-115">c.</span></span> <span data-ttu-id="13304-116">응용 프로그램을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="13304-116">Rebuild your application.</span></span>

<span data-ttu-id="13304-117">특정 클라이언트에서 발생 하는 HTTP 요청에서 처리 하 고 hello 동일 계속 사용할 수 있는 경우 역할 인스턴스가 둘 이상 있는 경우, 역할 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="13304-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="13304-118">hello Eclipse 도구 키트에 각 역할 인스턴스에 요청 라우팅 ARR (응용 프로그램)를 호출 하는 특수 한 IIS 모듈을 설치 하 여 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="13304-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="13304-119">ARR에 HTTP 요청 toohello 적절 한 역할 인스턴스로 다시 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="13304-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="13304-120">hello 도구 키트는 hello 들어오는 HTTP 트래픽이 않도록 첫 번째 라우트된 toohello ARR 소프트웨어로 hello 선택한 끝점을 자동으로 재구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="13304-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="13304-121">또한 hello toolkit Java 서버를 구성 된 toolisten 되는 새 내부 끝점을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="13304-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="13304-122">ARR tooreroute hello HTTP 트래픽 toohello 적절 한 역할 인스턴스에 사용 되는 hello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="13304-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="13304-123">이 방법으로 다중 인스턴스 배포의 각 역할 인스턴스는 모두에 대 한 역방향 프록시 hello 다른 경우 고정 세션을 사용 하도록 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13304-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="13304-124">세션 선호도 관련 참고 사항</span><span class="sxs-lookup"><span data-stu-id="13304-124">Notes about session affinity</span></span>
* <span data-ttu-id="13304-125">세션 선호도 hello 계산 에뮬레이터에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13304-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="13304-126">hello 설정을 hello 계산 에뮬레이터에서 빌드 프로세스를 방해 하지 않고 적용 하거나 계산 에뮬레이터 실행 하지만 자체 hello 기능은 hello 계산 에뮬레이터 내에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="13304-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="13304-127">세션 선호도 사용 하도록 설정 hello 추가 소프트웨어 다운로드 되 고 hello Azure 클라우드 서비스를 시작할 때 사용할 역할 인스턴스에 설치 하는 대로 azure에서 배포에서 사용할 디스크 공간에에서 증가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13304-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="13304-128">hello 시간 tooinitialize 각 역할 더 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="13304-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="13304-129">내부 끝점으로, 위에서 설명한 것 처럼 트래픽 rerouter toofunction 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="13304-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="13304-130">참고 항목</span><span class="sxs-lookup"><span data-stu-id="13304-130">See Also</span></span>
<span data-ttu-id="13304-131">[Eclipse용 Azure 도구 키트][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="13304-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="13304-132">[Eclipse에서 Azure용 Hello World 응용 프로그램 만들기][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="13304-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="13304-133">[Hello Eclipse 용 Azure 도구 키트 설치][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="13304-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="13304-134">Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터][Azure Java Developer Center]합니다.</span><span class="sxs-lookup"><span data-stu-id="13304-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
