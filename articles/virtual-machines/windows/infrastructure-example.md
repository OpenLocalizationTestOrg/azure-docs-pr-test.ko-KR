---
title: "Azure 인프라 연습 예제 | Microsoft Docs"
description: "Azure에서 인프라 예제를 배포하기 위한 핵심 디자인 및 구현 지침에 대해 알아봅니다."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7032b586-e4e5-4954-952f-fdfc03fc1980
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 84cefcdb85f1a3c753027e827abde010b461cda7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-windows-vms"></a><span data-ttu-id="78584-103">Windows VM에 대한 Azure 인프라 연습 예제</span><span class="sxs-lookup"><span data-stu-id="78584-103">Example Azure infrastructure walkthrough for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="78584-104">이 문서에서는 예제 응용 프로그램 인프라를 구축하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="78584-105">명명 규칙, 가용성 집합, 가상 네트워크 및 부하 분산 장치에 대한 모든 지침 및 결정 사항을 함께 제공하는 간단한 온라인 스토어용 인프라의 설계와 VM(가상 컴퓨터)의 실제 배포를 자세히 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="78584-105">We detail designing an infrastructure for a simple on-line store that brings together all the guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="78584-106">워크로드 예제</span><span class="sxs-lookup"><span data-stu-id="78584-106">Example workload</span></span>
<span data-ttu-id="78584-107">Adventure Works Cycles는 Azure에서 다음으로 구성된 온라인 스토어 응용 프로그램을 구축하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-107">Adventure Works Cycles wants to build an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="78584-108">웹 계층에 있으며 클라이언트 프런트 엔드를 실행하는 두 IIS 서버</span><span class="sxs-lookup"><span data-stu-id="78584-108">Two IIS servers running the client front-end in a web tier</span></span>
* <span data-ttu-id="78584-109">응용 프로그램 계층에 있으며 데이터 및 주문을 처리하는 두 IIS 서버</span><span class="sxs-lookup"><span data-stu-id="78584-109">Two IIS servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="78584-110">데이터베이스 계층에 제품 데이터 및 주문을 저장하기 위한 AlwaysOn 가용성 그룹(두 SQL Server 및 주 노드 감시) 이 있는 두 개의 Microsoft SQL Server 인스턴스</span><span class="sxs-lookup"><span data-stu-id="78584-110">Two Microsoft SQL Server instances with AlwaysOn availability groups (two SQL Servers and a majority node witness) for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="78584-111">인증 계층에 있는 고객 계정 및 공급자에 대한 두 Active Directory 도메인 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="78584-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="78584-112">모든 서버는 다음 두 서브넷에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78584-112">All the servers are located in two subnets:</span></span>
  * <span data-ttu-id="78584-113">웹 서버에 대한 프런트 엔드 서브넷</span><span class="sxs-lookup"><span data-stu-id="78584-113">a front-end subnet for the web servers</span></span> 
  * <span data-ttu-id="78584-114">응용 프로그램 서버, SQL 클러스터 및 도메인 컨트롤러에 대한 백 엔드 서브넷</span><span class="sxs-lookup"><span data-stu-id="78584-114">a back-end subnet for the application servers, SQL cluster, and domain controllers</span></span>

