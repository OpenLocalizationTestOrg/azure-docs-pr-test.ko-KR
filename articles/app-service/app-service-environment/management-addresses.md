---
title: "Azure App Service Environment 관리 주소"
description: "App Service Environment를 명령하는 데 사용되는 관리 주소를 나열합니다."
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
ms.openlocfilehash: e97a084772fd16252d925b62498d2e696629a25d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/29/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="e7392-103">App Service Environment 관리 주소</span><span class="sxs-lookup"><span data-stu-id="e7392-103">App Service Environment management addresses</span></span>

<span data-ttu-id="e7392-104">ASE(App Service Environment)는 Azure App Service를 사용자의 Azure VNet(Virtual Network)의 서브넷에 배포한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7392-104">The App Service Environment(ASE) is a deployment of the Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="e7392-105">ASE 는 관리가 가능하도록 Azure App Service에서 액세스할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7392-105">The ASE must be accessible from the Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="e7392-106">이 ASE 관리 트래픽은 사용자 제어 네트워크를 통과합니다.</span><span class="sxs-lookup"><span data-stu-id="e7392-106">This ASE management traffic traverses the user controlled network.</span></span>  <span data-ttu-id="e7392-107">Azure App Service 관리 서버에서 나와서 ASE와 연결된 공용 VIP로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e7392-107">It comes from Azure App Service management servers to the public VIP that is associated with the ASE.</span></span>  <span data-ttu-id="e7392-108">ASE 네트워킹 종속성에 대한 자세한 내용은 [네트워킹 고려 사항과 App Service Environment][networking]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7392-108">For details on the ASE networking dependencies read [Networking considerations and the App Service Environment][networking].</span></span>  <span data-ttu-id="e7392-109">시작하는 데 도움이 되는 ASE에 대한 일반적인 정보는 [App Service Environment 소개][intro]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7392-109">For general information on the ASE you can start with [Introduction to the App Service Environment][intro].</span></span>

<span data-ttu-id="e7392-110">이 문서에서는 ASE에 대한 관리 트래픽의 원본 IP를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="e7392-110">This document lists the source IPs for management traffic to the ASE.</span></span> <span data-ttu-id="e7392-111">이 주소를 사용하여 들어오는 트래픽을 잠글 네트워크 보안 그룹을 만들거나 필요에 따라 경로 테이블에서 이 주소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7392-111">You can use these addresses to create Network Security Groups to lock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="e7392-112">이 정보를 사용하려면 다음을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7392-112">To use this information you need to use:</span></span>

* <span data-ttu-id="e7392-113">모든 지역에 대해 나열된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e7392-113">the IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="e7392-114">ASE가 배포되어 있는 지역에 일치하는 IP 주소</span><span class="sxs-lookup"><span data-stu-id="e7392-114">the IP addresses that match to the region that your ASE is deployed into.</span></span>

<span data-ttu-id="e7392-115">들어오는 관리 트래픽은 다음과 같은 IP 주소에서 포트 454 및 포트 455로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e7392-115">The incoming management traffic comes in from these IP addresses to ports 454 and 455.</span></span>

| <span data-ttu-id="e7392-116">지역</span><span class="sxs-lookup"><span data-stu-id="e7392-116">Region</span></span> | <span data-ttu-id="e7392-117">주소</span><span class="sxs-lookup"><span data-stu-id="e7392-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="e7392-118">모든 지역</span><span class="sxs-lookup"><span data-stu-id="e7392-118">All regions</span></span> | <span data-ttu-id="e7392-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="e7392-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="e7392-120">미국 중남부, 미국 중북부</span><span class="sxs-lookup"><span data-stu-id="e7392-120">South Central US & North Central US</span></span> | <span data-ttu-id="e7392-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="e7392-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="e7392-122">오스트레일리아 남동부, 오스트레일리아 동부</span><span class="sxs-lookup"><span data-stu-id="e7392-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="e7392-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="e7392-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="e7392-124">미국 서부, 미국 동부</span><span class="sxs-lookup"><span data-stu-id="e7392-124">US West & US East</span></span> | <span data-ttu-id="e7392-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="e7392-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="e7392-126">서유럽, 북유럽</span><span class="sxs-lookup"><span data-stu-id="e7392-126">West Europe & North Europe</span></span> | <span data-ttu-id="e7392-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="e7392-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="e7392-128">미국 중서부, 미국 서부 2</span><span class="sxs-lookup"><span data-stu-id="e7392-128">West Central US & West US 2</span></span> | <span data-ttu-id="e7392-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="e7392-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="e7392-130">미국 중부, 미국 동부 2</span><span class="sxs-lookup"><span data-stu-id="e7392-130">Central US & East US 2</span></span> | <span data-ttu-id="e7392-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="e7392-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="e7392-132">동아시아, 동남 아시아</span><span class="sxs-lookup"><span data-stu-id="e7392-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="e7392-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="e7392-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="e7392-134">일본 동부, 일본 서부</span><span class="sxs-lookup"><span data-stu-id="e7392-134">Japan East & Japan West</span></span> | <span data-ttu-id="e7392-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="e7392-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="e7392-136">캐나다 중부, 캐나다 동부</span><span class="sxs-lookup"><span data-stu-id="e7392-136">Canada Central & Canada East</span></span> | <span data-ttu-id="e7392-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="e7392-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="e7392-138">영국 서부, 영국 남부</span><span class="sxs-lookup"><span data-stu-id="e7392-138">UK West & UK South</span></span> | <span data-ttu-id="e7392-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="e7392-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="e7392-140">한국 남부, 한국 중부</span><span class="sxs-lookup"><span data-stu-id="e7392-140">Korea South & Korea Central</span></span> | <span data-ttu-id="e7392-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="e7392-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="e7392-142">브라질 남부, 미국 중남부</span><span class="sxs-lookup"><span data-stu-id="e7392-142">Brazil South & South Central US</span></span>| <span data-ttu-id="e7392-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="e7392-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="e7392-144">인도 중부, 인도 남부</span><span class="sxs-lookup"><span data-stu-id="e7392-144">Central India & South India</span></span> | <span data-ttu-id="e7392-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="e7392-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="e7392-146">인도 서부, 인도 남부</span><span class="sxs-lookup"><span data-stu-id="e7392-146">West India & South India</span></span> | <span data-ttu-id="e7392-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="e7392-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
