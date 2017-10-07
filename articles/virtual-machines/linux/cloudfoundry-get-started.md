---
title: "Microsoft Azure에서 클라우드 대장간 시작 aaaGetting | Microsoft Docs"
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
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a><span data-ttu-id="fbd35-103">Azure의 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="fbd35-103">Cloud Foundry on Azure</span></span>

<span data-ttu-id="fbd35-104">Cloud Foundry는 다양한 언어 및 프레임워크로 개발되는 12개 요소(12-factor) 응용 프로그램을 빌드하고, 배포하고, 운영하기 위한 오픈 소스 PaaS(Platform-as-a-Service)입니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-104">Cloud Foundry is an open-source platform-as-a-service (PaaS) for building, deploying, and operating 12-factor applications developed in various languages and frameworks.</span></span> <span data-ttu-id="fbd35-105">이 문서에서는 Azure 및 시작할 수 있는 방법에서 클라우드 대장간 실행에 대 한 hello 옵션 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-105">This document describes hello options you have for running Cloud Foundry on Azure and how you can get started.</span></span>

## <a name="cloud-foundry-offerings"></a><span data-ttu-id="fbd35-106">Cloud Foundry 제품</span><span class="sxs-lookup"><span data-stu-id="fbd35-106">Cloud Foundry offerings</span></span>

