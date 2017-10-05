---
title: "연속 배달을 통해 원격 디버깅 사용 | Microsoft Docs"
description: "연속 배달을 사용하여 Azure에 배포할 경우 원격 디버깅을 사용하도록 설정하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 7a8a853a93e3e9915f687a20c871444e6a0de50d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-to-publish-to-azure"></a><span data-ttu-id="52539-103">연속 배달을 사용하여 Azure에 게시할 경우 원격 디버깅 사용</span><span class="sxs-lookup"><span data-stu-id="52539-103">Enable remote debugging when using continuous delivery to publish to Azure</span></span>
<span data-ttu-id="52539-104">클라우드 서비스 또는 가상 컴퓨터의 경우 다음 단계를 따라 [연속 배달](cloud-services-dotnet-continuous-delivery.md) 을 사용하여 Azure에 게시하면 Azure에서 원격 디버깅을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52539-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) to publish to Azure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="52539-105">클라우드 서비스에 원격 디버깅 사용</span><span class="sxs-lookup"><span data-stu-id="52539-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="52539-106">빌드 에이전트에서 [Azure에 대한 명령줄 빌드](http://msdn.microsoft.com/library/hh535755.aspx)에 간략히 설명된 Azure에 대한 초기 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-106">On the build agent, set up the initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="52539-107">패키지에 원격 디버그 런타임(msvsmon.exe)이 필요하므로, **Visual Studio용 원격 도구**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-107">Because the remote debug runtime (msvsmon.exe) is required for the package, install the **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="52539-108">Visual Studio 2017용 원격 도구</span><span class="sxs-lookup"><span data-stu-id="52539-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="52539-109">Visual Studio 2015용 원격 도구</span><span class="sxs-lookup"><span data-stu-id="52539-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="52539-110">Visual Studio 2013용 원격 도구 업데이트 5</span><span class="sxs-lookup"><span data-stu-id="52539-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="52539-111">또는 Visual Studio를 설치한 시스템에서 원격 디버그 이진을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52539-111">As an alternative, you can copy the remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="52539-112">[Azure 클라우드 서비스에 대한 인증서 개요](cloud-services-certs-create.md)에서 간략히 설명된 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52539-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="52539-113">.pfx 및 RDP 인증서 지문을 유지하고 대상 클라우드 서비스에 인증서를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-113">Keep the .pfx and RDP certificate thumbprint and upload the certificate to the target cloud service.</span></span>
4. <span data-ttu-id="52539-114">MSBuild 명령줄에 다음 옵션을 사용하여 원격 디버그를 사용하도록 설정한 상태로 빌드 및 패키지화합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-114">Use the following options in the MSBuild command line to build and package with remote debug enabled.</span></span> <span data-ttu-id="52539-115">(꺾쇠 괄호가 항목의 경우 시스템 및 프로젝트 파일에 대한 실제 경로를 대체합니다.)</span><span class="sxs-lookup"><span data-stu-id="52539-115">(Substitute actual paths to your system and project files for the angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of the certificate added to the cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path to your VS solution file>"
   
    <span data-ttu-id="52539-116">`VSX64RemoteDebuggerPath` Visual Studio용 원격 도구에서 msvsmon.exe를 포함하는 폴더의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="52539-116">`VSX64RemoteDebuggerPath` is the path to the folder containing msvsmon.exe in the Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="52539-117">`RemoteDebuggerConnectorVersion`은 클라우드 서비스의 Azure SDK 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="52539-117">`RemoteDebuggerConnectorVersion` is the Azure SDK version in your cloud service.</span></span> <span data-ttu-id="52539-118">또한 Visual Studio와 함께 설치된 버전과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-118">It should also match the version installed with Visual Studio.</span></span>
5. <span data-ttu-id="52539-119">위의 단계에서 생성한 패키지 및 .cscfg 파일을 사용하여 대상 클라우드 서비스에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-119">Publish to the target cloud service by using the package and .cscfg file generated in the previous step.</span></span>
6. <span data-ttu-id="52539-120">Visual Studio 및 Azure SDK for .NET이 설치된 컴퓨터로 인증서(.pfx 파일)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="52539-120">Import the certificate (.pfx file) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="52539-121">`CurrentUser\My` 인증서 저장소로 로 가져와야 합니다. 그렇지 않은 경우 Visual Studio의 디버거에 연결는 데 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-121">Make sure to import to the `CurrentUser\My` certificate store, otherwise attaching to the debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="52539-122">가상 컴퓨터에 원격 디버깅 사용</span><span class="sxs-lookup"><span data-stu-id="52539-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="52539-123">Azure 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="52539-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="52539-124">[Windows Server를 실행하는 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Visual Studio에서 Azure Virtual Machine 만들기 및 관리](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="52539-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="52539-125">[Azure 클래식 포털 페이지](http://go.microsoft.com/fwlink/p/?LinkID=269851)에서, 가상 컴퓨터 대시보드를 보고 가상 컴퓨터의 **RDP 인증서 지문**을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-125">On the [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view the virtual machine's dashboard to see the virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="52539-126">이 값은 확장 구성에서 `ServerThumbprint` 값에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="52539-126">This value is used for the `ServerThumbprint` value in the extension configuration.</span></span>
3. <span data-ttu-id="52539-127">[Azure 클라우드 서비스에 대한 인증서 개요](cloud-services-certs-create.md) 에서 간략히 설명한 대로 클라이언트 인증서를 만듭니다(.pfx 및 RDP 인증서 지문 유지).</span><span class="sxs-lookup"><span data-stu-id="52539-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep the .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="52539-128">Azure PowerShell(0.7.4 이후 버전)을 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)에 간략히 설명한 대로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="52539-129">다음 스크립트를 실행하여 RemoteDebug 확장을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-129">Run the following script to enable the RemoteDebug extension.</span></span> <span data-ttu-id="52539-130">경로 및 개인 데이터를 사용자의 데이터(예: 구독 이름, 서비스 이름 및 지문)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="52539-130">Replace the paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="52539-131">이 스크립트는 Visual Studio 2015에서 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="52539-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="52539-132">Visual Studio 2013 또는 Visual Studio 2017을 사용할 경우 아래 `$referenceName` 및 `$extensionName` 할당을 `RemoteDebugVS2013` 또는 `RemoteDebugVS2017`으로 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="52539-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify the `$referenceName` and `$extensionName` assignments below to `RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="52539-133">Visual Studio 및 Azure SDK for .NET 2.4가 설치된 컴퓨터로 인증서(.pfx)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="52539-133">Import the certificate (.pfx) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

