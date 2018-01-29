---
title: "Azure 마이크로 서비스 보안 정책에 대해 알아보기 | Microsoft Docs"
description: "응용 프로그램이 시작되려면 일부 권한 있는 작업을 수행해야 하는 SetupEntry 지점을 포함하여 시스템 및 로컬 보안 계정을 통해 서비스 패브릭 응용 프로그램을 실행하는 방법에 대한 개요"
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
ms.openlocfilehash: b2ff715d8225bd0a9c7f6108f8804cdfa3189cc8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2017
---
# <a name="configure-security-policies-for-your-application"></a>응용 프로그램에 대한 보안 정책 구성
Azure Service Fabric을 사용하여 다른 사용자 계정으로 클러스터에서 실행 중인 응용 프로그램을 보호할 수 있습니다. 또한 Service Fabric으로 배포 시 파일, 디렉터리, 인증서 등과 같은 사용자 계정을 통해 응용 프로그램에서 사용하는 리소스도 보호합니다. 따라서 공유되는 호스티드 환경에서도 서로 더욱 안전하게 응용 프로그램을 실행할 수 있습니다.

기본적으로 서비스 패브릭 응용 프로그램은 Fabric.exe 프로세스가 실행하는 계정을 통해 실행됩니다. 또한 Service Fabric은 응용 프로그램의 매니페스트 내에 지정된 로컬 사용자 계정 또는 로컬 시스템 계정을 통해 응용 프로그램을 실행하는 기능을 제공합니다. 지원되는 로컬 시스템 계정 유형은 **LocalUser**, **NetworkService**, **LocalService** 및 **LocalSystem**입니다.

 독립 실행형 설치 관리자를 사용하여 데이터 센터의 Windows Server에서 Service Fabric을 실행하는 경우 그룹 관리 서비스 계정을 포함하여 Active Directory 도메인 계정을 사용할 수 있습니다.

사용자 그룹을 정의하고 만들었으므로 각 그룹에 사용자를 한 명 이상 추가하여 한꺼번에 관리할 수 있습니다. 이 기능은 여러 서비스 진입점에 대한 사용자가 여러 명 있고 그 사용자들에게 그룹 수준에서 특정 공통 권한을 부여해야 하는 경우 유용합니다.

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a>서비스 설치 진입점에 대한 정책 구성
[응용 프로그램 및 서비스 매니페스트](service-fabric-application-and-service-manifests.md)에서 설명한 것처럼 설치 진입점인 **SetupEntryPoint**는 Service Fabric과 같은 자격 증명(일반적으로 *NetworkService* 계정)을 사용하여 다른 진입점보다 먼저 실행되는 권한 있는 진입점입니다. **EntryPoint**로 지정되는 실행 파일은 일반적으로 장기 실행 서비스 호스트입니다. 별도의 설치 진입점이 있으면 한동안은 높은 권한을 사용하여 서비스 호스트를 실행하지 않아도 됩니다. **EntryPoint**로 지정된 실행 파일은 **SetupEntryPoint**가 성공적으로 종료된 후 실행됩니다. 종료되지 않거나 충돌하는 경우 결과 프로세스를 모니터링하여 다시 시작합니다(**SetupEntryPoint**를 사용하여 다시 시작).

다음은 서비스에 대한 SetupEntryPoint 및 기본 EntryPoint를 보여주는 서비스 매니페스트의 간단한 예입니다.

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

### <a name="configure-the-policy-by-using-a-local-account"></a>로컬 계정을 사용하여 정책 구성
설치 항목 지점이 있도록 서비스를 구성한 후에 응용 프로그램 매니페스트에서 아래에서 실행되는 보안 권한을 변경할 수 있습니다. 다음은 사용자 관리자 계정 권한으로 실행되도록 서비스를 구성하는 방법을 보여 주는 예제입니다.

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

먼저, 사용자 이름(예: SetupAdminUser)을 사용하여 **주체** 섹션을 만듭니다. 이 사용자가 관리자 시스템 그룹의 구성원임을 나타내는 이름입니다.

