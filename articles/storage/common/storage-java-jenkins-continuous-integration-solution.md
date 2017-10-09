---
title: "Jenkins 연속 통합 솔루션과 Azure 저장소 aaaUsing | Microsoft Docs"
description: "이 자습서에서는 어떻게 toouse hello Azure blob 서비스에 대 한 리포지토리 빌드 아티팩트 Jenkins 연속 통합 솔루션을 통해 만든으로 보여 줍니다."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f4e5ca75-f6cb-4f74-981b-2aa06bb8de45
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 853c0c6c028596b3057bdc1dbbc59a9415c0fb77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-jenkins-continuous-integration-solution"></a>Jenkins 연속 통합 솔루션과 함께 Azure 저장소 사용
## <a name="overview"></a>개요
hello 다음과 같은 정보가 사용 방법을 보여 주는 toouse Blob 저장소의 Jenkins 연속 통합 (CI) 솔루션을 통해 만든 빌드 아티팩트 리포지토리로 또는 toobe 다운로드 가능한 파일의 원본으로 빌드 프로세스에서 합니다. Hello 시나리오의 위치는 여러분의 것 (Java 또는 다른 언어로 사용) 하는 agile 개발 환경에서 코딩 하 하 고 빌드 연속 통합에 따라 실행 중인 빌드 아티팩트에 대 한 저장소를 사용 해야 할 수 있도록 예를 들어 고객을 다른 조직 구성원과 공유할 하거나 아카이브를 유지 관리 합니다. 다른 시나리오에 빌드 작업 자체가 hello의 일부 빌드 입력으로 다른 파일을 종속성 toodownload 예를 들어 요구 하는 경우입니다.

이 자습서에서 사용할 Azure 저장소 플러그 인 hello 사용할 수 있게 하는 Jenkins CI에 대 한 합니다.

## <a name="overview-of-jenkins"></a>Jenkins 개요
Jenkins 하면 연속 통합 tooeasily 자신의 코드 변경 내용을 통합 하 고 있는 개발자가 허용 하 여 소프트웨어 프로젝트의 빌드 생성 된 자동으로 하 고 자주 hello 개발자의 hello 생산성을 높이기. 빌드는 버전이 지정 하 고 빌드 아티팩트 업로드 toovarious 저장소 일 수 있습니다. 이 항목은 어떻게 toouse Azure blob 저장소의 hello 빌드 아티팩트 hello 저장소로 표시 됩니다. 어떻게 toodownload 종속성에서 Azure blob 저장소도 표시 됩니다.

Jenkins에 대한 자세한 내용은 [Meet Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)에서 찾을 수 있습니다.

## <a name="benefits-of-using-hello-blob-service"></a>Hello Blob 서비스 사용의 이점
Blob 서비스 toohost hello를 사용 하 여 agile 개발 빌드 아티팩트 이점입니다.

* 빌드 아티팩트 및/또는 다운로드 가능 종속성의 고가용성
* Jenkins CI 솔루션이 빌드 아티팩트를 업로드할 때의 성능
* 고객 및 파트너가 빌드 아티팩트를 다운로드할 때의 성능
* 익명 액세스, 만료 기반 공유 액세스 서명 액세스, 전용 액세스 중에서 선택하여 사용자 액세스 정책 제어

## <a name="prerequisites"></a>필수 조건
있습니다 됩니다 필요 hello toouse hello 다음 Blob 서비스와 Jenkins CI 솔루션:

* Jenkins 연속 통합 솔루션
  
    현재는 Jenkins CI 솔루션 없는 경우 다음 기술을 hello를 사용 하는 Jenkins CI 솔루션을 실행할 수 있습니다.
  
  1. Java를 사용할 수 있는 컴퓨터에서 <http://jenkins-ci.org>로부터 jenkins.war를 다운로드합니다.
  2. 열린된 toohello 폴더 jenkins.war 포함 된 명령 프롬프트에서 다음을 실행 합니다.
     
      `java -jar jenkins.war`

  3. 브라우저에서 `http://localhost:8080/`을(를) 엽니다. 이 hello Jenkins 대시보드가 열립니다 tooinstall를 사용 하 고 hello Azure 저장소 플러그 인을 구성 합니다.
     
      일반적인 Jenkins CI 솔루션 서비스로 toorun를 설정할 수는, hello Jenkins 전쟁 hello 명령줄에서 실행 수이 자습서에 대 한 충분 한.
