---
title: "Azure 인프라 연습 aaaExample | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Azure에서 예제 인프라를 배포 하기 위한 방법을 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 281fc2c0-b533-45fa-81a3-728c0049c73d
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6b307c0112203aa83e1fada81966fc265397a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="example-azure-infrastructure-walkthrough-for-linux-vms"></a><span data-ttu-id="64c33-103">Linux VM에 대한 Azure 인프라 연습 예제</span><span class="sxs-lookup"><span data-stu-id="64c33-103">Example Azure infrastructure walkthrough for Linux VMs</span></span>

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="64c33-104">이 문서에서는 예제 응용 프로그램 인프라를 구축하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-104">This article walks through building out an example application infrastructure.</span></span> <span data-ttu-id="64c33-105">모든 hello 지침과 명명 규칙, 가용성 집합, 가상 네트워크 및 부하 분산 장치에 의사 결정을 함께 제공 하는 간단한 온라인 상점에 대 한 인프라를 디자인 하 고 가상 컴퓨터 (Vm)를 배포 실제로 우리 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-105">We detail designing an infrastructure for a simple on-line store that brings together all hello guidelines and decisions around naming conventions, availability sets, virtual networks and load balancers, and actually deploying your virtual machines (VMs).</span></span>

## <a name="example-workload"></a><span data-ttu-id="64c33-106">워크로드 예제</span><span class="sxs-lookup"><span data-stu-id="64c33-106">Example workload</span></span>
<span data-ttu-id="64c33-107">Adventure Works Cycles가 toobuild 구성 된 Azure에서 온라인 스토어 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="64c33-107">Adventure Works Cycles wants toobuild an on-line store application in Azure that consists of:</span></span>

* <span data-ttu-id="64c33-108">웹 계층의 프런트 엔드 hello 클라이언트를 실행 하는 두 개의 nginx 서버</span><span class="sxs-lookup"><span data-stu-id="64c33-108">Two nginx servers running hello client front-end in a web tier</span></span>
* <span data-ttu-id="64c33-109">응용 프로그램 계층에 있으며 데이터 및 주문을 처리하는 두 nginx 서버</span><span class="sxs-lookup"><span data-stu-id="64c33-109">Two nginx servers processing data and orders in an application tier</span></span>
* <span data-ttu-id="64c33-110">데이터베이스 계층에 있으며 제품 데이터 및 주문을 저장하기 위한 분할 클러스터의 두 MongoDB 서버 부분</span><span class="sxs-lookup"><span data-stu-id="64c33-110">Two MongoDB servers part of a sharded cluster for storing product data and orders in a database tier</span></span>
* <span data-ttu-id="64c33-111">인증 계층에 있는 고객 계정 및 공급자에 대한 두 Active Directory 도메인 컨트롤러</span><span class="sxs-lookup"><span data-stu-id="64c33-111">Two Active Directory domain controllers for customer accounts and suppliers in an authentication tier</span></span>
* <span data-ttu-id="64c33-112">서브넷인에 속하는 모든 hello 서버:</span><span class="sxs-lookup"><span data-stu-id="64c33-112">All hello servers are located in two subnets:</span></span>
  * <span data-ttu-id="64c33-113">웹 서버 hello에 대 한 프런트 엔드 서브넷</span><span class="sxs-lookup"><span data-stu-id="64c33-113">a front-end subnet for hello web servers</span></span> 
  * <span data-ttu-id="64c33-114">hello 응용 프로그램 서버, MongoDB 클러스터 및 도메인 컨트롤러에 대 한 백 엔드 서브넷</span><span class="sxs-lookup"><span data-stu-id="64c33-114">a back-end subnet for hello application servers, MongoDB cluster, and domain controllers</span></span>

![응용 프로그램 인프라의 여러 다른 계층 다이어그램](./media/infrastructure-example/example-tiers.png)

