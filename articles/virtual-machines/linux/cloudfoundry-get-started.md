---
title: "Microsoft Azure의 Cloud Foundry 시작 | Microsoft Docs"
description: "Microsoft Azure에서 OSS 또는 Pivotal Cloud Foundry 실행"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 94fbde7707ea9a91076780fdefc3f5a827e0e7b2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-foundry-on-azure"></a><span data-ttu-id="7be1b-103">Azure의 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="7be1b-103">Cloud Foundry on Azure</span></span>

<span data-ttu-id="7be1b-104">Cloud Foundry는 다양한 언어 및 프레임워크로 개발되는 12개 요소(12-factor) 응용 프로그램을 빌드하고, 배포하고, 운영하기 위한 오픈 소스 PaaS(Platform-as-a-Service)입니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in various languages and frameworks.</span></span> <span data-ttu-id="7be1b-105">이 문서는 Azure에서 Cloud Foundry를 실행할 수 있는 옵션과 시작하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-105">This document describes the options you have for running Cloud Foundry on Azure and how you can get started.</span></span>

## <a name="cloud-foundry-offerings"></a><span data-ttu-id="7be1b-106">Cloud Foundry 제품</span><span class="sxs-lookup"><span data-stu-id="7be1b-106">Cloud Foundry offerings</span></span>

<span data-ttu-id="7be1b-107">Azure에서 실행할 수 있는 Cloud Foundry에는 오픈 소스 Cloud Foundry(OSS CF) 및 Pivotal Cloud Foundry(PCF)라는 두 가지 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-107">There are two forms of Cloud Foundry available to run on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span></span> <span data-ttu-id="7be1b-108">OSS CF는 Cloud Foundry Foundation에서 관리하는 Cloud Foundry의 완전한 [오픈-소스](https://github.com/cloudfoundry) 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by the Cloud Foundry Foundation.</span></span> <span data-ttu-id="7be1b-109">Pivotal Cloud Foundry는 Pivotal Software Inc.의 Cloud Foundry 엔터프라이즈 배포판입니다. 이 두 가지 제품의 차이점을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of the differences between the two offerings.</span></span>

### <a name="open-source-cloud-foundry"></a><span data-ttu-id="7be1b-110">오픈 소스 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="7be1b-110">Open-source Cloud Foundry</span></span>

