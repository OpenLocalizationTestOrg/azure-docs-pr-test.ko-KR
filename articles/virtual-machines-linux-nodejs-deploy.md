---
title: "aaaDeploy Node.js 응용 프로그램 tooLinux Azure의 가상 컴퓨터"
description: "자세한 방법을 toodeploy는 Node.js 응용 프로그램이 Azure에서 가상 컴퓨터를 tooLinux 합니다."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Node.js 응용 프로그램 tooLinux Azure의 가상 컴퓨터 배포
이 자습서에서는 어떻게 tootake Node.js 응용 프로그램을 Azure에서 실행 중인 tooLinux 가상 컴퓨터에 배포 합니다. 이 자습서의 지침에 hello Node.js를 실행할 수 있는 모든 운영 체제에서 수행할 수 있습니다.

이 문서에서 배울 내용은 다음과 같습니다.

* 간단한 TODO 응용 프로그램을 포함하는 GitHub 리포지토리 분기 및 복제.
* 만들기 및 Azure toorun hello 응용 프로그램의 두 Linux 가상 컴퓨터 구성
* 업데이트 toohello 웹 프런트 엔드 가상 컴퓨터에 푸시하여 hello 응용 프로그램을 반복 합니다.

> [!NOTE]
> toocomplete이이 자습서에서는 hello는 개발 컴퓨터에서 기능 toouse Git 및 GitHub 계정 및 Microsoft Azure 계정 해야 합니다.
> 
> 현재 GitHub 계정이 없는 경우 [여기서](https://github.com/join)등록할 수 있습니다.
> 
> [Microsoft Azure](https://azure.microsoft.com/) 계정이 없으면 [여기서](https://azure.microsoft.com/pricing/free-trial/) 무료 평가판에 등록할 수 있습니다. 이 또한 단계별로 안내 합니다 hello 등록에 대 한 프로세스는 [Microsoft 계정](http://account.microsoft.com) 하면 아직 없는 경우. 또는 Visual Studio 구독자인 경우 [MSDN 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.
> 
> 개발 컴퓨터에 Git가 없으며 Macintosh 또는 Windows 컴퓨터를 사용하는 경우 Git를 [여기](http://www.git-scm.com)에서 설치합니다. Linux를 사용 하는 경우 설치와 같은,에 가장 적합 한 hello 메커니즘을 사용 하 여 git `sudo apt-get install git`합니다.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>분기 및 복제 hello TODO 응용 프로그램
이 자습서에서 사용 하는 할 일 응용 프로그램 hello 할 일 목록 추적 하는 MongoDB 인스턴스에 대해 간단한 웹 프런트 엔드를 구현 합니다. TooGitHub 로그인 한 후 이동 [여기](https://github.com/stepro/node-todo) toofind hello 응용 프로그램 및 hello 링크를 사용 하 여 오른쪽 위를 hello에 분기 합니다. *accountname*/node-todo로 명명된 계정에 리포지토리를 만들어야 합니다.

이제 개발 컴퓨터에서 이 리포지토리를 복제합니다.

    git clone https://github.com/accountname/node-todo.git

에서는 hello 저장소의 로컬 복제본이 약간 나중 toohello 소스 코드 변경 하는 경우.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>만들기 및 hello Linux 가상 컴퓨터를 구성 합니다.
Azure는 Linux 가상 컴퓨터를 사용하는 원시 계산을 훌륭히 지원합니다. 이 부분의 hello 자습서에서는 쉽게 두 Linux 가상 컴퓨터를 실행 하는 방법을 hello TODO 응용 프로그램 toothem, 실행 중인 hello 웹 프런트 엔드에 1과 hello MongoDB 인스턴스 다른 hello에 배포 합니다.

### <a name="creating-virtual-machines"></a>가상 컴퓨터 만들기
hello 가장 쉬운 방법은 toocreate Azure에서 새 가상 컴퓨터는 toouse hello Azure 포털입니다. 클릭 [여기](https://portal.azure.com) 웹 브라우저에서에 hello Azure 포털에서 toosign을 시작 합니다. Azure 포털 hello 로드 되 면 hello 다음 단계를 완료 합니다.

* 안녕하세요 "+ 새로 만들기"를 클릭 합니다. 연결;
* Hello "을 계산" 범주를 선택 하 고 "Ubuntu Server 14.04 LTS";를 선택 합니다.
* Hello "리소스 관리자" 배포 모델을 선택 하 고 "만들기";
* 다음 지침에 따라 hello 기본 사항을 입력 합니다.
  * 나중에 쉽게 식별할 수 있는 이름을 지정합니다.
  * 이 자습서에서는 암호 인증을 선택합니다.
  * 식별할 수 있는 이름으로 새 리소스 그룹을 만듭니다.
* Hello 가상 컴퓨터 크기에 대 한 "A1 표준" 되는 것이 좋습니다가이 자습서에 대 한 합니다.
* 추가 설정에 대 한 "Standard" hello 디스크 유형을 확인 하 고 나머지 항목을 기본값으로 hello 모든 동의 합니다.
* Hello 요약 페이지에 hello 만들기를 시작 합니다.

위의 hello 수행 hello 웹 프런트 엔드 및 hello MongoDB 인스턴스에 대 한 두 toocreate Linux 가상 컴퓨터에 두 번 처리 합니다. Hello 가상 컴퓨터 만들기에는 5-10 분 정도 소요 됩니다.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>가상 컴퓨터에 DNS 항목 할당
Azure에서 만든 가상 컴퓨터는 기본적으로 1.2.3.4와 같은 공용 IP 주소를 통해 액세스할 수 있습니다. 보겠습니다 hello 컴퓨터 보다 쉽게 식별할 수 있도록 DNS 항목을 지정 하 여 합니다.

Hello 포털 hello 가상 컴퓨터를 만들었다고에 표시 되 면 hello 왼쪽된 탐색 모음에서 hello "가상 컴퓨터" 링크를 클릭 하 고 컴퓨터를 찾습니다. 각 컴퓨터에 다음을 수행합니다.

* Hello Essentials 탭을 찾아서 hello 공용 IP 주소; 클릭
* Hello 공용 IP 주소 구성에서 DNS 이름 레이블을 할당 하 고 저장 합니다.

hello 포털은 해당 hello 이름을 지정 하는 사용할 수 있는 확인 합니다. Hello 구성에서 저장 한 후 가상 컴퓨터 이름을 갖게 됩니다. 호스트와 유사한 너무`machinename.region.cloudapp.azure.com`합니다.

### <a name="connecting-toohello-virtual-machines"></a>Toohello 가상 컴퓨터를 연결합니다.
가상 컴퓨터를 프로 비전 된 경우 SSH를 통해 미리 구성 된 tooallow 원격 연결 된입니다. 이 hello 메커니즘 tooconfigure hello 가상 컴퓨터를 사용 합니다. 개발 작업을 위한 기간을 사용 하는 경우 이미 않아도 하나 경우 tooget SSH 클라이언트를 해야 합니다. 여기서 일반적인 선택은 PuTTY이며 [여기](http://www.chiark.greenend.org.uk/~sgtatham/putty/)에서 다운로드할 수 있습니다. Macintosh 및 Linux OS는 미리 설치된 SSH 버전으로 제공됩니다.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Hello 웹 프런트 엔드 가상 컴퓨터를 구성합니다.
SSH toohello 웹 프런트 엔드 컴퓨터를 사용 하 여 PuTTY, ssh 명령줄 또는 다른 임의의 SSH 도구 만들어집니다. 명령 프롬프트에서 다음 환영 메시지가 표시되어야 합니다.

우선 Git 및 노드가 모두 설치되었는지 확인해보겠습니다.

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Hello 응용 프로그램의 웹 프런트 엔드 일부 네이티브 Node.js 모듈을 기반 tooinstall hello는 일련의 기본 빌드 도구도 필요 합니다.

    sudo apt-get install -y build-essential

마지막으로, 보겠습니다 라는 Node.js 응용 프로그램을 설치 *영원히*, toorun Node.js 서버 응용 프로그램 수:

    sudo npm install -g forever

이이 가상 컴퓨터 toobe 수 toorun hello 응용 프로그램의 웹 프런트 엔드에 필요한 모든 hello 종속성을 실행 하는 설정 하겠습니다 됩니다. toodo이를 먼저 만듭니다 hello GitHub 리포지토리 (다루게 될 것이 업데이트 시나리오 나중) 업데이트 toohello 가상 컴퓨터를 쉽게 게시할 하 고 다음 hello bare 복제 tooprovide를 복제할 수 있도록 이전에 분기의 복제본을 완전 한 버전의 hello 실제로 실행 될 수 있는 저장소입니다.

Hello 다음 명령을 실행 hello 홈 (~) 디렉터리에서 시작 합니다 (교체 *accountname* 을 GitHub 사용자 계정 이름):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

이제 hello 노드 todo 디렉터리를 입력 하 고이 명령을 실행.

    npm install
    forever start server.js

그러나 hello 웹 프런트 엔드 응용 프로그램의 실행 되, 즉 하나의 단계가 더 웹 브라우저에서 hello 응용 프로그램에 액세스 합니다. hello 만든 가상 컴퓨터 보호 되는 Azure 리소스를 호출 하 여 한 *네트워크 보안 그룹*, 만든 가상 컴퓨터를 프로 비전 할 때 hello에 대 한 합니다. 현재이 리소스는 외부 요청 tooport 라우팅된 22 toobe toohello 있는 가상 컴퓨터 hello 컴퓨터 하지만 다른와 SSH 통신만 허용 합니다. 따라서 순서 tooview hello 포트 8080에서 구성 된 toorun 되 TODO 응용 프로그램에서에서이 포트도 필요 열렸습니다 toobe 합니다.

Toohello Azure 포털을 반환 하 고 hello 다음 단계를 완료 합니다.

* "리소스 그룹" hello 왼쪽된 탐색 모음; 클릭
* 가상 컴퓨터를 포함 하는 hello 리소스 그룹 선택
* 리소스의 hello 결과 목록에서 hello 네트워크 보안 그룹 (hello 하나 방패 아이콘으로);를 선택 합니다.
* Hello 속성에서 "인바운드 보안 규칙";를 선택 합니다.
* Hello 도구 모음에서 "추가"를 클릭 합니다.
* "default-allow-todo"와 같은 이름을 제공합니다.
* 너무 hello 프로토콜 설정 "TCP";
* 대상 포트 범위를 hello 설정 너무 "8080";
* 확인을 클릭 하 고 hello 보안 규칙 toobe 생성 될 때까지 기다립니다.

이 보안 규칙을 만든 후 hello TODO 응용 프로그램에 공개적으로 표시 되는 인터넷 hello 및 URL을와 같은 사용 하는 예를 들어 tooit를 찾아볼 수 있습니다.

    http://machinename.region.cloudapp.azure.com:8080

에서는 아직 구성 하지 않은 hello MongoDB 가상 컴퓨터, 경우에 hello TODO 응용 프로그램 기능 매우 toobe이 표시 되는지 확인할 수 있습니다. Hello 소스 리포지토리는 하드 코드 된 toouse 미리 배포 MongoDB 인스턴스 때문입니다. Hello MongoDB 가상 컴퓨터를 구성한 후 뒤로 이동 하 고 대신 hello 소스 코드 tooutilize 개인 MongoDB 인스턴스를 변경 합니다.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Hello MongoDB 가상 컴퓨터를 구성합니다.
SSH toohello 두 번째 컴퓨터를 사용 하 여 PuTTY, ssh 명령줄 또는 다른 임의의 SSH 도구 만들어집니다. Hello 환영 메시지 및 명령 프롬프트를 확인 한 후 MongoDB 설치 (이 지침에서 수행 된 [여기](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

기본적으로 MongoDB는 로컬로 액세스할 수 있도록 구성됩니다. 이 자습서에서는 hello 응용 프로그램의 가상 컴퓨터에서 액세스할 수 있도록 MongoDB 구성 됩니다. Sudo 컨텍스트에서 hello /etc/mongod.conf 파일을 열고 hello 찾을 `# network interfaces` 섹션. 변경 hello `net.bindIp` 구성 값 너무`0.0.0.0`합니다.

> [!NOTE]
> 이 구성은이 자습서에만 hello 목적입니다. 권장되는 보안 사례가 **아니고** 프로덕션 환경에서는 사용되면 안됩니다.
> 
> 

이제 hello MongoDB 서비스가 시작 되었는지 확인 합니다.

    sudo service mongod restart

MongoDB는 기본적으로 포트 27017에 대해 작동합니다. Hello에 동일한 방식으로 tooopen 했습니다: 포트 8080 hello 웹 프런트 엔드 가상 컴퓨터에 있으므로 tooopen 포트 27017 hello MongoDB 가상 컴퓨터에 필요 합니다.

Toohello Azure 포털을 반환 하 고 hello 다음 단계를 완료 합니다.

* "리소스 그룹" hello 왼쪽된 탐색 모음; 클릭
* Hello MongoDB 가상 컴퓨터를 포함 하는 hello 리소스 그룹 선택
* 리소스의 hello 결과 목록에서 toohello MongoDB 가상 컴퓨터를 지정한 이름과 같은 이름을 hello로 hello 네트워크 보안 그룹 (hello 하나 방패 아이콘으로)을 선택
* Hello 속성에서 "인바운드 보안 규칙";를 선택 합니다.
* Hello 도구 모음에서 "추가"를 클릭 합니다.
* "default-allow-mongo"와 같은 이름을 제공합니다.
* 너무 hello 프로토콜 설정 "TCP";
* 대상 포트 범위를 hello 설정 너무 "27017";
* 확인을 클릭 하 고 hello 보안 규칙 toobe 생성 될 때까지 기다립니다.

## <a name="iterating-on-hello-todo-application"></a>Hello TODO 응용 프로그램에서 반복
지금까지 것을 프로 비전 Linux 가상 컴퓨터 2: MongoDB 인스턴스 하나를 실행 하는 hello 응용 프로그램의 웹 프런트 엔드 및 하나를 실행 합니다. 하지만 문제가-hello 웹 프런트 엔드 사용자를 프로 비전 하는 hello MongoDB 인스턴스를 아직 사용 실제로 되지 않습니다. 문제를 해결 하겠습니다 hello 웹 프런트 엔드 코드 toouse를 업데이트 하 여 하드 코드 된 인스턴스 대신 환경 변수입니다.

### <a name="changing-hello-todo-application"></a>Hello TODO 응용 프로그램 변경
먼저 hello 노드 todo 리포지토리를 복제 하려면 개발 컴퓨터에 hello 열고 `node-todo/config/database.js` 선호 하는 편집기에서 파일을 hello url 값과 같은 hello 하드 코드 된 값에서 변경 `mongodb://...` 너무`process.env.MONGODB`합니다.

변경 내용을 커밋하고 toohello GitHub 마스터 푸시하십시오.

    git commit -am "Get MongoDB instance from env"
    git push origin master

그러나이 hello 변경 toohello 웹 프런트 엔드 가상 컴퓨터를 게시 하지는 않습니다. 이제 몇 가지 더 많은 변경 내용을 toothat 가상 컴퓨터 tooenable hello hello 실제 환경에서 hello 변경 효과 신속 하 게 살펴볼 수 있도록 업데이트를 게시 하기 위한 단순 하지만 효율적인 메커니즘을 확인 합니다.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Hello 웹 프런트 엔드 가상 컴퓨터를 구성합니다.
이전에 만들었다고 hello 노드 todo 저장소의 복제본을 bare hello 웹 프런트 엔드 가상 컴퓨터에서 다시 호출 합니다. 밝혀졌습니다이 작업을 원격 toowhich 변경 내용을 푸시 될 수 있는 새 Git 만들었음을 합니다. 그러나 단순히 toothis 원격 푸시하여 매우 코드에서 작업할 때 개발자가 찾고 hello 신속 하 게 반복 모델을 제공 하지 않습니다.

어떤 것을 toobe 수 toodo는 hello 가상 컴퓨터에 밀어넣기 toohello 원격 리포지토리 발생할 때 TODO 응용 프로그램을 실행 하는 hello는 자동으로 업데이트 되도록 합니다. 다행히이 작업은 쉽게 tooachieve git 포함 합니다.

Git 후크 hello 저장소에서 수행 된 특정 시간 tooreact tooactions에 호출 되는 수를 제공 합니다. 셸 스크립트를 사용 하 여 hello 저장소에 지정 된 이러한 `hooks` 폴더입니다. 속성은 hello 자동 업데이트 시나리오에 가장 적합 hello 후크는 hello `post-update` 이벤트입니다.

SSH 세션 toohello 웹 프런트 엔드를 가상 컴퓨터에서 변경 toohello `~/node-todo.git/hooks` 디렉터리 hello 다음 라는 tooa 콘텐츠 파일을 추가 하 고 `post-update` (교체 `machinename` 및 `region` MongoDB 가상 컴퓨터 정보로):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Hello 다음 명령을 실행 하 여이 파일은 실행 파일을 확인 합니다.

    chmod 755 post-update

이 스크립트를 사용 하면 현재 hello 서버 응용 프로그램이 중지 되, hello 복제 된 저장소의 hello 코드를 업데이트 된 toohello 최신, 업데이트 된 종속성을 만족 hello 서버를 다시 시작 합니다. 또한 해당 hello 환경 수행 하도록 구성 되는 환경 변수에서 첫 번째 응용 프로그램 업데이트 tooget hello MongoDB 인스턴스를 수신 하기 위해 준비 하도록 합니다.

### <a name="configuring-your-development-machine"></a>개발 컴퓨터 구성
이제 개발 컴퓨터 toohello 웹 프런트 엔드 가상 컴퓨터를 연결 해 보겠습니다. 이 hello 완전 저장소는 원격 hello 가상 컴퓨터에 추가 하는 것과 간단 합니다. 이 스크립트 명령 toodo 다음 hello를 실행 (교체 *사용자* 을 웹 프런트 엔드 가상 컴퓨터 로그인 이름 및 *machinename* 및 *지역* 적절 하 게):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

이 필요한 tooenable 밀어넣거나 게시 적용, toohello 웹 프런트 엔드 가상 컴퓨터를 변경 하는 all입니다.

### <a name="publishing-updates"></a>업데이트 게시
Hello 응용 프로그램에서 고유한 MongoDB 인스턴스를 사용할 수 있도록 지금까지 설정한 hello 하나의 변경을 게시 해 보겠습니다.

    git push azure master

출력 유사한 toothis를 나타나야 합니다.

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

이 명령이 완료 된 후에 웹 브라우저에서 hello 응용 프로그램을 새로 고쳐 보십시오. 여기에 제시 된 hello 할 일 목록은 비어 있으며 공유 동률된 toohello MongoDB 인스턴스를 배포 하는 더 이상 수 toosee 있어야 합니다.

toocomplete hello 자습서 다른, 더 많은 보이는 변경을 만들어 보겠습니다. 개발 컴퓨터에서 선호 하는 편집기를 사용 하 여 hello node-todo/public/index.html 파일을 엽니다. Hello jumbotron 헤더를 찾아서 "저는 Todo-aholic"에서 너무 "I am Azure에서 Todo aholic!" hello 제목을 변경 합니다.

이제 커밋하겠습니다.

    git commit -am "Azurify hello title"

이 시간, tooback toohello GitHub 리포지토리를 푸시하기 전에 hello 변경 tooAzure를 게시 하겠습니다.

    git push azure master

이 명령이 완료 되 면 hello 웹 페이지를 새로 고 hello 변경 내용이 표시 됩니다. 자신을 이후 hello 변경 백 toohello 원본 원격 강제: 

    git push origin master

## <a name="next-steps"></a>다음 단계
방법을 보여 주었습니다.이 문서 tootake Node.js 응용 프로그램을 Azure에서 실행 중인 tooLinux 가상 컴퓨터에 배포 합니다. Azure에서 Linux 가상 컴퓨터에 대해 자세히 toolearn 참조 [Azure에서 소개 tooLinux](/documentation/articles/virtual-machines-linux-introduction/)합니다.

방법에 대 한 자세한 내용은 Azure에서 Node.js 응용 프로그램 toodevelop 참조 hello [Node.js 개발자 센터](/develop/nodejs/)합니다.

