---
title: "차이점 및 스택 Azure의에서 가상 컴퓨터에 대 한 고려 사항 | Microsoft Docs"
description: "스택에서 Azure 가상 컴퓨터와 작업 하는 경우의 차이점과 고려 사항에 알아봅니다."
services: azure-stack
documentationcenter: 
author: brenduns
manager: femila
editor: 
ms.assetid: 6613946D-114C-441A-9F74-38E35DF0A7D7
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/17/2018
ms.author: brenduns
ms.openlocfilehash: 6eafa2a5058ef1309cbf50be069ea1bb12f7e5b9
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="considerations-for-virtual-machines-in-azure-stack"></a>Azure 스택의 가상 컴퓨터에 대 한 고려 사항

*적용 대상: Azure 스택 통합 시스템과 Azure 스택 개발 키트*

가상 컴퓨터는 Azure 스택에서 제공 하는 확장 가능한 컴퓨팅 리소스는 요청입니다. 가상 컴퓨터를 사용 하는 경우에 Azure에서 사용할 수 있는 기능 및 Azure 스택 간에 차이가 있습니다 이해 해야 합니다. 이 문서에서는 가상 컴퓨터와 Azure 스택의 해당 기능에 대 한 고유 고려 사항에 대 한 개요를 제공 합니다. Azure 스택와 Azure 간의 대략적인 차이 대 한 자세한 내용은 [고려 사항 키](azure-stack-considerations.md) 문서.

## <a name="cheat-sheet-virtual-machine-differences"></a>치트 시트: 가상 컴퓨터의 차이점

