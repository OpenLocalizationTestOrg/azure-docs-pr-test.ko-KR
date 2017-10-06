---
title: "Azure와 New Relic aaaUsing | Microsoft Docs"
description: "Toouse New Relic 서비스 toomanage hello 하 고 Azure 응용 프로그램을 모니터링 하는 방법에 대해 알아봅니다."
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="9da36-103">Azure에서 New Relic 응용 프로그램 성능 관리</span><span class="sxs-lookup"><span data-stu-id="9da36-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="9da36-104">New Relic 세계적인 수준의 성능을 추가할 수 있습니다 tooyour 모니터링 Azure 호스팅 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="9da36-105">Azure 앱의 모니터링, 문제 해결 및 튜닝하는 포괄적인 기능과 함께 Azure를 사용하여 New Relic 제품을 할인된 가격으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="9da36-106">New Relic 정의</span><span class="sxs-lookup"><span data-stu-id="9da36-106">What is New Relic?</span></span>
<span data-ttu-id="9da36-107">와 [New Relic 제품](https://newrelic.com/products), 응용 프로그램 오류를 해결, 잠재적인 문제를 미리 및 전체 사용자 환경의 hello 성능을 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="9da36-108">식별 및 성능 문제를 진단 하는 경우 시간 디자인 된 toosave 이며 손쉽게 toosolve 이러한 문제 필요한 hello 정보를 가져가서입니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="9da36-109">새 Relic 트랙 hello 시간 및 처리량 웹 트랜잭션의 경우 모두 hello 서버와 사용자의 브라우저에서 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="9da36-110">Hello 데이터베이스에 소요 시간 처리 속도가 느린 쿼리를 분석 하 고 웹 요청, 가동 시간 모니터링 및 경고, 트랙 응용 프로그램 예외와 제공 훨씬 더 많은 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="9da36-111">특별가</span><span class="sxs-lookup"><span data-stu-id="9da36-111">Special pricing</span></span>
<span data-ttu-id="9da36-112">무료 tooAzure 사용자가 새 Relic 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="9da36-113">New Relic Pro는 Azure Cloud Services의 인스턴스 크기에 따라 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="9da36-114">가격 책정 정보 참조 hello [New Relic 페이지](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) hello Azure Marketplace에서 New Relic에 게 문의 하거나 (sales@newrelic.com) 엔터프라이즈 수준의 가격에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="9da36-115">Azure 고객 hello New Relic 에이전트를 배포할 때 새 Relic Pro의 두 가지 주 평가판 구독을 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="9da36-116">Hello Azure 저장소를 사용 하 여 New Relic에 등록</span><span class="sxs-lookup"><span data-stu-id="9da36-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="9da36-117">New Relic은 Azure 웹 역할 및 작업자 역할과 원활하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="9da36-118">쉽게 hello Azure 저장소에서 직접 New Relic에 등록할 빠르고 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="9da36-119">자세한 내용은 hello [Azure 저장 등록 지침](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) New Relic에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="9da36-120">데이터 보기</span><span class="sxs-lookup"><span data-stu-id="9da36-120">View your data</span></span>
<span data-ttu-id="9da36-121">일단 등록하면 New Relic의 훌륭한 응용 프로그램 모니터링 및 데이터 중심 분석을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="9da36-122">toocheck New Relic에 응용 프로그램의 성능:</span><span class="sxs-lookup"><span data-stu-id="9da36-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="9da36-123">Hello Azure 포털에서에서 [관리]를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="9da36-124">New Relic 계정 전자 메일 및 암호로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="9da36-125">에서 앱 선택 응용 프로그램 인덱스 tooview hello에서에서 모든 앱의 데이터 hello [APM 개요 페이지](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page)합니다.</span><span class="sxs-lookup"><span data-stu-id="9da36-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="9da36-126">Azure에서 New Relic 사용</span><span class="sxs-lookup"><span data-stu-id="9da36-126">Using New Relic with Azure</span></span>
<span data-ttu-id="9da36-127">New Relic 및 Azure를 사용하는 방법에 대한 자세한 내용은 다음을 비롯한 [New Relic 설명서 사이트](https://docs.newrelic.com/docs/agents/net-agent/azure-installation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9da36-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="9da36-128">.NET용 New Relic</span><span class="sxs-lookup"><span data-stu-id="9da36-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="9da36-129">Azure 클라우드 서비스에 대한 .NET 작업자 역할 계측</span><span class="sxs-lookup"><span data-stu-id="9da36-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="9da36-130">Microsoft Azure 클라우드 플랫폼 hello에 대 한 새 Relic</span><span class="sxs-lookup"><span data-stu-id="9da36-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="9da36-131">Microsoft Azure 앱 서비스 hello에 대 한 새 Relic</span><span class="sxs-lookup"><span data-stu-id="9da36-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="9da36-132">New Relic/Azure 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9da36-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

