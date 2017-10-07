---
title: "aaaNode.js 시작 가이드 | Microsoft Docs"
description: "Toocreate 간단한 Node.js 웹 응용 프로그램 및 tooan Azure 클라우드 서비스 배포 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>빌드 및 배포는 Node.js 응용 프로그램 tooan Azure 클라우드 서비스

이 자습서에서는 어떻게 toocreate 간단한 Node.js 응용 프로그램에서 Azure 클라우드 서비스를 실행 합니다. 클라우드 서비스는 Azure에서 확장 가능한 클라우드 응용 프로그램의 hello 구성 요소입니다. Hello 분리 하 고 독립적인 관리 및 응용 프로그램의 프런트 엔드 및 백 엔드 구성 요소 확장을 허용합니다.  클라우드 서비스는 각 역할을 안정적으로 호스팅할 수 있는 강력한 전용 가상 컴퓨터를 제공합니다.

클라우드 서비스와 어떻게 다른 지 tooAzure 웹 사이트 및 가상 컴퓨터에 대 한 자세한 내용은 참조 하십시오. [Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교]합니다.

> [!TIP]
> Toobuild 간단한 웹 사이트를 찾고 있습니까? 시나리오에 간단한 웹 사이트 프런트 엔드만 포함된 경우 [간단한 웹앱 사용]을 고려해 보십시오. 웹 응용 프로그램 증가 및 요구 사항 변경 tooa 클라우드 서비스를 쉽게 업그레이드할 수 있습니다.

이 자습서를 수행하여 웹 역할 내에서 호스트되는 간단한 웹 응용 프로그램을 빌드합니다. 사용 하는 hello 계산 에뮬레이터 tootest 응용 프로그램을 로컬로 합니다 PowerShell 명령줄 도구를 사용 하 여 배포 합니다.

hello 응용 프로그램은 간단한 "hello world" 응용 프로그램.