<span data-ttu-id="fbd35-107">두 가지 방법으로 Azure에서 사용할 수 있는 toorun 클라우드 대장간 형식의: 오픈 소스 클라우드 대장간 (OSS CF) 및 중요 클라우드 대장간 (PCF).</span><span class="sxs-lookup"><span data-stu-id="fbd35-107">There are two forms of Cloud Foundry available toorun on Azure: open-source Cloud Foundry (OSS CF) and Pivotal Cloud Foundry (PCF).</span></span> <span data-ttu-id="fbd35-108">OSS CF는는 완전히 [오픈 소스](https://github.com/cloudfoundry) hello 클라우드 대장간 Foundation에서 관리 하는 클라우드 대장간의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-108">OSS CF is an entirely [open-source](https://github.com/cloudfoundry) version of Cloud Foundry managed by hello Cloud Foundry Foundation.</span></span> <span data-ttu-id="fbd35-109">중요 클라우드 대장간은 중요 소프트웨어 inc.에서 클라우드 대장간은 엔터프라이즈 배포 보면 hello 차이점 hello 두 가지 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-109">Pivotal Cloud Foundry is an enterprise distribution of Cloud Foundry from Pivotal Software Inc. We look at some of hello differences between hello two offerings.</span></span>

### <a name="open-source-cloud-foundry"></a><span data-ttu-id="fbd35-110">오픈 소스 Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="fbd35-110">Open-source Cloud Foundry</span></span>

<span data-ttu-id="fbd35-111">먼저 BOSH 디렉터를 배포 하 고 다음 클라우드 대장간, hello를 사용 하 여를 배포 하 여 Azure에서 클라우드 대장간 OSS를 배포할 수 있습니다 [GitHub에서 제공 된 지침](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-111">You can deploy OSS Cloud Foundry on Azure by first deploying a BOSH director and then deploying Cloud Foundry, using hello [instructions provided on GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md).</span></span> <span data-ttu-id="fbd35-112">OSS CF 사용에 대 한 더 toolearn 참조 hello [설명서](https://docs.cloudfoundry.org/) hello 클라우드 대장간 Foundation에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-112">toolearn more about using OSS CF, see hello [documentation](https://docs.cloudfoundry.org/) provided by hello Cloud Foundry Foundation.</span></span>

<span data-ttu-id="fbd35-113">Microsoft는 커뮤니티 채널을 따라 hello 통해 OSS CF에 대 한 최상의 지원:</span><span class="sxs-lookup"><span data-stu-id="fbd35-113">Microsoft provides best-effort support for OSS CF through hello following community channels:</span></span>

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a><span data-ttu-id="fbd35-114">[Cloud Foundry Slack](https://slack.cloudfoundry.org/)의 bosh-azure-cpi 채널</span><span class="sxs-lookup"><span data-stu-id="fbd35-114">bosh-azure-cpi channel on [Cloud Foundry Slack](https://slack.cloudfoundry.org/)</span></span>
- [<span data-ttu-id="fbd35-115">cf-bosh mailing list</span><span class="sxs-lookup"><span data-stu-id="fbd35-115">cf-bosh mailing list</span></span>](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- <span data-ttu-id="fbd35-116">Hello에 대 한 GitHub 문제 [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) 및 [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span><span class="sxs-lookup"><span data-stu-id="fbd35-116">GitHub issues for hello [CPI](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) and [service broker](https://github.com/Azure/meta-azure-service-broker/issues)</span></span>

>[!NOTE]
> <span data-ttu-id="fbd35-117">같은 hello 가상 컴퓨터 클라우드 대장간을 실행 하 여 Azure 리소스에 대 한 지원 수준은 hello Azure 지원 계약을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-117">hello level of support for your Azure resources, such as hello virtual machines where you run Cloud Foundry, is based on your Azure support agreement.</span></span> <span data-ttu-id="fbd35-118">최상의 커뮤니티 지원은 toohello 클라우드 대장간 관련 구성 요소를만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-118">Best-effort community support only applies toohello Cloud Foundry-specific components.</span></span>

### <a name="pivotal-cloud-foundry"></a><span data-ttu-id="fbd35-119">Pivotal Cloud Foundry</span><span class="sxs-lookup"><span data-stu-id="fbd35-119">Pivotal Cloud Foundry</span></span>

<span data-ttu-id="fbd35-120">중요 클라우드 대장간 포함 hello 소유 관리 도구 및 엔터프라이즈 지원은 집합과 함께 hello OSS 배포로 동일한 핵심 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-120">Pivotal Cloud Foundry includes hello same core platform as hello OSS distribution, along with a set of proprietary management tools and enterprise support.</span></span> <span data-ttu-id="fbd35-121">Azure에서 PCF toorun Pivotal에서 라이선스를 획득 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-121">toorun PCF on Azure, you must acquire a license from Pivotal.</span></span> <span data-ttu-id="fbd35-122">Azure 마켓플레이스 hello에서 hello PCF 제안을 90 일 평가판 라이선스를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-122">hello PCF offer from hello Azure marketplace includes a 90-day trial license.</span></span>

<span data-ttu-id="fbd35-123">hello 도구 포함 [중요 Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), 배포 및 클라우드 대장간 foundation의 관리를 간소화 하는 웹 응용 프로그램 및 [중요 응용 프로그램 관리자](https://docs.pivotal.io/pivotalcf/console/), 관리 하기 위한 웹 응용 프로그램 사용자 및 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-123">hello tools include [Pivotal Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), a web application that simplifies deployment and management of a Cloud Foundry foundation, and [Pivotal Apps Manager](https://docs.pivotal.io/pivotalcf/console/), a web application for managing users and applications.</span></span>

<span data-ttu-id="fbd35-124">또한 위의 OSS CF에 대해 나열 된 지원 채널을 toohello, PCF 라이선스 있습니다 toocontact Pivotal 지원에 대 한를 가진 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-124">In addition toohello support channels listed for OSS CF above, a PCF license entitles you toocontact Pivotal for support.</span></span> <span data-ttu-id="fbd35-125">Microsoft 및 Pivotal도 사용 하도록 설정한 toocontact 할 수 있도록 지원 워크플로 어느 쪽에 있고 hello 문제가에 따라 적절히 라우팅할 질문 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-125">Microsoft and Pivotal have also enabled support workflows that allow you toocontact either party for assistance and have your inquiry routed appropriately depending on where hello issue lies.</span></span>

## <a name="azure-service-broker"></a><span data-ttu-id="fbd35-126">Service Broker</span><span class="sxs-lookup"><span data-stu-id="fbd35-126">Azure Service Broker</span></span>

<span data-ttu-id="fbd35-127">클라우드 대장간 hello이 권장 ["12 단계 app"](https://12factor.net/) 방법을 확실 하 게 구분 상태 비저장 응용 프로그램 프로세스 및 서비스를 백업 하는 상태 저장을 승격 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-127">Cloud Foundry encourages hello ["twelve-factor app"](https://12factor.net/) methodology, which promotes a clean separation of stateless application processes and stateful backing services.</span></span> <span data-ttu-id="fbd35-128">[서비스 브로커](https://docs.cloudfoundry.org/services/api.html) 일관 된 방식으로 tooprovision을 제공 하 고 백업 서비스 tooapplications 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-128">[Service brokers](https://docs.cloudfoundry.org/services/api.html) offer a consistent way tooprovision and bind backing services tooapplications.</span></span> <span data-ttu-id="fbd35-129">hello [Azure service broker](https://github.com/Azure/meta-azure-service-broker) hello 중 일부 Azure 저장소 및 SQL Azure를 포함 하 여이 채널을 통해 핵심 Azure 서비스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-129">hello [Azure service broker](https://github.com/Azure/meta-azure-service-broker) provides some of hello key Azure services through this channel, including Azure storage and Azure SQL.</span></span>

<span data-ttu-id="fbd35-130">중요 클라우드 대장간을 사용 하는 경우 hello service broker는 또한 [타일로 사용할 수 있는](https://docs.pivotal.io/azure-sb/installing.html) hello 중요 네트워크에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-130">If you are using Pivotal Cloud Foundry, hello service broker is also [available as a tile](https://docs.pivotal.io/azure-sb/installing.html) from hello Pivotal Network.</span></span>

## <a name="related-resources"></a><span data-ttu-id="fbd35-131">관련 리소스</span><span class="sxs-lookup"><span data-stu-id="fbd35-131">Related resources</span></span>

### <a name="visual-studio-team-services-plugin"></a><span data-ttu-id="fbd35-132">Visual Studio Team Services 플러그인</span><span class="sxs-lookup"><span data-stu-id="fbd35-132">Visual Studio Team Services plugin</span></span>

<span data-ttu-id="fbd35-133">클라우드 대장간 적합된 tooagile 소프트웨어 개발, CI (연속 통합) 및 지속적인 업데이트 (CD)의 hello 사용입니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-133">Cloud Foundry is well suited tooagile software development, including hello use of continuous integration (CI) and continuous delivery (CD).</span></span> <span data-ttu-id="fbd35-134">VSTS Visual Studio Team Services () toomanage 프로젝트를 사용 하 고 tooset 클라우드 대장간 대상 CI/CD 파이프라인 구성 하려는 경우에 hello을 사용할 수 있습니다 [VSTS 클라우드 대장간 빌드 확장](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension)합니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-134">If you use Visual Studio Team Services (VSTS) toomanage your projects and would like tooset up a CI/CD pipeline targeting Cloud Foundry, you can use hello [VSTS Cloud Foundry build extension](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension).</span></span> <span data-ttu-id="fbd35-135">hello 플러그 인을 사용 하면 간단한 tooconfigure 있으며 Azure 또는 다른 실행에 관계 없이 배포 tooCloud 대장간, 자동화 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="fbd35-135">hello plugin makes it simple tooconfigure and automate deployments tooCloud Foundry, whether running in Azure or another environment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbd35-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fbd35-136">Next steps</span></span>

- [<span data-ttu-id="fbd35-137">중요 클라우드 대장간 hello Azure Marketplace에서 배포</span><span class="sxs-lookup"><span data-stu-id="fbd35-137">Deploy Pivotal Cloud Foundry from hello Azure Marketplace</span></span>](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [<span data-ttu-id="fbd35-138">응용 프로그램 tooCloud 대장간 Azure에서 배포</span><span class="sxs-lookup"><span data-stu-id="fbd35-138">Deploy an app tooCloud Foundry in Azure</span></span>](./cloudfoundry-deploy-your-first-app.md)
