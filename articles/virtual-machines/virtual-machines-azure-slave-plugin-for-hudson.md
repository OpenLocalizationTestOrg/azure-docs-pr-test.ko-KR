---
title: "aaaHow toouse hello Azure 슬레이브는 Hudson 연속 통합 플러그 인 | Microsoft Docs"
description: "Toouse hello Azure 슬레이브는 Hudson 연속 통합 플러그 인 방법을 설명 합니다."
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a>어떻게 toouse hello Azure 슬레이브는 Hudson 연속 통합 플러그 인
hello Azure 슬레이브 Hudson에 대 한 플러그 인 사용 하면 tooprovision 슬레이브 노드를 Azure 배포를 실행 하는 경우.

## <a name="install-hello-azure-slave-plug-in"></a>Hello Azure 종속 플러그 인 설치
1. Hello Hudson 대시보드, 클릭 **관리 Hudson**합니다.
2. Hello에 **관리 Hudson** 페이지에서 클릭 **플러그 인 관리**합니다.
3. Hello 클릭 **사용 가능** 탭 합니다.
4. 클릭 **검색** 유형과 **Azure** toolimit hello 목록 toorelevant 플러그 인 합니다.
   
    사용 가능한 플러그 인의 hello 목록을 통해 tooscroll를 선택 하면 볼 수 있습니다 hello Azure 슬레이브 hello에서 플러그 인 **클러스터 관리 및 빌드 Distributed** hello에 대 한 섹션 **다른** 탭 합니다.
5. 에 대 한 hello 확인란 선택 **Azure 종속 플러그 인**합니다.
6. **Install**을 클릭합니다.
7. Hudson을 다시 시작합니다.

이제 해당 hello 플러그 인 설치 된 hello 다음 단계는 Azure 구독 프로필 및 toocreate hello 슬레이브 노드에 대 한 hello VM 만들기에 사용 되는 템플릿 사용 하 여 플러그 인 tooconfigure hello 것입니다.

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a>구독 프로필을 사용 하 여 hello Azure 종속 플러그 인 구성
구독 프로필도 참조 tooas 게시 설정는 보안 자격 증명 및 개발 환경에서 Azure와 toowork 해야 하는 몇 가지 추가 정보를 포함 하는 XML 파일입니다. tooconfigure hello Azure 종속 플러그 인, 해야합니다.

* 구독 ID
* 구독에 대한 관리 인증서

이러한 항목은 [구독 프로필]에 나와 있습니다. 다음은 구독 프로필의 예입니다.

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

구독 프로필을 만든 후 이러한 단계 tooconfigure hello Azure 종속 플러그 인을 수행 합니다.

1. Hello Hudson 대시보드, 클릭 **관리 Hudson**합니다.
2. **Configure System**을 클릭합니다.
3. Hello 페이지 toofind hello 아래로 스크롤하여 **클라우드** 섹션.
4. **Add new cloud > Microsoft Azure**를 클릭합니다.
   
    ![새 클라우드 추가][add new cloud]
   
    구독 정보 tooenter 해야 하는 hello 필드가 표시 됩니다.
   
    ![프로필 구성][configure profile]
5. 구독 프로필에서 hello 구독 id 및 관리 인증서를 복사한 hello 적절 한 필드에 붙여 넣습니다.
   
    Hello 구독 id 및 관리 인증서를 복사 하는 경우 **없는** hello 값을 포함 하는 hello 따옴표를 포함 합니다.
6. **Verify configuration**을 클릭합니다.
7. Hello 구성을 성공적으로 확인 하 고, 클릭 **저장**합니다.

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a>가상 컴퓨터 템플릿을 Azure 슬레이브 hello에 대 한 플러그 인 설정
Hello 매개 변수를 정의 하는 가상 컴퓨터 템플릿은 플러그 인 hello Azure에 toocreate 종속 노드를 사용 합니다. 단계를 수행 하는 hello에서 Ubuntu VM에 대 한 템플릿을 만드는 것입니다.

1. Hello Hudson 대시보드, 클릭 **관리 Hudson**합니다.
2. **Configure System**을 클릭합니다.
3. Hello 페이지 toofind hello 아래로 스크롤하여 **클라우드** 섹션.
4. Hello 내 **클라우드** 섹션에서 찾을 **Azure 가상 컴퓨터 템플릿을 추가** hello 클릭 **추가** 단추입니다.
   
    ![VM 템플릿 추가][add vm template]
