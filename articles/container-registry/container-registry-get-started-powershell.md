---
title: "컨테이너 레지스트리 리포지토리 aaaAzure | Microsoft Docs"
description: "어떻게 Docker 이미지에 대 한 toouse Azure 컨테이너 레지스트리 리포지토리"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Hello Azure PowerShell을 사용 하 여 개인 Docker 컨테이너 등록 만들기
명령을 사용 하 여 [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate 컨테이너 레지스트리 및 Windows 컴퓨터에서 해당 설정을 관리 합니다. 또한 생성 하 고 컨테이너 레지스트리에 hello를 사용 하 여 관리 수 [Azure 포털](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), 또는 프로그래밍 방식으로 컨테이너 레지스트리 hello [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376)합니다.


* 배경 및 개념에 대 한 참조 [hello 개요](container-registry-intro.md)
* 지원되는 cmdlet의 전체 목록은 [Azure Container Registry 관리 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/)을 참조하세요.


## <a name="prerequisites"></a>필수 조건
* **Azure PowerShell**: tooinstall Azure PowerShell을 시작 하 고 hello를 참조 하십시오 [설치 지침](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)합니다. 실행 하 여 Azure 구독 tooyour 로그인 `Login-AzureRMAccount`합니다. 자세한 내용은 [Azure PowerShell 시작](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep)을 참조하세요.
* **리소스 그룹**: 컨테이너 레지스트리를 만들기 전에 [리소스 그룹](../azure-resource-manager/resource-group-overview.md#resource-groups)을 만들거나 기존 리소스 그룹을 사용합니다. 컨테이너 레지스트리 서비스가 hello는 위치에는 hello 리소스 그룹이 있는지 확인 [사용 가능한](https://azure.microsoft.com/regions/services/)합니다. Azure PowerShell을 사용 하 여 리소스 그룹 toocreate 참조 [PowerShell 참조 hello](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group)합니다.
* **저장소 계정** (선택 사항): 표준 Azure 만들기 [저장소 계정](../storage/common/storage-introduction.md) tooback hello 컨테이너 레지스트리 hello에서 동일한 위치입니다. 사용 하 여 레지스트리를 만들 때 저장소 계정을 지정 하지 않으면 `New-AzureRMContainerRegistry`, 솔루션이 hello 명령을 생성 합니다. PowerShell을 사용 하 여 계정, 참조이 toocreate 저장소 [PowerShell 참조 hello](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount)합니다. Premium Storage는 현재 지원되지 않습니다.
* **서비스 주체**(선택 사항): PowerShell을 사용하여 레지스트리를 만들 때 기본적으로 액세스가 가능하도록 설정되지 않습니다. 필요에 따라 수는 기존 Azure Active Directory 서비스 보안 주체 tooa 레지스트리 할당 또는 만들고 새 할당 합니다. 또는 hello 레지스트리 관리자 사용자 계정을 활성화할 수 있습니다. 이 문서의 뒷부분에 나오는 hello 섹션을 참조 하십시오. 레지스트리 액세스 하는 방법에 대 한 자세한 내용은 참조 [hello 컨테이너 레지스트리로 인증](container-registry-authentication.md)합니다.

## <a name="create-a-container-registry"></a>컨테이너 레지스트리 만들기
Hello 실행 `New-AzureRMContainerRegistry` 명령 toocreate 컨테이너 레지스트리 합니다.

> [!TIP]
> 레지스트리를 만들 때 전역적으로 고유한 최상위 도메인 이름(문자 및 숫자만 포함)을 지정합니다. hello 예에서 hello 레지스트리 이름이 `MyRegistry`, 되지만 대신 사용자 고유의의 고유 이름입니다.
>
>

다음 명령을 사용 하 여 최소한의 매개 변수 toocreate 컨테이너 레지스트리 hello hello `MyRegistry` hello 리소스 그룹에 `MyResourceGroup` hello 미국 중남부 위치에서에서:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` 는 선택 사항입니다. 하지 않은 경우, 지정 된 저장소 계정을 hello 레지스트리 이름으로 된 이름을 만들어지고 타임 스탬프 hello에서 리소스 그룹을 지정 합니다.

## <a name="assign-a-service-principal"></a>서비스 주체 할당
PowerShell 명령 tooassign Azure Active Directory를 사용 하 여 [서비스 사용자](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa 레지스트리 합니다. hello 이러한 예에서 서비스 사용자는 할당 hello 소유자 역할 되지만 할당할 수 있습니다 [다른 역할](../active-directory/role-based-access-control-configure.md) 들어 있습니다.

### <a name="create-a-service-principal"></a>서비스 주체 만들기
다음 명령을 hello, 새 서비스 사용자를 만듭니다. Hello로 강력한 암호를 지정 `-Password` 매개 변수입니다.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>새로운 서비스 주체 또는 기존 서비스 주체 할당
새 데이터베이스 또는 기존 서비스 보안 주체 tooa 레지스트리를 할당할 수 있습니다. tooassign 것 소유자 역할 액세스 toohello 레지스트리, 다음 예제 명령은 비슷한 toohello 실행:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Hello 서비스 사용자를 사용 하 여 toohello 레지스트리에 로그인
Hello 서비스 보안 주체 toohello 레지스트리를 할당 한 후 다음 명령을 hello를 사용 하 여 로그인 할 수 있습니다.

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>관리자 자격 증명 관리
관리자 계정은 각 컨테이너 레지스트리에 대해 자동으로 생성되며 기본적으로 비활성화됩니다. hello 다음 예제에서는 PowerShell 명령을 toomanage hello 컨테이너 레지스트리에 대 한 자격 증명 관리

### <a name="obtain-admin-user-credentials"></a>관리자 사용자 자격 증명 가져오기
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>기존 레지스트리에 대한 관리자 사용자 활성화
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>기존 레지스트리에 대한 관리자 사용자 비활성화
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>다음 단계
* [Hello Docker CLI를 사용 하 여 첫 번째 이미지 강제](container-registry-get-started-docker-cli.md)
