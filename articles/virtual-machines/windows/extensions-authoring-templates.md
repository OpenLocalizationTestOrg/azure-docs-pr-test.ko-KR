---
title: "Windows VM 확장과 함께 aaaAuthoring 템플릿 | Microsoft Docs"
description: "Windows VM 확장을 사용하여 Azure Resource Manager 템플릿 작성에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a>Windows VM 확장을 사용하여 Azure Resource Manager 템플릿 작성
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

Azure PowerShell에서 hello 다음 Azure PowerShell cmdlet을 실행 합니다.

      Get-AzureVMAvailableExtension


이 cmdlet 반환 hello 게시자 이름, 확장 이름 및 버전을 다음과 같이 합니다.

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

이 세 가지 속성을 너무 매핑할 "publisher", "type" 및 "typeHandlerVersion" 템플릿 조각 위에 hello에 각각 있습니다.

> [!NOTE]
> 패턴은 항상 권장된 toouse hello 최신 확장 버전 tooget hello 가장 업데이트 기능입니다.
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>확장 구성 매개 변수 hello에 대 한 hello 스키마를 식별합니다.
hello와 확장 템플릿을 제작 하 고 다음 단계는 구성 매개 변수를 제공 하는 데 tooidentify hello 형식입니다. 각 확장은 자체 매개 변수 집합을 지원합니다.

Windows 확장에 대 한 샘플 구성에서 toolook 참조 [Windows 확장 샘플](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

Toohello tooget VM 확장 작업이 모두 완료 된 템플릿이 다음을 참조 하십시오.

[Windows VM의 사용자 지정 스크립트 확장](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

Hello 서식 파일을 작성 한 후 Azure PowerShell을 사용 하 여 배포할 수 있습니다.

