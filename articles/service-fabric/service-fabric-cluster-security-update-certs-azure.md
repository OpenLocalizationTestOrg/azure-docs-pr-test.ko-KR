---
title: "Azure 서비스 패브릭 클러스터에 있는 aaaManage 인증서 | Microsoft Docs"
description: "새 인증서 tooadd, 롤오버 인증서 및 제거 tooor 서비스 패브릭 클러스터에서이 인증서 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Azure에서 서비스 패브릭 클러스터에 대한 인증서 추가 또는 제거
서비스 패브릭 X.509 인증서를 사용 하는 방법을 파악 하 고 hello 잘 알고 있어야 하는 것이 좋습니다 [클러스터 보안 시나리오](service-fabric-cluster-security.md)합니다. 다음 과정으로 진행하기 전에 클러스터 인증서가 무엇이며 어떤 용도로 사용되는지를 이해해야 합니다.

인증서, 기본 및 보조 복제본이 구성 하는 경우 2 개의 클러스터를 지정할 수는 서비스 패브릭 있습니다 더하기 tooclient 인증서에서 클러스터를 만드는 동안 보안을 인증서입니다. 너무 참조[포털을 통해 azure는 클러스터를 만드는](service-fabric-cluster-creation-via-portal.md) 또는 [Azure Resource Manager를 통해 azure 클러스터에 만드는](service-fabric-cluster-creation-via-arm.md) 에서 설정에 대 한 내용은 생성 시간에 대 한 합니다. 클러스터 인증서를 하나만 지정 하는 경우 만들 때, hello 기본 인증서로 사용 되는 다음 합니다. 클러스터를 만든 후 새 인증서를 보조 인증서로 추가할 수 있습니다.

> [!NOTE]
> 보안 클러스터에 대 한 배포 유효한 (하지 해지 및 만료 된) 클러스터를 하나 이상 인증서 (주 또는 보조)가 항상 필요 (그렇지 않은 경우 hello 클러스터 작동을 멈춘). 90 일 동안 모든 올바른 인증서 만료 기간에 도달 하기 전에 hello 시스템 경고 추적 및 hello 노드에서 경고 상태 이벤트를 생성 합니다. 현재, 서비스 패브릭이 이 항목에 대해 전송하는 전자 메일 또는 기타 알림은 없습니다. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Hello 포털을 사용 하 여 보조 클러스터 인증서 추가

Hello Azure 포털을 통해 보조 클러스터 인증서를 추가할 수 없습니다. Azure toouse 있는 powershell에 대 한 합니다. 이 문서의 뒷부분에 나오는 hello 프로세스를 간략하게 설명 합니다.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Hello 포털을 사용 하 여 hello 클러스터 인증서 교환

성공적으로 배포한 후 보조 클러스터 인증서가 기본 및 보조 tooswap hello 하려는 경우, 다음 toohello 보안 블레이드를 찾아서 hello 상황에 맞는 메뉴 tooswap hello 보조 인증서와에서 hello '주와 스왑' 옵션을 선택 hello 기본 인증서입니다.

