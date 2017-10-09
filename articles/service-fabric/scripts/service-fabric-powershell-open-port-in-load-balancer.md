---
title: "PowerShell 스크립트 샘플-부하 분산 장치에서 응용 프로그램 열기 포트 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-서비스 패브릭 응용 프로그램에 대 한 hello Azure 부하 분산 장치에서 포트 열기."
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
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a>Hello Azure 부하 분산 장치에 응용 프로그램 포트 열기

Azure에서 실행 되는 서비스 패브릭 응용 프로그램은 hello Azure 부하 분산 장치 뒤에 있습니다. 이 샘플 스크립트는 Service Fabric 응용 프로그램이 외부 클라이언트와 통신할 수 있도록 Azure Load Balancer에서 포트를 엽니다. 필요에 따라 hello 매개 변수를 사용자 지정 합니다. 

필요한 경우 hello로 hello 서비스 패브릭 PowerShell 모듈을 설치 [서비스 패브릭 SDK](../service-fabric-get-started.md)합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.

| 명령 | 참고 사항 |
|---|---|
| [Get-AzureRmResource](/powershell/module/azurerm.resources/get-azurermresource) | Azure 리소스를 가져옵니다.  |
| [Get-AzureRmLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer) | Hello Azure 부하 분산 장치를 가져옵니다. |
| [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | 프로브 구성 tooa 부하 분산 장치를 추가합니다.|
| [Get-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | Load Balancer에 대한 프로브 구성을 가져옵니다. |
| [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | 규칙 구성 tooa 부하 분산 장치를 추가합니다. |
| [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) | 집합에는 부하 분산 장치에 대 한 목표 상태를 hello 합니다. |

## <a name="next-steps"></a>다음 단계

Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.

Azure Service Fabric에 대 한 추가 Powershell 샘플 hello에서 확인할 수 있습니다 [Azure PowerShell 샘플](../service-fabric-powershell-samples.md)합니다.
