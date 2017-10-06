---
title: "aaaAzure 함수 소비와 앱 서비스 계획 | Microsoft Docs"
description: "이벤트 기반 작업 부하의 toomeet hello 요구 사항을 Azure 기능을 확장 하는 방법 이해 합니다."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "Azure Functions, 함수, 이벤트 처리, webhook, 동적 계산, 서버가 없는 아키텍처"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Azure Functions 소비 및 App Service 계획 

## <a name="introduction"></a>소개

Azure Functions는 소비 계획 및 Azure App Service 계획 두 가지 모드로 실행할 수 있습니다. hello 소비 계획 코드 실행 되 고 필요한 toohandle 부하로 하 여 확장 하 고 그런 다음 코드를 실행 중이지 않을 때 확장 하는 경우 계산 능력을 자동으로 할당 합니다. 따라서 유휴 Vm에 대 한 toopay 없는 바뀌고 용량이 부족 tooreserve 미리. 이 문서는 hello 소비 계획에 중점을 둡니다. 앱 서비스 계획 hello 작동 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 앱 서비스 계획 심도 깊은 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다. 

Azure 기능에 익숙하지 않은 경우 참조 hello [Azure 함수 개요](functions-overview.md)합니다.

호스팅 계획을 구성 해야 함수 응용 프로그램을 만들 때 함수에 대 한 hello 이러한 앱을 포함 합니다. Hello의 인스턴스 두 모드에서는 *Azure 함수 호스트* hello 함수를 실행 합니다. hello 유형 계획 컨트롤입니다.

* 호스트 인스턴스 확장 방법
* hello 리소스는 사용할 수 있는 tooeach 호스트입니다.

현재 hello hello 함수 앱을 만드는 중 hello 계획 형식을 선택 해야 합니다. 나중에 변경할 수 없습니다. 

Hello 앱 서비스 계획에는 계층 간에 확장할 수 있습니다. Hello 소비 계획을 Azure 함수 모든 리소스 할당을 자동으로 처리합니다.

## <a name="consumption-plan"></a>소비 계획

소비 계획을 사용 하는 경우 hello Azure 함수 호스트 인스턴스가 동적으로 추가 및 제거 들어오는 이벤트의 hello 수를 기반 합니다. 이 계획은 자동으로 규모를 조정하며, 함수를 실행하는 경우에만 계산 리소스에 대한 요금이 청구됩니다. 소비 계획에서 함수는 최대 10분 동안 실행될 수 있습니다. 

> [!NOTE]
> 함수는 소비 계획에 대해 hello 기본 제한 시간 5 분입니다. hello 값일 수 증가 too10 분 hello 함수 응용 프로그램에 대 한 hello 속성을 변경 하 여 `functionTimeout` 에 [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)합니다.

대금 청구는 실행 시간 및 사용되는 메모리를 기반으로 하며 함수 앱 내에서 모든 함수에 대해 집계됩니다. 자세한 내용은 참조 hello [가격 책정 페이지 Azure 함수]합니다.

hello 소비 계획 hello 기본 템플릿이 고 hello 다음 이점을 제공 합니다.
- 함수를 실행 중인 경우에만 지불
- 높은 부하 기간 동안에도 자동으로 규모 확장

## <a name="app-service-plan"></a>앱 서비스 계획

Hello 앱 서비스 계획 기능 앱에서 Basic, Standard 및 Premium Sku 비슷한 tooWeb 앱 전용된 Vm에서 실행 합니다. 전용된 Vm는 할당 된 tooyour 앱 서비스 앱 hello 함수 호스트는 항상 실행 됩니다.

앱 서비스 계획의 경우 다음 hello에 고려해 야 합니다.
- 이미 다른 App Service 인스턴스를 실행하고 있는 기존의 활용도가 낮은 VM이 있습니다.
- 계속적으로 또는 연속적으로 거의 함수 앱 toorun을 예상 합니다.
- Hello 소비 계획에서 제공 하는 것 보다 많은 CPU 또는 메모리 옵션 필요 합니다.
- Hello hello 소비 계획에 허용 되는 최대 실행 시간 보다 긴 toorun이 필요 합니다.

