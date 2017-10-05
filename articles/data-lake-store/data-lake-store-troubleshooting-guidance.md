---
title: "Azure Data Lake Store에 대한 질문과 대답 | Microsoft Docs"
description: "Azure Data Lake Store와 관련된 문제를 해결 또는 완화에 대한 지침"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 44aaec9dc145b47b809a3ad4bc244eb9dfead24c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a><span data-ttu-id="c8d04-103">Azure Data Lake Store에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="c8d04-103">Frequently asked questions for Azure Data Lake Store</span></span>
<span data-ttu-id="c8d04-104">이 문서에서는 Azure Data Lake Store와 관련된 FAQ에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-104">In this article you will learn about FAQs related to Azure Data Lake Store.</span></span>

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a><span data-ttu-id="c8d04-105">어떻게 영역 전체의 재해 또는 실수로 인한 삭제로부터 내 데이터를 추가로 보호할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="c8d04-105">How can I further protect my data from region-wide disasters or accidental deletions?</span></span>
<span data-ttu-id="c8d04-106">Azure Data Lake Store 계정의 데이터는 자동화된 복제본을 통해 지역 내에서 일시적인 하드웨어 장애에 대한 복원력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-106">The data in your Azure Data Lake Store account is resilient to transient hardware failures within a region through automated replicas.</span></span> <span data-ttu-id="c8d04-107">이렇게 하면 Azure Data Lake Store SLA를 충족하는 내구성 및 고가용성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-107">This ensures durability and high availability, meeting the Azure Data Lake Store SLA.</span></span> <span data-ttu-id="c8d04-108">드물게 발생하는 전체 지역 가동 중단 또는 삭제 실수로부터 데이터를 보호하는 방법에 대한 몇 가지 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-108">Here's some guidance on how to further protect your data from rare region-wide outages or accidental deletions.</span></span>

### <a name="disaster-recovery-guidance"></a><span data-ttu-id="c8d04-109">재해 복구 지침</span><span class="sxs-lookup"><span data-stu-id="c8d04-109">Disaster recovery guidance</span></span>
<span data-ttu-id="c8d04-110">모든 고객은 자체적으로 재해 복구 계획을 준비하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-110">It is critical for every customer to prepare their own disaster recovery plan.</span></span> <span data-ttu-id="c8d04-111">재해 복구 계획을 빌드하려면 아래 Azure 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8d04-111">Please refer to the Azure documentation below to build your disaster recovery plan.</span></span> <span data-ttu-id="c8d04-112">여기에는 고유한 계획을 직접 만들 수 있는 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-112">Here are some resources that can help you create your own plan.</span></span>

