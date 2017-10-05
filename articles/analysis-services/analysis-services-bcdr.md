---
title: "Azure Analysis Services 고가용성 | Microsoft 문서"
description: "Azure Analysis Services 고가용성 보장."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 84b4c59bac1feeb8611b3a8d783d093ba073e532
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="70f6d-103">Analysis Services 고가용성</span><span class="sxs-lookup"><span data-stu-id="70f6d-103">Analysis Services high availability</span></span>
<span data-ttu-id="70f6d-104">이 문서에서는 Azure Analysis Services 서버에 대한 고가용성을 보장하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="70f6d-105">서비스가 중단된 동안 고가용성 보장</span><span class="sxs-lookup"><span data-stu-id="70f6d-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="70f6d-106">드문 경우지만 Azure 데이터 센터에서 가동 중단이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="70f6d-107">가동 중단이 발생하면 몇 분 내지 몇 시간 동안 지속될 수 있는 업무 중단이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="70f6d-108">고가용성은 대부분 서버 중복을 통해 획득됩니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="70f6d-109">Azure Analysis Services를 통해 하나 이상의 지역에서 추가적인 보조 서버를 만들어 중복을 획득할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="70f6d-110">중복 서버를 만들 경우 해당 서버의 데이터 및 메타데이터가 오프라인으로 전환된 지역의 서버와 동기화되도록 하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-110">When creating redundant servers, to assure the data and metadata on those servers is in-sync with the server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="70f6d-111">다른 지역의 중복 서버에 모델을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-111">Deploy models to redundant servers in other regions.</span></span> <span data-ttu-id="70f6d-112">이 방법을 적용할 경우 모든 서버가 동기화되도록 기본 서버와 중복 서버에서 모두 병렬로 데이터를 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="70f6d-113">기본 서버에서 데이터베이스를 백업하고 중복 서버에 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="70f6d-114">예를 들어 야간에 Azure Storage에 백업하는 작업을 자동화하고 다른 지역의 다른 중복 서버로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-114">For example, you can automate nightly backups to Azure storage, and restore to other redundant servers in other regions.</span></span> 

<span data-ttu-id="70f6d-115">어느 경우에나 기본 서버에서 작동 중단이 발생하면 다른 지역 데이터 센터의 서버에 연결하기 위해 보고 클라이언트에서 연결 문자열을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-115">In either case, if your primary server experiences an outage, you must change the connection strings in reporting clients to connect to the server in a different regional datacenter.</span></span> <span data-ttu-id="70f6d-116">이 변경은 마지막 수단으로, 치명적인 지역 데이터 센터 작동 중단이 발생한 경우에만 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="70f6d-117">모든 클라이언트에서 연결을 업데이트하기 전에 기본 서버를 호스트하는 데이터 센터 작동 중단 상태에서 다시 온라인 상태로 전환될 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="70f6d-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="70f6d-118">관련 정보</span><span class="sxs-lookup"><span data-stu-id="70f6d-118">Related information</span></span>
<span data-ttu-id="70f6d-119">[백업 및 복원](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="70f6d-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="70f6d-120">Azure Analysis Services 관리</span><span class="sxs-lookup"><span data-stu-id="70f6d-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

