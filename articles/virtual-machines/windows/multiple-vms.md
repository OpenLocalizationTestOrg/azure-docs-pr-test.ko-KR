---
title: "aaaCreate 여러 가상 컴퓨터 | Microsoft Docs"
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
ms.openlocfilehash: 37729fabd91049744f6bd94c55221f5c1c65d527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-multiple-azure-virtual-machines"></a>여러 Azure 가상 컴퓨터 만들기
많은 수의 유사한 가상 컴퓨터 (Vm) toocreate 해야 하는 많은 시나리오가 있습니다. 일부 예로는 HPC(고성능 컴퓨팅), 대규모 데이터 분석, 확장 가능하며 보통 상태 정보를 저장하지 않는 중간 계층 또는 백 엔드 서버(예: webserver), 분산 데이터베이스가 포함됩니다.

이 문서에서는 Azure에서 여러 Vm hello 사용할 수 있는 옵션 toocreate를 설명 합니다. 이러한 옵션은 수동으로 일련의 Vm 생성 하는 hello 간단한 경우 넘지. toocreate 많은 Vm을 일반적으로 사용 하는 hello 프로세스는 소수의 Vm 이상 toocreate 해야 하는 경우에 확장 하지 않습니다.

많은 유사한 Vm은 toouse hello Azure 리소스 관리자 구문의 한 가지 방법은 toocreate *리소스 루프*합니다.

## <a name="resource-loops"></a>리소스 루프
리소스 루프는 Azure Resource Manager 템플릿에 사용되는 간단한 구문입니다. 리소스 루프는 비슷하게 구성된 리소스 집합을 루프로 만들 수 있습니다. 여러 저장소 계정, 네트워크 인터페이스 또는 가상 컴퓨터 리소스 루프 toocreate를 사용할 수 있습니다. 너무 리소스 루프에 대 한 자세한 내용은 참조[리소스 루프를 사용 하 여 가용성 집합에서 Vm 만들기](https://azure.microsoft.com/documentation/templates/201-vm-copy-index-loops/)합니다.

## <a name="challenges-of-scale"></a>규모에 따른 해결 과제
리소스 루프 클라우드 인프라 쉽게 toobuild 배율로 지정 하 고 더 간결한 서식 파일을 생성, 있지만 특정 문제가 있는 상태로 유지 합니다. 예를 들어 한 리소스 루프 toocreate 100 가상 컴퓨터를 사용 하는 경우 해당 Vm 및 저장소 계정을 사용 하 여 toocorrelate 네트워크 인터페이스 컨트롤러 (Nic) 필요 합니다. Vm 수 hello hello 저장소 계정 수와에서 다른 가능성이 toobe 이기 때문에 해야 합니다. 다른 리소스 루프 크기를 가진 toodeal 너무 합니다. 해결할 수 있는 문제는 이지만 배율로 hello 복잡성이 크게 증가 합니다.

또 다른 과제는 탄력적으로 확장되는 인프라가 필요할 때 발생합니다. 예를 들어 자동으로 증가 하거나 hello 응답 tooworkload에서 Vm 수를 감소 하는 자동 크기 조정 인프라를 좋습니다. Vm 수 (수평 확장 및 눈금의)에 통합된 메커니즘 toovary에서는 제공 하지 않습니다. Vm을 제거 하 여 확장의 경우 어려운 tooguarantee 고가용성 Vm 업데이트 및 오류 도메인 간에 균형을 확인 하 여입니다.

마지막으로, 리소스 루프를 사용 하면 여러 호출 toocreate 리소스 toohello 기본 패브릭을 이동 합니다. 여러 번 호출 유사한 리소스를 만드는 경우 Azure이이 설계에는 암시적 기회 tooimprove 개이고 배포 안정성과 성능을 최적화 합니다. 이로 인해 *가상 컴퓨터 크기 집합* 이 탄생했습니다.

## <a name="virtual-machine-scale-sets"></a>가상 컴퓨터 확장 집합
가상 컴퓨터 크기 집합은 Azure 계산 리소스 toodeploy 되며 동일한 Vm 집합을 관리 합니다. 구성 된 모든 Vm이 있는 동일 hello, VM 크기 집합은에 쉽게 tooscale 및 스케일 아웃 합니다. 단순히 hello 집합에서 Vm의 hello 번호를 변경 합니다. 또한 VM 크기 조정 설정 tooautoscale hello 작업의 hello 수요에 따라 구성할 수 있습니다.

눈금에 및 tooscale 계산 리소스를 필요로 하는 응용 프로그램에 대 한 작업은 암시적으로 장애 도메인과 업데이트 도메인에 걸쳐 분산 됩니다.

VM 크기 집합에서는 IC, VM과 같은 여러 리소스 간의 상관 관계를 구성하지 않고 네트워크, 저장소, 가상 컴퓨터, 확장 속성을 중앙 집중적으로 구성할 수 있습니다.

소개 tooVM 배율 설정에 대 한 참조 toohello [제품 페이지를 설정 하는 가상 컴퓨터 크기](https://azure.microsoft.com/services/virtual-machine-scale-sets/)합니다. 자세한 내용은 이동 toohello [설명서를 설정 하는 가상 컴퓨터 크기 조정](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)합니다.