5. Hello에 클라우드 서비스 이름을 지정 **이름** 필드입니다. Tooan 기존 클라우드 서비스를 참조 하는 hello 이름을 지정 하는 경우 해당 서비스에 VM hello는 프로 비전 됩니다. 그렇지 않은 경우 Azure는 새로운 서비스를 만듭니다.
6. Hello에 **설명** 필드에, 만들고 있는 hello 템플릿을 설명 하는 텍스트를 입력 합니다. 이 정보는 설명 목적이며 VM 프로비저닝에는 사용되지 않습니다.
7. Hello에 **레이블을** 필드에, 입력 **linux**합니다. 이 레이블은 사용 되는 tooidentify hello 템플릿을 만들면 이며 Hudson 작업을 만들 때 사용 되는 이후에 tooreference hello 서식 파일입니다.
8. Hello VM 만들어지는 지역을 선택 합니다.
9. Hello 적절 한 VM 크기를 선택 합니다.
10. 저장소 계정을 hello VM을 만들 위치를 지정 합니다. Hello을 반드시 사용 하고자 하는 hello 클라우드 서비스와 동일한 지역입니다. 새 저장소 toobe 생성 하려는 경우이 필드를 비워 둘 수 있습니다.
11. 보존 시간 (분) Hudson 유휴 슬레이브를 삭제 하기 전에 hello 번호를 지정 합니다. Hello 기본값 60이 그대로 둡니다.
12. **사용**, 선택이 슬레이브 노드 사용 될 때 적절 한 조건 hello 합니다. 지금은 **Utilize this node as much as possible**을 선택합니다.
    
     이 시점에서 폼와 어느 정도 비슷한 toothis 형태가 됩니다.
    
     ![템플릿 구성][template config]
13. **이미지 제품군 또는 Id** toospecify 있는 어떤 시스템 이미지를 VM에 설치 됩니다. 이미지 제품군 목록에서 선택하거나 사용자 지정 이미지를 지정할 수 있습니다.
    
     Tooselect 이미지 제품군의 목록에서 hello 이름의 첫 문자 (대/소문자 구분) hello 이미지 패밀리를 입력 합니다. 예를 들어 **U** 를 입력하면 Ubuntu Server 제품군 목록이 표시됩니다. Hello 목록에서 선택 되 면 VM을 프로 비전 할 때 Jenkins hello 해당 시스템 이미지 해당 제품군에서의 최신 버전을 사용 합니다.
    
     ![OS 제품군 목록][OS family list]
    
     대신 toouse 원하는 사용자 지정 이미지를 사용 하도록 설정한 경우 해당 사용자 지정 이미지 hello 이름을 입력 합니다. 사용자 지정 이미지 이름이 표시 되지 않습니다는 목록에 없으므로 이름 hello tooensure을 올바르게 입력.    
    
     이 자습서에 대 한 입력 **U** Ubuntu 이미지 및 선택 목록을 toobring **Ubuntu Server 14.04 LTS**합니다.
14. **Launch method**에 대해서는 **SSH**를 선택합니다.
15. Hello에서 아래 hello 스크립트를 복사 및 붙여넣기 **Init 스크립트** 필드입니다.
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     hello **Init 스크립트** hello VM이 생성 후에 실행 됩니다. 이 예제에서는 hello 스크립트 Java, git, 및 ant를 설치합니다.
16. Hello에 **Username** 및 **암호** 필드를 VM에 만들어지는 hello 관리자 계정에 대 한 기본 설정된 값을 입력 합니다.
17. 클릭 **확인 템플릿** toocheck 지정한 hello 매개 변수는 유효 하는 경우.
18. **Save**를 클릭합니다.

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a>Azure의 슬레이브 노드에서 실행되는 Hudson 작업 만들기
이 섹션에서는 Azure의 슬레이브 노드에서 실행할 Hudson 작업을 만듭니다.

1. Hello Hudson 대시보드, 클릭 **새 작업**합니다.
2. 만들려는 hello 작업에 대 한 이름을 입력 합니다.
3. Hello 작업 유형에 대 한 선택 **빌드 자유 스타일 소프트웨어 작업**합니다.
4. **확인**을 클릭합니다.
5. Hello 작업 구성 페이지에서 선택 **이 프로젝트를 실행할 수 있는 제한**합니다.
6. 선택 **노드 및 레이블 메뉴** 선택 **linux** (지정이 레이블은 hello 이전 단원의 hello 가상 컴퓨터 템플릿을 만들 때).
7. Hello에 **빌드** 섹션에서 클릭 **추가 빌드 단계** 선택 **셸 실행**합니다.
8. 다음 스크립트, 대체 hello 편집 **{github 계정 이름은}**, **{project name}**, 및 **{프로젝트 디렉터리}** 와 적절 한 값을 복사한 hello 표시 되는 hello 텍스트 영역에는 스크립트를 편집 합니다.
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. **Save**를 클릭합니다.
10. 에 Hudson 대시보드 hello, 방금 만든 hello 작업을 찾 및 hello 클릭 **빌드를 예약** 아이콘입니다.

Hudson은 hello 이전 섹션에서 만든 hello 템플릿을 사용 하 여 종속 노드 만들기 및이 작업에 대 한 hello 빌드 단계에서 지정한 hello 스크립트 실행 됩니다.

## <a name="next-steps"></a>다음 단계
Java와 함께 Azure 사용에 대 한 자세한 내용은 참조 hello [Azure Java 개발자 센터]합니다.

<!-- URL List -->

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[구독 프로필]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

