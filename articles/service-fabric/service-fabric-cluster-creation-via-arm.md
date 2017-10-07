---
title: "서식 파일에서 aaaCreate Azure 서비스 패브릭 클러스터 | Microsoft Docs"
description: "이 문서에서는 클라이언트 인증을 위해 Azure 리소스 관리자, Azure 주요 자격 증명 모음 및 Azure Active Directory (Azure AD)를 사용 하 여 Azure에서 클러스터를 보안 서비스 패브릭 tooset 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a>Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기
> [!div class="op_single_selector"]
> * [Azure 리소스 관리자](service-fabric-cluster-creation-via-arm.md)
> * [Azure Portal](service-fabric-cluster-creation-via-portal.md)
>
>

Azure Resource Manager를 사용하여 Azure에 보안 Azure Service Fabric 클러스터를 설정하는 단계를 안내하는 단계별 가이드입니다. 에서는 승인 해당 hello 문서 깁니다. 그럼에도 불구 하 고 않으면 hello 콘텐츠로 철저 하 게 알고 이미 있다면 수 있는지 toofollow 각 단계 신중 하 게 합니다.

hello 가이드에서는 다음 절차를 수행 하는 hello에 설명 합니다.

* 클러스터 및 응용 프로그램 보안에 대 한 Azure 키 자격 증명 모음 tooupload 인증서는 설정
* Azure Resource Manager를 사용하여 Azure에 보안 클러스터 만들기
* 클러스터 관리를 위해 Azure Active Directory(Azure AD)를 사용하여 사용자 인증

보안 클러스터는 클러스터 무단된 액세스 toomanagement 작업을 수행할 수 있습니다. 배포, 업그레이드 및 삭제 하는 중 응용 프로그램, 서비스 및 포함 된 hello 데이터 포함 합니다. 보안 되지 않은 클러스터는 누구 든 지 tooat 언제 든 지 연결 고 관리 작업을 수행할 수는 클러스터. 가능한 toocreate 보안 되지 않은 클러스터는 아니지만 hello 처음부터 보안 클러스터를 만드는 것이 좋습니다. 비보안 클러스터는 나중에 보안 클러스터로 만들 수 없으므로 새 클러스터를 만들어야 합니다.

