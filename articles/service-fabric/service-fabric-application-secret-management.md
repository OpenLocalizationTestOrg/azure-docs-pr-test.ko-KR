---
title: "서비스 패브릭 응용 프로그램에서 aaaManaging 비밀 | Microsoft Docs"
description: "서비스 패브릭 응용 프로그램에서 toosecure 비밀 값 하는 방법을 설명 합니다."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a>서비스 패브릭 응용 프로그램의 비밀 관리
이 가이드는 서비스 패브릭 응용 프로그램의 암호 관리의 hello 단계를 안내 합니다. 저장소 연결 문자열, 암호, 일반 텍스트로 처리하면 안 되는 값 등 모든 민감한 정보를 비밀로 처리할 수 있습니다.

이 가이드에서는 Azure 키 자격 증명 모음 toomanage 키와 암호를 사용 합니다. 그러나 *를 사용 하 여* 응용 프로그램의 암호는 클라우드 플랫폼 제약 없는 tooallow 응용 프로그램 toobe 배포 tooa 클러스터 호스트 원하는 위치에 있습니다. 

## <a name="overview"></a>개요
hello 권장 되는 방법은 toomanage 서비스 구성 설정을 통해 됩니다 [구성 패키지 서비스][config-package]합니다. 구성 패키지는 관리되는 상태 유효성 검사 및 자동 롤백을 사용하여 롤링 업그레이드를 통해 버전이 관리되며 업데이트할 수 있습니다. 글로벌 서비스 중단의 hello 가능성 저하 기본 tooglobal 구성입니다. 암호화된 비밀도 마찬가지입니다. 서비스 패브릭에는 인증서 암호화를 사용하여 구성 패키지 Settings.xml 파일의 값을 암호화 및 해독하는 기본 기능이 포함되어 있습니다.

hello 다음 다이어그램에서는 서비스 패브릭 응용 프로그램의 보안 관리를 위한 기본 흐름 hello 수행 합니다.

![비밀 관리 개요][overview]

이 흐름은 주요 네 단계로 구성됩니다.

1. 데이터 암호화 인증서를 가져옵니다.
2. 클러스터의 hello 인증서를 설치 합니다.
3. Hello 인증서로 응용 프로그램을 배포 하는 경우 비밀 값을 암호화 하 고 서비스의 Settings.xml 구성 파일에 삽입 합니다.
4. 읽기 암호화 된 암호 해독 하 여 Settings.xml 값 hello 동일한 암호화 인증서입니다. 

[Azure 키 자격 증명 모음] [ key-vault-get-started] 인증서에 대 한 안전한 저장소 위치와 방법 tooget 여기에이 Azure에서 서비스 패브릭 클러스터에 설치 된 인증서입니다. TooAzure를 배포 하지 않은 경우에 서비스 패브릭 응용 프로그램에 toouse 주요 자격 증명 모음 toomanage 비밀 정보를 설치할 필요가 없습니다.

## <a name="data-encipherment-certificate"></a>데이터 암호화 인증서
데이터 암호화 인증서는 서비스에 포함된 Settings.xml의 구성 값을 암호화하고 해독하는 용도로만 엄격하게 사용되며 암호화 텍스트의 인증에는 사용되지 않습니다. hello 인증서 요구 사항을 준수 하는 hello를 충족 해야 합니다.