* Azure 계정. <http://www.azure.com>에서 Azure 계정을 등록할 수 있습니다.
* Azure 저장소 계정. 저장소 계정이 없는 경우 하나를 만들 수 있습니다에 hello 단계를 사용 하 여 [저장소 계정 만들기](../common/storage-create-storage-account.md#create-a-storage-account)합니다.
* Hello Jenkins CI 솔루션에 익숙한 좋지만 필요 하지 않습니다, Jenkins CI에 대 한 hello Blob 서비스의 리포지토리로 사용 하는 경우 필요한 단계를 hello 기본 예제에서는 tooshow 빌드 아티팩트 hello 다음 콘텐츠는 사용 합니다.

## <a name="how-toouse-hello-blob-service-with-jenkins-ci"></a>어떻게 toouse hello Jenkins ci Blob 서비스
tooinstall 필요한 Jenkins와 toouse hello Blob 서비스, Azure 저장소 플러그 인 hello hello 플러그 인 toouse 저장소 계정의 구성 하 고 다음 빌드 아티팩트 tooyour 저장소 계정에 업로드 하는 빌드 후 작업을 만듭니다. 이 단계는 hello 다음 섹션에서에서 설명 합니다.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>어떻게 tooinstall hello Azure 저장소 플러그 인
1. Hello Jenkins 대시보드 내에서 클릭 **관리 Jenkins**합니다.
2. Hello에 **관리 Jenkins** 페이지 **플러그 인 관리**합니다.
3. Hello 클릭 **사용 가능** 탭 합니다.
4. Hello에 **아티팩트 Uploaders** 확인 섹션 **Microsoft Azure Storage 플러그 인**합니다.
5. **Install without restart** 또는 **Download now and install after restart**를 클릭합니다.
6. Jenkins를 다시 시작합니다.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>어떻게 tooconfigure hello Azure 저장소 플러그 인 toouse 저장소 계정
1. Hello Jenkins 대시보드 내에서 클릭 **관리 Jenkins**합니다.
2. Hello에 **관리 Jenkins** 페이지 **시스템 구성**합니다.
3. Hello에 **Microsoft Azure 저장소 계정 구성** 섹션:
   1. Hello에서 구할 수 있는 사용자 저장소 계정 이름을 입력 [Azure 포털](https://portal.azure.com)합니다.
   2. 또한 hello에서 얻을 수 있는 저장소 계정 키를 입력 [Azure 포털](https://portal.azure.com)합니다.
   3. Hello에 대 한 기본값을 사용 하 여 **Blob 서비스 끝점 URL** hello 공용 Azure 클라우드를 사용 하는 경우. 다른 Azure 클라우드를 사용 하는 경우에 지정 된 hello로 hello 끝점을 사용 [Azure 포털](https://portal.azure.com) 저장소 계정에 대 한 합니다. 
   4. 클릭 **저장소 자격 증명의 유효성을 검사** toovalidate 저장소 계정입니다. 
   5. [선택 사항] 처리 된 사용 가능한 tooyour Jenkins CI를 지정 하는 추가 저장소 계정이 있는 경우 클릭 **저장소 계정을 추가**합니다.
   6. 클릭 **저장** toosave 설정 합니다.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>어떻게 toocreate 빌드 아티팩트 tooyour 저장소 계정에 업로드 하는 빌드 후 작업을
명령에서는 먼저 해야 toocreate 작업을 여러 개의 파일을 만들고 hello 빌드 후 작업 tooupload hello 파일 tooyour 저장소 계정에 추가 됩니다.

1. Hello Jenkins 대시보드 내에서 클릭 **새 항목**합니다.
2. 이름 hello 작업 **MyJob**, 클릭 **자유 스타일 소프트웨어 프로젝트를 빌드하**, 클릭 하 고 **확인**합니다.
3. Hello에 **빌드** 섹션 hello 작업 구성의 클릭 **추가 빌드 단계** 선택 **Windows 실행 일괄 처리 명령이**합니다.
4. **명령**, hello 다음 명령을 사용 하 여:

    ```   
    md text
    cd text
    echo Hello Azure Storage from Jenkins > hello.txt
    date /t > date.txt
    time /t >> date.txt
    ```

5. Hello에 **빌드 후 작업** 섹션 hello 작업 구성의 클릭 **빌드 후 작업을 추가** 선택 **아티팩트 tooAzure Blob 저장소에 업로드**합니다.
6. 에 대 한 **저장소 계정 이름**, 저장소 계정 toouse를 hello 선택 합니다.
7. 에 대 한 **컨테이너 이름을**, hello 컨테이너 이름을 지정 합니다. (hello 컨테이너가 만들어집니다 이미 없는 hello 빌드 아티팩트를 업로드 하는 경우.) 따라서이 예에서는 입력, 환경 변수를 사용할 수 있습니다 **${JOB_NAME}** hello 컨테이너 이름으로 합니다.
   
    **팁**
   
    Hello 아래 **명령** 섹션에 대 한 스크립트를 입력 한 **Windows 실행 일괄 처리 명령이** toohello 환경 변수 Jenkins에서 인식 되는 링크입니다. 해당 링크 toolearn hello 환경 변수 이름 및 설명을 클릭 합니다. 해당 환경에 유의 hello 등의 특수 문자를 포함 하는 변수 **BUILD_URL** 환경 변수를 컨테이너 이름 또는 공용 가상 경로 허용 되지 않습니다.
8. 이 예의 경우 **Make new container public by default** 를 클릭합니다. (Toouse 개인 컨테이너를 사용 하도록 하려는 경우 필요 함 toocreate 공유 액세스 서명 tooallow 액세스 합니다. 이 항목의 hello 범위를 벗어납니다. [SAS(공유 액세스 서명) 사용](../storage-dotnet-shared-access-signature-part-1.md)에서 공유 액세스 서명에 대한 자세한 내용을 알아볼 수 있습니다.)
9. [선택 사항] 클릭 **업로드 하기 전에 정리 컨테이너** 빌드 아티팩트 업로드할지 hello 컨테이너 toobe 내용의 삭제 하려는 경우 (그대로 선택 되지 않은 hello 컨테이너의 tooclean hello 내용을 하지 않을 경우).
10. 에 대 한 **아티팩트 목록 tooupload**, 입력  **텍스트 /*.txt** 합니다.
11. **Common virtual path for uploaded artifacts**에는 이 자습서에서 사용할 **${BUILD\_ID}/${BUILD\_NUMBER}**를 입력합니다.
12. 클릭 **저장** toosave 설정 합니다.
13. Hello Jenkins 대시보드 클릭 **이제 빌드** toorun **MyJob**합니다. 상태에 대 한 hello 콘솔 출력을 검사 합니다. Azure 저장소에 대 한 상태 메시지 hello 빌드 후 작업 tooupload 빌드 아티팩트를 시작할 때 hello 콘솔 출력에 포함 됩니다.
14. Hello 작업을 성공적으로 완료 되 면 hello 공용 blob을 열어 hello 빌드 아티팩트를 검사할 수 있습니다.
    1. 로그인 toohello [Azure 포털](https://portal.azure.com)합니다.
    2. **저장소**를 클릭합니다.
    3. Jenkins에 사용한 hello 저장소 계정 이름을 클릭 합니다.
    4. **컨테이너**를 클릭합니다.
    5. 라는 hello 컨테이너 클릭 **myjob**, hello hello Jenkins 작업을 만들 때 할당 된 hello 작업의 소문자 버전입니다. 컨테이너 이름 및 Blob 이름은 Azure 저장소에서 소문자(및 대/소문자 구분)입니다. Hello 라는 hello 컨테이너에 대 한 blob 목록 내에서 **myjob** 표시 되어야 **hello.txt** 및 **date.txt**합니다. 이들이 항목 중 하나에 대 한 hello URL을 복사 하 고 브라우저에서 엽니다. 빌드 아티팩트로 업로드 된 hello 텍스트 파일에 표시 됩니다.

작업당 아티팩트 tooAzure blob 저장소에 업로드 하는 빌드 후 작업을 하나만 만들 수 있습니다. 다른 파일 (와일드 카드 포함) 및 내에서 경로 toofiles hello 빌드 후 작업을 단일 tooupload 아티팩트 tooAzure blob 저장소를 지정할 수 **아티팩트 목록 tooupload** 구분 기호로 세미콜론을 사용 하 여 합니다. 프로그램 Jenkins 빌드 JAR 파일 및 프로그램 작업 영역에 TXT 파일 생성 하는 예를 들어 **빌드** 을 원하는 tooupload 모두 tooAzure blob 저장소, hello에 대 한 hello 다음 이름을 사용해 서 **아티팩트 목록 tooupload** 값: **빌드 /\*.jar; 빌드 /\*.txt**합니다. 또한 이중 콜론 구문 toospecify hello blob 이름 내에서 경로 toouse를 사용할 수 있습니다. 예를 들어, 사용 하 여 업로드 하는 hello Jar tooget **바이너리** hello blob 경로 hello TXT 파일 tooget에서 사용 하 여 업로드 **통지** hello blob 경로 사용 하 여 hello 다음 hello에 대 한  **아티팩트 tooupload 목록은** 값: **빌드 /\*. jar::binaries; 빌드 /\*. txt::notices**합니다.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>어떻게 toocreate 빌드 단계는에서 다운로드 Azure blob 저장소
단계를 수행 하는 hello tooconfigure 빌드 Azure blob 저장소에서 toodownload 항목을 실행 하는 방법을 보여 줍니다. 이 방법이 유용 tooinclude 항목에 빌드 하려는 경우 예를 들어 Azure에서 유지 하는 Jar blob 저장소입니다.

1. Hello에 **빌드** 섹션 hello 작업 구성의 클릭 **추가 빌드 단계** 선택 **Azure Blob 저장소에서 다운로드**합니다.
2. 에 대 한 **저장소 계정 이름**, 저장소 계정 toouse를 hello 선택 합니다.
3. 에 대 한 **컨테이너 이름을**, toodownload 원하는 hello blob hello 컨테이너의 hello 이름을 지정 합니다. 환경 변수를 사용할 수 있습니다.
4. 에 대 한 **Blob 이름**, hello blob 이름을 지정 합니다. 환경 변수를 사용할 수 있습니다. 또한는 별표를 와일드 카드로 hello blob 이름의 hello 초기 문자를 지정한 후에 사용할 수 있습니다. 예를 들어 **project\*** 는 이름이 **project** 로 시작하는 모든 Blob을 지정합니다.
5. [선택 사항] 에 대 한 **다운로드 경로**, Azure blob 저장소에서 toodownload 파일을 저장할 hello Jenkins 머신에서 hello 경로 지정 합니다. 환경 변수도 사용할 수 있습니다. (에 대 한 값을 제공 하지 않으면 **다운로드 경로**, hello 파일에 Azure blob 저장소에서 다운로드 한 toohello 작업의 작업 영역을 수 있습니다.)

Azure blob 저장소에서 toodownload를 원하는 다른 항목을 설정한 경우에 추가 빌드 단계를 만들 수 있습니다.

빌드를 실행 한 후에 hello 기록 콘솔 출력 빌드하거나 toosee는 다운로드 위치에 성공적으로 다운로드 되었는지 예상 blob를 hello 여부를 확인할 수 있습니다.  

## <a name="components-used-by-hello-blob-service"></a>Hello Blob 서비스에서 사용 하는 구성 요소
hello 다음 hello Blob 서비스 구성 요소에 대 한 개요를 제공합니다.

* **저장소 계정**: 저장소 계정을 통해 모든 액세스 tooAzure 저장소 작업은 수행 됩니다. Blob에 액세스 하기 위한 hello 네임 스페이스의 hello 가장 높은 수준입니다. 전체 크기가 100TB를 초과하지 않을 경우 한 계정에 포함될 수 있는 컨테이너 수는 제한이 없습니다.
* **컨테이너**: 컨테이너는 Blob 집합 그룹화를 제공합니다. 모든 Blob은 컨테이너에 있어야 합니다. 한 계정에 포함될 수 있는 컨테이너 수에는 제한이 없습니다. 한 컨테이너에 저장될 수 있는 Blob 수에도 제한이 없습니다.
* **Blob**: 모든 형식과 크기의 파일입니다. Azure Blob 저장소 서비스에 저장할 수 있는 Blob 유형에는 블록과 페이지 Blob 두 가지가 있습니다. 대부분의 파일은 블록 Blob입니다. 단일 블록 blob의 크기는 too200GB 될 수 있습니다. 이 자습서에서는 블록 Blob을 사용합니다. 페이지 blob이 blob 유형이 든 다른 파일의 바이트 범위가 자주 수정 될 때 크기 및은 더 효율적인 too1TB 될 수 있습니다. Blob에 대한 자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.
* **URL 형식**: Blob에는 주소 지정 가능한 URL 형식에 따라 hello를 사용 하 여:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (위의 hello 형식을 toohello 공용 Azure 클라우드를 적용 하는 데 사용 합니다. 다른 Azure 클라우드를 사용 하는 경우 hello 내 hello 끝점을 사용 [Azure 포털](https://portal.azure.com) toodetermine URL 끝점입니다.)
  
    위의 hello 형태로 `storageaccount` 나타냅니다 hello 저장소 계정의 이름을 `container_name` 나타냅니다 hello에 컨테이너의 이름 및 `blob_name` 나타냅니다 hello에 blob의 이름은 각각. Hello 컨테이너 이름으로 전달 슬래시로 구분 된 여러 경로가 있을 수 있습니다  **/** 합니다. 이 자습서에서는 예제 컨테이너 이름이 hello **MyJob**, 및 **${빌드\_ID} / ${빌드\_수}** hello 공용 가상 경로에 hello blob 것에 사용한는 Hello 다음 폼의 URL:
  
    `http://example.blob.core.windows.net/myjob/2014-04-14_23-57-00/1/hello.txt`

## <a name="next-steps"></a>다음 단계
* [Meet Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)
* [Java용 Azure 저장소 SDK](https://github.com/azure/azure-storage-java)
* [Azure 저장소 클라이언트 SDK 참조](http://dl.windowsazure.com/storage/javadoc/)
* [Azure Storage 서비스 REST API](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Azure 저장소 팀 블로그](http://blogs.msdn.com/b/windowsazurestorage/)

자세한 내용은 [Java 개발자용 Azure](/java/azure)를 방문하세요.