---
title: "클래식 Azure PowerShell aaaCreate 인터넷 연결 부하 분산 장치-| Microsoft Docs"
description: "인터넷 연결 toocreate PowerShell을 사용 하는 클래식 모드에서 분산 장치를 로드 하는 방법에 대해 알아봅니다"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>PowerShell에서 인터넷 연결 부하 분산 장치(클래식) 만들기 시작

> [!div class="op_single_selector"]
> * [Azure 클래식 포털](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure 클라우드 서비스](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Azure 리소스를 사용 하기 전에 Azure에 현재 두 가지 배포 모델에 중요 한 toounderstand: Azure 리소스 관리자 및 기본 합니다. Azure 리소스로 작업하기 전에 [배포 모델 및 도구](../azure-classic-rm.md) 를 이해해야 합니다. 이 문서의 hello 위쪽 hello 탭을 클릭 하 여 다양 한 도구에 대 한 hello 설명서를 볼 수 있습니다. 이 문서에서는 hello 클래식 배포 모델에 설명 합니다. 수도 있습니다 [toocreate 인터넷 연결 로드 분산 장치는 Azure 리소스 관리자를 사용 하는 방법에 대해 알아봅니다](load-balancer-get-started-internet-arm-ps.md)합니다.

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>PowerShell을 사용하여 부하 분산 장치 설정

아래의 hello 단계를 수행 하는 powershell을 사용 하 여 부하 분산 장치를 tooset:

1. Azure PowerShell을 처음 사용 하는 경우 참조 [어떻게 tooInstall 및 Azure PowerShell 구성](/powershell/azure/overview) 모든 hello 방식으로 toohello toosign를 Azure로 끝나고 구독을 선택 하는 hello 지침을 따릅니다.
2. 가상 컴퓨터를 만든 후 PowerShell cmdlet tooadd tooa 부하 분산 장치 가상 컴퓨터를 사용할 수 있습니다 hello 내에서 동일한 클라우드 서비스입니다.

Hello 부하 분산 장치 집합 이라는 toocloud "webfarm" 서비스 "mytestcloud" (또는 myctestcloud.cloudapp.net) hello에 대 한 hello 끝점 부하 분산 장치 toovirtual 추가 컴퓨터 추가한 다음 예제에서는 이름이 "w e b 1" 및 "web2"입니다. hello 부하 분산 장치 포트 80에서 네트워크 트래픽을 받아 hello 로컬 끝점 (이 경우 포트 80)에 정의 된 hello 가상 컴퓨터 간에 부하를 분산 시키고 TCP를 사용 합니다.

### <a name="step-1"></a>1단계

Web1"hello 첫 번째 VM"에 대 한 부하 분산 된 끝점 만들기

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>2단계

Hello 두 번째 VM "web2" hello를 사용 하 여 동일한 부하 분산 집합 이름이 다른 끝점 만들기

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>부하 분산 장치에서 가상 컴퓨터 제거

제거 AzureEndpoint tooremove hello 부하 분산 장치에서 가상 컴퓨터 끝점을 사용할 수 있습니다.

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>다음 단계

[내부 부하 분산 장치를 시작](load-balancer-get-started-ilb-classic-ps.md)하고 특정 부하 분산 장치 네트워크 트래픽 동작에 대한 [배포 모드](load-balancer-distribution-mode.md) 유형을 구성할 수도 있습니다.

경우 응용 프로그램 서버 부하 분산 장치 뒤에 대 한 연결 유지 tookeep 연결에 필요한를 이해할 수 있습니다 더에 대 한 [부하 분산 장치에 대 한 TCP 시간 제한 설정을 유휴](load-balancer-tcp-idle-timeout.md)합니다. 유휴 연결 동작에 대 한 toolearn Azure 부하 분산 장치를 사용 하는 경우 도움이 됩니다.
