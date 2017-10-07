---
title: "Azure에서 aaaCreate 서비스 패브릭 클러스터 | Microsoft Docs"
description: "PowerShell을 사용 하 여 Azure에 있는 toocreate Windows 또는 Linux 서비스 패브릭 클러스터 하는 방법을 알아봅니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a>PowerShell을 사용하여 Azure에서 보안 클러스터 만들기
이 자습서에서는 어떻게 toocreate 서비스 패브릭 클러스터를 실행 (Windows 또는 Linux) Azure에서. 작업을 완료 하는 경우 응용 프로그램을 배포할 수 있는 hello 클라우드에서 실행 하는 클러스터를 수 있습니다.

이 자습서에서는 다음 방법에 대해 알아봅니다.

> [!div class="checklist"]
> * PowerShell을 사용하여 Azure에서 안전한 Service Fabric 클러스터 만들기
> * X.509 인증서로 hello 클러스터 보안
> * PowerShell을 사용 하 여 toohello 클러스터에 연결
> * 클러스터 제거

## <a name="prerequisites"></a>필수 조건
이 자습서를 시작하기 전에:
- Azure 구독이 없는 경우 [평가판 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.
- Hello 설치 [서비스 패브릭 SDK 및 PowerShell 모듈](service-fabric-get-started.md)
- Hello 설치 [Azure Powershell 모듈 버전 4.1 이상](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)

절차를 수행 하는 hello 단일 노드 (단일 가상 컴퓨터) 미리 보기 서비스 패브릭 클러스터를 만듭니다. hello 클러스터 hello 클러스터와 함께 생성를 가져오고 다음 키 자격 증명 모음에 배치 하는 자체 서명 된 인증서에 의해 보안 됩니다. 단일 노드 클러스터의 가상 컴퓨터를 하나 이상 확장할 수 없습니다 및 미리 보기 클러스터 업그레이드 toonewer 버전 일 수 없습니다.

서비스 패브릭 클러스터를 사용 하 여 Azure hello에서 실행 하 여 발생 하는 toocalculate 비용 [Azure 가격 계산기](https://azure.microsoft.com/pricing/calculator/)합니다.
Service Fabric 클러스터를 만드는 방법에 대한 자세한 내용은 [Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-via-arm.md)를 참조하세요.

## <a name="create-hello-cluster-using-azure-powershell"></a>Azure PowerShell을 사용 하 여 hello 클러스터 만들기
1. Hello에서 hello Azure 리소스 관리자 템플릿 및 hello 매개 변수 파일의 로컬 복사본을 다운로드 [서비스 패브릭 용 Azure 리소스 관리자 템플릿](https://aka.ms/securepreviewonelineclustertemplate) GitHub 리포지토리 합니다.  *azuredeploy.json* 서비스 패브릭 클러스터를 정의 하는 hello Azure 리소스 관리자 템플릿이 됩니다. *azuredeploy.parameters.json* toocustomize hello 클러스터 배포는 매개 변수 파일 수는 있습니다.

2. Hello hello에 대 한 매개 변수 뒤에 사용자 지정 *azuredeploy.parameters.json* 매개 변수 파일:

   | 매개 변수       | 설명 | 제안 값 |
   | --------------- | ----------- | --------------- |
   | clusterLocation | hello Azure 지역 toowhich toodeploy hello 클러스터입니다. | *예: westeurope, eastasia, eastus* |
   | clusterName     | 이름을 원하는 toocreate hello 클러스터입니다. | *예: bobs-sfpreviewcluster* |
   | adminUserName   | 가상 컴퓨터를 클러스터링 하는 hello에 대 한 hello 로컬 관리자 계정. | *모든 유효한 Windows Server 사용자 이름* |
   | adminPassword   | 가상 컴퓨터를 클러스터링 하는 hello에 대 한 hello 로컬 관리자 계정의 암호입니다. | *모든 유효한 Windows Server 암호* |
   | clusterCodeVersion | 서비스 패브릭 버전 toorun hello 합니다. (미리 보기 버전은 255.255.X.255) | **255.255.5718.255** |
   | vmInstanceCount | (1 개 또는 3-99 일 수 있음) 클러스터의 가상 컴퓨터의 hello 수입니다. | **1** | *미리 보기 클러스터에 하나의 가상 컴퓨터를 지정합니다.* |

3. PowerShell 콘솔, 로그인 tooAzure 열고 toodeploy hello 클러스터에서 원하는 hello 구독을 선택 합니다.

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. 페이지를 만들고 서비스 패브릭에서 사용 하는 hello 인증서 toobe에 대 한 암호를 암호화 합니다.

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. Hello 다음 명령을 실행 하 여 hello 클러스터 및 해당 인증서를 만듭니다.

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   >hello `-CertificateSubjectName` hello 매개 변수 파일에 지정 된 hello clusterName 매개 변수 매개 변수 맞춰짐을도 hello 도메인 연결 toohello Azure 지역으로 선택한와 같은: `clustername.eastus.cloudapp.azure.com`합니다.

Hello 구성 완료 되 면 Azure에서 만든 hello 클러스터에 대 한 정보를 출력 합니다. 또한이 매개 변수에 대해 지정 된 hello 경로에 hello 클러스터 인증서 toohello-CertificateOutputFolder 디렉터리를 복사 합니다. 이 인증서 tooaccess 클러스터의 서비스 패브릭 탐색기 및 보기 hello 상태 해야합니다.

비슷한 toohello 일 수 있는 클러스터에 대 한 hello URL을 기록해 url: *https://mycluster.westeurope.cloudapp.azure.com:19080*

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a>서비스 패브릭 탐색기 액세스 및 hello 인증서 수정 ##

1. Hello 인증서 tooopen hello 인증서 가져오기 마법사를 두 번 클릭 합니다.

2. 기본 설정을 사용 하지만 있는지 toocheck hello **이 키를 내보낼 수 있도록 표시 합니다.** 확인란 hello **개인 키 보호** 단계입니다. 이 자습서의 뒷부분에 나오는 Azure 컨테이너 레지스트리 tooService 패브릭 클러스터 인증을 구성할 때 visual Studio tooexport hello 인증서가 필요 합니다.

3. 이제 브라우저에서 Service Fabric Explorer를 열 수 있습니다. toodo toohello를 따라서 이동 **ManagementEndpoint** 웹 브라우저를 컴퓨터에 저장 된 select hello 인증서를 사용 하 여 클러스터에 대 한 URL입니다.

>[!NOTE]
>Service Fabric Explorer를 열면 인증서 오류가 표시되는데 이는 자체 서명된 인증서를 사용하고 있기 때문입니다. Edge에서는 tooclick 있는 *세부 정보* 다음 hello 및 *toohello 웹 페이지에서 이동* 링크 합니다. Chrome에서는 tooclick 있는 *고급* 다음 hello 및 *계속* 링크 합니다.

>[!NOTE]
>Hello 클러스터 만들기가 실패할 경우에 이미 배포 된 hello 리소스를 업데이트 하는 hello 명령 항상 다시 실행할 수 있습니다. 에서 실패 하는 hello 배포의 일부로 인증서를 만든 경우 새로 생성 됩니다. tootroubleshoot 클러스터를 만드는 참조 [Azure 리소스 관리자를 사용 하 여 서비스 패브릭 클러스터를 만들](service-fabric-cluster-creation-via-arm.md)합니다.

## <a name="connect-toohello-secure-cluster"></a>Toohello 보안 클러스터에 연결
서비스 패브릭 SDK hello와 함께 설치 하는 hello 서비스 패브릭 PowerShell 모듈을 사용 하 여 toohello 클러스터에 연결 합니다.  첫째, 컴퓨터에 hello 현재 사용자의 개인 (My) 저장소 hello로 hello 인증서를 설치 합니다.  Hello 다음 PowerShell 명령을 실행 합니다.

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

준비 tooconnect tooyour 보안 클러스터가 나타납니다.

hello **서비스 패브릭** PowerShell 모듈 서비스 패브릭 클러스터, 응용 프로그램 및 서비스를 관리 하기 위한 많은 cmdlet을 제공 합니다.  사용 하 여 hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello 보안 클러스터입니다. 인증서 지문을 hello 및 연결 끝점 세부 정보는 이전 단계의 hello 출력에서 찾을 수 있습니다.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

연결 하 고 hello 클러스터 상태가 정상이 hello를 사용 하 여 확인 [Get ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a>리소스 정리

클러스터 구성 된 다른 Azure 리소스로 또한 자체 toohello 클러스터 리소스입니다. hello 가장 간단한 방법은 toodelete hello 클러스터와 사용 하는 모든 hello 리소스 toodelete hello 리소스 그룹입니다.

TooAzure을 고 tooremove hello 클러스터 할 hello 구독 ID를 선택 합니다.  Toohello에 로그인 하 여 구독 ID를 찾을 수 [Azure 포털](http://portal.azure.com)합니다. Hello 리소스 그룹 및 hello를 사용 하 여 모든 hello 클러스터 리소스 삭제 [제거 AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup)합니다.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음 방법에 대해 알아보았습니다.

> [!div class="checklist"]
> * Azure에서 Service Fabric 클러스터 만들기
> * X.509 인증서로 hello 클러스터 보안
> * PowerShell을 사용 하 여 toohello 클러스터에 연결
> * 클러스터 제거

다음으로 이동 하는 자습서 toolearn 방법을 따르는 toohello toodeploy 기존 응용 프로그램입니다.
> [!div class="nextstepaction"]
> [Docker Compose를 사용하여 기존 .NET 응용 프로그램 배포](service-fabric-host-app-in-a-container.md)