* hello 인증서 개인 키를 포함 해야 합니다.
* 키 교환, 내보낼 수 있는 tooa 개인 정보 교환 (.pfx) 파일에 대 한 hello 인증서를 만들어야 합니다.
* hello 인증서 키 용도 데이터 암호화 (10)을 포함 해야 하 고 서버 인증이 나 클라이언트 인증 포함 되지 않습니다. 
  
  PowerShell을 사용 하 여 자체 서명 된 인증서를 만들 때 다음 예를 들어 hello `KeyUsage` 너무 플래그를 설정 해야`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>클러스터의 hello 인증서를 설치 합니다.
이 인증서는 hello 클러스터의 각 노드에서 설치 되어야 합니다. 서비스의 Settings.xml에 저장 된 런타임 toodecrypt 값에 사용 됩니다. 참조 [어떻게 toocreate Azure 리소스 관리자를 사용 하는 클러스터] [ service-fabric-cluster-creation-via-arm] 설치 지침에 대 한 합니다. 

## <a name="encrypt-application-secrets"></a>응용 프로그램 비밀 암호화
서비스 패브릭 SDK hello 기본 제공 보안 암호화 및 암호 해독 함수에 있습니다. 작성 시 비밀 값을 암호화한 후 서비스 코드에서 프로그래밍 방식으로 해독하여 읽을 수 있습니다. 

hello 다음 PowerShell 명령을 사용 하는 tooencrypt 되는 암호입니다. 이 명령은 hello value;을 암호화 그렇게 **하지** hello 암호화 텍스트를 서명 합니다. Hello를 사용 해야 비밀 값에 대 한 프로그램 클러스터 tooproduce 암호 텍스트에 설치 된 동일한 암호화 인증서:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

hello 결과 base64 문자열에 포함 되어으로 hello 비밀 암호화 텍스트 정보를 사용 하는 tooencrypt hello 인증서에 대 한 것입니다.  hello e-64로 인코딩된 문자열에 삽입할 수 hello로 서비스의 Settings.xml 구성 파일에 대 한 매개 변수 `IsEncrypted` 특성이 너무 설정`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>응용 프로그램 비밀을 응용 프로그램 인스턴스에 삽입
이상적으로 배포 toodifferent 환경 최대한 자동화 해야 합니다. 이 빌드 환경에서 보안 암호화를 수행 하 고 응용 프로그램 인스턴스를 만들 때 매개 변수로 hello 암호화 암호를 제공 하 여 수행할 수 있습니다.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Settings.xml에 재정의 가능한 매개 변수 사용
hello Settings.xml 구성 파일에서는 응용 프로그램 생성 시 제공 될 수 있는 재정의 가능한 매개 변수입니다. 사용 하 여 hello `MustOverride` 매개 변수 값을 제공 하는 대신 특성:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

Settings.xml에 toooverride 값 applicationmanifest.xml에서 hello 서비스에 대 한 재정의 매개 변수는 선언 합니다.

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

이제 hello 값으로 지정할 수는 *응용 프로그램 매개 변수가* hello 응용 프로그램의 인스턴스를 만들 때. 응용 프로그램 인스턴스 만들기를 PowerShell로 스크립팅하거나 C#으로 작성하면 빌드 프로세스에 쉽게 통합할 수 있습니다.

Hello 매개 변수는 PowerShell을 사용 하 여, 제공 된 toohello `New-ServiceFabricApplication` 명령는 [해시 테이블](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

C#을 사용하면 응용 프로그램 매개 변수가 `ApplicationDescription`에 `NameValueCollection`로 지정됩니다.

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>서비스 코드에서 비밀 해독
서비스 패브릭에서 서비스 네트워크 서비스에서 기본적으로 Windows에서 실행 하 고 설치 되어 있지 않은 액세스 toocertificates 몇 가지 추가 설정 없이 hello 노드의 합니다.

데이터 암호화 인증서를 사용 하 여 네트워크 서비스 또는 어떤 사용자 계정 hello 서비스가 실행 되 고 액세스 toohello 인증서의 개인 키가 있는지 toomake가 필요 합니다. 서비스 패브릭 서비스에 대 한 액세스 하는 경우 구성한 toodo 하므로 자동으로 부여를 처리 합니다. 이 구성은 ApplicationManifest.xml에서 인증서의 사용자 및 보안 정책을 정의하여 수행할 수 있습니다. 다음 예제는 hello, hello 네트워크 서비스 계정에 읽기 액세스 tooa 인증서 지 문으로 정의 된 제공 됩니다.

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> 인증서 지문을 복사 하는 경우 hello 인증서 저장소에서 스냅인 Windows에, 보이지 않는 문자는 hello 지문 문자열의 hello 시작 부분에 위치 합니다. 이 보이지 않는 문자 오류가 발생할 수 있습니다 때 toolocate 인증서 지 문으로, 기울여야 있는지 toodelete이 추가 문자로 합니다.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>서비스 코드에 응용 프로그램 암호 사용
구성 패키지에 Settings.xml에서 구성 값에 액세스 하기 위한 API hello hello 밑줄이 있는 값의 쉬운 암호 해독을 위한 허용 `IsEncrypted` 특성이 너무 설정`true`합니다. 암호화에 사용 되는 hello 인증서에 대 한 정보를 포함 하는 hello 암호화 텍스트를 하기 때문에 toomanually 찾기 hello 인증서를 설치할 필요가 없습니다. hello 인증서 면 toobe hello 서비스에서 실행 되는 hello 노드에 설치 됩니다. Hello를 호출 하기만 하면 `DecryptValue()` 메서드 tooretrieve hello 원래 비밀 값:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>다음 단계
[다양한 보안 권한으로 응용 프로그램 실행](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
