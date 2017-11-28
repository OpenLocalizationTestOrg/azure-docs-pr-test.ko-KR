---
title: "Azure 데이터 레이크 저장소에 대 한 질문과 aaaFrequently | Microsoft Docs"
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
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a><span data-ttu-id="16624-103">Azure Data Lake Store에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="16624-103">Frequently asked questions for Azure Data Lake Store</span></span>
<span data-ttu-id="16624-104">이 문서에 대 한 Faq 관련된 tooAzure 데이터 레이크 저장소는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="16624-104">In this article you will learn about FAQs related tooAzure Data Lake Store.</span></span>

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a><span data-ttu-id="16624-105">어떻게 영역 전체의 재해 또는 실수로 인한 삭제로부터 내 데이터를 추가로 보호할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="16624-105">How can I further protect my data from region-wide disasters or accidental deletions?</span></span>
<span data-ttu-id="16624-106">Azure Data Lake 저장소 계정이 hello 데이터는 자동화 된 복제본을 통해 영역 내에서 복원 tootransient 하드웨어 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="16624-106">hello data in your Azure Data Lake Store account is resilient tootransient hardware failures within a region through automated replicas.</span></span> <span data-ttu-id="16624-107">이렇게 하면 내 구성과 고가용성 회의 hello Azure 데이터 레이크 저장소 SLA 합니다.</span><span class="sxs-lookup"><span data-stu-id="16624-107">This ensures durability and high availability, meeting hello Azure Data Lake Store SLA.</span></span> <span data-ttu-id="16624-108">Toofurther 드문 전체 지역 가동 중단 또는 실수로 인 한 삭제에서 데이터를 보호 하는 방법에 몇 가지 지침이입니다.</span><span class="sxs-lookup"><span data-stu-id="16624-108">Here's some guidance on how toofurther protect your data from rare region-wide outages or accidental deletions.</span></span>

### <a name="disaster-recovery-guidance"></a><span data-ttu-id="16624-109">재해 복구 지침</span><span class="sxs-lookup"><span data-stu-id="16624-109">Disaster recovery guidance</span></span>
<span data-ttu-id="16624-110">모든 고객 tooprepare에는 자신의 재해 복구 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="16624-110">It is critical for every customer tooprepare their own disaster recovery plan.</span></span> <span data-ttu-id="16624-111">재해 복구 계획 toohello toobuild 아래 Azure 문서 키를 읽어보십시오.</span><span class="sxs-lookup"><span data-stu-id="16624-111">Please refer toohello Azure documentation below toobuild your disaster recovery plan.</span></span> <span data-ttu-id="16624-112">여기에는 고유한 계획을 직접 만들 수 있는 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16624-112">Here are some resources that can help you create your own plan.</span></span>

