---
title: "aaaPassing tooAzure DSC를 사용 하 여 자격 증명 | Microsoft Docs"
description: "PowerShell 필요한 상태 구성을 사용 하 여 tooAzure 가상 컴퓨터 자격 증명을 안전 하 게 전달에 대 한 개요"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>자격 증명 toohello Azure DSC 확장 처리기를 전달합니다.
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

이 문서에서는 Azure 용 hello 필요한 상태 구성 확장을 설명합니다. hello DSC 확장 처리기에 대 한 개요를 확인할 수 있습니다 [소개 toohello Azure 필요한 상태 구성 확장 처리기](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 

## <a name="passing-in-credentials"></a>자격 증명 전달
Hello 구성 프로세스의 일부로 tooset 해야 사용자 계정을 서비스에 액세스 하거나 사용자 컨텍스트에서 프로그램을 설치 합니다. toodo 이러한 것 들 tooprovide 자격 증명이 필요 합니다. 

자격 증명의 hello 구성에 전달 되며 안전 하 게 MOF 파일에 저장 된 매개 변수가 있는 구성을 DSC 수 있습니다. Azure 확장 처리기 hello 인증서의 자동 관리를 제공 하 여 자격 증명 관리를 간소화 합니다. 

Hello hello 지정한 암호로 로컬 사용자 계정을 만들어 DSC 구성 스크립트를 다음을 고려 합니다.

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

중요 한 tooinclude는 *노드 localhost* hello 구성의 일부분으로 합니다. 이 문은 누락 되 면 hello 다음 단계가 작동 하지 않습니다 대로 hello 확장 처리기는 특히 hello 노드 localhost 문에 대 한 검색 합니다. 것도 중요 tooinclude hello 형식 캐스팅 *[PsCredential]*와 마찬가지로이 특정 형식 hello 확장 tooencrypt hello 자격 증명을 트리거합니다. 

이 스크립트 tooblob 저장소 게시:

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Hello Azure DSC 확장을 설정 하 고 hello 자격 증명을 제공 합니다.

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>자격 증명의 보안을 유지하는 방법
이 코드를 실행하면 자격 증명을 묻는 메시지가 나타납니다. 자격 증명이 제공되면 메모리에 잠시 저장됩니다. 으로 게시 되는 경우 `Set-AzureVmDscExtension` cmdlet 것 HTTPS toohello VM 통해 전송 된, 여기서 Azure 저장소는 hello 로컬 VM 인증서를 사용 하 여 디스크에서 암호화 합니다. 메모리와 다시 암호화 toopass에 간단 하 게 해독 된 다음 해당 tooDSC 합니다.

이 동작은 다른 [hello 확장 처리기 없이 보안 구성을 사용 하 여](https://msdn.microsoft.com/powershell/dsc/securemof)합니다. Azure 환경 hello 인증서를 통해 안전 하 게 방식으로 tootransmit 구성 데이터를 제공합니다. Hello DSC 확장 처리기를 사용 하는 경우 없습니다 필요 tooprovide $CertificatePath 또는 $CertificateID 있습니다 / ConfigurationData $Thumbprint 항목입니다.

## <a name="next-steps"></a>다음 단계
Hello Azure DSC 확장 처리기에 대 한 자세한 내용은 참조 하십시오. [소개 toohello Azure 필요한 상태 구성 확장 처리기](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 

Hello 검사 [hello DSC 확장에 대 한 Azure Resource Manager 템플릿](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

PowerShell DSC에 대 한 자세한 내용은 [hello PowerShell 설명서 센터를 방문](https://msdn.microsoft.com/powershell/dsc/overview)합니다. 

PowerShell DSC로 관리할 수 있는 toofind 추가 기능 [hello PowerShell 갤러리 찾아보기](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) 자세한 DSC 리소스에 대 한 합니다.

