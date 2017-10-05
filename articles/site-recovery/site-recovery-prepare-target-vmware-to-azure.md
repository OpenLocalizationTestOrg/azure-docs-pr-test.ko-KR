---
title: "대상 준비(VMware에서 Azure로) | Microsoft Docs"
description: "이 문서에서는 VMware 가상 컴퓨터를 Azure에 복제하는 작업을 시작하기 위해 Azure 환경을 준비하는 방법을 설명합니다."
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
ms.openlocfilehash: c84a775564769ddc796aa9d75add019ef1003175
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-target-vmware-to-azure"></a><span data-ttu-id="700ee-103">대상 준비(VMware에서 Azure로)</span><span class="sxs-lookup"><span data-stu-id="700ee-103">Prepare target (VMware to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="700ee-104">VMware에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="700ee-104">VMware to Azure</span></span>](./site-recovery-prepare-target-vmware-to-azure.md)
> * [<span data-ttu-id="700ee-105">물리적 서버에서 Azure로</span><span class="sxs-lookup"><span data-stu-id="700ee-105">Physical to Azure</span></span>](./site-recovery-prepare-target-physical-to-azure.md)

<span data-ttu-id="700ee-106">이 문서에서는 VMware 가상 컴퓨터를 Azure에 복제하는 작업을 시작하기 위해 Azure 환경을 준비하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-106">This article describes how to prepare your Azure environment to start replicating VMware virtual machines to Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="700ee-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="700ee-107">Prerequisites</span></span>

<span data-ttu-id="700ee-108">이 문서에서는 다음을 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-108">The article assumes the following:</span></span>
- <span data-ttu-id="700ee-109">VMware 가상 컴퓨터를 보호하기 위해 Recovery Services 자격 증명 모음을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-109">You have created a Recovery Services Vault to protect your VMware virtual machines.</span></span> <span data-ttu-id="700ee-110">[Azure Portal](http://portal.azure.com "Azure Portal")에서 Recovery Services 자격 증명 모음을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-110">You can create a Recovery Services Vault from the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="700ee-111">Azure에 VMware 가상 컴퓨터를 복제하기 위한 [온-프레미스 환경을 설정](./site-recovery-set-up-vmware-to-azure.md)했습니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-111">You have [setup your on-premises environment](./site-recovery-set-up-vmware-to-azure.md) to replicate VMware virtual machines to Azure.</span></span>

## <a name="prepare-target"></a><span data-ttu-id="700ee-112">대상 준비</span><span class="sxs-lookup"><span data-stu-id="700ee-112">Prepare target</span></span>

<span data-ttu-id="700ee-113">**1단계: 보호 목표 선택** 및 **2단계: 원본 준비**를 완료한 후 **3단계: 대상**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-113">After completing the **Step 1:Select Protection goal** and **Step 2:Prepare Source**, you are taken to **Step 3: Target**</span></span>

![대상 준비](./media/site-recovery-prepare-target-vmware-to-azure/prepare-target-vmware-to-azure.png)

1. <span data-ttu-id="700ee-115">**구독:** 드롭다운 메뉴에서 가상 컴퓨터를 복제할 대상 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-115">**Subscription:** From the drop down menu, select the Subscription that you want to replicate your virtual machines to.</span></span>
2. <span data-ttu-id="700ee-116">**배포 모델:** 배포 모델(클래식 또는 리소스 관리자)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-116">**Deployment Model:** Select the deployment model (Classic or Resource Manager)</span></span>

<span data-ttu-id="700ee-117">선택한 배포 모델에 따라 유효성 검사를 실행하여, 가상 컴퓨터를 복제하고 장애 조치를 수행할 대상 구독에 하나 이상의 호환되는 저장소 계정 및 가상 네트워크가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-117">Based on the chosen deployment model, a validation is run to ensure that you have at least one compatible storage account and virtual network in the target subscription to replicate and failover your virtual machine to.</span></span>

<span data-ttu-id="700ee-118">유효성 검사가 성공적으로 완료되면 확인을 클릭하여 다음 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-118">Once the validations complete successfully, click OK to go to the next step.</span></span>

<span data-ttu-id="700ee-119">호환되는 Resource Manager 저장소 계정 또는 가상 네트워크가 없거나 더 추가하려는 경우 블레이드 맨 위에서 **+저장소 계정** 또는 **+네트워크** 단추를 클릭하여 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="700ee-119">If you don't have a compatible Resource Manager storage account or virtual network, or would like to add more, you can do so by clicking the **+ Storage Account** or **+ Network** buttons on the top of the blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="700ee-120">다음 단계</span><span class="sxs-lookup"><span data-stu-id="700ee-120">Next steps</span></span>
<span data-ttu-id="700ee-121">[복제 설정 구성](./site-recovery-setup-replication-settings-vmware.md)</span><span class="sxs-lookup"><span data-stu-id="700ee-121">[Configure replication settings](./site-recovery-setup-replication-settings-vmware.md).</span></span>
