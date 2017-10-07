---
title: "Visual Studio Online을 사용 하 여 클라우드에 대 한 aaaContinuous 배달 서비스 | Microsoft Docs"
description: "자세한 방법을 tooset Azure에 대 한 지속적인 업데이트를 클라우드 앱 진단 저장소 키 toohello 서비스 구성 파일을 저장 하지 않고"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a>Securely 클라우드 서비스 진단 저장소 키 저장 및 Visual Studio Online을 사용 하 여 설치 연속 통합 및 배포 tooAzure
 이제 것이 일반적인 사례 tooopen 소스 프로젝트입니다. 구성 파일에 응용 프로그램 암호를 저장하는 방식은 암호가 공개 소스 제어에서 유출되어 보안 취약점에 노출되므로 더 이상 안전하지 않습니다. 연속 통합 파이프라인의 파일에 일반 텍스트 형식 안전 하지 않습니다. 암호를 저장 하거나 빌드 서버 수 있으므로 공유 리소스 hello 클라우드 환경에서입니다. 이 문서에서는 Visual Studio 및 Visual Studio Online 완화 하는 방법을 hello 보안상 개발 및 연속 통합 프로세스 중에 대해 설명 합니다.

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a>프로젝트 구성 파일에서 진단 저장소 키 암호 제거
클라우드 서비스 진단 확장에서는 진단 결과를 저장하기 위해 Azure Storage가 필요합니다. 이전 hello 저장소 연결 문자열 hello 클라우드 서비스 구성 (.cscfg) 파일에 지정 된 및 toosource 제어 확인할 수 있습니다. 최신 Azure SDK 릴리스 hello hello 동작 tooonly 저장소는 토큰으로 대체 하는 hello 키와 부분 연결 문자열을 변경 했습니다. 단계를 수행 하는 hello hello 새 클라우드 서비스 도구가 작동 하는 방법을 설명 합니다.

### <a name="1-open-hello-role-designer"></a>1. Hello 역할 디자이너를 열으십시오
* 두 번 클릭 하거나 클라우드 서비스 역할 tooopen 역할 디자이너를 마우스 오른쪽 단추로 클릭

![역할 디자이너 열기][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a>2. 진단 섹션에 새 확인란 "프로젝트에서 저장소 키 암호를 제거하지 마세요."가 추가됨
* Hello 로컬 저장소 에뮬레이터를 사용 하는 경우이 확인란을 사용할 수 없습니다. UseDevelopmentStorage hello 로컬 연결 문자열에 대 한 비밀 toomanage 없습니다는 = true입니다.

![로컬 저장소 에뮬레이터 연결 문자열은 암호가 아님][1]

* 새 프로젝트를 만드는 경우 기본적으로 이 확인란이 선택되지 않습니다. 이 인해 선택 된 hello 저장소 연결 문자열을 토큰으로 대체 될의 hello 저장소 키 섹션. hello hello 토큰의 값 섹션 hello 현재 사용자의 로밍 하는 응용 프로그램 데이터 폴더 아래 예를 들어: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService

> Note hello user\AppData 폴더에 대 한 액세스 제어 기능을 통해 사용자 로그인은와 안전한 곳 toostore 개발 비밀 것으로 간주 됩니다.
> 
> 

![저장소 키가 사용자 프로필 폴더에 저장됨][2]

### <a name="3-select-a-diagnostics-storage-account"></a>3. 진단 저장소 계정 선택
* Hello "..."를 클릭 하 여 시작 하는 hello 대화 상자에서 저장소 계정 선택 단추를 선택합니다. 어떻게 생성 된 hello 저장소 연결 문자열 체계가 없습니다 hello 저장소 계정 키를 확인 합니다.
* 예: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)

### <a name="4----debugging-hello-project"></a>4.    Hello 프로젝트 디버깅
* F5 toostart Visual Studio에서 디버깅 합니다. 모든 항목에서 작동 해야 hello 동일한 방식으로 이전 처럼 합니다.
  ![로컬로 디버그 시작][3]

### <a name="5-publish-project-from-visual-studio"></a>5. Visual Studio에서 프로젝트 게시
* 시작 hello 게시 대화 상자 및 로그인 지침 toopublish hello applicaion tooAzure 진행 합니다.

### <a name="6-additional-information"></a>6. 추가 정보
> 참고: hello 역할 디자이너에서 hello 설정 패널에 지금은 있는 그대로 유지 됩니다. 진단에 대 한 toouse hello 암호 관리 기능을 원하는 경우 toohello 구성 탭으로 이동 합니다.
> 
> 

