---
title: "이벤트 허브를 사용 하 여 Azure 키 자격 증명 모음에서 aaaIntegrate 로그 | Microsoft Docs"
description: "Azure 로그 통합을 사용 하 여 사용 가능한 tooa SIEM를 기록 하는 hello 필요한 단계 toomake 주요 자격 증명 모음을 제공 하는 자습서"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Azure 로그 통합 자습서: Event Hubs를 사용하여 Azure Key Vault 이벤트 처리

Azure 로그 통합 tooretrieve 기록 된 이벤트를 사용할 수 있으며 사용 가능한 tooyour 보안 정보 및 이벤트 (SIEM) 관리 시스템을 확인 하십시오. 이 자습서에서는 Azure 로그 통합 Azure 이벤트 허브에서 구입한 tooprocess 사용 되는 로그를 수 있는 방법의 예를 보여 줍니다.
 
이 자습서 tooget 어떻게 하 여 다음 작업을 Azure 로그 통합 및 이벤트 허브 hello 예제 단계를 숙지 하 고 각 단계 hello 솔루션을 지원 하는 방법을 이해를 사용 합니다. 작업을 수행할 수 있는 다음 배운 여기 toocreate 단계 toosupport 고유한 회사의 고유한 요구 사항입니다.

>[!WARNING]
hello 단계와이 자습서에서는 명령을 복사 하 고 붙여넣을 의도 한 toobe 않습니다. 예제일 뿐입니다. 라이브 환경에서 "있는 그대로" hello PowerShell 명령을 사용 하지 마십시오. 이러한 명령은 고유 환경에 맞게 사용자 지정해야 합니다.


이 자습서에서는 Azure 키 자격 증명 모음 활동 기록된 tooan 이벤트 허브를 수행 하 고 JSON 파일 tooyour SIEM 시스템으로 사용할 수 있도록 hello 과정을 안내 합니다. 그런 다음 SIEM 시스템 tooprocess hello JSON 파일을 구성할 수 있습니다.

>[!NOTE]
>이 자습서의 단계 hello 대부분 키 자격 증명 모음, 저장소 계정 및 이벤트 허브 구성 작업이 포함 됩니다. hello 특정 Azure 로그 통합 단계는이 자습서의 hello 끝에서 있습니다. 프로덕션 환경에서 다음 단계를 수행하지 마세요. 랩 환경 전용으로 작성되었습니다. 프로덕션 환경에서 사용 하기 전에 hello 단계를 사용자 지정 해야 합니다.

정보는 각 단계 hello 용도 이해 hello 방법 사용 하면 함께 제공 합니다. 링크 tooother 문서에서 특정 항목에 대 많은 정보를 제공 합니다.

이 자습서를 언급 하는 hello 서비스에 대 한 자세한 내용은 다음을 참조 합니다. 

