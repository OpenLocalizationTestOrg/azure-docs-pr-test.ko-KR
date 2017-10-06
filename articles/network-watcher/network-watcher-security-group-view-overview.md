---
title: "Azure 네트워크 감시자에서 aaaIntroduction toosecurity 그룹 보기 | Microsoft Docs"
description: "이 페이지 hello 네트워크 감시자 보안 보기 기능에 대 한 개요를 제공합니다."
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
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="ef13f-103">Azure 네트워크 감시자 소개 toonetwork 보안 그룹 보기</span><span class="sxs-lookup"><span data-stu-id="ef13f-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="ef13f-104">네트워크 보안 그룹은 서브넷 수준 또는 NIC 수준에서 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="ef13f-105">서브넷 수준에서 연결 된, tooall hello VM 인스턴스 hello 서브넷에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="ef13f-106">네트워크 보안 그룹 뷰는 모든 hello 구성에 대 한 정보를 제공 하는 가상 컴퓨터에 대 한 서브넷과 NIC 수준에서 연결 된 규칙 및 구성 하는 hello Nsg를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="ef13f-107">또한 hello 효과적인 보안 규칙은 VM에서 nic hello 각각에 대해 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="ef13f-108">네트워크 보안 그룹 보기를 사용하여 열린 포트와 같은 네트워크 취약점에 대해 VM을 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="ef13f-109">네트워크 보안 그룹에 따라 예상 대로 작동 하는 경우에 확인할 수 있습니다는 [hello 간의 비교는 구성 하 고 효과적인 보안 규칙 hello](network-watcher-nsg-auditing-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="ef13f-110">더 확장된 사용 사례는 보안 규정 준수 및 감사에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="ef13f-111">조직의 보안 관리를 위해 규범적인 보안 규칙의 집합을 모델로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="ef13f-112">주기적인 준수 감사 hello Vm 네트워크에 각각에 대해 hello 규범적인 규칙을 hello 효과적인 규칙과 비교 하 여 프로그래밍 방식으로 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="ef13f-113">Hello에 포털 규칙 적용, 서브넷, 네트워크 인터페이스 및 기본으로 나뉩니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="ef13f-114">Hello 규칙이 적용 되는 tooa 가상 컴퓨터에 대 한 간단한 뷰를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="ef13f-115">다운로드 단추 tooeasily CSV 파일로 hello 탭에 관계 없이 모든 hello 보안 규칙을 다운로드 하는 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![보안 그룹 보기][1]

<span data-ttu-id="ef13f-117">규칙 선택 하 고 tooshow hello 네트워크 보안 그룹 및 원본 및 대상 접두사는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="ef13f-118">이 블레이드 이동할 수 직접 toohello 네트워크 보안 그룹 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ef13f-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![드릴다운][2]

### <a name="next-steps"></a><span data-ttu-id="ef13f-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef13f-120">Next steps</span></span>

<span data-ttu-id="ef13f-121">어떻게 tooaudit 네트워크 보안 그룹에 대해 알아봅니다 방문 하 여 설정을 [PowerShell 사용 하 여 감사 네트워크 보안 그룹 설정](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="ef13f-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