| 기능 | Azure (global) | Azure Stack |
| --- | --- | --- |
| 가상 컴퓨터 이미지 | Azure 마켓플레이스는 가상 컴퓨터를 만드는 데 사용할 수 있는 이미지를 포함 합니다. 참조는 [Azure 마켓플레이스](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) 페이지 Azure 마켓플레이스에서 사용할 수 있는 이미지 목록을 볼 수 있습니다. | 기본적으로 없습니다 이미지 사용할 수 있는 Azure 스택 시장에서. Azure 스택 클라우드 관리자에 게시 하거나 사용자가 사용 전에 Azure 스택 마켓플레이스 이미지를 다운로드 해야 합니다. |
| 가상 머신 크기 | Azure 가상 컴퓨터에 대 한 다양 한 크기를 지원합니다. 에 사용 가능한 크기와 옵션에 대 한 자세한 참조는 [Windows 가상 컴퓨터 크기](../../virtual-machines/virtual-machines-windows-sizes.md) 및 [Linux 가상 컴퓨터 크기](../../virtual-machines/linux/sizes.md) 항목입니다. | Azure 스택 Azure에서 사용할 수 있는 가상 컴퓨터 크기의 하위 집합을 지원 합니다. 지원 되는 크기의 목록을 보려면를 참조는 [가상 컴퓨터 크기](#virtual-machine-sizes) 이 문서의 섹션. |
| 가상 컴퓨터 할당량 | [할당량 한도](../../azure-subscription-service-limits.md#service-specific-limits) Microsoft에서 설정 | 가상 컴퓨터 사용자에 게 제공 하기 전에 Azure 스택 클라우드 관리자가 할당량을 할당 해야 합니다. |
| 가상 머신 확장 |Azure 가상 컴퓨터 확장의 다양 한 지원합니다. 에 사용 가능한 확장에 대 한 자세한 참조는 [가상 컴퓨터 확장 및 기능](../../virtual-machines/windows/extensions-features.md) 문서.| Azure 스택 Azure에서 사용할 수 있는 확장의 하위 집합을 지원 하 고 각 확장의 특정 버전을 보유 합니다. Azure 스택 클라우드 관리자가 사용자에 게 사용할 수 있게 되는 확장을 선택할 수 있습니다. 지원 되는 확장 목록을 보려면를 참조는 [가상 컴퓨터 확장](#virtual-machine-extensions) 이 문서의 섹션. |
| 가상 컴퓨터 네트워크 | 테 넌 트 가상 컴퓨터에 할당 된 공용 IP 주소는 인터넷을 통해 액세스할 수 있습니다.<br><br><br>Azure 가상 컴퓨터의 고정된 DNS 이름 | 테 넌 트 가상 컴퓨터에 할당 된 공용 IP 주소는만 스택 개발 키트 Azure 환경 내에서 액세스할 수 있습니다. 사용자를 통해 Azure 스택 개발 키트를 액세스할 수 있어야 합니다. [RDP](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop) 또는 [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) Azure 스택에 만들어지는 가상 컴퓨터에 연결 합니다.<br><br>특정 Azure 스택 인스턴스 내에서 만든 가상 컴퓨터 클라우드 관리자가 구성 된 값에 따라 DNS 이름이 있습니다. |
| 가상 컴퓨터 저장소 | 지원 [디스크를 관리 합니다.](../../virtual-machines/windows/managed-disks-overview.md) | 관리 되는 디스크는 Azure 스택의 아직 지원 되지 않습니다. |
| API 버전 | Azure는 항상 모든 가상 컴퓨터 기능에 대 한 최신 API 버전을 갖습니다. | Azure 스택 이러한 서비스에 대 한 특정 Azure 서비스 및 특정 API 버전을 지원합니다. 지원 되는 API 버전 목록을 보려면를 참조는 [API 버전](#api-versions) 이 문서의 섹션. |
|가상 컴퓨터 가용성 집합|여러 오류 도메인 (2 또는 3 / 지역당)<br>여러 업데이트 도메인<br>관리 디스크 지원|단일 장애 도메인<br>단일 업데이트 도메인<br>관리 되는 디스크 지원 되지 않습니다|
|가상 머신 크기 집합|자동 크기 조정 지원|자동 크기 조정 지원 되지 않습니다.<br>더 많은 인스턴스 크기 포털, 리소스 관리자 템플릿 또는 PowerShell을 사용 하 여 집합에 추가 합니다.

## <a name="virtual-machine-sizes"></a>가상 머신 크기

Azure 스택 다음 크기를 지원합니다.

| type | 크기 | 지원 되는 크기의 범위 |
| --- | --- | --- |
|범용 가상 컴퓨터 |Basic A|A0 - A4|
|범용 가상 컴퓨터 |표준 A|A0 - A7|
|범용 가상 컴퓨터 |D 시리즈|D1 - D4|
|범용 가상 컴퓨터 |Dv2 시리즈|D1_v2 - D5_v2|
|범용 가상 컴퓨터 |DS 시리즈|DS1 - DS4|
|범용 가상 컴퓨터 |DSv2 시리즈|DS1_v2 - DS5_v2|
|메모리에 최적화|DS 시리즈|DS11 - DS14|
|메모리에 최적화 |DSv2 시리즈|DS11_v2 - DS14_v2|

가상 컴퓨터 크기와 해당 관련된 리소스 수량 Azure 스택와 Azure 간에 일치 됩니다. 예를 들어이 일관성 메모리, 코어 수 및 만들 수 있는 데이터 디스크의 수/크기 걸린 시간이 포함 됩니다. 그러나 Azure 스택에는 동일한 VM 크기의 성능을 특정 Azure 스택 환경의 기본 특성에 따라 달라 집니다.

## <a name="virtual-machine-extensions"></a>가상 머신 확장

 Azure 스택 다음 가상 컴퓨터 확장 버전을 지원합니다.

![VM 확장](media/azure-stack-vm-considerations/vm-extensions.png)

Azure 스택 환경에서 사용할 수 있는 가상 컴퓨터 확장 목록을 가져오려면 다음 PowerShell 스크립트 사용 하세요.

```powershell
Get-AzureRmVmImagePublisher -Location local | `
  Get-AzureRmVMExtensionImageType | `
  Get-AzureRmVMExtensionImage | `
  Select Type, Version | `
  Format-Table -Property * -AutoSize
```

## <a name="api-versions"></a>API 버전

Azure 스택에서 가상 컴퓨터 기능이 다음 API 버전을 지원합니다.

![VM 리소스 종류](media/azure-stack-vm-considerations/vm-resoource-types.png)

Azure 스택 환경에서 사용할 수 있는 가상 컴퓨터 기능에 대 한 API 버전을 가져오려는 다음 PowerShell 스크립트를 사용할 수 있습니다.

```powershell
Get-AzureRmResourceProvider | `
  Select ProviderNamespace -Expand ResourceTypes | `
  Select * -Expand ApiVersions | `
  Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} | `
  where-Object {$_.ProviderNamespace -like “Microsoft.compute”}
```
지원 되는 리소스 종류 및 API 버전 목록을 통해 클라우드 운영자는 새 버전으로 Azure 스택 환경을 업데이트 하는 경우 달라질 수 있습니다.

## <a name="next-steps"></a>다음 단계

[Azure 스택에서 PowerShell을 사용한 Windows 가상 컴퓨터 만들기](azure-stack-quick-create-vm-windows-powershell.md)