다음으로, **ServiceManifestImport** 섹션에서 정책을 구성하여 이 주체를 **SetupEntryPoint**에 적용합니다. 이렇게 하면 Service Fabric에서는 **MySetup.bat** 파일이 실행될 때 관리자 권한이 있는 `RunAs`인지 확인합니다. 기본 진입점에 정책을 적용하지 *않으면* **MyServiceHost.exe**의 코드가 시스템 **NetworkService** 계정에서 실행됩니다. 이 계정은 모든 서비스 진입점이 run as인 기본 계정입니다.

이제 MySetup.bat 파일을 Visual Studio 프로젝트에 추가하여 관리자 권한을 테스트하겠습니다. Visual Studio에서 서비스 프로젝트를 마우스 오른쪽 단추로 클릭하고 새 파일 MySetup.bat을 추가합니다.

다음으로 MySetup.bat 파일이 서비스 패키지에 포함되어 있도록 합니다. 기본적으로 아닙니다. 파일을 선택하고 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭하며 **속성**을 선택합니다. 속성 대화 상자에서 **출력 디렉터리로 복사**가 **변경된 내용만 복사**로 설정되도록 합니다. 다음 스크린샷이 표시됩니다.

![SetupEntryPoint 배치 파일에 대한 Visual Studio CopyToOutput][image1]

이제 MySetup.bat 파일을 열고 다음 명령을 추가합니다.

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

다음으로 솔루션을 빌드하여 로컬 개발 클러스터에 배포합니다. 서비스가 시작되면 Service Fabric Explorer에 표시된 대로 MySetup.bat 파일이 두 가지 방법으로 성공한 것을 볼 수 있습니다. Azure PowerShell 명령 프롬프트를 열고 입력합니다.

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

그런 다음 서비스가 배포되고 Service Fabric Explorer에서 시작된 노드의 이름(예: 노드2)을 적어둡니다. 다음으로 응용 프로그램 인스턴스 작업 폴더로 이동하여 **TestVariable**값을 보여주는 out.txt 파일을 찾습니다. 예를 들어 이 서비스가 노드 2에 배포된 경우 **MyApplicationType**에 대한 이 경로로 이동할 수 있습니다.

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a>로컬 시스템 계정을 사용하여 정책 구성
관리자 계정이 아닌 로컬 시스템 계정을 사용하여 스크립트의 시작을 실행하는 것이 일반적으로 더 좋습니다. 컴퓨터는 기본적으로 UAC(사용자 Access Control)를 사용하도록 설정되어 있기 때문에 관리자 그룹의 구성원으로 RunAs 정책을 실행하면 일반적으로 잘 작동하지 않습니다. 이러한 경우 **관리자 그룹에 추가된 로컬 사용자 대신 LocalSystem으로 SetupEntryPoint를 실행하는 것이 좋습니다**. 다음 예제에서는 LocalSystem으로 실행하도록 SetupEntryPoint를 설정합니다.

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

Linux 클러스터의 경우 서비스 또는 설정 진입점을 **root**로 실행하려면 **AccountType**을 **LocalSystem**으로 지정해야 합니다.

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>설치 진입점에서 PowerShell 명령 시작
**SetupEntryPoint** 지점에서 PowerShell을 실행하려면 PowerShell 파일을 가리키는 배치 파일에서 **PowerShell.exe**를 실행하면 됩니다. 먼저 서비스 프로젝트(예: **MySetup.ps1**)에 PowerShell 파일을 추가합니다. 이 파일도 서비스 패키지에 포함되도록 *변경된 내용만 복사* 속성을 설정해야 합니다. 다음은 **TestVariable**이라는 시스템 환경 변수를 설정하는 PowerShell 파일 MySetup.ps1을 시작하는 간단한 배치 파일을 보여 주는 예제입니다.

PowerShell 파일을 시작하기 위한 MySetup.bat입니다.

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

