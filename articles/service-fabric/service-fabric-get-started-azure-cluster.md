---
title: "Azure 서비스 패브릭 클러스터를 aaaSet | Microsoft Docs"
description: "빠른 시작 - Azure에서 Windows 또는 Linux Service Fabric 클러스터를 만듭니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a>Azure에서 첫 번째 Service Fabric 클러스터 만들기
[Service Fabric 클러스터](service-fabric-deploy-anywhere.md): 마이크로 서비스가 배포되고 관리되는 네트워크로 연결된 가상 또는 실제 컴퓨터 집합입니다. 이 퀵 스타트의 toocreate hello를 통해 Windows 또는 Linux를 실행 하는 다섯 개 노드 클러스터를 사용 하면. [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) 또는 [Azure 포털](http://portal.azure.com) 단 몇 분 후에 있습니다.  

Azure 구독이 아직 없는 경우 시작하기 전에 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 을 만듭니다.


## <a name="use-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여

Toohello Azure 포털에 로그인 [http://portal.azure.com](http://portal.azure.com)합니다.

### <a name="create-hello-cluster"></a>Hello 클러스터 만들기

1. Hello 클릭 **새로** 단추 hello 왼쪽 위 모서리의 hello Azure 포털에서 찾을 수 있습니다.
2. 선택 **계산** hello에서 **새로** 블레이드에 대 한 다음 선택 **서비스 패브릭 클러스터** hello에서 **계산** 블레이드입니다.
3. 서비스 패브릭 hello 채울 **기본 사항** 폼입니다. 에 대 한 **운영 체제**선택, hello 버전의 Windows 또는 Linux 클러스터 노드 toorun hello 원하는 합니다. hello 사용자 이름 및 암호를 여기에 입력 된 toohello 가상 컴퓨터에서 사용 되는 toolog입니다. **리소스 그룹**에 대해 새 리소스 그룹을 만듭니다. 리소스 그룹은 Azure 리소스가 만들어지고 전체적으로 관리되는 논리적 컨테이너입니다. 완료되면 **확인**을 클릭합니다.

    ![클러스터 설정 출력][cluster-setup-basics]

4. Hello 채울 **클러스터 구성** 폼입니다.  **노드 유형 개수**에는 "1"을 입력합니다.

5. 선택 **노드 유형 1 (기본)** hello 확인 하 고 **노드 유형 구성** 폼입니다.  노드 유형 이름을 입력 하 고 hello 설정 [내구성 계층](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) 너무 "브론즈."  VM 크기를 선택합니다.

    기타 설정에 대 한 해당 유형의 Vm hello 및 노드 형식은 hello VM 크기, Vm, 사용자 지정 끝점 수를 정의 합니다. 정의 된 각 노드 형식 집합으로 사용 되는 toodeploy 및 관리 되는 가상 컴퓨터에이 별도 가상 컴퓨터 크기 집합으로 설정 되어 있습니다. 각 노드 형식은 독립적으로 확장 또는 축소되고, 다른 포트의 집합을 열며 다른 용량 메트릭을 가질 수 있습니다.  hello 첫 번째 또는, 주 노드 유형 중 이며 여기서 서비스 패브릭 시스템 서비스 호스팅되는 Vm 5 개 이상 있어야 합니다.

    프로덕션 배포의 경우 [용량 계획](service-fabric-cluster-capacity.md)은 중요한 단계입니다.  하지만 이 빠른 시작의 경우 응용 프로그램을 실행하지 않으므로 *DS1_v2 표준* VM 크기를 선택합니다.  Hello에 대 한 "Silver"를 선택 [안정성 계층](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) 초기 가상 컴퓨터 크기는 5의 용량을 설정 합니다.  

    사용자 지정 끝점 hello 클러스터에서 실행 중인 응용 프로그램과 연결할 수 있도록 hello Azure 부하 분산 장치에 포트를 엽니다.  포트 80 및 8172를 "80, 8172" tooopen를 입력 합니다.

    Hello 검사 안 함 **고급 설정 구성** TCP/HTTP 관리 끝점, 응용 프로그램 포트 범위를 사용자 지정에 사용 되는 상자 [배치 제약 조건](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), 및 [용량 속성](service-fabric-cluster-resource-manager-metrics.md)합니다.    

    **확인**을 선택합니다.

6. Hello에 **클러스터 구성** 양식에서 설정 **진단** 너무**에**합니다.  이 빠른 시작에 대 한 불필요 tooenter 어떤 [패브릭 설정](service-fabric-cluster-fabric-settings.md) 속성입니다.  **패브릭 버전**선택, **자동** Microsoft hello 버전의 hello 클러스터를 실행 하는 hello 패브릭 코드를 자동으로 업데이트 되도록 모드를 업그레이드 합니다.  너무 hello 모드 설정**수동** 너무 하려는 경우[지원 되는 버전 선택](service-fabric-cluster-upgrade.md) tooupgrade를 합니다. 

    ![노드 유형 구성][node-type-config]

    **확인**을 선택합니다.

7. Hello 채울 **보안** 폼입니다.  이 빠른 시작의 경우 **보안 해제**를 선택합니다.  그러나이 뛰어납니다 toocreate 프로덕션 작업에 대 한 보안 클러스터 하므로 권장 익명으로 tooan 보안 되지 않은 클러스터에 연결 하 고 관리 작업을 수행할 수 누구나 합니다.  

    인증서 서비스 패브릭 tooprovide toosecure 인증 및 암호화에에서 사용 되는 클러스터 및 해당 응용 프로그램의 다양 한 측면입니다. Service Fabric에서 인증서가 사용되는 방식에 대한 자세한 내용은 [Service Fabric 클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.  응용 프로그램 보안에 대 한 Azure Active Directory 또는 tooset 인증서를 사용 하 여 tooenable 사용자 인증 [리소스 관리자 템플릿에서 클러스터를 만드는](service-fabric-cluster-creation-via-arm.md)합니다.

    **확인**을 선택합니다.

8. 검토 hello를 요약 합니다.  입력 hello 설정에서 작성 된 리소스 관리자 템플릿을 toodownload 원하는 경우, 선택 **템플릿 및 매개 변수를 다운로드**합니다.  선택 **만들기** toocreate hello 클러스터입니다.

    Hello 알림이 hello 만들기 진행률을 볼 수 있습니다. (근처 hello 상태 표시줄 hello 오른쪽 상단의 화면에 "hello"벨 아이콘을 클릭 합니다.) 클릭 한 경우 **Pin tooStartboard** 참조 hello 클러스터를 만드는 동안 **서비스 패브릭 클러스터 배포** toohello 고정 **시작** 보드 합니다.

### <a name="view-cluster-status"></a>클러스터 상태 보기
클러스터를 만든 후 hello에서 클러스터를 검사할 수 있습니다 **개요** 블레이드 hello 포털에서입니다. 이제 클러스터 대시보드에 hello hello 클러스터의 공용 끝점 및 링크 tooService 패브릭 탐색기 등의 hello 세부 정보를 볼 수 있습니다.

![클러스터 상태][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>서비스 패브릭 탐색기를 사용 하 여 hello 클러스터 시각화
[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)는 클러스터를 시각화하고 응용 프로그램을 관리할 수 있는 좋은 도구입니다.  서비스 패브릭 탐색기는 hello 클러스터에서 실행 되는 서비스입니다.  웹 브라우저를 사용 하 여 hello를 클릭 하 여 액세스할 **서비스 패브릭 탐색기** hello 클러스터의 링크 **개요** hello 포털의 페이지입니다.  Hello 브라우저에 직접 hello 주소를 입력할 수도 있습니다: [http://quickstartcluster.westus.cloudapp.azure.com:19080/탐색기](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)

hello 클러스터 대시보드는 응용 프로그램 및 노드 상태 요약을 포함 하 여 클러스터에 대 한 개요를 제공 합니다. hello 노드 보기 hello hello 클러스터의 실제 레이아웃을 표시합니다. 지정된 노드의 경우 해당 노드에 배포된 코드를 가진 응용 프로그램을 검사할 수 있습니다.

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a>PowerShell을 사용 하 여 toohello 클러스터에 연결
PowerShell을 사용 하 여 연결 하 여 해당 hello 클러스터가 실행 중인지 확인 합니다.  hello ServiceFabric PowerShell 모듈이 설치 된 hello로 [서비스 패브릭 SDK](service-fabric-get-started.md)합니다.  hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet은 연결 toohello 클러스터를 설정 합니다.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
참조 [연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md) 연결 tooa 클러스터의 다른 예입니다. 연결 toohello 클러스터 후 hello를 사용 하 여 [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello 클러스터 및 상태 정보를 각 노드에 대 한 노드 목록입니다. **HealthState**는 노드마다 *OK* 상태여야 합니다.

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a>Hello 클러스터 제거
서비스 패브릭 클러스터 구성 된 다른 Azure 리소스로 또한 자체 toohello 클러스터 리소스입니다. Toocompletely 서비스 패브릭 클러스터를 삭제 하므로 toodelete 모든 hello 리소스 구성 되어 있어야 합니다. hello 가장 간단한 방법은 toodelete hello 클러스터와 사용 하는 모든 hello 리소스 toodelete hello 리소스 그룹입니다. 다른 방법으로 toodelete 클러스터 나 toodelete 리소스 그룹의 일부 (모두는 아니지만) hello 리소스 참조에 대 한 [클러스터를 삭제](service-fabric-cluster-delete.md)

Hello Azure 포털에서에서 리소스 그룹을 삭제 합니다.
1. 원하는 toodelete toohello 서비스 패브릭 클러스터를 이동 합니다.
2. Hello 클릭 **리소스 그룹** hello 클러스터 essentials 페이지 이름입니다.
3. Hello에 **리소스 그룹 Essentials** 페이지 **리소스 그룹 삭제** hello 리소스 그룹의 해당 페이지 toocomplete hello 삭제 시 hello 지침을 따릅니다.
    ![Hello 리소스 그룹 삭제][cluster-delete]


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a>Azure Powershell toodeploy 보안 클러스터를 사용 하 여
1. Hello 다운로드 [Azure Powershell 모듈 버전 4.0 이상이](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) 컴퓨터에 있습니다.

2. 다음 명령을 실행 hello Windows PowerShell 창을 엽니다. 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    출력 유사한 toohello 다음을 표시 되어야 합니다.

    ![ps-list][ps-list]

3. 로그인 tooAzure 및 선택 hello 구독 toowhich toocreate hello 클러스터

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. 다음 명령은 toonow 실행된 hello 보안 클러스터를 만듭니다. Toocustomize hello 매개 변수를 잊지 마십시오. 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    hello 명령에서 10 분 too30 분 toocomplete hello 끝 부분에서 아무 곳 이나 사용할 수 있는, 출력 유사한 toohello 다음을 얻어야 합니다. hello 출력 hello 인증서를 업로드, KeyVault hello에 대 한 정보 및 hello 로컬 폴더 hello 인증서 복사 합니다. 

    ![ps-out][ps-out]

5. Hello 전체 출력 복사한 toorefer tooit 필요 하므로 tooa 텍스트 파일을 저장 합니다. Hello hello 출력에서 다음 정보를 기록해 둡니다. 

    - **CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx
    - **CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10
    - **ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080
    - **ClientConnectionEndpointPort** : 19000

### <a name="install-hello-certificate-on-your-local-machine"></a>로컬 컴퓨터에 hello 인증서 설치
  
tooconnect toohello 클러스터 hello 현재 사용자의 개인 (My) 저장소 hello로 tooinstall hello 인증서가 필요 합니다. 

다음 PowerShell hello를 실행 합니다.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

준비 tooconnect tooyour 보안 클러스터가 나타납니다.

### <a name="connect-tooa-secure-cluster"></a>Tooa 보안 클러스터에 연결 

다음 PowerShell 명령을 tooconnect tooa 보안 클러스터 hello를 실행 합니다. hello 인증서 세부 정보는 hello 클러스터를 사용 하는 tooset 했던 인증서를 일치 해야 합니다. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


다음 예제에서는 hello hello 매개 변수를 완료 합니다. 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

다음 명령 toocheck 연결 하 고 hello 클러스터 상태가 정상이 hello를 실행 합니다.

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a>Visual Studio에서 앱 tooyour 클러스터 게시

에 Azure 클러스터를 설정 했으므로 다음 hello 하 여 Visual Studio에서 응용 프로그램 tooit 프로그램을 게시할 수 있습니다 [게시 tooan 클러스터](service-fabric-publish-app-remote-cluster.md) 문서. 

### <a name="remove-hello-cluster"></a>Hello 클러스터 제거
클러스터 구성 된 다른 Azure 리소스로 또한 자체 toohello 클러스터 리소스입니다. hello 가장 간단한 방법은 toodelete hello 클러스터와 사용 하는 모든 hello 리소스 toodelete hello 리소스 그룹입니다. 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a>다음 단계
에 개발 클러스터를 설정 했으므로 hello 다음을 시도해 보십시오.
* [Hello 포털에서 보안 클러스터 만들기](service-fabric-cluster-creation-via-portal.md)
* [템플릿에서 클러스터 만들기](service-fabric-cluster-creation-via-arm.md) 
* [PowerShell을 사용하여 앱 배포](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