- [Azure Key Vault](../key-vault/key-vault-whatis.md)
- [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Azure 로그 통합](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>초기 설치

이 문서의 hello 단계를 완료할 수 있습니다, 전에 hello 다음을 해야 합니다.

1. Azure 구독 및 관리자 권한이 있는 해당 구독의 계정. 구독이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.
 
2. 액세스 toohello 시스템과 Azure 로그 통합 설치를 위한 hello 요구 사항을 충족 하는 인터넷 합니다. hello 시스템 클라우드 서비스에 있을 수 있습니다 또는 온-프레미스를 호스트 합니다.

3. [Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324) 설치됨. tooinstall 하기:

   a. 2 단계에서 언급 한 원격 데스크톱 tooconnect toohello 시스템을 사용 합니다.   
   b. Hello Azure 로그 통합 설치 관리자 toohello 시스템에 복사 합니다. 있습니다 수 [hello 설치 파일을 다운로드](https://www.microsoft.com/download/details.aspx?id=53324)합니다.   
   c. Hello 설치 관리자를 시작 하 고 hello Microsoft 소프트웨어 사용 조건에 동의 합니다.   
   d. 원격 분석 정보를 제공 하는 경우에 hello 확인란 선택 된 상태로 둡니다. 사용 현황 정보 tooMicrosoft을 하지 보내는 대신 것 hello 확인란의 선택을 취소 합니다.
   
   Azure 로그 통합에 대 한 자세한 내용은 방법과 tooinstall, 참조 [Azure 진단 로깅 및 Windows 이벤트 전달을 사용 하 여 Azure 로그 통합](security-azure-log-integration-get-started.md)합니다.

4. hello 최신 PowerShell 버전입니다.
 
   Windows Server 2016이 설치되어 있는 경우 PowerShell 5.0 이상이 설치되어 있는 것입니다. 다른 버전의 Windows Server를 사용 중인 경우 이전 버전의 PowerShell이 설치되어 있을 수 있습니다. 입력 하 여 hello 버전을 확인 하면 ```get-host``` PowerShell 창에서. PowerShell 5.0이 설치되어 있지 않으면 [다운로드](https://www.microsoft.com/download/details.aspx?id=50395)할 수 있습니다.

   이상의 후 PowerShell 5.0 tooinstall hello 최신 버전을 계속 진행할 수 있습니다.
   
   a. PowerShell 창에서 입력 hello ```Install-Module Azure``` 명령입니다. Hello 설치 단계를 완료 합니다.    
   b. Hello 입력 ```Install-Module AzureRM``` 명령입니다. Hello 설치 단계를 완료 합니다.

   자세한 내용은 [Azure PowerShell 설치](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0)를 참조하세요.


## <a name="create-supporting-infrastructure-elements"></a>지원 인프라 요소 만들기

1. 관리자 PowerShell 창을 열고 다음 너무 이동**C:\Program Files\Microsoft Azure 로그 통합**합니다.
2. LoadAzLogModule.ps1 hello 스크립트를 실행 하 여 hello AzLog cmdlet을 가져옵니다. Hello 입력 `.\LoadAzLogModule.ps1` 명령입니다. (공지 hello "입니다. \" 해당 명령에서.) 다음과 유사한 결과가 표시됩니다.</br>

   ![로드된 모듈 목록](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Hello 입력 `Login-AzureRmAccount` 명령입니다. Hello 로그인 창에서이 자습서에 사용할 hello 구독에 대 한 hello 자격 증명 정보를 입력 합니다.

   >[!NOTE]
   >인 경우 hello tooAzure에서이 컴퓨터에 로그인 하는 처음으로 Microsoft toocollect PowerShell 사용 현황 데이터를 허용 하는 방법에 대 한 메시지가 표시 됩니다. 사용 되는 Azure PowerShell tooimprove 수 있으므로이 데이터 컬렉션을 사용 하는 것이 좋습니다.

4. 인증을 완료 한 후 로그인 및 hello 스크린 샷 뒤의 hello 정보를 참조 합니다. Hello 구독 ID 및 구독 이름을 기록해, toocomplete 나중 단계 이므로 해야 합니다.

   ![PowerShell 창](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Toostore 값 나중에 사용 되는 변수를 만듭니다. 위의 PowerShell 삼각형 hello을 각각 입력 합니다. 사용자 환경 tooadjust hello 값 toomatch를 할 수 있습니다.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(구독 이름은 다를 수 있습니다. 볼 수 있습니다 것 hello 이전 명령의 hello 출력의 일부로.)
    - ```$location = 'West US'```(이 변수는 사용 되는 toopass hello 위치 리소스를 만들 이어야 합니다. 변경할 수 있습니다이 변수 toobe 임의의 위치를 선택 합니다.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(아무 것도 hello 이름이 될 수 있지만 소문자와 숫자만 포함 되어야 합니다.)
    - ``` $storageName = $name```(이 변수는 hello 저장소 계정 이름에 대해 사용할 수 됩니다.)
    - ```$rgname = $name ```(이 변수는 hello 리소스 그룹 이름에 사용할 수 됩니다.)
    - ``` $eventHubNameSpaceName = $name```(Hello 이벤트 허브 네임 스페이스의 hello 이름입니다.)
6. Hello 구독으로 작업을 지정 합니다.
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. 리소스 그룹 만들기:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   입력 하는 경우 `$rg` 유사한 toothis 스크린 샷 출력을이 시점에서 표시 됩니다.

   ![리소스 그룹 생성 후 출력](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. 상태 정보를 사용 하는 tookeep 추적 수 있는 저장소 계정을 만듭니다.
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Hello 이벤트 허브 네임 스페이스를 만듭니다. 이 필수 toocreate 이벤트 허브입니다.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Hello insights 공급자와 함께 사용할 hello 규칙 ID 가져오기:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. 가능한 모든 Azure 위치를 가져오고 이후 단계에서 사용할 수 있는 hello 이름 tooa 변수를 추가 합니다.
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    입력 하는 경우 `$locations` 이 시점에서 hello AzureRmLocation Get에서 반환 되는 추가 정보 없는 hello 위치 이름을 표시 합니다.
12. Azure Resource Manager 로그 프로필을 만듭니다. 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Hello Azure 로그 프로필에 대 한 자세한 내용은 참조 [hello Azure 활동 로그 간략하게](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)합니다.

> [!NOTE]
> 로그 프로필 toocreate 려 할 때 오류 메시지가 표시 될 수 있습니다. 그런 다음 Get AzureRmLogProfile 및 제거 AzureRmLogProfile hello 설명서를 검토할 수 있습니다. Get AzureRmLogProfile를 실행 하면 hello 로그 프로필에 대 한 정보가 표시 됩니다. Hello를 입력 하 여 hello 기존 로그 프로필을 삭제할 수 있습니다 ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` 명령입니다.
>
>![Resource Manager 프로필 오류](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>키 자격 증명 모음 만들기

1. Hello 주요 자격 증명 모음을 만듭니다.

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Hello 주요 자격 증명 모음에 대 한 로깅을 구성 합니다.

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>로그 작업 생성

요청 toobe tooKey 자격 증명 모음 toogenerate 로그 작업을 전송 해야 합니다. 키 생성, 암호 저장 또는 Key Vault에서 암호 읽기 등의 작업은 로그 항목을 만듭니다.

1. Hello 현재 저장소 키를 표시 합니다.
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. 새로운 **key2**를 생성합니다.
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Hello 키를 다시 표시 하 고 있는지 **key2** 다른 값을 보유 합니다.
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. 설정 및 비밀 toogenerate 추가 로그 항목을 읽고 있습니다.
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![반환된 암호](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Azure 로그 통합 구성

모든 hello 필수 요소 toohave 주요 자격 증명 모음 로깅 tooan 이벤트 허브를 구성 했으므로 tooconfigure Azure 로그 통합 해야 합니다.

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

각 이벤트 허브에 대 한 hello AzLog 명령을 실행 합니다.

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

1 분 정도 지난 hello 마지막 두 명령은 실행 한 후 생성 되는 JSON 파일을 볼 수 있습니다. Hello 디렉터리를 모니터링 하 여 되는지 확인할 수 있습니다 **C:\users\AzLog\EventHubJson**합니다.

## <a name="next-steps"></a>다음 단계

- [Azure 로그 통합 FAQ](security-azure-log-integration-faq.md)
- [Azure 로그 통합 시작](security-azure-log-integration-get-started.md)
- [Azure 리소스의 로그를 SIEM 시스템에 통합](security-azure-log-integration-overview.md)
