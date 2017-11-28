---
title: "지속적인 업데이트 된 원격 디버깅 aaaEnable | Microsoft Docs"
description: "자세한 내용은 방법 toodeploy tooAzure 지속적인 업데이트를 사용 하 여 tooenable 원격 디버깅"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="abf9b-103">지속적인 업데이트 toopublish tooAzure를 사용 하는 경우 원격 디버깅을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="abf9b-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="abf9b-104">Azure에서 원격 디버깅, 클라우드 서비스 또는 가상 컴퓨터에 대 한 사용 하는 경우 사용 하도록 설정할 수 있습니다 [지속적인 업데이트](cloud-services-dotnet-continuous-delivery.md) 다음이 단계를 수행 하 여 toopublish tooAzure 합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="abf9b-105">클라우드 서비스에 원격 디버깅 사용</span><span class="sxs-lookup"><span data-stu-id="abf9b-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="abf9b-106">Hello 빌드 에이전트에서 hello 초기 환경을 설정 되는 azure에 설명 된 대로 [Azure에 대 한 명령줄 빌드](http://msdn.microsoft.com/library/hh535755.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="abf9b-107">Hello 원격 디버그 런타임 (msvsmon.exe) hello 패키지에 대 한 필요 하므로 설치 hello **Visual Studio 용 원격 도구**합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="abf9b-108">Visual Studio 2017용 원격 도구</span><span class="sxs-lookup"><span data-stu-id="abf9b-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="abf9b-109">Visual Studio 2015용 원격 도구</span><span class="sxs-lookup"><span data-stu-id="abf9b-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="abf9b-110">Visual Studio 2013용 원격 도구 업데이트 5</span><span class="sxs-lookup"><span data-stu-id="abf9b-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="abf9b-111">대신, Visual Studio가 설치 되어 있는 시스템에서 hello 원격 디버그 바이너리를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="abf9b-112">[Azure 클라우드 서비스에 대한 인증서 개요](cloud-services-certs-create.md)에서 간략히 설명된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="abf9b-113">Hello.pfx 및 인증서 지문을 RDP 유지 하 고 hello 인증서 toohello 대상 클라우드 서비스에 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="abf9b-114">Hello 원격 디버그를 사용 하도록 설정 된 다음 hello MSBuild 명령줄 toobuild 및 패키지의 옵션을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="abf9b-115">(Hello 각도 대괄호로 묶지 항목에 대 한 실제 경로 tooyour 시스템 및 프로젝트 파일을 대체 합니다.)</span><span class="sxs-lookup"><span data-stu-id="abf9b-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="abf9b-116">`VSX64RemoteDebuggerPath`hello 경로 toohello 폴더 for Visual Studio 원격 도구 hello에서에서 msvsmon.exe를 포함입니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="abf9b-117">`RemoteDebuggerConnectorVersion`클라우드 서비스에서 hello Azure SDK 버전이입니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="abf9b-118">또한 Visual Studio와 함께 설치 하는 hello 버전와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="abf9b-119">Hello 이전 단계에서 생성 된 hello 패키지 및.cscfg 파일을 사용 하 여 toohello 대상 클라우드 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="abf9b-120">설치 된.NET 용 Azure SDK와 Visual Studio가 있는 hello 인증서 (.pfx 파일) toohello 컴퓨터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="abf9b-121">있는지 tooimport toohello 확인 `CurrentUser\My` 인증서 저장소, 그렇지 않으면 Visual Studio에서 toohello 디버거를 연결 하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="abf9b-122">가상 컴퓨터에 원격 디버깅 사용</span><span class="sxs-lookup"><span data-stu-id="abf9b-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="abf9b-123">Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="abf9b-124">[Windows Server를 실행하는 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Visual Studio에서 Azure Virtual Machine 만들기 및 관리](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="abf9b-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="abf9b-125">Hello에 [Azure 클래식 포털 페이지](http://go.microsoft.com/fwlink/p/?LinkID=269851), hello 가상 컴퓨터의 대시보드 toosee hello 가상 컴퓨터의 보기 **RDP 인증서 지문을**합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="abf9b-126">이 값은 hello에 대 한 사용 `ServerThumbprint` hello 확장 구성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="abf9b-127">에 설명 된 대로 클라이언트 인증서를 만들어 [Azure 클라우드 서비스에 대 한 인증서 개요](cloud-services-certs-create.md) (hello.pfx 및 RDP 인증서 지문을 유지).</span><span class="sxs-lookup"><span data-stu-id="abf9b-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="abf9b-128">Azure Powershell을 설치 (버전 0.7.4 이상)에 설명 된 대로 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="abf9b-129">다음 스크립트 tooenable hello RemoteDebug 확장 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="abf9b-130">사용자의 구독 이름, 서비스 이름 및 지문 같은 hello 경로 및 개인 데이터를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="abf9b-131">이 스크립트는 Visual Studio 2015에서 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="abf9b-132">Visual Studio 2013 또는 Visual Studio 2017을 사용 하는 경우 수정 hello `$referenceName` 및 `$extensionName` 할당 아래 너무`RemoteDebugVS2013` 또는 `RemoteDebugVS2017`합니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="abf9b-133">설치 된.NET 용 Azure SDK와 Visual Studio가 있는 hello 인증서 (.pfx) toohello 컴퓨터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="abf9b-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