hello 개념 만드는 보안 클러스터의 Linux 또는 Windows 클러스터 되었든 관계 없이 동일 하지만, hello 됩니다. 자세한 내용 및 보안 Linux 클러스터 만들기를 위한 도우미 스크립트는 [Linux에서 보안 클러스터 만들기](#secure-linux-clusters)를 참조하세요.

## <a name="sign-in-tooyour-azure-account"></a>Azure 계정 tooyour에 로그인
이 가이드에서는 [Azure PowerShell][azure-powershell]을 사용합니다. 새 PowerShell 세션을 시작할 때 tooyour Azure 계정에에서 로그인 하 고 Azure 명령을 실행 하기 전에 구독을 선택 합니다.

Azure 계정 tooyour에 로그인 합니다.

```powershell
Login-AzureRmAccount
```

구독을 선택합니다.

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a>Key Vault 설정
이 섹션에서는 Azure에서 Service Fabric 클러스터에 대해서와 Service Fabric 응용 프로그램에 대해서 Key Vault를 만드는 단계를 살펴봅니다. 완벽 가이드 tooAzure 주요 자격 증명 모음에 대 한 참조 toohello [키 자격 증명 모음 시작 가이드][key-vault-get-started]합니다.

서비스 패브릭 X.509 인증서 toosecure 클러스터를 사용 하 고 응용 프로그램 보안 기능을 제공 합니다. Azure에서 서비스 패브릭 클러스터에 대 한 주요 자격 증명 모음 toomanage 인증서를 사용합니다. Azure에서 클러스터를 배포 하는 경우 서비스 패브릭 클러스터 만들기를 담당 하는 hello Azure 리소스 공급자에서 키 자격 증명 모음 인증서를 끌어온 hello 클러스터 Vm에 설치 합니다.

hello 다음 다이어그램에서는 Azure 키 자격 증명 모음, 서비스 패브릭 클러스터 및 클러스터를 만들 때 주요 자격 증명 모음에 저장 된 인증서를 사용 하는 hello Azure 리소스 공급자 사이의 hello 관계 수행 합니다.

![인증서 설치 다이어그램][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>리소스 그룹 만들기
hello 첫 번째 단계는 toocreate 주요 자격 증명 모음 용으로 특별히 리소스 그룹입니다. 리소스 그룹에 hello 주요 자격 증명 모음을 두는 것이 좋습니다. 이 작업에는 hello 계산 및 저장소 리소스 그룹이 포함 된 그룹 키 및 암호를 손실 하지 않고 서비스 패브릭 클러스터를 포함 하는 hello 리소스 그룹을 제거할 수 있습니다. 주요 자격 증명 모음을 포함 하는 hello 리소스 그룹 _hello에 있어야 동일한 지역_ 가 사용 하는 hello 클러스터로 합니다.

여러 지역에서 toodeploy 클러스터를 계획 하는 경우 hello 키 자격 증명 모음에 속해 있는 영역을 표시 하는 방법 및 hello 리소스 그룹 이름을 지정 하는 것이 좋습니다.  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
hello 출력은 다음과 같이 표시 됩니다.

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a>Hello 새 리소스 그룹에서 주요 자격 증명 모음 만들기
hello 주요 자격 증명 모음 _배포를 설정 해야_ tooallow에서 계산 리소스 공급자 tooget 인증서 hello 및 가상 컴퓨터 인스턴스에서 설치:

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

hello 출력은 다음과 같이 표시 됩니다.

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a>기존 Key Vault 사용

기존 키 자격 증명 모음, toouse 있습니다 _배포에 대 한 활성화 해야_ tooallow에서 계산 리소스 공급자 tooget 인증서 hello 및 클러스터 노드에 설치:

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a>인증서 tooyour 자격 증명 모음 키를 추가 합니다.

인증서 서비스 패브릭 tooprovide toosecure 인증 및 암호화에에서 사용 되는 클러스터 및 해당 응용 프로그램의 다양 한 측면입니다. Service Fabric에서 인증서가 사용되는 방식에 대한 자세한 내용은 [Service Fabric 클러스터 보안 시나리오][service-fabric-cluster-security]를 참조하세요.

### <a name="cluster-and-server-certificate-required"></a>클러스터 및 서버 인증서(필수)
이 인증서는 필수 toosecure 클러스터 및 tooit 무단된 액세스를 방지 합니다. 다음 두 방법으로 클러스터 보안을 제공합니다.

* 클러스터 인증: 클러스터 페더레이션을 위해 노드 간 통신을 인증합니다. 이 인증서와 함께 자신의 신분을 증명 노드만 hello 클러스터에 가입할 수 있습니다.
* 서버 인증: 알 수 있도록 hello 관리 클라이언트 toohello 실제 클러스터와 통신할 hello 클러스터 관리 끝점 tooa 관리 클라이언트를 인증 합니다. 이 인증서 또한 제공 SSL hello HTTPS 관리 API에 대 한 서비스 패브릭 탐색기에 대 한 HTTPS를 통해 합니다.

tooserve 이러한으로 hello 인증서 요구 사항을 준수 하는 hello를 충족 해야 합니다.

* hello 인증서 개인 키를 포함 해야 합니다.
* 개인 정보 교환 (.pfx) 파일 tooa를 내보낼 수 있는 키 교환에 대 한 hello 인증서를 만들어야 합니다.
* hello 인증서의 주체 이름은 tooaccess hello 서비스 패브릭 클러스터를 사용 하는 hello 도메인을 일치 해야 합니다. 이 일치는 필요한 tooprovide hello 클러스터의 HTTPS 관리 끝점에 대 한 SSL 및 서비스 패브릭 탐색기입니다. Hello에 대 한 인증 기관 (CA)에서 SSL 인증서를 가져올 수 없습니다. cloudapp.azure.com 도메인입니다. 클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다. CA에서 인증서를 요청할 때 hello 인증서의 주체 이름은 일치 해야 합니다 클러스터에 대해 사용 하는 hello 사용자 지정 도메인 이름.

### <a name="application-certificates-optional"></a>응용 프로그램 인증서(선택 사항)
응용 프로그램 보안을 위해 클러스터에 제한 없는 수의 인증서를 추가로 설치할 수 있습니다. 클러스터를 만들기 전에 hello 응용 프로그램 보안 시나리오를 같은 hello 노드에 설치 하는 인증서 toobe를 필요로 하는 것이 좋습니다.

* 응용 프로그램 구성 값의 암호화 및 암호 해독
* 복제 중에 노드 간 데이터 암호화

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Azure 리소스 공급자 사용을 위한 인증서 서식 지정
Key Vault를 통해 개인 키 파일(.pfx)을 직접 추가하여 사용할 수 있습니다. 그러나 hello Azure 계산 리소스 공급자에는 특별 한 개체 JSON (JavaScript Notation) 형식으로 저장 된 키 toobe가 필요 합니다. hello 형식에는 기본 64로 인코딩된 문자열 및 개인 키 암호 hello로 hello.pfx 파일로를 포함 됩니다. tooaccommodate hello JSON 문자열에 배치 하 고 "secrets" hello 키에로 저장 한 다음 키 해야 이러한 요구 사항을 자격 증명 모음입니다.

이 프로세스는 더 쉽게 toomake는 [PowerShell 모듈은 GitHub에서 사용할 수 있는][service-fabric-rp-helpers]합니다. toouse hello 모듈 다음 hello지 않습니다.

1. 로컬 디렉터리에 hello hello 리포지토리의 전체 콘텐츠를 다운로드 합니다.
2. Toohello 로컬 디렉터리를 이동 합니다.
2. PowerShell 창에 hello ServiceFabricRPHelpers 모듈을 가져옵니다.

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

hello `Invoke-AddCertToKeyVault` 이 PowerShell 모듈에서 명령을 자동으로 인증서 개인 키를 JSON 문자열로 서식을 지정 하 고 toohello 주요 자격 증명 모음에 업로드 합니다. Hello 명령 tooadd hello 클러스터 인증서 및 모든 추가 응용 프로그램 인증서 toohello 주요 자격 증명 모음을 사용 합니다. 클러스터에 tooinstall 포함 하려는 경우 추가 인증서에 대해이 단계를 반복 합니다.

#### <a name="uploading-an-existing-certificate"></a>기존 인증서 업로드

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

여기에 표시 된 하나 hello 같은 오류가 발생할 경우에 일반적으로 리소스 URL 충돌이 있는지 의미 합니다. hello 주요 자격 증명 모음 이름 변경 tooresolve hello 충돌 합니다.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Hello 충돌을 해결 한 후 hello 출력은 다음과 같이 표시 됩니다.

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
>Hello 세 위의 문자열, CertificateThumbprint, SourceVault, 및 CertificateURL, tooset tooobtain 및 보안 서비스 패브릭 클러스터를 응용 프로그램 보안을 위해 사용 하 고 있는 모든 응용 프로그램 인증서가 필요 합니다. Hello 문자열을 저장 하지 않으면 어려운 tooretrieve hello 키를 쿼리하여 해당 자격 증명 모음에 나중에 가능 합니다.

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a>자체 서명 된 인증서를 만들고 toohello 주요 자격 증명 모음 업로드

주요 자격 증명 인증서 toohello 모음을 이미 업로드 하는 경우이 단계를 건너뜁니다. 이 단계는 tooyour 주요 자격 증명 모음에 업로드 하 고 새 자체 서명 된 인증서를 생성 합니다. 다음 스크립트는 hello hello 매개 변수를 변경 하 고 다음 실행 후 인증서 암호를 입력 해야 합니다.  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

여기에 표시 된 하나 hello 같은 오류가 발생할 경우에 일반적으로 리소스 URL 충돌이 있는지 의미 합니다. tooresolve hello 충돌, hello 주요 자격 증명 모음 이름 변경, RG 이름 및 등입니다.

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

Hello 충돌을 해결 한 후 hello 출력은 다음과 같이 표시 됩니다.

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
>Hello 세 위의 문자열, CertificateThumbprint, SourceVault, 및 CertificateURL, tooset tooobtain 및 보안 서비스 패브릭 클러스터를 응용 프로그램 보안을 위해 사용 하 고 있는 모든 응용 프로그램 인증서가 필요 합니다. Hello 문자열을 저장 하지 않으면 어려운 tooretrieve hello 키를 쿼리하여 해당 자격 증명 모음에 나중에 가능 합니다.

 이 시점에서 요소를에서 다음 hello가 있어야 합니다.

* hello 주요 자격 증명 모음 리소스 그룹입니다.
* 안녕 주요 자격 증명 모음 및 해당 URL (SourceVault hello PowerShell 출력 앞에).
* hello 클러스터 서버 인증 인증서 및 hello 주요 자격 증명 모음에서 해당 URL입니다.
* hello 응용 프로그램 인증서 및 hello 키 자격 증명 모음에 사이트의 Url입니다.


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a>클라이언트 인증에 대한 Azure Active Directory 설정

Azure AD 조직 (테 넌 트 라고) toomanage 사용자 액세스 tooapplications를 수 있습니다. 응용 프로그램은 웹 기반 로그인 UI를 갖는 항목과 네이티브 클라이언트 환경을 갖는 항목으로 나뉩니다. 이 문서에서는 이미 테넌트를 만들었다고 가정합니다. 하지 않은 경우 먼저 읽으십시오 [tooget Azure Active Directory 테 넌 트][active-directory-howto-tenant]합니다.

서비스 패브릭 클러스터는 웹 기반 hello를 포함 하 여 관리 기능을 몇 가지 항목 지점 tooits 제공 [서비스 패브릭 탐색기] [ service-fabric-visualizing-your-cluster] 및 [Visual Studio] [service-fabric-manage-application-in-visual-studio]. 결과적으로, toocontrol 액세스 toohello 클러스터에 대 한 두 개의 Azure AD 응용 프로그램, 웹 응용 프로그램 및 한 네이티브 응용 프로그램을 만듭니다.

서비스 패브릭 클러스터를 사용 하 여 Azure AD를 구성에 관련 hello 단계 중 일부는 toosimplify, Windows PowerShell 스크립트 집합을 작성 했습니다.

> [!NOTE]
> Hello hello 클러스터를 만들기 전에 다음 단계를 완료 해야 합니다. Hello 스크립트에 예상 되는 클러스터 이름 및 끝점 때문에 hello 값 계획 해야 하 고 값을 이미 만든 하지 않습니다.

1. [Hello 스크립트 다운로드] [ sf-aad-ps-script-download] tooyour 컴퓨터입니다.
2. 마우스 오른쪽 단추로 클릭 hello zip 파일을 선택 **속성**선택, hello **차단 해제** 확인란을 선택한 다음 클릭 **적용**합니다.
3. Hello zip 파일을 추출 합니다.
4. 실행 `SetupApplications.ps1`, hello TenantId를 ClusterName, 및 WebApplicationReplyUrl 매개 변수로 제공 합니다. 예:

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    Hello PowerShell 명령을 실행 하 여 프로그램 TenantId를 찾을 수 있습니다 `Get-AzureSubscription`합니다. 모든 구독에 대 한 hello TenantId 표시이 명령을 실행 합니다.

    ClusterName는 hello 스크립트에 의해 만들어진 사용 되는 tooprefix hello Azure AD 응용 프로그램입니다. 않아도 toomatch hello 실제 클러스터 이름을 정확 하 게 합니다. 것이 유일한 toomake 의도 한 것으로 사용 되는 보다 쉽게 Azure AD toomap 아티팩트 toohello 서비스 패브릭 클러스터입니다.

    WebApplicationReplyUrl은 Azure AD 로그인 후 tooyour 사용자가 반환 하는 hello 기본 끝점입니다. 기본적으로 클러스터에 대 한 hello 서비스 패브릭 탐색기 끝점으로이 끝점을 설정 합니다.

    https://&lt;cluster_domain&gt;:19080/Explorer

    Hello Azure AD 테 넌 트에 대 한 관리자 권한이 있는 tooan 계정에서 증명된 toosign 됩니다. 에 로그인 한 후 hello 스크립트가 만듭니다 hello 웹 및 네이티브 응용 프로그램 toorepresent 서비스 패브릭 클러스터. Hello의 hello 테 넌 트의 응용 프로그램을 확인 하면 [Azure 클래식 포털][azure-classic-portal], 새 항목 두 개 표시 됩니다.

   * *ClusterName*\_클러스터
   * *ClusterName*\_클라이언트

   hello 스크립트 hello Azure Resource Manager 템플릿에 좋습니다 tookeep hello PowerShell 창을 이므로 hello 다음 단원의 hello 클러스터를 만들 때 필요한 JSON 열 hello를 인쇄 합니다.

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a>서비스 패브릭 클러스터 Resource Manager 템플릿 만들기
이 섹션에서는 hello 서비스 패브릭 클러스터 리소스 관리자 템플릿을 PowerShell 명령을 사용 하는 hello 앞의 출력 합니다.

예제 리소스 관리자 템플릿을 hello에서 사용할 수 있는 [GitHub의 Azure 빠른 시작 템플릿 갤러리][azure-quickstart-templates]합니다. 이러한 템플릿은 클러스터 템플릿의 시작점으로 사용할 수 있습니다.

### <a name="create-hello-resource-manager-template"></a>Hello 리소스 관리자 템플릿 만들기
이 가이드에서는 hello [5 노드 보안 클러스터] [ service-fabric-secure-cluster-5-node-1-nodetype] 예제 템플릿과 템플릿 매개 변수입니다. 다운로드 `azuredeploy.json` 및 `azuredeploy.parameters.json` tooyour 컴퓨터 하 고 원하는 텍스트 편집기에서 두 파일을 엽니다.

### <a name="add-certificates"></a>인증서 추가
Hello 주요 자격 증명 모음 hello 인증서 키가 포함 된 참조 하 여 인증서 tooa 클러스터 리소스 관리자 템플릿을 추가 합니다. 리소스 관리자 템플릿 매개 변수 파일에 키 자격 증명 모음 값 hello를 배치 하는 것이 좋습니다. 이렇게 유지 hello 리소스 관리자 템플릿 파일 다시 사용할 수 있고 특정 tooa 배포 값이 없는 합니다.

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a>모든 인증서 toohello 가상 컴퓨터 크기 집합 osProfile 추가
Hello 클러스터에 설치 된 모든 인증서는 hello 눈금 집합 리소스 (Microsoft.Compute/virtualMachineScaleSets)의 hello osProfile 섹션에 구성 되어야 합니다. 이 작업에는 hello 리소스 공급자 tooinstall hello 인증서 hello Vm에 지시합니다. 이 설치는 hello 클러스터 인증서와 응용 프로그램에 대 한 toouse를 계획 하는 모든 응용 프로그램 보안 인증서를 모두 포함 되어 있습니다.

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a>Hello 서비스 패브릭 클러스터 인증서 구성
두 hello 서비스 패브릭 클러스터 리소스 (Microsoft.ServiceFabric/clusters) hello 클러스터 인증 인증서로 구성 되어 있어야 하 고 hello 가상 컴퓨터 크기 조정 집합 리소스에 설정 하는 가상 컴퓨터 크기에 대 한 서비스 패브릭 확장 hello 합니다. 이 정렬을 hello 서비스 패브릭 리소스 공급자 tooconfigure 사용 하면 클러스터 인증 및 관리 끝점에 대 한 서버 인증에 사용 하기 위해 합니다.

##### <a name="virtual-machine-scale-set-resource"></a>가상 컴퓨터 확장 집합 리소스:
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a>서비스 패브릭 리소스:
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a>Azure AD 구성 삽입
Azure AD hello 구성 이전에 만든 서식 파일에 리소스 관리자에 직접 삽입할 수 있습니다. 그러나 먼저 매개 변수 파일 tookeep hello 리소스 관리자 템플릿 재사용에 hello 값을 추출 하는 값 특정 tooa 배포는 것이 좋습니다.

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <a "configure-arm" ></a>Resource Manager 템플릿 매개 변수 구성
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
마지막으로 hello 주요 자격 증명 모음 및 Azure AD PowerShell 명령 toopopulate hello 매개 변수 파일에서 hello 출력 값을 사용 합니다.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
이 시점에서 요소를에서 다음 hello가 있어야 합니다.

* Key Vault 리소스 그룹
  * 주요 자격 증명 모음
  * 클러스터 서버 인증 인증서
  * 데이터 암호화 인증서
* Azure Active Directory 테넌트
  * 웹 기반 관리 및 Service Fabric Explorer에 대한 Azure AD 응용 프로그램
  * 네이티브 클라이언트 관리에 대한 Azure AD 응용 프로그램
  * 사용자 및 할당된 역할
* 서비스 패브릭 클러스터 Resource Manager 템플릿
  * Key Vault를 통해 구성된 인증서
  * 구성된 Azure Active Directory

다이어그램을 다음 hello 주요 자격 증명 모음 및 Azure AD 구성 리소스 관리자 서식 파일에 필요한 경우를 보여 줍니다.

![리소스 관리자 종속성 맵][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a>Hello 클러스터 만들기
현재 위치는 준비 toocreate hello 클러스터를 사용 하 여 [Azure 리소스 템플릿 배포][resource-group-template-deploy]합니다.

#### <a name="test-it"></a>테스트
다음 PowerShell 명령을 tootest hello를 리소스 관리자 템플릿을 사용 하 여 매개 변수 파일:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a>배포
Hello 리소스 관리자 템플릿 테스트 통과 하는 경우 다음 PowerShell 명령을 toodeploy hello 사용자 리소스 관리자 템플릿을 사용 매개 변수 파일:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a>사용자가 tooroles 할당
Hello 응용 프로그램 toorepresent 클러스터를 만든 후 사용자가 서비스 패브릭에서 지 원하는 toohello 역할을 할당: 읽기 전용 및 관리자 Hello를 사용 하 여 hello 역할을 할당할 수 있습니다 [Azure 클래식 포털][azure-classic-portal]합니다.

1. Hello Azure 포털에서에서 tooyour 테 넌 트를 선택한 후 선택 **응용 프로그램**합니다.
2. Hello 웹 응용 프로그램을 선택 이름이 같은 `myTestCluster_Cluster`합니다.
3. Hello 클릭 **사용자** 탭 합니다.
4. 사용자 tooassign를 선택 하 고 hello를 클릭 한 다음 **할당** hello hello 화면 맨 아래에 단추입니다.

    ![할당 사용자 tooroles 단추][assign-users-to-roles-button]
5. Hello 역할 tooassign toohello 사용자를 선택 합니다.

    !["사용자 지정" 대화 상자][assign-users-to-roles-dialog]

> [!NOTE]
> 서비스 패브릭의 역할에 대한 자세한 내용은 [서비스 패브릭 클라이언트의 역할 기반 액세스 제어](service-fabric-cluster-security-roles.md)를 참조하세요.
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a>Linux에서 보안 클러스터 만들기
제공 된 보다 쉽게 toomake hello 프로세스는 [도우미 스크립트](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux)합니다. 이 도우미 스크립트를 사용하기 전에 먼저 Azure CLI(명령줄 인터페이스)를 설치했으며 해당 경로에 있는지 확인합니다. Hello 스크립트를 실행 하 여 사용 권한을 tooexecute에 있는지 확인 `chmod +x cert_helper.py` 다운로드 한 후 합니다. hello 첫 번째 단계 hello로 CLI를 사용 하 여 toosign tooyour Azure 계정에에서는 `azure login` 명령입니다. Tooyour Azure 계정이 로그인 한 후 해당 CA 사용 하 여 hello 도우미 스크립트 서명 된 인증서를 hello 다음 명령으로:

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

hello-ifile 매개 변수는 hello 인증서 종류 (pfx 또는 pem, 또는 자체 서명 된 인증서 경우 ss)을 입력으로.pfx 파일 또는.pem 파일 걸릴 수 있습니다.
hello 매개 변수-h hello 도움말 텍스트 한 출력합니다.


이 명령은 hello 세 개의 문자열 hello 출력으로 다음을 반환 합니다.

* Hello에 대 한 hello id는 SourceVaultID를 생성 하는 새 KeyVault 리소스 그룹
* Hello 인증서에 액세스 하기 위한 CertificateUrl
* 인증에 사용되는 CertificateThumbprint 

다음 예제는 hello toouse 명령 hello 하는 방법을 보여 줍니다.

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
앞에 다음과 같은 세 개의 문자열을 hello 명령을 제공 하는 hello를 실행 하는 중:

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

hello 인증서의 주체 이름은 tooaccess hello 서비스 패브릭 클러스터를 사용 하는 hello 도메인을 일치 해야 합니다. 이 항목은 필요한 tooprovide hello 클러스터의 HTTPS 관리 끝점에 대 한 SSL 및 서비스 패브릭 탐색기입니다. Hello에 대 한 CA에서 SSL 인증서를 가져올 수 없습니다 `.cloudapp.azure.com` 도메인입니다. 클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다. CA에서 인증서를 요청할 때 hello 인증서의 주체 이름은 일치 해야 합니다 클러스터에 대해 사용 하는 hello 사용자 지정 도메인 이름.

주체 이름에 이러한 항목이 hello toocreate (Azure AD) 없이 보안 서비스 패브릭 클러스터를 필요에 설명 된 대로 [리소스 관리자 구성 템플릿 매개 변수](#configure-arm)합니다. 에 대 한 hello 지침에 따라 toohello 보안 클러스터를 연결할 수 있습니다 [클라이언트 액세스 tooa 클러스터 인증](service-fabric-connect-to-secure-cluster.md)합니다. Linux 미리 보기 클러스터에서는 Azure AD 인증을 지원하지 않습니다. Hello에 설명 된 대로 관리자 및 클라이언트 역할을 할당할 수 [역할 toousers 할당](#assign-roles) 섹션. Linux 미리 보기 클러스터에 대 한 관리 및 클라이언트 역할을 지정 하면 인증에 인증서 지문을 tooprovide 해야 합니다. (제공 하지 않으면 hello 주체 이름 체인 유효성 검사 또는 해지 없습니다이 미리 보기 릴리스에서 수행 하므로.)

테스트를 위해 toouse 자체 서명 된 인증서를 원하는 경우 사용할 수 있습니다 하나는 동일한 스크립트 toogenerate hello 합니다. Hello 플래그를 제공 하 여 hello 인증서 tooyour 주요 자격 증명 모음을 업로드 한 다음 `ss` hello 인증서 경로 및 인증서 이름을 제공 하는 대신 합니다. 예를 들어 다음 명령을 만들고 자체 서명 된 인증서를 업로드 하기 위한 hello 참조:

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
이 명령은 반환 동일한 세 개의 문자열 hello: SourceVault, CertificateUrl, 및 CertificateThumbprint 합니다. 보안 Linux 클러스터와 hello 자체 서명 된 인증서를 배치할 위치 모두에 hello 문자열 toocreate 유도할 수 있습니다. Hello 자체 서명 된 인증서 tooconnect toohello 클러스터를 해야합니다. 에 대 한 hello 지침에 따라 toohello 보안 클러스터를 연결할 수 있습니다 [클라이언트 액세스 tooa 클러스터 인증](service-fabric-connect-to-secure-cluster.md)합니다.

hello 인증서의 주체 이름은 tooaccess hello 서비스 패브릭 클러스터를 사용 하는 hello 도메인을 일치 해야 합니다. 이 항목은 필요한 tooprovide hello 클러스터의 HTTPS 관리 끝점에 대 한 SSL 및 서비스 패브릭 탐색기입니다. Hello에 대 한 CA에서 SSL 인증서를 가져올 수 없습니다 `.cloudapp.azure.com` 도메인입니다. 클러스터에 대한 사용자 지정 도메인 이름을 획득해야 합니다. CA에서 인증서를 요청할 때 hello 인증서의 주체 이름은 일치 해야 합니다 클러스터에 대해 사용 하는 hello 사용자 지정 도메인 이름.

Hello에 설명 된 대로 hello 도우미 스크립트 hello Azure 포털에서에서 hello 매개 변수를 채울 수 [hello Azure 포털에서에서 클러스터 만들기](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) 섹션.

## <a name="next-steps"></a>다음 단계
이제 Azure Active Directory를 사용하여 관리 인증을 제공하는 보안 클러스터가 생겨났습니다. 그런 다음, [tooyour 클러스터 연결](service-fabric-connect-to-secure-cluster.md) 너무 방법을 알아봅니다[응용 프로그램 암호 관리](service-fabric-application-secret-management.md)합니다.

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a>클라이언트 인증에 대한 Azure Active Directory 설정 문제 해결
클라이언트 인증을 위해 Azure AD를 설정 하는 동안 문제를 실행 하면이 섹션의 hello 잠재적 해결 방법을 검토 합니다.

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a>서비스 패브릭 탐색기 tooselect 인증서 라는 메시지가 표시
#### <a name="problem"></a>문제
서비스 패브릭 탐색기에서 AD tooAzure 성공적으로 로그인 한 후에 hello 브라우저 toohello 홈 페이지를 반환 하지만 tooselect 인증서 라는 메시지가 나타납니다.

![SFX 인증서 선택 대화 상자][sfx-select-certificate-dialog]

#### <a name="reason"></a>이유
hello 사용자 hello Azure AD 클러스터 응용 프로그램에서에서 역할을 할당 되지 않습니다. 이 때문에 Service Fabric 클러스터에서 Azure AD 인증이 실패합니다. 서비스 패브릭 탐색기 대신 toocertificate 인증 합니다.

#### <a name="solution"></a>해결 방법
Azure AD를 설정 하기 위한 지침을 hello 하 고 사용자 역할을 할당 합니다. 또한 "사용자 할당 필요 tooaccess app" 설정 하는 것이 `SetupApplications.ps1` 않습니다.

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a>PowerShell 사용한 연결 오류가 발생 하면서 실패: "hello 지정 된 자격 증명이 올바르지 않습니다".
#### <a name="problem"></a>문제
오류가 발생 하 여 hello 연결이 실패 tooAzure AD 성공적으로 로그인 한 후에 "AzureActiveDirectory" 보안 모드를 사용 하 여 PowerShell tooconnect toohello 클러스터를 사용할 때는: "hello" 지정 된 자격 증명이 올바르지 않습니다.

#### <a name="solution"></a>해결 방법
이 솔루션은 hello 앞서 hello와 동일 합니다.

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a>로그인할 때 Service Fabric Explorer가 실패를 반환함: "AADSTS50011"
#### <a name="problem"></a>문제
서비스 패브릭 탐색기에서 tooAzure AD에서에서 toosign을 시도할 때 hello 페이지에서 오류를 반환 하는: "AADSTS50011: 회신 주소 hello &lt;url&gt; hello 응용 프로그램으로 구성 된 hello 회신 주소와 일치 하지 않습니다: &lt;guid&gt;."

![SFX 회신 주소가 일치하지 않습니다.][sfx-reply-address-not-match]

#### <a name="reason"></a>이유
서비스 패브릭 탐색기를 나타내는 hello 클러스터 (웹) 응용 프로그램이 Azure AD에 대해 tooauthenticate를 시도 하 고 hello 리디렉션 반환 URL hello 요청의 일부로 제공 합니다. Hello URL hello Azure AD 응용 프로그램에 나열 되지 않은 하지만 **회신 URL** 목록입니다.

#### <a name="solution"></a>해결 방법
Hello에 **구성** hello 탭 (웹) 응용 프로그램을 클러스터의 경우 추가 hello 서비스 패브릭 탐색기 URL toohello **회신 URL** 나열 하거나 hello hello 목록의 항목 중 하나를 대체 합니다. 마친 후 변경 사항을 저장합니다.

![웹 응용 프로그램 회신 URL][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a>PowerShell 통해 Azure AD 인증을 사용 하 여 hello 클러스터에 연결
서비스 패브릭 클러스터 tooconnect hello 다음 PowerShell 명령 예제는 hello를 사용 합니다.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

toolearn hello Connect-servicefabriccluster cmdlet에 대 한 참조 [Connect-servicefabriccluster](https://msdn.microsoft.com/library/mt125938.aspx)합니다.

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a>여러 개의 클러스터에 hello 동일한 Azure AD 테 넌 트를 다시 사용할 수 있습니까?
예. 그러나 tooadd hello 서비스 패브릭 탐색기 URL tooyour 클러스터 (웹) 응용 프로그램. 그러지 않으면 Service Fabric Explorer가 작동하지 않습니다.

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a>Azure AD가 사용되도록 설정된 경우에도 서버 인증서가 계속 필요한 이유는 무엇인가요?
FabricClient와 FabricGateway는 상호 인증을 수행합니다. Azure AD 인증 하는 동안 Azure AD 통합 id toohello 서버는 클라이언트를 제공 하 고 hello 서버 인증서가 사용 되는 tooverify hello 서버 id입니다. Service Fabric 인증서에 대한 자세한 내용은 [X.509 인증서 및 Service Fabric][x509-certificates-and-service-fabric]을 참조하세요.

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

