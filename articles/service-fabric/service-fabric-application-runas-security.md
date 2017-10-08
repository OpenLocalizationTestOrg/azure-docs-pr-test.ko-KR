---
title: "Azure microservices 보안 정책에 대 한 aaaLearn | Microsoft Docs"
description: "작업을 시작 하기 전에 toorun 시스템 및 보안 로컬 계정에서 서비스 패브릭 응용 프로그램에서 응용 프로그램 해야 tooperform 일부 hello SetupEntry 지점 포함 어떻게 privileged의 개요"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a>응용 프로그램에 대한 보안 정책 구성
Azure Service Fabric을 사용 하 여 다른 사용자 계정으로 hello 클러스터에서 실행 되는 응용 프로그램을 보호할 수 있습니다. 서비스 패브릭 예를 들어 hello 사용자 계정-배포의 hello 시 응용 프로그램에서 사용 되는 보안 hello 리소스, 파일, 디렉터리 및 인증서에도 도움이 됩니다. 따라서 공유되는 호스티드 환경에서도 서로 더욱 안전하게 응용 프로그램을 실행할 수 있습니다.

기본적으로 서비스 패브릭 응용 프로그램 hello Fabric.exe 프로세스를 실행 하는 hello 계정에서 실행 합니다. 서비스 패브릭은 또한 hello 기능 toorun 응용 프로그램을 로컬 사용자 계정 또는 응용 프로그램 매니페스트 hello에 지정 된 로컬 시스템 계정에서 제공 합니다. 지원되는 로컬 시스템 계정 유형은 **LocalUser**, **NetworkService**, **LocalService** 및 **LocalSystem**입니다.

 를 실행 중인 서비스 패브릭 Windows 서버에서 데이터 센터에서 hello 독립 실행형 설치 관리자를 사용 하 여 그룹 관리 서비스 계정을 포함 하는 Active Directory 도메인 계정을 사용할 수 있습니다.

정의 하 고 하나 이상의 사용자를 추가할 수 있으며 함께 관리 tooeach 그룹 toobe 있도록 사용자 그룹을 만들 수 있습니다. 다른 서비스 진입점에 대 한 여러 사용자가 있으며 toohave hello 그룹 수준에서 사용할 수 있는 일반적인 특정 권한이 필요한 경우에 유용 합니다.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>서비스 설치 시작 지점에 대 한 hello 정책 구성
Hello에 설명 된 대로 [응용 프로그램 모델](service-fabric-application-model.md), 설치 진입점 hello **SetupEntryPoint**, hello 서비스 패브릭으로 동일한 자격 증명으로 실행 되는 권한 있는 요소입니다 (일반적으로 hello *NetworkService* 계정) 전에 다른 진입점입니다. 지정 된 hello 실행 파일 **EntryPoint** hello 장기 실행 서비스 호스트는 일반적으로 합니다. 오랜 시간에 대 한 toorun hello 서비스 호스트 높은 권한으로 실행을 않아도 따라서 별도 설치 진입점을 필요 합니다. hello를 실행 하는 **EntryPoint** 지정 후 실행 **SetupEntryPoint** 정상적으로 종료 합니다. hello 결과 프로세스를 모니터링 하 고 다시 시작으로 다시 시작 하 고 **SetupEntryPoint** 적이 종료 되거나 충돌 합니다.

hello 다음은 간단한 서비스 매니페스트 예제 프로그램 SetupEntryPoint hello 및 hello hello 서비스에 대 한 주 진입점입니다.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a>로컬 계정을 사용 하 여 hello 정책 구성
Hello 서비스 toohave 설치 진입점을 구성한 후에 hello 응용 프로그램 매니페스트는 아래에서 실행 되는 hello 보안 권한을 변경할 수 있습니다. 다음 예제는 hello tooconfigure 사용자 관리자 계정 권한으로 서비스 toorun hello 하는 방법을 보여 줍니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

먼저, 사용자 이름(예: SetupAdminUser)을 사용하여 **주체** 섹션을 만듭니다. 이 해당 hello 사용자 hello 관리자 시스템 그룹의 구성원임을 나타냅니다.

