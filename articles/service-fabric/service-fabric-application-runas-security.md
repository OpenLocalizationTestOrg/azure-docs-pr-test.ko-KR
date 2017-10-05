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
ms.openlocfilehash: e673b45a43a06d18040c3437caf8765704d5c36a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="e13ca-103">응용 프로그램에 대한 보안 정책 구성</span><span class="sxs-lookup"><span data-stu-id="e13ca-103">Configure security policies for your application</span></span>
<span data-ttu-id="e13ca-104">Azure Service Fabric을 사용하여 다른 사용자 계정으로 클러스터에서 실행 중인 응용 프로그램을 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-104">By using Azure Service Fabric, you can secure applications that are running in the cluster under different user accounts.</span></span> <span data-ttu-id="e13ca-105">또한 Service Fabric으로 배포 시 파일, 디렉터리, 인증서 등과 같은 사용자 계정을 통해 응용 프로그램에서 사용하는 리소스도 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-105">Service Fabric also helps secure the resources that are used by applications at the time of deployment under the user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="e13ca-106">따라서 공유되는 호스티드 환경에서도 서로 더욱 안전하게 응용 프로그램을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="e13ca-107">기본적으로 서비스 패브릭 응용 프로그램은 Fabric.exe 프로세스가 실행하는 계정을 통해 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-107">By default, Service Fabric applications run under the account that the Fabric.exe process runs under.</span></span> <span data-ttu-id="e13ca-108">또한 Service Fabric은 응용 프로그램의 매니페스트 내에 지정된 로컬 사용자 계정 또는 로컬 시스템 계정을 통해 응용 프로그램을 실행하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-108">Service Fabric also provides the capability to run applications under a local user account or local system account, which is specified within the application manifest.</span></span> <span data-ttu-id="e13ca-109">지원되는 로컬 시스템 계정 유형은 **LocalUser**, **NetworkService**, **LocalService** 및 **LocalSystem**입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="e13ca-110">독립 실행형 설치 관리자를 사용하여 데이터 센터의 Windows Server에서 Service Fabric을 실행하는 경우 그룹 관리 서비스 계정을 포함하여 Active Directory 도메인 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-110">When you're running Service Fabric on Windows Server in your datacenter by using the standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="e13ca-111">사용자 그룹을 정의하고 만들었으므로 각 그룹에 사용자를 한 명 이상 추가하여 한꺼번에 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-111">You can define and create user groups so that one or more users can be added to each group to be managed together.</span></span> <span data-ttu-id="e13ca-112">이 기능은 여러 서비스 진입점에 대한 사용자가 여러 명 있고 그 사용자들에게 그룹 수준에서 특정 공통 권한을 부여해야 하는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-112">This is useful when there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span>

## <a name="configure-the-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="e13ca-113">서비스 설치 진입점에 대한 정책 구성</span><span class="sxs-lookup"><span data-stu-id="e13ca-113">Configure the policy for a service setup entry point</span></span>
<span data-ttu-id="e13ca-114">[응용 프로그램 모델](service-fabric-application-model.md)에서 설명한 것처럼 설치 진입점인 **SetupEntryPoint**는 Service Fabric과 같은 자격 증명(일반적으로 *NetworkService* 계정)을 사용하여 다른 진입점보다 먼저 실행되는 권한 있는 진입점입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-114">As described in the [application model](service-fabric-application-model.md), the setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with the same credentials as Service Fabric (typically the *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="e13ca-115">**EntryPoint**로 지정되는 실행 파일은 일반적으로 장기 실행 서비스 호스트입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-115">The executable that is specified by **EntryPoint** is typically the long-running service host.</span></span> <span data-ttu-id="e13ca-116">별도의 설치 진입점이 있으면 한동안은 높은 권한을 사용하여 서비스 호스트를 실행하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-116">So having a separate setup entry point avoids having to run the service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="e13ca-117">**EntryPoint**로 지정된 실행 파일은 **SetupEntryPoint**가 성공적으로 종료된 후 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-117">The executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="e13ca-118">종료되지 않거나 충돌하는 경우 결과 프로세스를 모니터링하여 다시 시작합니다(**SetupEntryPoint**를 사용하여 다시 시작).</span><span class="sxs-lookup"><span data-stu-id="e13ca-118">The resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="e13ca-119">다음은 서비스에 대한 SetupEntryPoint 및 기본 EntryPoint를 보여주는 서비스 매니페스트의 간단한 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-119">The following is a simple service manifest example that shows the SetupEntryPoint and the main EntryPoint for the service.</span></span>

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

