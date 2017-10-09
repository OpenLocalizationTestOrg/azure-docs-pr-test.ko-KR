---
title: "Linux VM 에이전트 개요 aaaAzure | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall 및 Linux 에이전트 (waagent) toomanage Azure 패브릭 컨트롤러와 가상 컴퓨터의 상호 작용을 구성 합니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>이해 및 hello Azure Linux 에이전트를 사용 합니다.
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>소개
hello Microsoft Azure Linux 에이전트 (waagent) Linux 및 FreeBSD 프로비저닝, 및 hello Azure 패브릭 컨트롤러와 VM의 상호 작용을 관리 합니다. Linux 및 FreeBSD IaaS 배포에 대 한 기능을 수행 하는 hello를 제공 합니다.

> [!NOTE]
> Hello Azure Linux 에이전트 참조 [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) 추가 세부 정보에 대 한 합니다.
> 
> 

* **이미지 프로비전**
  
  * 사용자 계정 만들기
  * SSH 인증 유형 구성
  * SSH 공개 키 및 키 쌍 배포
  * 설정 hello 호스트 이름
  * 게시 hello 호스트 이름 toohello 플랫폼 DNS
  * 보고 SSH 호스트 키 지문 toohello 플랫폼
  * 리소스 디스크 관리
  * 서식 지정 및 hello 리소스 디스크를 탑재 합니다.
  * 스왑 공간 구성
* **네트워킹**
  
  * 경로 tooimprove 호환 플랫폼 DHCP 서버 관리
  * Hello 네트워크 인터페이스 이름의 hello 안정성 보장
* **커널**
  
  * 가상 NUMA 구성(커널에 대해 사용 안 함 <2.6.37)
  * /dev/random의 Hyper-V 엔트로피 이용
  * Hello 루트 장치 (원격 일 수도 있음)에 대 한 SCSI 제한 구성
* **진단**
  
  * 콘솔 리디렉션 toohello 직렬 포트
* **SCVMM 배포**
  
  * 검색 하 고 System Center Virtual Machine Manager 2012 R2 환경에서 실행 하는 경우 Linux 용 hello VMM 에이전트를 시작 되도록