<span data-ttu-id="64c33-116">보안 들어오는 웹 트래픽의 같아야 hello 웹 서버 간에 부하 분산 된 고객 hello 온라인 스토어를 검색할 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-116">Incoming secure web traffic must be load-balanced among hello web servers as customers browse hello on-line store.</span></span> <span data-ttu-id="64c33-117">주문 hello 형식의 HTTP 트래픽을 처리 hello 웹 서버 해야 수에 부하 분산 hello 응용 프로그램 서버에서에서 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-117">Order processing traffic in hello form of HTTP requests from hello web servers must be load-balanced among hello application servers.</span></span> <span data-ttu-id="64c33-118">또한 고가용성을 위해 hello 인프라를 설계 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-118">Additionally, hello infrastructure must be designed for high availability.</span></span>

<span data-ttu-id="64c33-119">hello 결과 디자인에 통합 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-119">hello resulting design must incorporate:</span></span>

* <span data-ttu-id="64c33-120">Azure 구독 및 계정</span><span class="sxs-lookup"><span data-stu-id="64c33-120">An Azure subscription and account</span></span>
* <span data-ttu-id="64c33-121">단일 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="64c33-121">A single resource group</span></span>
* <span data-ttu-id="64c33-122">Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="64c33-122">Azure Managed Disks</span></span>
* <span data-ttu-id="64c33-123">두 서브넷을 사용하는 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="64c33-123">A virtual network with two subnets</span></span>
* <span data-ttu-id="64c33-124">비슷한 역할을 가진 Vm hello에 대 한 가용성 집합</span><span class="sxs-lookup"><span data-stu-id="64c33-124">Availability sets for hello VMs with a similar role</span></span>
* <span data-ttu-id="64c33-125">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="64c33-125">Virtual machines</span></span>

<span data-ttu-id="64c33-126">위의 모든 hello 명명 규칙에 부합 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-126">All hello above follow these naming conventions:</span></span>

* <span data-ttu-id="64c33-127">Adventure Works Cycles는 **[IT 작업]-[위치]-[Azure 리소스]** 를 접두사로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-127">Adventure Works Cycles uses **[IT workload]-[location]-[Azure resource]** as a prefix</span></span>
  * <span data-ttu-id="64c33-128">예를 들어 "**azos**" (Azure 온라인 저장소)는 IT 워크 로드 이름을 hello 및 "**사용**"는 hello 위치 (미국 동부 2)</span><span class="sxs-lookup"><span data-stu-id="64c33-128">For this example, "**azos**" (Azure On-line Store) is hello IT workload name and "**use**" (East US 2) is hello location</span></span>
* <span data-ttu-id="64c33-129">가상 네트워크는 AZOS-USE-VN**[숫자]**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-129">Virtual networks use AZOS-USE-VN**[number]**</span></span>
* <span data-ttu-id="64c33-130">가용성 집합은 azos-use-as-**[역할]**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-130">Availability sets use azos-use-as-**[role]**</span></span>
* <span data-ttu-id="64c33-131">가상 컴퓨터 이름은 azos-use-vm-**[VM 이름]**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-131">Virtual machine names use azos-use-vm-**[vmname]**</span></span>

## <a name="azure-subscriptions-and-accounts"></a><span data-ttu-id="64c33-132">Azure 구독 및 계정</span><span class="sxs-lookup"><span data-stu-id="64c33-132">Azure subscriptions and accounts</span></span>
<span data-ttu-id="64c33-133">Adventure Works Cycles는 Adventure Works 엔터프라이즈 구독을이 IT 워크 로드에 대 한 청구 tooprovide 라는 자신의 엔터프라이즈 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-133">Adventure Works Cycles is using their Enterprise subscription, named Adventure Works Enterprise Subscription, tooprovide billing for this IT workload.</span></span>

## <a name="storage"></a><span data-ttu-id="64c33-134">저장소</span><span class="sxs-lookup"><span data-stu-id="64c33-134">Storage</span></span>
<span data-ttu-id="64c33-135">Adventure Works Cycles에서는 Azure Managed Disks를 사용해야 한다고 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-135">Adventure Works Cycles determined that they should use Azure Managed Disks.</span></span> <span data-ttu-id="64c33-136">VM을 만들 때 사용 가능한 두 저장소 계층이 모두 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-136">When creating VMs, both storage available storage tiers are used:</span></span>

