---
title: "B2B-Azure 논리 앱에 대 한 통합 aaaEnterprise | Microsoft Docs"
description: "B2B 워크플로 작성 하 고 엔터프라이즈 통합 팩 hello 사용 하 여 논리 앱에 대 한 엔터프라이즈 통합 시나리오를 지원 합니다."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="f5178-103">개요: B2B 시나리오 및 엔터프라이즈 통합 팩 hello와의 통신</span><span class="sxs-lookup"><span data-stu-id="f5178-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="f5178-104">기업 (B2B) 워크플로 및 Azure 논리 앱와 원활 하 게 통신에 대 한 Microsoft의 클라우드 기반 솔루션에서는 엔터프라이즈 통합 팩 hello 엔터프라이즈 통합 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="f5178-105">조직에서는 다른 프로토콜 및 형식을 사용하더라도 전자 방식으로 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="f5178-106">다양 한 형식 시스템의 조직에서 해석 하 고 처리할 수 있는 한 형식으로 변환 하는 hello 팩.</span><span class="sxs-lookup"><span data-stu-id="f5178-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="f5178-107">조직은 [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) 및 [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md)를 비롯한 업계 표준 프로토콜을 통해 메시지를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="f5178-108">암호화 및 디지털 서명 둘 다를 사용하여 메시지를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="f5178-109">BizTalk Server 또는 Microsoft Azure BizTalk 서비스에 잘 알고 있다면 hello 엔터프라이즈 통합 기능은 쉽게 toouse 대부분 개념 유사 하기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="f5178-110">한 가지 주요 차이점은 엔터프라이즈 통합 통합 계정 toosimplify hello 저장소 및 관리의 B2B 통신에 사용 되는 아티팩트를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="f5178-111">아키텍처 측면에서 엔터프라이즈 통합 팩 hello "통합 계정"은 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="f5178-112">이러한 계정은 스키마, 파트너, 인증서, 맵 및 규약 등의 모든 사용자 아티팩트를 저장하는 클라우드 기반 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="f5178-113">이러한 아티팩트 toodesign 사용 지정, 배포 및 B2B 응용 프로그램 및 또한 논리 앱에 대 한 toobuild B2B 워크플로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="f5178-114">하지만 통합 계정 tooyour 논리 앱 전에 이러한 아티팩트를 사용 하려면 먼저 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="f5178-115">그런 후에 논리 앱에서 통합 계정의 아티팩트에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="f5178-116">엔터프라이즈 통합을 사용하는 이유</span><span class="sxs-lookup"><span data-stu-id="f5178-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="f5178-117">엔터프라이즈 통합을 사용하면 통합 계정에 모든 아티팩트를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="f5178-118">B2B 워크플로 작성 하 고 hello Azure 논리 앱 엔진 및 모든 커넥터를 사용 하 여 제 3 자 소프트웨어 as service (SaaS) 앱, 온-프레미스 응용 프로그램, 사용자 지정 앱와 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="f5178-119">Azure Functions를 사용하여 Logic Apps에 대한 사용자 지정 코드를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="f5178-120">Tooget를 어떻게 시작 엔터프라이즈 통합?</span><span class="sxs-lookup"><span data-stu-id="f5178-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="f5178-121">빌드하고 hello에 hello 논리가 응용 프로그램 디자이너를 통해 엔터프라이즈 통합 팩 hello 사용 하 여 B2B 앱을 관리할 수 있습니다 **Azure 포털**합니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="f5178-122">[PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic Apps PowerShell 항목")을 사용하여 Logic Apps를 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="f5178-123">Hello Azure 포털에서에서 앱을 만들기 전에 수행 해야 하는 hello 상위 수준 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![개요 이미지](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="f5178-125">몇 가지 일반적인 시나리오는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="f5178-125">What are some common scenarios?</span></span>

<span data-ttu-id="f5178-126">엔터프라이즈 통합은 이러한 업계 표준을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="f5178-127">EDI - 전자 데이터 교환</span><span class="sxs-lookup"><span data-stu-id="f5178-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="f5178-128">EAI - 엔터프라이즈 응용 프로그램 통합</span><span class="sxs-lookup"><span data-stu-id="f5178-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="f5178-129">여기에 시작 tooget</span><span class="sxs-lookup"><span data-stu-id="f5178-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="f5178-130">통합 계정을 사용하는 Azure 구독</span><span class="sxs-lookup"><span data-stu-id="f5178-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="f5178-131">Visual Studio 2015 toocreate 맵과 스키마</span><span class="sxs-lookup"><span data-stu-id="f5178-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="f5178-132">Visual Studio용 Microsoft Azure Logic Apps 엔터프라이즈 통합 도구 2015 2.0</span><span class="sxs-lookup"><span data-stu-id="f5178-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="f5178-133">지금 평가판 사용</span><span class="sxs-lookup"><span data-stu-id="f5178-133">Try it now</span></span>

<span data-ttu-id="f5178-134">[배포 완벽 하 게 작동 샘플 AS2 송신 및 수신 논리 앱](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) Azure 논리 앱에 대 한 hello B2B 기능을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5178-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="f5178-135">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="f5178-135">Learn more</span></span>
* [<span data-ttu-id="f5178-136">규약</span><span class="sxs-lookup"><span data-stu-id="f5178-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")
* [<span data-ttu-id="f5178-137">비즈니스 tooBusiness (B2B) 시나리오</span><span class="sxs-lookup"><span data-stu-id="f5178-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "학습 방법을 B2B 기능을 사용 하 여 toocreate 논리 앱")  
* [<span data-ttu-id="f5178-138">인증서</span><span class="sxs-lookup"><span data-stu-id="f5178-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "엔터프라이즈 통합 인증서에 대해 알아보기")
* [<span data-ttu-id="f5178-139">플랫 파일 인코딩/디코딩</span><span class="sxs-lookup"><span data-stu-id="f5178-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "학습 방법을 tooencode 및 플랫 파일 내용을 디코딩")  
* [<span data-ttu-id="f5178-140">Integration accounts</span><span class="sxs-lookup"><span data-stu-id="f5178-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn about 통합 계정")
* [<span data-ttu-id="f5178-141">맵</span><span class="sxs-lookup"><span data-stu-id="f5178-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "엔터프라이즈 통합 맵에 대해 알아보기")
* [<span data-ttu-id="f5178-142">파트너</span><span class="sxs-lookup"><span data-stu-id="f5178-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "엔터프라이즈 통합 파트너에 대해 알아보기")
* [<span data-ttu-id="f5178-143">스키마</span><span class="sxs-lookup"><span data-stu-id="f5178-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "엔터프라이즈 통합 스키마에 대해 알아보기")
* [<span data-ttu-id="f5178-144">XML 메시지 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="f5178-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "논리 앱 toovalidate XML 메시지 하는 방법을 알아봅니다")
* [<span data-ttu-id="f5178-145">XML 변환</span><span class="sxs-lookup"><span data-stu-id="f5178-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "엔터프라이즈 통합 맵에 대해 알아보기")
* [<span data-ttu-id="f5178-146">엔터프라이즈 통합 커넥터</span><span class="sxs-lookup"><span data-stu-id="f5178-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "엔터프라이즈 통합 팩 커넥터에 대해 알아보기")
* [<span data-ttu-id="f5178-147">통합 계정 메타데이터</span><span class="sxs-lookup"><span data-stu-id="f5178-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "통합 계정 메타데이터에 대해 알아보기")
* [<span data-ttu-id="f5178-148">B2B 메시지 모니터링</span><span class="sxs-lookup"><span data-stu-id="f5178-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "B2B 메시지를 모니터링하는 방법에 대해 알아보기")
* [<span data-ttu-id="f5178-149">OMS 포털에서 B2B 메시지 추적</span><span class="sxs-lookup"><span data-stu-id="f5178-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "OMS 포털에서 B2B 메시지를 추적하는 방법에 대해 알아보기")