* **VM 확장**
  
  * Linux VM (IaaS) tooenable 소프트웨어 및 구성 자동화로 Microsoft 및 협력 업체에서 작성 된 구성 요소를 삽입 합니다.
  * [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>통신
두 개의 채널을 통해 hello 정보 흐름 hello 플랫폼 toohello 에이전트에서 발생합니다.

* IaaS 배포를 위해 부팅 시 연결된 DVD. 이 DVD hello 실제 SSH 키 쌍 이외의 모든 프로 비전 정보를 포함 하는 규격 OVF 구성 파일을 포함 합니다.
* REST API를 노출 하는 TCP 끝점 tooobtain 배포 및 토폴로지 구성을 사용 합니다.

## <a name="requirements"></a>요구 사항
hello 다음과 같은 시스템 테스트를 거쳐 Azure Linux 에이전트 hello로 toowork 알려진:

> [!NOTE]
> 이 목록은 여기에서 설명한 대로 hello 공식 목록 hello Microsoft Azure 플랫폼에서 지원 되는 시스템에서 달라질 수 있습니다: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3 이상
* Red Hat Enterprise Linux 6.7 이상
* Debian 7.0 이상
* Ubuntu 12.04 이상
* openSUSE 12.3 이상
* SLES 11 SP3 이상
* Oracle Linux 6.4 이상

기타 지원되는 시스템:

* FreeBSD 10 이상(Azure Linux 에이전트 v2.0.10 이상)

hello Linux 에이전트 제대로 순서 toofunction에 일부 시스템 패키지에 따라 다릅니다.:

* Python 2.6 이상
* OpenSSL 1.0 이상
* OpenSSH 5.3 이상
* 파일 시스템 유틸리티: sfdisk, fdisk, mkfs, parted
* 암호 도구: chpasswd, sudo
* 텍스트 처리 도구: sed, grep
* 네트워크 도구: ip-route
* UDF 파일 시스템 탑재에 대한 커널 지원

## <a name="installation"></a>설치
분포의 패키지 저장소는 RPM 또는 DEB 패키지를 사용 하 여 설치는 설치 및 hello Azure Linux 에이전트 업그레이드의 기본 설정 하는 hello 메서드입니다. 모든 hello [배포 공급자 보증](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) hello Azure Linux 에이전트 패키지를 해당 이미지 및 저장소에 통합 합니다.

Hello에 toohello 문서를 참조 하십시오 [GitHub의 Azure Linux 에이전트 리포지토리](https://github.com/Azure/WALinuxAgent) 소스 또는 toocustom 위치나 접두사에서 설치 하는 등의 고급 설치 옵션에 대 한 합니다.

## <a name="command-line-options"></a>명령줄 옵션
### <a name="flags"></a>플래그
* verbose: 지정한 명령의 세부 정보 표시를 늘립니다.
* force: 일부 명령의 대화형 확인을 건너뜁니다.

### <a name="commands"></a>명령
* 도움말: hello 지원 명령 및 플래그를 나열 합니다.
* 프로 비전 해제: tooclean hello 시스템을 시도 하 고 다시 프로 비전에 맞게 사용할 수 있습니다. 이 작업 hello 다음을 삭제 합니다.
  
  * 모든 SSH 호스트 키 (Provisioning.RegenerateSshHostKeyPair 'y' hello 구성 파일의 경우)
  * /etc/resolv.conf의 Nameserver 구성
  * /Etc/shadow (Provisioning.DeleteRootPassword 'y' hello 구성 파일의 경우)의 루트 암호
  * 캐시된 DHCP 클라이언트 임대
  * 다시 설정 합니다. 호스트 이름 toolocalhost.localdomain

> [!WARNING]
> 프로 비전 해제 해당 hello 이미지는 중요 한 정보를 모두 선택 취소 하 고 재배포를 위해 적합 한 보장 하지 않습니다.
> 
> 

* 프로 비전 해제 + 사용자:-프로 비전 해제 (위) 아래에 있는 모든 수행 하 고도 (/var/lib/waagent에서 가져온) hello 마지막 프로 비전 된 사용자 계정을 삭제 하 고 연결 된 데이터입니다. Azure에서 이전에 프로비전한 이미지의 프로비전을 해제하여 이미지를 캡처하고 다시 사용할 수 있도록 하는 경우에 이 매개 변수를 사용합니다.
* 버전: waagent의 hello 버전을 표시 합니다
* serialconsole: GRUB toomark ttyS0 구성 (첫 번째 직렬 포트 hello) hello 부팅 콘솔로 합니다. 이렇게 하면 커널 부팅 로그 디버깅에 사용할 수 있는 전송 toothe 직렬 포트를 합니다.
* 디먼: waagent hello 플랫폼과 상호 작용을 데몬 toomanage로 실행 합니다. 이 인수는 hello waagent init 스크립트에 지정 된 toowaagent입니다.
* start: waagent를 백그라운드 프로세스로 실행

## <a name="configuration"></a>구성
구성 파일 (/ etc/waagent.conf) 컨트롤 hello waagent의 동작입니다. 다음은 샘플 구성 파일입니다.

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

hello 다양 한 구성 옵션은 아래에서 자세히 설명 합니다. 구성 옵션으로 부울, 문자열 또는 정수의 세 가지 형식이 있습니다. "y" 또는 "n"으로 hello 부울 구성 옵션을 지정할 수 있습니다. 안녕 특별 한 키워드 "None" 일부 문자열 형식 구성 항목에 설명 된 대로 아래에 사용할 수 있습니다.

**Provisioning.Enabled:**  
형식: Boolean  
기본값: y

이 사용자 tooenable hello를 허용 하거나 hello hello 에이전트의 기능을 프로 비전을 사용 하지 않도록 설정 합니다. 유효한 값은 "y" 또는 "n"입니다. 프로 비전을 해제 하면 SSH 호스트 및 사용자 키 hello 이미지에는 유지 하 고 hello Azure 프로 비전 API에에서 지정 된 모든 구성 무시 됩니다.

> [!NOTE]
> hello `Provisioning.Enabled` 프로 비전에 대 한 클라우드 초기화를 사용 하는 클라우드 이미지와 Ubuntu 너무 "n" 매개 변수 기본값입니다.
> 
> 

**Provisioning.DeleteRootPassword:**  
형식: Boolean  
기본값: n

Hello/등/섀도 파일에 hello 루트 암호를 설정 하는 동안 지워진 경우 hello 프로 비전 프로세스입니다.

**Provisioning.RegenerateSshHostKeyPair:**  
형식: Boolean  
기본값: y

집합에 모든 SSH 호스트 키 쌍 (예: ecdsa, dsa 및 rsa) 하는 동안 삭제 되 면 hello /etc/ssh/에서 프로 비전 프로세스입니다. 그리고 새로운 단일 키 쌍이 생성됩니다.

hello 새로운 키 쌍에 대 한 암호화 유형 적용 hello가 hello Provisioning.SshHostKeyPairType 항목 구성할 수 있습니다. 일부 배포를 다시 만듭니다 누락 된 모든 암호화 종류에 대 한 SSH 키 쌍 (예: 다시 부팅) 시 hello SSH 디먼이 다시 시작 되 면 note 하십시오.

**Provisioning.SshHostKeyPairType:**  
형식: String  
기본값: rsa

Tooan hello SSH 디먼이 hello 가상 컴퓨터에서 지원 되는 암호화 알고리즘 유형을 설정할 수 있습니다. 일반적으로 지원 되는 hello 값은 "rsa", "dsa" 및 "ecdsa"입니다. Windows의 "putty.exe"는 "ecdsa"를 지원하지 않습니다. 따라서 Windows tooconnect tooa Linux 배포에서 toouse putty.exe 하려는 경우에 사용 하십시오 "rsa" 또는 "dsa".

**Provisioning.MonitorHostName:**  
형식: Boolean  
기본값: y

집합 경우 waagent 됩니다 (hello "hostname" 명령에서 반환 된)을 호스트 이름 변경에 대 한 hello Linux 가상 컴퓨터를 모니터링할 고 hello 이미지 tooreflect hello 변경에서 네트워킹 구성 hello를 자동으로 업데이트 합니다. 순서 toopush hello 이름에서 toohello DNS 서버를 변경, 네트워킹 hello 가상 컴퓨터 다시 시작 됩니다. 이 때문에 인터넷 연결이 잠시 끊어집니다.

**Provisioning.DecodeCustomData**  
형식: Boolean  
기본값: n

설정되면 waagent는 Base64에서 CustomData를 디코딩합니다.

**Provisioning.ExecuteCustomData**  
형식: Boolean  
기본값: n

설정되면 waagent는 프로비전 후에 CustomData를 실행합니다.

**Provisioning.PasswordCryptId**  
형식:String  
기본값: 6

암호 해시를 생성할 때 암호화에 사용되는 알고리즘입니다.  
 1 - MD5  
 2a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
형식:String  
기본값: 10

암호 해시를 생성할 때 사용되는 임의 salt의 길이입니다.

**ResourceDisk.Format:**  
형식: Boolean  
기본값: y

설정, hello 플랫폼에서 제공 하는 hello 리소스 디스크 포맷 하 고 됩니다 "ResourceDisk.Filesystem"에서 hello 사용자가 요청한 hello 파일 시스템 형식 "ntfs" 이외의 값 이면 waagent을 통해 탑재 된 합니다. Linux (83) 형식의 단일 파티션은 사용 가능 하 게 hello 디스크에 있습니다. 이 파티션이 탑재될 수 있는 경우에는 포맷되지 않습니다.

**ResourceDisk.Filesystem:**  
형식: String  
기본값: ext4

Hello 리소스 디스크에 대 한 hello 파일 시스템 형식을 지정합니다. 지원되는 값은 Linux 배포에 따라 달라집니다. Hello 문자열 X, 다음 mkfs 경우. X는 hello Linux 이미지에 존재 해야 합니다. 일반적으로 SLES 11 이미지는 'ext3'을 사용해야 합니다. 여기에서 FreeBSD 이미지는 'ufs2'를 사용해야 합니다.

**ResourceDisk.MountPoint:**  
형식: String  
기본값: /mnt/resource 

Hello 리소스 디스크 탑재 hello 경로 지정 합니다. 해당 하는 hello 리소스 디스크는 한 *임시* , 디스크 및 hello VM 프로 비전 해제 된 경우 비울 수 있습니다.

**ResourceDisk.MountOptions**  
형식: String  
기본값: 없음

디스크 탑재 옵션 전달 toobe toohello 탑재-o 명령을 지정합니다. 쉼표로 구분된 값 목록입니다(예: 'nodev,nosuid'). 자세한 내용은 mount(8)를 참조하세요.

**ResourceDisk.EnableSwap:**  
형식: Boolean  
기본값: n

경우 설정, 스왑 파일 (/ 스왑 파일) hello 리소스 디스크에 생성 되 고 toohello 시스템 스왑 공간을 추가 합니다.

**ResourceDisk.SwapSizeMB:**  
형식: Integer  
기본값: 0

hello 크기 (메가바이트)에서 hello 스왑 파일입니다.

**Logs.Verbose:**  
형식: Boolean  
기본값: n

설정한 경우 로그에 대한 세부 정보 표시가 향상됩니다. Waagent은 too/var/log/waagent.log를 로그 및 hello 시스템 logrotate 기능 toorotate 로그를 활용 합니다.

**OS.EnableRDMA**  
형식: Boolean  
기본값: n

설정, hello 에이전트는 시도 tooinstall 하 고 다음 기반 하드웨어 hello hello 펌웨어 hello 버전과 일치 하는 RDMA 커널 드라이버를 로드 합니다.

**OS.RootDeviceScsiTimeout:**  
형식: Integer  
기본값: 300

Hello SCSI 제한 시간 (초) hello OS 디스크 및 데이터 드라이브에서 구성 됩니다. 설정 하지 않으면 hello 시스템 기본값이 사용 됩니다.

**OS.OpensslPath:**  
형식: String  
기본값: 없음

이 사용 되는 toospecify 암호화 작업에 대 한 openssl 이진 toouse hello에 대 한 대체 경로 수 있습니다.

**HttpProxy.Host, HttpProxy.Port**  
형식: String  
기본값: 없음

설정 하면, hello 에이전트는 사용이 프록시 서버 tooaccess hello 인터넷 합니다. 

## <a name="ubuntu-cloud-images"></a>Ubuntu 클라우드 이미지
Ubuntu 클라우드 이미지를 활용 하는 참고 [클라우드 init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform 그렇지 않으면으로 하 여 관리할 수 있는 많은 구성 작업 hello Azure Linux 에이전트입니다.  다음 차이점 hello를 note 하십시오.

* **Provisioning.Enabled** Ubuntu 클라우드 이미지와 클라우드 init tooperform 작업 프로 비전을 사용 하는 "n" 너무 기본값입니다.
* 구성 매개 변수 뒤 hello 클라우드 init는 toomanage hello 리소스 디스크 및 스왑 공간을 사용 하는 Ubuntu 클라우드 이미지에 영향을 미치지:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* 프로 비전 시 스왑 Ubuntu 클라우드 이미지에는 공간 및 hello 리소스 tooconfigure hello 리소스 디스크 탑재 지점를 참조 하십시오.
  
  * [Ubuntu Wiki: Swap 파티션 구성](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Azure 가상 컴퓨터에 사용자 지정 데이터 삽입](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