* <span data-ttu-id="64c33-137">**표준 저장소** hello 웹 서버, 응용 프로그램 서버 및 도메인 컨트롤러 및 해당 데이터 디스크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-137">**Standard storage** for hello web servers, application servers, and domain controllers and their data disks.</span></span>
* <span data-ttu-id="64c33-138">**프리미엄 저장소** hello MongoDB 분할 클러스터 서버 및 데이터 디스크에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-138">**Premium storage** for hello MongoDB sharded cluster servers and their data disks.</span></span>

## <a name="virtual-network-and-subnets"></a><span data-ttu-id="64c33-139">가상 네트워크 및 서브넷</span><span class="sxs-lookup"><span data-stu-id="64c33-139">Virtual network and subnets</span></span>
<span data-ttu-id="64c33-140">Hello 가상 네트워크는 진행 중인 연결 toohello Adventure 작업 Cycles 온-프레미스 네트워크를 필요 하지 않습니다, 클라우드 전용 가상 네트워크에서 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-140">Because hello virtual network does not need ongoing connectivity toohello Adventure Work Cycles on-premises network, they decided on a cloud-only virtual network.</span></span>

<span data-ttu-id="64c33-141">자신이 만든 다음 hello Azure 포털을 사용 하 여 설정을 hello로 클라우드 전용 가상 네트워크:</span><span class="sxs-lookup"><span data-stu-id="64c33-141">They created a cloud-only virtual network with hello following settings using hello Azure portal:</span></span>

* <span data-ttu-id="64c33-142">이름: AZOS-USE-VN01</span><span class="sxs-lookup"><span data-stu-id="64c33-142">Name: AZOS-USE-VN01</span></span>
* <span data-ttu-id="64c33-143">위치: East US 2</span><span class="sxs-lookup"><span data-stu-id="64c33-143">Location: East US 2</span></span>
* <span data-ttu-id="64c33-144">가상 네트워크 주소 공간: 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="64c33-144">Virtual network address space: 10.0.0.0/8</span></span>
* <span data-ttu-id="64c33-145">첫 번째 서브넷:</span><span class="sxs-lookup"><span data-stu-id="64c33-145">First subnet:</span></span>
  * <span data-ttu-id="64c33-146">이름: FrontEnd</span><span class="sxs-lookup"><span data-stu-id="64c33-146">Name: FrontEnd</span></span>
  * <span data-ttu-id="64c33-147">주소 공간: 10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="64c33-147">Address space: 10.0.1.0/24</span></span>
* <span data-ttu-id="64c33-148">두 번째 서브넷:</span><span class="sxs-lookup"><span data-stu-id="64c33-148">Second subnet:</span></span>
  * <span data-ttu-id="64c33-149">이름: BackEnd</span><span class="sxs-lookup"><span data-stu-id="64c33-149">Name: BackEnd</span></span>
  * <span data-ttu-id="64c33-150">주소 공간: 10.0.2.0/24</span><span class="sxs-lookup"><span data-stu-id="64c33-150">Address space: 10.0.2.0/24</span></span>

## <a name="availability-sets"></a><span data-ttu-id="64c33-151">가용성 집합</span><span class="sxs-lookup"><span data-stu-id="64c33-151">Availability sets</span></span>
<span data-ttu-id="64c33-152">온라인 상점별 4 개 가용성 집합을 결정된 Adventure Works Cycles의 모든 4 개 계층의 고가용성을 toomaintain:</span><span class="sxs-lookup"><span data-stu-id="64c33-152">toomaintain high availability of all four tiers of their on-line store, Adventure Works Cycles decided on four availability sets:</span></span>

* <span data-ttu-id="64c33-153">**웹으로 azos 사용** hello 웹 서버에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-153">**azos-use-as-web** for hello web servers</span></span>
* <span data-ttu-id="64c33-154">**앱으로 azos 사용** hello 응용 프로그램 서버에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-154">**azos-use-as-app** for hello application servers</span></span>
* <span data-ttu-id="64c33-155">**db로 azos 사용** hello 서버 hello MongoDB 분할 클러스터에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-155">**azos-use-as-db** for hello servers in hello MongoDB sharded cluster</span></span>
* <span data-ttu-id="64c33-156">**dc로 azos 사용** hello 도메인 컨트롤러에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-156">**azos-use-as-dc** for hello domain controllers</span></span>

