---
title: "대상 (VMware tooAzure) 준비 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 tooprepare VMware 가상 컴퓨터 tooAzure를 복제 하 여 Azure 환경 toostart 합니다."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhemraj
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 5/31/2017
ms.author: bsiva
ms.openlocfilehash: 5975d3c122032f92f8df370ee74fa0c7012ebe2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-target-vmware-tooazure"></a><span data-ttu-id="549eb-103">대상 (VMware tooAzure) 준비</span><span class="sxs-lookup"><span data-stu-id="549eb-103">Prepare target (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="549eb-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="549eb-104">VMware tooAzure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="549eb-105">물리적 tooAzure</span><span class="sxs-lookup"><span data-stu-id="549eb-105">Physical tooAzure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="549eb-106">이 문서에서는 설명 방법을 tooprepare VMware 가상 컴퓨터 tooAzure를 복제 하 여 Azure 환경 toostart 합니다.</span><span class="sxs-lookup"><span data-stu-id="549eb-106">This article describes how tooprepare your Azure environment toostart replicating VMware virtual machines tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="549eb-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="549eb-107">Prerequisites</span></span>

<span data-ttu-id="549eb-108">hello 문서 hello 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="549eb-108">hello article assumes hello following:</span></span>
- <span data-ttu-id="549eb-109">복구 서비스 자격 증명 모음 tooprotect VMware 가상 컴퓨터를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="549eb-109">You have created a Recovery Services Vault tooprotect your VMware virtual machines.</span></span> <span data-ttu-id="549eb-110">Hello에서 복구 서비스 자격 증명 모음을 만들 수 있습니다 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.</span><span class="sxs-lookup"><span data-stu-id="549eb-110">You can create a Recovery Services Vault from hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="549eb-111">있는 [온-프레미스 환경을 설정](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware 가상 컴퓨터 tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="549eb-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) tooreplicate VMware virtual machines tooAzure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="549eb-112">대상 준비</span><span class="sxs-lookup"><span data-stu-id="549eb-112">Prepare target</span></span>

<span data-ttu-id="549eb-113">Hello를 완료 한 후 **단계 1:Select 보호 목표** 및 **2 단계: 준비 소스**, 너무 취해집니다**3 단계: 대상**</span><span class="sxs-lookup"><span data-stu-id="549eb-113">After completing hello **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken too**Step 3: Target**</span></span>

![대상 준비](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="549eb-115">**구독:** hello에서 드롭 다운 메뉴에서 선택 hello tooreplicate 구독에 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="549eb-115">**Subscription:** From hello drop down menu, select hello Subscription that you want tooreplicate your virtual machines to.</span></span>
2. <span data-ttu-id="549eb-116">**배포 모델:** 선택 hello 배포 모델 (Classic 또는 리소스 관리자)</span><span class="sxs-lookup"><span data-stu-id="549eb-116">**Deployment Model:** Select hello deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="549eb-117">배포 모델을 선택 하는 hello에 따라, 유효성 검사를 tooensure 해야 하는 하나 이상의 호환 되는 저장소 계정 및 대상 구독 tooreplicate hello 및 장애 조치의 가상 네트워크를 가상 컴퓨터를 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="549eb-117">Based on hello chosen deployment model, a validation is run tooensure that you have at least one compatible storage account and virtual network in hello target subscription tooreplicate and failover your virtual machine to.</span></span>

<span data-ttu-id="549eb-118">Hello 유효성 검사를 성공적으로 완료 되 면 확인 toogo toohello 다음 단계를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="549eb-118">Once hello validations complete successfully, click OK toogo toohello next step.</span></span>

<span data-ttu-id="549eb-119">더 많은 tooadd ु 없거나 호환 리소스 관리자 저장소 계정 또는 가상 네트워크 않은 후 그렇게 hello를 클릭 하 여 **저장소 계정 추가** 또는 **+ 네트워크** hello hello 위쪽에 단추 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="549eb-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like tooadd more, you can do so by clicking hello **+ Storage Account** or **+ Network** buttons on hello top of hello blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="549eb-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="549eb-120">Next steps</span></span>
<span data-ttu-id="549eb-121">[복제 설정 구성](./site-recovery-setup-replication-settings-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="549eb-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
