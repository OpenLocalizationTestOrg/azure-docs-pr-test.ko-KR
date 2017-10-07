---
title: "자습서: Azure 포털 hello로 DevOps | Microsoft Docs"
description: "자세한 내용은 hello Azure 포털에서에서 다양 한 DevOps 워크플로 hello 합니다."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Azure 포털 hello로 DevOps 자습서:
Azure 플랫폼 hello 유연한 DevOps 워크플로의 가득 찼습니다. 이 자습서에서는 hello Azure 포털 toodevelop의 tooleverage hello 기능 테스트, 배포, 문제 해결, 모니터링 및 관리 방법을 실행 중인 응용 프로그램 설명 합니다. 이 자습서는 hello 다음에 중점을 둡니다.

1. 웹앱 만들기 및 지속적인 배포 사용
2. 앱 개발 및 테스트
3. 앱 모니터링 및 문제 해결
4. 일반 응용 프로그램 관리 작업

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>웹앱 만들기 및 지속적인 배포 사용
웹 앱을 만드는 [Azure 앱 서비스](https://azure.microsoft.com/services/app-service/),이 자습서의 나머지 부분 hello에서에서 사용할 수 있습니다. 실행 중인 Azure 환경에 소스 코드 리포지토리의 지속적인 배포를 처음부터 사용할 수 있습니다.

1. Hello Azure 포털에 로그인
2. 선택 **응용 프로그램 서비스** &gt; **추가 아이콘** 입력 이름을, 구독을 선택 하 고 새 리소스 그룹 tooserve hello 서비스에 대 한 hello 컨테이너로 만듭니다.
   
   리소스 그룹을 사용 toomanage 하면 대금 청구, 배포 및 모니터링 모두를 통해 단일 그룹으로 같은 hello 솔루션의 다양 한 측면 [Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md)합니다.
   
   ![image1][image1]
3. 앱 서비스는 몇 분 후에 생성됩니다. Hello 포털에서 몇 분 tooexplore hello hello 서비스에 대 한 다양 한 메뉴 옵션을 사용 합니다.
   
   ![image2][image2]    
4. Hello URL을 클릭 합니다. Hello 다양 한 도구 및 저장소에 대해 사용 가능한 선택 항목을 확인 합니다. 또한 hello 언어 및.NET, Java, Ruby 등 원하는 프레임 워크를 사용할 수 있습니다.
   
   ![image3][image3]    
5. hello Azure 포털만 몇 가지 간단한 단계를 수행 해야 하는 쉬운 작업을 연속 배포를 만듭니다. Hello Azure 포털에서에서 방금 만든 hello 응용 프로그램 서비스에 대 한 hello 아이콘에서 설정을 선택 합니다.
   
   ![image4][image4]
   
   Hello 오른쪽에 열리는 hello 블레이드에서에서 섹션 게시 toohello를 스크롤하십시오.
   
   ![image5][image5]
6. 다음으로 hello 앱에 대 한 일부 설정을 tooenable 연속 배포를 구성 합니다. 배포 원본을 클릭한 다음 원본 선택을 클릭합니다. Hello 다양 한 리포지토리 소스에 대 한 옵션을 확인 합니다.
   
   ![image6][image6]
7. 이 예제에서는 GitHub를 선택합니다. 원하는 경우 원하는 hello 리포지토리를 선택 하 고 hello 권한 부여 자격 증명을 설정 합니다.
   
   ![image7][image7]
8. 권한 부여 tooyour 저장소 후 프로젝트 및 toodeploy 원하는 분기를 다음 선택할 수 있습니다. 여러 가상 샘플 예제가 아래에 나열됩니다.
   
   ![image8][image8]
9. 프로젝트 및 분기를 선택하면 확인을 클릭합니다. 배포의 toosee 알림을 시작 해야 합니다.
   
   ![image9][image9]
10. Azure를 사용 하 여 toointegrate hello 소스 제어 리포지토리에 만든 뒤로 tooGitHub toosee hello webhook을 이동 합니다. hello Azure 포털에는 몇 가지 간단한 단계만 거치면만 GitHub와 통합할 수 있습니다.
    
    ![image10][image10]
11. toodemonstrate 연속 배포를 신속 하 게 추가한 일부 콘텐츠 toohello 저장소입니다. 간단한 예제에서는 샘플 텍스트 파일 tooa GitHub 리포지토리를 추가 합니다. 넌 무료 toouse.NET, Ruby, Python 또는 기타 다른 유형의 응용 프로그램 서비스와 응용 프로그램. 무료 tooadd 텍스트 파일을 느낄 ASP.NET MVC, Java 또는 Ruby 응용 프로그램 toohello 리포지토리를 선택 합니다.
    
    ![image11][image11]
12. 변경 내용을 tooyour 리포지토리를 커밋한 후 새 표시 hello 포털 알림 영역에서 배포를 시작 합니다. Tooyour 리포지토리 커밋한 후 변경 내용을 신속 하 게 표시 되지 않으면 동기화를 클릭 합니다.
    
    ![image12][image12]
13. 이 시점에서 hello 응용 프로그램 서비스에 대 한 hello 페이지를 로드 하 고 시도 하는 경우에 403 오류가 나타날 수 있습니다. 이 예제에서는 되므로 index.htm 또는 default.html와 같은 파일 처럼 hello 페이지에 대 한 일반적인 기본 문서를 설치 하지 않아도 됩니다. Hello Azure 포털에서에서 tooling hello로이 문제를 신속 하 게 해결할 수 있습니다.  Hello Azure 포털에서에서 설정을 선택 &gt; 응용 프로그램 설정 합니다.
    
     ![image13][image13]
14. 응용 프로그램 설정을 위한 블레이드가 열립니다. Hello 페이지 "SamplePage.html" hello 이름을 입력 하 고 저장을 클릭 합니다. 몇 분 tooexplore hello 다른 설정을 사용 합니다.
    
    ![image14][image14]
15. 필요에 따라 예상 hello 변경 내용을 참조 하 여 브라우저 URL tooensure를 새로 고칩니다. 이 경우 몇 가지 간단한 텍스트 이제 hello 페이지를 채우는 있습니다. 각 추가 변경 toohello 저장소는 새 자동 배포 유발 합니다.
    
    ![image15][image15]
    
    Azure 포털 hello로 연속 배포를 사용 하면 쉽게입니다. 더 복잡 한 릴리스 파이프라인 하 고 기존 소스 제어 및 연속 통합 시스템 toodeploy tooAzure 자동화 된 빌드 및 릴리스 관리 시스템을 활용 하는 등 다른 여러 가지 방법을 사용할 수도 있습니다.

## <a name="develop-and-test-an-app"></a>앱 개발 및 테스트
다음을 일부 변경 toohello 코드 기본 하 고 신속 하 게 이러한 변경 내용을 배포 합니다. 일부 성능 hello 웹 앱에 대 한 테스트를 설정할는 있습니다.

1. Hello Azure 포털에서에서 hello 탐색 창에서 응용 프로그램 서비스를 선택 하 고 응용 프로그램 서비스를 찾습니다.
   
   ![image16][image16]
2. 도구를 클릭합니다.
   
   ![image17][image17]
3. Hello 개발 도구는 범주를 확인 합니다. 여러 가지 유용한 도구가 여기 hello Azure 포털을 종료 하지 않고 앱과 toowork 수 있는 합니다. 콘솔을 클릭합니다.
   
   ![image18][image18]
4. Hello 콘솔 창에 앱에 대 한 라이브 명령을 실행할 수 있습니다. Type hello dir 명령 고를 입력합니다. 상승된 권한이 필요한 명령은 작동하지 않습니다.
   
   ![image19][image19]
5. Toohello 개발 범주를 다시 이동 하 고 Visual Studio Online을 선택 합니다. 참고: Visual Studio Online은 이제 Visual Studio Team Services로 이름을 지정합니다.
   
   ![image20][image20]
6. 앱에 대 한 브라우저 내부 편집 환경을 hello 전환 합니다.
   
   ![image21][image21]
7. 앱에 웹 확장을 설치합니다. 확장 쉽고 빠르게 기능 tooapps Azure에서 추가. Hello 스크린 샷 아래에서 사용할 수 있는 다른 확장 형식 hello 중 일부를 확인 합니다.
   
   ![image22][image22]
8. Visual Studio Online 확장 hello 설치 되 면 이동을 클릭 합니다.
   
   ![image23][image23]
9. 브라우저 탭이 열리고 hello 브라우저에서 직접 개발 IDE를 표시 합니다. 크롬 아래 공지 hello 환경이입니다.
   
   ![image24][image24]
10. 편집 파일 등 여러 작업을 수행 하 고, 파일 및 폴더를 추가 하 고, hello 라이브 사이트에서 콘텐츠를 다운로드 수 있습니다. 빠른 편집 toohello SamplePage.html 파일을 확인 합니다.
    
    ![image25][image25]
11. 몇 분 정도 hello 변경 내용은 자동으로 저장 됩니다. 뒤로 toohello 페이지를 탐색 하는 경우 hello 변경 내용을 볼 수 있습니다. 다음과 같은 라이브 편집이 프로덕션 환경에 적합하지 않다는 점을 염두에 둡니다. 그러나 hello 도구 개발에 대 한 매우 쉽게 toomake 빠른 변경 하 고 테스트 환경 합니다.
    
    ![image26][image26]
    
    ![image27][image27]
12. Toohello 도구 블레이드를 다시 이동 하 고 hello 개발 범주에서 성능 테스트를 클릭 합니다.
    
    ![image28][image28]
13. Tooset team services 계정이 필요합니다. 자세한 내용을 보려면 [팀 서비스 계정 만들기](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
14. 새 toocreate 성능 테스트를 클릭 합니다.
    
    ![image29][image29]
    
    구성 다양 한 값을 hello 및 hello 아래쪽 hello dialogue tooinitiate 성능 테스트의 테스트 실행을 클릭 합니다.
    
    ![image30][image30]
    
    ![image31][image31]
15. Hello 테스트 실행 시작 되 면 hello 상태를 모니터링할 수 있습니다.
    
    ![image32][image32]
    
    Hello 테스트 완료 되 면 hello 결과 클릭 하면 자세한 세부 정보를 표시 합니다.
    
    ![image33][image33]
16. 이 예제에서는 제한 된 데이터 tooanalyze 이지만 있습니다 수 다양 한 메트릭을 확인할 뿐만 아니라이 보기에서 테스트를 다시 실행 되도록 실행 하는 작은 테스트를 만들었습니다. hello Azure 포털 만들기, 실행 및 웹 성능 테스트 쉬운 작업 분석을 만듭니다. 아래 hello 스크린샷과 hello 성능 데이터를 표시합니다.
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>앱 모니터링 및 문제 해결
Azure는 실행 중인 응용 프로그램을 모니터링하고 문제를 해결하는 다양한 기능을 제공합니다.

1. 웹 앱에 대 한 hello Azure 포털에서에서 도구를 선택 합니다.
   
   ![image37][image37]
2. Hello 문제 해결 범주에서 hello 도구 tootroubleshoot 잠재적 문제를 실행 중인 응용 프로그램 사용에 대 한 다양 한 옵션을 확인 합니다. HTTP 라이브 트래픽 모니터링, 자체 치유 사용, 로그 보기 등의 작업을 수행할 수 있습니다.
   
   ![image38][image38]
3. 사이트 메트릭을 tooquickly get 일부 HTTP 코드의 보기를 선택 합니다.
   
   ![image39][image39]
4. 서비스로서의 진단을 선택합니다. 응용 프로그램 형식을 선택한 다음 실행을 선택합니다.
   
   ![image40][image40]
   
   컬렉션을 시작합니다.
   
   ![image41][image41]
5. Hello 적절 한 로그 toodiagnose 잠재적인 문제를 선택할 수 있습니다. Hello 사용 가능한 데이터의 모든 HTTP 로그와 같은 옵션 tooenable 로깅 toosee가 필요 합니다.
   
   ![image42][image42]
   
   Hello 메모리 덤프 파일을 다운로드 하 고는 \t<li>debugdiag을 분석할 수를 클릭 하 여 분석 보고서 toohelp 잠재적인 문제를 찾습니다.
   
   ![image43][image43]
6. tooview 더 많은 데이터를 추가 로깅 tooenable 필요 합니다. Hello Azure 포털에서에서 toohello 웹 응용 프로그램을 이동 하 고 설정을 선택 합니다.
   
   ![image44][image44]
7. Toohello 기능 범주, 아래로 스크롤하여 진단 로그를 선택 합니다.
   
      ![image45][image45]
8. Hello 로깅에 대 한 다양 한 옵션을 확인 합니다. 웹 서버 로깅을 설정하고 저장을 클릭합니다.
   
   ![image46][image46]
9. Hello 앱에 대 한 toohello 도구 영역 다시 이동 하 고 진단 서비스를 선택 합니다. 실행 toorerun hello 데이터 컬렉션을 클릭 합니다.
   
   ![image47][image47]
10. Hello HTTP 로깅 설정을 사용 하도록 설정, 이제 HTTP 로그 수집 된 데이터를 표시 합니다.
    
    ![image48][image48]
11. Hello HTML 파일 로그를 클릭 하 여 추가로 조사 하기 위해 풍부한 브라우저 기반 보고서를 생성 합니다.
    
    ![image49][image49]
12. Hello 앱에 대 한 hello Azure 포털의에서 도구 섹션 toohello 다시 이동 합니다. Toohello 도구 섹션 스크롤하여 프로세스 탐색기를 선택 합니다.
    
    ![image50][image50]
13. 프로세스 탐색기를 선택하여 프로세스를 실행하는 방법에 대한 세부 정보를 볼 수 있습니다. 알림 하위 프로세스 더 자세히 분석 하 고도 모두 hello Azure 포털에서에서 프로세스를 종료할 수 있습니다.
    
    ![image51][image51]
    
    ![image52][image52]
14. Toohello 설정 블레이드에서 hello 왼쪽에 다시 이동 합니다. 새 지원 요청을 클릭합니다.
    
    ![image53][image53]
15. Hello 오른쪽에 hello 블레이드에서 hello 문제에 대 한 세부 정보를 채울 연락처 정보를 입력 한도 진단 데이터를 업로드 수 있습니다. Azure 포털 hello 원활한 환경을 Microsoft 지원에 사용할 수 있습니다.
    
    ![image54][image54]
    
    ![image55][image55]
    
    강력 하 고 친숙 한 환경을 toohelp 모니터 도구를 제공 하 고 실행 중인 응용 프로그램을 해결 하는 hello Azure 포털. 인 수 tootake 동작 신속 하 게 프로세스 재활용, 활성화 및 다양 한 데이터 컬렉션을 비활성화 및 Microsoft 전문가 지원와도 통합 등의 작업을 수행 하 여 합니다.

## <a name="general-application-management"></a>일반 응용 프로그램 관리
응용 프로그램을 관리 하는 경우, 다양 한 백업 전략을 구성, 구현 및 id 공급자를 관리 및 역할 기반 액세스 제어를 구성 하는 등의 작업 tooperform이 필요한 경우가 많습니다. 와 다른 DevOps 경험 hello, 처럼 hello Azure 플랫폼 hello 포털에 직접 이러한 작업을 통합 합니다.

1. tooensure 관리 하는 웹 응용 프로그램 hello tooconfigure 백업이 필요한 데이터 손실 로부터 안전 하 게 합니다. 웹 앱에 대 한 toohello 설정 영역을 이동 합니다.
   
   ![image56][image56]
2. Hello 오른쪽에 hello 블레이드에서 toohello 기능 범주 아래로 스크롤하십시오.
   
    ![image57][image57]
3. 백업을;를 선택 합니다. hello 오른쪽에 블레이드가 열립니다.
   
   ![image58][image58]
4. 구성, 오른쪽 hello에 hello 블레이드에서 저장소 계정을 선택 합니다.
   
   ![image59][image59]
5. 잠시 만들고 이제 저장소 컨테이너 toohold 백업을 선택 합니다. Hello hello 블레이드 맨 아래에 만들기를 클릭 합니다. 다음 hello 컨테이너를 선택 합니다.
   
   ![image60][image60]
6. Hello 컨테이너를 선택 하면 데이터베이스에 대 한 설치 백업 뿐만 아니라 일정을 구성할 수 있습니다. 이 시나리오에 대 한 hello 저장 아이콘을 클릭 합니다.
   
    ![image61][image61]
7. 저장 한 후 백업에 대 한 hello 왼쪽에 뒤로 toohello 블레이드를 스크롤하십시오. 지금 백업 tooback hello 응용 프로그램을 클릭 합니다.
   
    ![image62][image62]
8. 몇 분 내에 만든 백업을 볼 수 있습니다. 공지 hello hello 스크린 샷 아래에서 지금 복원 옵션입니다.
   
    ![image63][image63]
9. 지금 복원 클릭 하 고 오른쪽 hello에 hello 옵션 toohello 블레이드를 검토 합니다. 적절 한 백업 및 쉽게 복원 tooan 이전 상태 필요에 따라 선택할 수 있습니다. Azure 포털 hello hello 앱에 대 한 간단한 재해 복구 전략을 사용 하는 쉽게 통해 합니다.
   
    ![image64][image64]
10. Hello 왼쪽에 및 기능에서 toohello 설정 블레이드에서 다시 이동 하 고 인증/권한 부여를 선택 합니다.
    
     ![image65][image65]
11. Hello 오른쪽에 hello 블레이드에서 응용 프로그램 서비스 인증을 선택 합니다. Hello 다양 한 인기 있는 공급자와 함께 구성할 수 있습니다 하는 옵션을 확인 합니다.
    
     ![image66][image66]
12. 원하는 hello 공급자를 선택 하 고 hello 범위에 대 한 hello 옵션을 확인 합니다. 앱 ID와 응용 프로그램 암호를 제공할 수 있으며 hello 앱에 대 한 Facebook 인증을 신속 하 게 수 있습니다. hello Azure 포털 앱에 대 한 턴키 솔루션으로 인증을 활성화 합니다.
    
     ![image67][image67]
13. Toohello 설정 블레이드를 다시 이동 하 고 hello 리소스 관리 범주 아래에서 사용자를 선택 합니다.
    
     ![image68][image68]
14. Hello 오른쪽에 hello 블레이드에서 검사 hello 역할 및 사용자를 추가 하기 위한 다양 한 옵션입니다. Azure 포털 hello를 사용 하면 쉽게 hello 응용 프로그램에 대 한 RBAC (역할 기반 액세스 제어)를 제어할 수 있습니다.
    
     ![image69][image69]

## <a name="summary"></a>요약
이 자습서는 hello Azure 플랫폼을 사용 하 여 hello 전원 중 일부를 신속 하 게 웹 앱에 대 한 연속 배포를 사용 하도록 설정, 다양 한 개발을 수행 하 고 테스트 작업을 수행할 모니터링 및 라이브 앱 문제 해결 및 마지막으로 키를 관리 하 여 표시 재해 복구, id 및 역할 기반 액세스 제어와 같은 전략입니다. Azure 플랫폼 hello 이러한 DevOps 워크플로에 대 한 통합된 된 환경을 있으며 특정 hello 진행 중인 작업에 대 한 컨텍스트에 유지 하 여 효율적으로 작업할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* Azure 리소스 관리자는 DevOps hello Azure 플랫폼에서 사용 하도록 설정 하는 데 중요 합니다.  toolearn 더 방문 [Azure 리소스 관리자 개요](../azure-resource-manager/resource-group-overview.md)합니다.
* Azure 앱 서비스 배포에 대 한 자세한 방문 toolearn [사용자 앱 tooAzure 앱 서비스 배포](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
