---
title: "3 노드 Deis aaaDeploy 클러스터 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 toocreate 3 노드 Deis Azure 리소스 관리자 템플릿을 사용 하 여 Azure에서 클러스터"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Azure에서 3노드 Deis 클러스터 배포 및 구성
이 문서는 Azure에서 [Deis](http://deis.io/) 클러스터를 프로비전하는 과정을 단계별로 안내합니다. 필요한 인증서 toodeploying hello를 만들고 샘플 크기 조정에서 모든 hello 단계에서는 **이동** hello 새로 프로 비전 된 클러스터에서 응용 프로그램입니다.

hello 다음 다이어그램 아키텍처를 보여 줍니다 hello 배포 된 hello 시스템입니다. 시스템 관리자를 사용 하 여 hello 클러스터 관리 도구와 같은 Deis **deis** 및 **deisctl**합니다. 연결은은 hello 멤버의 hello 연결 tooone hello 클러스터에서 노드를 전달 하는 Azure 부하 분산 장치를 통해 설정 됩니다. hello 클라이언트 액세스를 배포 된 hello 부하 분산 장치를 통해도 응용 프로그램입니다. 이 경우 hello 부하 분산 장치 전달 hello 트래픽 tooa Deis hello 클러스터에서 호스트 하는 트래픽을 toocorresponding Docker 컨테이너를 추가로 routs 라우터 메시를 합니다.

  ![배포된 Desis 클러스터의 아키텍처 다이어그램](./media/deis-cluster/architecture-overview.png)

단계를 수행 하는 hello 통해 순서 toorun에 다음이 필요 합니다.

* 활성 Azure 구독. 없는 경우 [azure.com](https://azure.microsoft.com/)에서 평가판을 얻을 수 있습니다.
* 회사 또는 학교 id toouse Azure 리소스 그룹입니다. 너무 필요한 개인 계정과 Microsoft id 사용 하 여 로그를 있으면[개인 컴퓨터로에서 작업 id를 만들](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.
* -하나-클라이언트 운영 체제에 따라 hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) 또는 hello [Mac, Linux 및 Windows에 대 한 Azure CLI](../../cli-install-nodejs.md)합니다.
* [OpenSSL](https://www.openssl.org/). OpenSSL 사용 되는 toogenerate hello 필요한 인증서입니다.
* [Git Bash](https://git-scm.com/)와 같은 Git 클라이언트
* tootest hello 샘플 응용 프로그램을도 DNS 서버가 필요 합니다. 모든 DNS 서버 또는 와일드 카드 A 레코드를 지원하는 서비스를 사용할 수 있습니다.
* 컴퓨터 toorun Deis 클라이언트 도구입니다. 로컬 컴퓨터 또는 가상 컴퓨터 중 하나를 사용할 수 있습니다. 거의 모든 Linux 배포판에 이러한 도구를 실행할 수는 있지만 hello 다음 명령을 사용 하 여 Ubuntu 합니다.

## <a name="provision-hello-cluster"></a>프로 비전 hello 클러스터
이 섹션에서는 [Azure 리소스 관리자](../../azure-resource-manager/resource-group-overview.md) hello 오픈 소스 리포지토리에서 템플릿을 [azure-빠른 시작-템플릿](https://github.com/Azure/azure-quickstart-templates)합니다. 첫째, 다운 hello 템플릿을 복사 합니다. 그런 다음 인증에 대해 새 SSH 키 쌍을 만듭니다. 그런 다음 클러스터에 대해 새 식별자를 구성합니다. 및 마지막으로 hello 셸 스크립트 또는 hello PowerShell 스크립트 tooprovision hello 클러스터 사용 합니다.

1. 복제 hello 리포지토리: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates)합니다.
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Toohello 템플릿 폴더를 이동 합니다.
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. ssh-keygen를 사용하여 새 SSH 키 쌍 만들기:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. 개인 키 위에 hello를 사용 하 여 인증서를 생성 합니다.
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. 너무 이동[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate 새 클러스터 토큰을 다음과 같은 형식입니다.
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   각 CoreOS 클러스터 toohave이 무료 서비스에서 고유한 토큰이 필요합니다. 자세한 내용은 [CoreOS 설명서](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) 를 참조하세요.
6. Hello 수정 **클라우드 config.yaml** tooreplace hello 기존 파일 **검색** hello 새 토큰으로 토큰:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Hello 수정 **azuredeploy parameters.json** 파일: 텍스트 편집기에서 4 단계에서 만든 열기 hello 인증서입니다. 사이의 모든 텍스트를 복사 `----BEGIN CERTIFICATE-----` 및 `-----END CERTIFICATE-----` hello에 **sshKeyData** 매개 변수 (필요 함 tooremove 모든 줄 바꿈 문자)입니다.
8. Hello 수정 **newStorageAccountName** 매개 변수입니다. VM OS 디스크에 대 한 hello 저장소 계정입니다. 이 계정 이름은 전역적으로 고유 toobe에 있습니다.
9. Hello 수정 **publicDomainName** 매개 변수입니다. 이 hello 부하 분산 장치에 대 한 공용 IP와 관련 된 hello DNS 이름의 일부가 됩니다. hello 최종 FQDN 갖습니다 hello 형식의 *[이 매개 변수 값]*. *[region]* . cloudapp.azure.com 합니다. 예를 들어 hello 리소스 그룹은 배포 된 toohello 미국 서 부 지역 다음 항목은 최종 hello 및 deishbai32, hello 이름을 지정한 경우 FQDN tooyour 부하 분산 장치에 deishbai32.westus.cloudapp.azure.com 됩니다.
10. Hello 매개 변수 파일을 저장 합니다. 및 다음 Azure PowerShell을 사용 하 여 hello 클러스터를 구축할 수 있습니다.
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    또는 Azure CLI:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Hello 리소스 그룹은 프로 비전 되 면 hello 그룹의에서 모든 리소스 hello Azure 클래식 포털에서 볼 수 있습니다. 표시 된 대로 다음 스크린 샷에서 hello hello에 세 개의 Vm이 있는 가상 네트워크를 포함 하는 리소스 그룹 toohello 조인 되는 동일한 가용성 집합입니다. hello 그룹에 연결 된 공용 ip 부하 분산 장치 포함 되어 있습니다.
    
    ![hello Azure 클래식 포털에서 리소스 그룹을 프로 비전](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Hello 클라이언트 설치
필요한 **deisctl** toocontrol 프로그램 클러스터 Deis 합니다. Deisctl 모든 hello 클러스터 노드에 자동으로 설치 됩니다, 있지만 별도 관리 컴퓨터는 것이 좋습니다 toouse deisctl 됩니다. 또한 개인 IP 주소만 사용 하 여 모든 노드를 구성 하기 때문에 hello 부하 분산 된 공용 IP tooconnect toohello 노드 컴퓨터에 있는 통해 toouse SSH 터널링 필요 합니다. hello 다음 단계가 hello deisctl를 별도 Ubuntu 물리적 또는 가상 컴퓨터를 설정 합니다.

1. deisctl 설치:mkdir deis
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. 개인 키 toossh 에이전트를 추가 합니다.
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Deisct 구성:
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

hello 템플릿은 정의 2223 tooinstance 1, 매핑하는 인바운드 NAT 규칙 2224 tooinstance 2, 및 2225 tooinstance 3입니다. 이 hello deisctl 도구를 사용 하는 것에 대 한 중복성을 제공 합니다. Azure 클래식 포털에서 이러한 규칙을 검사할 수 있습니다.

![Hello 부하 분산 장치에서 NAT 규칙](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> 현재 hello 템플릿 3 개 노드 클러스터만 지원합니다. 이것은 루프 구문을 지원하지 않는 Azure 리소스 관리자 템플릿 NAT 규칙 정의의 제한 사항 때문입니다.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>설치 하 고 hello 시작 Deis 플랫폼
이제 deisctl tooinstall를 사용 하 고 hello 시작 플랫폼 Deis:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> 약간의 시간이 시작 hello 플랫폼 (으로 10 분)입니다. 특히, hello 작성기 서비스를 시작 하는 시간이 오래 걸릴 수 있습니다. 몇 번의 시도 toosucceed 걸리는 경우에 따라 및: hello 작업 toohang를 것 같으면 라고 입력 해 보세요 `ctrl+c` toobreak 실행 hello 명령 및 다시 시도 합니다.
> 
> 

사용할 수 있습니다 `deisctl list` tooverify 모든 서비스가 실행 중인 경우:

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

축하합니다. 이제 Azure에서 Deis 클러스터를 실행할 수 있습니다! 다음으로 샘플 동작에서 Go 응용 프로그램 toosee hello 클러스터를 배포 해 보겠습니다.

## <a name="deploy-and-scale-a-hello-world-application"></a>Hello World 응용 프로그램 배포 및 확장
hello 다음 단계 표시 방법 toodeploy "Hello World"으로 응용 프로그램 toohello 클러스터입니다. hello 단계에 기반 [설명서 Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles)합니다.

1. 라우팅 메시 toowork hello에 대 한 적절 하 게 해야 toohave 와일드 카드 A 레코드 toohello hello 부하 분산 장치의 공용 IP를 가리키는 도메인에 대 한 합니다. hello 다음 스크린샷은 도메인을 등록 하는 샘플에 대 한 hello A 레코드 GoDaddy에:
   
    ![Godaddy A 레코드](./media/deis-cluster/go-daddy.png)
   
   <p />
2. deis 설치:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. 새 SSH 키를 만들고 공개 키 tooGitHub hello를 추가 (물론, 또한 다시 사용할 수 있습니다 프로그램 기존 키)입니다. toocreate 새 SSH 키 쌍을 사용 합니다.
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. Id_rsa.pub, 또는 사용자가 선택한 tooGitHub의 hello 공개 키를 추가 합니다. SSH 키 구성 화면에서 hello 추가 SSH 키 단추를 사용 하 여이 수행할 수 있습니다.
   
   ![GitHub 키](./media/deis-cluster/github-key.png)
   
   <p />
5. 새 사용자 등록:
   
        deis register http://deis.[your domain]
   <p />
6. Hello SSH 키를 추가 합니다.
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. 응용 프로그램을 만듭니다.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.hello git 푸시 Docker 이미지 toobe를 빌드 및 배포, 몇 분 정도 걸리며를 트리거합니다. 내 경험에서 경우에 따라 10 단계 (Pushing 이미지 tooprivate 리포지토리) 중단 될 수 있습니다. 이런 경우 hello 프로세스를 중지할 수 있습니다 사용 하 여 제거 hello 응용 프로그램 ' 앱 deis: – destroy <application name> ` tooremove hello application and try again. You can use `apps:list deis' toofind 응용 프로그램의 hello 이름입니다. 작동 하는 것, 명령 출력의 hello 끝에서 hello 다음과 같은 내용이 나타납니다.
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Hello 응용 프로그램 작동 하 고 있는지 확인 합니다.
   
        curl -S http://[your application name].[your domain]
   다음과 같은 결과가 표시됩니다.
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Hello 응용 프로그램 too3 인스턴스 크기를 조정 합니다.
    
        deis scale cmd=3
    <p />
11. 사용할 수 있습니다 deis 응용 프로그램의 정보 tooexamine 세부 정보입니다. hello 다음 출력은 내 응용 프로그램 배포:
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>다음 단계
이 문서는 새 Deis 모든 hello 단계 tooprovision 단계는 Azure 리소스 관리자 템플릿을 사용 하 여 Azure에서 클러스터입니다. hello 템플릿에서 배포 된 응용 프로그램에 부하 분산 뿐 아니라 연결 tooling에 중복성을 지원 합니다. hello 서식 파일에는 귀중 한 공용 IP 리소스를 저장 하 고 더욱 안전한 환경 toohost 응용 프로그램을 제공 하는 멤버 노드에 공용 Ip를 사용 하지 않습니다. 더 toolearn hello 다음 문서를 참조:

[Azure Resource Manager 개요][resource-group-overview]  
[Toouse는 Azure CLI hello 하는 방법][azure-command-line-tools]  
[Azure Resource Manager로 Azure PowerShell 사용][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
