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
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>지속적인 업데이트 toopublish tooAzure를 사용 하는 경우 원격 디버깅을 사용 하도록 설정
Azure에서 원격 디버깅, 클라우드 서비스 또는 가상 컴퓨터에 대 한 사용 하는 경우 사용 하도록 설정할 수 있습니다 [지속적인 업데이트](cloud-services-dotnet-continuous-delivery.md) 다음이 단계를 수행 하 여 toopublish tooAzure 합니다.

## <a name="enabling-remote-debugging-for-cloud-services"></a>클라우드 서비스에 원격 디버깅 사용
1. Hello 빌드 에이전트에서 hello 초기 환경을 설정 되는 azure에 설명 된 대로 [Azure에 대 한 명령줄 빌드](http://msdn.microsoft.com/library/hh535755.aspx)합니다.
2. Hello 원격 디버그 런타임 (msvsmon.exe) hello 패키지에 대 한 필요 하므로 설치 hello **Visual Studio 용 원격 도구**합니다.

    * [Visual Studio 2017용 원격 도구](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Visual Studio 2015용 원격 도구](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Visual Studio 2013용 원격 도구 업데이트 5](https://www.microsoft.com/download/details.aspx?id=48156)
    
    대신, Visual Studio가 설치 되어 있는 시스템에서 hello 원격 디버그 바이너리를 복사할 수 있습니다.

3. [Azure 클라우드 서비스에 대한 인증서 개요](cloud-services-certs-create.md)에서 간략히 설명된 인증서를 만듭니다. Hello.pfx 및 인증서 지문을 RDP 유지 하 고 hello 인증서 toohello 대상 클라우드 서비스에 업로드 합니다.
4. Hello 원격 디버그를 사용 하도록 설정 된 다음 hello MSBuild 명령줄 toobuild 및 패키지의 옵션을 사용 합니다. (Hello 각도 대괄호로 묶지 항목에 대 한 실제 경로 tooyour 시스템 및 프로젝트 파일을 대체 합니다.)
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`hello 경로 toohello 폴더 for Visual Studio 원격 도구 hello에서에서 msvsmon.exe를 포함입니다.
    `RemoteDebuggerConnectorVersion`클라우드 서비스에서 hello Azure SDK 버전이입니다. 또한 Visual Studio와 함께 설치 하는 hello 버전와 일치 해야 합니다.
5. Hello 이전 단계에서 생성 된 hello 패키지 및.cscfg 파일을 사용 하 여 toohello 대상 클라우드 서비스를 게시 합니다.
6. 설치 된.NET 용 Azure SDK와 Visual Studio가 있는 hello 인증서 (.pfx 파일) toohello 컴퓨터를 가져옵니다. 있는지 tooimport toohello 확인 `CurrentUser\My` 인증서 저장소, 그렇지 않으면 Visual Studio에서 toohello 디버거를 연결 하지 못합니다.

## <a name="enabling-remote-debugging-for-virtual-machines"></a>가상 컴퓨터에 원격 디버깅 사용
1. Azure 가상 컴퓨터를 만듭니다. [Windows Server를 실행하는 가상 컴퓨터 만들기](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Visual Studio에서 Azure Virtual Machine 만들기 및 관리](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)를 참조하세요.
2. Hello에 [Azure 클래식 포털 페이지](http://go.microsoft.com/fwlink/p/?LinkID=269851), hello 가상 컴퓨터의 대시보드 toosee hello 가상 컴퓨터의 보기 **RDP 인증서 지문을**합니다. 이 값은 hello에 대 한 사용 `ServerThumbprint` hello 확장 구성의 값입니다.
3. 에 설명 된 대로 클라이언트 인증서를 만들어 [Azure 클라우드 서비스에 대 한 인증서 개요](cloud-services-certs-create.md) (hello.pfx 및 RDP 인증서 지문을 유지).
4. Azure Powershell을 설치 (버전 0.7.4 이상)에 설명 된 대로 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
5. 다음 스크립트 tooenable hello RemoteDebug 확장 hello를 실행 합니다. 사용자의 구독 이름, 서비스 이름 및 지문 같은 hello 경로 및 개인 데이터를 대체 합니다.
   
   > [!NOTE]
   > 이 스크립트는 Visual Studio 2015에서 구성되었습니다. Visual Studio 2013 또는 Visual Studio 2017을 사용 하는 경우 수정 hello `$referenceName` 및 `$extensionName` 할당 아래 너무`RemoteDebugVS2013` 또는 `RemoteDebugVS2017`합니다.

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

6. 설치 된.NET 용 Azure SDK와 Visual Studio가 있는 hello 인증서 (.pfx) toohello 컴퓨터를 가져옵니다.

