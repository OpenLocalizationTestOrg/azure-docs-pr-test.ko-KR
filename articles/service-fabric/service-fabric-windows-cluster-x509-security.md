---
title: "인증서를 사용 하 여 Windows Azure 서비스 패브릭 aaaSecure 클러스터 | Microsoft Docs"
description: "이 문서에서는 hello 독립 실행형 내에서 또는 개인 toosecure 통신도: 클라이언트와 hello 클러스터 클러스터 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: fe0ed74c-9af5-44e9-8d62-faf1849af68c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dekapur
ms.openlocfilehash: f0d411963615349a84edfc8125dec4ee5908f146
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-using-x509-certificates"></a>X.509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보호
이 문서에서는 어떻게 간의 toosecure hello 통신 hello 독립 실행형 Windows 클러스터의 다양 한 노드는 방법과 tooauthenticate 연결 하는 클라이언트 toothis 클러스터 X.509 인증서를 사용 하 여 설명 합니다. 이렇게 하는 권한이 있는 사용자는 hello 클러스터를 액세스할 수 있습니다 hello 배포 된 응용 프로그램 관리 작업을 수행 합니다.  Hello 클러스터가 생성 될 때 hello 클러스터에 대 한 인증서 보안을 설정 해야 합니다.  

노드 간 보안, 클라이언트-노드 보안 및 역할 기반 액세스 제어와 같은 클러스터 보안에 대한 자세한 내용은 [클러스터 보안 시나리오](service-fabric-cluster-security.md)를 참조하세요.

