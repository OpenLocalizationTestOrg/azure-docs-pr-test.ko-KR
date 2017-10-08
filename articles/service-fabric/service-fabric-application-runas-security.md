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
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="99bcc-103">응용 프로그램에 대한 보안 정책 구성</span><span class="sxs-lookup"><span data-stu-id="99bcc-103">Configure security policies for your application</span></span>
<span data-ttu-id="99bcc-104">Azure Service Fabric을 사용 하 여 다른 사용자 계정으로 hello 클러스터에서 실행 되는 응용 프로그램을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="99bcc-105">서비스 패브릭 예를 들어 hello 사용자 계정-배포의 hello 시 응용 프로그램에서 사용 되는 보안 hello 리소스, 파일, 디렉터리 및 인증서에도 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="99bcc-106">따라서 공유되는 호스티드 환경에서도 서로 더욱 안전하게 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="99bcc-107">기본적으로 서비스 패브릭 응용 프로그램 hello Fabric.exe 프로세스를 실행 하는 hello 계정에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="99bcc-108">서비스 패브릭은 또한 hello 기능 toorun 응용 프로그램을 로컬 사용자 계정 또는 응용 프로그램 매니페스트 hello에 지정 된 로컬 시스템 계정에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="99bcc-109">지원되는 로컬 시스템 계정 유형은 **LocalUser**, **NetworkService**, **LocalService** 및 **LocalSystem**입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="99bcc-110">를 실행 중인 서비스 패브릭 Windows 서버에서 데이터 센터에서 hello 독립 실행형 설치 관리자를 사용 하 여 그룹 관리 서비스 계정을 포함 하는 Active Directory 도메인 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="99bcc-111">정의 하 고 하나 이상의 사용자를 추가할 수 있으며 함께 관리 tooeach 그룹 toobe 있도록 사용자 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="99bcc-112">다른 서비스 진입점에 대 한 여러 사용자가 있으며 toohave hello 그룹 수준에서 사용할 수 있는 일반적인 특정 권한이 필요한 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="99bcc-113">서비스 설치 시작 지점에 대 한 hello 정책 구성</span><span class="sxs-lookup"><span data-stu-id="99bcc-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="99bcc-114">Hello에 설명 된 대로 [응용 프로그램 모델](service-fabric-application-model.md), 설치 진입점 hello **SetupEntryPoint**, hello 서비스 패브릭으로 동일한 자격 증명으로 실행 되는 권한 있는 요소입니다 (일반적으로 hello *NetworkService* 계정) 전에 다른 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="99bcc-115">지정 된 hello 실행 파일 **EntryPoint** hello 장기 실행 서비스 호스트는 일반적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="99bcc-116">오랜 시간에 대 한 toorun hello 서비스 호스트 높은 권한으로 실행을 않아도 따라서 별도 설치 진입점을 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="99bcc-117">hello를 실행 하는 **EntryPoint** 지정 후 실행 **SetupEntryPoint** 정상적으로 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="99bcc-118">hello 결과 프로세스를 모니터링 하 고 다시 시작으로 다시 시작 하 고 **SetupEntryPoint** 적이 종료 되거나 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="99bcc-119">hello 다음은 간단한 서비스 매니페스트 예제 프로그램 SetupEntryPoint hello 및 hello hello 서비스에 대 한 주 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

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

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="99bcc-120">로컬 계정을 사용 하 여 hello 정책 구성</span><span class="sxs-lookup"><span data-stu-id="99bcc-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="99bcc-121">Hello 서비스 toohave 설치 진입점을 구성한 후에 hello 응용 프로그램 매니페스트는 아래에서 실행 되는 hello 보안 권한을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="99bcc-122">다음 예제는 hello tooconfigure 사용자 관리자 계정 권한으로 서비스 toorun hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

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