PowerShell 파일에서 다음을 추가하여 시스템 환경 변수를 설정합니다.

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> 기본적으로 배치 파일이 실행될 때 **work**라는 응용 프로그램 폴더에서 파일을 찾습니다. 이 경우 MySetup.bat가 실행될 때 같은 폴더(응용 프로그램 **코드 패키지** 폴더)에서 MySetup.ps1 파일을 찾으려고 합니다. 이 폴더를 변경하려면 아래와 같이 작업 폴더를 설정합니다.
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
디버깅 목적으로 스크립트를 실행하여 콘솔 출력을 확인하는 것이 유용할 때가 있습니다. 이 작업을 수행하기 위해 파일에 출력을 기록하는 콘솔 리디렉션 정책을 설정할 수 있습니다. 파일 출력은 응용 프로그램이 배포되고 실행되는 노드에 **log**라는 응용 프로그램 폴더에 기록됩니다. (앞의 예제에서 이를 찾을 수 있는 위치 참조)

> [!WARNING]
> 절대 프로덕션에 배포된 응용 프로그램의 콘솔 리디렉션 정책은 사용하지 마세요. 응용 프로그램 장애 조치(failover)에 영향을 줄 수 있기 때문입니다. 로컬 개발 및 디버깅 목적으로*만* 사용하세요.  
> 
> 

다음 예제에서는 콘솔 리디렉션을 FileRetentionCount 값으로 설정합니다.

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

이제 MySetup.ps1 파일을 변경하여 **Echo** 명령을 작성하면 디버깅 목적으로 출력 파일에 기록합니다.

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

**스크립트를 디버그한 후 즉시 이 콘솔 리디렉션 정책을 제거합니다.**

## <a name="configure-a-policy-for-service-code-packages"></a>서비스 코드 패키지에 대한 정책 구성
이전 단계에서 SetupEntryPoint에 RunAs 정책을 적용하는 방법을 살펴보았습니다. 이번에는 서비스 정책으로 적용할 수 있는 다양한 주체를 만드는 방법을 좀 더 자세히 살펴보겠습니다.

### <a name="create-local-user-groups"></a>로컬 사용자 그룹 만들기
그룹에 사용자를 한 명 이상 추가하도록 사용자 그룹을 정의하고 만들 수 있습니다. 이 기능은 여러 서비스 진입점에 대한 사용자가 여러 명 있고 그 사용자들에게 그룹 수준에서 특정 공통 권한을 부여해야 하는 경우 유용합니다. 다음은 관리자 권한이 있는 **LocalAdminGroup**이라는 로컬 그룹을 보여 줍니다. 두 사용자 Customer1과 Customer2를 이 그룹 구성원으로 만듭니다.

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
응용 프로그램 내에서 서비스를 보호하는 데 사용할 수 있는 로컬 사용자를 만들 수 있습니다. 응용 프로그램 매니페스트의 주체 섹션에서 **LocalUser** 계정 형식이 지정되면 Service Fabric에서는 응용 프로그램이 배포되는 컴퓨터에 로컬 사용자 계정을 만듭니다. 기본적으로 이러한 계정은 응용 프로그램 매니페스트(예: 다음 샘플의 Customer3)에 지정된 것과 동일한 이름을 갖지 않습니다. 대신 동적으로 생성되며 임의 암호를 포함합니다.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

응용 프로그램에서 사용자 계정과 암호가 모든 컴퓨터에서 같도록 요구할 경우(예: NTLM 인증을 사용하기 위해) 클러스터 매니페스트는 NTLMAuthenticationEnabled를 true로 설정해야 합니다. 클러스터 매니페스트는 모든 컴퓨터에서 동일한 암호를 생성하는 데 사용된 NTLMAuthenticationPasswordSecret도 지정해야 합니다.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a>서비스 코드 패키지에 정책 할당
**ServiceManifestImport**에 대한 **RunAsPolicy** 섹션은 코드 패키지를 실행하는 데 사용되어야 하는 주체 섹션에서 계정을 지정합니다. 또한 서비스 매니페스트에서 코드 패키지를 주체 섹션에서 사용자 계정과 연결합니다. 설정 또는 기본 진입점에 대해 이 정책을 적용할 수도 있고 `All` 을 지정하여 양쪽에 적용할 수 있습니다. 다음은 여러 정책을 적용하는 방법을 보여주는 예입니다.

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