![설정 추가][4]

> 참고: 사용 하도록 설정 하는 경우 일반 텍스트로 hello Application Insights 키 저장 됩니다. 중요 한 데이터 손상 될 위험에 노출 되도록 업로드 내용에 대 한 hello 키만 사용 됩니다.
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a>Visual Studio Online 작업 템플릿을 사용하여 클라우드 서비스 프로젝트 빌드 및 게시
* 단계를 수행 하는 hello에서는 어떻게 toosetup 클라우드 서비스에 대 한 연속 통합 프로젝트 Visual Studio 온라인 작업을 사용 하 여:
  ### <a name="1----obtain-a-vso-account"></a>1.    VSO 계정 얻기
* [Visual Studio Online 계정을 만들] [ Create Visual Studio Online account] 없는 이미 있는 경우
* [팀 프로젝트 만들기] [ Create team project] Visual Studio online 계정에서

### <a name="2----setup-source-control-in-visual-studio"></a>2.    Visual Studio에서 소스 제어 설정
* Tooa 팀 프로젝트 연결

![Tooteam 프로젝트 연결][5]

![팀 프로젝트 tooconnect를 선택 합니다.][6]

* 프로젝트 toosource 컨트롤 추가

![프로젝트 toosource 컨트롤 추가][7]

![프로젝트 tooa 소스 제어 폴더 매핑][8]

* 팀 탐색기에서 프로젝트 체크 인

![체크 인 프로젝트 toosource 제어][9]

### <a name="3----configure-build-process"></a>3.    빌드 프로세스 구성
* Tooyour 팀 프로젝트를 찾아 새 빌드 프로세스 템플릿 추가

![새 빌드 추가][10]

* 빌드 작업 선택

![빌드 작업 추가][11]

![Visual Studio 빌드 작업 템플릿 선택][12]

* 빌드 작업 입력을 편집합니다. 매개 변수 tooyour에 따라 필요한 hello 빌드 지정 필요

![빌드 작업 구성][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* 빌드 변수를 구성합니다.

![빌드 변수를 구성합니다.][14]

* 추가 작업 tooupload 빌드 저장

![빌드 저장 위치 게시 작업 선택][15]

![빌드 저장 위치 게시 작업 구성][16]

* Hello 빌드 실행

![새 빌드 큐 대기][17]

![빌드 요약 보기][18]

* 결과 유사한 toobelow 표시는 hello 빌드에 성공 하는 경우

![빌드 결과][19]

### <a name="4----configure-release-process"></a>4.    릴리스 프로세스 구성
* 새 릴리스를 만듭니다.

![새 릴리스 만들기][20]

* Hello Azure 클라우드 서비스 배포 작업을 선택 합니다.

![Azure 클라우드 서비스 배포 작업 선택][21]

* 저장소 계정 키를 hello toosource 컨트롤을 선택 하지 않으면으로 진단 확장을 설정 하기 위한 toospecify hello에 대 한 비밀 키가 필요 합니다. Hello 확장 **새 서비스 만들기에 대 한 고급 옵션** 섹션 및 hello 편집 **진단 저장소 계정 키** 매개 변수 입력 합니다. 여러 줄의 hello 형식에 키-값 쌍의에이 입력 됩니다 **[RoleName]:$(StorageAccountKey)**

> 참고: 진단 저장소 계정이 동일한 구독 hello 클라우드 서비스 응용 프로그램을 게시할 hello, 하는 경우 키가 없는 tooenter hello hello 배포 작업 입력;에 구독에서 hello 배포 hello 저장소 정보를 프로그래밍 방식으로 얻이 됩니다.
> 
> 

![클라우드 서비스 배포 작업 구성][22]

* 사용 하 여 보안 저장소 키 변수 toosave를 빌드합니다. 암호로 변수 hello hello 오른쪽에 hello 잠금 아이콘을 클릭 toomask 변수 입력

![암호 빌드 변수에 저장소 키 저장][23]

* 릴리스를 만들고 프로젝트 tooAzure 배포

![새 릴리스 만들기][24]

## <a name="next-steps"></a>다음 단계
Azure 클라우드 서비스에 대 한 진단 확장 설정에 대 한 더 toolearn 보십시오 [PowerShell을 사용 하 여 Azure 클라우드 서비스에서 진단 사용][Enable diagnostics in Azure Cloud Services using PowerShell]

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
