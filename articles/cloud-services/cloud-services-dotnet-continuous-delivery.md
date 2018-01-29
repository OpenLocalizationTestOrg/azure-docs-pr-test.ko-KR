---
title: "Azure의 TFS를 사용한 Cloud Services의 지속적인 전송 | Microsoft Docs"
description: "Azure 클라우드 앱에 대해 지속적인 전송을 설정하는 방법에 대해 알아봅니다. MSBuild 명령줄 문 및 PowerShell 스크립트에 대한 코드 샘플도 제공됩니다."
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: 470fda7722e6a22e50ed66a7bc193fc7c9f71536
ms.sourcegitcommit: cc03e42cffdec775515f489fa8e02edd35fd83dc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/07/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Azure Cloud Services의 지속적인 전송
이 문서에서 설명하는 프로세스에서는 Azure 클라우드 앱에 대해 지속적인 전송을 설정하는 방법을 보여 줍니다. 이 프로세스를 통해 각 코드 체크 인 이후에 자동으로 패키지를 만들어 Azure에 배포할 수 있습니다. 이 문서에서 설명하는 패키지 빌드 프로세스는 Visual Studio의 **패키지** 명령과 동일하며 게시 단계는 Visual Studio의 **게시** 명령과 동일합니다.
이 문서에서는 MSBuild 명령줄 문과 Windows PowerShell 스크립트를 사용하여 빌드 서버를 만드는 데 사용하는 메서드에 대해 설명하고, MSBuild 명령 및 PowerShell 스크립트를 사용하도록 선택적으로 Visual Studio Team Foundation Server - 팀 빌드 정의를 구성하는 방법도 보여 줍니다. 이 프로세스는 빌드 환경 및 Azure 대상 환경에 맞게 사용자 지정할 수 있습니다.

또한 Azure에서 호스트되는 TFS 버전인 Visual Studio Team Services를 사용하면 이 작업을 보다 쉽게 수행할 수 있습니다. 

시작하기 전에 Visual Studio에서 응용 프로그램을 게시해야 합니다.
그러면 게시 프로세스를 자동화하려고 할 때 모든 리소스가 사용 가능하며 초기화됩니다.

## <a name="1-configure-the-build-server"></a>1: 빌드 서버 구성
MSBuild를 사용하여 Azure 패키지를 만들려면 먼저 필요한 소프트웨어 및 도구를 빌드 서버에 설치해야 합니다.

Visual Studio는 빌드 서버에 설치할 필요가 없습니다. Team Foundation Build 서비스를 사용하여 빌드 서버를 관리하려면 [Team Foundation Build Service][Team Foundation Build Service](영문) 설명서의 지침을 따르세요.

