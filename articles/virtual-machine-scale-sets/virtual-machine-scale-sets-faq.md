---
title: "가상 컴퓨터 크기 aaaAzure 설정 Faq | Microsoft Docs"
description: "가상 컴퓨터 크기 집합에 대 한 질문과 대답 toofrequently를 가져옵니다."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Azure Virtual Machine Scale Sets에 대한 FAQ

Azure에서 설정 하는 toofrequently 가상 컴퓨터 크기에 대 한 질문과 대답을 가져옵니다.

## <a name="autoscale"></a>Autoscale

### <a name="what-are-best-practices-for-azure-autoscale"></a>Azure 자동 크기 조정에 대한 모범 사례는 무엇인가요?

자동 크기 조정에 대한 모범 사례는 [가상 컴퓨터 자동 크기 조정에 대한 모범 사례](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices)를 참조하세요.

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>호스트 기반 메트릭을 사용하는 자동 크기 조정에 대한 메트릭 이름은 어디에서 찾을 수 있나요?

호스트 기반 메트릭을 사용하는 자동 크기 조정에 대한 메트릭 이름은 [Azure Monitor에서 지원되는 메트릭](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/)을 참조하세요.

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Azure Service Bus 토픽과 큐 길이를 기준으로 하는 자동 크기 조정의 예가 있나요?

예. Azure Service Bus 토픽과 큐 길이를 기준으로 하는 자동 크기 조정의 예는 [Azure Monitor 자동 크기 조정 공용 메트릭](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)을 참조하세요.

서비스 버스 큐에 대 한 다음 JSON hello를 사용 합니다.

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

저장소 큐에 대 한 다음 JSON hello를 사용 합니다.

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

예제 값을 리소스 URI(Uniform Resource Identifier)로 바꿉니다.


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>자동 크기 조정을 수행할 때 호스트 기반 메트릭과 진단 확장 중에서 어떤 방식을 사용하는 것이 바람직한가요?

자동 크기 조정 설정에 VM toouse 호스트 수준 메트릭 또는 게스트 운영 체제 기반 메트릭을 만들 수 있습니다.

지원되는 메트릭 목록에 대해서는 [Azure Monitor 자동 크기 조정 공용 메트릭](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics)을 참조하세요. 

가상 컴퓨터 확장 집합의 전체 샘플을 보려면 [가상 컴퓨터 확장 집합에 대해 Resource Manager 템플릿을 사용하여 고급 자동 크기 조정 구성](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets)을 참조하세요. 

hello 샘플 hello 호스트 수준 CPU 메트릭 및 메시지 개수 메트릭을 사용합니다.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>가상 컴퓨터 확장 집합에 대해 경고 규칙을 설정하려면 어떻게 해야 하나요?

PowerShell 또는 Azure CLI를 통해 가상 컴퓨터 확장 집합의 메트릭에 대해 경고를 만들 수 있습니다. 자세한 내용은 [Azure Monitor PowerShell 빠른 시작 샘플](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) 및 [Azure Monitor 플랫폼 간 CLI 빠른 시작 샘플](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts)을 참조하세요.

hello TargetResourceId hello 가상 컴퓨터 크기 집합의 모양은 다음과 같습니다. 

/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname

파일로 선택할 수 있습니다 VM 성능 카운터 메트릭 tooset hello에 대 한 경고입니다. 자세한 내용은 참조 [리소스 관리자 기반 Windows Vm에 대 한 게스트 OS 메트릭을](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) 및 [Linux Vm에 대 한 게스트 OS 메트릭을](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) hello에 [Azure 모니터 자동 크기 조정 공통 메트릭을](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)문서.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>PowerShell을 사용하여 가상 컴퓨터 확장 집합에 대해 자동 크기 조정을 설정하려면 어떻게 하나요?

hello 블로그 게시물을 참조 하는 PowerShell을 사용 하 여 설정 하는 가상 컴퓨터 크기에서 자동 크기 조정을 tooset [tooadd 자동 크기 조정 tooan Azure 가상 컴퓨터 크기 설정 하는 방법을](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/)합니다.




## <a name="certificates"></a>인증서

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>안전 하 게 인증서 toohello VM을 제공지 않습니다는 방법 가상 컴퓨터 크기 조정 설정 toorun 여기서 hello hello 웹 사이트에 대 한 SSL 배송 안전 하 게 인증서 구성에서 웹 사이트를 프로 비전 하는 방법 (hello 공용 인증서 회전 작업 것 수 거의 hello 구성 업데이트 작업와 동일 합니다.) 방법의 예로 해야 toodo이 있습니까? 

