---
title: "PowerShell 스크립트 샘플-aaaAzure 서비스 패브릭 클러스터 만들기 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - Service Fabric 클러스터 만들기"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a>Service Fabric 클러스터 만들기

이 샘플 스크립트는 Service Fabric 클러스터를 X.509 인증서를 사용하여 보호되는 5노드 클러스터로 만듭니다.  hello 명령은 자체 서명 된 인증서를 만들고 tooa 새 키 자격 증명 모음에 업로드 합니다. hello 인증서 복사한 tooa 로컬 디렉터리 이기도합니다.  집합 hello *-OS* toochoose hello 버전의 Windows 또는 Linux hello 클러스터 노드에서 실행 하는 매개 변수입니다.  필요에 따라 hello 매개 변수를 사용자 지정 합니다.

필요한 경우 설치 명령 hello를 사용 하 여 Azure PowerShell hello 있는 hello [Azure PowerShell 가이드](/powershell/azure/overview) 다음 실행 `Login-AzureRmAccount` toocreate Azure와의 연결 합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a>배포 정리 

Hello 스크립트 예제를 실행 한 후 다음 명령을 hello 사용된 tooremove hello 리소스 그룹, 클러스터 및 관련 된 모든 리소스를 수 있습니다.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [New-AzureRmServiceFabricCluster](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | 새 Service Fabric 클러스터를 만듭니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

Azure Service Fabric에 대 한 추가 Azure Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.
