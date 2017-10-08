---
title: "Azure 서비스 패브릭 XPlat CLI aaaGetting 시작"
description: "Azure Service Fabric XPlat CLI 시작"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>서비스 패브릭 클러스터 XPlat CLI toointeract hello를 사용 하 여

Hello XPlat CLI를 사용 하 여 Linux에서 Linux 컴퓨터에서 서비스 패브릭 클러스터와 상호 작용할 수 있습니다.

hello 첫 번째 단계에서 다음 명령을 사용 하 여 경로에서 작업을 hello 집합과 hello git rep hello CLI의 hello 최신 버전을 가져오기 됩니다.

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

각 명령에 대 한 지원, 해당 명령에 대 한 hello 명령 tooobtain hello 도움말의 hello 이름을 입력할 수 있습니다.
Hello 명령에 대 한 자동 완성 지원 됩니다. 다음 명령을 통해 모든 hello 응용 프로그램 명령에 대 한 도움말 hello 예를 들어 

```sh
 azure servicefabric application 
```

다음 예제와 hello로 hello 도움말 tooa 특정 명령, 필터링 할 수 있습니다.

```sh
 azure servicefabric application  create
```

tooenable 자동 완성 hello CLI hello 다음 명령을 실행 합니다.

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

다음 명령을 hello toohello 클러스터 및 hello 클러스터의 노드 hello 표시를 연결 합니다.

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

다음을 입력할 수 있습니다-toouse 명명 된 매개 변수를 찾아 무엇 인지, 명령 도움말입니다. 예:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

컴퓨터에서 tooa 다중 컴퓨터 클러스터에 연결할 때 **즉의 일부가 아닌 hello 클러스터**, hello 다음 명령을 사용 하 여:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Hello 실제 IP 또는 FQDN으로 적절 하 게 hello PublicIPorFQDN 태그를 대체 합니다. 컴퓨터에서 tooa 다중 컴퓨터 클러스터에 연결할 때 **hello 클러스터의 일부인**, hello 다음 명령을 사용 하 여:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

PowerShell을 사용 하 여 또는 hello Azure 포털을 통해 CLI toointeract Linux 서비스 패브릭 클러스터를 생성 합니다.

> [!WARNING]
> 이러한 클러스터 보안 되지, 따라서 있습니다 수 수 열기 1 박스를 hello 클러스터 매니페스트에 hello 공용 IP 주소를 추가 하 여 합니다.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>Hello XPlat CLI tooconnect tooa 서비스 패브릭 클러스터를 사용 하 여

Azure CLI 명령을 수행 하는 hello tooconnect tooa 클러스터를 보호 하는 방법을 설명 합니다. hello 인증서 세부 정보는 hello 클러스터 노드에서 인증서를 일치 해야 합니다.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

인증서 인증 기관 (Ca)가 있으면 다음 예제는 hello와 같은 tooadd hello-ca-cert-path 매개 변수가 필요 합니다. 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

여러 Ca가 hello 구분 기호로 쉼표를 사용 합니다.

Hello 매개 변수를 사용할 수 hello 인증서에 사용자의 일반 이름이 hello 연결 끝점을 일치 하지 않으면, `--strict-ssl-false` 다음 명령을 hello에 표시 된 대로 toobypass hello 확인:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Tooskip hello CA 확인, 원하는 경우 hello-거부-권한이 없음-거짓 매개 변수는 다음 명령을 hello에 표시 된 대로 추가할 수 있습니다. 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

연결 된 후 있어야 수 toorun와 다른 CLI 명령을 toointeract hello 클러스터입니다.

## <a name="deploying-your-service-fabric-application"></a>서비스 패브릭 응용 프로그램 배포

다음 명령을 toocopy, 등록 및 hello 서비스 패브릭 응용 프로그램을 시작 하는 hello를 실행 합니다.

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>응용 프로그램 업그레이드

hello 프로세스는 유사 toohello [Windows에 프로세스](service-fabric-application-upgrade-tutorial-powershell.md)).

프로젝트 루트 디렉터리에서 응용 프로그램을 빌드, 복사, 등록 및 만듭니다. 응용 프로그램 인스턴스 이름이 `fabric:/MySFApp`, 및 hello 형식이 MySFApp 이면 hello 명령을 다음과 같습니다.

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Hello tooyour 응용 프로그램을 변경 하 고 수정 하는 hello 서비스를 다시 작성을 확인 합니다.  업데이트 hello 서비스의 매니페스트 파일 (ServiceManifest.xml) hello 업데이트 버전으로 hello 서비스에 대 한 (및 코드 또는 구성 또는 수정한 데이터를 적절 하 게). 또한 hello 응용 프로그램에 대 한 버전 번호를 업데이트 하는 hello hello 응용 프로그램 매니페스트 (ApplicationManifest.xml)를 수정 하 고 수정 된 서비스 hello 합니다.  이제 복사 및 hello 다음 명령을 사용 하 여 업데이트 된 응용 프로그램을 등록 합니다.

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

이제, 다음 명령을 hello로 hello 응용 프로그램 업그레이드를 시작할 수 있습니다.

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

이제 SFX를 사용 하 여 hello 응용 프로그램 업그레이드를 모니터링할 수 있습니다. 잠시 후에 hello 응용 프로그램은 업데이트 되었습니다. 오류가 발생 하 여 업데이트 된 앱을 시도 하 고 서비스 패브릭에서 hello 자동 롤백 기능을 확인할 수도 있습니다.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>PFX tooPEM에서 그 반대로 변환합니다.

다른 환경에 있을 수 있는 로컬 컴퓨터 (Windows 또는 Linux) tooaccess 보안 클러스터의 tooinstall 인증서를 할 수 있습니다. 예를 들어 Windows 컴퓨터에서 그 반대의 보안된 Linux 클러스터를 액세스 하는 동안 해야 tooconvert 인증서 PFX tooPEM에서 그 반대의 합니다. 

PEM 파일 tooa PFX 파일을 다음 명령을 사용 하 여 hello에서 tooconvert:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

PFX 파일 tooa PEM 파일을 다음 명령을 사용 하 여 hello에서 tooconvert:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

너무 참조[OpenSSL 설명서](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) 대 한 자세한 내용은 합니다.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>문제 해결


### <a name="copying-of-hello-application-package-does-not-succeed"></a>Hello 응용 프로그램 패키지의 복사 실패

`openssh` 가 설치되어 있는지 확인합니다. 기본적으로 Ubuntu Desktop에는 설치되어 있지 않습니다. 다음 명령을 hello를 사용 하 여 설치 합니다.

```sh
sudo apt-get install openssh-server openssh-client**
```

Hello 문제가 계속 되 면 사용 하지 않도록 설정에 대 한 PAM ssh hello를 변경 하 여 시도 `sshd_config` hello 다음 명령을 사용 하 여 파일:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Hello 문제가 여전히 계속 되 면, 시도 hello 수가 늘어나면 ssh 세션 hello 다음 명령을 실행 하 여:

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

에 대 한 키를 사용 하 여 ssh 인증 (것과 반대로 toopasswords)으로 아직 지원 되지 (hello 플랫폼을 사용 하므로 ssh toocopy 패키지), 따라서 암호 인증을 대신 사용 합니다.

## <a name="next-steps"></a>다음 단계

[Hello 개발 환경을 설정 하 고 서비스 패브릭 응용 프로그램 tooa Linux 클러스터를 배포 합니다.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>관련 문서

* [Service Fabric 및 Azure CLI 2.0 시작](service-fabric-azure-cli-2-0.md)