1. 빌드 서버에 MSBuild가 포함된 [.NET Framework 4.5.2][.NET Framework 4.5.2]를 설치합니다.
2. 최신 [.NET용 Azure 작성 도구](https://azure.microsoft.com/develop/net/)를 설치합니다.
3. [.NET용 Azure 라이브러리](http://go.microsoft.com/fwlink/?LinkId=623519)를 설치합니다.
4. Visual Studio 설치에서 Microsoft.WebApplication.targets 파일을 빌드 서버에 복사합니다.

   Visual Studio가 설치된 컴퓨터에서 이 파일은 디렉터리 C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications에 있습니다. 빌드 서버의 동일한 디렉터리에 해당 파일을 복사해야 합니다.
5. [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)를 설치합니다.

## <a name="2-build-a-package-using-msbuild-commands"></a>2: MSBuild 명령을 사용하여 패키지 빌드
이 섹션에서는 Azure 패키지를 빌드하는 MSBuild 명령 구성 방법에 대해 설명합니다. 빌드 서버에서 이 단계를 실행하여 모든 항목이 제대로 구성되어 있고 MSBuild 명령이 원하는 대로 수행되는지 확인합니다. 다음 섹션에 설명된 대로 이 명령줄을 빌드 서버의 기존 빌드 스크립트에 추가하거나 TFS 빌드 정의에서 명령줄을 사용할 수 있습니다. 명령줄 매개 변수 및 MSBuild에 대한 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)를 참조하세요.

1. Visual Studio가 빌드 서버에 설치되어 있는 경우 Windows의 **Visual Studio Tools** 폴더에서 **Visual Studio 명령 프롬프트**를 찾아서 클릭합니다.

   Visual Studio가 빌드 서버에 설치되어 있지 않으면 명령 프롬프트를 열고 해당 경로에서 MSBuild.exe에 액세스할 수 있는지 확인합니다. MSBuild는 .NET Framework와 함께 %WINDIR%\\Microsoft.NET\\Framework\\*Version* 경로에 설치됩니다. 예를 들어 .NET Framework 4를 설치한 경우 PATH 환경 변수에 MSBuild.exe를 추가하려면 명령 프롬프트에서 다음 명령을 입력하세요.

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. 명령 프롬프트에서 빌드할 Azure 프로젝트 파일이 포함된 폴더로 이동합니다.
3. 다음 예제와 /target:Publish 옵션을 사용하여 MSBuild를 실행합니다.

       MSBuild /target:Publish

   이 옵션은 /t:Publish로 간략하게 표시할 수 있습니다. MSBuild의 /t:Publish 옵션을 Azure SDK를 설치한 경우 Visual Studio에서 제공되는 게시 명령과 혼동해서는 안 됩니다. /t:Publish 옵션은 Azure 패키지를 빌드만 합니다. Visual Studio의 게시 명령처럼 패키지를 배포하지는 않습니다.

   선택적으로 프로젝트 이름을 MSBuild 매개 변수로 지정할 수 있습니다. 지정하지 않으면 현재 디렉터리가 사용됩니다. MSBuild 명령줄 옵션에 대한 자세한 내용은 [MSBuild 명령줄 참조](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx)를 참조하세요.
4. 출력을 찾습니다. 기본적으로 이 명령은 프로젝트의 루트 폴더를 기준으로 디렉터리를 만듭니다(예: *ProjectDir*\\bin\\*Configuration*\\app.publish\\). Azure 프로젝트를 빌드하면 패키지 파일 자체와 함께 제공되는 구성 파일의 두 파일이 생성됩니다.

   * Project.cspkg
   * ServiceConfiguration.*TargetProfile*.cscfg

   기본적으로 각 Azure 프로젝트에는 로컬(디버깅) 빌드용 서비스 구성 파일(.cscfg 파일) 하나와 클라우드(스테이징 또는 프로덕션) 빌드용 서비스 구성 파일 하나가 포함되지만 필요에 따라 서비스 구성 파일을 추가하거나 제거할 수 있습니다. Visual Studio 내에서 패키지를 빌드하면 패키지와 함께 포함할 서비스 구성 파일을 묻는 메시지가 표시됩니다.
5. 서비스 구성 파일을 지정합니다. MSBuild를 사용하여 패키지를 빌드하면 로컬 서비스 구성 파일이 기본적으로 포함됩니다. 다른 서비스 구성 파일을 포함하려면 다음 예제와 같이 MSBuild 명령의 TargetProfile 속성을 설정합니다.

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. 출력의 위치를 지정합니다. 다음 예제와 같이 뒤에 오는 백슬래시 구분 기호를 포함하는 /p:PublishDir=*Directory*\\ 옵션을 사용하여 경로를 설정합니다.

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   적절한 MSBuild 명령줄을 구성하고 테스트하여 프로젝트를 빌드하고 Azure 패키지로 결합했으면 이 명령줄을 빌드 스크립트에 추가할 수 있습니다. 빌드 서버에서 사용자 지정 스크립트를 사용하는 경우 이 프로세스는 사용자 지정 빌드 프로세스의 세부 사항에 따라 달라집니다. TFS를 빌드 환경으로 사용하는 경우 다음 단계의 지침에 따라 Azure 패키지 빌드를 빌드 프로세스에 추가할 수 있습니다.

## <a name="3-build-a-package-using-tfs-team-build"></a>3: TFS 팀 빌드를 사용하여 패키지 빌드
TFS(Team Foundation Server)를 빌드 컨트롤러로 설정하고 빌드 서버를 TFS 빌드 컴퓨터로 설정한 경우 Azure 패키지에 대해 자동화된 빌드를 선택적으로 설정할 수 있습니다. Team Foundation Server를 빌드 시스템으로 설정하고 사용하는 방법에 대한 자세한 내용은 [빌드 시스템 확장][Scale out your build system]을 참조하세요. 특히 다음 절차에서는 빌드 서버를 [빌드 서버 배포 및 구성][Deploy and configure a build server]에 설명된 대로 구성했고, 팀 프로젝트를 만들고 팀 프로젝트에 클라우드 서비스를 만들었다고 가정합니다.

Azure 패키지를 빌드하도록 TFS를 구성하려면 다음 단계를 수행하세요.

1. 개발 컴퓨터의 Visual Studio 보기 메뉴에서 **팀 Explorer**를 선택하거나 Ctrl+\\, Ctrl+M을 선택합니다. 팀 Explorer 창에서 **빌드** 노드를 확장하거나 **빌드** 페이지를 선택하고 **새 빌드 정의**를 선택합니다.

   ![새 빌드 정의 옵션][0]
2. **트리거** 탭을 선택하고 패키지를 빌드하려는 경우에 원하는 조건을 지정합니다. 예를 들어 소스 제어 체크 인이 발생할 때마다 패키지를 빌드하려면 **연속 통합**을 지정합니다.
3. **소스 설정** 탭을 선택하고 프로젝트 폴더가 **소스 제어 폴더** 열에 나열되고 상태가 **활성**인지 확인합니다.
4. **빌드 기본값** 탭을 선택하고 빌드 컨트롤러에서 빌드 서버의 이름을 확인합니다.  또한 **다음 저장 폴더에 빌드 출력 복사** 옵션을 선택하고 원하는 저장 위치를 지정합니다.
5. **프로세스** 탭을 선택합니다. 프로세스 탭에서 기본 템플릿을 선택하고 **빌드**에서 프로젝트를 선택한 다음(선택되지 않은 경우) 표의 **빌드** 섹션에서 **고급** 섹션을 확장합니다.
6. **MSBuild Arguments**를 선택하고 위의 2단계에서 설명한 대로 적절한 MSBuild 명령줄 인수를 설정합니다. 예를 들어 패키지를 빌드하고 패키지 파일을 \\\\myserver\\drops\\ 위치에 복사하려면 **/t:Publish /p:PublishDir=\\\\myserver\\drops\\**를 입력합니다.

   ![MSBuild Arguments][2]

   > [!NOTE]
   > 파일을 공용 공유 위치에 복사하면 개발 컴퓨터에서 패키지를 수동으로 배포하기가 더 쉽습니다.
7. 프로젝트의 변경 내용을 체크 인하여 빌드 단계의 성공 여부를 테스트하거나 새 빌드를 큐에 대기시킵니다. 새 빌드를 큐에 대기시키려면 팀 Explorer에서 **모든 빌드 정의**를 마우스 오른쪽 단추로 클릭한 다음 **새 빌드 큐 대기**를 선택합니다.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4: PowerShell 스크립트를 사용하여 패키지 게시
이 섹션에서는 선택적 매개 변수를 사용하여 클라우드 앱 패키지 출력을 Azure에 게시할 Windows PowerShell 스크립트를 구성하는 방법에 대해 설명합니다. 이 스크립트는 사용자 지정 빌드 자동화의 빌드 단계 후에 호출할 수 있으며, Visual Studio TFS 팀 빌드의 프로세스 템플릿 워크플로 작업에서 호출할 수도 있습니다.

1. [Azure PowerShell cmdlet][Azure PowerShell cmdlets](v0.6.1 이상)을 설치합니다.
   cmdlet 설치 단계 중 스냅인으로 설치하도록 선택합니다. 이전 버전의 번호는 2.x.x로 지정되었지만 공식적으로 지원되는 이 버전이 CodePlex를 통해 제공된 이전 버전을 대체합니다.
2. 시작 메뉴나 시작 페이지를 사용하여 Azure PowerShell을 시작합니다. 이런 방식으로 시작하면 Azure PowerShell cmdlet이 로드됩니다.
3. PowerShell 프롬프트에서 부분 명령 `Get-Azure`를 입력한 다음 문 완성에 대한 Tab 키를 눌러 PowerShell cmdlet가 로드되는지 확인합니다.

   Tab 키를 반복해서 누르면 다양한 Azure PowerShell 명령이 표시됩니다.
4. .publishsettings 파일에서 구독 정보를 가져와 Azure 구독에 연결할 수 있는지 확인합니다.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   다음 명령을 입력합니다.

   `Get-AzureSubscription`

   그러면 구독에 대한 정보가 표시됩니다. 모든 정보가 올바른지 확인합니다.
5. 이 문서의 끝에 제공된 스크립트 템플릿을 c:\\scripts\\WindowsAzure\\**PublishCloudService.ps1**로 스크립트 폴더에 저장합니다.
6. 스크립트의 매개 변수 섹션을 검토합니다. 기본값을 추가하거나 수정합니다. 이러한 값은 명시적 매개 변수를 전달하여 언제든지 재정의할 수 있습니다.
7. 게시 스크립트에서 대상으로 지정할 수 있는 유효한 클라우드 서비스 및 저장소 계정이 구독에 만들어져 있는지 확인합니다. 저장소 계정(Blob Storage)은 배포를 만드는 동안 배포 패키지 및 구성 파일을 업로드하고 일시적으로 저장하는 데 사용됩니다.

   * 새 클라우드 서비스를 만들려면 다음 스크립트를 호출하거나 [Azure Portal](https://portal.azure.com)을 사용할 수 있습니다. 클라우드 서비스 이름은 정규화된 도메인 이름의 접두사로 사용되므로 고유해야 합니다.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * 새 저장소 계정을 만들려면 다음 스크립트를 호출하거나 [Azure Portal](https://portal.azure.com)을 사용할 수 있습니다. 저장소 계정 이름은 정규화된 도메인 이름의 접두사로 사용되므로 고유해야 합니다. 클라우드 서비스와 같은 이름을 사용할 수 있습니다.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Azure PowerShell에서 직접 스크립트를 호출하거나 패키지 빌드 후 수행되도록 호스트 빌드 자동화에 이 스크립트를 연결합니다.

   > [!IMPORTANT]
   > 스크립트는 기존 배포가 검색될 경우 기본적으로 항상 삭제하거나 대체합니다. 사용자에게 확인할 수 없는 경우 자동화에서 지속적인 전송을 사용하도록 설정해야 합니다.
   >
   >

   **예제 시나리오 1:** 서비스의 스테이징 환경에 지속적인 배포:

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   그런 다음 일반적으로 테스트 실행 검증 및 VIP 교환이 수행됩니다. VIP 교환은 [Azure Portal](https://portal.azure.com)이나 Move-Deployment cmdlet을 사용하여 수행할 수 있습니다.

   **예제 시나리오 2:** 전용 테스트 서비스의 프로덕션 환경에 지속적인 배포

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **원격 데스크톱:**

   Azure 프로젝트에서 원격 데스크톱을 사용하는 경우 일회성 단계를 추가로 수행하여 이 스크립트의 대상이 되는 모든 Cloud Services에 올바른 클라우드 서비스 인증서가 업로드되었는지 확인해야 합니다.

   역할에 필요한 인증서 지문 값을 찾습니다. 지문 값은 클라우드 config 파일(예: ServiceConfiguration.Cloud.cscfg)의 Certificates 섹션에 표시됩니다. 옵션 표시를 선택하고 선택한 인증서를 보면 Visual Studio의 원격 데스크톱 구성 대화 상자에도 표시됩니다.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   다음 cmdlet 스크립트를 사용하여 원격 데스크톱 인증서를 일회성 설치 단계로 업로드합니다.

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   예:

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   또는 개인 키로 인증서 파일 PFX를 내보내고 [Azure Portal](https://portal.azure.com)을 사용하여 각 대상 클라우드 서비스에 인증서를 업로드할 수 있습니다.

   <!---
   Fixing broken links for Azure content migration from ACOM to DOCS. I'm unable to find a replacement links, so I'm commenting out this reference for now. The author can investigate in the future. "Read the following article to learn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **배포 업그레이드 및 배포 삭제 -\> 새 배포**

   매개 변수가 전달되지 않거나 값 1이 명시적으로 전달되는 경우 스크립트는 기본적으로 배포 업그레이드($enableDeploymentUpgrade = 1)를 수행합니다. 단일 인스턴스인 경우 전체 배포보다 시간이 적게 걸린다는 장점이 있습니다. 고가용성이 필요한 인스턴스의 경우 일부 인스턴스가 업그레이드(업데이트 도메인 이동)되는 동안 다른 인스턴스가 계속 실행되며 VIP가 삭제되지 않는다는 장점도 있습니다.

   배포 업그레이드는 스크립트에서($enableDeploymentUpgrade = 0) 또는 *-enableDeploymentUpgrade 0* 을 매개 변수로 전달하여 사용하지 않도록 설정함으로써 기존 배포를 먼저 삭제한 다음 새 배포를 만들도록 스크립트 동작을 변경할 수 있습니다.

   > [!IMPORTANT]
   > 스크립트는 기존 배포가 검색될 경우 기본적으로 항상 삭제하거나 대체합니다. 사용자에게 확인할 수 없는 경우 자동화에서 지속적인 전송을 사용하도록 설정해야 합니다.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5: TFS 팀 빌드를 사용하여 패키지 게시
이 선택적 단계에서는 TFS 팀 빌드를 4단계에서 만든 스크립트에 연결하여 Azure에 패키지 빌드 게시를 처리합니다. 그런 다음 빌드 정의에서 사용하는 프로세스 템플릿을 수정하여 워크플로가 끝날 때 게시 작업이 실행되도록 합니다. 게시 작업에서는 빌드에서 매개 변수를 전달하는 PowerShell 명령을 실행합니다. MSBuild 대상 및 게시 스크립트의 출력은 표준 빌드 출력에 연결됩니다.

1. 지속적인 배포를 담당하는 빌드 정의를 편집합니다.
2. **프로세스** 탭을 선택합니다.
3. [다음 지침](http://msdn.microsoft.com/library/dd647551.aspx)에 따라 빌드 프로세스 템플릿에 대한 작업 프로젝트를 추가하고, 기본 템플릿을 다운로드하여 프로젝트에 추가하고, 체크 인합니다. 빌드 프로세스 템플릿에 새 이름을 지정합니다(예: AzureBuildProcessTemplate).
4. **프로세스** 탭으로 돌아가서 **자세한 정보 표시**를 사용하여 사용 가능한 빌드 프로세스 템플릿 목록을 표시합니다. **새로 만들기...** 단추를 선택하고 방금 추가하고 체크 인한 프로젝트로 이동합니다. 방금 만든 템플릿을 찾은 다음 **확인**을 선택합니다.
5. 선택한 프로세스 템플릿을 열어 편집합니다. Workflow Designer에서 직접 열거나 XML 편집기에서 열어 XAML로 작업합니다.
6. 다음 새 인수 목록을 별도의 라인 항목으로 Workflow Designer의 인수 탭에 추가합니다. 모든 인수는 direction=In 및 type=String이어야 합니다. 이러한 값은 빌드 정의에서 워크플로로 매개 변수가 흐르는 데 사용된 다음 게시 스크립트를 호출하는 데 사용됩니다.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![인수 목록][3]

   해당 XAML은 다음과 같이 표시됩니다.

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. 에이전트에서 실행이 끝나면 새 시퀀스를 추가합니다.

   1. 유효한 스크립트 파일을 확인하는 If 문 작업을 추가하여 시작합니다. 조건을 다음 값으로 설정합니다.

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. If 문의 Then 케이스에서 새 시퀀스 작업을 추가합니다. 표시 이름을 'Start publish'로 설정합니다.
   3. Start publish 시퀀스를 선택한 상태에서 다음 새 변수 목록을 별도의 라인 항목으로 Workflow Designer의 변수 탭에 추가합니다. 모든 변수의 변수 유형은 문자열이고 범위는 Start publish여야 합니다. 이러한 값은 빌드 정의에서 워크플로로 매개 변수가 흐르는 데 사용된 다음 게시 스크립트를 호출하는 데 사용됩니다.

      * SubscriptionDataFilePath, 문자열 유형
      * PublishScriptFilePath, 문자열 유형

        ![새 변수][4]
   4. TFS 2012 이하를 사용하고 있으면 새 시퀀스의 시작 부분에 ConvertWorkspaceItem 작업을 추가합니다. TFS 2013 이상을 사용하고 있으면 새 시퀀스의 시작 부분에 GetLocalPath 작업을 추가합니다. ConvertWorkspaceItem의 경우 다음과 같이 속성을 설정합니다. Direction=ServerToLocal, DisplayName='Convert publish script filename', Input=' PublishScriptLocation', Result='PublishScriptFilePath', Workspace='Workspace'. GetLocalPath 작업의 경우 IncomingPath 속성을 'PublishScriptLocation'으로 설정하고 Result를 'PublishScriptFilePath'로 설정합니다. 이 작업은 TFS 서버 위치(해당되는 경우)의 게시 스크립트 경로를 표준 로컬 디스크 경로로 변환합니다.
   5. TFS 2012 이하를 사용하고 있으면 새 시퀀스의 끝 부분에 또 다른 ConvertWorkspaceItem 작업을 추가합니다. Direction=ServerToLocal, DisplayName='Convert subscription filename', Input=' SubscriptionDataFileLocation', Result= 'SubscriptionDataFilePath', Workspace='Workspace'. TFS 2013 이상을 사용하고 있으면 또 다른 GetLocalPath를 추가합니다. IncomingPath='SubscriptionDataFileLocation' 및 Result='SubscriptionDataFilePath'입니다.
   6. 새 시퀀스의 끝 부분에 InvokeProcess 작업을 추가합니다.
      이 작업은 빌드 정의에 의해 전달된 인수를 사용하여 PowerShell.exe를 호출합니다.

      + Arguments = String.Format(" -File ""{0}"" -serviceName {1}  -storageAccountName {2} -packageLocation ""{3}""  -cloudConfigLocation ""{4}"" -subscriptionDataFile ""{5}""  -selectedSubscription {6} -environment ""{7}""",  PublishScriptFilePath, ServiceName, StorageAccountName,  PackageLocation, CloudConfigLocation,  SubscriptionDataFilePath, SubscriptionName, Environment)
      + DisplayName = Execute publish script
      + FileName = "PowerShell"(따옴표 포함)
      + OutputEncoding=  System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage)
   7. InvokeProcess의 **표준 출력 처리** 섹션 텍스트 상자에서 텍스트 상자 값을 'data'로 설정합니다. 이 값은 표준 출력 데이터를 저장하는 변수입니다.
   8. **표준 출력 처리** 섹션 바로 아래에 WriteBuildMessage 작업을 추가합니다. Importance = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' 및 Message='data'로 설정합니다. 그러면 스크립트의 표준 출력이 빌드 출력에 기록됩니다.
   9. InvokeProcess의 **오류 출력 처리** 섹션 텍스트 상자에서 텍스트 상자 값을 'data'로 설정합니다. 이 값은 표준 오류 데이터를 저장하는 변수입니다.
   10. **오류 출력 처리** 섹션 바로 아래에 WriteBuildError 작업을 추가합니다. Message='data'로 설정합니다. 그러면 스크립트의 표준 오류가 빌드 오류 출력에 기록됩니다.
   11. 파란색 느낌표가 표시된 오류를 수정합니다. 오류에 대한 힌트를 얻으려면 느낌표를 마우스로 가리킵니다. 오류를 지우려면 워크플로를 저장합니다.

   게시 워크플로 작업의 최종 결과는 디자이너에 다음과 같이 표시됩니다.

   ![워크플로 작업][5]

   게시 워크플로 작업의 최종 결과는 XAML로 다음과 같이 표시됩니다.

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. 빌드 프로세스 템플릿 워크플로를 저장하고 이 파일을 체크 인합니다.
9. 빌드 정의를 편집하고(이미 열려 있는 경우 닫기), 프로세스 템플릿 목록에 새 템플릿이 표시되지 않으면 **새로 만들기** 단추를 선택합니다.
10. 기타 섹션에서 매개 변수 속성 값을 다음과 같이 설정합니다.

    1. CloudConfigLocation ='c:\\drops\\app.publish\\ServiceConfiguration.Cloud.cscfg' *이 값의 파생 위치: ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. PackageLocation = 'c:\\drops\\app.publish\\ContactManager.Azure.cspkg' *이 값의 파생 위치: ($PublishDir)($ProjectName).cspkg*
    3. PublishScriptLocation = 'c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = 'mycloudservicename' *여기에 적절한 클라우드 서비스 이름 사용*
    5. Environment = 'Staging'
    6. StorageAccountName = 'mystorageaccountname' *여기에 적절한 저장소 계정 이름 사용*
    7. SubscriptionDataFileLocation = 'c:\\scripts\\WindowsAzure\\Subscription.xml'
    8. SubscriptionName = 'default'

    ![매개 변수 속성 값][6]
11. 변경 내용을 빌드 정의에 저장합니다.
12. 빌드를 큐에 대기시켜 패키지 빌드와 게시를 모두 실행합니다. 트리거를 지속적인 통합으로 설정한 경우 이 동작이 체크 인할 때마다 실행됩니다.

### <a name="publishcloudserviceps1-script-template"></a>PublishCloudService.ps1 스크립트 템플릿
```powershell
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy to $servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according to $alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress to activity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>다음 단계
연속 배달을 사용하는 경우 원격 디버깅을 사용하려면 [연속 배달을 사용하여 Azure에 게시할 경우 원격 디버깅 사용](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)을 참조하세요.

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
