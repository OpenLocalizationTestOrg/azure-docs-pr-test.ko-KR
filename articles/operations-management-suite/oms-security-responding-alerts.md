---
title: "Operations Management Suite 보안 및 감사 솔루션의 보안 경고 모니터링 및 응답 | Microsoft Docs"
description: "이 문서는 OMS 보안 및 감사에서 사용 가능한 위협 인텔리전스 옵션을 사용하여 보안 경고를 모니터링하고 대응하는 방법을 설명합니다."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 7d45a32b-1341-4bb5-a436-1f42a8a2590a
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/13/2017
ms.author: yurid
ms.openlocfilehash: 0cf9b83d7023641ec445a59a5e61d3da038695fa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-and-responding-to-security-alerts-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="2ffa1-103">Operations Management Suite 보안 및 감사 솔루션의 보안 경고 모니터링 및 응답</span><span class="sxs-lookup"><span data-stu-id="2ffa1-103">Monitoring and responding to security alerts in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="2ffa1-104">이 문서는 OMS 보안 및 감사에서 사용 가능한 위협 인텔리전스 옵션을 사용하여 보안 경고를 모니터링하고 대응하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-104">This document helps you use the threat intelligence option available in OMS Security and Audit to monitor and respond to security alerts.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="2ffa1-105">OMS란?</span><span class="sxs-lookup"><span data-stu-id="2ffa1-105">What is OMS?</span></span>
<span data-ttu-id="2ffa1-106">Microsoft Operations Management Suite(OMS)란 온-프레미스 및 클라우드 인프라를 관리 및 보호하도록 도와주는 Microsoft의 클라우드 기반 IT 관리 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="2ffa1-107">OMS에 대한 자세한 내용은 [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-107">For more information about OMS, read the article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="threat-intelligence"></a><span data-ttu-id="2ffa1-108">위협 인텔리전스</span><span class="sxs-lookup"><span data-stu-id="2ffa1-108">Threat intelligence</span></span>
<span data-ttu-id="2ffa1-109">사용자가 네트워크에 광범위하게 액세스할 수 있고 다양한 장치를 사용하여 기업 데이터에 연결하는 엔터프라이즈 환경에서는 리소스를 능동적으로 모니터링하고 보안 문제에 빠르게 대응하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-109">In an enterprise environment where users have broad access to the network and use a variety of devices to connect to corporate data, it is imperative that you can actively monitor your resources and quickly respond to security incidents.</span></span> <span data-ttu-id="2ffa1-110">이러한 대응은 일부 사이버 보안 위협은 기존 보안 기술 통제 수단으로 식별할 수 있는 경고나 의심스러운 활동으로 나타나지 않기 때문에 보안 수명 주기 측면에서 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-110">This is particular important from the security lifecycle perspective because some cybersecurity threats may not raise alerts or suspicious activities that can be identified by traditional security technical controls.</span></span> 

<span data-ttu-id="2ffa1-111">IT 관리자는 OMS의 **위협 인텔리전스** 옵션을 사용하여 환경에 대한 보안 위협을 식별할 수 있습니다. 예를 들어 특정 컴퓨터가 [봇넷](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection)의 일부인 경우를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-111">By using the **Threat Intelligence** option available in OMS Security and Audit, IT administrators can identify security threats against the environment, for example, identify if a particular computer is part of a [botnet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection).</span></span> <span data-ttu-id="2ffa1-112">공격자가 컴퓨터를 명령 및 컨트롤에 몰래 연결하는 맬웨어를 불법으로 설치할 경우 해당 컴퓨터가 봇넷의 노드가 되었다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-112">Computers can become nodes in a botnet when attackers illicitly install malware that secretly connects this computer to the command and control.</span></span> <span data-ttu-id="2ffa1-113">또한 [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents)과 같은 지하 통신 채널에서 오는 잠재적 위협도 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-113">It can also identify potential threats coming from underground communication channels, such as [darknet](https://www.microsoft.com/security/sir/story/default.aspx#!botnetsection_honeypots_darkents).</span></span> 

<span data-ttu-id="2ffa1-114">OMS 보안 및 감사는 이러한 위협 인텔리전스를 구축하기 위해 Microsoft 내의 여러 소스에서 가져온 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-114">In order to build this threat intelligence, OMS Security and Audit use data coming from multiple sources within Microsoft.</span></span> <span data-ttu-id="2ffa1-115">OMS 보안 및 감사는 이 데이터를 사용하여 사용자 환경에 대한 잠재적 위협을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-115">OMS Security and Audit will leverage this data to identify potential threats against your environment.</span></span>

<span data-ttu-id="2ffa1-116">위협 인텔리전스 창은 세 가지 기본 옵션으로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-116">The Threat Intelligence pane is composed by three major options:</span></span>

* <span data-ttu-id="2ffa1-117">아웃바운드 악성 트래픽이 있는 서버</span><span class="sxs-lookup"><span data-stu-id="2ffa1-117">Servers with outbound malicious traffic</span></span>
* <span data-ttu-id="2ffa1-118">검색된 위협 유형</span><span class="sxs-lookup"><span data-stu-id="2ffa1-118">Detected threats types</span></span>
* <span data-ttu-id="2ffa1-119">위협 인텔리전스 맵</span><span class="sxs-lookup"><span data-stu-id="2ffa1-119">Threat intelligence map</span></span>

> [!NOTE]
> <span data-ttu-id="2ffa1-120">모든 옵션에 대한 개요는 [Operations Management Suite 보안 및 감사 솔루션 시작](oms-security-getting-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-120">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="responding-to-security-alerts"></a><span data-ttu-id="2ffa1-121">보안 경고에 대응</span><span class="sxs-lookup"><span data-stu-id="2ffa1-121">Responding to security alerts</span></span>
<span data-ttu-id="2ffa1-122">[보안 사고 대응](https://technet.microsoft.com/library/cc512623.aspx) 프로세스 단계 중 하나는 손상된 시스템의 심각도를 식별하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-122">One of the steps of a [security incident response](https://technet.microsoft.com/library/cc512623.aspx) process is to identify the severity of the compromise system(s).</span></span> <span data-ttu-id="2ffa1-123">이 단계에서는 다음 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-123">In this phase you should perform the following tasks:</span></span>

* <span data-ttu-id="2ffa1-124">공격 특성 확인</span><span class="sxs-lookup"><span data-stu-id="2ffa1-124">Determine the nature of the attack</span></span>
* <span data-ttu-id="2ffa1-125">공격 원점 확인</span><span class="sxs-lookup"><span data-stu-id="2ffa1-125">Determine the attack point of origin</span></span>
* <span data-ttu-id="2ffa1-126">공격 의도 확인</span><span class="sxs-lookup"><span data-stu-id="2ffa1-126">Determine the intent of the attack.</span></span> <span data-ttu-id="2ffa1-127">특정 정보를 얻기 위해 사용자 조직만 노린 공격입니까, 아니면 무작위 공격입니까?</span><span class="sxs-lookup"><span data-stu-id="2ffa1-127">Was the attack specifically directed at your organization to acquire specific information, or was it random?</span></span>
* <span data-ttu-id="2ffa1-128">손상된 시스템 식별</span><span class="sxs-lookup"><span data-stu-id="2ffa1-128">Identify the systems that have been compromised</span></span>
* <span data-ttu-id="2ffa1-129">액세스된 파일 식별 및 해당 파일의 중요도 확인</span><span class="sxs-lookup"><span data-stu-id="2ffa1-129">Identify the files that have been accessed and determine the sensitivity of those files</span></span>

<span data-ttu-id="2ffa1-130">OMS 보안 및 감사 솔루션의 **위협 인텔리전스** 정보를 활용하여 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-130">You can leverage **Threat Intelligence** information in OMS Security and Audit solution to help with these tasks.</span></span> <span data-ttu-id="2ffa1-131">이 **위협 인텔리전스** 옵션에 액세스하려면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-131">Follow the steps below to access this **Threat Intelligence** options:</span></span>

1. <span data-ttu-id="2ffa1-132">**Microsoft Operations Management Suite** 기본 대시보드에서 **보안 및 감사** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-132">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![보안 및 감사](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="2ffa1-134">아래와 같이 **보안 및 감사** 대시보드의 오른쪽에 **위협 인텔리전스** 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-134">In the **Security and Audit** dashboard, you will see the **Threat Intelligence** options in the right, as shown below:</span></span>
   
    ![위협 인텔리전스](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig2-ga.png)

<span data-ttu-id="2ffa1-136">이러한 세 타일은 현재 위협에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-136">These three tiles will give you an overview of the current threats.</span></span> <span data-ttu-id="2ffa1-137">**아웃바운드 악성 트래픽이 있는 서버** 에서는 모니터링 중인 컴퓨터(네트워크 내부 또는 외부)에서 인터넷에 악성 트래픽을 전송하고 있는지 여부를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-137">In the **Server with outbound malicious traffic** you will be able to identify if there is any computer that you are monitoring (inside or outside of your network) that is sending malicious traffic to the Internet.</span></span> 

<span data-ttu-id="2ffa1-138">**검색된 위협 유형** 타일에는 현재 "널리 퍼져 있는" 위협의 요약이 표시되며 이 타일을 클릭하면 아래와 같이 이러한 위협에 대한 자세한 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-138">The **Detected threat types** tile shows a summary of the threats that are current “in the wild”, if you click on this tile you will see more details about these threats as show below:</span></span>

![검색된 위협 유형](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig3.png)

<span data-ttu-id="2ffa1-140">각 위협을 클릭하여 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-140">You can extract more information about each threat by clicking on it.</span></span> <span data-ttu-id="2ffa1-141">아래 예는 봇넷에 대한 자세한 정보를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-141">The example below shows more details about Botnet:</span></span>

![위협에 대한 자세한 내용](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig4.png)

<span data-ttu-id="2ffa1-143">이 섹션의 시작 부분에서 설명한 대로 이 정보는 사고 대응 사례에서 매우 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-143">As described in the beginning of this section, this information can be very useful during an incident response case.</span></span> <span data-ttu-id="2ffa1-144">또한 공격 원점, 손상된 시스템, 시기를 찾아야 하는 범죄 수사에서도 중요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-144">It can also be important during a forensic investigation, where you need to find the source of the attack, which system was compromised and the timeline.</span></span> <span data-ttu-id="2ffa1-145">이 보고서에서는 공격 원점, 손상된 로컬 IP, 연결의 현재 세션 상태와 같이 공격에 대한 주요 정보를 쉽게 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-145">In this report you can easily identify some key details about the attack, such as: the source of the attack, the local IP that was compromised and the current session state of the connection.</span></span> 

<span data-ttu-id="2ffa1-146">**위협 인텔리전스 맵**에서는 전 세계에서 악성 트래픽이 있는 현재 위치를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-146">The **threat intelligence map** will help you to identify the current locations around the globe that have malicious traffic.</span></span> <span data-ttu-id="2ffa1-147">이 맵에는 트래픽의 방향을 식별하는 주황색(들어오는) 및 빨간색(나가는) 화살표가 있습니다. 각 화살표를 클릭하면 아래와 같이 위협의 유형과 트래픽의 방향이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-147">There are orange (incoming) and red (outgoing) arrows in this map that identify the traffic direction, if you click in one of these arrows, it will show the type of threat and the traffic direction as shown below:</span></span>

![위협 인텔리전스 맵](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig5.png)

> [!NOTE]
> <span data-ttu-id="2ffa1-149">인시던트 응답 프로세스 중에 이 기능을 사용하는 방법에 대한 데모는 Microsoft Ignite에서 제공하는 [Operations Management Suite를 사용하여 안내식 조사를 통해 데이터 센터 보안 위협 완화](https://myignite.microsoft.com/videos/5000) 프레젠테이션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-149">You can see a demonstration on how to use this capability during an incident response process by watching the presentation [Mitigate datacenter security threats with guided investigation using Operations Management Suite](https://myignite.microsoft.com/videos/5000) delivered at Microsoft Ignite.</span></span>
> 

### <a name="responding-to-distinct-malicious-ip-accessed"></a><span data-ttu-id="2ffa1-150">액세스한 명확한 악성 IP에 대한 대응</span><span class="sxs-lookup"><span data-stu-id="2ffa1-150">Responding to distinct malicious IP accessed</span></span>
<span data-ttu-id="2ffa1-151">일부 시나리오에서는 모니터링되는 한 컴퓨터에서 잠재적인 악성 IP에 액세스한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-151">In some scenarios, you may notice a potential malicious IP that was accessed from one monitored computer:</span></span>

![위협 인텔리전스 맵](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

<span data-ttu-id="2ffa1-153">이 경고와 같은 범주 내의 다른 경고는 [Microsoft 위협 인텔리전스](https://youtu.be/O4WtxgUrDc8)를 활용하여 OMS 보안을 통해 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-153">This alert and others within the same category, are generated via OMS Security by leveraging [Microsoft Threat Intelligence](https://youtu.be/O4WtxgUrDc8).</span></span> <span data-ttu-id="2ffa1-154">위협 인텔리전스 데이터는 Microsoft에서 수집하며 업계 선두적인 위협 인텔리전스 공급자로부터 구입합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-154">The Threat Intelligence data is collected by Microsoft as well as purchased from leading threat intelligence providers.</span></span> <span data-ttu-id="2ffa1-155">이 데이터는 자주 업데이트되며 빠르게 변화하는 위협에 대해 대응합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-155">This data is updated frequently and adapted to fast-moving threats.</span></span> <span data-ttu-id="2ffa1-156">이러한 특성으로 인해 보안 경고를 [조사](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)하는 동안 다른 보안 정보 원본과 결합되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-156">Due to its nature, it should be combined with other sources of security information while [investigating](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/) a security alert.</span></span> 

## <a name="customize-alerts-received-via-e-mail"></a><span data-ttu-id="2ffa1-157">전자 메일을 통해 수신한 경고를 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="2ffa1-157">Customize alerts received via e-mail</span></span>

<span data-ttu-id="2ffa1-158">OMS 보안을 통해 보안 경고가 트리거되면 조직의 어떤 사용자에게 통보할지 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-158">You can customize which users in your organization will be notified when security alerts are triggered by OMS Security.</span></span> <span data-ttu-id="2ffa1-159">이 옵션은 OMS 대시보드의 개요/설정에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-159">This option is available under Overview / Settings at the OMS dashboard:</span></span>

![Email](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig7.png)

## <a name="see-also"></a><span data-ttu-id="2ffa1-161">참고 항목</span><span class="sxs-lookup"><span data-stu-id="2ffa1-161">See also</span></span>
<span data-ttu-id="2ffa1-162">이 문서에서는 OMS 보안 및 감사 솔루션의 **위협 인텔리전스** 옵션을 사용하여 보안 경고에 대응하는 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-162">In this document, you learned how to use the **Threat Intelligence** option in OMS Security and Audit solution to respond to security alerts.</span></span> <span data-ttu-id="2ffa1-163">OMS 보안에 대해 자세히 알아보려면 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2ffa1-163">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="2ffa1-164">OMS(Operations Management Suite) 개요</span><span class="sxs-lookup"><span data-stu-id="2ffa1-164">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="2ffa1-165">Operations Management Suite 보안 및 감사 솔루션 시작</span><span class="sxs-lookup"><span data-stu-id="2ffa1-165">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="2ffa1-166">Operations Management Suite 보안 및 감사 솔루션의 리소스 모니터링</span><span class="sxs-lookup"><span data-stu-id="2ffa1-166">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

