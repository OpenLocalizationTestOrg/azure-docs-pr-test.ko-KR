---
title: "서비스 패브릭 aaaCreate hello Azure 포털에 있는 클러스터 | Microsoft Docs"
description: "이 문서에서는 Azure 포털 및 Azure 키 자격 증명 모음 사용 하 여 Azure에서 보안 서비스 패브릭 클러스터를 tooset hello 하는 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 Azure에서 서비스 패브릭 클러스터 만들기
> [!div class="op_single_selector"]
> * [Azure 리소스 관리자](service-fabric-cluster-creation-via-arm.md)
> * [Azure 포털](service-fabric-cluster-creation-via-portal.md)
> 
> 

이 hello Azure 포털을 사용 하 여 Azure에서 보안 서비스 패브릭 클러스터를 설정 하는 hello 단계를 안내 하는 방법을 단계별로 설명 합니다. 이 가이드에서는 hello 다음 단계를 안내 합니다.

* 클러스터 보안에 대 한 주요 자격 증명 모음 toomanage 키를 설정 합니다.
* Azure의 hello Azure 포털을 통해 보안 된 클러스터를 만듭니다.
* 인증서를 사용하여 관리자를 인증합니다.

> [!NOTE]
> Azure Active Directory를 사용한 사용자 인증 및 응용 프로그램 보안에 대한 인증서 설정 등의 고급 보안 옵션을 사용하려면 [Azure Resource Manager를 사용하여 클러스터를 만듭니다][create-cluster-arm].
> 
> 

보안 클러스터는 배포, 업그레이드 및 응용 프로그램, 서비스 및 포함 된 hello 데이터 삭제를 포함 하는 무단된 액세스 toomanagement 작업을 수행할 수 하는 클러스터입니다. 보안 되지 않은 클러스터는 누구 든 지 tooat 언제 든 지 연결 고 관리 작업을 수행할 수는 클러스터. 가능한 toocreate 보안 되지 않은 클러스터는 아니지만 **보안 클러스터 toocreate을 적극 권장**합니다. 비보안 클러스터는 **나중를 보안될 수 없습니다** -새 클러스터를 만들어야 합니다.