![Hello World Hello 웹 페이지를 표시 하는 웹 브라우저][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>필수 조건
> [!NOTE]
> 이 자습서는 Azure PowerShell을 사용하며,

* [Azure PowerShell]을 설치하고 구성합니다.
* 다운로드 및 설치 hello [Azure SDK for.NET 2.7]합니다. Hello에서 설치 프로그램을 설치, 선택:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Azure 클라우드 서비스 프로젝트 만들기
Hello 작업 toocreate 기본 Node.js 스 캐 폴딩 함께 새 Azure 클라우드 서비스 프로젝트를 다음을 수행 합니다.

1. 실행 **Windows PowerShell** 관리자 권한으로; hello **시작 메뉴** 또는 **시작 화면**, 검색할 **Windows PowerShell**합니다.
2. [PowerShell 연결] tooyour 구독 합니다.
3. 다음 PowerShell cmdlet toocreate toocreate hello 프로젝트 hello를 입력 합니다.

        New-AzureServiceProject helloworld

    ![hello New-azureservice helloworld 명령의 hello 결과][hello result of hello New-AzureService helloworld command]

    hello **새로 AzureServiceProject** cmdlet은 Node.js 응용 프로그램 tooa 클라우드 서비스를 게시 하기 위한 기본 구조를 생성 합니다. 여기에 게시 tooAzure에 필요한 구성 파일이 포함 됩니다. hello cmdlet도 hello 서비스에 대 한 작업 디렉터리 toohello 디렉터리를 변경합니다.

    hello cmdlet에는 다음 파일이 hello를 만듭니다.

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** 및 **ServiceDefinition.csdef**는 응용 프로그램을 게시하는 데 필요한 Azure 관련 파일입니다. 자세한 내용은 [Azure에 대한 호스티드 서비스 만들기 개요](영문)를 참조하세요.
   * **deploymentSettings.json**: hello Azure PowerShell 배포 cmdlet에서 사용 되는 로컬 설정을 저장 합니다.
4. Hello 명령 tooadd 새 웹 역할 다음을 입력 합니다.

       Add-AzureNodeWebRole

   ![hello 추가 AzureNodeWebRole 명령의 hello 출력][hello output of hello Add-AzureNodeWebRole command]

   hello **추가 AzureNodeWebRole** cmdlet은 기본 Node.js 응용 프로그램을 만듭니다. 또한 hello 수정 **.csfg** 및 **.csdef** hello 새 역할에 대 한 구성 항목 tooadd 파일입니다.

   > [!NOTE]
   > 역할 이름을 지정하지 않으면 기본 이름이 사용됩니다. Hello 첫 번째 cmdlet 매개 변수로 이름을 제공할 수 있습니다.`Add-AzureNodeWebRole MyRole`

hello 파일에 정의 된 hello Node.js 앱 **server.js**hello 웹 역할에 대 한 hello 디렉터리에 있는 (**WebRole1** 기본적으로). Hello 코드는 다음과 같습니다.

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

이 코드는 "Hello World" hello와 동일 hello에 예제 hello 기본적으로 [nodejs.org] hello 클라우드 환경에 의해 할당 된 hello 포트 번호를 사용 하 여 제외 하 고 웹 사이트입니다.

## <a name="deploy-hello-application-tooazure"></a>Hello 응용 프로그램 tooAzure 배포

> [!NOTE]
> toocomplete이이 자습서에서는 Azure 계정이 필요 합니다. [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF)하거나 [무료 계정을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF)할 수 있습니다.

### <a name="download-hello-azure-publishing-settings"></a>Hello Azure 다운로드 게시 설정
toodeploy 프로그램 응용 프로그램 tooAzure 하면 Azure 구독에 대 한 설정을 게시 하는 hello 먼저 다운로드 해야 합니다.

1. Hello 다음 Azure PowerShell cmdlet을 실행 합니다.

       Get-AzurePublishSettingsFile

   브라우저를 사용 하는이 toonavigate toohello 설정 다운로드 페이지를 게시 합니다. Microsoft 계정으로 증명된 toolog 수도 있습니다. 이 경우에 Azure 구독에 연결 된 hello 계정을 사용 합니다.

   다운로드 한 hello 프로필 tooa 파일 위치에 쉽게 액세스할 수를 저장 합니다.
2. Cmdlet tooimport hello 게시 프로필 다운로드 한 다음 실행 합니다.

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Hello를 가져온 다음 게시 설정, 누군가가 문제가 발생할 수 있는 정보가 포함 되어 있어.publishSettings 파일을 다운로드 한 hello 삭제를 고려해 tooaccess 계정.

### <a name="publish-hello-application"></a>Hello 응용 프로그램 게시
toopublish hello 다음 명령을 실행 합니다.

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** hello 배포에 대 한 hello 이름을 지정 합니다. 고유 이름 이어야 합니다, 그렇지 않으면 hello 게시 프로세스가 실패 합니다. hello **Get-date** hello 이름이 고유 해야 하는 날짜/시간 문자열에 tacks 명령입니다.
* **-위치** hello 응용 프로그램에서 호스팅하는 hello 데이터 센터를 지정 합니다. 사용 가능한 데이터 센터를 사용 하 여 hello 목록이 toosee **Get AzureLocation** cmdlet.
* **-시작** 배포 완료 된 후 toohello 호스팅된 서비스를 이동 하는 브라우저 창을 엽니다.

게시에 성공 하면 응답 비슷한 toohello 다음을 표시 됩니다.

![hello Publish-azureservice 명령의 hello 출력][hello output of hello Publish-AzureService command]

> [!NOTE]
> 응용 프로그램 toodeploy hello에 대 일 분 정도 걸릴 하 고 처음 게시할 때 사용할 수 있을 수 있습니다.

Hello 배포 완료 되 면 브라우저 창을 열고 toohello 클라우드 서비스를 이동 됩니다.

![Hello hello world 페이지를 표시 하는 브라우저 창 hello URL hello 페이지는 Azure에서 호스트 되는 것을 나타냅니다.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

이제 응용 프로그램이 Azure에서 실행되고 있습니다.

hello **게시 AzureServiceProject** cmdlet hello 다음 단계를 수행 합니다.

1. 패키지 toodeploy를 만듭니다. hello 패키지 응용 프로그램 폴더에 모든 hello 파일을 포함 합니다.
2. **저장소 계정** 이 없는 경우 새로 만듭니다. hello Azure 저장소 계정에는 배포 하는 동안 사용 되는 toostore hello 응용 프로그램 패키지입니다. 배포를 완료 한 후에 안전 하 게 hello 저장소 계정을 삭제할 수 있습니다.
3. **클라우드 서비스** 가 아직 없는 경우 새로 만듭니다. A **클라우드 서비스** 는 배포 된 tooAzure 되었을 때 응용 프로그램 호스팅 hello 컨테이너입니다. 자세한 내용은 [Azure에 대한 호스티드 서비스 만들기 개요](영문)를 참조하세요.
4. 배포 패키지 tooAzure hello를 게시합니다.

## <a name="stopping-and-deleting-your-application"></a>응용 프로그램 중지 및 삭제
응용 프로그램을 배포한 후 toodisable 경우가 되므로 추가 비용을 방지할 수 있습니다. Azure는 사용된 서버 시간의 시간당 웹 역할 인스턴스 요금을 청구합니다. 서버 시간 hello 인스턴스를 실행 하지 않는 및 hello 중지 상태인 경우에 응용 프로그램을 배포한 후에 사용 됩니다.

1. Hello Windows PowerShell 창에서 cmdlet 뒤 hello를 사용 하 여 hello 이전 섹션에서 만든 hello 서비스 배포를 중지 합니다.

       Stop-AzureService

   Hello 서비스를 중지 하면 몇 분 정도 걸릴 수 있습니다. Hello 서비스가 중지 되 면이 중지 되었음을 나타내는 메시지가 나타납니다.

   ![hello 중지 AzureService 명령 hello 상태][hello status of hello Stop-AzureService command]
2. cmdlet을 다음 호출 hello toodelete hello 서비스:

       Remove-AzureService

   메시지가 표시 되 면 입력 **Y** toodelete hello 서비스입니다.

   Hello 서비스를 삭제 하면 몇 분 정도 걸릴 수 있습니다. Hello 서비스를 삭제 한 후에 hello 서비스가 삭제 되었거나를 나타내는 메시지가 표시 됩니다.

   ![hello 제거 AzureService 명령 hello 상태][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Hello 서비스를 삭제 hello 서비스, 초기에 게시 하는 경우 만든 hello 저장소 계정을 삭제 되지 않으며 사용 되는 저장소에 대 한 청구 toobe 계속 청구 됩니다. Toodelete hello 저장소를 사용 하는 다른 경우 않을 것입니다.

## <a name="next-steps"></a>다음 단계
자세한 내용은 참조 hello [Node.js 개발자 센터]합니다.

<!-- URL List -->

[Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교]: ../app-service-web/choose-web-site-cloud-service-vm.md
[간단한 웹앱 사용]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK for.NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[PowerShell 연결]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Azure에 대한 호스티드 서비스 만들기 개요]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js 개발자 센터]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