![응용 프로그램 인프라의 여러 다른 계층 다이어그램](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="78584-116">고객이 온라인 스토어를 검색할 때 들어오는 보안 웹 트래픽의 부하는 웹 서버 사이에서 분산되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-116">Incoming secure web traffic must be load-balanced among the web servers as customers browse the on-line store.</span></span> <span data-ttu-id="78584-117">웹 서버에서 HTTP 요청 양식의 주문 처리 트래픽의 부하는 응용 프로그램 서버 사이에서 부하 분산되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-117">Order processing traffic in the form of HTTP requests from the web servers must be balanced among the application servers.</span></span> <span data-ttu-id="78584-118">또한 인프라는 고가용성을 위해 설계되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-118">Additionally, the infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="78584-119">결과로 나온 디자인 다음을 통합해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-119">The resulting design must incorporate:</span></span>

* <span data-ttu-id="78584-120">Azure 구독 및 계정</span><span class="sxs-lookup"><span data-stu-id="78584-120">An Azure subscription and account</span></span>
* <span data-ttu-id="78584-121">단일 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="78584-121">A single resource group</span></span>
* <span data-ttu-id="78584-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="78584-122">Azure Managed Disks</span></span>
* <span data-ttu-id="78584-123">두 서브넷을 사용하는 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="78584-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="78584-124">역할이 비슷한 VM에 대한 가용성 집합</span><span class="sxs-lookup"><span data-stu-id="78584-124">Availability sets for the VMs with a similar role</span></span>
* <span data-ttu-id="78584-125">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="78584-125">Virtual machines</span></span>

<span data-ttu-id="78584-126">위의 모든 사항은 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="78584-126">All the above follow these naming conventions:</span></span>

* <span data-ttu-id="78584-127">Adventure Works Cycles는 **[IT 작업]-[위치]-[Azure 리소스]** 를 접두사로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="78584-128">이 예제에서 "**azos**"(Azure 온라인 저장소)는 IT 워크로드 이름이고 "**use**"(미국 동부 2)는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="78584-128">For this example, "**azos**" (Azure On-line Store) is the IT workload name and "**use**" (East US 2) is the location</span></span>
* <span data-ttu-id="78584-129">가상 네트워크는 AZOS-USE-VN**[숫자]**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="78584-130">가용성 집합은 azos-use-as-**[역할]**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="78584-131">가상 컴퓨터 이름은 azos-use-vm-**[VM 이름]**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="78584-132">Azure 구독 및 계정</span><span class="sxs-lookup"><span data-stu-id="78584-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="78584-133">Adventure Works Cycles는 이 IT 작업에 대한 청구를 제공하기 위해 Adventure Works Enterprise Subscription이라는 엔터프라이즈 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, to provide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="78584-134">저장소</span><span class="sxs-lookup"><span data-stu-id="78584-134">Storage</span></span>
<span data-ttu-id="78584-135">Adventure Works Cycles에서는 Azure Managed Disks를 사용해야 한다고 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="78584-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="78584-136">VM을 만들 때 사용 가능한 두 저장소 계층이 모두 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="78584-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="78584-137">**Standard Storage** - 웹 서버, 응용 프로그램 서버 및 도메인 컨트롤러와 해당 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="78584-137">**Standard storage** for the web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="78584-138">**Premium Storage** - SQL Server VM과 해당 데이터 디스크</span><span class="sxs-lookup"><span data-stu-id="78584-138">**Premium storage** for the SQL Server VMs and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="78584-139">가상 네트워크 및 서브넷</span><span class="sxs-lookup"><span data-stu-id="78584-139">Virtual network and subnets</span></span>
<span data-ttu-id="78584-140">가상 네트워크는 Adventure Work Cycles 온-프레미스 네트워크에 지속적인 연결이 필요하지 않기 때문에 클라우드 전용 가상 네트워크로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="78584-140">Because the virtual network does not need ongoing connectivity to the Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="78584-141">Azure 포털을 사용하여 다음 설정을 포함한 클라우드 전용 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78584-141">They created a cloud-only virtual network with the following settings using the Azure portal:</span></span>

* <span data-ttu-id="78584-142">이름: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="78584-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="78584-143">위치: East US 2</span><span class="sxs-lookup"><span data-stu-id="78584-143">Location: East US 2</span></span>
* <span data-ttu-id="78584-144">가상 네트워크 주소 공간: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="78584-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="78584-145">첫 번째 서브넷:</span><span class="sxs-lookup"><span data-stu-id="78584-145">First subnet:</span></span>
  * <span data-ttu-id="78584-146">이름: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="78584-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="78584-147">주소 공간: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="78584-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="78584-148">두 번째 서브넷:</span><span class="sxs-lookup"><span data-stu-id="78584-148">Second subnet:</span></span>
  * <span data-ttu-id="78584-149">이름: BackEnd</span><span class="sxs-lookup"><span data-stu-id="78584-149">Name: BackEnd</span></span>
  * <span data-ttu-id="78584-150">주소 공간: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="78584-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="78584-151">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="78584-151">Availability sets</span></span>
<span data-ttu-id="78584-152">온라인 스토어의 모든 네 개 계층의 고가용성을 유지하기 위해 Adventure Works Cycles는 다음과 같은 네 개의 가용성 집합으로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="78584-152">To maintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="78584-153">**azos-use-as-web** </span><span class="sxs-lookup"><span data-stu-id="78584-153">**azos-use-as-web** for the web servers</span></span>
* <span data-ttu-id="78584-154">**azos-use-as-app** </span><span class="sxs-lookup"><span data-stu-id="78584-154">**azos-use-as-app** for the application servers</span></span>
* <span data-ttu-id="78584-155">**azos-use-as-sql** </span><span class="sxs-lookup"><span data-stu-id="78584-155">**azos-use-as-sql** for the SQL Servers</span></span>
* <span data-ttu-id="78584-156">**azos-use-as-dc** </span><span class="sxs-lookup"><span data-stu-id="78584-156">**azos-use-as-dc** for the domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="78584-157">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="78584-157">Virtual machines</span></span>
<span data-ttu-id="78584-158">Adventure Works Cycles는 Azure VM에 대해 다음 이름을 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="78584-158">Adventure Works Cycles decided on the following names for their Azure VMs:</span></span>

* <span data-ttu-id="78584-159">**azos-use-vm-web01** </span><span class="sxs-lookup"><span data-stu-id="78584-159">**azos-use-vm-web01** for the first web server</span></span>
* <span data-ttu-id="78584-160">**azos-use-vm-web02** </span><span class="sxs-lookup"><span data-stu-id="78584-160">**azos-use-vm-web02** for the second web server</span></span>
* <span data-ttu-id="78584-161">**azos-use-vm-app01** </span><span class="sxs-lookup"><span data-stu-id="78584-161">**azos-use-vm-app01** for the first application server</span></span>
* <span data-ttu-id="78584-162">**azos-use-vm-app02** </span><span class="sxs-lookup"><span data-stu-id="78584-162">**azos-use-vm-app02** for the second application server</span></span>
* <span data-ttu-id="78584-163">**azfae-use-vm-sql01** </span><span class="sxs-lookup"><span data-stu-id="78584-163">**azos-use-vm-sql01** for the first SQL Server server in the cluster</span></span>
* <span data-ttu-id="78584-164">**azfae-use-vm-sql02** </span><span class="sxs-lookup"><span data-stu-id="78584-164">**azos-use-vm-sql02** for the second SQL Server server in the cluster</span></span>
* <span data-ttu-id="78584-165">**azos-use-vm-dc01** </span><span class="sxs-lookup"><span data-stu-id="78584-165">**azos-use-vm-dc01** for the first domain controller</span></span>
* <span data-ttu-id="78584-166">**azos-use-vm-dc02** </span><span class="sxs-lookup"><span data-stu-id="78584-166">**azos-use-vm-dc02** for the second domain controller</span></span>

<span data-ttu-id="78584-167">다음은 결과 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="78584-167">Here is the resulting configuration.</span></span>

![Azure에 배포되는 최종 응용 프로그램 인프라](./media/infrastructure-example/example-config.png)

<span data-ttu-id="78584-169">이 구성은 다음을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="78584-169">This configuration incorporates:</span></span>

* <span data-ttu-id="78584-170">두 서브넷을 사용하는 클라우드 전용 가상 네트워크(프런트 엔드 및 백 엔드)</span><span class="sxs-lookup"><span data-stu-id="78584-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="78584-171">Standard 디스크와 Premium 디스크가 둘 다 있는 Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="78584-171">Azure Managed Disks with both Standard and Premium disks</span></span>
* <span data-ttu-id="78584-172">네 개의 가용성 집합, 온라인 스토어의 각 계층마다 한 개</span><span class="sxs-lookup"><span data-stu-id="78584-172">Four availability sets, one for each tier of the on-line store</span></span>
* <span data-ttu-id="78584-173">네 계층에 대한 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="78584-173">The virtual machines for the four tiers</span></span>
* <span data-ttu-id="78584-174">인터넷에서 웹 서버 간 HTTPS 기반 웹 트래픽에 대한 외부 부하 분산 집합</span><span class="sxs-lookup"><span data-stu-id="78584-174">An external load balanced set for HTTPS-based web traffic from the Internet to the web servers</span></span>
* <span data-ttu-id="78584-175">웹 서버에서 응용 프로그램 서버 간 암호화되지 않은 웹 트래픽에 대한 내부 부하 분산 집합</span><span class="sxs-lookup"><span data-stu-id="78584-175">An internal load balanced set for unencrypted web traffic from the web servers to the application servers</span></span>
* <span data-ttu-id="78584-176">단일 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="78584-176">A single resource group</span></span>