hello 개념 hello 클러스터는 Linux 클러스터 또는 Windows 클러스터 보안 클러스터를 만들기 위한 동일한 hello 됩니다. 자세한 내용 및 보안 Linux 클러스터 만들기를 위한 도우미 스크립트는 [Linux에서 보안 클러스터 만들기](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters)를 참조하세요. hello hello 도우미 스크립트를 제공 하 여 가져오는 매개 변수 입력 될 수 hello 포털에 직접 hello 섹션에 설명 된 대로 [hello Azure 포털에서에서 클러스터 만들기](#create-cluster-portal)합니다.

## <a name="log-in-tooazure"></a>TooAzure 로그인
이 가이드에서는 [Azure PowerShell][azure-powershell]을 사용합니다. 새 PowerShell 세션을 시작할 때 tooyour Azure 계정이 로그인 하 고 Azure 명령을 실행 하기 전에 구독을 선택 합니다.

Tooyour azure 계정에 로그인 합니다.

```powershell
Login-AzureRmAccount
```

구독을 선택합니다.

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>주요 자격 증명 모음 설정
Hello 가이드의이 부분에서는 주요 자격 증명 모음에서 Azure 서비스 패브릭 클러스터에 대 한 및 서비스 패브릭 응용 프로그램을 만드는 과정을 안내 합니다. 주요 자격 증명 모음에 완전 한 설명서 참조 hello [키 자격 증명 모음 시작 가이드][key-vault-get-started]합니다.

서비스 패브릭 X.509 인증서 toosecure 클러스터를 사용합니다. Azure 키 자격 증명 모음에는 azure에서 서비스 패브릭 클러스터에 대 한 인증서 사용된 toomanage입니다. Azure에서 클러스터를 배포 하는 경우 hello Azure 리소스 공급자 서비스 패브릭 클러스터 만들기를 담당 주요 자격 증명 모음에서 인증서를 끌어온 hello 클러스터 Vm에 설치 합니다.

hello 다음 다이어그램에서는 키 자격 증명 모음, 서비스 패브릭 클러스터 및 클러스터를 만들 때 주요 자격 증명 모음에 저장 된 인증서를 사용 하는 hello Azure 리소스 공급자 사이의 hello 관계 수행 합니다.

![인증서 설치][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>리소스 그룹 만들기
hello 첫 번째 단계는 toocreate 주요 자격 증명 모음에 맞게 새 리소스 그룹입니다. 주요 자격 증명 모음 자체 리소스 그룹 넣는 것이 좋습니다-와 같은 서비스 패브릭 클러스터에 있는 hello 리소스 그룹-계산 및 저장소 리소스 그룹을 제거할 수 있도록 키와 암호를 손실 하지 않고. 주요 자격 증명 모음에 있는 hello 리소스 그룹 hello에 있어야 합니다. 사용 중인 hello 클러스터와 동일한 영역입니다.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>주요 자격 증명 모음 만들기
Hello 새 리소스 그룹에서 주요 자격 증명 모음을 만듭니다. 주요 자격 증명 모음 hello **배포를 설정 해야** tooallow 서비스 패브릭에서 리소스 공급자 tooget 인증서 hello 및 클러스터 노드에 설치:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

기존 주요 자격 증명 모음이 있는 경우라면 Azure CLI를 사용하여 배포에 대해 사용하도록 설정할 수 있습니다.

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>자격 증명 모음 인증서 tooKey 추가
인증서 서비스 패브릭 tooprovide toosecure 인증 및 암호화에에서 사용 되는 클러스터 및 해당 응용 프로그램의 다양 한 측면입니다. Service Fabric에서 인증서가 사용되는 방식에 대한 자세한 내용은 [Service Fabric 클러스터 보안 시나리오][service-fabric-cluster-security]를 참조하세요.

### <a name="cluster-and-server-certificate-required"></a>클러스터 및 서버 인증서(필수)
이 인증서는 필수 toosecure 클러스터 및 tooit 무단된 액세스를 방지 합니다. 다음 몇 가지 방법으로 클러스터 보안을 제공합니다.

* **클러스터 인증:** 클러스터 페더레이션에 대한 노드 간 통신을 인증합니다. 이 인증서와 함께 자신의 신분을 증명 노드만 hello 클러스터에 가입할 수 있습니다.
* **서버 인증:** 알 수 있도록 hello 관리 클라이언트 toohello 실제 클러스터와 통신할 hello 클러스터 관리 끝점 tooa 관리 클라이언트를 인증 합니다. 이 인증서 또한 제공 SSL hello HTTPS 관리 API에 대 한 서비스 패브릭 탐색기에 대 한 HTTPS를 통해 합니다.

tooserve 이러한으로 hello 인증서 요구 사항을 준수 하는 hello를 충족 해야 합니다.

* hello 인증서 개인 키를 포함 해야 합니다.
* 키 교환, 내보낼 수 있는 tooa 개인 정보 교환 (.pfx) 파일에 대 한 hello 인증서를 만들어야 합니다.
* hello 인증서의 주체 이름이 같아야 hello 사용 되는 도메인 tooaccess hello 서비스 패브릭 클러스터 합니다. 이 hello 클러스터의 HTTPS 관리 끝점 및 서비스 패브릭 탐색기에 대 한 SSL tooprovide 필요 합니다. Hello에 대 한 인증 기관 (CA)에서 SSL 인증서를 가져올 수 없습니다 `.cloudapp.azure.com` 도메인입니다. 클러스터에 대한 사용자 지정 도메인 이름을 획득합니다. 요청 하는 경우 CA hello 인증서의 주체 이름에서 발급 한 인증서 클러스터에 사용 되는 hello 사용자 지정 도메인 이름이 일치 해야 합니다.

### <a name="client-authentication-certificates"></a>클라이언트 인증 인증서
추가 클라이언트 인증서가 클러스터 관리 작업을 위해 관리자를 인증합니다. 서비스 패브릭은 **관리자** 및 **읽기 전용 사용자**의 두 가지 액세스 수준을 제공합니다. 최소한 관리 액세스에 대해 단일 인증서를 사용해야 합니다. 추가 사용자 수준 액세스를 위해서는 별도 인증서를 제공해야 합니다. 액세스 역할에 대한 자세한 내용은 [Service Fabric 클라이언트의 역할 기반 액세스 제어][service-fabric-cluster-security-roles]를 참조하세요.

Tooupload 클라이언트 인증 인증서 tooKey 자격 증명 모음 toowork 서비스 패브릭 필요가 없습니다. 이러한 인증서는 클러스터 관리에 대 한 권한이 있는 사용자만 toousers 제공 toobe만 필요 합니다. 

> [!NOTE]
> Azure Active Directory는 hello 권장 클러스터에 대 한 방식으로 tooauthenticate 클라이언트 관리 작업입니다. Azure Active Directory toouse 해야 [Azure 리소스 관리자를 사용 하 여 클러스터 만들기][create-cluster-arm]합니다.
> 
> 

### <a name="application-certificates-optional"></a>응용 프로그램 인증서(선택 사항)
응용 프로그램 보안을 위해 클러스터에 제한 없는 수의 인증서를 추가로 설치할 수 있습니다. 클러스터를 만들기 전에 hello 응용 프로그램 보안 시나리오를 같은 hello 노드에 설치 하는 인증서 toobe를 필요로 하는 것이 좋습니다.

* 응용 프로그램 구성 값의 암호화 및 암호 해독
* 복제 중에 노드 간 데이터 암호화 

Hello Azure 포털을 통해 클러스터를 만들 때 응용 프로그램 인증서를 구성할 수 없습니다. 해야 tooconfigure 클러스터 설치 시 응용 프로그램 인증서를 [Azure 리소스 관리자를 사용 하 여 클러스터 만들기][create-cluster-arm]합니다. 만든 후에 응용 프로그램 인증서 toohello 클러스터를 추가할 수 있습니다.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Azure 리소스 공급자 사용을 위한 인증서 서식 지정
개인 키 파일(.pfx)을 추가하고 주요 자격 증명 모음을 통해 직접 사용할 수 있습니다. 그러나 hello Azure 리소스 공급자는 e-64로 인코딩된 문자열 및 hello 개인 키 암호도 hello.pfx를 포함 하는 특수 한 JSON 형식으로 저장 하는 키 toobe가 필요 합니다. 키 이러한 요구 사항을 JSON 문자열에 배치 하 고 다음으로 저장 해야 tooaccommodate *비밀* 키 자격 증명 모음에 있습니다.

이 프로세스는 쉽게 toomake, PowerShell 모듈은 [GitHub에서 사용할 수 있는][service-fabric-rp-helpers]합니다. 이러한 단계 toouse hello 모듈을 수행 합니다.

1. 로컬 디렉터리에 hello hello 리포지토리의 전체 콘텐츠를 다운로드 합니다. 
2. PowerShell 창에 hello 모듈을 가져옵니다.

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

hello `Invoke-AddCertToKeyVault` 이 PowerShell 모듈에서 명령을 자동으로 인증서 개인 키를 JSON 문자열로 서식을 지정 하 고 tooKey 자격 증명 모음에 업로드 합니다. Tooadd hello 클러스터 인증서 및 자격 증명 모음의 모든 추가 응용 프로그램 인증서 tooKey 사용 합니다. 클러스터에 tooinstall 포함 하려는 경우 추가 인증서에 대해이 단계를 반복 합니다.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

이러한 모든 hello 키 자격 증명 모음 필수 구성 요소는 노드 인증, 관리 끝점 보안 및 인증 및 모든 추가 응용 프로그램 보안에 대 한 인증서를 설치 하는 서비스 패브릭 클러스터 리소스 관리자 템플릿 구성 X.509 인증서를 사용 하는 기능. 이 시점에서 이제 있어야 다음과 같은 설정이 Azure의 hello:

* 주요 자격 증명 모음 리소스 그룹
  * 키 자격 증명 모음
    * 클러스터 서버 인증 인증서

</a "create-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Hello Azure 포털에서에서 클러스터 만들기
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Hello 서비스 패브릭 클러스터 리소스 검색
![hello Azure 포털에 서비스 패브릭 클러스터 서식 파일을 검색 합니다.][SearchforServiceFabricClusterTemplate]

1. Toohello 로그인 [Azure 포털][azure-portal]합니다.
2. 클릭 **새로** tooadd 새 리소스 템플릿이 있습니다. Hello에 hello 서비스 패브릭 클러스터 서식 파일에 대 한 검색 **마켓플레이스** 아래 **모든**합니다.
3. 선택 **서비스 패브릭 클러스터** hello 목록에서 합니다.
4. Toohello 이동 **서비스 패브릭 클러스터** 블레이드에서 클릭 **만들기**,
5. hello **만들 서비스 패브릭 클러스터** 블레이드는 hello 4 개 단계를 수행 합니다.

#### <a name="1-basics"></a>1. 기본 사항
![새 리소스 그룹 만들기 스크린샷][CreateRG]

Hello 기본 사항 블레이드에서 클러스터에 대해 tooprovide hello에 대 한 기본 정보가 필요 합니다.

1. 클러스터의 hello 이름을 입력 합니다.
2. 입력 한 **사용자 이름** 및 **암호** hello Vm에 대 한 원격 데스크톱에 대 한 합니다.
3. 있는지 tooselect hello 확인 **구독** 여러 구독이 있는 경우에 특히,에 배포 하 여 클러스터 toobe 되도록 합니다.
4. **새 리소스 그룹**을 만듭니다. 것이 가장 좋은 toogive을 찾아서 나중 toomake 변경 tooyour 배포 하려고 하거나 클러스터를 삭제 하는 경우에 특히 도움이 되었기 때문에 hello 클러스터와 동일한 이름의 hello 합니다.
   
   > [!NOTE]
   > Toouse 기존 리소스 그룹을 결정할 수 있습니다, 이지만 좋습니다 toocreate 새 리소스 그룹입니다. 이 통해 쉽게 toodelete 클러스터 필요 하지 않습니다.
   > 
   > 
5. 선택 hello **지역** toocreate hello 클러스터를 선택 합니다. 키 자격 증명 모음에 동일한 지역에는 hello를 사용 해야 합니다.

#### <a name="2-cluster-configuration"></a>2. 클러스터 구성
![노드 형식 만들기][CreateNodeType]

클러스터 노드를 구성합니다. 노드 형식은 hello VM 크기, Vm, hello 수 및 해당 속성을 정의합니다. 클러스터에서 둘 이상의 노드 형식이 아니라 hello 주 노드 유형 (첫 번째 hello 포털에서 정의 하는 hello)이 필요 합니다 5 개 이상의 Vm이 hello 노드 형식이 서비스 패브릭 시스템 서비스 포함 됩니다. "NodeTypeName"의 기본 배치 속성은 자동으로 추가되므로 **배치 속성** 을 구성하지 마세요.

> [!NOTE]
> 여러 노드 형식 사용에 대한 일반적인 시나리오는 프런트 엔드 서비스 및 백 엔드 서비스를 포함하는 응용 프로그램입니다. 포트 열기 toohello 인터넷으로 (예: D2 VM 크기) 보다 작은 Vm에서 tooput hello 프런트 엔드 서비스 지만 없는 인터넷 연결 포트가 열려 (D4, d 6, d, 15 등 VM 크기)을 통해 더 큰 Vm에서 tooput hello 백 엔드 서비스를 만들 합니다.
> 
> 

1. (1 too12 포함 하는 문자 문자와 숫자) 노드 유형에 대 한 이름을 선택 합니다.
2. 최소 hello **크기** 주 노드 hello에 대 한 vm 유형 hello에 의해 이루어집니다 **내구성** 계층 hello 클러스터에 대 한 선택 합니다. hello hello 내구성 계층에 대 한 기본값이 동입니다. 내구성에 자세한 내용은 참조 하십시오. [toochoose hello 서비스 패브릭 클러스터 안정성 및 지 속성 방법][service-fabric-cluster-capacity]합니다.
3. Hello VM 크기 및 가격 책정 계층을 선택 합니다. D 시리즈 VM에는 SSD 드라이브가 있으므로 특히 상태 저장 응용 프로그램에 권장됩니다. 부분 코어가 있거나 사용 가능한 디스크 용량이 7GB 미만인 VM SKU를 사용하지 마세요. 
4. 최소 hello **번호** 주 노드 hello에 대 한 vm 유형 사항에 의해 hello **안정성** 선택한 계층입니다. hello hello 안정성 계층에 대 한 기본값이 실버입니다. 안정성에 대 한 자세한 내용은 참조 하십시오. [toochoose hello 서비스 패브릭 클러스터 안정성 및 지 속성 방법][service-fabric-cluster-capacity]합니다.
5. Hello hello 노드 형식에 대 한 Vm 수를 선택 합니다. 위나 아래로 hello 노드 형식에서 Vm 수를 나중에 확장할 수 있지만 hello 기본 노드 형식에 최소 hello 하고자 하는 hello 안정성 수준에 의해 이루어집니다. 다른 노드 유형은 VM이 1대만 있어도 됩니다.
6. 사용자 지정 끝점을 구성합니다. 이 필드는 쉼표로 구분 된 목록이 hello Azure 부하 분산 장치 toohello 통해 tooexpose 포트 tooenter에서는 공용 인터넷 응용 프로그램에 대 한 합니다. 예를 들어 웹 응용 프로그램 tooyour 클러스터 toodeploy 하려는 경우 여기에 입력 "80" 클러스터에 포트 80에서 트래픽을 tooallow 합니다. 끝점에 대한 자세한 내용은 [응용 프로그램과 통신][service-fabric-connect-and-communicate-with-services]을 참조하세요.
7. 클러스터 **진단**을 구성합니다. 기본적으로 진단 문제를 해결 하 여 클러스터 tooassist에 활성화 됩니다. Toodisable 진단 hello를 변경 하려면 **상태** 너무 설정/해제**오프**합니다. 진단을 끄지 **않는** 것이 좋습니다.
8. 패브릭 클러스터 설정 하는 것이 원하는 모드를 업그레이드 하는 hello를 선택 합니다. 선택 **자동**hello 시스템 tooautomatically 선택 hello 사용 가능한 최신 버전을 선택 하 고 tooupgrade 클러스터 tooit, 합니다. 너무 hello 모드 설정**수동**toochoose 지원 되는 버전을 사용 하려는 경우.

> [!NOTE]
> 지원되는 버전의 Service Fabric이 실행되는 클러스터만 지원합니다. Hello를 선택 하 여 **수동** 모드에서 수행 하는 hello 책임 tooupgrade에 클러스터 지원 tooa 버전입니다. Hello Fabric 업그레이드 모드에 대 한 자세한 내용은 참조는 hello [패브릭 클러스터 업그레이드 서비스 문서입니다.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. 보안
![Azure 포털의 보안 구성 스크린샷][SecurityConfigs]

hello 마지막 단계는 hello 주요 자격 증명 모음 및 정보 앞에서 만든 인증서를 사용 하 여 tooprovide 인증서 정보 toosecure hello 클러스터입니다.

* Hello 업로드에서 가져온 hello 출력 hello 기본 인증서 필드를 채울 **클러스터 인증서** tooKey 자격 증명 모음 사용 하 여 hello `Invoke-AddCertToKeyVault` PowerShell 명령입니다.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Hello 확인 **고급 설정 구성** tooenter 클라이언트 인증서에 대 한 상자 **관리자 클라이언트** 및 **읽기 전용 클라이언트**합니다. 이러한 필드에 해당 하는 경우 관리자에 클라이언트 인증서의 지문 hello 및 읽기 전용 사용자 클라이언트 인증서의 지문 hello 입력 합니다. 관리자 tooconnect toohello 클러스터를 만들려고 여기에 입력 된 hello 지문 값과 일치 하는 지문이 있는 인증서가 있는 경우에 액세스가 부여 됩니다.  

#### <a name="4-summary"></a>4. 요약
!["배포 서비스 패브릭 클러스터."를 표시 하는 hello 시작 보드의 스크린 샷 ][Notifications]

toocomplete hello 클러스터 만들기 클릭 **요약** toosee hello 구성, 제공 하거나 다운로드 하는 hello Azure 리소스 관리자는 하는 데 사용 된 템플릿에 toodeploy 클러스터입니다. 필수 설정을 hello를 제공한 후 hello **확인** 단추 녹색 고 클릭 하 여 hello 클러스터를 만드는 프로세스를 시작할 수 있습니다.

Hello 알림이 hello 만들기 진행률을 볼 수 있습니다. (근처 hello 상태 표시줄 hello 오른쪽 상단의 화면에 "hello"벨 아이콘을 클릭 합니다.) 클릭 한 경우 **Pin tooStartboard** hello 클러스터를 만드는 동안 나타납니다 **서비스 패브릭 클러스터 배포** toohello 고정 **시작** 보드 합니다.

### <a name="view-your-cluster-status"></a>클러스터 상태 보기
![Hello 대시보드에 클러스터 세부 정보 스크린 샷][ClusterDashboard]

클러스터를 만든 후 hello 포털에서 클러스터를 검사할 수 있습니다.

1. 너무 이동**찾아보기** 클릭 **서비스 패브릭 클러스터**합니다.
2. 클러스터를 찾아 클릭합니다.
3. 이제 클러스터 대시보드에 hello hello 클러스터의 공용 끝점 및 링크 tooService 패브릭 탐색기 등의 hello 세부 정보를 볼 수 있습니다.

hello **노드 모니터** hello 클러스터 대시보드 블레이드에서 섹션 Vm 정상 및 비정상 hello 수를 나타냅니다. Hello 클러스터의 상태에 대 한 자세한 정보를 찾을 수 있습니다 [서비스 패브릭 상태 모델 소개][service-fabric-health-introduction]합니다.

> [!NOTE]
> 서비스 패브릭 클러스터 노드 toobe 항상 toomaintain 가용성을 특정 횟수를 필요로 하며 상태-참조 tooas "쿼럼을 유지 관리"를 유지 합니다. Therfore, 아니므로 일반적으로 hello 클러스터의 모든 컴퓨터를 안전 하 게 보호 tooshut 처음 수행 하지 않는 한는 [시/도의 전체 백업][service-fabric-reliable-services-backup-restore]합니다.
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>원격 연결 tooa 가상 컴퓨터 크기 집합 인스턴스 또는 클러스터 노드
클러스터 설치를 시작 하는 가상 컴퓨터 크기 집합의 결과에 지정 각각 hello NodeTypes 합니다. 참조 [원격 연결 tooa 가상 컴퓨터 크기 집합 인스턴스] [ remote-connect-to-a-vm-scale-set] 대 한 자세한 내용은 합니다.

## <a name="next-steps"></a>다음 단계
이제 관리 인증을 위해 인증서를 사용하는 보안 클러스터가 구축되었습니다. 그런 다음, [tooyour 클러스터 연결](service-fabric-connect-to-secure-cluster.md) 너무 방법을 알아봅니다[응용 프로그램 암호 관리](service-fabric-application-secret-management.md)합니다.  또한 [Service Fabric 지원 옵션](service-fabric-support.md)을 알아봅니다.

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
