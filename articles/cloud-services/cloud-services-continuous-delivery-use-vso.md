---
title: "Azure에서 Visual Studio Team Services를 사용한 aaaContinuous 배달 | Microsoft Docs"
description: "어떻게 tooconfigure Visual Studio Team Services 팀 프로젝트 tooautomatically 빌드 및 Azure 앱 서비스 또는 클라우드 서비스의 toohello 웹 응용 프로그램 기능을 배포에 대해 알아봅니다."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>Visual Studio Team Services를 사용 하 여 지속적인 업데이트 tooAzure
Visual Studio Team Services 팀 프로젝트 tooautomatically 빌드를 구성 하 고 tooAzure 웹 앱을 배포 하거나 클라우드 서비스 수 있습니다.  (Tooset 연속 빌드를 하 고 사용 하 여 시스템을 배포 하는 방법에 대 한 내용은 *온-프레미스* Team Foundation Server 참조 [Azure에서 클라우드 서비스에 대 한 지속적인 업데이트](cloud-services-dotnet-continuous-delivery.md).)

이 자습서에서는 Visual Studio 2013과 hello Azure SDK가 설치 되어 있다고 가정 합니다. Visual Studio 2013, 아직 없는 경우 hello를 선택 하 여 다운로드 **무료로 시작** 동시 연결할 [www.visualstudio.com](http://www.visualstudio.com)합니다. 설치에서 Azure SDK hello [여기](http://go.microsoft.com/fwlink/?LinkId=239540)합니다.

> [!NOTE]
> 이 자습서는 Visual Studio Team Services 계정 toocomplete 필요한: 할 수 있습니다 [무료 Visual Studio Team Services 계정 열고](http://go.microsoft.com/fwlink/p/?LinkId=512979)합니다.
> 
> 

클라우드 서비스 tooautomatically tooset 빌드 및 Visual Studio Team Services를 사용 하 여 tooAzure 배포, 다음이 단계를 수행 합니다.

## <a name="1-create-a-team-project"></a>1:팀 프로젝트 만들기
Hello 지침에 따라 [여기](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate 팀 프로젝트 및 tooVisual Studio에 연결 합니다. 이 연습에서는 TFVC(Team Foundation 버전 제어)를 소스 제어 솔루션으로 사용하고 있는 것으로 가정합니다. 버전 제어에 Git toouse를 원하는 경우 참조 [이 연습의 hello Git 버전](http://go.microsoft.com/fwlink/p/?LinkId=397358)합니다.

## <a name="2-check-in-a-project-toosource-control"></a>2: 프로젝트 toosource 컨트롤에서 확인 필요
1. Visual Studio에서 toodeploy, 하거나 새로 만들 hello 솔루션을 엽니다.
   웹 앱을 배포할 수 또는이 연습 단계를 다음 hello 사용 하 여 클라우드 서비스 (Azure 응용 프로그램).
   Toocreate 새 솔루션을 사용 하도록 하려는 경우 새 Azure 클라우드 서비스 프로젝트를 또는 새 ASP.NET MVC 프로젝트를 만듭니다. 있는지 하는 프로젝트의 대상.NET Framework 4 또는 4.5에서 hello와 클라우드 서비스 프로젝트를 만드는 경우 ASP.NET MVC 웹 역할 및 작업자 역할을 추가 하 고 hello 웹 역할에 대 한 인터넷 응용 프로그램을 선택 합니다. 메시지가 표시되면 **인터넷 응용 프로그램**을 선택합니다.
   웹 앱 toocreate 원한다 면 hello ASP.NET 웹 응용 프로그램 프로젝트 템플릿을 선택 하 고 MVC를 선택 합니다. [Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램 만들기](../app-service-web/app-service-web-get-started-dotnet.md)
   
   > [!NOTE]
   > Visual Studio Team Services는 현재 Visual Studio 웹 응용 프로그램의 CI 배포만 지원합니다. 웹 사이트 프로젝트는 범위를 벗어납니다.
   > 
   > 
2. Hello 솔루션에 대 한 hello 상황에 맞는 메뉴를 열고 **솔루션 추가 tooSource 컨트롤**합니다.
   
    ![][5]
3. 수락 하거나 hello 기본값을 변경 하 고 hello 선택 **확인** 단추입니다. Hello 프로세스가 완료 되 면 소스 제어 아이콘에 표시 **솔루션 탐색기**합니다.
   
    ![][6]
4. Hello 솔루션에 대 한 hello 바로 가기 메뉴를 열고 **체크 인**합니다.
   
    ![][7]
5. Hello에 **보류 중인 변경 내용** 부문의 **팀 탐색기**hello 체크 인에 대 한 설명을 입력 하 고 hello 선택 **체크 인** 단추입니다.
   
    ![][8]
   
    Hello 옵션 tooinclude 또는 특정 변경 내용을 체크 인할 때 제외. 제외 된 변경 내용이 필요한 경우 선택 hello **모두 포함** 링크 합니다.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3: hello 프로젝트 tooAzure 연결
1. 준비 tooconnect는 몇 가지 소스 코드로 VS Team Services 팀 프로젝트에를 팀 프로젝트 tooAzure 합니다.  Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885)클라우드 서비스나 웹 응용 프로그램을 선택 하거나 hello를 선택 하 여 새로 만들  **+**  왼쪽 아래 hello 및 선택 아이콘 **클라우드서비스** 또는 **웹 앱** 차례로 **빨리 만들기**합니다. Hello 선택 **Visual Studio Team Services를 통해 게시 설정** 링크 합니다.
   
    ![][10]
2. Hello 마법사에서 hello 텍스트 상자에 hello Visual Studio Team Services 계정 이름을 입력 하 고 hello 클릭 **이제 권한을 부여** 링크 합니다. toosign을 메시지가 나타날 수 있습니다.
   
    ![][11]
3. Hello에 **연결 요청** 팝업 대화 상자에서 선택 hello **Accept** 단추 tooauthorize Azure tooconfigure VS Team Services에서 팀 프로젝트입니다.
   
    ![][12]
4. 권한 부여가 완료되면 Visual Studio Team Services 팀 프로젝트 목록이 포함된 드롭다운이 표시됩니다. Hello 이전 단계에서 만든 팀 프로젝트의 hello 이름을 선택 하 고 hello 마법사의 확인 표시 단추를 선택 합니다.
   
    ![][13]
5. 프로젝트에 연결 된 후 변경 내용 tooyour Visual Studio Team Services 팀 프로젝트에서 검사에 대 한 몇 가지 지침 표시 됩니다.  다음에 체크 인할에서 Visual Studio Team Services 빌드하고 프로젝트 tooAzure 배포 됩니다.  이 구문은 이제 hello를 클릭 하 여 try **Visual Studio에서 체크 인** 링크를 선택한 다음 hello **Visual Studio 시작** 링크 (또는 해당 하는 hello **Visual Studio** hello 아래쪽의 단추 hello 포털 화면)입니다.
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: 프로젝트 다시 빌드 및 다시 배포 트리거
1. Visual Studio에서 **팀 탐색기**, hello 선택 **소스 제어 탐색기** 링크 합니다.
   
    ![][15]
2. Tooyour 솔루션 파일을 찾아 엽니다.
   
    ![][16]
3. **솔루션 탐색기**에서 파일을 열어 변경합니다. 예를 들어 hello 파일을 변경 `_Layout.cshtml` hello 보기에서\\MVC 웹 역할에서 공유 폴더입니다.
   
    ![][17]
4. Hello 사이트에 대 한 hello 로고를 편집 및 선택 **Ctrl + S** toosave hello 파일입니다.
   
    ![][18]
5. **팀 탐색기**, hello 선택 **보류 중인 변경 내용** 링크 합니다.
   
    ![][19]
6. 메모를 입력 한 다음 hello **체크 인** 단추입니다.
   
    ![][20]
7. Hello 선택 **홈** 단추 tooreturn toohello **팀 탐색기** 홈 페이지입니다.
   
    ![][21]
8. Hello 선택 **빌드** 링크 tooview hello 빌드 진행 중에서입니다.
   
    ![][22]
   
    **팀 탐색기** 에서 빌드의 체크 인이 트리거되었음을 보여 줍니다.
   
    ![][23]
9. 진행 중 tooview 자세한 로그의에서 hello 빌드의 hello 이름을 두 번 클릭 hello 빌드 진행 됨에 따라.
   
    ![][24]
10. Hello 빌드가 진행 중인 hello 마법사를 사용 하 여 TFS tooAzure를 연결 하면 만든 hello 빌드 정의에서 살펴보겠습니다.  Hello 빌드 정의 대 한 hello 바로 가기 메뉴를 열고 **빌드 정의 편집**합니다.
    
     ![][25]
    
     Hello에 **트리거** 탭 표시 됩니다는 hello 빌드 정의 toobuild 모든 체크 인에서 기본적으로 설정 됩니다.
    
     ![][26]
    
     Hello에 **프로세스** 탭 hello 배포 환경에 클라우드 서비스 또는 웹 응용 프로그램의 toohello 이름을 설정 되어을 확인할 수 있습니다. 웹 앱을 사용 하는 참조 하는 hello 속성 다르면 여기에 표시 됩니다.
    
     ![][27]
11. Hello 기본값 값은 다른 hello 속성에 대 한 값을 지정 합니다. hello Azure 게시에 대 한 속성에에서 있는 hello **배포** 섹션.
    
     hello 다음 표에 나와 hello 사용 가능한 속성 hello **배포** 섹션:
    
    | 속성 | 기본값 |
    | --- | --- |
    | 신뢰할 수 없는 인증서 허용 |false인 경우 루트 인증 기관에서 SSL 인증서에 서명해야 합니다. |
    | 업그레이드 허용 |Hello 배포 tooupdate 새로 만드는 대신 기존 배포를 허용 합니다. Hello IP 주소를 유지합니다. |
    | 삭제 안 함 |true인 경우 관련 없는 기존 배포를 덮어쓰지 않습니다(업그레이드가 허용됨). |
    | 경로 tooDeployment 설정 |hello tooyour.pubxml 파일 경로 웹 앱, 상대 toohello hello 리 포 루트 폴더에 대 한 합니다. 클라우드 서비스의 경우 무시됩니다. |
    | SharePoint 배포 환경 |hello 서비스 이름으로을 hello 동일 합니다. |
    | Azure 배포 환경 |hello 웹 응용 프로그램 또는 클라우드 서비스 이름입니다. |
12. 여러 서비스 구성 파일 (.cscfg)을 사용 하는 경우 hello에 원하는 서비스 구성을 hello를 지정할 수 있습니다 **빌드, 고급, MSBuild 인수** 설정 합니다. 예를 들어 toouse ServiceConfiguration.Test.cscfg, MSBuild 인수 선 옵션 설정 `/p:TargetProfile=Test`합니다.
    
     ![][38]
    
     이제 빌드가 완료됩니다.
    
     ![][28]
13. Hello 빌드 이름을 두 번 클릭 하면 Visual Studio는 표시는 **빌드 요약**, 연결 된 단위 테스트 프로젝트의 모든 테스트 결과 포함 합니다.
    
     ![][29]
14. Hello에 [Azure 클래식 포털](http://go.microsoft.com/fwlink/?LinkID=213885), hello에 관련 된 hello 배포를 볼 수 있습니다 **배포** hello 스테이징 환경 선택 된 경우를 탭 합니다.
    
     ![][30]
15. 찾아보기 tooyour 사이트의 URL입니다. 웹 앱에 대 한 클릭 hello **찾아보기** hello 명령 모음에서 단추입니다. 클라우드 서비스에 대 한 hello에 hello URL 선택 **빠른 보기** hello 섹션 **대시보드** 클라우드 서비스에 대 한 hello 스테이징 환경을 보여 주는 페이지. 클라우드 서비스에 대 한 연속 통합에서 배포는 기본적으로 게시 된 toohello 스테이징 환경입니다. Hello 설정 하 여 변경할 수 있습니다 **대체 클라우드 서비스 환경** 속성 너무**프로덕션**합니다. 이 스크린샷은 여기서 hello hello 클라우드 서비스의 대시보드 페이지에서 사이트 URL이 있습니다.
    
    ![][31]
    
    새 브라우저 탭이 열립니다 실행 중인 사이트 tooreveal 됩니다.
    
    ![][32]
    
    클라우드 서비스에 대 한 다른 변경 내용을 tooyour 프로젝트를 만들면 하면 트리거 더 빌드 및 배포를 여러 개를 누적 합니다. hello 최신 활성으로 표시 합니다.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: 초기 빌드 다시 배포
이 단계는 toocloud 서비스를 적용 하 고 선택 사항입니다. 에 Azure 클래식 포털 hello 이전 배포를 선택 하 고 hello 선택 **재배포** 단추 toorewind 사이트 tooan를 앞에서 체크 인 합니다.  그러면 TFS에 새 빌드가 트리거되고 배포 기록에 새 항목이 생성됩니다.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: hello 프로덕션 배포를 변경 합니다.
이 단계는 웹 앱이 아니라 toocloud 서비스만 적용 됩니다. 준비 되 면 hello를 선택 하 여 hello 준비 toohello 프로덕션 환경의 승격할 수 있습니다 **교체** hello Azure 클래식 포털에서에서 단추입니다. 새로 배포 된 hello 스테이징 환경 승격된 tooProduction 이며 hello 이전 프로덕션 환경에서는 있는 경우 스테이징 환경 있게 됩니다. 활성 배포 hello hello 프로덕션 및 스테이징 환경에 대해 다를 수 있습니다 하지만 최근 빌드 hello 배포 기록을 hello 동일 환경에 관계 없이 합니다.

![][35]

## <a name="7-run-unit-tests"></a>7: 단위 테스트 실행
이 단계에만 tooweb 앱, 클라우드 서비스가 아닌 적용 됩니다. 배포에 품질 게이트 tooput 단위 테스트를 실행할 수 있습니다 및 hello 배포 하지 않은 경우 중지할 수 있습니다.

1. Visual Studio에서 단위 테스트 프로젝트를 추가합니다.
   
   ![][39]
2. Tootest 원하는 프로젝트 참조 toohello 프로젝트를 추가 합니다.
   
   ![][40]
3. 일부 단위 테스트를 추가합니다. 시작 tooget는 항상 전달 하는 더미 테스트를 하십시오.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Hello 빌드 정의 편집, hello 선택 **프로세스** 탭을 확장 hello **테스트** 노드.
5. 집합 hello **테스트 실패 시 빌드 실패** tooTrue 합니다. 즉, hello 테스트를 통과 하지 않는 한 hello 배포가 발생 하지 않습니다.
   
   ![][41]
6. 새 빌드를 큐에 넣습니다.
   
   ![][42]
   
   ![][43]
7. Hello 빌드가 진행 되는 동안 해당 진행 상태를 확인 합니다.
   
    ![][44]
   
    ![][45]
8. Hello 빌드가 완료 된 hello 테스트 결과 확인 합니다.
   
    ![][46]
   
    ![][47]
9. 실패로 끝나는 테스트를 만들어 봅니다. 첫 번째 hello를 복사 하 여 새 테스트를 추가 하 고 이름을 바꾸거나, NotImplementedException 된 예상 되는 예외를 설명 하는 코드의 hello 줄을 주석으로 합니다.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. 체크 인 hello tooqueue 새 빌드를 변경 합니다.
    
     ![][48]
11. Hello 테스트 결과 toosee hello 실패에 대 한 정보를 봅니다.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>다음 단계
Visual Studio Team Services의 단위 테스트에 대한 자세한 내용은 [빌드에서 단위 테스트 실행](http://go.microsoft.com/fwlink/p/?LinkId=510474)을 참조하세요. Git를 사용 하 여 참조 [Git에서 코드를 공유할](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) 및 [연속 배포 tooAzure 앱 서비스](../app-service-web/app-service-continuous-deployment.md)합니다.  Visual Studio Team Services에 대한 자세한 내용은 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)를 참조하세요.

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
