---
title: "Azure VM에 대 한 aaaDetailed SSH 문제 해결 | Microsoft Docs"
description: "더 자세한 문제 해결 단계 tooan Azure 가상 컴퓨터를 연결 하는 문제에 대 한 SSH"
keywords: "ssh 연결 거부,ssh 오류,azure ssh,SSH 연결 실패"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: b8e8be5f-e8a6-489d-9922-9df8de32e839
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: support-article
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 3f711e53a8251f8c06dbb589a258222566a4ae1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-ssh-troubleshooting-steps-for-issues-connecting-tooa-linux-vm-in-azure"></a>문제 해결 단계는 Azure에서 Linux VM tooa 연결 문제에 대 한 자세한 SSH
여러 가지가 있습니다 가능한 hello SSH 클라이언트 hello VM에서 수 tooreach hello SSH 서비스 되지 않을 수 있습니다. 더 hello를 통해 수행한 경우 [문제 해결 단계는 일반 SSH](troubleshoot-ssh-connection.md), toofurther 필요한 hello 연결 문제를 해결 합니다. 이 문서 과정을 안내해 자세한 문제 해결 단계 toodetermine hello SSH 연결 실패 하는 위치와 방법을 tooresolve 것입니다.

## <a name="take-preliminary-steps"></a>준비 단계 수행
hello 다음 그림에 사용 되는 hello 구성 요소입니다.

![SSH 서비스의 구성 요소를 보여주는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot1.png)

hello 다음 단계 수 hello 소스 hello 실패의 원인을 찾아내서 해결 방법 또는 솔루션을 파악 합니다.

