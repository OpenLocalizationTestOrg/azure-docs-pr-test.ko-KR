---
title: "여러 가상 컴퓨터 만들기 | Microsoft Docs"
description: "Windows에서 여러 가상 컴퓨터 만들기에 대한 옵션"
services: virtual-machines-windows
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: dfc1d1bb-a47d-4d7c-9fd2-f12050baacab
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: guybo
ms.openlocfilehash: 5e96805f8880a30a5fc8779d8f07addb6d068c09
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>여러 Azure 가상 컴퓨터 만들기
많은 수의 유사한 VM(가상 컴퓨터)을 만들어야 하는 다양한 시나리오가 있습니다. 일부 예로는 HPC(고성능 컴퓨팅), 대규모 데이터 분석, 확장 가능하며 보통 상태 정보를 저장하지 않는 중간 계층 또는 백 엔드 서버(예: webserver), 분산 데이터베이스가 포함됩니다.

이 문서에서는 Azure에서 여러 VM을 만들기 위해 사용할 수 있는 옵션에 대해 설명합니다. 이러한 옵션은 VM 시리즈를 수동으로 만드는 단순한 경우를 벗어납니다. 많은 VM을 만들어야 하는 경우 일반적으로 사용하는 프로세스는 적절하게 확장되지 않습니다.

여러 개의 유사한 VM을 만드는 한 가지 방법은 Azure Resource Manager의 *리소스 루프*구조를 사용하는 것입니다.

## <a name="resource-loops"></a>리소스 루프
리소스 루프는 Azure Resource Manager 템플릿에 사용되는 간단한 구문입니다. 리소스 루프는 비슷하게 구성된 리소스 집합을 루프로 만들 수 있습니다. 리소스 루프를 사용하면 여러 개의 저장소 계정, 네트워크 인터페이스 또는 가상 컴퓨터를 만들 수 있습니다. 리소스 루프에 대한 자세한 내용은 [리소스 루프를 사용하여 가용성 집합에 VM 만들기](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/)를 참조하세요.

## <a name="challenges-of-scale"></a>규모에 따른 해결 과제
리소스 루프를 사용하면 대규모 클라우드 인프라를 손쉽게 만들고 좀 더 간결한 템플릿을 생성할 수 있지만 해결해야 할 문제도 있습니다. 예를 들어 리소스 루프를 사용하여 100개의 가상 컴퓨터를 만드는 경우 해당 VM 및 저장소 계정과 NIC(네트워크 인터페이스 컨트롤러) 간에 상관 관계를 구축해야 합니다. VM 수가 저장소 계정의 수와 다를 수 있으므로 다양한 리소스 루프 크기를 처리해야 합니다. 이러한 문제는 해결할 수 있지만 규모에 따라 복잡성이 크게 증가합니다.

또 다른 과제는 탄력적으로 확장되는 인프라가 필요할 때 발생합니다. 예를 들어 워크로드에 따라 VM 수를 자동으로 늘리거나 줄이는 자동 크기 조정 인프라를 원할 수 있습니다. VM은 수 변경(규모 확장 및 규모 감축)에 대한 통합 메커니즘을 제공하지 않습니다. VM을 제거하여 규모를 줄일 경우 업데이트 및 장애 도메인 간에 VM 균형을 유지하여 고가용성을 보장하는 일이 어려워집니다.

마지막으로 리소스 루프를 사용할 때 리소스를 만들기 위한 여러 번의 호출이 기본 패브릭에 대해 진행됩니다. 여러 호출이 유사한 리소스를 만들 경우 Azure는 이 디자인을 개선하고 최적화하여 배포 안정성 및 성능을 개선할 암시적 기회를 얻게 됩니다. 이로 인해 *가상 컴퓨터 크기 집합* 이 탄생했습니다.

## <a name="virtual-machine-scale-sets"></a>가상 컴퓨터 크기 집합
가상 컴퓨터 크기 집합은 동일한 VM 집합을 배포하고 관리하기 위한 Azure 계산 리소스입니다. 모든 VM이 동일하게 구성되면 VM 크기 집합의 규모를 쉽게 감축 및 확장할 수 있습니다. 집합의 VM 수만 변경하면 되기 때문입니다. 또한 워크로드의 요구에 따라 자동으로 크기가 조정되도록 VM 크기 집합을 구성할 수도 있습니다.

계산 리소스 크기를 조정해야 하는 응용 프로그램의 경우 크기 조정 작업은 장애 도메인 및 업데이트 도메인 간에 암시적으로 균형이 조정됩니다.

VM 크기 집합에서는 IC, VM과 같은 여러 리소스 간의 상관 관계를 구성하지 않고 네트워크, 저장소, 가상 컴퓨터, 확장 속성을 중앙 집중적으로 구성할 수 있습니다.

VM 크기 집합에 대한 소개 정보를 보려면 [가상 컴퓨터 크기 집합 제품 페이지](https://azure.microsoft.com/services/virtual-machine-scale-sets/)를 참조하세요. 자세한 내용은 [가상 컴퓨터 크기 집합 설명서](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)를 참조하세요.