**EntryPointType** 을 지정하지 않으면 기본적으로 EntryPointType=”Main”으로 지정됩니다. 특히 시스템 계정에서 특정 고수준 권한 설정 작업을 실행하려면 **SetupEntryPoint**를 지정하는 것이 매우 유용합니다. 실제 서비스 코드는 낮은 권한 계정으로 실행할 수 있습니다.

### <a name="apply-a-default-policy-to-all-service-code-packages"></a>모든 서비스 코드 패키지에 기본 정책 적용
**DefaultRunAsPolicy** 섹션은 특정 **RunAsPolicy**가 정의되지 않은 모든 코드 패키지에 대해 기본 사용자 계정을 지정하는 데 사용됩니다. 응용 프로그램에서 사용하는 서비스 매니페스트에 지정된 대부분의 코드 패키지가 동일한 사용자를 통해 실행되어야 하는 경우 응용 프로그램에서 해당 사용자 계정을 사용하여 기본 RunAs 정책을 정의할 수 있습니다. 다음은 코드 패키지의 **RunAsPolicy**가 지정되지 않으면 주체 섹션에 지정된 **MyDefaultAccount**에서 코드 패키지가 수행되는 예제입니다.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Active Directory 도메인 그룹 또는 사용자 사용
독립 실행형 설치 관리자를 사용하여 Windows Server에 설치된 Service Fabric 인스턴스의 경우 Active Directory 사용자 또는 그룹 계정에 대한 자격 증명으로 서비스를 실행할 수 있습니다. 도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다. 도메인 사용자 또는 그룹을 사용하여 권한이 부여된 도메인의 다른 리소스(예: 파일 공유)에 액세스할 수 있습니다.

다음 예제는 *TestUser*라는 Active Directory 사용자와 *MyCert*라는 인증서를 사용하여 암호화된 도메인 암호를 보여 줍니다. `Invoke-ServiceFabricEncryptText` PowerShell 명령을 사용하여 암호 텍스트를 만들 수 있습니다. 자세한 내용은 [Service Fabric 응용 프로그램의 비밀 관리](service-fabric-application-secret-management.md)를 참조하세요.

암호 해독을 위한 인증서의 개인 키는 대역 외 메서드를 사용하여(Azure에서는 Azure Resource Manager를 통해) 로컬 컴퓨터에 배포해야 합니다. 그런 다음 Service Fabric이 컴퓨터에 서비스 패키지를 배포할 때 사용자 이름과 함께 암호를 해독하고 이 자격 증명으로 실행하도록 Active Directory로 인증할 수 있습니다.

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
독립 실행형 설치 관리자를 사용하여 Windows Server에 설치된 Service Fabric 인스턴스의 경우 그룹 관리 서비스 계정(gMSA)으로 서비스를 실행할 수 있습니다. 도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다. gMSA를 사용하면 `Application Manifest`에 저장된 암호 또는 암호화된 암호가 없습니다.

다음 예에서는 *svc-Test$*라는 gMSA 계정을 작성하는 방법, 해당 관리 서비스 계정을 클러스터 노드에 배포하는 방법 및 사용자 주체를 구성하는 방법을 보여줍니다.

##### <a name="prerequisites"></a>필수 조건.
- 도메인에 KDS 루트 키가 필요합니다.
- Windows Server 2012 이상 기능 수준에 도메인이 있어야 합니다.