![인증서 교환][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Hello 포털을 사용 하 여 클러스터 인증서 제거

보안 클러스터에 대 한 항상 하나 이상의 유효한 (하지 해지 및 만료 된) 인증서 필요 (주 또는 보조) 배포 파일이 없으면 hello 클러스터 작동을 중지 합니다.

클러스터 보안, toohello 보안 블레이드를 탐색 및 선택 hello 'Delete' hello 상황에 맞는 메뉴에서에서 옵션 hello 보조 인증서에 사용 되지 않도록 보조 인증서 tooremove 합니다.

원래의 도와 tooremove hello 인증서 tooswap 해야 합니다, 주 표시 된 경우 사용 하 여 먼저 보조 hello 삭제 한 후 보조 hello hello 업그레이드가 완료 된 후.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Resource Manager Powershell을 사용하여 보조 인증서 추가

이러한 단계는 적어도 하나의 서비스 패브릭 클러스터 리소스 관리자 템플릿을 사용 하 여 배포한 및 hello 템플릿이 tooset 편리 hello 클러스터를 사용 하는 리소스 관리자 작동 방법에 대해 잘 알고 있는지 가정 합니다. 또한 JSON을 잘 사용하여 작업할 수 있다고 간주합니다.

> [!NOTE]
> 샘플 템플릿과 toofollow 시작 지점으로 또는 함께 사용할 수 있는 매개 변수에 대 한 원하는 경우 다음에서 다운로드할이 [git 리포지토리](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)합니다. 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Resource Manager 템플릿 편집

보지 쉽도록 샘플 5-VM-1-NodeTypes-Secure_Step2.JSON 수행할 예정 hello 편집 내용을 모두 포함 합니다. hello 샘플에서 제공 됩니다. [git 리포지토리](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample)합니다.

**모든 hello 단계 toofollow 있는지 확인**

**1 단계:** toodeploy 클러스터링을 사용 하는 hello 리소스 관리자 템플릿을 엽니다. (리포지토리 위에 hello에서 hello 샘플을 다운로드 한 경우 다음 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy 보안 클러스터를 사용 하 여 한 다음 해당 서식 파일을 엽니다).

**2 단계:** 추가 **두 개의 새 매개 변수** "secCertificateThumbprint" 및 "secCertificateUrlValue" 형식의 "string" 서식 파일의 매개 변수 섹션 toohello 합니다. 다음 코드 조각 hello 복사한 toohello 템플릿을 추가할 수 있습니다. 서식 파일의 hello 소스에 따라 정의 된 이러한 사항이 하, 그렇다면 toohello 다음 단계를 이동 이미 수 있습니다. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**3 단계:** toohello 변경 **Microsoft.ServiceFabric/clusters** 리소스-템플릿에 hello "Microsoft.ServiceFabric/clusters" 리소스 정의 찾습니다. 해당 정의의 속성에서 있습니다 "Certificate" JSON 태그 hello 다음 JSON 코드 조각은 다음과 같아야 합니다.

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

새 태그 "ThumbprintSecondary"를 추가하고 "[parameters('secCertificateThumbprint')]" 값을 지정합니다.  

리소스 정의 hello hello 다음과 같아야 합니다. 지금 (hello 서식 파일의 원본에 따라 아닐 아래 hello 조각 똑같이). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

너무 하려는 경우**hello 인증서 롤오버**, 다음으로 기본 및 이동 hello 현재 주 복제본에서 보조 데이터베이스로 hello 새 인증서를 지정 합니다. 따라서 하나의 배포 단계에서 현재 기본 인증서 toohello 새 인증서의 hello 롤오버 됩니다.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**4 단계:** 너무 변경**모든** hello **Microsoft.Compute/virtualMachineScaleSets** 리소스 정의-hello Microsoft.Compute/virtualMachineScaleSets 리소스 찾기 정의 합니다. 스크롤 toohello "publisher": "Microsoft.Azure.ServiceFabric"에서 "virtualMachineProfile"입니다.

Hello 서비스 패브릭 게시자 설정을 다음과 같이 나타납니다.

![Json_Pub_Setting1][Json_Pub_Setting1]

새 인증서 항목 tooit hello를 추가 합니다.

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

hello 속성은 이제 다음과 같이 표시

![Json_Pub_Setting2][Json_Pub_Setting2]

너무 하려는 경우**hello 인증서 롤오버**, 다음으로 기본 및 이동 hello 현재 주 복제본에서 보조 데이터베이스로 hello 새 인증서를 지정 합니다. 따라서 하나의 배포 단계에서 현재 인증서 toohello 새 인증서의 hello 롤오버 됩니다. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
hello 속성은 이제 다음과 같이 표시

![Json_Pub_Setting3][Json_Pub_Setting3]


**5 단계:** 너무 변경할**모든** hello **Microsoft.Compute/virtualMachineScaleSets** 리소스 정의-hello Microsoft.Compute/virtualMachineScaleSets 리소스 찾기 정의 합니다. Toohello "vaultCertificates" 스크롤하여:, "OSProfile" 아래에서 합니다. 다음과 같이 표시됩니다.


![Json_Pub_Setting4][Json_Pub_Setting4]

Hello secCertificateUrlValue tooit를 추가 합니다. 다음 코드 조각 hello를 사용 합니다.

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
이제 Json으로 인해 발생 하는 hello 다음과 같이 표시 됩니다.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> 서식 파일에서 4, 5 단계를 반복 모든 hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets 리소스 정의 대 한 있어야 하 고 있는지 확인 합니다. 그 중 하나를 누락 하는 경우 해당 VMSS에 hello 인증서 설치 되지 않습니다 및 (올바른 인증서가 해당 hello 클러스터 보안을 위해 사용할 수 있습니다 /fd 경우 내려갈 hello 클러스터를 포함 하 여 클러스터에서 예기치 않은 결과 갖게 됩니다. 따라서 진행에 앞서 다시 한 번 확인하세요.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>템플릿 파일 tooreflect hello 새 매개 변수 위에 추가 편집
Hello hello 샘플을 사용 하는 경우 [git 리포지토리](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow toomake 변경 hello 샘플 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON에서 시작할 수 있습니다, 

Hello 두 개의 새 매개 변수를 추가 secCertificateThumbprint 및 secCertificateUrlValue를 리소스 관리자 템플릿 매개 변수 파일을 편집 합니다. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Hello 템플릿 tooAzure 배포

- 사용자는 이제 준비 toodeploy 템플릿 tooAzure 합니다. Azure PS 버전 1+ 명령 프롬프트를 엽니다.
- Azure 계정 tooyour을 고 hello 특정 azure 구독을 선택 합니다. 이것이 azure 구독 하나 보다 액세스 toomore 직원에 대 한 중요 한 단계입니다.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Hello 템플릿 이전 toodeploying 테스트 것입니다. 사용 하 여 hello 현재 클러스터에 배포 되는 동일한 리소스 그룹입니다.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Hello 템플릿 tooyour 리소스 그룹을 배포 합니다. 사용 하 여 hello 현재 클러스터에 배포 되는 동일한 리소스 그룹입니다. Hello 새로 AzureRmResourceGroupDeployment 명령을 실행 합니다. Hello 기본값 이므로 toospecify hello 모드 불필요 **증분**합니다.

> [!NOTE]
> TooComplete 모드를 설정 하는 경우 서식 파일에 있지 않은 리소스를 실수로 삭제할 수 있습니다. 따라서 이러한 경우에는 사용하지 않도록 합니다.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

여기 채워진는 hello의 예에서는 아웃은 동일한 powershell 합니다.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Hello 배포 완료 되 면 연결 tooyour 클러스터를 사용 하 여 새 인증서를 hello 및 일부 쿼리를 수행 합니다. 수 toodo 경우. 그런 다음 hello 이전 인증서를 삭제할 수 있습니다. 

자체 서명 된 인증서를 사용 하는 경우 tooimport 잊지 마십시오를 로컬 TrustedPeople 인증서 저장소에 해당 합니다.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
빠른 참조에 대 한 같습니다 hello 명령 tooconnect tooa 보안 클러스터 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
빠른 참조에 대 한 같습니다 hello 명령 tooget 클러스터 상태

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>응용 프로그램 인증서 toohello 클러스터를 배포 합니다.

Hello keyvault toohello 노드에서에서 배포 된 toohave hello 인증서 위의 5 단계에에서 설명 된 대로 동일한 단계를 사용할 수 있습니다. 다른 매개 변수를 정의하여 사용하면 됩니다.


## <a name="adding-or-removing-client-certificates"></a>클라이언트 인증서 추가 또는 제거

또한 toohello 클러스터 인증서에 서비스 패브릭 클러스터에 대 한 클라이언트 인증서 tooperform 관리 작업을 추가할 수 있습니다.

관리자 또는 읽기 전용 등, 두 종류의 클라이언트 인증서를 추가할 수 있습니다. 그런 다음 사용된 toocontrol 액세스 toohello 관리 작업 및 hello 클러스터에서 쿼리 작업 수 있습니다. 기본적으로 hello 클러스터 인증서에는 관리 인증서 목록 허용 toohello를 추가 됩니다.

클라이언트 수를 원하는 대로 지정할 수 있습니다. 구성 업데이트 toohello 서비스 패브릭 클러스터의 각 추가/삭제 결과


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>포털을 통해 관리자 또는 읽기 전용 클라이언트 인증서 추가

1. Toohello 보안 블레이드를 탐색 하 고 hello 선택 '+ 인증' hello 보안 블레이드 맨 위에 있는 단추입니다.
2. Hello ' 추가 인증 ' 블레이드에서 hello ' 인증 유형 '-'읽기 전용 클라이언트' 또는 '관리 클라이언트'를 선택 합니다.
3. 이제 hello 인증 방법을 선택 합니다. 패브릭 tooService hello 주체 이름 또는 손도장이 hello 사용 하 여이 인증서를 조회 해야 하는지 여부를 나타냅니다. 일반적으로 주체 이름의 좋은 보안 방법은 toouse hello 권한 부여 메서드 않습니다. 

![클라이언트 인증서 추가][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>클라이언트 인증서-관리자 또는 읽기 전용으로 사용 하 여 삭제 hello 포털

클러스터 보안, toohello 보안 블레이드를 탐색 및 선택 hello 'Delete' hello 상황에 맞는 메뉴에서에서 옵션 hello 특정 인증서에 사용 되지 않도록 보조 인증서 tooremove 합니다.



## <a name="next-steps"></a>다음 단계
클러스터 관리에 대한 자세한 내용은 다음 문서를 읽어보세요.

* [서비스 패브릭 클러스터 업그레이드 프로세스 및 사용자 기대 수준](service-fabric-cluster-upgrade.md)
* [클라이언트에 대한 역할 기반 액세스 설정](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


