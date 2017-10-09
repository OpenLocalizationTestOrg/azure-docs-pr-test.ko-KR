---
title: "PowerShell 스크립트 샘플-aaaAzure tooa 클러스터 응용 프로그램 배포 | Microsoft Docs"
description: "Azure PowerShell 스크립트 예제-응용 프로그램 tooa 서비스 패브릭 클러스터를 배포 합니다."
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>응용 프로그램 tooa 서비스 패브릭 클러스터를 배포 합니다.

이 샘플 스크립트 응용 프로그램 패키지 tooa 클러스터 이미지 저장소에 복사 하 고 hello 클러스터에 hello 응용 프로그램 종류를 등록 한 hello 응용 프로그램 종류에서 응용 프로그램 인스턴스를 만듭니다.  기본 서비스 hello 대상 응용 프로그램 종류의 hello 응용 프로그램 매니페스트에서 정의 된 경우에 해당 서비스이 이번에 생성 됩니다. 필요에 따라 hello 매개 변수를 사용자 지정 합니다. 

필요한 경우 hello로 hello 서비스 패브릭 PowerShell 모듈을 설치 [서비스 패브릭 SDK](../service-fabric-get-started.md)합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 스크립트 예제를 실행 한 후에 스크립트 hello [응용 프로그램을 제거](service-fabric-powershell-remove-application.md) 사용된 tooremove hello 응용 프로그램 인스턴스 수, hello 응용 프로그램 종류의 등록을 취소 및 hello 이미지 저장소에서 hello 응용 프로그램 패키지를 삭제할 수 있습니다.

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | 응용 프로그램 패키지 toohello 클러스터 이미지 저장소에 복사 합니다.  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| 응용 프로그램 유형 및 버전 hello 클러스터에 등록합니다. |
|[New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| 등록된 응용 프로그램 유형에서 응용 프로그램을 만듭니다. |

## <a name="next-steps"></a>다음 단계

Hello 서비스 패브릭 PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/service-fabric/?view=azureservicefabricps)합니다.

Azure Service Fabric에 대 한 추가 Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.
