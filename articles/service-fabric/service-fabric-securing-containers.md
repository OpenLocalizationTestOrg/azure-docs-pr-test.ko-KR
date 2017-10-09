---
title: "서비스 패브릭 컨테이너 보안 aaaAzure | Microsoft Docs"
description: "이제 toosecure 컨테이너 서비스에 알아봅니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88faf4e8f949c2f7743756b6272ca672d9710630
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="container-security"></a>컨테이너 보안

서비스 패브릭 (5.7 이상 버전)는 Windows 또는 Linux 클러스터의 hello 노드에 설치 되어 있는 인증서 컨테이너 tooaccess 내 서비스에 대 한 메커니즘을 제공 합니다. 또한 Service Fabric은 Windows 컨테이너에 gMSA(그룹 관리 서비스 계정)도 지원합니다. 

## <a name="certificate-management-for-containers"></a>컨테이너에 대한 인증서 관리

인증서를 지정하여 컨테이너 서비스를 보호할 수 있습니다. hello 클러스터의 노드에 hello hello 인증서를 설치 해야 합니다. hello 인증서 정보에에서 제공 됩니다 hello에서 응용 프로그램 매니페스트 hello `ContainerHostPolicies` hello 조각과 다음으로 태그:

```xml
  <ContainerHostPolicies CodePackageRef="NodeContainerService.Code">
    <CertificateRef Name="MyCert1" X509StoreName="My" X509FindValue="[Thumbprint1]"/>
    <CertificateRef Name="MyCert2" X509FindValue="[Thumbprint2]"/>
 ```

Hello 응용 프로그램을 시작할 때 hello 런타임 hello 인증서를 읽고 PFX 파일 및 각 인증서의 암호를 생성 합니다. 이 PFX 파일 및 암호는 hello 다음 환경 변수를 사용 하 여 hello 컨테이너 내에서 액세스할 수 있습니다: 

* **Certificate_[CodePackageName]_[CertName]_PFX**
* **Certificate_[CodePackageName]_[CertName]_Password**

hello 컨테이너 서비스 또는 프로세스는 hello 컨테이너로 hello PFX 파일을 가져오는 작업을 수행 합니다. 사용할 수 있습니다 tooimport hello 인증서 `setupentrypoint.sh` 스크립트 또는 hello 컨테이너 프로세스 내에서 사용자 지정 코드를 실행 합니다. Hello PFX 파일을 가져오는 C# 샘플 코드는 따릅니다.

```c#
    string certificateFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_PFX");
    string passwordFilePath = Environment.GetEnvironmentVariable("Certificate_NodeContainerService.Code_MyCert1_Password");
    X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
    string password = File.ReadAllLines(passwordFilePath, Encoding.Default)[0];
    password = password.Replace("\0", string.Empty);
    X509Certificate2 cert = new X509Certificate2(certificateFilePath, password, X509KeyStorageFlags.MachineKeySet | X509KeyStorageFlags.PersistKeySet);
    store.Open(OpenFlags.ReadWrite);
    store.Add(cert);
    store.Close();
```
이 PFX 인증서 authenticate hello 응용 프로그램 또는 서비스 또는 다른 서비스와 보안 commmunication에 사용할 수 있습니다.


## <a name="set-up-gmsa-for-windows-containers"></a>Windows 컨테이너용 gMSA 설정

gMSA (그룹 관리 서비스 계정) 자격 증명 사양 파일을 tooset (`credspec`) hello 클러스터의 모든 노드에 배치 됩니다. VM 확장을 사용 하는 모든 노드에서 hello 파일을 복사할 수 있습니다.  hello `credspec` 파일 hello gMSA 계정 정보를 포함 해야 합니다. Hello에 대 한 자세한 내용은 `credspec` 파일, 참조 [서비스 계정](https://github.com/MicrosoftDocs/Virtualization-Documentation/tree/live/windows-server-container-tools/ServiceAccounts)합니다. hello 자격 증명 사양 및 hello `Hostname` 태그 hello 응용 프로그램 매니페스트에 지정 됩니다. hello `Hostname` 태그에서 컨테이너 실행 hello hello gMSA 계정 이름이 일치 해야 합니다.  hello `Hostname` 태그를 사용 하면 자체 hello 컨테이너 tooauthenticate tooother 도메인 서비스에 hello Kerberos 인증을 사용 합니다.  Hello를 지정 하기 위한 샘플 `Hostname` 및 hello `credspec` hello에 응용 프로그램 매니페스트는 hello 다음 코드 조각으로에서 표시 됩니다.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="process" Hostname="gMSAAccountName">
    <SecurityOption Value="credentialspec=file://WebApplication1.json"/>
  </ContainerHostPolicies>
</Policies>
```
## <a name="next-steps"></a>다음 단계

* [Windows 컨테이너 tooService 패브릭 Windows Server 2016 배포](service-fabric-get-started-containers.md)
* [Docker 컨테이너 tooService 패브릭 linux 배포](service-fabric-get-started-containers-linux.md)