<span data-ttu-id="99bcc-123">먼저, 사용자 이름(예: SetupAdminUser)을 사용하여 **주체** 섹션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="99bcc-124">이 해당 hello 사용자 hello 관리자 시스템 그룹의 구성원임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="99bcc-125">Hello 아래에서 다음 **ServiceManifestImport** 섹션에서 정책 tooapply이 보안이 주체를 너무 구성한**SetupEntryPoint**합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="99bcc-126">이렇게 하면 서비스 패브릭 하는 경우 hello **MySetup.bat** 파일을 실행 하는 것, `RunAs` 관리자 권한으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="99bcc-127">있다면 *하지* 적용 정책 toohello 주 진입점의 hello 코드 **MyServiceHost.exe** hello 시스템에서 실행 **NetworkService** 계정.</span><span class="sxs-lookup"><span data-stu-id="99bcc-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="99bcc-128">모든 서비스 진입점으로 실행 하는 hello 기본 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="99bcc-129">이제 hello 파일 MySetup.bat toohello Visual Studio 프로젝트 tootest hello 관리자 권한이 추가해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="99bcc-130">Visual Studio에서 hello 서비스 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 MySetup.bat 이라는 새 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="99bcc-131">다음으로 hello 서비스 패키지에 해당 hello MySetup.bat 파일이 포함 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="99bcc-132">기본적으로 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-132">By default, it is not.</span></span> <span data-ttu-id="99bcc-133">Hello 파일 선택 tooget hello 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="99bcc-134">Hello 속성 대화 상자에서 **tooOutput 디렉터리 복사** 너무 설정**변경 된 내용만 복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="99bcc-135">다음 스크린 샷 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="99bcc-135">See hello following screenshot.</span></span>

![SetupEntryPoint 배치 파일에 대한 Visual Studio CopyToOutput][image1]

