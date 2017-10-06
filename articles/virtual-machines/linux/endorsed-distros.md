---
title: "aaaEndorsed 배포판의 Linux | Microsoft Docs"
description: "Ubuntu, CentOS, Oracle 및 SUSE 관련 지침을 포함하여 Azure에서 Linux의 인증 배포를 수행하는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Azure 보증 배포판의 Linux
파트너는 hello Azure Marketplace에서에서 Linux 이미지를 제공 합니다. 여기서 사용 하는 다양 한 Linux 커뮤니티 tooadd 더 많은 버전 toohello 보증 메일 그룹입니다. Hello 그 동안가 아닌 분포에 대 한 hello Marketplace에서에서 사용할 수 있는 가져올 수 있습니다 항상 직접 Linux에서 hello 지침에 따라 [만들기 및 업로드 hello Linux 운영 체제를포함하는가상하드디스크](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>지원되는 배포판 및 버전
hello 다음 표에 hello Linux 배포판 및 Azure에서 지원 되는 버전입니다. 너무 참조[Microsoft Azure에서 Linux에 대 한 지원을 이미지](https://support.microsoft.com/en-us/kb/2941892) 대 한 자세한 내용은 합니다.

Hyper-v와 Azure에 대 한 hello Linux Integration Services (LIS) 드라이버는 Microsoft 기여 직접 toohello 업스트림 Linux 커널을 커널 모듈입니다.  기본적으로 일부 LIS 드라이버 hello 분포의 커널으로 빌드됩니다. RHEL(Red Hat Enterprise)/CentOS를 기반으로 둔 이전 배포는 [Linux Integration Services Version 4.1 for Hyper-V](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)(Hyper-V용 Linux Integration Services 버전 4.1)에서 별도의 다운로드로 제공됩니다. 참조 [Linux 커널 요구 사항](create-upload-generic.md#linux-kernel-requirements) hello LIS 드라이버에 대 한 자세한 내용은 합니다.

hello Azure Linux 에이전트 hello Azure 마켓플레이스 이미지에 이미 설치 전 되며 hello 분포의 패키지 저장소에서 일반적으로 사용할 수 있습니다. 소스 코드는 [GitHub](https://github.com/azure/walinuxagent)에서 찾을 수 있습니다.

| 배포 | 버전 | 드라이버 | 에이전트 |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3 이상, 7.0 이상 |CentOS 6.3: [LIS 다운로드](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4+: 커널에 있음 |패키지: "WALinuxAgent"의 [리포지토리](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/)에 있음 <br/>소스 코드: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0 이상 |커널에 있음 |소스 코드: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7.9 이상, 8.2 이상 |커널에 있음 |패키지: "waagent"에서 리포지토리의  <br/>소스 코드: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4 이상, 7.0 이상 |커널에 있음 |패키지: "WALinuxAgent"의 리포지토리에 있음  <br/>소스 코드: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7+, 7.1+ |커널에 있음 |패키지: "WALinuxAgent"의 리포지토리에 있음  <br/>소스 코드: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SAP용 SLES<br>11 SP4<br>12 SP1+|커널에 있음 |패키지:<p> 11의 경우 [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) 리포지토리에 있음<br>12의 경우 "python-azure-agent" 아래의 "공용 클라우드" 모듈에 포함됨<br/>소스 코드: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE Leap 42.1+ |커널에 있음 |패키지: "python-azure-agent"의 [Cloud:Tools](https://build.opensuse.org/project/show/Cloud:Tools) 리포지토리에 있음 <br/>소스 코드: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |커널에 있음 |패키지: "WALinuxAgent"의 리포지토리에 있음  <br/>소스 코드: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>파트너

### <a name="coreos"></a>CoreOS
[https://coreos.com/docs/running-coreos/cloud-providers/azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

Hello CoreOS 웹 사이트:

*CoreOS는 보안, 일관성 및 안정성을 위해 설계되었습니다. Yum 통해 또는 apt 패키지를 설치 하는 대신 CoreOS Linux 컨테이너 toomanage 서비스에서 사용 더 높은 수준의 추상화 합니다. 단일 서비스 코드 및 모든 종속성이 하나 또는 여러 CoreOS 컴퓨터에서 실행할 수 있는 컨테이너 내에서 패키지됩니다.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ는 독립적인 컨설팅 및 무료 소프트웨어를 사용 하 여 hello 개발 및 전문 솔루션의 구현을 전문으로 하는 서비스 회사입니다. 시장을 선도하는 오픈 소스 전문 회사인 Credative는 지원을 받는 많은 IT 부서들로부터 국제적인 명성을 얻고 있습니다. 현재 Credativ는 Microsoft와 협력 관계를 맺고 Debian 8(Jessie) 및 Debian 7(Wheezy) 이전 버전에 해당하는 Debian 이미지를 준비 중입니다. 이미지를 모두 Azure에서 특별히 설계 된 toorun 되며 hello 플랫폼을 통해 쉽게 관리할 수 있습니다. Credativ는 hello 장기적인 유지 관리 하 고 hello Debian 이미지의 오픈 소스 지원 센터를 통해 Azure에 대 한 업데이트에 지원 합니다.

### <a name="oracle"></a>Oracle
[http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Oracle의 전략은 광범위 한 공용 및 사설 클라우드를 위한 솔루션 포트폴리오 toooffer입니다. hello 전략 선택 및 Oracle 클라우드에서 Oracle 소프트웨어 및 클라우드가 다른 배포 방법에 대 한 유연성 고객을 제공 합니다. Microsoft 공용 및 개인 클라우드에서 고객 toodeploy Oracle 소프트웨어의 인증 및 Oracle에서 지원 하 여 hello 정확 수 있도록 하는 Microsoft와 oracle의 협력 합니다.  Oracle 공용 및 사설 클라우드 솔루션에 대한 Oracle의 이행 및 투자는 변하지 않습니다.

### <a name="red-hat"></a>Red Hat
[http://www.redhat.com/en/partners/strategic-alliance/microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

세계에서 선두 제공 오픈 소스 솔루션의 hello, Red Hat 90% 이상 Fortune 500 회사의 비즈니스 문제를 해결, IT 및 비즈니스 전략 기술의 hello 미래를 준비 합니다. 이를 위해 Red Hat은 개방형 비즈니스 모델과 경제적이고 예측 가능한 구독 모델을 통해 안전한 솔루션을 제공합니다.

### <a name="suse"></a>SUSE
[http://www.suse.com/suse-linux-enterprise-server-on-azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server on Azure는 클라우드 컴퓨팅에 대해 우수한 안정성과 보안을 제공하는 검증된 플랫폼입니다. SUSE의 다양 한 Linux 플랫폼 원활 하 게 통합 되어 Azure 클라우드 서비스 toodeliver 쉽게 관리할 수 있는 클라우드 환경 있습니다. SUSE Linux Enterprise Server에 대 한 1, 800 개 이상의 독립 소프트웨어 공급 업체에서 인증 된 응용 프로그램 이상 9,200, SUSE에서는 되었는지 확인 hello 데이터 센터에서 지원 되는 실행 되는 작업에 Azure에 자신 있게 배포할 수 있습니다.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/azure](http://www.ubuntu.com/cloud/azure)

Canonical 엔지니어링과 개방형 커뮤니티 거버넌스로 인해 소비자용 개인 클라우드 서비스를 비롯한 클라이언트, 서버 및 클라우드 컴퓨팅에서 Ubuntu가 성공할 수 있었습니다. Canonical의 비전 전화 toocloud에서 Ubuntu에서 통합 된 무료 플랫폼의 hello 전화, 태블릿, TV, 및 데스크톱에 대 한 일관 된 인터페이스의 제품군을 제공합니다. 이 비전 Ubuntu hello 가전 공용 클라우드 공급자 toohello 결정권자에서 다양 한 기관에 대 한 첫 번째 선택 및 개별 기술자 간에 즐겨찾기를 만듭니다.

개발자와 hello 전 세계 엔지니어링 센터 Canonical는 소프트웨어 개발자가 toobring Ubuntu 솔루션 toomarket Pc, 서버 및 핸드헬드 장치에 대 한 하드웨어 제조업체, 콘텐츠 공급자와 고유 하 게 위치 지정된 toopartner입니다.
