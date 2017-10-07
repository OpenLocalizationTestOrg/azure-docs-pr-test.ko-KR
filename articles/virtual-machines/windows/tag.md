---
title: "Azure에서 Windows VM 리소스 aaaHow tootag | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 만든 Windows 가상 컴퓨터 태그를 지정 하는 방법에 대 한 자세한 내용은"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a>어떻게 tootag Azure에서 Windows 가상 컴퓨터
이 문서에서는 다양 한 방법 tootag hello 리소스 관리자 배포 모델을 통해 Azure에서 Windows 가상 컴퓨터를 설명 합니다. 태그는 리소스 또는 리소스 그룹에 직접 배치할 수 있는 사용자 정의 키/값 쌍입니다. 현재 azure 리소스 및 리소스 그룹 당 too15 태그를 지원합니다. 태그 생성 hello 시 리소스에 배치 될 수 있습니다 또는 tooan 기존 리소스를 추가 합니다. Hello 리소스 관리자 배포 모델만을 통해 생성 된 리소스에 대 한 태그는 지원 note 하십시오. Linux 가상 컴퓨터를 tootag 참조 [어떻게 tootag Azure에서 Linux 가상 컴퓨터를](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>PowerShell을 사용한 태그 지정
먼저 tooset, toocreate, 추가 및 PowerShell 통해 태그를 삭제 하면 [PowerShell 환경에서 Azure 리소스 관리자와][PowerShell environment with Azure Resource Manager]합니다. Hello 설치를 완료 한 후에 계산, 네트워크 및 저장소 리소스를 만들 때 또는 PowerShell을 통해 hello 리소스 만들어진 후에 태그를 배치할 수 있습니다. 이 문서에서는 가상 컴퓨터에 배치된 태그 보기/편집을 중점적으로 살펴봅니다.

첫째, hello 통해 tooa 가상 컴퓨터를 이동 `Get-AzureRmVM` cmdlet.

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

가상 컴퓨터에 이미 태그가 포함 된 다음 리소스에 대해 모든 hello 태그가 표시 됩니다.

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

PowerShell 통해 tooadd 태그를 원하는 경우 hello를 사용할 수 있습니다 `Set-AzureRmResource` 명령입니다. PowerShell을 통해 태그를 업데이트하는 경우 태그가 전체적으로 업데이트됩니다. 태그를 이미가지고 있는 하나의 태그 tooa 리소스를 추가 하는 경우 나오는 tooinclude toobe hello 리소스에 배치 하려는 모든 hello 태그입니다. 다음은 tooadd 추가 PowerShell Cmdlet을 통해 tooa 리소스 태그를 삽입 방법의 예입니다.

이 첫 번째 cmdlet 설정에 배치 하는 hello 태그를 모두 *MyTestVM* toohello *$tags* hello를 사용 하 여 변수, `Get-AzureRmResource` 및 `Tags` 속성입니다.

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

두 번째 명령은 hello 변수가 hello에 대 한 hello 태그를 표시 합니다.

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

hello 세 번째 명령은 추가 추가 태그 toohello *$tags* 변수입니다. Hello hello 사용  **+=**  tooappend hello 새 키/값 쌍 toohello *$tags* 목록입니다.

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

hello에 정의 된 hello 태그를 모두 설정 하는 hello 네 번째 명령은 *$tags* 변수 toohello 리소스를 제공 합니다. 이 경우 MyTestVM입니다.

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

다섯 번째 명령은 hello hello 리소스에 hello 태그를 모두 표시합니다. 볼 수 있듯이 *위치* 이제 포함 된 태그가으로 정의 되어 *MyLocation* hello 값으로.

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

에 대해 더 알아봅니다 toolearn hello를 확인해 보세요 PowerShell을 통해 태그 지정 [Azure 리소스 Cmdlet][Azure Resource Cmdlets]합니다.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>다음 단계
* Azure 리소스 태그에 대 한 자세한 toolearn 참조 [Azure 리소스 관리자 개요] [ Azure Resource Manager Overview] 및 [tooorganize 태그를 사용 하 여 Azure 리소스] [ Using Tags tooorganize your Azure Resources].
* toosee 태그 수 Azure 리소스의 사용을 관리 하는 방법 참조 [Azure 청구서 이해] [ Understanding your Azure Bill] 및 [Microsoft Azure 리소스 소비량에 대 한 이해력] [Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