1. Hello 포털에서 VM hello의 hello 상태를 확인 합니다.
   Hello에 [Azure 포털](https://portal.azure.com)선택, **가상 컴퓨터** > *VM 이름*합니다.

   hello hello VM에 대 한 상태 창 표시할지 **실행**합니다. 계산, 저장소 및 네트워크 리소스에 대 한 최근 활동 tooshow 아래로 스크롤하십시오.

2. 선택 **설정을** tooexamine 끝점, IP 주소, 네트워크 보안 그룹 및 기타 설정 합니다.

   hello VM에서 볼 수 있는 SSH 트래픽에 대해 정의 된 끝점과 있어야 **끝점** 또는  **[네트워크 보안 그룹](../../virtual-network/virtual-networks-nsg.md)**합니다. Resource Manager를 사용하여 만든 VM의 끝점은 네트워크 보안 그룹에 저장됩니다. 또한, 있는지 hello 규칙 적용된 toohello 네트워크 보안 그룹 추가 되었으며 hello 서브넷에서 참조 되 고 있는지 확인 합니다.

tooverify 네트워크 연결은 hello 구성 된 끝점을 확인 하 고 참조 하는 경우 HTTP 또는 다른 서비스와 같은 다른 프로토콜을 통해 VM hello에 도달할 수 있습니다.

이러한 단계 이후 hello SSH 연결을 다시 시도 하십시오.

## <a name="find-hello-source-of-hello-issue"></a>Hello 문제의 hello 소스 찾기
컴퓨터에 SSH 클라이언트 hello tooreach hello SSH 서비스 hello Azure VM tooissues 또는 hello 다음 영역에서에서 구성 오류 때문에 실패할 수 있습니다.

* [SSH 클라이언트 컴퓨터](#source-1-ssh-client-computer)
* [조직 에지 장치](#source-2-organization-edge-device)
* [클라우드 서비스 끝점 및 액세스 제어 목록(ACL)](#source-3-cloud-service-endpoint-and-acl)
* [네트워크 보안 그룹](#source-4-network-security-groups)
* [Linux 기반 Azure VM](#source-5-linux-based-azure-virtual-machine)

## <a name="source-1-ssh-client-computer"></a>발생지 1: SSH 클라이언트 컴퓨터
tooeliminate hello 오류의 hello 소스로 컴퓨터 SSH 연결 tooanother 온-프레미스를 만들 수 있는지를 확인 Linux 기반 컴퓨터입니다.

![SSH 클라이언트 컴퓨터 구성 요소를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot2.png)

Hello 연결에 실패 하면 hello에 나오는 문제에 따라 컴퓨터를 확인 합니다.

* 인바운드 또는 아웃 바운드 SSH 트래픽(TCP 22)을 차단하는 로컬 방화벽 설정
* SSH 연결을 방지하는 로컬에 설치된 클라이언트 프록시 소프트웨어
* SSH 연결을 방지하는 로컬에 설치된 네트워크 모니터링 소프트웨어
* 트래픽을 모니터링하거나 특정 유형의 트래픽을 허용하거나 허용하지 않는 다른 유형의 보안 소프트웨어

다음이 조건 중 하나를 적용 하는 경우 일시적으로 hello 소프트웨어를 사용 하지 않도록 설정 하 고 컴퓨터에 hello 연결을 차단 하 고 hello 이유 아웃는 SSH 연결 tooan 온-프레미스 컴퓨터 toofind를 시도 하십시오. 그런 다음 네트워크 관리자 toocorrect hello 소프트웨어 설정 tooallow SSH 연결을 사용 합니다.

인증서 인증을 사용 하는 경우 홈 디렉터리에 이러한 사용 권한을 toohello.ssh 폴더 있는지 확인 합니다.

* Chmod 700 ~/.ssh
* Chmod 644 ~/.ssh/\*.pub
* Chmod 600 ~/.ssh/id_rsa(또는 개인 키가 저장되어 있는 기타 파일)
* Chmod 644 ~/.ssh/known_hosts (toovia SSH를 연결 하는 호스트 포함)

## <a name="source-2-organization-edge-device"></a>발생지 2: 조직 에지 장치
tooeliminate hello 오류의 hello 소스로 사용자 조직에 지 장치 toohello 인터넷에 직접 연결에 있는 컴퓨터에 SSH 연결 tooyour Azure VM을 만들 수 있음을 확인 합니다. Hello VM에 사이트 간 VPN 이나 Azure express 경로 연결을 통해 액세스 하는 경우 너무 건너뜁니다[소스 4: 네트워크 보안 그룹](#nsg)합니다.

![조직 에지 장치를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot3.png)

직접 연결 된 toohello 인터넷 되는 컴퓨터에 없을 경우 자체 리소스 그룹 또는 클라우드 서비스에 새 Azure VM 만들고 사용 합니다. 자세한 내용은 [Azure에서 Linux를 실행하는 가상 컴퓨터 만들기](quick-create-cli.md)를 참조하세요. 테스트와 완료 되 면 hello 리소스 그룹이 나 VM 및 클라우드 서비스를 삭제 합니다.

Toohello 인터넷에 직접 연결에 있는 컴퓨터와 SSH 연결을 만들 수 있습니다, 경우에 대 한 사용자 조직에 지 장치를 확인 합니다.

* 인터넷 hello 사용 하 여 SSH 트래픽을 차단 하는 내부 방화벽
* SSH 연결을 방지하는 프록시 서버
* 경계 네트워크의 장치에서 실행되는, SSH 연결을 방지하는 침입 검색 또는 네트워크 모니터링 소프트웨어

인터넷 hello로 조직 가장자리 장치 tooallow SSH 트래픽 네트워크 관리자 toocorrect hello 설정과 함께 작동 합니다.

## <a name="source-3-cloud-service-endpoint-and-acl"></a>발생지 3: 클라우드 서비스 끝점 및 ACL
> [!NOTE]
> 이 소스 hello 클래식 배포 모델을 사용 하 여 만든 tooVMs만 적용 됩니다. 리소스 관리자를 사용 하 여 만든 Vm에 대 한 건너뛸 너무[원본 4: 네트워크 보안 그룹](#nsg)합니다.

다른 Azure VM에 동일을 hello tooeliminate hello 클라우드 서비스 끝점 및 hello 오류의 hello 소스로 ACL 확인 가상 네트워크는 SSH 연결 tooyour VM을 만들 수 있습니다.

![클라우드 서비스 끝점 및 ACL을 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot4.png)

다른 VM hello에 없는 경우 동일한 가상 네트워크를 쉽게 만들 수 있습니다 하나입니다. 자세한 내용은 참조 [hello CLI를 사용 하 여 Azure에서 Linux VM을 만들](quick-create-cli.md)합니다. 삭제 테스트와 완료 되 면 추가 VM hello 합니다.

에 VM으로 SSH 연결을 만들 수 있으면 hello 동일한 가상 네트워크, 영역을 다음 hello 확인:

* **hello hello 대상 VM에서 SSH 트래픽에 대 한 끝점 구성입니다.** hello hello 끝점의 개인 TCP 포트는 hello SSH hello VM에서 서비스 수신 hello TCP 포트를 일치 해야 합니다. (hello 기본 포트는 22). 선택 하 여 hello Azure 포털에에서 hello SSH TCP 포트 번호를 확인 **가상 컴퓨터** > *VM 이름* > **설정**  >  **끝점**합니다.
* **hello hello 대상 가상 컴퓨터에 SSH 트래픽 끝점 hello에 대 한 ACL 선택 합니다.** ACL 허용 또는 원본 IP 주소에 기반 하는 hello 인터넷에서에서 들어오는 트래픽을 거부 toospecify가 있습니다. 잘못 구성 된 Acl 들어오는 SSH 트래픽 toohello 끝점을 방지할 수 있습니다. Hello 공용 IP 주소에 프록시 또는 다른 지 서버에서 들어오는 트래픽을 허용 하 여 Acl tooensure를 확인 합니다. 자세한 내용은 [네트워크 ACL(액세스 제어 목록) 정보](../../virtual-network/virtual-networks-acl.md)를 참조하세요.

tooeliminate hello 끝점 hello 문제의 원인으로 hello 현재 끝점을 제거 다른 끝점을 만들고 hello SSH 이름 (TCP 포트 22 hello 공용 및 개인 포트 번호에 대 한)를 지정 합니다. 자세한 내용은 [Azure의 가상 컴퓨터에 끝점 설정](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.

<a id="nsg"></a>

## <a name="source-4-network-security-groups"></a>발생지 4: 네트워크 보안 그룹
네트워크 보안 그룹 사용 toohave 허용 된 인바운드 및 아웃 바운드 트래픽 더 세부적으로 제어 합니다. Azure 가상 네트워크의 서브넷 및 클라우드 서비스에 적용되는 규칙을 만들 수 있습니다. 사용자 네트워크 보안 그룹 규칙 tooensure 해당 SSH 트래픽 tooand를 인터넷 ï ´ ù hello에서 확인 하십시오.
자세한 내용은 [네트워크 보안 그룹 정보](../../virtual-network/virtual-networks-nsg.md)를 참조하세요.

또한 IP 확인 toovalidate hello NSG 구성을 사용할 수 있습니다. 자세한 내용은 [Azure 네트워크 모니터링 개요](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)를 참조하세요. 

## <a name="source-5-linux-based-azure-virtual-machine"></a>발생지 5: Linux 기반 Azure 가상 컴퓨터
가능한 문제 hello 마지막 소스는 hello Azure 가상 컴퓨터 자체입니다.

![Linux 기반 Azure 가상 컴퓨터를 강조하는 다이어그램](./media/detailed-troubleshoot-ssh-connection/ssh-tshoot5.png)

아직 수행 하지 않은 경우 hello 지침에 따라 [tooreset 암호 또는 Linux 기반 가상 컴퓨터에 대 한 SSH](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

컴퓨터에서 다시 연결을 시도하세요. 문제가 계속 발생 hello 다음은 일부 hello 관련 문제입니다.

* SSH 서비스 hello hello 대상 가상 컴퓨터에서 실행 되지 않습니다.
* hello SSH 서비스는 TCP 포트 22에서 수신 하지 않는 합니다. tootest, 로컬 컴퓨터의 텔넷 클라이언트를 설치 하 고 실행 "텔넷 *cloudServiceName*. cloudapp.net 22"입니다. 이 단계는 hello 가상 컴퓨터 인바운드 및 아웃 바운드 통신 toohello SSH 끝점을 허용 하는 경우를 확인 합니다.
* hello hello 대상 가상 컴퓨터에서 로컬 방화벽에 인바운드 또는 아웃 바운드 SSH 트래픽을 방지 하는 규칙이 있습니다.
* 침입 검색 또는 모니터링 소프트웨어 hello Azure 가상 컴퓨터에서 실행 되는 네트워크 SSH 연결을 차단 중인 합니다.

## <a name="additional-resources"></a>추가 리소스
응용 프로그램 액세스 문제를 해결 하는 방법에 대 한 자세한 내용은 참조 [문제 해결 액세스 tooan 응용 프로그램이 Azure 가상 컴퓨터에서 실행 중인](troubleshoot-app-connection.md)