Hello 아래에서 다음 **ServiceManifestImport** 섹션에서 정책 tooapply이 보안이 주체를 너무 구성한**SetupEntryPoint**합니다. 이렇게 하면 서비스 패브릭 하는 경우 hello **MySetup.bat** 파일을 실행 하는 것, `RunAs` 관리자 권한으로 합니다. 있다면 *하지* 적용 정책 toohello 주 진입점의 hello 코드 **MyServiceHost.exe** hello 시스템에서 실행 **NetworkService** 계정. 모든 서비스 진입점으로 실행 하는 hello 기본 계정입니다.

이제 hello 파일 MySetup.bat toohello Visual Studio 프로젝트 tootest hello 관리자 권한이 추가해보겠습니다. Visual Studio에서 hello 서비스 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 MySetup.bat 이라는 새 파일을 추가 합니다.

다음으로 hello 서비스 패키지에 해당 hello MySetup.bat 파일이 포함 되는지 확인 합니다. 기본적으로 아닙니다. Hello 파일 선택 tooget hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다. Hello 속성 대화 상자에서 **tooOutput 디렉터리 복사** 너무 설정**변경 된 내용만 복사**합니다. 다음 스크린 샷 hello를 참조 하십시오.

![SetupEntryPoint 배치 파일에 대한 Visual Studio CopyToOutput][image1]

이제 hello MySetup.bat 파일을 열고 추가 명령을 수행 하는 hello:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

다음으로, 빌드 및 hello 솔루션 tooa 로컬 개발 클러스터를 배포 합니다. Hello 서비스가 시작 서비스 패브릭 탐색기에 표시 된 것 처럼, 해당 hello MySetup.bat 파일 두 가지 방법으로 성공적으로 볼 수 있습니다. Azure PowerShell 명령 프롬프트를 열고 입력합니다.

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

그런 다음 note hello 이름 hello 노드 hello 서비스의 배포 된 및 예를 들어 노드 2에서 서비스 패브릭 탐색기-시작 위치입니다. 다음으로 toohello 응용 프로그램 인스턴스 작업 폴더 toofind hello out.txt 파일이 hello 값을 보여 주는 이동 **TestVariable**합니다. 예를 들어이 서비스에 배포 된 tooNode 2 되었으면 있습니다 수 이동 하 여 hello에 대 한 toothis 경로 **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>로컬 시스템 계정을 사용 하 여 hello 정책 구성
대개는 관리자 계정이 아닌 로컬 시스템 계정을 사용 하 여 선호 toorun hello 시작 스크립트는. 관리자 그룹 일반적으로 작동 하지 않는 컴퓨터에 액세스 제어 UAC (사용자) 기본적으로 사용할 수 있어야 하기 때문에 잘 hello의 구성원으로 hello RunAs 정책을 실행 합니다. 이러한 경우 **hello 좋습니다 toorun hello LocalSystem으로 SetupEntryPoint 대신 tooAdministrators 추가 된 로컬 사용자 그룹으로**합니다. hello 다음 예제는 hello SetupEntryPoint toorun 설정을 LocalSystem으로.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>설치 진입점에서 PowerShell 명령 시작
hello에서 PowerShell toorun **SetupEntryPoint** 지점을 실행할 수 있습니다 **PowerShell.exe** tooa PowerShell 가리키는 배치 파일에서 파일입니다. 먼저 PowerShell 파일 toohello 서비스 프로젝트-예를 들어 추가 **MySetup.ps1**합니다. Tooset hello 기억 *변경 된 내용만 복사* 속성이 해당 hello 파일 hello 서비스 패키지에도 포함 되어 있도록 합니다. hello 다음 예제 MySetup.ps1 라는 시스템 환경 변수를 설정 하 라는 PowerShell 파일을 시작 하는 샘플 배치 파일 **TestVariable**합니다.

MySetup.bat toostart PowerShell 파일:

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