<span data-ttu-id="99bcc-137">이제 hello MySetup.bat 파일을 열고 추가 명령을 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="99bcc-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="99bcc-138">다음으로, 빌드 및 hello 솔루션 tooa 로컬 개발 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="99bcc-139">Hello 서비스가 시작 서비스 패브릭 탐색기에 표시 된 것 처럼, 해당 hello MySetup.bat 파일 두 가지 방법으로 성공적으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="99bcc-140">Azure PowerShell 명령 프롬프트를 열고 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="99bcc-141">그런 다음 note hello 이름 hello 노드 hello 서비스의 배포 된 및 예를 들어 노드 2에서 서비스 패브릭 탐색기-시작 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="99bcc-142">다음으로 toohello 응용 프로그램 인스턴스 작업 폴더 toofind hello out.txt 파일이 hello 값을 보여 주는 이동 **TestVariable**합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="99bcc-143">예를 들어이 서비스에 배포 된 tooNode 2 되었으면 있습니다 수 이동 하 여 hello에 대 한 toothis 경로 **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="99bcc-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="99bcc-144">로컬 시스템 계정을 사용 하 여 hello 정책 구성</span><span class="sxs-lookup"><span data-stu-id="99bcc-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="99bcc-145">대개는 관리자 계정이 아닌 로컬 시스템 계정을 사용 하 여 선호 toorun hello 시작 스크립트는.</span><span class="sxs-lookup"><span data-stu-id="99bcc-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="99bcc-146">관리자 그룹 일반적으로 작동 하지 않는 컴퓨터에 액세스 제어 UAC (사용자) 기본적으로 사용할 수 있어야 하기 때문에 잘 hello의 구성원으로 hello RunAs 정책을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="99bcc-147">이러한 경우 **hello 좋습니다 toorun hello LocalSystem으로 SetupEntryPoint 대신 tooAdministrators 추가 된 로컬 사용자 그룹으로**합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="99bcc-148">hello 다음 예제는 hello SetupEntryPoint toorun 설정을 LocalSystem으로.</span><span class="sxs-lookup"><span data-stu-id="99bcc-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="99bcc-149">설치 진입점에서 PowerShell 명령 시작</span><span class="sxs-lookup"><span data-stu-id="99bcc-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="99bcc-150">hello에서 PowerShell toorun **SetupEntryPoint** 지점을 실행할 수 있습니다 **PowerShell.exe** tooa PowerShell 가리키는 배치 파일에서 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="99bcc-151">먼저 PowerShell 파일 toohello 서비스 프로젝트-예를 들어 추가 **MySetup.ps1**합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="99bcc-152">Tooset hello 기억 *변경 된 내용만 복사* 속성이 해당 hello 파일 hello 서비스 패키지에도 포함 되어 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="99bcc-153">hello 다음 예제 MySetup.ps1 라는 시스템 환경 변수를 설정 하 라는 PowerShell 파일을 시작 하는 샘플 배치 파일 **TestVariable**합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="99bcc-154">MySetup.bat toostart PowerShell 파일:</span><span class="sxs-lookup"><span data-stu-id="99bcc-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="99bcc-155">Hello PowerShell 파일에서 hello 다음 tooset 시스템 환경 변수를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="99bcc-156">기본적으로 hello 배치 파일을 실행할 때 확인 hello 라고 하는 응용 프로그램 폴더 **작동** 파일에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="99bcc-157">이 경우 MySetup.bat 실행 될 때 원하는 hello에이 toofind hello MySetup.ps1 파일 같은 hello 응용 프로그램 폴더에 **코드 패키지** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="99bcc-158">toochange이 폴더, 집합 hello 작업 폴더:</span><span class="sxs-lookup"><span data-stu-id="99bcc-158">toochange this folder, set hello working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="99bcc-159">로컬 디버깅에 대한 콘솔 리디렉션 사용</span><span class="sxs-lookup"><span data-stu-id="99bcc-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="99bcc-160">경우에 따라 디버깅을 위해 스크립트 실행에서 유용한 toosee hello 콘솔 출력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="99bcc-161">toodo이 hello 출력 tooa 파일을 작성 하는 콘솔 리디렉션을 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="99bcc-162">hello 파일 출력 toohello 작성 된 응용 프로그램 폴더 라고 **로그** hello 노드에서 hello 응용 프로그램은 배포 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="99bcc-163">(참조 위치 toofind hello 이전 예제에서에서이.)</span><span class="sxs-lookup"><span data-stu-id="99bcc-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="99bcc-164">Hello 콘솔 리디렉션 정책 hello 응용 프로그램 장애 조치에 영향을 줄 수 있으므로 프로덕션에 배포 된 응용 프로그램에서 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="99bcc-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="99bcc-165">로컬 개발 및 디버깅 목적으로*만* 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="99bcc-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="99bcc-166">hello 다음 예제는 FileRetentionCount 값이 있는 hello 콘솔 리디렉션을 설정.</span><span class="sxs-lookup"><span data-stu-id="99bcc-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="99bcc-167">Hello MySetup.ps1 파일 toowrite 지금 변경 하는 경우는 **에코** 명령,이 디버깅을 위해 toohello 출력 파일을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="99bcc-168">**스크립트를 디버그한 후 즉시 이 콘솔 리디렉션 정책을 제거합니다.**</span><span class="sxs-lookup"><span data-stu-id="99bcc-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="99bcc-169">서비스 코드 패키지에 대한 정책 구성</span><span class="sxs-lookup"><span data-stu-id="99bcc-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="99bcc-170">Hello 이전 단계에서에서 언급 했 듯이 어떻게 tooapply RunAs 정책 tooSetupEntryPoint 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="99bcc-171">살펴보겠습니다 좀 더 자세히 방식으로 적용할 수 있는 toocreate 다른 보안 주체 서비스 정책에.</span><span class="sxs-lookup"><span data-stu-id="99bcc-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="99bcc-172">로컬 사용자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="99bcc-172">Create local user groups</span></span>
<span data-ttu-id="99bcc-173">정의 하 고 하나를 사용할 수 있는 사용자 그룹을 만들 수 또는 더 많은 사용자가 toobe tooa 그룹에 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="99bcc-174">다른 서비스 진입점에 대 한 여러 사용자가 있으며 toohave hello 그룹 수준에서 사용할 수 있는 일반적인 특정 권한이 필요한 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="99bcc-175">hello 다음 보여 주는 예제 라는 로컬 그룹이 **LocalAdminGroup** 관리자 권한이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="99bcc-176">두 사용자 Customer1과 Customer2를 이 그룹 구성원으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="99bcc-177">로컬 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="99bcc-177">Create local users</span></span>
<span data-ttu-id="99bcc-178">Hello 응용 프로그램 내에서 서비스 보안 사용된 toohelp 일 수 있는 로컬 사용자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="99bcc-179">경우는 **LocalUser** 계정 유형의 서비스 패브릭 hello 응용 프로그램 배포 된 컴퓨터에서 로컬 사용자 계정을 만들어 hello 응용 프로그램 매니페스트의 hello 주체 섹션에 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="99bcc-180">기본적으로 이러한 계정 (예: hello 샘플 다음에 Customer3) hello 응용 프로그램에 지정 된 것과 같은 이름을 매니페스트 hello를 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="99bcc-181">대신 동적으로 생성되며 임의 암호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="99bcc-182">응용 프로그램이 필요한 경우 hello 사용자 계정 및 암호가 모든 컴퓨터 (예를 들어 tooenable NTLM 인증)에 동일한 수, hello 클러스터 매니페스트 NTLMAuthenticationEnabled tootrue를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="99bcc-183">hello 클러스터 매니페스트도 지정 해야 사용 되는 NTLMAuthenticationPasswordSecret toogenerate 모든 컴퓨터에 같은 암호를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="99bcc-184">할당 정책을 toohello 서비스 코드 패키지</span><span class="sxs-lookup"><span data-stu-id="99bcc-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="99bcc-185">hello **RunAsPolicy** 섹션는 **ServiceManifestImport** hello 계정을 사용 하는 코드 패키지 toorun 되어야 하는 hello 주체 섹션에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="99bcc-186">또한 코드 hello 서비스에서 패키지 매니페스트 hello 주체 섹션에서 사용자 계정으로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="99bcc-187">Hello 설치 프로그램 또는 주 진입점에 대 한이 지정할 수 있습니다 또는 지정할 수 있습니다 `All` tooapply 것 tooboth 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="99bcc-188">hello 다음 예제는 서로 다른 정책 적용.</span><span class="sxs-lookup"><span data-stu-id="99bcc-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="99bcc-189">경우 **EntryPointType** 를 지정 하지 않으면 hello 기본값은 tooEntryPointType 설정 = "Main"입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="99bcc-190">지정 **SetupEntryPoint** toorun 시스템 계정에서 특정 권한이 높은 설치 작업을 사용할 때 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="99bcc-191">hello 실제 서비스 코드 보다 낮은 권한 계정으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="99bcc-192">기본 정책 tooall 서비스 코드 패키지를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="99bcc-193">Hello를 사용 하 여 **DefaultRunAsPolicy** 섹션 toospecify 특정 하지 않은 모든 코드 패키지에 대 한 기본 사용자 계정 **RunAsPolicy** 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="99bcc-194">대부분의 응용 프로그램에서 사용 하는 hello 서비스 매니페스트에 지정 된 hello 코드 패키지에서 toorun 필요 hello 동일한 사용자 hello 응용 프로그램이 해당 사용자 계정 가진 기본 실행 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="99bcc-195">hello 다음 예제에서는 지정 하는 코드 패키지에 없는 경우는 **RunAsPolicy** 지정 hello 코드 패키지를 실행할 hello **MyDefaultAccount** hello 주체 섹션에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="99bcc-196">Active Directory 도메인 그룹 또는 사용자 사용</span><span class="sxs-lookup"><span data-stu-id="99bcc-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="99bcc-197">서비스 패브릭 hello 독립 실행형 설치 관리자를 사용 하 여 Windows Server에 설치 된 인스턴스에 대 한 Active Directory 사용자 또는 그룹 계정에 대 한 hello 자격 증명으로 hello 서비스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="99bcc-198">도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="99bcc-199">도메인 사용자 또는 그룹을 사용 하 여 권한을 부여 받은 기타 리소스 hello 도메인 (예: 파일 공유)에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="99bcc-200">hello 다음 예제에서는 Active Directory 사용자를 호출 *TestUser* 가 도메인 인증서를 사용 하 여 암호화 된 암호 호출 *MyCert*합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="99bcc-201">Hello를 사용할 수 있습니다 `Invoke-ServiceFabricEncryptText` PowerShell 명령 toocreate hello 비밀 암호화 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="99bcc-202">자세한 내용은 [Service Fabric 응용 프로그램의 비밀 관리](service-fabric-application-secret-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99bcc-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="99bcc-203">밴드의 범위를 벗어난 메서드를 사용 하 여 hello hello 인증서 toodecrypt hello 암호 toohello 로컬 컴퓨터의 개인 키를 배포 해야 (azure에서이 Azure 리소스 관리자를 통해).</span><span class="sxs-lookup"><span data-stu-id="99bcc-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="99bcc-204">그런 다음 서비스 패브릭 hello 서비스 패키지 toohello 컴퓨터를 배포 하면 수 toodecrypt hello 암호로 및 hello 사용자 이름) (함께 Active Directory toorun 이러한 자격 증명을 사용 하 여 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="99bcc-205">그룹 관리 서비스 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="99bcc-206">서비스 패브릭 hello 독립 실행형 설치 관리자를 사용 하 여 Windows Server에 설치 된 인스턴스에 대 한 hello 서비스 그룹 관리 서비스 계정 (gMSA)로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="99bcc-207">도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="99bcc-208">GMSA를 사용 하 여 암호 또는 없을 hello에 저장 된 암호화 된 암호 `Application Manifest`합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="99bcc-209">hello 다음 예제에서는 호출 방법을 보여 줍니다 toocreate gMSA 계정 *svc 테스트 $*toodeploy를 관리 하는 방법은; 서비스 계정 toohello 클러스터 노드; 및 어떻게 tooconfigure hello 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="99bcc-210">필수 조건.</span><span class="sxs-lookup"><span data-stu-id="99bcc-210">Prerequisites.</span></span>
- <span data-ttu-id="99bcc-211">hello 도메인 KDS 루트 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="99bcc-212">hello 도메인 기능 수준을 이상 또는 Windows Server 2012에서 toobe가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="99bcc-213">예제</span><span class="sxs-lookup"><span data-stu-id="99bcc-213">Example</span></span>
1. <span data-ttu-id="99bcc-214">Hello를 사용 하 여 그룹 관리 서비스 계정을 만드는 active directory 도메인 관리자가 `New-ADServiceAccount` commandlet 해당 hello 확인 `PrincipalsAllowedToRetrieveManagedPassword` hello 서비스 패브릭 클러스터 노드를 모두 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="99bcc-215">`AccountName`, `DnsHostName` 및 `ServicePrincipalName`이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="99bcc-216">각 hello 서비스 패브릭 클러스터 노드에서 (예를 들어 `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`) 설치 하 고 hello gMSA를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="99bcc-217">Hello 사용자 계정 구성 하 고 hello RunAsPolicy tooreference hello 사용자를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="99bcc-218">HTTP 및 HTTPS 끝점에 보안 액세스 정책 할당</span><span class="sxs-lookup"><span data-stu-id="99bcc-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="99bcc-219">실행 정책 tooa 서비스를 적용 하 고 hello HTTP 프로토콜을 사용 하 여 끝점 리소스를 선언 하는 hello 서비스 매니페스트를 지정 해야 합니다는 **SecurityAccessPolicy** tooensure toothese 끝점 포트에 할당 되는 요소가 올바르게 hello에 대 한 hello 서비스가 실행 되는 실행 사용자 계정을 나열 하는 액세스 제어.</span><span class="sxs-lookup"><span data-stu-id="99bcc-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="99bcc-220">그렇지 않으면 **http.sys** 액세스 toohello 서비스가 되어 있지 않으며 hello 클라이언트에서 호출 에서도 오류를 받아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="99bcc-221">hello 다음 예제에서는 적용 라는 hello Customer1 계정 tooan 끝점 **EndpointName**, 모든 액세스 권한을 제공 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="99bcc-222">Hello HTTPS 끝점에 대 한 hello 인증서 tooreturn toohello 클라이언트의 tooindicate hello 이름을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="99bcc-223">사용 하 여이 작업을 수행할 수 **EndpointBindingPolicy**, hello 응용 프로그램 매니페스트에서 인증서 섹션에 정의 된 hello 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="99bcc-224">https 끝점으로 여러 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="99bcc-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="99bcc-225">Toobe 주의 필요 하지 toouse hello **동일한 포트** hello의 다른 인스턴스에 대해 http를 사용 하는 경우 동일한 응용 프로그램**s**합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="99bcc-226">hello 이유가 서비스 패브릭이 hello 응용 프로그램 인스턴스 중 하나에 대 한 수 tooupgrade hello 인증서를 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="99bcc-227">예를 들어, 응용 프로그램 1 개 또는 응용 프로그램 2 두 원하는 tooupgrade 자신의 인증서 1 toocert 2입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="99bcc-228">Hello 업그레이드 문제가 발생 하면 서비스 패브릭 정리 수 http.sys 사용 하 여 hello 인증서 1 등록 hello 다른 응용 프로그램은 사용 중인 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="99bcc-229">tooprevent이를 서비스 패브릭에서 hello 인증서를 사용 하 여 hello 포트에 등록 하는 다른 응용 프로그램 인스턴스가 이미 임을 감지한 (due toohttp.sys) 및 실패 hello 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="99bcc-230">따라서 서비스 패브릭 지원 하지 않습니다 두 개의 서로 다른 서비스를 사용 하 여 업그레이드 **동일한 포트 hello** 서로 다른 응용 프로그램의 경우.</span><span class="sxs-lookup"><span data-stu-id="99bcc-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="99bcc-231">Hello에 서로 다른 서비스에 동일한 인증서 hello을 사용할 수 없습니다 즉, 동일한 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="99bcc-232">Toohave 필요한 경우 공유 인증서에 hello 동일한 포트 tooensure 배치 제약 조건으로 서로 다른 컴퓨터에 대 한 서비스 사항은 해당 hello를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="99bcc-233">또는 각 응용 프로그램 인스턴스에서 각 서비스에 대해 Service Fabric 동적 포트를 사용하는 것이 좋습니다(가능한 경우).</span><span class="sxs-lookup"><span data-stu-id="99bcc-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="99bcc-234">Https로 업그레이드는 실패를 표시 하는 경우 "hello Windows HTTP 서버 API 지원 하지 않습니다 여러 인증서를 포트를 공유 하는 응용 프로그램에 대 한." 메시지가 표시 되는 오류 경고</span><span class="sxs-lookup"><span data-stu-id="99bcc-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="99bcc-235">완전한 응용 프로그램 매니페스트의 예</span><span class="sxs-lookup"><span data-stu-id="99bcc-235">A complete application manifest example</span></span>
<span data-ttu-id="99bcc-236">다른 설정을 응용 프로그램 매니페스트를 수행 하는 hello 다양 한 hello를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="99bcc-236">hello following application manifest shows many of hello different settings:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="99bcc-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="99bcc-237">Next steps</span></span>
* [<span data-ttu-id="99bcc-238">Hello 응용 프로그램 모델 이해</span><span class="sxs-lookup"><span data-stu-id="99bcc-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="99bcc-239">서비스 매니페스트에서 리소스 지정</span><span class="sxs-lookup"><span data-stu-id="99bcc-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="99bcc-240">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="99bcc-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
