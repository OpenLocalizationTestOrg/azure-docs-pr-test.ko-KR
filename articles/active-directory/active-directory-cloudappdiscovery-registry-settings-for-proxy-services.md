---
title: "프록시 서비스용 클라우드 앱 검색 레지스트리 설정 | Microsoft Docs"
description: "이 항목의 목표는 클라우드 앱 검색 에이전트를 실행하는 컴퓨터에 필요한 포트를 설정하기 위해 수행해야 하는 단계를 제공하는 것입니다."
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
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="4ba58-103">프록시 서비스용 클라우드 앱 검색 레지스트리 설정</span><span class="sxs-lookup"><span data-stu-id="4ba58-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="4ba58-104">클라우드 앱 검색 에이전트는 기본적으로 80 또는 443 포트만 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="4ba58-105">사용자 지정 포트(80이나 443이 아닌)를 사용하는 프록시 서버가 있는 환경에 클라우드 앱 검색을 설치하고자 한다면 이 포트를 사용하도록 에이전트를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="4ba58-106">구성은 레지스트리 키를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="4ba58-107">이 항목의 목표는 클라우드 앱 검색 에이전트를 실행하는 컴퓨터에 필요한 포트를 설정하기 위해 수행해야 하는 단계를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="4ba58-108">**클라우드 앱 검색 에이전트를 실행하는 컴퓨터에서 사용하는 포트를 수정하려면 다음 단계를 수행합니다.**</span><span class="sxs-lookup"><span data-stu-id="4ba58-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="4ba58-109">레지스트리 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-109">Start the registry editor.</span></span> <br> ![실행](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="4ba58-111">다음 레지스트리 키로 이동하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="4ba58-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="4ba58-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="4ba58-113">**포트**라고 불리는 새 **다중 문자열**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="4ba58-114">![새로 만들기](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="4ba58-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="4ba58-115">**다중 문자열 편집** 대화 상자를 열려면 해당 포트 값을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="4ba58-116">값 데이터 상자에 다음 값을 입력하고 조직에서 사용되는 모든 사용자 지정 포트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="4ba58-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="4ba58-117">
   **80**</span></span> <br><span data-ttu-id="4ba58-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="4ba58-118">
   **8080**</span></span> <br><span data-ttu-id="4ba58-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="4ba58-119">
   **8118**</span></span> <br><span data-ttu-id="4ba58-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="4ba58-120">
   **8888**</span></span> <br><span data-ttu-id="4ba58-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="4ba58-121">
   **81**</span></span> <br><span data-ttu-id="4ba58-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="4ba58-122">
   **12080**</span></span> <br><span data-ttu-id="4ba58-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="4ba58-123">
**6999**</span></span> <br><span data-ttu-id="4ba58-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="4ba58-124">
**30606**</span></span> <br><span data-ttu-id="4ba58-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="4ba58-125">
**31595**</span></span> <br><span data-ttu-id="4ba58-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="4ba58-126">
**4080**</span></span> <br><span data-ttu-id="4ba58-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="4ba58-127">
**443**</span></span> <br><span data-ttu-id="4ba58-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="4ba58-128">
**1110**</span></span> <br><br><span data-ttu-id="4ba58-129">
![다중 문자열 편집](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="4ba58-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="4ba58-130">**확인**을 클릭하여 **다중 문자열 편집** 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="4ba58-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="4ba58-131">**추가 리소스**</span><span class="sxs-lookup"><span data-stu-id="4ba58-131">**Additional Resources**</span></span>

* [<span data-ttu-id="4ba58-132">조직 내에서 사용되고 있는 허용되지 않은 클라우드 앱을 검색하는 방법</span><span class="sxs-lookup"><span data-stu-id="4ba58-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

