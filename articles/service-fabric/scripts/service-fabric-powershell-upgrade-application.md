---
title: "서비스 패브릭 응용 프로그램을 업그레이드 하는 PowerShell 스크립트 샘플-aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 응용 프로그램 업그레이드"
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Service Fabric 응용 프로그램 업그레이드

이 샘플 스크립트를 실행 중인 서비스 패브릭 응용 프로그램 인스턴스 tooversion 1.3.0 업그레이드합니다. hello 스크립트 hello 새 응용 프로그램 패키지 toohello 클러스터 이미지 저장소에 복사, hello 응용 프로그램 유형을 등록, 모니터링 되는 업그레이드를 시작 및 hello 업그레이드 완료 되거나 롤백합니다 때까지 계속 hello 업그레이드 상태를 확인 합니다. 필요에 따라 hello 매개 변수를 사용자 지정 합니다. 

필요한 경우 hello로 hello 서비스 패브릭 PowerShell 모듈을 설치 [서비스 패브릭 SDK](../service-fabric-get-started.md)합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Hello 서비스 패브릭 클러스터의 모든 hello 응용 프로그램 또는 특정 응용 프로그램을 가져옵니다.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | 서비스 패브릭 응용 프로그램 업그레이드의 hello 상태를 가져옵니다. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Hello 서비스 패브릭 클러스터에 등록 하는 hello 서비스 패브릭 응용 프로그램 종류를 가져옵니다. |
| [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Service Fabric 응용 프로그램 유형을 등록 취소합니다.  |
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | 서비스 패브릭 응용 프로그램 패키지 toohello 이미지 저장소를 복사 합니다.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Service Fabric 응용 프로그램 유형을 등록합니다. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | 서비스 패브릭 응용 프로그램 toohello 지정 된 응용 프로그램 종류 버전을 업그레이드합니다. |


## <a name="next-steps"></a>다음 단계

Hello 서비스 패브릭 PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/service-fabric/?view=azureservicefabricps)합니다.

Azure Service Fabric에 대 한 추가 Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.
