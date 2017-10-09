---
title: "aaaAzure 앱 서비스 환경 관리 주소"
description: "목록 hello 관리 주소가 toocommand 앱 서비스 환경 사용"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="50bd7-103">App Service Environment 관리 주소</span><span class="sxs-lookup"><span data-stu-id="50bd7-103">App Service Environment management addresses</span></span>

<span data-ttu-id="50bd7-104">앱 서비스 Environment(ASE) hello는 Azure 가상 네트워크 (VNet)에서 서브넷에 hello Azure 앱 서비스의 배포입니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-104">hello App Service Environment(ASE) is a deployment of hello Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="50bd7-105">관리할 수 있도록 hello ASE hello Azure 앱 서비스에서에서 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-105">hello ASE must be accessible from hello Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="50bd7-106">이 ASE 관리 트래픽을 hello 사용자 제어 네트워크에서 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-106">This ASE management traffic traverses hello user controlled network.</span></span>  <span data-ttu-id="50bd7-107">Azure 앱 서비스 관리 서버 toohello 공용 VIP hello ASE 연관 된에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-107">It comes from Azure App Service management servers toohello public VIP that is associated with hello ASE.</span></span>  <span data-ttu-id="50bd7-108">Hello ASE에 대 한 자세한 내용은 종속성 네트워킹 읽을 [네트워킹 고려 사항 및 앱 서비스 환경 hello][networking]합니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-108">For details on hello ASE networking dependencies read [Networking considerations and hello App Service Environment][networking].</span></span>  <span data-ttu-id="50bd7-109">Hello ASE에 대 한 일반적인 정보로 시작할 수 있습니다 [소개 toohello 앱 서비스 환경][intro]합니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-109">For general information on hello ASE you can start with [Introduction toohello App Service Environment][intro].</span></span>

<span data-ttu-id="50bd7-110">이 문서에 대 한 관리 트래픽 toohello ASE hello 원본 Ip를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-110">This document lists hello source IPs for management traffic toohello ASE.</span></span> <span data-ttu-id="50bd7-111">이러한 주소 toocreate 네트워크 보안 그룹 toolock 들어오는 트래픽 다운을 사용 하거나 필요에 따라 경로 테이블에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-111">You can use these addresses toocreate Network Security Groups toolock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="50bd7-112">toouse toouse 필요한이 정보:</span><span class="sxs-lookup"><span data-stu-id="50bd7-112">toouse this information you need toouse:</span></span>

* <span data-ttu-id="50bd7-113">모든 지역에 대해 나열 된 hello IP 주소</span><span class="sxs-lookup"><span data-stu-id="50bd7-113">hello IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="50bd7-114">hello IP 주소 여 ASE에 배포 된 해당 일치 toohello 지역.</span><span class="sxs-lookup"><span data-stu-id="50bd7-114">hello IP addresses that match toohello region that your ASE is deployed into.</span></span>

<span data-ttu-id="50bd7-115">hello 들어오는 관리 트래픽에 이러한 IP 주소에서 tooports 454 및 455 있습니다.</span><span class="sxs-lookup"><span data-stu-id="50bd7-115">hello incoming management traffic comes in from these IP addresses tooports 454 and 455.</span></span>

| <span data-ttu-id="50bd7-116">지역</span><span class="sxs-lookup"><span data-stu-id="50bd7-116">Region</span></span> | <span data-ttu-id="50bd7-117">주소</span><span class="sxs-lookup"><span data-stu-id="50bd7-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="50bd7-118">모든 지역</span><span class="sxs-lookup"><span data-stu-id="50bd7-118">All regions</span></span> | <span data-ttu-id="50bd7-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="50bd7-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="50bd7-120">미국 중남부, 미국 중북부</span><span class="sxs-lookup"><span data-stu-id="50bd7-120">South Central US & North Central US</span></span> | <span data-ttu-id="50bd7-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="50bd7-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="50bd7-122">오스트레일리아 남동부, 오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="50bd7-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="50bd7-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="50bd7-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="50bd7-124">미국 서부, 미국 동부</span><span class="sxs-lookup"><span data-stu-id="50bd7-124">US West & US East</span></span> | <span data-ttu-id="50bd7-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="50bd7-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="50bd7-126">서유럽, 북유럽</span><span class="sxs-lookup"><span data-stu-id="50bd7-126">West Europe & North Europe</span></span> | <span data-ttu-id="50bd7-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="50bd7-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="50bd7-128">미국 중서부, 미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="50bd7-128">West Central US & West US 2</span></span> | <span data-ttu-id="50bd7-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="50bd7-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="50bd7-130">미국 중부, 미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="50bd7-130">Central US & East US 2</span></span> | <span data-ttu-id="50bd7-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="50bd7-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="50bd7-132">동아시아, 동남 아시아</span><span class="sxs-lookup"><span data-stu-id="50bd7-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="50bd7-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="50bd7-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="50bd7-134">일본 동부, 일본 서부</span><span class="sxs-lookup"><span data-stu-id="50bd7-134">Japan East & Japan West</span></span> | <span data-ttu-id="50bd7-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="50bd7-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="50bd7-136">캐나다 중부, 캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="50bd7-136">Canada Central & Canada East</span></span> | <span data-ttu-id="50bd7-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="50bd7-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="50bd7-138">영국 서부, 영국 남부</span><span class="sxs-lookup"><span data-stu-id="50bd7-138">UK West & UK South</span></span> | <span data-ttu-id="50bd7-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="50bd7-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="50bd7-140">한국 남부, 한국 중부</span><span class="sxs-lookup"><span data-stu-id="50bd7-140">Korea South & Korea Central</span></span> | <span data-ttu-id="50bd7-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="50bd7-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="50bd7-142">브라질 남부, 미국 중남부</span><span class="sxs-lookup"><span data-stu-id="50bd7-142">Brazil South & South Central US</span></span>| <span data-ttu-id="50bd7-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="50bd7-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="50bd7-144">인도 중부, 인도 남부</span><span class="sxs-lookup"><span data-stu-id="50bd7-144">Central India & South India</span></span> | <span data-ttu-id="50bd7-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="50bd7-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="50bd7-146">인도 서부, 인도 남부</span><span class="sxs-lookup"><span data-stu-id="50bd7-146">West India & South India</span></span> | <span data-ttu-id="50bd7-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="50bd7-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