### <a name="configure-the-policy-by-using-a-local-account"></a><span data-ttu-id="e13ca-120">로컬 계정을 사용하여 정책 구성</span><span class="sxs-lookup"><span data-stu-id="e13ca-120">Configure the policy by using a local account</span></span>
<span data-ttu-id="e13ca-121">설치 항목 지점이 있도록 서비스를 구성한 후에 응용 프로그램 매니페스트에서 아래에서 실행되는 보안 권한을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-121">After you configure the service to have a setup entry point, you can change the security permissions that it runs under in the application manifest.</span></span> <span data-ttu-id="e13ca-122">다음은 사용자 관리자 계정 권한으로 실행되도록 서비스를 구성하는 방법을 보여 주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-122">The following example shows how to configure the service to run under user administrator account privileges.</span></span>

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

<span data-ttu-id="e13ca-123">먼저, 사용자 이름(예: SetupAdminUser)을 사용하여 **주체** 섹션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="e13ca-124">이 사용자가 관리자 시스템 그룹의 구성원임을 나타내는 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-124">This indicates that the user is a member of the Administrators system group.</span></span>

<span data-ttu-id="e13ca-125">다음으로, **ServiceManifestImport** 섹션에서 정책을 구성하여 이 주체를 **SetupEntryPoint**에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-125">Next, under the **ServiceManifestImport** section, configure a policy to apply this principal to **SetupEntryPoint**.</span></span> <span data-ttu-id="e13ca-126">이렇게 하면 Service Fabric에서는 **MySetup.bat** 파일이 실행될 때 관리자 권한이 있는 `RunAs`인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-126">This tells Service Fabric that when the **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="e13ca-127">기본 진입점에 정책을 적용하지 *않으면* **MyServiceHost.exe**의 코드가 시스템 **NetworkService** 계정에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-127">Given that you have *not* applied a policy to the main entry point, the code in **MyServiceHost.exe** runs under the system **NetworkService** account.</span></span> <span data-ttu-id="e13ca-128">이 계정은 모든 서비스 진입점이 run as인 기본 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-128">This is the default account that all service entry points are run as.</span></span>

<span data-ttu-id="e13ca-129">이제 MySetup.bat 파일을 Visual Studio 프로젝트에 추가하여 관리자 권한을 테스트하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-129">Let's now add the file MySetup.bat to the Visual Studio project to test the administrator privileges.</span></span> <span data-ttu-id="e13ca-130">Visual Studio에서 서비스 프로젝트를 마우스 오른쪽 단추로 클릭하고 새 파일 MySetup.bat을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-130">In Visual Studio, right-click the service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="e13ca-131">다음으로 MySetup.bat 파일이 서비스 패키지에 포함되어 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-131">Next, ensure that the MySetup.bat file is included in the service package.</span></span> <span data-ttu-id="e13ca-132">기본적으로 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-132">By default, it is not.</span></span> <span data-ttu-id="e13ca-133">파일을 선택하고 상황에 맞는 메뉴를 마우스 오른쪽 단추로 클릭하며 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-133">Select the file, right-click to get the context menu, and choose **Properties**.</span></span> <span data-ttu-id="e13ca-134">속성 대화 상자에서 **출력 디렉터리로 복사**가 **변경된 내용만 복사**로 설정되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-134">In the Properties dialog box, ensure that **Copy to Output Directory** is set to **Copy if newer**.</span></span> <span data-ttu-id="e13ca-135">다음 스크린샷이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-135">See the following screenshot.</span></span>

