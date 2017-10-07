---
title: "Windows 가상 컴퓨터에 대해 aaaAbout 이미지 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터와 함께 이미지를 사용하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 66ff3fab-8e7f-4dff-b8da-ab1c9c9c9af8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: cynthn
ms.openlocfilehash: c7cfa1d018a5e99d5b68f559ec9ae1f14e4dec8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-images-for-windows-virtual-machines"></a>Windows 가상 컴퓨터에 대한 이미지 정보
> [!IMPORTANT]
> Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다. 이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다. 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다. 찾기 및 hello 리소스 관리자 모델에 이미지를 사용 하는 방법에 대 한 내용은 [여기](../../virtual-machines-windows-cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

[!INCLUDE [virtual-machines-common-classic-about-images](../../../../includes/virtual-machines-common-classic-about-images.md)]

## <a name="working-with-images"></a>이미지 작업

Hello Azure PowerShell 모듈 및 hello Azure 포털 toomanage hello 이미지 사용 가능한 tooyour Azure 구독을 사용할 수 있습니다. 정확히 어떤를 쉽게 파악할 수 있도록 hello Azure PowerShell 모듈에 많은 명령 옵션을 제공 toosee 하려고 하거나 수행 합니다. Azure 포털 hello 많은 hello 일상적인 관리 작업에 대 한 GUI를 제공합니다.

다음은 hello Azure PowerShell 모듈을 사용 하는 몇 가지 예입니다.

* **모든 이미지를 가져올**:`Get-AzureVMImage`현재 구독에서 사용할 수 있는 모든 hello 이미지의 목록을 반환 합니다: 이미지와 Azure 또는 파트너에서 제공 하는 것입니다. hello 결과 목록을 클 수 없습니다. 다음 예제에서는 보여 어떻게 hello tooget 짧은 목록입니다.
* **이미지 제품군 가져오기**:`Get-AzureVMImage | select ImageFamily` **ImageFamily** 속성 문자열을 표시하여 이미지 제품군 목록을 가져옵니다.
* **특정 제품군의 모든 이미지 가져오기**: `Get-AzureVMImage | Where-Object {$_.ImageFamily -eq $family}`
* **VM 이미지 찾기**: `Get-AzureVMImage | where {(gm –InputObject $_ -Name DataDiskConfigurations) -ne $null} | Select -Property Label, ImageName` tooVM 이미지에만 적용 됩니다 hello DataDiskConfiguration 속성을 필터링 하 여이 cmdlet이 작동 합니다. 이 예에서는 hello는 출력 tooonly hello 레이블 및 이미지 이름을 필터링 하 고 합니다.
* **일반화된 이미지 저장**: `Save-AzureVMImage –ServiceName "myServiceName" –Name "MyVMtoCapture" –OSState "Generalized" –ImageName "MyVmImage" –ImageLabel "This is my generalized image"`
* **특수화된 이미지 저장**: `Save-AzureVMImage –ServiceName "mySvc2" –Name "MyVMToCapture2" –ImageName "myFirstVMImageSP" –OSState "Specialized" -Verbose`

  > [!TIP]
  > hello OSState 매개 변수가 필요한 toocreate VM 이미지에 대 한 연결 된 데이터 디스크와 hello 운영 체제 디스크를 포함 하는 경우 Hello 매개 변수를 사용 하지 않는 경우 hello cmdlet은 운영 체제 이미지를 만듭니다. hello 이미지를 일반화 하거나 특수화를 다시 사용할 수 있도록 준비 된 운영 체제 디스크 hello 여부에 따라 hello hello 매개 변수 값을 나타냅니다.

* **이미지 삭제**: `Remove-AzureVMImage –ImageName "MyOldVmImage"`

## <a name="next-steps"></a>다음 단계
수도 있습니다 [hello Azure 포털을 사용 하 여 Windows 컴퓨터를 만들](tutorial.md)합니다.