<span data-ttu-id="7be1b-111">Azure에 OSS Cloud Foundry를 배포하려면 [GitHub에 제공된 지침](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md)을 사용하여 우선 BOSH 디렉터를 배포한 다음 Cloud Foundry를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using the [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span></span> <span data-ttu-id="7be1b-112">OSS CF 사용에 대한 자세한 내용은 Cloud Foundry Foundation에서 제공하는 [설명서](https://docs.cloudfoundry.org/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7be1b-112">To learn more about using OSS CF, see the [documentation](https://docs.cloudfoundry.org/) provided by the Cloud Foundry Foundation.</span></span>

<span data-ttu-id="7be1b-113">Microsoft는 다음과 같은 커뮤니티 채널을 통해 OSS CF에 대한 최선의 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-113">Microsoft provides best-effort support for OSS CF through the following community channels:</span></span>

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a><span data-ttu-id="7be1b-114">[Cloud Foundry Slack](https://slack.cloudfoundry.org/)의 bosh-azure-cpi 채널</span><span class="sxs-lookup"><span data-stu-id="7be1b-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span></span>
- [<span data-ttu-id="7be1b-115">cf-bosh mailing list</span><span class="sxs-lookup"><span data-stu-id="7be1b-115">cf-bosh mailing list</span></span>](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- <span data-ttu-id="7be1b-116">[CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) 및 [Service Broker](https://github.com/Azure/meta-azure-service-broker/issues)에 대한 GitHub Issues</span><span class="sxs-lookup"><span data-stu-id="7be1b-116">GitHub issues for the [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span></span>

>[!NOTE]
> <span data-ttu-id="7be1b-117">Cloud Foundry를 실행하는 가상 컴퓨터와 같은 Azure 리소스에 대한 지원 수준은 Azure 지원 계약을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-117">The level of support for your Azure resources, such as the virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span></span> <span data-ttu-id="7be1b-118">최선의 커뮤니티 지원은 Cloud Foundry에 해당하는 구성 요소에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-118">Best-effort community support only applies to the Cloud Foundry-specific components.</span></span>

### <a name="pivotal-cloud-foundry"></a><span data-ttu-id="7be1b-119">Pivotal Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="7be1b-119">Pivotal Cloud Foundry</span></span>

<span data-ttu-id="7be1b-120">Pivotal Cloud Foundry는 독점적인 관리 도구 및 엔터프라이즈 지원과 더불어 OSS 배포판과 동일한 핵심 플랫폼을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-120">Pivotal Cloud Foundry includes the same core platform as the OSS distribution, along with a set of proprietary management tools and enterprise support.</span></span> <span data-ttu-id="7be1b-121">PCF를 Azure에서 실행하려면 Pivotal로부터 라이선스를 취득해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-121">To run PCF on Azure, you must acquire a license from Pivotal.</span></span> <span data-ttu-id="7be1b-122">Azure Marketplace의 PCF 제품에는 90일 평가판 라이선스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-122">The PCF offer from the Azure marketplace includes a 90-day trial license.</span></span>

<span data-ttu-id="7be1b-123">이 도구는 Cloud Foundry Foundation의 배포 및 관리를 간소화하는 웹 응용 프로그램인 [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/)와 사용자 및 응용 프로그램 관리를 위한 웹 응용 프로그램인 [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/)를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-123">The tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span></span>

<span data-ttu-id="7be1b-124">위에 나열된 OSS CF에 대한 지원 채널 외에도 PCF 라이선스를 취득하면 Pivotal에 지원을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-124">In addition to the support channels listed for OSS CF above, a PCF license entitles you to contact Pivotal for support.</span></span> <span data-ttu-id="7be1b-125">Microsoft와 Pivotal에는 두 회사 중 어느 곳에라도 지원을 요청하면 문제의 소재에 따라 적절하게 질의가 전달될 수 있는 지원 워크플로가 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-125">Microsoft and Pivotal have also enabled support workflows that allow you to contact either party for assistance and have your inquiry routed appropriately depending on where the issue lies.</span></span>

## <a name="azure-service-broker"></a><span data-ttu-id="7be1b-126">Service Broker</span><span class="sxs-lookup"><span data-stu-id="7be1b-126">Azure Service Broker</span></span>

<span data-ttu-id="7be1b-127">Cloud Foundry는 상태 비저장 응용 프로그램 프로세스와 상태 저장 백업 서비스의 완전한 분리를 조장하는 ["twelve-factor app"](https://12factor.net/) 방법론을 장려합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-127">Cloud Foundry encourages the ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span></span> <span data-ttu-id="7be1b-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html)는 응용 프로그램에 대한 백업 서비스를 바인딩하고 프로비전하는 일관적인 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way to provision and bind backing services to applications.</span></span> <span data-ttu-id="7be1b-129">[Azure Service Broker](https://github.com/Azure/meta-azure-service-broker)는 이러한 채널을 통해 Azure Storage 및 Azure SQL을 비롯한 주요한 Azure 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-129">The [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of the key Azure services through this channel, including Azure storage and Azure SQL.</span></span>

<span data-ttu-id="7be1b-130">Pivotal Cloud Foundry를 사용하는 경우 Service Broker는 Pivotal Network의 [타일로도 제공](https://docs.pivotal.io/azure-sb/installing.html)됩니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-130">If you are using Pivotal Cloud Foundry, the service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from the Pivotal Network.</span></span>

## <a name="related-resources"></a><span data-ttu-id="7be1b-131">관련 리소스</span><span class="sxs-lookup"><span data-stu-id="7be1b-131">Related resources</span></span>

### <a name="visual-studio-team-services-plugin"></a><span data-ttu-id="7be1b-132">Visual Studio Team Services 플러그인</span><span class="sxs-lookup"><span data-stu-id="7be1b-132">Visual Studio Team Services plugin</span></span>

<span data-ttu-id="7be1b-133">Cloud Foundry는 연속 통합(CI) 및 지속적인 업데이트(CD) 사용을 포함하는 Agile 소프트웨어 개발에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-133">Cloud Foundry is well suited to agile software development, including the use of continuous integration (CI) and continuous delivery (CD).</span></span> <span data-ttu-id="7be1b-134">Visual Studio Team Services(VSTS)를 사용하여 프로젝트를 관리하는 경우 Cloud Foundry를 대상으로 하는 CI/CD 파이프라인을 설정하려면 [VSTS Cloud Foundry 빌드 확장](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-134">If you use Visual Studio Team Services (VSTS) to manage your projects and would like to set up a CI/CD pipeline targeting Cloud Foundry, you can use the [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span></span> <span data-ttu-id="7be1b-135">이 플러그 인은 Azure 또는 기타 환경에서 실행 중인 Cloud Foundry에 대한 배포를 구성하고 자동화하는 작업을 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="7be1b-135">The plugin makes it simple to configure and automate deployments to Cloud Foundry, whether running in Azure or another environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7be1b-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7be1b-136">Next steps</span></span>

- [<span data-ttu-id="7be1b-137">Azure Marketplace에서 Pivotal Cloud Foundry 배포</span><span class="sxs-lookup"><span data-stu-id="7be1b-137">Deploy Pivotal Cloud Foundry from the Azure Marketplace</span></span>](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [<span data-ttu-id="7be1b-138">Azure에서 Cloud Foundry에 앱 배포</span><span class="sxs-lookup"><span data-stu-id="7be1b-138">Deploy an app to Cloud Foundry in Azure</span></span>](./cloudfoundry-deploy-your-first-app.md)