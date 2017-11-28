---
title: "프록시 서비스에 대 한 App Discovery 레지스트리 설정 aaaCloud | Microsoft Docs"
description: "hello이이 항목에서는 tooprovide hello로 사용자의 단계 필요한 tooperform tooset hello 필요한 포트 hello Cloud App Discovery 에이전트를 실행 하는 hello 컴퓨터에 있어야 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="6dac1-103">프록시 서비스용 클라우드 앱 검색 레지스트리 설정</span><span class="sxs-lookup"><span data-stu-id="6dac1-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="6dac1-104">Hello Cloud App Discovery 에이전트는 기본적으로 구성 된 toouse만 hello 포트 80 또는 443입니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="6dac1-105">사용자 지정 포트 (80 또는 443)를 사용 하는 프록시 서버는 환경에서 Cloud App Discovery를 설치 하려는 경우 필요한 tooconfigure 에이전트 toouse이이 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="6dac1-106">hello 구성 레지스트리 키를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="6dac1-107">hello이이 항목에서는 tooprovide hello로 사용자의 단계 필요한 tooperform tooset hello 필요한 포트 hello Cloud App Discovery 에이전트를 실행 하는 hello 컴퓨터에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="6dac1-108">**toomodify hello 포트 hello Cloud App Discovery 에이전트를 실행 하는 hello 컴퓨터에서 사용 하는 hello 다음 단계를 수행 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6dac1-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="6dac1-109">Hello 레지스트리 편집기를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-109">Start hello registry editor.</span></span> <br> ![실행](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="6dac1-111">탐색 tooor hello 다음 레지스트리 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="6dac1-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="6dac1-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="6dac1-113">**포트**라고 불리는 새 **다중 문자열**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="6dac1-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="6dac1-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="6dac1-115">tooopen hello **다중 문자열 편집** 대화 상자에서 hello 포트 값을 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="6dac1-116">Hello 값 데이터 입력란 hello 다음 값을 입력 하 고 조직에서 사용 되는 모든 사용자 지정 포트를 추가 합니다. 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6dac1-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="6dac1-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="6dac1-117">
   **80**</span></span> <br><span data-ttu-id="6dac1-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="6dac1-118">
   **8080**</span></span> <br><span data-ttu-id="6dac1-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="6dac1-119">
   **8118**</span></span> <br><span data-ttu-id="6dac1-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="6dac1-120">
   **8888**</span></span> <br><span data-ttu-id="6dac1-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="6dac1-121">
   **81**</span></span> <br><span data-ttu-id="6dac1-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="6dac1-122">
   **12080**</span></span> <br><span data-ttu-id="6dac1-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="6dac1-123">
**6999**</span></span> <br><span data-ttu-id="6dac1-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="6dac1-124">
**30606**</span></span> <br><span data-ttu-id="6dac1-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="6dac1-125">
**31595**</span></span> <br><span data-ttu-id="6dac1-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="6dac1-126">
**4080**</span></span> <br><span data-ttu-id="6dac1-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="6dac1-127">
**443**</span></span> <br><span data-ttu-id="6dac1-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="6dac1-128">
**1110**</span></span> <br><br><span data-ttu-id="6dac1-129">
![다중 문자열 편집](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="6dac1-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="6dac1-130">클릭 **확인** tooclose hello **다중 문자열 편집** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="6dac1-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="6dac1-131">**추가 리소스**</span><span class="sxs-lookup"><span data-stu-id="6dac1-131">**Additional Resources**</span></span>

* [<span data-ttu-id="6dac1-132">조직 내에서 사용되고 있는 허용되지 않은 클라우드 앱을 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="6dac1-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