* [<span data-ttu-id="c8d04-113">Azure 응용 프로그램에 대한 재해 복구 및 고가용성</span><span class="sxs-lookup"><span data-stu-id="c8d04-113">Disaster recovery and high availability for Azure applications</span></span>](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [<span data-ttu-id="c8d04-114">Azure 복구력 기술 지침</span><span class="sxs-lookup"><span data-stu-id="c8d04-114">Azure resiliency technical guidance</span></span>](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a><span data-ttu-id="c8d04-115">모범 사례</span><span class="sxs-lookup"><span data-stu-id="c8d04-115">Best practices</span></span>
<span data-ttu-id="c8d04-116">재해 복구 계획의 요구에 맞게 정렬된 주파수를 사용하여 다른 지역의 다른 Data Lake Store 계정에 중요한 데이터를 복사하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-116">We recommend that you copy your critical data to another Data Lake Store account in another region with a frequency aligned to the needs of your disaster recovery plan.</span></span> <span data-ttu-id="c8d04-117">[ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) 또는 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)를 포함하여 데이터를 복사하는 다양한 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-117">There are a variety of methods to copy data including [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) or [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span> <span data-ttu-id="c8d04-118">Azure Data Factory는 반복적으로 데이터 이동 파이프라인을 만들고 배포하기 위한 유용한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-118">Azure Data Factory is a useful service for creating and deploying data movement pipelines on a recurring basis.</span></span>

<span data-ttu-id="c8d04-119">지역 가동 중단이 발생하는 경우 데이터가 복사된 지역에 있는 데이터에 액세스할 수 있습니다. [Azure 서비스 상태 대시보드](https://azure.microsoft.com/status/)를 모니터링하여 전세계의 Azure 서비스 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-119">If a regional outage occurs, you can then access your data in the region where the data was copied.You can monitor the [Azure Service Health Dashboard](https://azure.microsoft.com/status/) to determine the Azure service status across the globe.</span></span>

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a><span data-ttu-id="c8d04-120">데이터 손상 또는 삭제 실수 복구 지침</span><span class="sxs-lookup"><span data-stu-id="c8d04-120">Data corruption or accidental deletion recovery guidance</span></span>
<span data-ttu-id="c8d04-121">Azure Data Lake Store가 자동화된 복제본을 통해 데이터 복원력을 제공하는 반면 이렇게 하더라도 응용 프로그램(또는 개발자/사용자)의 데이터를 손상시키거나 실수로 삭제하지 않도록 방지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-121">While Azure Data Lake Store provides data resiliency through automated replicas, this does not prevent your application (or developers/users) from corrupting data or accidentally deleting it.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="c8d04-122">모범 사례</span><span class="sxs-lookup"><span data-stu-id="c8d04-122">Best practices</span></span>
<span data-ttu-id="c8d04-123">삭제 실수를 방지하려면 Data Lake Store 계정에 대한 올바른 액세스 정책을 먼저 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-123">To prevent accidental deletion, we recommend that you first set the correct access policies for your Data Lake Store account.</span></span>  <span data-ttu-id="c8d04-124">여기에는 [Azure 리소스 잠금](../azure-resource-manager/resource-group-lock-resources.md)을 적용하여 중요한 리소스를 잠그는 것은 물론 사용 가능한 [Data Lake Store 보안 기능](data-lake-store-security-overview.md)을 사용하여 계정 및 파일 수준 액세스 제어를 적용하는 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-124">This includes applying [Azure resource locks](../azure-resource-manager/resource-group-lock-resources.md) to lock down important resources as well as applying account and file level access control using the available [Data Lake Store security features](data-lake-store-security-overview.md).</span></span> <span data-ttu-id="c8d04-125">다른 Data Lake Store 계정, 폴더 또는 Azure 구독에서 [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) 또는 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)를 사용하여 중요한 데이터의 복사본을 정기적으로 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-125">We also recommend that you routinely create copies of your critical data using [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) or [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) in another Data Lake Store account, folder, or Azure subscription.</span></span>  <span data-ttu-id="c8d04-126">데이터 손상 또는 삭제 인시던트로부터 복구하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-126">This can be used to recover from a data corruption or deletion incident.</span></span> <span data-ttu-id="c8d04-127">Azure Data Factory는 반복적으로 데이터 이동 파이프라인을 만들고 배포하기 위한 유용한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-127">Azure Data Factory is a useful service for creating and deploying data movement pipelines on a recurring basis.</span></span>

<span data-ttu-id="c8d04-128">조직에서는 해당 Azure Data Lake Store 계정에 대한 [진단 로깅](data-lake-store-diagnostic-logs.md)을 활성화하여 파일을 삭제하거나 업데이트할 수 있는 사용자에 대한 정보를 제공하는 데이터 액세스 감사 추적을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8d04-128">Organizations can also enable [diagnostic logging](data-lake-store-diagnostic-logs.md) for their Azure Data Lake Store account to collect data access audit trails that provides information about who might have deleted or updated a file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8d04-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c8d04-129">Next steps</span></span>
* [<span data-ttu-id="c8d04-130">Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="c8d04-130">Get Started with Azure Data Lake Store</span></span>](data-lake-store-get-started-portal.md)
* [<span data-ttu-id="c8d04-131">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="c8d04-131">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