## <a name="virtual-machines"></a><span data-ttu-id="64c33-157">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="64c33-157">Virtual machines</span></span>
<span data-ttu-id="64c33-158">Adventure Works Cycles의 Azure Vm에 대 한 이름 다음 hello 결정:</span><span class="sxs-lookup"><span data-stu-id="64c33-158">Adventure Works Cycles decided on hello following names for their Azure VMs:</span></span>

* <span data-ttu-id="64c33-159">**사용 하 여 vm web01 azos** hello 첫 번째 웹 서버에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-159">**azos-use-vm-web01** for hello first web server</span></span>
* <span data-ttu-id="64c33-160">**사용 하 여 vm web02 azos** hello 두 번째 웹 서버에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-160">**azos-use-vm-web02** for hello second web server</span></span>
* <span data-ttu-id="64c33-161">**사용 하 여 vm app01 azos** hello 첫 번째 응용 프로그램 서버에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-161">**azos-use-vm-app01** for hello first application server</span></span>
* <span data-ttu-id="64c33-162">**사용 하 여 vm app02 azos** hello 두 번째 응용 프로그램 서버에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-162">**azos-use-vm-app02** for hello second application server</span></span>
* <span data-ttu-id="64c33-163">**azos-사용-vm-d b를 01** hello 클러스터의 첫 번째 MongoDB 서버 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-163">**azos-use-vm-db01** for hello first MongoDB server in hello cluster</span></span>
* <span data-ttu-id="64c33-164">**사용 하 여 vm db02 azos** hello 클러스터의 두 번째 MongoDB 서버 hello에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-164">**azos-use-vm-db02** for hello second MongoDB server in hello cluster</span></span>
* <span data-ttu-id="64c33-165">**사용 하 여 vm dc01 azos** hello 첫 번째 도메인 컨트롤러에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-165">**azos-use-vm-dc01** for hello first domain controller</span></span>
* <span data-ttu-id="64c33-166">**azos 02로 사용 하 여-vm-복제** hello 두 번째 도메인 컨트롤러에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-166">**azos-use-vm-dc02** for hello second domain controller</span></span>

<span data-ttu-id="64c33-167">다음은 hello 결과 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-167">Here is hello resulting configuration.</span></span>

![Azure에 배포되는 최종 응용 프로그램 인프라](./media/infrastructure-example/example-config.png)

<span data-ttu-id="64c33-169">이 구성은 다음을 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="64c33-169">This configuration incorporates:</span></span>

* <span data-ttu-id="64c33-170">두 서브넷을 사용하는 클라우드 전용 가상 네트워크(프런트 엔드 및 백 엔드)</span><span class="sxs-lookup"><span data-stu-id="64c33-170">A cloud-only virtual network with two subnets (FrontEnd and BackEnd)</span></span>
* <span data-ttu-id="64c33-171">표준 디스크와 프리미엄 디스크를 모두 사용하는 Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="64c33-171">Azure Managed Disks using both Standard and Premium disks</span></span>
* <span data-ttu-id="64c33-172">Hello 온라인 상점의 각 계층에 대해 하나씩 네 개의 가용성 집합</span><span class="sxs-lookup"><span data-stu-id="64c33-172">Four availability sets, one for each tier of hello on-line store</span></span>
* <span data-ttu-id="64c33-173">hello 4 계층에 대 한 hello 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="64c33-173">hello virtual machines for hello four tiers</span></span>
* <span data-ttu-id="64c33-174">Hello 인터넷 toohello 웹 서버에서 웹 HTTPS 기반 트래픽에 대 한 외부 부하 분산 된 집합</span><span class="sxs-lookup"><span data-stu-id="64c33-174">An external load balanced set for HTTPS-based web traffic from hello Internet toohello web servers</span></span>
* <span data-ttu-id="64c33-175">내부 부하 분산 집합 hello 웹 서버 toohello 응용 프로그램 서버에서 암호화 되지 않은 웹 트래픽에 대 한</span><span class="sxs-lookup"><span data-stu-id="64c33-175">An internal load balanced set for unencrypted web traffic from hello web servers toohello application servers</span></span>
* <span data-ttu-id="64c33-176">단일 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="64c33-176">A single resource group</span></span>