toosecurely 배송 인증서 toohello VM, hello 고객의 주요 자격 증명 모음에서 Windows 인증서 저장소에 직접 고객 인증서를 설치할 수 있습니다.

다음 JSON hello를 사용 합니다.

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

hello 코드는 Windows 및 Linux를 지원합니다.

자세한 내용은 [가상 컴퓨터 확장 집합 만들기 또는 업데이트](https://msdn.microsoft.com/library/mt589035.aspx)를 참조하세요.


### <a name="example-of-self-signed-certificate"></a>자체 서명된 인증서 예제

1.  Key Vault에서 자체 서명된 인증서를 만듭니다.

    다음 PowerShell 명령을 사용 하 여 hello:

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    Azure 리소스 관리자 템플릿 hello에 대 한 입력을 hello이 명령 제공 합니다.

    어떻게 toocreate 키 자격 증명 모음에 자체 서명 된 인증서 참조에 대 한 예제 [서비스 패브릭 클러스터 보안 시나리오](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)합니다.

2.  Hello 리소스 관리자 템플릿을 변경 합니다.

    이 속성을 너무 추가**virtualMachineProfile**, hello의 일부분으로 가상 컴퓨터 크기 집합 리소스:

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>Linux 가상 컴퓨터 크기 집합 리소스 관리자 템플릿을 기반에서으로 한 SSH 키 쌍 toouse SSH 인증에 대 한를 지정할 수 있습니까?  

예. REST API에 대 한 hello **osProfile** 비슷한 toohello standard VM REST API입니다. 

템플릿에 **osProfile**을 포함합니다.

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
이 JSON 블록이에 사용 되는 [hello 101-vm-sshkey GitHub 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)합니다.
 
또한 hello OS 프로필에 사용 되 [hello grelayhost.json GitHub 빠른 시작 템플릿](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json)합니다.

자세한 내용은 [가상 컴퓨터 확장 집합 만들기 또는 업데이트](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration)를 참조하세요.
  

### <a name="how-do-i-remove-deprecated-certificates"></a>사용되지 않는 인증서를 제거하려면 어떻게 합니까? 

tooremove 사용 인증서를, hello 자격 증명 모음 인증서 목록에서 hello 이전 인증서 제거 되지 않습니다. Hello 목록에서 컴퓨터에 tooremain 되도록 모든 hello 인증서를 유지 합니다. 모든 Vm에서 hello 인증서를 제거 되지 않습니다. Hello 인증서 toonew hello 가상 컴퓨터 크기 집합에 만들어진 Vm 추가 되지 않습니다. 

기존 Vm에서 tooremove hello 인증서를 인증서 저장소에서에서 사용자 지정 스크립트 확장 toomanually hello 인증서 제거 작성 합니다.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>어떻게 수행 하나요 기존 SSH 공개 키에 삽입할 hello 가상 컴퓨터 크기 조정 설정 SSH 레이어 프로 비전 중? 원하는 toostore hello SSH 공개 키 값 Azure 키 자격 증명 모음에 다음에 내 리소스 관리자 템플릿을 사용 합니다.

Vm hello를 공용 SSH 키에만 제공 하는 경우 키 자격 증명 모음의 tooput hello 공개 키 필요는 없습니다. 공개 키는 비밀이 아닙니다.
 
Linux VM을 만들 때 일반 텍스트로 SSH 공개 키를 제공할 수 있습니다.

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
linuxConfiguration 요소 이름 | 필수 | 형식 | 설명
--- | --- | --- | --- |  ---
ssh | 아니요 | 컬렉션 | Linux OS에 대 한 hello SSH 키 구성 지정
path | 예 | 문자열 | 여기서 hello SSH 키 또는 인증서를 배치 해야 하는 hello Linux 파일 경로 지정
keyData | 예 | String | base64로 인코딩된 SSH 공개 키를 지정합니다.

예를 들어 참조 [hello 101-vm-sshkey GitHub 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json)합니다.

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>실행할 때 `Update-AzureRmVmss` hello에서 둘 이상의 인증서를 추가한 후 같은 키 자격 증명 모음을 참조 하려면 아래와 같은 메시지가 hello:
 
>Update-AzureRmVmss: 허용되지 않는 /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev의 반복된 인스턴스를 포함하고 있는 비밀을 나열합니다.
 
Toore 시도 하면이 발생할 수 있습니다-hello 동일 hello 기존 원본 자격 증명 모음에 대 한 새 자격 증명 모음 인증서를 사용 하는 대신 자격 증명 모음을 추가 합니다. hello `Add-AzureRmVmssSecret` 추가 암호를 추가 하는 경우 명령이 제대로 작동 하지 않습니다.
 
tooadd hello에서 더 많은 비밀 같은 키 자격 증명 모음, hello $vmss.properties.osProfile.secrets[0].vaultCertificates 목록 업데이트 합니다.
 
Hello 예상 입력된 구조에 대 한 참조 [가상 컴퓨터 설정 만들기 또는 업데이트](https://msdn.microsoft.com/library/azure/mt589035.aspx)합니다.
 
Hello 주요 자격 증명 모음에 있는 hello 가상 컴퓨터 크기 조정 집합 개체에 hello 비밀을 찾습니다. Hello 자격 증명 모음과 연결 된 인증서 참조 (URL hello 및 hello 암호 저장소 이름) toohello 목록에 추가 합니다.

> [!NOTE] 
> 현재 hello 가상 컴퓨터 크기 조정 설정 API를 사용 하 여 Vm에서 인증서를 제거할 수 없습니다.
>

새 Vm hello 이전 인증서를 보유 하지 않습니다. 그러나, 인증서가 hello 고 이미 배포 되어 있는 Vm hello 이전 인증서를 갖게 됩니다.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>인증서 toohello 가상 컴퓨터 크기 집합 hello 인증서 hello 암호 저장소에 있으면 hello 암호를 제공 하지 않고 푸시할 수 있습니까?

스크립트에서 toohard 코드 암호 필요가 없습니다. 암호를 동적으로 검색할 수 있습니다 hello 사용 권한을 가진 toorun hello 배포 스크립트를 사용 합니다. Hello 보안 저장소 키 자격 증명 모음에서 인증서를 이동 하는 스크립트를 사용 하도록 설정한 경우 보안 저장소 hello `get certificate` 명령 또한 hello.pfx 파일의 hello 암호도 출력 합니다.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>가상 컴퓨터 크기에 대 한 virtualMachineProfile.osProfile의 hello 비밀 속성 작업을 설정 하는 방법 인증서에 대 한 절대 URI hello certificateUrl 속성을 사용 하 여 hello toospecify가 있고 hello sourceVault 값 필요한 이유는 무엇입니까? 

Windows 원격 관리 (WinRM) 인증서 참조 hello hello OS 프로필의 암호 속성에에서 있어야 합니다. 

hello hello 원본 자격 증명 모음을 나타내는의 목적은 사용자의 Azure 클라우드 서비스 모델에 있는 tooenforce 액세스 제어 목록 (ACL) 정책입니다. Hello 원본 자격 증명 모음을 지정 하지 않은 경우 사용 권한 문제나 toodeploy 비밀 tooa 키 자격 증명 모음에는 없는 경우에 사용자 수를 계산 리소스 공급자 (CRP) toothrough 것입니다. ACL은 존재하지 않는 리소스에 대해서도 존재합니다.

올바른 주요 자격 증명 모음 URL 있지만 잘못 된 원본 자격 증명 모음 ID를 제공 하는 경우 작업을 hello를 폴링할 때 오류가 보고 됩니다.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>비밀 tooan 기존 가상 컴퓨터 크기 집합에 추가 하는 경우는 hello 비밀 기존 Vm 또는 삽입만 새로? 

인증서 tooall 추가 되는 스토리를 기존 Vm에 있습니다. 가상 컴퓨터 크기 설정 upgradePolicy 속성은 설정 너무**수동**, hello 인증서가 VM hello에 대 한 수동 업데이트를 수행 하면 toohello VM 추가 합니다.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Linux VM에 대한 인증서는 어디에서 추가하나요?

Linux Vm에 대 한 toodeploy 인증서를 확인 하려면 어떻게 toolearn [배포에서 고객이 관리 하는 키 자격 증명 모음 인증서 tooVMs](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/)합니다.
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>새 자격 증명 모음 인증서 tooa 새 인증서 개체를 추가 하려면 어떻게 해야 합니까?

자격 증명 모음 인증서 tooan 기존 암호 tooadd hello 다음 PowerShell 예제를 참조 하십시오. 비밀 개체를 하나만 사용합니다.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>VM 이미지를 복원 하는 경우 toocertificates 어떻게 됩니까?

VM을 이미지로 다시 설치할 경우 인증서는 삭제됩니다. 삭제 hello 전체 운영 체제 디스크를 이미지로 다시 설치 합니다. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>Hello 주요 자격 증명 모음에서 인증서를 삭제 하면 어떻게 되나요?

Hello 암호는 hello 주요 자격 증명 모음에서 삭제 한 다음 실행 `stop deallocate` 모든 Vm에 대 한 다음 다시 시작 하 고, 오류가 발생 합니다. hello 오류가 hello CRP hello 키 자격 증명 모음에서 tooretrieve hello 비밀 하지만 불가능 하기 때문에 발생 합니다. 이 시나리오에서는 가상 컴퓨터 확장 집합 범위가 hello에서 hello 인증서를 삭제할 수 있습니다. 

hello CRP 구성 요소에는 고객 비밀 유지 되지 않습니다. 실행 하는 경우 `stop deallocate` hello 가상 컴퓨터 크기 집합의 모든 Vm에 대 한 hello 캐시가 삭제 됩니다. 이 시나리오에서는 비밀 hello 주요 자격 증명 모음에서 검색 됩니다.

Hello 단일 패브릭 테 넌 트 모델의 Azure 서비스 패브릭에서 hello 암호의 캐시 된 복사본이 있기 때문에 수평 확장 하는 경우이 문제가 발생 하지 않습니다.
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>ह ा व toospecify hello hello 인증서 URL에 대 한 정확한 위치 (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>)에 표시 된 대로, [서비스 패브릭 클러스터 보안 시나리오](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Azure 키 자격 증명 모음 설명서 hello hello 버전이 지정 되지 않은 경우 보안 REST API 가져오기 hello hello 암호의 최신 버전을 반환 해야 하는 hello를 상태입니다.
 
메서드 | URL
--- | ---
GET | https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}

대체 {*보안 이름*}을 hello 이름으로 바꾸고 {*암호 버전*} tooretrieve hello 버전 hello 암호의 원하는 합니다. hello 암호 버전을 제외 될 수 있습니다. 이 경우 hello 최신 버전이 검색 됩니다.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>ह ा व toospecify hello 인증서 버전 키 자격 증명 모음을 사용 합니까?

hello hello 키 자격 증명 모음 요구 사항 toospecify hello 인증서 버전의 목적은 toomake 것을 알 수 toohello 사용자가 Vm에 어떤 인증서가 배포입니다.

VM을 만들고 다음 hello 키 자격 증명 모음에서에 암호를 업데이트 하는 경우 hello 새 인증서를 다운로드 한 tooyour Vm 없습니다. 하지만 Vm 및 새 Vm hello 새 암호를 받을 tooreference 나타납니다. tooavoid이 필요한 tooreference 암호 버전 됩니다.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>내 팀 toous.cer 공개 키로 배포 되는 몇 가지 인증서와 함께 작동 합니다. 이러한 인증서 tooa 가상 컴퓨터 크기 집합 배포 방식을 권장 hello 이란?

toodeploy.cer 공개 키 tooa 가상 컴퓨터 크기 집합.cer 파일에만 포함 하는.pfx 파일을 생성할 수 있습니다. toodo이를 사용 하이 여 `X509ContentType = Pfx`합니다. 예를 들어 hello.cer 파일을 로드 하의 C# 또는 PowerShell을 x509Certificate2 개체 hello 메서드를 호출 합니다. 

자세한 내용은 [X509Certificate.Export 메서드(X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx))를 참조하세요.

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Base64 문자열에 사용자가 toopass 인증서에 대 한 옵션을 나타나지 않습니다. 대부분의 다른 리소스 공급자는 이 옵션을 제공합니다.

base64 문자열에 따라 인증서를 전달 하는 tooemulate hello 최신 버전이 있는 URL 리소스 관리자 서식 파일에서 추출할 수 있습니다. 리소스 관리자 템플릿에 JSON 속성을 다음 hello를 다음과 같습니다.

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>키 자격 증명 모음에 JSON 개체에서 toowrap 인증서 있습니까?

가상 컴퓨터 확장 집합 및 VM에서 인증서가 JSON 개체에 래핑되어야 합니다. 

Hello 콘텐츠 형식을 응용 프로그램/x-pkcs12도 지원 합니다. application/x-pkcs12 사용에 대한 지침을 보려면 [Azure Key Vault의 PFX 인증서](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/)를 참조하세요.
 
현재 .cer 파일은 지원하지 않습니다. toouse.cer 파일을.pfx 컨테이너에 내보내야 합니다.



## <a name="compliance"></a>규정 준수

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>가상 컴퓨터 확장 집합은 PCI 규정을 준수하나요?

가상 컴퓨터 크기 집합은 hello CRP 최상위 씬 API 계층입니다. 두 구성 요소가 Azure 서비스 트리 hello에 hello 계산 플랫폼의 일부입니다.

규정 준수의 관점에서 가상 컴퓨터 크기 집합 hello Azure 계산 플랫폼의 핵심 부분 됩니다. 팀, 도구, 프로세스, 배포 방법이, 보안 제어, 적시에 (JIT) 컴파일, 모니터링, 경고 및 등 hello CRP 자체와 공유 합니다. 가상 컴퓨터 크기 집합은 업계 PCI (Payment Card)-hello CRP hello 현재 PCI 데이터 보안 표준 (DSS) 증명의 일부 이므로 규정을 준수 합니다.

자세한 내용은 참조 [Microsoft 보안 센터 hello](https://www.microsoft.com/TrustCenter/Compliance/PCI)합니다.






## <a name="extensions"></a>확장

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>가상 컴퓨터 확장 집합 확장을 삭제하려면 어떻게 해야 하나요?

가상 컴퓨터 크기 toodelete 확장을 사용 하 여 hello 다음 PowerShell 예제를 설정 합니다.

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
hello extensionName 값을 찾을 수 `$vmss`합니다.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Operations Management Suite와 통합되는 가상 컴퓨터 확장 집합 템플릿 예제가 있나요?

Operations Management Suite로 통합 하는 서식 파일 예제를 설정 하는 가상 컴퓨터 크기에 대 한 참조의 두 번째 예제 hello [Azure 서비스 패브릭 클러스터를 배포 하 고 로그 분석을 사용 하 여 모니터링을 사용 하도록 설정](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric)합니다.
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>확장 가상 컴퓨터 크기 집합에서 병렬로 toorun 것 같습니다. 이렇게 하면 사용자 지정 스크립트 확장 toofail 내 됩니다. 수행할 수 있는 toofix이 있습니까?

가상 컴퓨터 크기 집합 확장명 시퀀스에 대 한 toolearn 참조 [Azure 가상 컴퓨터 크기 집합의 확장 순서](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/)합니다.
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>어떻게 재설정 합니까 hello 암호 Vm에 대 한 내 가상 컴퓨터 크기 집합의?

가상 컴퓨터 크기에서 Vm에 대 한 tooreset hello 암호 설정, VM 액세스 확장을 사용 합니다. 

다음 PowerShell 예에서는 hello를 사용 합니다.

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>내 가상 컴퓨터 크기 집합의 확장 tooall Vm을 추가 하려면 어떻게 해야 합니까?

업데이트 정책 설정 된 경우 너무**자동**, 재배포 hello 템플릿을 hello 새 확장 속성을 가진 모든 Vm을 업데이트 합니다.

업데이트 정책 설정 된 경우 너무**수동**, 먼저 hello 확장을 업데이트 하 고 Vm에서 모든 인스턴스를 수동으로 업데이트 합니다.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>연결 된 기존 가상 컴퓨터 크기 집합 hello 확장 업데이트 되는 경우 영향을 받는 Vm 기존? (즉, Vm hello 됩니다 *하지* 일치 hello 가상 컴퓨터 확장 집합 범위가?) 또는 무시되나요? 기존 컴퓨터를 이미지로 다시 설치 하거나 서비스 치료할 때 hello 구성 된 스크립트는 현재 실행 하는 hello 가상 컴퓨터 크기 집합에 VM을 처음으로 만들어진 hello를 사용 하는 경우에 구성 된 hello 스크립트 또는?

Hello 가상 컴퓨터 규모에 맞게 hello 확장 정의 설정 하는 경우 모델 업데이트 되 고 hello upgradePolicy 속성이 너무**자동**, hello Vm을 업데이트 합니다. Hello upgradePolicy 속성이 너무**수동**, 확장 hello 모델에 일치 하지 않는으로 표시 됩니다. 

기존 VM 서비스 치료 이면으로 다시 부팅 한 표시 하 고 hello 확장을 다시 실행 되지 않습니다. 이미지로 다시 설치 되 고 있는지와 같은 hello 소스 이미지와 hello 운영 체제 드라이브의 교체 합니다. 확장을 같은 hello 최신 모델의 모든 특수화 실행 됩니다.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>가상 컴퓨터 크기 조정 설정 tooan Azure AD 도메인에 참여 하려면?

가상 컴퓨터 크기 조정 설정 tooan Azure Active Directory (Azure AD) 도메인 toojoin 확장을 정의할 수 있습니다. 

확장을 toodefine hello JsonADDomainExtension 속성을 사용 하 여:

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>내 가상 컴퓨터 크기 조정 집합 확장 시도 tooinstall 다시 부팅 해야 하는 것입니다. 예: "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"

시도 하는 경우 가상 컴퓨터 크기 조정 설정 확장 프로그램은 tooinstall 다시 부팅 해야 하는 것을 hello Azure 자동화 필요한 상태 구성 (자동화 DSC) 확장을 사용할 수 있습니다. Hello 운영 체제가 Windows Server 2012 r 2 인 경우 Azure hello WMF Windows Management Framework () 5.0 설치 재부팅 시 끌어와 hello 구성을 사용 하 여 계속 합니다. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>가상 컴퓨터 확장 집합에 대해 맬웨어 방지를 설정하려면 어떻게 해야 하나요?

가상 컴퓨터 크기에서 맬웨어 방지에 tooturn 설정, hello 다음 PowerShell 예제를 사용 하 여:

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>Tooexecute 개인 저장소 계정에서 호스트 되는 사용자 지정 스크립트를 필요 합니다. hello 저장소는 공용 이지만 한 공유 액세스 서명 (SAS) toouse 려 할 때 hello 스크립트가 성공적으로 실행, 실패 합니다. “올바른 공유 액세스 서명에 대한 필수 매개 변수가 없음” 메시지가 표시됩니다. Link+SAS는 로컬 브라우저에서 잘 작동합니다.

개인 저장소 계정에서 호스트 되는 사용자 지정 스크립트 tooexecute hello 저장소 계정 키 및 이름을 사용 하 여 보호 된 설정을 설정 합니다. 자세한 내용은 [Windows용 사용자 지정 스크립트 확장](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings)을 참조하세요.







## <a name="networking"></a>네트워킹
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>Tooall hello VM Nic hello 집합에 적용할 수 있도록 보안 그룹 NSG (네트워크) tooa 배율 설정 가능한 tooassign는?

예. 직접 hello 네트워크 프로필의 안녕하세요 networkInterfaceConfigurations 섹션에 참조 하 여 tooa 크기 집합 네트워크 보안 그룹을 적용할 수 있습니다. 예제:

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>어떻게 하나요 VIP 교체 hello에 가상 컴퓨터 크기 집합 동일한 구독 및 지역이 동일한?

두 개의 가상 설정한 경우 Azure 부하 분산 장치 프런트 엔드가 있는 컴퓨터 크기를 설정 하 고 있는 구독 및 지역이 동일한 hello, hello 각 항목에서 공용 IP 주소 할당을 취소 하 고 다른 toohello를 할당할 수 있습니다. 예제는 [VIP 교체: Azure Resource Manager에서 청록색 배포](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/)를 참조하세요. 이 옵션을 사용 hello로 리소스는 서로 다르지만 할당/할당 취소 hello 네트워크 수준에서 지연을 의미지 않습니다. 빠른 옵션은 두 개의 백 엔드 풀 및 라우팅 규칙을 사용 하 여 Azure 응용 프로그램 게이트웨이 toouse 합니다. 또는 스테이징 및 프로덕션 슬롯 간의 빠른 전환을 지원하는 [Azure App service](https://azure.microsoft.com/en-us/services/app-service/)를 사용하여 응용 프로그램을 호스트할 수도 있습니다.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>개인 IP 주소 toouse 정적 개인 IP 주소 할당에 대 한 범위를 지정 하는 방법

IP 주소는 사용자가 지정한 서브넷에서 선택됩니다. 

가상 컴퓨터 크기 조정 설정 IP 주소의 hello 할당 메서드는 항상 "동적" 되더라도 이러한 IP 주소를 변경할 수 있습니다. 이 경우 "동적"만 의미 PUT 요청에서 hello IP 주소를 지정 하지 않으면 합니다. 정적 hello 서브넷을 사용 하 여 설정 hello를 지정 합니다. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>가상 컴퓨터 크기 집합 tooan 기존 Azure 가상 네트워크를 어떻게 배포 합니까? 

toodeploy 가상 컴퓨터 크기 집합 tooan 기존 Azure 가상 네트워크를 참조 하십시오 [는 가상 컴퓨터 크기 집합 tooan 기존 가상 네트워크를 배포](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet)합니다. 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Hello IP 주소를 추가 하는 방법 hello 가상 컴퓨터 크기에서 첫 번째 VM 템플릿의 toohello 출력 설정 되어 있습니까?

hello의 tooadd hello IP 주소는 서식 파일의 가상 컴퓨터 크기 조정 설정 toohello 출력에서 첫 번째 VM 참조 [ARM: 가져오기 VMSS 개인 Ip](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips)합니다.

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>가속 네트워킹을 포함한 확장 집합을 사용할 수 있나요?

예. 네트워킹, accelerated toouse enableAcceleratedNetworking tootrue 눈금에서 집합의 networkInterfaceConfigurations 설정을 설정 합니다. 예:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>크기 집합에서 사용 하는 hello DNS 서버를 구성 하려면 어떻게 해야 합니까?

toocreate VM 크기 설정 사용자 지정 DNS 구성을 dnsSettings JSON 패킷 toohello 눈금 집합 Networkinterfaceconfiguration 섹션을 추가 합니다. 예제:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>눈금 집합 tooassign 공용 IP 주소 tooeach VM 구성 하려면 어떻게 해야 합니까?

toocreate VM 크기 집합을 할당 한 공용 IP 주소 tooeach VM hello Microsoft.Compute/virtualMAchineScaleSets 리소스의 hello API 버전이 2017-03-30 되었는지 확인 하 고 추가 _publicipaddressconfiguration_ JSON 패킷 toohello 배율 ipConfigurations 섹션을 설정합니다. 예제:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>눈금 집합 toowork 여러 응용 프로그램 게이트웨이를 구성할 수 있습니까?

예. Hello 리소스 id는 여러 응용 프로그램 게이트웨이 백 엔드 주소 풀 toohello 추가할 수 있습니다 _applicationGatewayBackendAddressPools_ hello 목록 _ipConfigurations_ 크기 집합의 섹션 네트워크 프로필입니다.

## <a name="scale"></a>확장

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>어떤 경우에 VM이 2개 미만인 가상 컴퓨터 확장 집합을 만들어야 하나요?

한 가지 이유 toocreate는 가상 컴퓨터 크기 집합 vm이 두 개 미만의 가상 컴퓨터 크기의 toouse hello 탄력적 속성 설정 됩니다. 예를 들어 배포할 수 있습니다는 가상 컴퓨터 크기 집합 Vm toodefine 0으로 인프라 비용을 실행 하는 VM을 지불 하지 않고. 그런 다음 준비 toodeploy Vm 인 경우 hello "용량의" hello 가상 컴퓨터 확장 집합 toohello 프로덕션 인스턴스 개수 증가 합니다.

VM이 2개 미만인 가상 컴퓨터 확장 집합을 만드는 또 다른 경우는 개별 VM이 있는 가용성 집합을 사용하는 것보다 가용성에 별 관심이 없을 때입니다. 가상 컴퓨터 크기 집합에는 대체 가능 포트나 계산 단위가 있는 방식으로 toowork를 제공 합니다. 이 일관성은 가상 컴퓨터 확장 집합과 가용성 집합의 주요 차별 요인이기도 합니다. 다양한 상태 비저장 워크로드는 개별 단위를 추적하지 않습니다. Hello 작업 부하를 삭제 하는 경우 tooone 계산 단위 축소 없으며 hello 작업이 증가 하는 경우 toomany 다음 확장할 수 있습니다.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>가상 컴퓨터 크기 집합의 Vm hello 수를 변경 하려면 어떻게 해야 합니까?

Vm의 가상 컴퓨터 크기 집합 toochange hello 번호 참조 [가상 컴퓨터 크기 집합의 인스턴스 수는 hello 변경](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/)합니다.

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>특정 임계값에 도달하는 경우 사용자 지정 경고를 정의하려면 어떻게 해야 하나요?

지정된 임계값에 대한 경고를 처리하는 방법은 다소 유연한 편입니다. 예를 들어 사용자 지정 웹후크를 정의할 수 있습니다. 다음 예에서는 webhook hello은 리소스 관리자 템플릿으로입니다.

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

이 예제에서는 경고 임계값에 도달 하면 tooPagerduty.com를 이동 합니다.



## <a name="patching-and-operations"></a>패치 및 작업

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>기존 리소스 그룹에서 확장 집합을 만들려면 어떻게 하나요?

크기 집합 만들기에 기존 리소스 그룹이 아직 수 없으면 hello Azure 포털에서에서 하지만 Azure 리소스 관리자 템플릿에서 집합 소수 자릿수를 배포한 경우에 기존 리소스 그룹을 지정할 수 있습니다. 또한 Azure PowerShell 또는 CLI를 사용하여 확장 집합을 만들 때에도 기존 리소스 그룹을 지정할 수 있습니다.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>눈금 설정 tooanother 리소스 그룹을 이동할 수 우리?

예, 배율 집합 리소스 tooa 새 구독 또는 리소스 그룹을 이동할 수 있습니다.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>방법 tooI 업데이트 내 가상 컴퓨터 크기 집합 tooa 새 이미지? 패치는 어떻게 관리해야 하나요?

tooa 새 이미지 및 toomanage 패치, 가상 컴퓨터 크기 설정 tooupdate 참조 [가상 컴퓨터 크기 집합 업그레이드](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set)합니다.

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>Hello 이미지를 변경 하지 않고 hello 이미지로 다시 설치 작업 tooreset VM을 사용할 수 있습니까? (즉, 원하는 재설정 VM toofactory 설정 tooa 새 이미지가 아닌.)

예, hello 이미지를 변경 하지 않고 hello 이미지로 다시 설치 작업 tooreset VM을 사용할 수 있습니다. 그러나 가상 컴퓨터 크기 집합 참조와 플랫폼 이미지 `version = latest`, VM tooa를 업데이트할 수 이상 운영 체제 이미지를 호출할 때 `reimage`합니다.

자세한 내용은 [가상 컴퓨터 확장 집합의 모든 VM 관리](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set)를 참조하세요.



## <a name="troubleshooting"></a>문제 해결

### <a name="how-do-i-turn-on-boot-diagnostics"></a>부팅 진단을 켜려면 어떻게 하나요?

부트 진단 tooturn는 먼저 저장소 계정을 만듭니다. 그런 다음 가상 컴퓨터 크기 집합의이 JSON 블록을 삽입 **virtualMachineProfile**, hello 가상 컴퓨터 크기 집합을 업데이트 합니다.

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

새 VM이 만들어지면 hello hello VM의 InstanceView 속성 hello 스크린 샷 및 기타 등등에 대 한 hello 세부 정보를 표시 합니다. 예를 들면 다음과 같습니다.
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>가상 컴퓨터 속성

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>여러 번 호출하지 않고도 각 VM에 대한 속성 정보를 얻으려면 어떻게 합니까? 예를 들어는 얻으려면 어떻게 hello 장애 도메인 각 hello에 대 한 100 Vm 내 가상 컴퓨터 크기 집합의?

호출할 수 있습니다 tooget를 여러 번 호출 하지 않고 각 VM에 대 한 속성 정보를 `ListVMInstanceViews` REST API를 수행 하 여 `GET` hello 리소스 URI 뒤에:

/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>있습니까 인수를 전달할 수 다른 확장 toodifferent Vm에서 가상 컴퓨터 크기 집합?

아니요, 전달할 수 없으며 다른 확장 인수 toodifferent Vm 가상 컴퓨터 크기 집합입니다. 그러나 확장 hello hello hello 컴퓨터 이름에서와 같이에서 실행 중인 VM의 고유한 속성에 따라 작동할 수 있습니다. 확장도 쿼리할 수 http://169.254.169.254 tooget에 인스턴스 메타 데이터 hello VM에 대 한 자세한 정보.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>가상 컴퓨터 확장 집합 VM 컴퓨터 이름과 VM ID 간에 차이가 발생하는 이유는 무엇인가요? 예를 들어 0, 1, 3...입니다.

가상 컴퓨터 크기 집합이 아니므로 가상 컴퓨터 크기 조정 설정 VM 컴퓨터 이름 및 VM Id 사이 간격이 없는 **과도 프로 비전이** 속성의 기본값 toohello **true**합니다. 너무 설정 과도 프로 비전**true**를 생성 하는 요청 된 수보다 더 많은 Vm입니다. 그런 후에 추가 VM은 삭제됩니다. 이 경우 배포 향상 된 안정성을 얻을 수 있지만 연속 이름 지정 및 인접 한 네트워크 주소 변환 (NAT)의 hello 비용 규칙. 

이 속성을 너무 설정할 수**false**합니다. 소규모 가상 컴퓨터 확장 집합의 경우 이렇게 해도 배포 안정성에 큰 영향을 주지는 않습니다.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>가상 컴퓨터 크기 집합의 VM을 삭제 하 고 hello VM 할당 해제 hello 차이 무엇입니까? 다른 hello 속도 중에서 선택 해야는 경우

hello 가상 컴퓨터 크기 집합의 VM을 삭제 하 고 hello VM 할당 해제 간의 주요 차이점은 `deallocate` hello 가상 하드 디스크 (Vhd)를 삭제 하지 않습니다. `stop deallocate` 실행과 관련된 저장소 비용이 있습니다. 하나를 사용 하거나 hello 다음 이유 중 하나에 대 한 다른 hello 수 있습니다.

- 계산 비용을 지불 toostop 싶지만 hello Vm의 tookeep hello 디스크 상태를 원하는 합니다.
- 원하는 가상 컴퓨터 크기 집합을 확장할 수 있는 보다 더 빨리 toostart Vm 집합입니다.
  - 관련된 toothis 시나리오에서는 만든 사용자 고유의 자동 크기 조정 엔진 및 더 빠른 종단 간 눈금 원하는 합니다.
- 장애 도메인이나 업데이트 도메인 간에 고르게 분산되지 않은 가상 컴퓨터 확장 집합이 있습니다. 이러한 상황은 과도한 프로비저닝 후에 선택적으로 VM을 삭제했거나 VM이 삭제되었기 때문에 발생할 수 있습니다. 실행 `stop deallocate` 이어서 `start` hello 가상 컴퓨터 크기 집합을 균등 하 게 분산 hello Vm 장애 도메인 또는 업데이트 도메인입니다.

