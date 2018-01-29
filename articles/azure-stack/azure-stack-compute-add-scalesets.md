---
title: "가상 컴퓨터 크기 집합에서에서 사용할 수 있도록 Azure 스택"
description: "클라우드 관리자가 Azure 스택 마켓플레이스로 가상 컴퓨터 크기를 추가할 수는 방법에 대해 알아봅니다"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 9/25/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 31aeb963bdf4fd32712bc6f29f64060ec1c77cb8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a>가상 컴퓨터 크기 집합에서에서 사용할 수 있도록 Azure 스택

*적용 대상: Azure 스택 통합 시스템과 Azure 스택 개발 키트*

가상 컴퓨터 크기 집합에는 Azure 스택 계산 리소스가 됩니다. 배포 하 고 동일한 가상 컴퓨터의 집합을 관리할 사용할 수 있습니다. 모든 가상 컴퓨터와 동일 하 게 구성, 크기 집합의 가상 컴퓨터 프로 비전 미리 필요 하지 않습니다. 큰 계산, 빅 데이터 및 컨테이너 화 된 작업을 대상으로 하는 대규모 서비스를 빌드하는 것이 쉽습니다.

이 항목에서는 Azure 스택 Marketplace에 크기 집합을 사용할 수 있도록 하는 프로세스를 안내 합니다. 이 절차를 완료 한 후 사용자는 해당 구독에 가상 컴퓨터 크기 집합을 추가할 수 있습니다.

Azure 스택에 가상 컴퓨터 크기 집합은 Azure에서 가상 컴퓨터 크기 집합 같습니다. 자세한 내용은 다음 동영상을 참조 하십시오.
* [Mark Russinovich의 Azure 확장 집합 설명](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [Guy Bowerman과 가상 컴퓨터 규모 집합](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

Azure 스택, 가상 컴퓨터 크기 집합에는 자동 크기 조정 지원 하지 않습니다. Azure 스택 포털, 리소스 관리자 템플릿 또는 PowerShell을 사용 하 여 설정 눈금에 더 많은 인스턴스를 추가할 수 있습니다.

## <a name="prerequisites"></a>필수 조건
* **Powershell 및 도구**

   설치 하 고 Azure 스택에 대해 구성 된 PowerShell 및 Azure 스택 도구. 참조 [스택에서 Azure PowerShell을 시작 하 고 실행](azure-stack-powershell-configure-quickstart.md)합니다.

   Azure 스택 도구를 설치한 후 다음 PowerShell 모듈을 가져올 수 있는지 확인 (기준으로 경로. AzureStack 도구 마스터 폴더에 \ComputeAdmin 폴더):

        Import-Module .\AzureStack.ComputeAdmin.psm1

* **운영 체제 이미지**

   Azure 스택 마켓플레이스로 운영 체제 이미지를 추가 하지 않았다면, 참조 [Azure 스택 시장에 Windows Server 2016 VM 이미지를 추가](azure-stack-add-default-image.md)합니다.

   Linux 지원 Ubuntu Server 16.04를 다운로드 하 고 사용 하 여 추가 ```Add-AzsVMImage``` 는 다음 매개 변수: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```합니다.

## <a name="add-the-virtual-machine-scale-set"></a>가상 컴퓨터 크기 집합 추가

사용자 환경에 대해 다음 PowerShell 스크립트를 편집 하 고 가상 컴퓨터 크기 집합 Azure 스택 마켓플레이스로 추가 하도록를 실행 하십시오. 

``$User``관리자 포털을 연결 하는 데 사용할 계정이입니다. 예: serviceadmin@contoso.onmicrosoft.com.

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a>가상 컴퓨터 크기 집합 제거

가상 컴퓨터를 제거 하려면 set 갤러리 항목의 크기를 조정, 다음 PowerShell 명령을 실행 합니다.

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> 갤러리 항목은 즉시 제거할 수 없습니다. 포털을 새로 고치려면 여러 번 시장에서 제거 되기 전에 해야 합니다.


## <a name="next-steps"></a>다음 단계
[Azure 스택 질문과 대답](azure-stack-faq.md)