##### <a name="example"></a>예제
1. Active Directory 도메인 관리자가 `New-ADServiceAccount` commandlet을 사용하여 그룹 관리 서비스 계정을 만들고 `PrincipalsAllowedToRetrieveManagedPassword`에 Serivce Fabric 클러스터 노드가 모두 포함되도록 합니다. `AccountName`, `DnsHostName` 및 `ServicePrincipalName`이 고유해야 합니다.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. 각 Service Fabric 클러스터 노드(예: `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`)에서 gMSA를 설치하고 테스트합니다.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. 사용자 보안 주체를 구성하고 사용자를 참조하도록 RunAsPolicy를 구성합니다.
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
서비스에 RunAs 정책을 적용하고 서비스 매니페스트에서 HTTP 프로토콜을 사용하여 끝점 리소스를 선언할 경우 이러한 끝점에 할당된 포트가 서비스가 실행되는 RunAs 사용자 계정에 대해 올바르게 액세스 제어 나열되도록 **SecurityAccessPolicy**를 지정해야 합니다. 그러지 않으면 **http.sys** 가 해당 서비스에 액세스할 수 없고 클라이언트의 호출과 함께 오류가 발생합니다. 다음은 **EndpointName**이라는 끝점에 Customer1 계정을 적용하여 전체 액세스 권한을 부여하는 예제입니다.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

또한 HTTPS 끝점의 경우 클라이언트에 반환할 인증서의 이름을 나타내야 합니다. 응용 프로그램 매니페스트에서 인증서 섹션에 정의된 인증서를 통해 **EndpointBindingPolicy**를 사용하여 수행할 수 있습니다.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>https 끝점으로 여러 응용 프로그램 업그레이드
http**s**를 사용할 때는 동일한 응용 프로그램의 서로 다른 인스턴스에 대해 **동일한 포트**를 사용하지 않도록 주의해야 합니다. Service Fabric에서 응용 프로그램 인스턴스 중 하나에 대해 인증서를 업그레이드할 수 없기 때문입니다. 예를 들어, 응용 프로그램 1 또는 응용 프로그램 2 모두 해당 인증서 1을 인증서 2로 업그레이드하려고 합니다. 업그레이드가 발생할 때 Service Fabric은 다른 응용 프로그램에서 아직 사용 중이라고 하더라도 http.sys에서 인증서 1 등록을 정리할 수 있습니다. 이러한 상황을 방지하기 위해 Service Fabric은 인증서와 함께 해당 포트에 등록된(http.sys에 따라) 다른 응용 프로그램 인스턴스가 이미 있는지 검색하고 있는 경우 작업이 실패합니다.

따라서 Service Fabric은 서로 다른 응용 프로그램 인스턴스에 **동일한 포트**를 사용하는 두 가지 다른 서비스의 업그레이드를 지원하지 않습니다. 즉, 동일한 포트에서 서로 다른 서비스에 동일한 인증서를 사용할 수 없습니다. 동일한 포트에서 공유 인증서를 포함해야 하는 경우 배치 제약 조건에 따라 서비스가 서로 다른 컴퓨터에 배치되는지 확인해야 합니다. 또는 각 응용 프로그램 인스턴스에서 각 서비스에 대해 Service Fabric 동적 포트를 사용하는 것이 좋습니다(가능한 경우). 

https로 업그레이드 실패가 표시되면 “The Windows HTTP Server API does not support multiple certificates for applications that share a port(Windows HTTP 서버 API에서 포트를 공유하는 응용 프로그램에 대해 여러 인증서를 지원하지 않습니다).”라는 오류 경고가 표시됩니다.

## <a name="a-complete-application-manifest-example"></a>완전한 응용 프로그램 매니페스트의 예
다음 응용 프로그램 매니페스트는 여러 설정을 보여줍니다.

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
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed the EndpointName is secured with https -->
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


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>다음 단계
* [응용 프로그램 모델의 이해](service-fabric-application-model.md)
* [서비스 매니페스트에서 리소스 지정](service-fabric-service-manifest-resources.md)
* [응용 프로그램 배포](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