VM은 런타임 및 메모리에서 비용을 분리합니다. 결과적으로 할당 하는 hello VM 인스턴스의 hello 비용 보다 더 지불 하지 않습니다. 앱 서비스 계획 hello 작동 하는 방법에 대 한 자세한 내용은 참조 hello [Azure 앱 서비스 계획 심도 깊은 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다. 

App Service 계획을 사용하면 더 많은 VM 인스턴스를 추가하여 수동으로 확장하거나 자동 조정을 사용하도록 설정할 수 있습니다. 자세한 내용은 [수동 또는 자동으로 인스턴스 개수 조정](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)을 참조하세요. 다른 App Service 계획을 선택하여 확장할 수도 있습니다. 자세한 내용은 [Azure에서 앱 확장](../app-service-web/web-sites-scale.md)을 참조하세요. 앱 서비스 계획에 toorun JavaScript 함수를 계획 하는 경우 더 적은 코어 있는 계획을 선택 해야 합니다. 자세한 내용은 참조 hello [함수에 대 한 JavaScript 참조](functions-reference-node.md#choose-single-core-app-service-plans)합니다.  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
### 무중단

앱 서비스 계획을 실행 하면 hello를 사용 해야 하면 **Always On** 함수 앱은 제대로 실행 되도록 설정 합니다. 앱 서비스 계획을 hello 함수 런타임 HTTP 트리거만 "시작 하 여" 함수 있으므로 몇 분 동안 활동이 없, 유휴 상태 전환 됩니다. 이 비슷한 toohow WebJobs Always On을 사용 해야 합니다. 

무중단은 App Service 계획에서만 사용할 수 있습니다. 한 소비 계획 hello 플랫폼 기능 앱을 자동으로 활성화합니다.

## <a name="storage-account-requirements"></a>저장소 계정 요구 사항

소비 계획 또는 App Service 계획에서 함수 앱에는 Azure Blob, Queue 및 Table storage를 지원하는 Azure Storage 계정이 필요합니다. 내부적으로 Azure Functions는 트리거 관리 및 함수 실행 로깅 등의 작업을 위해 Azure Storage를 사용합니다. Blob 전용 저장소 계정(Premium Storage 포함) 및 영역 중복 저장소 복제가 사용되는 범용 저장소 계정 같은 일부 저장소 계정은 큐 및 테이블을 지원하지 않습니다. 이러한 계정은 hello에서 필터링 됩니다 **저장소 계정** 블레이드 함수 응용 프로그램을 만들 때.

저장소 계정 유형에 대 한 자세한 정보는 toolearn 참조 [hello Azure 저장소 서비스 소개](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)합니다.

## <a name="how-hello-consumption-plan-works"></a>Hello 소비 계획의 작동 원리

hello 소비 계획 hello 함수에 트리거되는 이벤트 수에 따라 hello 함수 호스트의 추가 인스턴스를 추가 하 여 CPU 및 메모리 리소스를 자동으로 조정 합니다. Hello 함수 호스트의 각 인스턴스에 메모리 제한 too1.5 GB입니다.

사용 하는 경우에 호스팅 계획 소비 hello을 함수 코드 파일 hello 주 저장소 계정에서 Azure 파일 공유에 저장 됩니다. Hello 주 저장소 계정을 삭제 하면이 콘텐츠는 삭제 되 고 복구할 수 없습니다.

> [!NOTE]
> Blob 트리거 소비 계획을 사용 하는 경우에 있을 수 있습니다 켜기 tooa 10 분 지연 함수 앱이 유휴 내려갔습니다 경우 새 blob을 처리 합니다. Hello 함수 응용 프로그램을 실행 한 후 blob 즉시 처리 됩니다. 이 초기 tooavoid 지연 hello 다음 옵션 중 하나를 고려 하십시오.
> - 무중단이 사용되는 App Service 계획을 사용합니다.
> - 예: hello blob 이름을 포함 하는 큐 메시지 처리, 다른 메커니즘 tootrigger hello blob을 사용 합니다. 예를 들어 [Blob 입력 바인딩을 사용하여 큐 트리거](functions-bindings-storage-blob.md#input-sample)를 참조하세요.

### <a name="runtime-scaling"></a>런타임 크기 조정

Azure 함수 hello 라는 구성 요소를 사용 하 여 *배율 컨트롤러* toomonitor 이벤트의 비율이 hello 및 확인 여부 tooscale out 또는 축소 합니다. hello 눈금 컨트롤러 휴리스틱을 사용 하 여 각 트리거 형식에 대 한 합니다. 예를 들어 Azure 큐 저장소 트리거를 사용 하는 경우 hello 큐 길이 및 hello 가장 오래 된 큐 메시지의 hello 나이에 따라 조정 합니다.

눈금의 hello 단위는 hello 함수 앱입니다. Hello 함수 앱으로 크기가 조정 될 때 더 많은 리소스를 toorun hello Azure 함수 호스트의 여러 인스턴스를 할당 합니다. 반대로, 요구량이 감소할 계산, hello 눈금 컨트롤러 함수 호스트 인스턴스를 제거 합니다. hello 인스턴스 수는 결국 축소 toozero 함수 앱 내에서 실행 하는 함수가 없는 경우.

![이벤트를 모니터링하고 인스턴스를 만드는 크기 조정 컨트롤러](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>청구 모델

Hello 소비 계획 hello에 자세히 설명 되어 대금 청구 [가격 책정 페이지 Azure 함수]합니다. 사용 현황 hello 함수 앱 수준에서 집계 되 고 함수 코드를 실행 하는 hello 시간만 계산 합니다. hello 다음은 청구에 대 한 단위입니다. 
* **기가바이트-초 단위의 리소스 소비(GB-s)**. 함수 앱 내 모든 함수의 메모리 크기와 실행 시간 조합으로 계산됩니다. 
* **실행 횟수**. 응답 tooan 이벤트에서 트리거되는 바인딩에서 함수가 실행 될 때마다를 계산 합니다.

[가격 책정 페이지 Azure 함수]: https://azure.microsoft.com/pricing/details/functions