Hello PowerShell 파일에서 hello 다음 tooset 시스템 환경 변수를 추가 합니다.

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> 기본적으로 hello 배치 파일을 실행할 때 확인 hello 라고 하는 응용 프로그램 폴더 **작동** 파일에 대 한 합니다. 이 경우 MySetup.bat 실행 될 때 원하는 hello에이 toofind hello MySetup.ps1 파일 같은 hello 응용 프로그램 폴더에 **코드 패키지** 폴더입니다. toochange이 폴더, 집합 hello 작업 폴더:
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a>로컬 디버깅에 대한 콘솔 리디렉션 사용
경우에 따라 디버깅을 위해 스크립트 실행에서 유용한 toosee hello 콘솔 출력 됩니다. toodo이 hello 출력 tooa 파일을 작성 하는 콘솔 리디렉션을 정책을 설정할 수 있습니다. hello 파일 출력 toohello 작성 된 응용 프로그램 폴더 라고 **로그** hello 노드에서 hello 응용 프로그램은 배포 하 고 실행 합니다. (참조 위치 toofind hello 이전 예제에서에서이.)

> [!WARNING]
> Hello 콘솔 리디렉션 정책 hello 응용 프로그램 장애 조치에 영향을 줄 수 있으므로 프로덕션에 배포 된 응용 프로그램에서 사용 하지 마십시오. 로컬 개발 및 디버깅 목적으로*만* 사용하세요.  
> 
> 

hello 다음 예제는 FileRetentionCount 값이 있는 hello 콘솔 리디렉션을 설정.

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Hello MySetup.ps1 파일 toowrite 지금 변경 하는 경우는 **에코** 명령,이 디버깅을 위해 toohello 출력 파일을 작성 합니다.

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**스크립트를 디버그한 후 즉시 이 콘솔 리디렉션 정책을 제거합니다.**

## <a name="configure-a-policy-for-service-code-packages"></a>서비스 코드 패키지에 대한 정책 구성
Hello 이전 단계에서에서 언급 했 듯이 어떻게 tooapply RunAs 정책 tooSetupEntryPoint 합니다. 살펴보겠습니다 좀 더 자세히 방식으로 적용할 수 있는 toocreate 다른 보안 주체 서비스 정책에.

### <a name="create-local-user-groups"></a>로컬 사용자 그룹 만들기
정의 하 고 하나를 사용할 수 있는 사용자 그룹을 만들 수 또는 더 많은 사용자가 toobe tooa 그룹에 추가 했습니다. 다른 서비스 진입점에 대 한 여러 사용자가 있으며 toohave hello 그룹 수준에서 사용할 수 있는 일반적인 특정 권한이 필요한 경우에 유용 합니다. hello 다음 보여 주는 예제 라는 로컬 그룹이 **LocalAdminGroup** 관리자 권한이 있는 합니다. 두 사용자 Customer1과 Customer2를 이 그룹 구성원으로 만듭니다.

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a>로컬 사용자 만들기
Hello 응용 프로그램 내에서 서비스 보안 사용된 toohelp 일 수 있는 로컬 사용자를 만들 수 있습니다. 경우는 **LocalUser** 계정 유형의 서비스 패브릭 hello 응용 프로그램 배포 된 컴퓨터에서 로컬 사용자 계정을 만들어 hello 응용 프로그램 매니페스트의 hello 주체 섹션에 지정 됩니다. 기본적으로 이러한 계정 (예: hello 샘플 다음에 Customer3) hello 응용 프로그램에 지정 된 것과 같은 이름을 매니페스트 hello를 갖지 않습니다. 대신 동적으로 생성되며 임의 암호를 포함합니다.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

응용 프로그램이 필요한 경우 hello 사용자 계정 및 암호가 모든 컴퓨터 (예를 들어 tooenable NTLM 인증)에 동일한 수, hello 클러스터 매니페스트 NTLMAuthenticationEnabled tootrue를 설정 해야 합니다. hello 클러스터 매니페스트도 지정 해야 사용 되는 NTLMAuthenticationPasswordSecret toogenerate 모든 컴퓨터에 같은 암호를 hello 합니다.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>할당 정책을 toohello 서비스 코드 패키지
hello **RunAsPolicy** 섹션는 **ServiceManifestImport** hello 계정을 사용 하는 코드 패키지 toorun 되어야 하는 hello 주체 섹션에서 지정 합니다. 또한 코드 hello 서비스에서 패키지 매니페스트 hello 주체 섹션에서 사용자 계정으로 연결 합니다. Hello 설치 프로그램 또는 주 진입점에 대 한이 지정할 수 있습니다 또는 지정할 수 있습니다 `All` tooapply 것 tooboth 합니다. hello 다음 예제는 서로 다른 정책 적용.

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

