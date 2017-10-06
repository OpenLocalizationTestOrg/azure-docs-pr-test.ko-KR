---
title: "Microsoft Azure 클라우드 서비스 FAQ에 대 한 aaaDeployment 문제 | Microsoft Docs"
description: "이 문서에서는 Microsoft Azure 클라우드 서비스에 대 한 배포에 대 한 질문과 대답 hello를 나열 합니다."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure Cloud Services의 배포 문제: FAQ(질문과 대답)

이 문서는 [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services)의 배포 문제에 대한 질문과 대답을 포함합니다. Hello를 참조할 수 있습니다 [클라우드 서비스 VM 크기 페이지](cloud-services-sizes-specs.md) 크기 정보에 대 한 합니다.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>이유에서 클라우드 서비스 toohello 배포 슬롯을 때때로 준비 실패 리소스 할당 오류와 함께 이미 있는 경우 hello 프로덕션 슬롯에서 기존 배포 합니까?
클라우드 서비스에 배포 슬롯에 경우 hello 전체 클라우드 서비스는 고정 된 tooa 특정 클러스터입니다. 이 hello 프로덕션 슬롯에 배포를 이미 있으면 새 스테이징 배포 할당할 수 있습니다. 동일한 hello 프로덕션 슬롯으로 클러스터 hello에 것을 의미 합니다.

할당 오류 클라우드 서비스가 위치한 hello 클러스터에 충분 한 물리적 계산 리소스 toosatisfy 배포 요청 없을 때 발생 합니다.

이러한 할당 오류를 완화하는 도움말은 [Cloud Service 할당 실패: 솔루션](cloud-services-allocation-failures.md#solutions)을 참조하세요.

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>클라우드 서비스 배포를 스케일 업 또는 스케일 아웃하는 경우 할당 오류가 발생하는 이유는 무엇인가요?
클라우드 서비스를 배포 하는 경우 일반적으로 고정 된 tooa 특정 클러스터를 가져옵니다. 즉, 수직 확장/아웃 기존 클라우드 서비스 hello에 새 인스턴스를 할당 해야 동일한 클러스터입니다. Hello 클러스터 용량에 가까워졌습니다 또는 hello 필요한 VM 크기/유형을 사용할 수 없는 hello 요청이 실패할 수 있습니다.

이러한 할당 오류를 완화하는 도움말은 [Cloud Service 할당 실패: 솔루션](cloud-services-allocation-failures.md#solutions)을 참조하세요.

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>선호도 그룹에 클라우드 서비스를 배포하는 경우 할당 오류가 발생하는 이유는 무엇인가요?
새 배포 tooan 빈 클라우드 서비스는 hello 클라우드 서비스는 고정 된 tooan 선호도 그룹 하지 않는 한 hello 패브릭으로 해당 지역에서 어떤 클러스터에 할당할 수 있습니다. Hello에 동일한 선호도 그룹을 시도 하는 배포 toohello 동일한 클러스터입니다. Hello 클러스터 용량에 가까워졌습니다, hello 요청이 실패할 수 있습니다.

이러한 할당 오류를 완화하는 도움말은 [Cloud Service 할당 실패: 솔루션](cloud-services-allocation-failures.md#solutions)을 참조하세요.

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>이유는 v M 크기를 변경 하거나 새 VM tooan 기존 클라우드 서비스를 경우에 따라 추가 할당 오류가 발생?
데이터 센터의 hello 클러스터 컴퓨터 종류 (예:는 계열, Av2 시리즈, D 시리즈, Dv2 시리즈, G 시리즈, H 시리즈, 등)의 구성이 각기 다른 있을 수 있습니다. 하지만 일부 hello 클러스터 Vm의 모든 hello 종류에는 반드시 합니다. 예를 들어 tooadd D 시리즈 A 시리즈 전용 클러스터에 이미 배포 된 VM tooa 클라우드 서비스에서 하면 할당 오류가 발생 합니다. 또한 발생 합니다 하면 (예: A 시리즈 tooa D 시리즈에서 전환) toochange SKU VM의 크기를 조정 합니다.

이러한 할당 오류를 완화하는 도움말은 [Cloud Service 할당 실패: 솔루션](cloud-services-allocation-failures.md#solutions)을 참조하세요.

해당 지역에서 사용할 수 있는 toocheck hello 크기 참조 [Microsoft Azure: 지역에 따라 사용할 수 있는 제품](https://azure.microsoft.com/regions/services)합니다.

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>이유는 클라우드 배포 서비스 수행 어느 fail due toolimits/할당량/제약 조건 내 구독 또는 서비스에서?
클라우드 서비스의 배포는 hello 리소스를 할당 하는 필수 toobe hello 기본값 또는 hello 지역/데이터 센터 수준에서 서비스에 대해 허용 된 최대 할당량을 초과 하는 경우 실패할 수 있습니다. 자세한 내용은 [Cloud Services 제한](../azure-subscription-service-limits.md#cloud-services-limits)을 참조하세요.

또한 hello 포털에서 구독에 대 한 현재 사용량/할당량 hello를 추적할 수 있습니다: Azure 포털 = > 구독 = > \<구독 적절 한 > = > "사용량 + 할당량"입니다.

Hello Azure 청구 Api를 통해 리소스 사용/사용 관련 정보를 검색할 수도 있습니다. [Azure 리소스 사용량 API(미리 보기)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview)을 참조하세요.

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>다시 배포 하지 않고 배포 된 클라우드 서비스 VM의 hello 크기를 변경할 수는 방법
다시 배포 하지 않고 배포 된 클라우드 서비스의 hello VM 크기를 변경할 수 없습니다. VM 크기 hello hello CSDEF는 재배포를 업데이트할 수 있는 내장 됩니다.

자세한 내용은 참조 [어떻게 tooupdate 클라우드 서비스](cloud-services-update-azure-service.md)합니다.

 
