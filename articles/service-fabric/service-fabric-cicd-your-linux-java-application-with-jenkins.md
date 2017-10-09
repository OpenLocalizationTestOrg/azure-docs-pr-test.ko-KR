---
title: "aaaContinuous 빌드 및 Jenkins를 사용 하 여 Azure 서비스 패브릭 Linux Java 응용 프로그램에 대 한 통합 | Microsoft Docs"
description: "Jenkins를 사용하여 Linux Java 응용 프로그램 연속 빌드 및 통합"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Jenkins toobuild를 사용 하 고 Linux Java 응용 프로그램 배포
Jenkins는 앱의 연속 통합 및 배포를 위한 인기 있는 도구입니다. 다음은 어떻게 toobuild Jenkins를 사용 하 여 Azure 서비스 패브릭 응용 프로그램을 배포 합니다.

## <a name="general-prerequisites"></a>일반 필수 조건
- 로컬로 설치된 Git가 있어야 합니다. Hello에서 적절 한 Git 버전을 설치할 수 있습니다 [hello Git 다운로드 페이지](https://git-scm.com/downloads)운영 체제에 따라 합니다. 새 tooGit 인 경우에서 자세한 내용을 알아볼 항목에 대 한 hello [Git 설명서](https://git-scm.com/docs)합니다.
- 서비스 패브릭 Jenkins 플러그 인 hello가 편리 합니다. [Service Fabric 다운로드](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi)에서 다운로드할 수 있습니다.

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Service Fabric 클러스터 내에서 Jenkins 설정

Service Fabric 클러스터 내부 또는 외부에서 Jenkins를 설정할 수 있습니다. hello 다음 섹션 표시 방법을 tooset 후 Azure 저장소를 사용 하는 동안 클러스터 내부의 계정 hello 컨테이너 인스턴스의 toosave hello 상태입니다.

### <a name="prerequisites"></a>필수 조건
1. Service Fabric Linux 클러스터를 준비합니다. 이미 hello Azure 포털에서에서 만든 서비스 패브릭 클러스터에 Docker가 설치 된 있습니다. Hello 클러스터를 로컬로 실행 중인 경우 hello 명령을 사용 하 여 Docker가 설치 되었는지 확인 ``docker info``합니다. 그에 따라을 사용 하 여 설치 되지 않은 경우 설치 다음 명령을 hello:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Hello 서비스 패브릭 컨테이너 응용 프로그램을 단계를 수행 하는 hello를 사용 하 여 hello 클러스터에 배포 했습니다.

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. Hello 필요한 toopersist hello 상태의 hello Jenkins 컨테이너 인스턴스를 원하는 hello Azure 저장소 파일 공유의 옵션 세부 정보를 연결 합니다. Hello에 대 한 hello Microsoft Azure 포털을 사용 하는 경우 동일 하십시오 hello 단계에 따라-예를 들어 Azure 저장소 계정을 만들고 ``sfjenkinsstorage1``합니다. ``sfjenkins``라는 저장소 계정 아래 **파일 공유**를 만듭니다. 클릭 **연결** hello 파일 공유 및 참고 hello 값을 표시 합니다. 아래에 대 한 **Linux에서 연결**, 예를 들어이 다음과 같은 다음과 같습니다.
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Hello hello 자리 표시자 값을 업데이트 ```setupentrypoint.sh``` 해당 azure 저장소 세부 정보를 사용 하 여 스크립트입니다.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
대체 ``[REMOTE_FILE_SHARE_LOCATION]`` hello 값을 가진 ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` hello의 hello 출력에서 위의 3 지점에 연결 합니다.
대체 ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` hello 값을 가진 ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` 위의 3 지 점으로부터 합니다.

5. Toohello 클러스터에 연결 하 고 hello 컨테이너 응용 프로그램을 설치 합니다.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
이렇게 Jenkins 컨테이너 hello 클러스터에 설치 되 고 hello 서비스 패브릭 탐색기를 사용 하 여 모니터링할 수 있습니다.

### <a name="steps"></a>단계
1. 브라우저에서 이동 너무``http://PublicIPorFQDN:8081``합니다. 초기 관리자 암호 필요 toosign hello의 hello 경로 제공합니다. 관리자 권한으로 toouse Jenkins를 계속할 수 있습니다. 또는 만들고 hello 초기 관리자 계정으로 로그인 한 후 hello 사용자를 변경할 수 있습니다.

   > [!NOTE]
   > Hello 클러스터를 만드는 동안 hello 8081 포트 hello 응용 프로그램 끝점 포트도 지정 했는지 확인 합니다.
   >

2. 사용 하 여 hello 컨테이너 인스턴스 ID를 가져올 ``docker ps -a``합니다.
3. Toohello 컨테이너에서 SSH 로그인을 보안 하 고 hello Jenkins 포털에 표시 된 hello 경로 붙여 넣습니다. 예를 들어, hello 경로 hello 포털에 표시 되는 경우 `PATH_TO_INITIAL_ADMIN_PASSWORD`, hello 다음 실행:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Jenkins와 GitHub toowork에 언급 된 hello 단계를 사용 하 여 설정 [새 SSH 키를 생성 하 고 toohello SSH 에이전트 추가](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)합니다.
    * GitHub toogenerate hello SSH 키 및 tooadd hello SSH 키 toohello 저장소를 호스팅하는 GitHub 계정에서 제공 하는 hello 지침을 사용 합니다.
    * Hello hello Jenkins Docker 셸 (및 호스트에 없는) 링크를 앞에서 언급 한 hello 명령을 실행 합니다.
    * 호스트에서 다음 명령을 사용 하 여 hello Jenkins 셸 toohello에 toosign:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Service Fabric 클러스터 외부에서 Jenkins 설정

Service Fabric 클러스터 내부 또는 외부에서 Jenkins를 설정할 수 있습니다. 섹션 표시 방법을 따르는 hello tooset 클러스터 외부을 것입니다.

### <a name="prerequisites"></a>필수 조건
Docker가 설치 된 toohave가 필요 합니다. 다음 명령은 hello 터미널 hello에서 사용 되는 tooinstall Docker 될 수 있습니다.

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

이렇게 하면 실행할 때 ``docker info`` hello 터미널, 표시 되어야 hello 출력에서 해당 hello Docker 서비스를 실행 합니다.

### <a name="steps"></a>단계
  1. 끌어오기 hello 서비스 패브릭 Jenkins 컨테이너 이미지:``docker pull raunakpandya/jenkins:v1``
  2. Hello 컨테이너 이미지를 실행 합니다.``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Hello 컨테이너 이미지 인스턴스의 hello ID를 가져옵니다. Hello 명령 사용 하 여 모든 hello Docker 컨테이너를 나열할 수 있습니다.``docker ps –a``
  4. 단계를 수행 하는 hello를 사용 하 여 Jenkins 포털 toohello에 로그인 합니다.

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    컨테이너 ID가 2d24a73b5964이면 2d24를 사용합니다.
    * 이 암호는 toohello Jenkins 대시보드는 포털에서 로그인에 대 한 필요``http://<HOST-IP>:8080``
    * 로그인 한 후 hello에 대 한 처음으로, 사용자 고유의 사용자 계정을 만들고 이후 목적으로 사용할 수 있습니다 또는 toouse hello 관리자 계정을 계속 수 있습니다. 사용자를 만든 후 해당 toocontinue를 해야 합니다.
  5. Jenkins와 GitHub toowork에 언급 된 hello 단계를 사용 하 여 설정 [새 SSH 키를 생성 하 고 toohello SSH 에이전트 추가](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)합니다.
        * GitHub toogenerate hello SSH 키 및 tooadd hello SSH 키 toohello hello 저장소를 호스팅하는 GitHub 계정에서 제공 하는 hello 지침을 사용 합니다.
        * Hello hello Jenkins Docker 셸 (및 호스트에 없는) 링크를 앞에서 언급 한 hello 명령을 실행 합니다.
      * 호스트에서 다음 명령을 사용 하 여 hello Jenkins 셸 toohello에 toosign:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

해당 hello 클러스터 또는 hello Jenkins 컨테이너 이미지는 호스트의 공용 IP가 있는 컴퓨터를 확인 합니다. 그러면 GitHub에서 hello Jenkins 인스턴스 tooreceive 알림.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>서비스 패브릭 Jenkins 플러그 인 hello hello 포털에서 설치

1. 너무 이동``http://PublicIPorFQDN:8081``
2. Hello Jenkins 대시보드에서 선택 **관리 Jenkins** > **플러그 인 관리** > **고급**합니다.
여기에서는 플러그 인을 업로드할 수 있습니다. 선택 **파일 선택**를 선택한 후 hello **serviceFabric.hpi** 필수 구성 요소에서 다운로드 한 파일입니다. 선택 하는 경우 **업로드**을 Jenkins hello 플러그 인을 자동으로 설치 합니다. 요청된 경우 다시 시작을 허용합니다.

## <a name="create-and-configure-a-jenkins-job"></a>Jenkins 작업 만들기 및 구성

1. 대시보드에서 **새 항목**을 만듭니다.
2. 항목 이름을 입력합니다(예: **MyJob**). **자유로운 프로젝트**를 선택하고 **확인**을 클릭합니다.
3. Hello 작업 페이지를 이동 하 고 클릭 **구성**합니다.

   a. Hello 일반 섹션의에서 **GitHub 프로젝트**, GitHub 프로젝트 URL을 지정 합니다. 이 URL 호스트 hello 서비스 패브릭 Java 응용 프로그램 Jenkins 연속 통합 hello로 toointegrate 원하는 연속 배포 (CI/CD) 흐름 (예를 들어 ``https://github.com/sayantancs/SFJenkins``).

   b. Hello에서 **소스 코드 관리** 섹션에서 **Git**합니다. Jenkins CI/CD 흐름 hello로 toointegrate 원하는 hello 서비스 패브릭 Java 응용 프로그램을 호스팅하는 hello 리포지토리 URL을 지정 (예를 들어 ``https://github.com/sayantancs/SFJenkins.git``). 또한 지정할 수 있습니다 여기는 분기 toobuild (예를 들어 **/마스터**).
4. 구성 프로그램 *GitHub* (를 호스팅하는 hello 리포지토리) 수 tootalk tooJenkins 되도록 합니다. 단계를 수행 하는 hello를 사용 합니다.

   a. Tooyour GitHub 리포지토리 페이지로 이동 합니다. 너무 이동**설정** > **통합 및 서비스**합니다.

   b. 선택 **서비스 추가**, 형식 **Jenkins**, 및 select hello **Jenkins GitHub 플러그**합니다.

   c. Jenkins Webhook URL을 입력합니다(기본적으로 ``http://<PublicIPorFQDN>:8081/github-webhook/``이여야 함). **서비스 추가/업데이트**를 클릭합니다.

   d. 테스트 이벤트 tooyour Jenkins 인스턴스에 전송 됩니다. 프로젝트를 빌드하기 및 github를 hello webhook 하면 녹색 확인 표시를 볼 해야 합니다.

   e. Hello에서 **빌드 트리거** 섹션에서 원하는 옵션을 선택 하는 빌드를 선택 합니다. 이 예에서는 원하는 tootrigger 빌드 일부 푸시 toohello 리포지토리 발생할 때마다 합니다. 따라서 **GITScm 폴링에 대한 GitHub 후크 트리거**를 선택합니다. (이 옵션을 이전에 호출한 **변경 tooGitHub 푸시 될 때 빌드**.)

   f. Hello에서 **섹션 빌드**, hello 드롭다운 목록에서 **추가 빌드 단계**, hello 옵션을 선택 **Gradle 스크립트 호출**합니다. 제공 된 hello 위젯에서 hello 경로 지정 너무**루트 빌드 스크립트** 응용 프로그램에 대 한 합니다. 지정 된 hello 경로에서 build.gradle를 선택 하 고 적절 하 게 작동 합니다. 명명 된 프로젝트를 만드는 경우 ``MyActor`` hello 루트 빌드 스크립트에 포함 해야 (hello Eclipse 플러그 인 또는 Yeoman 생성기 사용), ``${WORKSPACE}/MyActor``합니다. 이 기능에 대 한 예제 스크린 샷 다음 hello 참조:

    ![Service Fabric Jenkins 빌드 작업][build-step]

   g. Hello에서 **빌드 후 작업** 드롭다운 목록에서 선택 **서비스 패브릭 프로젝트 배포**합니다. 여기 tooprovide 클러스터 세부 정보를 hello Jenkins 컴파일된 서비스 패브릭 응용 프로그램 배포 되도록 해야 합니다. Toodeploy hello 응용 프로그램을 사용 하는 추가 응용 프로그램 세부 정보를 제공할 수도 있습니다. 이 기능에 대 한 예제 스크린 샷 다음 hello 참조:

    ![Service Fabric Jenkins 빌드 작업][post-build-step]

   > [!NOTE]
   > 서비스 패브릭 toodeploy hello Jenkins 컨테이너 이미지를 사용 하는 경우 여기에 hello 클러스터 hello 하나의 호스팅 hello Jenkins 컨테이너 응용 프로그램으로 동일한 수 있습니다.
   >

## <a name="next-steps"></a>다음 단계
이제 GitHub 및 Jenkins가 구성되었습니다. 변경에 몇 가지 예제를 만드는 것이 좋습니다 프로그램 ``MyActor`` hello 저장소 예제에서 프로젝트 https://github.com/sayantancs/SFJenkins 합니다. 변경 내용을 tooa 원격 푸시 ``master`` 분기 (또는 사용자가 구성한와 toowork 분기). 이 경우 hello Jenkins 작업 ``MyJob``, 구성 합니다. GitHub에서 hello 변경 인출,을 빌드하고 빌드 후 작업에 지정 된 hello 응용 프로그램 toohello 클러스터 끝점을 배포 합니다.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