경우 **EntryPointType** 를 지정 하지 않으면 hello 기본값은 tooEntryPointType 설정 = "Main"입니다. 지정 **SetupEntryPoint** toorun 시스템 계정에서 특정 권한이 높은 설치 작업을 사용할 때 특히 유용 합니다. hello 실제 서비스 코드 보다 낮은 권한 계정으로 실행할 수 있습니다.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>기본 정책 tooall 서비스 코드 패키지를 적용 합니다.
Hello를 사용 하 여 **DefaultRunAsPolicy** 섹션 toospecify 특정 하지 않은 모든 코드 패키지에 대 한 기본 사용자 계정 **RunAsPolicy** 정의 합니다. 대부분의 응용 프로그램에서 사용 하는 hello 서비스 매니페스트에 지정 된 hello 코드 패키지에서 toorun 필요 hello 동일한 사용자 hello 응용 프로그램이 해당 사용자 계정 가진 기본 실행 정책을 정의할 수 있습니다. hello 다음 예제에서는 지정 하는 코드 패키지에 없는 경우는 **RunAsPolicy** 지정 hello 코드 패키지를 실행할 hello **MyDefaultAccount** hello 주체 섹션에 지정 합니다.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Active Directory 도메인 그룹 또는 사용자 사용
서비스 패브릭 hello 독립 실행형 설치 관리자를 사용 하 여 Windows Server에 설치 된 인스턴스에 대 한 Active Directory 사용자 또는 그룹 계정에 대 한 hello 자격 증명으로 hello 서비스를 실행할 수 있습니다. 도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다. 도메인 사용자 또는 그룹을 사용 하 여 권한을 부여 받은 기타 리소스 hello 도메인 (예: 파일 공유)에 액세스할 수 있습니다.

hello 다음 예제에서는 Active Directory 사용자를 호출 *TestUser* 가 도메인 인증서를 사용 하 여 암호화 된 암호 호출 *MyCert*합니다. Hello를 사용할 수 있습니다 `Invoke-ServiceFabricEncryptText` PowerShell 명령 toocreate hello 비밀 암호화 텍스트입니다. 자세한 내용은 [Service Fabric 응용 프로그램의 비밀 관리](service-fabric-application-secret-management.md)를 참조하세요.