* [<span data-ttu-id="16624-113">Azure 응용 프로그램에 대한 재해 복구 및 고가용성</span><span class="sxs-lookup"><span data-stu-id="16624-113">Disaster recovery and high availability for Azure applications</span></span>](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [<span data-ttu-id="16624-114">Azure 복구력 기술 지침</span><span class="sxs-lookup"><span data-stu-id="16624-114">Azure resiliency technical guidance</span></span>](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a><span data-ttu-id="16624-115">모범 사례</span><span class="sxs-lookup"><span data-stu-id="16624-115">Best practices</span></span>
<span data-ttu-id="16624-116">재해 복구 계획의 주파수 정렬 toohello 요구를 사용 하 여 다른 영역에 데이터 레이크 저장소 계정에 중요 한 데이터 tooanother을 복사 해야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16624-116">We recommend that you copy your critical data tooanother Data Lake Store account in another region with a frequency aligned toohello needs of your disaster recovery plan.</span></span> <span data-ttu-id="16624-117">다양 한 메서드 toocopy 데이터 등 [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) 또는 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16624-117">There are a variety of methods toocopy data including [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) or [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span> <span data-ttu-id="16624-118">Azure Data Factory는 반복적으로 데이터 이동 파이프라인을 만들고 배포하기 위한 유용한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="16624-118">Azure Data Factory is a useful service for creating and deploying data movement pipelines on a recurring basis.</span></span>

<span data-ttu-id="16624-119">지역 가동 중단 발생 하는 경우 데이터 hello 데이터 복사 된 hello 영역에 액세스할 수 있습니다. Hello를 모니터링할 수 있습니다 [Azure 서비스 상태 대시보드에서](https://azure.microsoft.com/status/) toodetermine hello hello 전세계 Azure 서비스 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="16624-119">If a regional outage occurs, you can then access your data in hello region where hello data was copied.You can monitor hello [Azure Service Health Dashboard](https://azure.microsoft.com/status/) toodetermine hello Azure service status across hello globe.</span></span>

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a><span data-ttu-id="16624-120">데이터 손상 또는 삭제 실수 복구 지침</span><span class="sxs-lookup"><span data-stu-id="16624-120">Data corruption or accidental deletion recovery guidance</span></span>
<span data-ttu-id="16624-121">Azure Data Lake Store가 자동화된 복제본을 통해 데이터 복원력을 제공하는 반면 이렇게 하더라도 응용 프로그램(또는 개발자/사용자)의 데이터를 손상시키거나 실수로 삭제하지 않도록 방지하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="16624-121">While Azure Data Lake Store provides data resiliency through automated replicas, this does not prevent your application (or developers/users) from corrupting data or accidentally deleting it.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="16624-122">모범 사례</span><span class="sxs-lookup"><span data-stu-id="16624-122">Best practices</span></span>
<span data-ttu-id="16624-123">tooprevent 실수로 삭제 데이터 레이크 저장소 계정에 대 한 hello 올바른 액세스 정책을 먼저 설정 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16624-123">tooprevent accidental deletion, we recommend that you first set hello correct access policies for your Data Lake Store account.</span></span>  <span data-ttu-id="16624-124">여기에 적용 [Azure 리소스 잠금을](../azure-resource-manager/resource-group-lock-resources.md) 으로 중요 한 리소스를 사용할 수 있는 hello를 사용 하 여 적용 계정 및 파일 수준 액세스 제어 아래로 toolock [데이터 레이크 저장소 보안 기능](data-lake-store-security-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="16624-124">This includes applying [Azure resource locks](../azure-resource-manager/resource-group-lock-resources.md) toolock down important resources as well as applying account and file level access control using hello available [Data Lake Store security features](data-lake-store-security-overview.md).</span></span> <span data-ttu-id="16624-125">다른 Data Lake Store 계정, 폴더 또는 Azure 구독에서 [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) 또는 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md)를 사용하여 중요한 데이터의 복사본을 정기적으로 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="16624-125">We also recommend that you routinely create copies of your critical data using [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) or [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) in another Data Lake Store account, folder, or Azure subscription.</span></span>  <span data-ttu-id="16624-126">이 경우 데이터 손상 또는 삭제 인시던트에서 사용 되는 toorecover 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16624-126">This can be used toorecover from a data corruption or deletion incident.</span></span> <span data-ttu-id="16624-127">Azure Data Factory는 반복적으로 데이터 이동 파이프라인을 만들고 배포하기 위한 유용한 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="16624-127">Azure Data Factory is a useful service for creating and deploying data movement pipelines on a recurring basis.</span></span>

<span data-ttu-id="16624-128">또한 조직에서는 사용할 수 [진단 로깅](data-lake-store-diagnostic-logs.md) 자신의 Azure 데이터 레이크 저장소 계정 toocollect 삭제 하거나 파일을 업데이트 수는 방법에 대 한 정보를 제공 하는 데이터 액세스 감사 내역은 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="16624-128">Organizations can also enable [diagnostic logging](data-lake-store-diagnostic-logs.md) for their Azure Data Lake Store account toocollect data access audit trails that provides information about who might have deleted or updated a file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16624-129">다음 단계</span><span class="sxs-lookup"><span data-stu-id="16624-129">Next steps</span></span>
* [<span data-ttu-id="16624-130">Azure Data Lake Store 시작</span><span class="sxs-lookup"><span data-stu-id="16624-130">Get Started with Azure Data Lake Store</span></span>](data-lake-store-get-started-portal.md)
* [<span data-ttu-id="16624-131">데이터 레이크 저장소의 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="16624-131">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

