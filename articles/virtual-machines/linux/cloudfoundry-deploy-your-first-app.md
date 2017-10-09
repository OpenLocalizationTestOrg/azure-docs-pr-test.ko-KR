---
title: "aaaDeploy 프로그램 첫 번째 앱 tooCloud Microsoft Azure에서 대장간 | Microsoft Docs"
description: "응용 프로그램 tooCloud 대장간 Azure에서 배포"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a>Microsoft Azure에서 대장간 첫 번째 앱 tooCloud 프로그램 배포

[Cloud Foundry](http://cloudfoundry.org)는 Microsoft Azure에서 사용할 수 있는 인기 있는 오픈 소스 응용 프로그램 플랫폼입니다. 이 문서에서는 보여줍니다 어떻게 toodeploy 및 Azure 환경에서 클라우드 대장간에서 응용 프로그램을 관리 합니다.

## <a name="create-a-cloud-foundry-environment"></a>Cloud Foundry 환경 만들기

Azure에 Cloud Foundry 환경을 만들기 위한 여러 가지 옵션이 있습니다.

- 사용 하 여 hello [중요 클라우드 대장간 제안] [ pcf-azuremarketplace] hello Azure 마켓플레이스 toocreate PCF Ops Manager 및 Service Broker Azure hello를 포함 하는 표준 환경에에서 있습니다. 찾을 수 있습니다 [지침을 완료] [ pcf-azuremarketplace-pivotaldocs] hello 마켓플레이스를 배포 하기 위한 hello 중요 설명서에에서 제공 합니다.
- [Pivotal Cloud Foundry를 수동으로 배포][pcf-custom]하여 사용자 지정된 환경을 만듭니다.
- [Hello 오픈 소스 클라우드 대장간 패키지를 직접 배포] [ oss-cf-bosh] 를 설정 하 여 한 [BOSH](http://bosh.io) hello 클라우드 대장간 환경의 hello 배포를 조정 하는 VM 감독 합니다.

> [!IMPORTANT] 
> Hello Azure Marketplace에서에서 PCF를 배포 하는 경우 hello SYSTEMDOMAINURL 메모 및 tooaccess hello hello 마켓플레이스 배포 가이드에 설명 되어 있는 중요 응용 프로그램 관리자 hello 관리자 자격 증명이 필요 합니다. 이 자습서에서는 필요한 toocomplete 됩니다. 마켓플레이스 배포 hello SYSTEMDOMAINURL hello 양식 https://system가 있습니다. *ip 주소*. cf.pcfazure.com 합니다.

## <a name="connect-toohello-cloud-controller"></a>Toohello 클라우드 컨트롤러를 연결 합니다.

hello 클라우드 컨트롤러는 배포 하 고 응용 프로그램 관리에 대 한 hello 대 한 주 진입점 지점 tooa 클라우드 대장간 환경입니다. hello 코어 클라우드 컨트롤러 API (CCAPI)는 REST API, 이지만 다양 한 도구를 통해 액세스할 수 있습니다. Hello를 통해 상호 작용 우리는 경우 [클라우드 대장간 CLI][cf-cli]합니다. Windows, Linux, MacOS 등 또는에 hello CLI를 설치할 수 있지만 것도 가능 하다 hello에 미리 설치 된 tooinstall 하지 않으려면 [Azure 클라우드 셸][cloudshell-docs]합니다.

앞에 추가 되는, toolog `api` toohello hello 마켓플레이스 배포에서 얻은 SYSTEMDOMAINURL 합니다. Hello도 포함 해야 hello 기본 배포는 자체 서명 된 인증서를 사용 하므로 `skip-ssl-validation` 전환 합니다.

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

Toohello 클라우드 컨트롤러에에서 증명된 toolog 됩니다. Hello 마켓플레이스 배포 단계에서 복사한 hello 관리자 계정 자격 증명을 사용 합니다.

클라우드 대장간 제공 *조직* 및 *공간* 네임 스페이스 tooisolate hello 팀과 공유 배포 내에서 환경으로 합니다. hello PCF 마켓플레이스 배포 포함 hello 기본 *시스템* org 및 공백 집합 toocontain 같은 hello 자동 크기 조정 서비스 및 hello Azure service broker의 hello 기본 구성 요소를 생성 합니다. 지금은 hello 선택 *시스템* 공간입니다.


## <a name="create-an-org-and-space"></a>조직 및 공간 만들기

입력 하는 경우 `cf apps`, hello 시스템 조직 내에서 hello 시스템 공간에 배포 된 시스템 응용 프로그램 집합 표시 

Hello를 유지 해야 *시스템* 시스템 응용 프로그램에 대 한 예약 org 만드세요 org 및 공간 toohouse 샘플 응용 프로그램입니다.

```bash
cf create-org myorg
cf create-space dev -o myorg
```

Hello 대상 명령 tooswitch toohello 새 조직 및 공간을 사용 합니다.

```bash
cf target -o testorg -s dev
```

이제 응용 프로그램을 배포 하면 hello 새 조직 및 공간에서 자동으로 생성 됩니다. 현재 tooconfirm hello 새 org/공간에 앱이 없습니다. 입력 `cf apps` 다시 합니다.

> [!NOTE] 
> 조직 및 공백 및 역할 기반 액세스 제어 (RBAC)에 사용할 수 있습니다 어떻게 하는 방법에 대 한 자세한 내용은 참조 hello [클라우드 대장간 설명서][cf-orgs-spaces-docs]합니다.

## <a name="deploy-an-application"></a>응용 프로그램 배포

Java로 작성 되 고 hello에 따라 Hello ' 봄 ' 클라우드를 호출 하는 샘플 클라우드 대장간 응용 프로그램 사용 [Spring Framework](http://spring.io) 및 [스프링 부팅](http://projects.spring.io/spring-boot/)합니다.

### <a name="clone-hello-hello-spring-cloud-repository"></a>Hello Hello 스프링 클라우드 리포지토리 복제

hello Hello 스프링 클라우드 샘플 응용 프로그램은 GitHub에서 사용할 수 있습니다. Tooyour 환경을 복제 하 고 hello 새 디렉터리로 변경 합니다.

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a>Hello 응용 프로그램 빌드

사용 하 여 빌드 hello 앱 [Apache Maven](http://maven.apache.org)합니다.

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a>Cf 푸시를 통한 hello 응용 프로그램 배포

대부분 응용 프로그램 tooCloud 대장간을 배포할 수 있습니다 hello를 사용 하 여 `push` 명령:

```bash
cf push
```

때 있습니다 *푸시* 응용 프로그램을 클라우드 대장간 hello 유형의 응용 프로그램 (이 경우 Java 응용 프로그램에서)를 검색 하 고 해당 종속성 (이 경우 hello Spring framework)을에서 식별 합니다. 다음 패키지 모든 toorun 코드 라고 하는 독립 실행형 컨테이너 이미지에 필요한는 *드롭릿*합니다. 마지막으로, 클라우드 대장간 일정 hello 사용자 환경에서 사용할 수 있는 컴퓨터 중 하나에서 응용 프로그램 hello 및 위치에 도달할 수, hello 명령의 hello 출력에서 제공 되는 URL을 만듭니다.

![cf 밀어넣기 명령의 출력][cf-push-output]

toosee hello hello 스프링 클라우드 응용 프로그램을 브라우저에서 제공 하는 개방형 hello URL:

![Hello Spring Cloud용 기본 UI][hello-spring-cloud-basic]

> [!NOTE] 
> toolearn 처리 과정에 대 한 자세한 `cf push`, 참조 [응용 프로그램 준비 된] [ cf-push-docs] hello 클라우드 대장간 설명서에에서 있습니다.

## <a name="view-application-logs"></a>응용 프로그램 로그 보기

이름을 사용 하 여 응용 프로그램에 대 한 hello 클라우드 대장간 CLI tooview 로그를 사용할 수 있습니다.

```bash
cf logs hello-spring-cloud
```

기본적으로 hello 로깅합니다 명령을 사용 하 여 *꼬리*, 작성 된 대로 새 로그를 보여 주는 합니다. toosee 새 로그 표시 hello 브라우저에서 hello hello 스프링 클라우드 앱을 새로 고칩니다.

이미 작성 tooview 로그 추가 hello `recent` 전환:

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a>배율 hello 응용 프로그램

기본적으로 `cf push`만 응용 프로그램의 단일 인스턴스를 만듭니다. tooensure 고가용성 및 높은 처리량을 위한 확장 가능 응용 프로그램의 인스턴스가 둘 이상 toorun 일반적으로 원하는 합니다. Hello를 사용 하 여 이미 배포 된 응용 프로그램을 쉽게 확장할 수 있습니다 `scale` 명령:

```bash
cf scale -i 2 hello-spring-cloud
```

실행 중인 hello `cf app` 명령 hello 응용 프로그램에 클라우드 대장간은 hello 응용 프로그램의 다른 인스턴스를 만드는 것을 표시 합니다. Hello 응용 프로그램 시작 된 후 클라우드 대장간 부하 분산 트래픽 tooit를 자동으로 시작 합니다.


## <a name="next-steps"></a>다음 단계

- [읽기 hello 클라우드 대장간 설명서][cloudfoundry-docs]
- [클라우드 대장간에 대 한 hello Visual Studio Team Services 플러그 인을 설정 합니다.][vsts-plugin]
- [클라우드 대장간에 대 한 로그 분석 노즐 Microsoft hello를 구성 합니다.][loganalytics-nozzle]

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png