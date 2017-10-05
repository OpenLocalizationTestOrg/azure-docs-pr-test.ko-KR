---
title: "Azure에서 New Relic 사용 | Microsoft Docs"
description: "New Relic 서비스를 사용하여 Azure 응용 프로그램을 관리 및 모니터링하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: f4f13c909a6ff640d403f5264004176c087925dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="39be3-103">Azure에서 New Relic 응용 프로그램 성능 관리</span><span class="sxs-lookup"><span data-stu-id="39be3-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="39be3-104">Azure 호스티드 응용 프로그램에 세계 최고 수준의 New Relic 성능 모니터링을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-104">You can add New Relic's world-class performance monitoring to your Azure hosted applications.</span></span> <span data-ttu-id="39be3-105">Azure 앱의 모니터링, 문제 해결 및 튜닝하는 포괄적인 기능과 함께 Azure를 사용하여 New Relic 제품을 할인된 가격으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="39be3-106">New Relic 정의</span><span class="sxs-lookup"><span data-stu-id="39be3-106">What is New Relic?</span></span>
<span data-ttu-id="39be3-107">[New Relic 제품](https://newrelic.com/products)을 사용하여 앱 오류를 해결하고 잠재적인 문제에 앞서 전체 환경의 성능을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand the performance of your entire environment.</span></span> <span data-ttu-id="39be3-108">성능 문제를 확인하고 진단할 때 시간을 절약할 수 있도록 설계되었으며, 성능 문제를 해결하는 데 필요한 정보를 즉시 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-108">It is designed to save you time when identifying and diagnosing performance issues, and it puts the information you need to solve these issues at your fingertips.</span></span>

<span data-ttu-id="39be3-109">New Relic은 서버 및 사용자 브라우저의 웹 트랜잭션에 대한 부하 시간 및 처리량을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-109">New Relic tracks the load time and throughput for your web transactions, both from the server and your users' browsers.</span></span> <span data-ttu-id="39be3-110">그리고 데이터베이스 사용 시간을 보여 주고, 느린 쿼리 및 웹 요청을 분석하고, 가동 시간 모니터링 및 경고를 제공하고, 응용 프로그램 예외를 추적하는 등의 다양한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-110">It shows how much time you spend in the database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="39be3-111">특별가</span><span class="sxs-lookup"><span data-stu-id="39be3-111">Special pricing</span></span>
<span data-ttu-id="39be3-112">New Relic Standard는 Azure 사용자에게 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-112">New Relic Standard is free to Azure users.</span></span> <span data-ttu-id="39be3-113">New Relic Pro는 Azure Cloud Services의 인스턴스 크기에 따라 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="39be3-114">가격 책정 정보에 대 한 참조는 [New Relic 페이지](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) Azure 마켓플레이스 또는 연락처 New Relic에서 (sales@newrelic.com) 엔터프라이즈 수준의 가격에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-114">For pricing information, see the [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in the Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="39be3-115">Azure 고객은 New Relic 에이전트를 배포할 때 New Relic Pro에 대해 2주의 평가판 구독을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy the New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-the-azure-store"></a><span data-ttu-id="39be3-116">Azure 스토어를 사용하여 New Relic에 등록</span><span class="sxs-lookup"><span data-stu-id="39be3-116">Sign up for New Relic using the Azure Store</span></span>
<span data-ttu-id="39be3-117">New Relic은 Azure 웹 역할 및 작업자 역할과 원활하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="39be3-118">쉽고 빠르게 Azure Store에서 직접 New Relic에 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-118">You can quickly and easily sign up for New Relic directly from the Azure Store.</span></span> <span data-ttu-id="39be3-119">자세한 내용은 New Relic에서 [Azure Store 등록 지침](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39be3-119">For instructions, see the [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="39be3-120">데이터 보기</span><span class="sxs-lookup"><span data-stu-id="39be3-120">View your data</span></span>
<span data-ttu-id="39be3-121">일단 등록하면 New Relic의 훌륭한 응용 프로그램 모니터링 및 데이터 중심 분석을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="39be3-122">New Relic에서 앱의 성능을 확인하려면:</span><span class="sxs-lookup"><span data-stu-id="39be3-122">To check your app's performance in New Relic:</span></span>

1. <span data-ttu-id="39be3-123">Azure Portal에서 관리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-123">From the Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="39be3-124">New Relic 계정 전자 메일 및 암호로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="39be3-125">응용 프로그램 인덱스에서 앱을 선택하여 [APM 개요 페이지](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page)에서 모든 앱의 데이터를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="39be3-125">Select your app from the Application index to view all your app's data in the [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="39be3-126">Azure에서 New Relic 사용</span><span class="sxs-lookup"><span data-stu-id="39be3-126">Using New Relic with Azure</span></span>
<span data-ttu-id="39be3-127">New Relic 및 Azure를 사용하는 방법에 대한 자세한 내용은 다음을 비롯한 [New Relic 설명서 사이트](https://docs.newrelic.com/docs/agents/net-agent/azure-installation)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="39be3-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="39be3-128">.NET용 New Relic</span><span class="sxs-lookup"><span data-stu-id="39be3-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="39be3-129">Azure 클라우드 서비스에 대한 .NET 작업자 역할 계측</span><span class="sxs-lookup"><span data-stu-id="39be3-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="39be3-130">Microsoft Azure 클라우드 플랫폼용 New Relic</span><span class="sxs-lookup"><span data-stu-id="39be3-130">New Relic for the Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="39be3-131">Microsoft Azure App Services용 New Relic</span><span class="sxs-lookup"><span data-stu-id="39be3-131">New Relic for the Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="39be3-132">New Relic/Azure 문제 해결</span><span class="sxs-lookup"><span data-stu-id="39be3-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