![SetupEntryPoint 배치 파일에 대한 Visual Studio CopyToOutput][image1]

<span data-ttu-id="e13ca-137">이제 MySetup.bat 파일을 열고 다음 명령을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-137">Now open the MySetup.bat file and add the following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set to > out.txt
echo %TestVariable% >> out.txt

REM To delete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="e13ca-138">다음으로 솔루션을 빌드하여 로컬 개발 클러스터에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-138">Next, build and deploy the solution to a local development cluster.</span></span> <span data-ttu-id="e13ca-139">서비스가 시작되면 Service Fabric Explorer에 표시된 대로 MySetup.bat 파일이 두 가지 방법으로 성공한 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-139">After the service has started, as shown in Service Fabric Explorer, you can see that the MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="e13ca-140">Azure PowerShell 명령 프롬프트를 열고 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="e13ca-141">그런 다음 서비스가 배포되고 Service Fabric Explorer에서 시작된 노드의 이름(예: 노드2)을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-141">Then, note the name of the node where the service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="e13ca-142">다음으로 응용 프로그램 인스턴스 작업 폴더로 이동하여 **TestVariable**값을 보여주는 out.txt 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-142">Next, navigate to the application instance work folder to find the out.txt file that shows the value of **TestVariable**.</span></span> <span data-ttu-id="e13ca-143">예를 들어 이 서비스가 노드 2에 배포된 경우 **MyApplicationType**에 대한 이 경로로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-143">For example, if this service was deployed to Node 2, then you can go to this path for the **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-the-policy-by-using-local-system-accounts"></a><span data-ttu-id="e13ca-144">로컬 시스템 계정을 사용하여 정책 구성</span><span class="sxs-lookup"><span data-stu-id="e13ca-144">Configure the policy by using local system accounts</span></span>
<span data-ttu-id="e13ca-145">관리자 계정이 아닌 로컬 시스템 계정을 사용하여 스크립트의 시작을 실행하는 것이 일반적으로 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-145">Often, it's preferable to run the startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="e13ca-146">컴퓨터는 기본적으로 UAC(사용자 액세스 제어)를 사용하도록 설정되어 있기 때문에 관리자 그룹의 구성원으로 RunAs 정책을 실행하면 일반적으로 잘 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-146">Running the RunAs policy as a member of the Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="e13ca-147">이러한 경우 **관리자 그룹에 추가된 로컬 사용자 대신 LocalSystem으로 SetupEntryPoint를 실행하는 것이 좋습니다**.</span><span class="sxs-lookup"><span data-stu-id="e13ca-147">In such cases, **the recommendation is to run the SetupEntryPoint as LocalSystem, instead of as a local user added to Administrators group**.</span></span> <span data-ttu-id="e13ca-148">다음 예제에서는 LocalSystem으로 실행하도록 SetupEntryPoint를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-148">The following example shows setting the SetupEntryPoint to run as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="e13ca-149">설치 진입점에서 PowerShell 명령 시작</span><span class="sxs-lookup"><span data-stu-id="e13ca-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="e13ca-150">**SetupEntryPoint** 지점에서 PowerShell을 실행하려면 PowerShell 파일을 가리키는 배치 파일에서 **PowerShell.exe**를 실행하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-150">To run PowerShell from the **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points to a PowerShell file.</span></span> <span data-ttu-id="e13ca-151">먼저 서비스 프로젝트(예: **MySetup.ps1**)에 PowerShell 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-151">First, add a PowerShell file to the service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="e13ca-152">이 파일도 서비스 패키지에 포함되도록 *변경된 내용만 복사* 속성을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-152">Remember to set the *Copy if newer* property so that the file is also included in the service package.</span></span> <span data-ttu-id="e13ca-153">다음은 **TestVariable**이라는 시스템 환경 변수를 설정하는 PowerShell 파일 MySetup.ps1을 시작하는 간단한 배치 파일을 보여 주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-153">The following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="e13ca-154">PowerShell 파일을 시작하기 위한 MySetup.bat입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-154">MySetup.bat to start a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="e13ca-155">PowerShell 파일에서 다음을 추가하여 시스템 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-155">In the PowerShell file, add the following to set a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="e13ca-156">기본적으로 배치 파일이 실행될 때 **work**라는 응용 프로그램 폴더에서 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-156">By default, when the batch file runs, it looks at the application folder called **work** for files.</span></span> <span data-ttu-id="e13ca-157">이 경우 MySetup.bat가 실행될 때 같은 폴더(응용 프로그램 **코드 패키지** 폴더)에서 MySetup.ps1 파일을 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-157">In this case, when MySetup.bat runs, we want this to find the MySetup.ps1 file in the same folder, which is the application **code package** folder.</span></span> <span data-ttu-id="e13ca-158">이 폴더를 변경하려면 아래와 같이 작업 폴더를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-158">To change this folder, set the working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="e13ca-159">로컬 디버깅에 대한 콘솔 리디렉션 사용</span><span class="sxs-lookup"><span data-stu-id="e13ca-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="e13ca-160">디버깅 목적으로 스크립트를 실행하여 콘솔 출력을 확인하는 것이 유용할 때가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-160">Occasionally, it's useful to see the console output from running a script for debugging purposes.</span></span> <span data-ttu-id="e13ca-161">이 작업을 수행하기 위해 파일에 출력을 기록하는 콘솔 리디렉션 정책을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-161">To do this, you can set a console redirection policy, which writes the output to a file.</span></span> <span data-ttu-id="e13ca-162">파일 출력은 응용 프로그램이 배포되고 실행되는 노드에 **log**라는 응용 프로그램 폴더에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-162">The file output is written to the application folder called **log** on the node where the application is deployed and run.</span></span> <span data-ttu-id="e13ca-163">(앞의 예제에서 이를 찾을 수 있는 위치 참조)</span><span class="sxs-lookup"><span data-stu-id="e13ca-163">(See where to find this in the preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="e13ca-164">절대 프로덕션에 배포된 응용 프로그램의 콘솔 리디렉션 정책은 사용하지 마세요. 응용 프로그램 장애 조치(failover)에 영향을 줄 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-164">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="e13ca-165">로컬 개발 및 디버깅 목적으로*만* 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="e13ca-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="e13ca-166">다음 예제에서는 콘솔 리디렉션을 FileRetentionCount 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-166">The following example shows setting the console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="e13ca-167">이제 MySetup.ps1 파일을 변경하여 **Echo** 명령을 작성하면 디버깅 목적으로 출력 파일에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-167">If you now change the MySetup.ps1 file to write an **Echo** command, this will write to the output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes to the application log folder on the node that the application is deployed to"
```

<span data-ttu-id="e13ca-168">**스크립트를 디버그한 후 즉시 이 콘솔 리디렉션 정책을 제거합니다.**</span><span class="sxs-lookup"><span data-stu-id="e13ca-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="e13ca-169">서비스 코드 패키지에 대한 정책 구성</span><span class="sxs-lookup"><span data-stu-id="e13ca-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="e13ca-170">이전 단계에서 SetupEntryPoint에 RunAs 정책을 적용하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-170">In the preceding steps, you saw how to apply a RunAs policy to SetupEntryPoint.</span></span> <span data-ttu-id="e13ca-171">이번에는 서비스 정책으로 적용할 수 있는 다양한 주체를 만드는 방법을 좀 더 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-171">Let's look a little deeper into how to create different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="e13ca-172">로컬 사용자 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e13ca-172">Create local user groups</span></span>
<span data-ttu-id="e13ca-173">그룹에 사용자를 한 명 이상 추가하도록 사용자 그룹을 정의하고 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-173">You can define and create user groups that allow one or more users to be added to a group.</span></span> <span data-ttu-id="e13ca-174">이 기능은 여러 서비스 진입점에 대한 사용자가 여러 명 있고 그 사용자들에게 그룹 수준에서 특정 공통 권한을 부여해야 하는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-174">This is useful if there are multiple users for different service entry points and they need to have certain common privileges that are available at the group level.</span></span> <span data-ttu-id="e13ca-175">다음은 관리자 권한이 있는 **LocalAdminGroup**이라는 로컬 그룹을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-175">The following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="e13ca-176">두 사용자 Customer1과 Customer2를 이 그룹 구성원으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="e13ca-177">로컬 사용자 만들기</span><span class="sxs-lookup"><span data-stu-id="e13ca-177">Create local users</span></span>
<span data-ttu-id="e13ca-178">응용 프로그램 내에서 서비스를 보호하는 데 사용할 수 있는 로컬 사용자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-178">You can create a local user that can be used to help secure a service within the application.</span></span> <span data-ttu-id="e13ca-179">응용 프로그램 매니페스트의 주체 섹션에서 **LocalUser** 계정 형식이 지정되면 Service Fabric에서는 응용 프로그램이 배포되는 컴퓨터에 로컬 사용자 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-179">When a **LocalUser** account type is specified in the principals section of the application manifest, Service Fabric creates local user accounts on machines where the application is deployed.</span></span> <span data-ttu-id="e13ca-180">기본적으로 이러한 계정은 응용 프로그램 매니페스트(예: 다음 샘플의 Customer3)에 지정된 것과 동일한 이름을 갖지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-180">By default, these accounts do not have the same names as those specified in the application manifest (for example, Customer3 in the following sample).</span></span> <span data-ttu-id="e13ca-181">대신 동적으로 생성되며 임의 암호를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="e13ca-182">응용 프로그램에서 사용자 계정과 암호가 모든 컴퓨터에서 같도록 요구할 경우(예: NTLM 인증을 사용하기 위해) 클러스터 매니페스트는 NTLMAuthenticationEnabled를 true로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-182">If an application requires that the user account and password be same on all machines (for example, to enable NTLM authentication), the cluster manifest must set NTLMAuthenticationEnabled to true.</span></span> <span data-ttu-id="e13ca-183">클러스터 매니페스트는 모든 컴퓨터에서 동일한 암호를 생성하는 데 사용된 NTLMAuthenticationPasswordSecret도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-183">The cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used to generate the same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-to-the-service-code-packages"></a><span data-ttu-id="e13ca-184">서비스 코드 패키지에 정책 할당</span><span class="sxs-lookup"><span data-stu-id="e13ca-184">Assign policies to the service code packages</span></span>
<span data-ttu-id="e13ca-185">**ServiceManifestImport**에 대한 **RunAsPolicy** 섹션은 코드 패키지를 실행하는 데 사용되어야 하는 주체 섹션에서 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-185">The **RunAsPolicy** section for a **ServiceManifestImport** specifies the account from the principals section that should be used to run a code package.</span></span> <span data-ttu-id="e13ca-186">또한 서비스 매니페스트에서 코드 패키지를 주체 섹션에서 사용자 계정과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-186">It also associates code packages from the service manifest with user accounts in the principals section.</span></span> <span data-ttu-id="e13ca-187">설정 또는 기본 진입점에 대해 이 정책을 적용할 수도 있고 `All` 을 지정하여 양쪽에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-187">You can specify this for the setup or main entry points, or you can specify `All` to apply it to both.</span></span> <span data-ttu-id="e13ca-188">다음은 여러 정책을 적용하는 방법을 보여주는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-188">The following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="e13ca-189">**EntryPointType** 을 지정하지 않으면 기본적으로 EntryPointType=”Main”으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-189">If **EntryPointType** is not specified, the default is set to EntryPointType=”Main”.</span></span> <span data-ttu-id="e13ca-190">특히 시스템 계정에서 특정 고수준 권한 설정 작업을 실행하려면 **SetupEntryPoint**를 지정하는 것이 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-190">Specifying **SetupEntryPoint** is especially useful when you want to run certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="e13ca-191">실제 서비스 코드는 낮은 권한 계정으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-191">The actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-to-all-service-code-packages"></a><span data-ttu-id="e13ca-192">모든 서비스 코드 패키지에 기본 정책 적용</span><span class="sxs-lookup"><span data-stu-id="e13ca-192">Apply a default policy to all service code packages</span></span>
<span data-ttu-id="e13ca-193">**DefaultRunAsPolicy** 섹션은 특정 **RunAsPolicy**가 정의되지 않은 모든 코드 패키지에 대해 기본 사용자 계정을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-193">You use the **DefaultRunAsPolicy** section to specify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="e13ca-194">응용 프로그램에서 사용하는 서비스 매니페스트에 지정된 대부분의 코드 패키지가 동일한 사용자를 통해 실행되어야 하는 경우 응용 프로그램에서 해당 사용자 계정을 사용하여 기본 RunAs 정책을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-194">If most of the code packages that are specified in the service manifest used by an application need to run under the same user, the application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="e13ca-195">다음은 코드 패키지의 **RunAsPolicy**가 지정되지 않으면 주체 섹션에 지정된 **MyDefaultAccount**에서 코드 패키지가 수행되는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-195">The following example specifies that if a code package does not have a **RunAsPolicy** specified, the code package should run under the **MyDefaultAccount** specified in the principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="e13ca-196">Active Directory 도메인 그룹 또는 사용자 사용</span><span class="sxs-lookup"><span data-stu-id="e13ca-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="e13ca-197">독립 실행형 설치 관리자를 사용하여 Windows Server에 설치된 Service Fabric 인스턴스의 경우 Active Directory 사용자 또는 그룹 계정에 대한 자격 증명으로 서비스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-197">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service under the credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="e13ca-198">도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e13ca-199">도메인 사용자 또는 그룹을 사용하여 권한이 부여된 도메인의 다른 리소스(예: 파일 공유)에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-199">By using a domain user or group, you can then access other resources in the domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="e13ca-200">다음 예제는 *TestUser*라는 Active Directory 사용자와 *MyCert*라는 인증서를 사용하여 암호화된 도메인 암호를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-200">The following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="e13ca-201">`Invoke-ServiceFabricEncryptText` PowerShell 명령을 사용하여 암호 텍스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-201">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text.</span></span> <span data-ttu-id="e13ca-202">자세한 내용은 [Service Fabric 응용 프로그램의 비밀 관리](service-fabric-application-secret-management.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e13ca-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="e13ca-203">암호 해독을 위한 인증서의 개인 키는 대역 외 메서드를 사용하여(Azure에서는 Azure Resource Manager를 통해) 로컬 컴퓨터에 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-203">You must deploy the private key of the certificate to decrypt the password to the local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="e13ca-204">그런 다음 Service Fabric이 컴퓨터에 서비스 패키지를 배포할 때 사용자 이름과 함께 암호를 해독하고 이 자격 증명으로 실행하도록 Active Directory로 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-204">Then, when Service Fabric deploys the service package to the machine, it is able to decrypt the secret and (along with the user name) authenticate with Active Directory to run under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="e13ca-205">그룹 관리 서비스 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="e13ca-206">독립 실행형 설치 관리자를 사용하여 Windows Server에 설치된 Service Fabric 인스턴스의 경우 그룹 관리 서비스 계정(gMSA)으로 서비스를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-206">For an instance of Service Fabric that was installed on Windows Server by using the standalone installer, you can run the service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="e13ca-207">도메인 내의 Active Directory 온-프레미스이며 Azure Active Directory(Azure AD)를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e13ca-208">gMSA를 사용하면 `Application Manifest`에 저장된 암호 또는 암호화된 암호가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-208">By using a gMSA there is no password or encrypted password stored in the `Application Manifest`.</span></span>

<span data-ttu-id="e13ca-209">다음 예에서는 *svc-Test$*라는 gMSA 계정을 작성하는 방법, 해당 관리 서비스 계정을 클러스터 노드에 배포하는 방법 및 사용자 주체를 구성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-209">The following example shows how to create a gMSA account called *svc-Test$*; how to deploy that managed service account to the cluster nodes; and how to configure the user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="e13ca-210">필수 조건.</span><span class="sxs-lookup"><span data-stu-id="e13ca-210">Prerequisites.</span></span>
- <span data-ttu-id="e13ca-211">도메인에 KDS 루트 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-211">The domain needs a KDS root key.</span></span>
- <span data-ttu-id="e13ca-212">Windows Server 2012 이상 기능 수준에 도메인이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-212">The domain needs to be at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="e13ca-213">예제</span><span class="sxs-lookup"><span data-stu-id="e13ca-213">Example</span></span>
1. <span data-ttu-id="e13ca-214">Active Directory 도메인 관리자가 `New-ADServiceAccount` commandlet을 사용하여 그룹 관리 서비스 계정을 만들고 `PrincipalsAllowedToRetrieveManagedPassword`에 Serivce Fabric 클러스터 노드가 모두 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-214">Have an active directory domain administrator create a group managed service account using the `New-ADServiceAccount` commandlet and ensure that the `PrincipalsAllowedToRetrieveManagedPassword` includes all of the service fabric cluster nodes.</span></span> <span data-ttu-id="e13ca-215">`AccountName`, `DnsHostName` 및 `ServicePrincipalName`이 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="e13ca-216">각 Service Fabric 클러스터 노드(예: `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`)에서 gMSA를 설치하고 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-216">On each of the service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test the gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="e13ca-217">사용자 보안 주체를 구성하고 사용자를 참조하도록 RunAsPolicy를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-217">Configure the User principal, and configure the RunAsPolicy to reference the user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="e13ca-218">HTTP 및 HTTPS 끝점에 보안 액세스 정책 할당</span><span class="sxs-lookup"><span data-stu-id="e13ca-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="e13ca-219">서비스에 RunAs 정책을 적용하고 서비스 매니페스트에서 HTTP 프로토콜을 사용하여 끝점 리소스를 선언할 경우 이러한 끝점에 할당된 포트가 서비스가 실행되는 RunAs 사용자 계정에 대해 올바르게 액세스 제어 나열되도록 **SecurityAccessPolicy**를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-219">If you apply a RunAs policy to a service and the service manifest declares endpoint resources with the HTTP protocol, you must specify a **SecurityAccessPolicy** to ensure that ports allocated to these endpoints are correctly access-control listed for the RunAs user account that the service runs under.</span></span> <span data-ttu-id="e13ca-220">그러지 않으면 **http.sys** 가 해당 서비스에 액세스할 수 없고 클라이언트의 호출과 함께 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-220">Otherwise, **http.sys** does not have access to the service, and you get failures with calls from the client.</span></span> <span data-ttu-id="e13ca-221">다음은 **EndpointName**이라는 끝점에 Customer1 계정을 적용하여 전체 액세스 권한을 부여하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-221">The following example applies the Customer1 account to an endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="e13ca-222">또한 HTTPS 끝점의 경우 클라이언트에 반환할 인증서의 이름을 나타내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-222">For the HTTPS endpoint, you also have to indicate the name of the certificate to return to the client.</span></span> <span data-ttu-id="e13ca-223">응용 프로그램 매니페스트에서 인증서 섹션에 정의된 인증서를 통해 **EndpointBindingPolicy**를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-223">You can do this by using **EndpointBindingPolicy**, with the certificate defined in a certificates section in the application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and the Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if the EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="e13ca-224">https 끝점으로 여러 응용 프로그램 업그레이드</span><span class="sxs-lookup"><span data-stu-id="e13ca-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="e13ca-225">http**s**를 사용할 때는 동일한 응용 프로그램의 서로 다른 인스턴스에 대해 **동일한 포트**를 사용하지 않도록 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-225">You need to be careful not to use the **same port** for different instances of the same application when using http**s**.</span></span> <span data-ttu-id="e13ca-226">Service Fabric에서 응용 프로그램 인스턴스 중 하나에 대해 인증서를 업그레이드할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-226">The reason is that Service Fabric won't be able to upgrade the cert for one of the application instances.</span></span> <span data-ttu-id="e13ca-227">예를 들어, 응용 프로그램 1 또는 응용 프로그램 2 모두 해당 인증서 1을 인증서 2로 업그레이드하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-227">For example, if application 1 or application 2 both want to upgrade their cert 1 to cert 2.</span></span> <span data-ttu-id="e13ca-228">업그레이드가 발생할 때 Service Fabric은 다른 응용 프로그램에서 아직 사용 중이라고 하더라도 http.sys에서 인증서 1 등록을 정리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-228">When the upgrade happens, Service Fabric might have cleaned up the cert 1 registration with http.sys even though the other application is still using it.</span></span> <span data-ttu-id="e13ca-229">이러한 상황을 방지하기 위해 Service Fabric은 인증서와 함께 해당 포트에 등록된(http.sys에 따라) 다른 응용 프로그램 인스턴스가 이미 있는지 검색하고 있는 경우 작업이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-229">To prevent this, Service Fabric detects that there is already another application instance registered on the port with the certificate (due to http.sys) and fails the operation.</span></span>

<span data-ttu-id="e13ca-230">따라서 Service Fabric은 서로 다른 응용 프로그램 인스턴스에 **동일한 포트**를 사용하는 두 가지 다른 서비스의 업그레이드를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-230">Hence Service Fabric does not support upgrading two different services using **the same port** in different application instances.</span></span> <span data-ttu-id="e13ca-231">즉, 동일한 포트에서 서로 다른 서비스에 동일한 인증서를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-231">In other words, you cannot use the same certificate on different services on the same port.</span></span> <span data-ttu-id="e13ca-232">동일한 포트에서 공유 인증서를 포함해야 하는 경우 배치 제약 조건에 따라 서비스가 서로 다른 컴퓨터에 배치되는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-232">If you need to have a shared certificate on the same port, you need to ensure that the services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="e13ca-233">또는 각 응용 프로그램 인스턴스에서 각 서비스에 대해 Service Fabric 동적 포트를 사용하는 것이 좋습니다(가능한 경우).</span><span class="sxs-lookup"><span data-stu-id="e13ca-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="e13ca-234">https로 업그레이드 실패가 표시되면 “The Windows HTTP Server API does not support multiple certificates for applications that share a port(Windows HTTP 서버 API에서 포트를 공유하는 응용 프로그램에 대해 여러 인증서를 지원하지 않습니다).”라는 오류 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-234">If you see an upgrade fail with https, an error warning saying "The Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="e13ca-235">완전한 응용 프로그램 매니페스트의 예</span><span class="sxs-lookup"><span data-stu-id="e13ca-235">A complete application manifest example</span></span>
<span data-ttu-id="e13ca-236">다음 응용 프로그램 매니페스트는 여러 설정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e13ca-236">The following application manifest shows many of the different settings:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="e13ca-237">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e13ca-237">Next steps</span></span>
* [<span data-ttu-id="e13ca-238">응용 프로그램 모델의 이해</span><span class="sxs-lookup"><span data-stu-id="e13ca-238">Understand the application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="e13ca-239">서비스 매니페스트에서 리소스 지정</span><span class="sxs-lookup"><span data-stu-id="e13ca-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="e13ca-240">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e13ca-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
