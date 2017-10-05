---
title: "Azure Network Watcher에서 보안 그룹 보기 소개 | Microsoft Docs"
description: "이 페이지는 Network Watcher 보안 보기 기능에 대한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 2c581a2d152a6d3f16de8f249e27a426aa9f844f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="fba03-103">Azure Network Watcher에서 네트워크 보안 그룹 보기 소개</span><span class="sxs-lookup"><span data-stu-id="fba03-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="fba03-104">네트워크 보안 그룹은 서브넷 수준 또는 NIC 수준에서 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="fba03-105">서브넷 수준에서 연결되는 경우 서브넷의 모든 VM 인스턴스에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="fba03-106">네트워크 보안 그룹 보기는 가상 컴퓨터에 대한 NIC 및 서브넷 수준에서 연결된 모든 구성된 NSG 및 규칙을 반환하여 구성을 이해하기 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span></span> <span data-ttu-id="fba03-107">또한 VM의 각 NIC에 대해 유효 보안 규칙이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="fba03-108">네트워크 보안 그룹 보기를 사용하여 열린 포트와 같은 네트워크 취약점에 대해 VM을 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="fba03-109">또한 네트워크 보안 그룹이 [구성된 보안 규칙 및 유효 보안 규칙 간의 비교](network-watcher-nsg-auditing-powershell.md)에 따라 예상대로 작동하는지 검증할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="fba03-110">더 확장된 사용 사례는 보안 규정 준수 및 감사에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="fba03-111">조직의 보안 관리를 위해 규범적인 보안 규칙의 집합을 모델로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="fba03-112">정기적 규정 준수 감사는 네트워크의 각 VM에 대해 규범적인 규칙을 유효 규칙과 비교하여 프로그래밍 방식으로 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="fba03-113">포털에서 규칙은 유효, 서브넷, 네트워크 인터페이스 및 기본으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="fba03-114">가상 컴퓨터에 적용되는 규칙에 대한 간단한 보기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="fba03-115">CSV 파일에 있는 탭에 관계 없이 모든 보안 규칙을 쉽게 다운로드하는 다운로드 단추가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![보안 그룹 보기][1]

<span data-ttu-id="fba03-117">규칙을 선택할 수 있으며 네트워크 보안 그룹 및 원본 및 대상 접두사를 표시하는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="fba03-118">이 블레이드에서 네트워크 보안 그룹 리소스로 직접 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fba03-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![드릴다운][2]

### <a name="next-steps"></a><span data-ttu-id="fba03-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fba03-120">Next steps</span></span>

<span data-ttu-id="fba03-121">[PowerShell을 사용하여 네트워크 보안 그룹 설정 감사](network-watcher-nsg-auditing-powershell.md)를 방문하여 네트워크 보안 그룹 설정을 감사하는 방법에 대해 알아보기</span><span class="sxs-lookup"><span data-stu-id="fba03-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









