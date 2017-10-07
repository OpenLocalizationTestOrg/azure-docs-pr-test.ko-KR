---
title: "PowerShell 스크립트 예제는 클러스터에서 응용 프로그램 제거 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 클러스터에서 응용 프로그램 제거"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Service Fabric 클러스터에서 응용 프로그램 제거

이 샘플 스크립트는 실행 중인 서비스 패브릭 응용 프로그램 인스턴스를 삭제 하 고, 응용 프로그램 유형 및 버전 hello 클러스터에서 등록을 취소, hello 클러스터 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제 합니다.  Hello 응용 프로그램 인스턴스 삭제는 실행 중인 서비스 인스턴스를 해당 응용 프로그램과 관련 된 모든 hello도 삭제 됩니다. 필요에 따라 hello 매개 변수를 사용자 지정 합니다. 

필요한 경우 hello로 hello 서비스 패브릭 PowerShell 모듈을 설치 [서비스 패브릭 SDK](../service-fabric-get-started.md)합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Hello 클러스터에서 실행 중인 서비스 패브릭 응용 프로그램 인스턴스를 제거합니다.  |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | 서비스 패브릭 응용 프로그램 유형 및 버전 hello 클러스터에서 등록 취소합니다. |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Hello 이미지 저장소에서 서비스 패브릭 응용 프로그램 패키지를 제거합니다.|

## <a name="next-steps"></a>다음 단계

Hello 서비스 패브릭 PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/service-fabric/?view=azureservicefabricps)합니다.

Azure Service Fabric에 대 한 추가 Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.