## <a name="which-certificates-will-you-need"></a>어떤 인증서가 필요한가요?
toostart [hello 독립 실행형 클러스터 패키지를 다운로드](service-fabric-cluster-creation-for-windows-server.md#downloadpackage) tooone hello 노드 클러스터에 있습니다. Hello에 다운로드 한 패키지를 찾을 수 있습니다는 **ClusterConfig.X509.MultiMachine.json** 파일입니다. Hello 파일을 열고 한 hello 섹션을 검토 **보안** hello에서 **속성** 섹션:

```JSON
"security": {
    "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
    "ClusterCredentialType": "X509",
    "ServerCredentialType": "X509",
    "CertificateInformation": {
        "ClusterCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },        
        "ClusterCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ServerCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ServerCertificateCommonNames": {
            "CommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]"
            }
            ],
            "X509StoreName": "My"
        },
        "ClientCertificateThumbprints": [
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": false
            },
            {
                "CertificateThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ClientCertificateCommonNames": [
            {
                "CertificateCommonName": "[CertificateCommonName]",
                "CertificateIssuerThumbprint": "[Thumbprint]",
                "IsAdmin": true
            }
        ],
        "ReverseProxyCertificate": {
            "Thumbprint": "[Thumbprint]",
            "ThumbprintSecondary": "[Thumbprint]",
            "X509StoreName": "My"
        },
        "ReverseProxyCertificateCommonNames": {
            "CommonNames": [
                {
                "CertificateCommonName": "[CertificateCommonName]"
                }
            ],
            "X509StoreName": "My"
        }
    }
},
```

이 섹션에서는 독립 실행형 Windows 클러스터 보안 설정에 필요한 hello 인증서를 설명 합니다. 클러스터 인증서를 지정 하는 경우 설정의 hello 값 **ClusterCredentialType** too_**X509**_합니다. 외부 연결에 대 한 서버 인증서를 지정 하는 경우 설정 hello **ServerCredentialType** 너무_**X509**_합니다. 하지만 필수는 아니지만 좋습니다 toohave 올바르게 보호 클러스터에 대 한 이러한 두 인증서를. 이러한 값을 너무 설정*X509* hello 해당 인증서 또는 서비스 패브릭에서 예외를 throw 합니다도 지정 해야 합니다. 일부 시나리오에서는 경우에 좋습니다 toospecify hello _ClientCertificateThumbprints_ 또는 _ReverseProxyCertificate_합니다. 이러한 시나리오에서는 필요한 설정 하면 _ClusterCredentialType_ 또는 _ServerCredentialType_ too_X509_합니다.


> [!NOTE]
> A [지문](https://en.wikipedia.org/wiki/Public_key_fingerprint) hello 인증서의 기본 id입니다. 읽기 [방법을 인증서의 지문을 tooretrieve](https://msdn.microsoft.com/library/ms734695.aspx) toofind 만드는 hello 인증서의 지문 hello 아웃 합니다.
> 
> 

hello 다음 표에 클러스터 설치에서 필요한 hello 인증서.

| **CertificateInformation 설정** | **설명** |
| --- | --- |
| ClusterCertificate |테스트 환경에 권장됩니다. 이 인증서는 hello 노드 클러스터 간의 필요한 toosecure hello 통신입니다. 업그레이드에 두 개의 다른 인증서, 기본 및 보조 인증서를 사용할 수 있습니다. Hello에 hello 기본 인증서의 지문 hello 설정 **지문** 섹션과 hello hello에 보조의 **ThumbprintSecondary** 변수입니다. |
| ClusterCertificateCommonNames |프로덕션 환경에 권장됩니다. 이 인증서는 hello 노드 클러스터 간의 필요한 toosecure hello 통신입니다. 하나 또는 두 개의 클러스터 인증서 일반 이름을 사용할 수 있습니다. |
| ServerCertificate |테스트 환경에 권장됩니다. 이 인증서는 tooconnect toothis 클러스터를 읽으려고 할 때 toohello 클라이언트를 표시 됩니다. 편의 위해 toouse를 선택할 수 있습니다에 대 한 인증서 같은 hello *ClusterCertificate* 및 *ServerCertificate*합니다. 업그레이드에 두 개의 다른 서버 인증서, 기본 및 보조 인증서를 사용할 수 있습니다. Hello에 hello 기본 인증서의 지문 hello 설정 **지문** 섹션과 hello hello에 보조의 **ThumbprintSecondary** 변수입니다. |
| ServerCertificateCommonNames |프로덕션 환경에 권장됩니다. 이 인증서는 tooconnect toothis 클러스터를 읽으려고 할 때 toohello 클라이언트를 표시 됩니다. 편의 위해 toouse를 선택할 수 있습니다에 대 한 인증서 같은 hello *ClusterCertificateCommonNames* 및 *ServerCertificateCommonNames*합니다. 하나 또는 두 개의 서버 인증서 일반 이름을 사용할 수 있습니다. |
| ClientCertificateThumbprints |Tooinstall hello 인증 클라이언트에서 인증서의 집합입니다. Tooallow 액세스 toohello 클러스터 hello 컴퓨터에 설치 된 다른 클라이언트 인증서의 수를 할 수 있습니다. Hello에 각 인증서의 지문을 hello 설정 **CertificateThumbprint** 변수입니다. Hello를 설정한 경우 **IsAdmin** 너무*true*, 다음에 설치 된이 인증서를 사용 하 여 hello 클라이언트 관리자 hello 클러스터에서 관리 작업 수행 수입니다. 경우 hello **IsAdmin** 은 *false*,이 인증서를 사용 하 여 hello 클라이언트 사용자 액세스 권한, 일반적으로 읽기 전용에 대 한 hello 작업에만 수행할 수 있습니다. 역할에 대한 자세한 내용은 [RBAC(역할 기반 액세스 제어)](service-fabric-cluster-security.md#role-based-access-control-rbac) |
| ClientCertificateCommonNames |집합 hello 일반 이름 hello 첫 번째 클라이언트 인증서의 hello에 대 한 **CertificateCommonName**합니다. hello **CertificateIssuerThumbprint** 이 인증서의 발급자 hello hello 지문입니다. 읽기 [인증서 작업](https://msdn.microsoft.com/library/ms731899.aspx) tooknow 일반 이름 및 발급자 hello에 대 한 자세한 합니다. |
| ReverseProxyCertificate |테스트 환경에 권장됩니다. 이것은 사용할 수 있는 선택적 인증서는 toosecure 하려는 경우 지정 된 프로그램 [역방향 프록시](service-fabric-reverseproxy.md)합니다. 이 인증서를 사용하는 경우 reverseProxyEndpointPort가 nodeTypes로 설정되어야 합니다. |
| ReverseProxyCertificateCommonNames |프로덕션 환경에 권장됩니다. 이것은 사용할 수 있는 선택적 인증서는 toosecure 하려는 경우 지정 된 프로그램 [역방향 프록시](service-fabric-reverseproxy.md)합니다. 이 인증서를 사용하는 경우 reverseProxyEndpointPort가 nodeTypes로 설정되어야 합니다. |

다음은 hello 클러스터, 서버 및 클라이언트 인증서 제공 된 클러스터 구성의 예입니다. 클러스터에 대 한 참고 사항 / 서버 reverseProxy 인증서, 지문 및 일반 이름이 허용 되지 않습니다 toobe 구성 함께 hello에 대 한 동일한 / 인증서 종류가 있습니다.

 ```JSON
 {
    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "2016-09-26",
    "nodes": [{
        "nodeName": "vm0",
        "metadata": "Replace hello localhost below with valid IP address or FQDN",
        "iPAddress": "10.7.0.5",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "iPAddress": "10.7.0.4",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "10.7.0.6",
        "metadata": "Replace hello localhost with valid IP address or FQDN",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],
    "properties": {
        "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
        }
        "security": {
            "metadata": "hello Credential type X509 indicates this is cluster is secured using X509 Certificates. hello thumbprint format is - d5 ec 42 3b 79 cb e5 07 fd 83 59 3c 56 b9 d5 31 24 25 42 64.",
            "ClusterCredentialType": "X509",
            "ServerCredentialType": "X509",
            "CertificateInformation": {
                "ClusterCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myClusterCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ServerCertificateCommonNames": {
                  "CommonNames": [
                    {
                      "CertificateCommonName": "myServerCertCommonName"
                    }
                  ],
                  "X509StoreName": "My"
                },
                "ClientCertificateThumbprints": [{
                    "CertificateThumbprint": "c4 c18 8e aa a8 58 77 98 65 f8 61 4a 0d da 4c 13 c5 a1 37 6e",
                    "IsAdmin": false
                }, {
                    "CertificateThumbprint": "71 de 04 46 7c 9e d0 54 4d 02 10 98 bc d4 4c 71 e1 83 41 4e",
                    "IsAdmin": true
                }]
            }
        },
        "reliabilityLevel": "Bronze",
        "nodeTypes": [{
            "name": "NodeType0",
            "clientConnectionEndpointPort": "19000",
            "clusterConnectionEndpointPort": "19001",
            "leaseDriverEndpointPort": "19002",
            "serviceConnectionEndpointPort": "19003",
            "httpGatewayEndpointPort": "19080",
            "applicationPorts": {
                "startPort": "20001",
                "endPort": "20031"
            },
            "ephemeralPorts": {
                "startPort": "20032",
                "endPort": "20062"
            },
            "isPrimary": true
        }
         ],
        "fabricSettings": [{
            "name": "Setup",
            "parameters": [{
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
            }, {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
            }]
        }]
    }
}
 ```

## <a name="certificate-roll-over"></a>인증서 롤오버
지문 대신 인증서 일반 이름을 사용하는 경우 인증서 롤오버를 위해 클러스터 구성을 업그레이드하지 않아도 됩니다.
인증서 롤오버 발급자 포함 되는 경우 롤오버 하십시오 hello 인증서 저장소에 발급자 인증서를 이전 하는 hello을 hello 새 발급자 인증서를 설치한 후 2 시간 이상 유지 합니다.

## <a name="acquire-hello-x509-certificates"></a>Hello X.509 인증서를 획득 합니다.
hello 클러스터 내에서 toosecure 통신을 먼저 해야 tooobtain X.509 인증서 클러스터 노드에 대 한. 또한 toolimit 연결 toothis tooauthorized 컴퓨터/사용자가 클러스터, tooobtain 필요 하 고 hello 클라이언트 컴퓨터에 대 한 인증서를 설치 합니다.

프로덕션 작업을 실행 하는 클러스터에 사용할지는 [인증 기관 (CA)](https://en.wikipedia.org/wiki/Certificate_authority) X.509 인증서 toosecure hello 클러스터 서명 합니다. 이러한 인증서를 얻는 방법에 자세한 이동 너무[하는 방법: 인증서 얻기](http://msdn.microsoft.com/library/aa702761.aspx)합니다.

테스트를 위해 사용 하는 클러스터를 toouse 자체 서명 된 인증서를 선택할 수 있습니다.

## <a name="optional-create-a-self-signed-certificate"></a>선택 사항: 자체 서명된 인증서 만들기
한 가지 방법은 toocreate 올바르게 보호 될 수 있는 자체 서명 된 인증서는 toouse hello *CertSetup.ps1* hello 디렉터리의 hello 서비스 패브릭 SDK 폴더에 스크립트 *C:\Program Files\Microsoft SDKs\Service Fabric\ ClusterSetup\Secure*합니다. Hello 인증서의이 파일 toochange hello 기본 이름을 편집 (hello 값 찾기 위해 *CN = ServiceFabricDevClusterCert*). 이 스크립트를 `.\CertSetup.ps1 -Install`로 실행합니다.

이제 보호 된 암호로 hello 인증서 tooa PFX 파일을 내보냅니다. 먼저 hello 인증서의 지문을 hello를 가져옵니다. Hello에서 *시작* hello 실행 메뉴 *컴퓨터 인증서 관리*합니다. Toohello 이동 **Local Computer\Personal** 폴더 및 hello 방금 인증서 찾기 생성 합니다. Hello 인증서 tooopen를 두 번 클릭이 선택 hello *세부 정보* 탭과 toohello 아래로 스크롤하여 *지문* 필드입니다. Hello 공백을 제거한 후 아래 hello PowerShell 명령으로 스크립팅 hello 지문 값을 복사 합니다.  변경 hello `String` 및 PowerShell에서 다음 실행된 hello tooa 적합 한 보안 암호 tooprotect 값:

```powershell   
$pswd = ConvertTo-SecureString -String "1234" -Force –AsPlainText
Get-ChildItem -Path cert:\localMachine\my\<Thumbprint> | Export-PfxCertificate -FilePath C:\mypfx.pfx -Password $pswd
```

hello에 설치 하는 인증서의 toosee hello 세부 사항을 컴퓨터 있습니다 hello 다음 PowerShell 명령을 실행할 수 있습니다.

```powershell
$cert = Get-Item Cert:\LocalMachine\My\<Thumbprint>
Write-Host $cert.ToString($true)
```

또는 Azure 구독을 보유 하는 경우 수행 hello 섹션 [추가 자격 증명 모음 인증서 tooKey](service-fabric-cluster-creation-via-arm.md#add-certificate-to-key-vault)합니다.

## <a name="install-hello-certificates"></a>Hello 인증서 설치
인증서를 만든 후에 hello 클러스터 노드에 설치할 수 있습니다. 노드가 필요 toohave Windows PowerShell 최신 hello 3.x에 설치 되어 있습니다. 클러스터와 서버 인증서 및 모든 보조 인증서에 대 한 각 노드에서 이러한 단계 toorepeat를 해야 합니다.

1. Hello.pfx 파일 toohello 노드를 복사 합니다.
2. 관리자 권한으로 PowerShell 창을 열고 다음 명령 hello를 입력 합니다. Hello 대체 *$pswd* hello 암호를 사용 하 여 toocreate이이 인증서를 사용 합니다. Hello 대체 *$PfxFilePath* hello.pfx 복사한 toothis 노드의 hello 전체 경로 포함 합니다.
   
    ```powershell
    $pswd = "1234"
    $PfxFilePath ="C:\mypfx.pfx"
    Import-PfxCertificate -Exportable -CertStoreLocation Cert:\LocalMachine\My -FilePath $PfxFilePath -Password (ConvertTo-SecureString -String $pswd -AsPlainText -Force)
    ```
3. 이제 hello 네트워크 서비스 계정에서 실행 되는 hello 서비스 패브릭 프로세스 hello 다음 스크립트를 실행 하 여 사용할 수 있도록이 인증서에 hello 액세스 제어를 설정 합니다. Hello 인증서와 hello 서비스 계정에 대해 "NETWORK SERVICE"의 hello 지문을 제공 합니다. Hello 인증서에 열어 hello 인증서에 해당 hello Acl이 올바른지 확인할 수 있습니다 *시작* > *컴퓨터 인증서 관리* 살펴보고 *모든작업*  >  *개인 키 관리*합니다.
   
    ```powershell
    param
    (
    [Parameter(Position=1, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$pfxThumbPrint,
   
    [Parameter(Position=2, Mandatory=$true)]
    [ValidateNotNullOrEmpty()]
    [string]$serviceAccount
    )
   
    $cert = Get-ChildItem -Path cert:\LocalMachine\My | Where-Object -FilterScript { $PSItem.ThumbPrint -eq $pfxThumbPrint; }
   
    # Specify hello user, hello permissions and hello permission type
    $permission = "$($serviceAccount)","FullControl","Allow"
    $accessRule = New-Object -TypeName System.Security.AccessControl.FileSystemAccessRule -ArgumentList $permission
   
    # Location of hello machine related keys
    $keyPath = Join-Path -Path $env:ProgramData -ChildPath "\Microsoft\Crypto\RSA\MachineKeys"
    $keyName = $cert.PrivateKey.CspKeyContainerInfo.UniqueKeyContainerName
    $keyFullPath = Join-Path -Path $keyPath -ChildPath $keyName
   
    # Get hello current acl of hello private key
    $acl = (Get-Item $keyFullPath).GetAccessControl('Access')
   
    # Add hello new ace toohello acl of hello private key
    $acl.SetAccessRule($accessRule)
   
    # Write back hello new acl
    Set-Acl -Path $keyFullPath -AclObject $acl -ErrorAction Stop
   
    # Observe hello access rights currently assigned toothis certificate.
    get-acl $keyFullPath| fl
    ```
4. 각 서버 인증서에 대 한 위의 hello 단계를 반복 합니다. 이러한 단계 tooinstall hello 클라이언트 hello 컴퓨터에 있는 인증서 tooallow 액세스 toohello 클러스터를 사용할 수 있습니다.

## <a name="create-hello-secure-cluster"></a>Hello 보안 클러스터 만들기
Hello를 구성한 후 **보안** hello 섹션 **ClusterConfig.X509.MultiMachine.json** 파일을 이동 하려면 너무[클러스터를 만듭니다](service-fabric-cluster-creation-for-windows-server.md#createcluster) 섹션 tooconfigure 노드 hello 고 hello 독립 실행형 클러스터를 만듭니다. Toouse hello 기억 **ClusterConfig.X509.MultiMachine.json** hello 클러스터를 만드는 동안 파일입니다. 예를 들어 명령 hello 다음과 같을 수 있습니다.

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

독립 실행형 Windows 성공적으로 실행 중인 클러스터 및 인증 된 클라이언트 tooconnect tooit hello, hello 섹션에 따라 설치 프로그램을 보안 hello 있으면 [PowerShell을 사용 하 여 연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md#connectsecurecluster) tooconnect tooit 합니다. 예:

```powershell
$ConnectArgs = @{  ConnectionEndpoint = '10.7.0.5:19000';  X509Credential = $True;  StoreLocation = 'LocalMachine';  StoreName = "MY";  ServerCertThumbprint = "057b9544a6f2733e0c8d3a60013a58948213f551";  FindType = 'FindByThumbprint';  FindValue = "057b9544a6f2733e0c8d3a60013a58948213f551"   }
Connect-ServiceFabricCluster $ConnectArgs
```

이 클러스터와 다른 PowerShell 명령을 toowork를 실행할 수 있습니다. 예를 들어 [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode.md?view=azureservicefabricps) tooshow이 보안 클러스터에서 노드 목록이 있습니다.


tooremove hello 클러스터 hello 서비스 패브릭 패키지를 다운로드 하는 hello 클러스터에서 노드 toohello 연결 명령줄 열고 toohello 패키지 폴더를 이동 합니다. 이제 hello 다음 명령을 실행 합니다.

```powershell
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.X509.MultiMachine.json
```

> [!NOTE]
> 잘못 된 인증서 구성에서 배포 중에 나오는 hello 클러스터가 되지 않을 수 있습니다. tooself-보안 문제를 진단, 이벤트 뷰어 그룹에서 참조 하십시오 *Applications and Services Logs* > *Microsoft 서비스 패브릭*합니다.
> 
> 