밴드의 범위를 벗어난 메서드를 사용 하 여 hello hello 인증서 toodecrypt hello 암호 toohello 로컬 컴퓨터의 개인 키를 배포 해야 (azure에서이 Azure 리소스 관리자를 통해). 그런 다음 서비스 패브릭 hello 서비스 패키지 toohello 컴퓨터를 배포 하면 수 toodecrypt hello 암호로 및 hello 사용자 이름) (함께 Active Directory toorun 이러한 자격 증명을 사용 하 여 인증 합니다.

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a>그룹 관리 서비스 계정을 사용합니다.
서비스 패브릭 hello 독립 실행형 설치 관리자를 사용 하 여 Windows Server에 설치 된 인스턴스에 대 한 hello 서비스 그룹 관리 서비스 계정 (gMSA)로 실행할 수 있습니다. 도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다. GMSA를 사용 하 여 암호 또는 없을 hello에 저장 된 암호화 된 암호 `Application Manifest`합니다.

hello 다음 예제에서는 호출 방법을 보여 줍니다 toocreate gMSA 계정 *svc 테스트 $*toodeploy를 관리 하는 방법은; 서비스 계정 toohello 클러스터 노드; 및 어떻게 tooconfigure hello 사용자 계정입니다.

##### <a name="prerequisites"></a>필수 조건.
- hello 도메인 KDS 루트 키가 필요합니다.
- hello 도메인 기능 수준을 이상 또는 Windows Server 2012에서 toobe가 필요합니다.

##### <a name="example"></a>예제
1. Hello를 사용 하 여 그룹 관리 서비스 계정을 만드는 active directory 도메인 관리자가 `New-ADServiceAccount` commandlet 해당 hello 확인 `PrincipalsAllowedToRetrieveManagedPassword` hello 서비스 패브릭 클러스터 노드를 모두 포함 합니다. `AccountName`, `DnsHostName` 및 `ServicePrincipalName`이 고유해야 합니다.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. 각 hello 서비스 패브릭 클러스터 노드에서 (예를 들어 `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`) 설치 하 고 hello gMSA를 테스트 합니다.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Hello 사용자 계정 구성 하 고 hello RunAsPolicy tooreference hello 사용자를 구성 합니다.
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>HTTP 및 HTTPS 끝점에 보안 액세스 정책 할당
실행 정책 tooa 서비스를 적용 하 고 hello HTTP 프로토콜을 사용 하 여 끝점 리소스를 선언 하는 hello 서비스 매니페스트를 지정 해야 합니다는 **SecurityAccessPolicy** tooensure toothese 끝점 포트에 할당 되는 요소가 올바르게 hello에 대 한 hello 서비스가 실행 되는 실행 사용자 계정을 나열 하는 액세스 제어. 그렇지 않으면 **http.sys** 액세스 toohello 서비스가 되어 있지 않으며 hello 클라이언트에서 호출 에서도 오류를 받아야 합니다. hello 다음 예제에서는 적용 라는 hello Customer1 계정 tooan 끝점 **EndpointName**, 모든 액세스 권한을 제공 하 합니다.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Hello HTTPS 끝점에 대 한 hello 인증서 tooreturn toohello 클라이언트의 tooindicate hello 이름을 할 수 있습니다. 사용 하 여이 작업을 수행할 수 **EndpointBindingPolicy**, hello 응용 프로그램 매니페스트에서 인증서 섹션에 정의 된 hello 인증서를 사용 합니다.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>https 끝점으로 여러 응용 프로그램 업그레이드
Toobe 주의 필요 하지 toouse hello **동일한 포트** hello의 다른 인스턴스에 대해 http를 사용 하는 경우 동일한 응용 프로그램**s**합니다. hello 이유가 서비스 패브릭이 hello 응용 프로그램 인스턴스 중 하나에 대 한 수 tooupgrade hello 인증서를 수 없습니다. 예를 들어, 응용 프로그램 1 개 또는 응용 프로그램 2 두 원하는 tooupgrade 자신의 인증서 1 toocert 2입니다. Hello 업그레이드 문제가 발생 하면 서비스 패브릭 정리 수 http.sys 사용 하 여 hello 인증서 1 등록 hello 다른 응용 프로그램은 사용 중인 경우에 합니다. tooprevent이를 서비스 패브릭에서 hello 인증서를 사용 하 여 hello 포트에 등록 하는 다른 응용 프로그램 인스턴스가 이미 임을 감지한 (due toohttp.sys) 및 실패 hello 작업 합니다.

따라서 서비스 패브릭 지원 하지 않습니다 두 개의 서로 다른 서비스를 사용 하 여 업그레이드 **동일한 포트 hello** 서로 다른 응용 프로그램의 경우. Hello에 서로 다른 서비스에 동일한 인증서 hello을 사용할 수 없습니다 즉, 동일한 포트입니다. Toohave 필요한 경우 공유 인증서에 hello 동일한 포트 tooensure 배치 제약 조건으로 서로 다른 컴퓨터에 대 한 서비스 사항은 해당 hello를 해야 합니다. 또는 각 응용 프로그램 인스턴스에서 각 서비스에 대해 Service Fabric 동적 포트를 사용하는 것이 좋습니다(가능한 경우). 

Https로 업그레이드는 실패를 표시 하는 경우 "hello Windows HTTP 서버 API 지원 하지 않습니다 여러 인증서를 포트를 공유 하는 응용 프로그램에 대 한." 메시지가 표시 되는 오류 경고

## <a name="a-complete-application-manifest-example"></a>완전한 응용 프로그램 매니페스트의 예
다른 설정을 응용 프로그램 매니페스트를 수행 하는 hello 다양 한 hello를 보여줍니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>다음 단계
* [Hello 응용 프로그램 모델 이해](service-fabric-application-model.md)
* [서비스 매니페스트에서 리소스 지정](service-fabric-service-manifest-resources.md)
* [응용 프로그램 배포](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
