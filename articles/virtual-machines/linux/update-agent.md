---
title: "GitHub에서 Azure Linux 에이전트 aaaUpdate hello | Microsoft Docs"
description: "자세한 내용은 방법 tooupdate Azure toohello GitHub에서 최신 버전의 Linux VM에 대 한 Azure Linux 에이전트"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Tooupdate VM에 Azure Linux 에이전트를 hello 하는 방법

tooupdate 프로그램 [Azure Linux 에이전트](https://github.com/Azure/WALinuxAgent) Azure에서 Linux VM에서 이미 있어야 합니다.

- Azure에서 실행 중인 Linux VM
- 연결 toothat Linux VM SSH를 사용 하 여 합니다.

항상 확인 해야 hello Linux 배포판 저장소의 패키지에 대해 먼저 합니다. 그러나 있습니다 사용할 수 있는 hello 패키지 hello 최신 버전을 사용 하지 못할 자동 업데이트를 사용 하도록 설정 하면 hello Linux 에이전트는 항상 hello 최신 업데이트 받습니다. Hello 패키지 관리자에서 설치 문제가 있는 해야 hello distro 공급 업체에서 지원을 검색 해야 합니다.

## <a name="updating-hello-azure-linux-agent"></a>Hello Azure Linux 에이전트를 업데이트합니다.

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>현재 패키지 버전 확인

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>패키지 캐시 업데이트

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Hello 최신 패키지 버전 설치

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>자동 업데이트가 활성화되었는지 확인

사용 하는 경우 먼저 toosee를 확인 합니다.

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled'를 찾습니다. 이 출력이 표시되는 경우 활성화되었습니다.

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 실행:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hello waagent 서비스를 다시 시작

#### <a name="restart-agent-for-1404"></a>14.04에 대한 에이전트 다시 시작

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>16.04 / 17.04에 대한 에이전트 다시 시작

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 “Wheezy”

#### <a name="check-your-current-package-version"></a>현재 패키지 버전 확인

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>패키지 캐시 업데이트

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Hello 최신 패키지 버전 설치

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>에이전트 자동 업데이트 활성화
이 버전의 Debian이 2.0.16 이상의 버전을 포함하지 않으므로 AutoUpdate를 사용할 수 없습니다. hello 패키지가 최신 상태 인지 표시 명령 위에 hello hello 출력 됩니다.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 “Jessie” / Debian 9 “Stretch”

#### <a name="check-your-current-package-version"></a>현재 패키지 버전 확인

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>패키지 캐시 업데이트

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Hello 최신 패키지 버전 설치

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>자동 업데이트가 활성화되었는지 확인 

사용 하는 경우 먼저 toosee를 확인 합니다.

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled'를 찾습니다. 이 출력이 표시되는 경우 활성화되었습니다.

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 실행:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hello waagent 서비스를 다시 시작

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>Redhat / CentOS

### <a name="rhelcentos-6"></a>RHEL/CentOS 6

#### <a name="check-your-current-package-version"></a>현재 패키지 버전 확인

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>사용 가능한 업데이트 확인

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Hello 최신 패키지 버전 설치

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>자동 업데이트가 활성화되었는지 확인 

사용 하는 경우 먼저 toosee를 확인 합니다.

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled'를 찾습니다. 이 출력이 표시되는 경우 활성화되었습니다.

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 실행:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hello waagent 서비스를 다시 시작

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL/CentOS 7

#### <a name="check-your-current-package-version"></a>현재 패키지 버전 확인

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>사용 가능한 업데이트 확인

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Hello 최신 패키지 버전 설치

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>자동 업데이트가 활성화되었는지 확인 

사용 하는 경우 먼저 toosee를 확인 합니다.

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled'를 찾습니다. 이 출력이 표시되는 경우 활성화되었습니다.

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 실행:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hello waagent 서비스를 다시 시작

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>현재 패키지 버전 확인

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>사용 가능한 업데이트 확인

위의 출력 hello hello 패키지 toodate 중일 경우에 표시 됩니다.

#### <a name="install-hello-latest-package-version"></a>Hello 최신 패키지 버전 설치

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>자동 업데이트가 활성화되었는지 확인 

사용 하는 경우 먼저 toosee를 확인 합니다.

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled'를 찾습니다. 이 출력이 표시되는 경우 활성화되었습니다.

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 실행:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hello waagent 서비스를 다시 시작

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>현재 패키지 버전 확인

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>사용 가능한 업데이트 확인

위의 hello hello 출력을이 hello 패키지 키는 최신 인지 하면 표시 됩니다.

#### <a name="install-hello-latest-package-version"></a>Hello 최신 패키지 버전 설치

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>자동 업데이트가 활성화되었는지 확인 

사용 하는 경우 먼저 toosee를 확인 합니다.

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled'를 찾습니다. 이 출력이 표시되는 경우 활성화되었습니다.

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 실행:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Hello waagent 서비스를 다시 시작

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 및 7

Oracle Linux에 대 한 확인 해당 hello `Addons` 리포지토리를 사용할 수 있습니다. Tooedit hello 파일 선택 `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) 또는 `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), hello 줄을 변경 하 고 `enabled=0` 너무`enabled=1` 아래 **[ol6_addons]** 또는 **[ol7_addons]** 이 파일입니다.

그런 다음 tooinstall hello 최신 버전의 hello Azure Linux 에이전트 유형:

```bash
sudo yum install WALinuxAgent
```

Hello 추가 기능 저장소를 찾을 수 없는 경우 tooyour Oracle Linux 버전에 따라.repo 파일의 hello 끝에이 줄을 간단히 추가할 수 있습니다.

Oracle Linux 6 가상 컴퓨터의 경우:

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Oracle Linux 7 가상 컴퓨터의 경우:

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

그런 다음 입력합니다.

```bash
sudo yum update WALinuxAgent
```

일반적으로 필요한 경우 tooinstall 필요한 몇 가지 이유로 https://github.com를 직접 사용 하 여 hello 뒤에서 단계를 제외한 모든입니다.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>배포에 대 한 에이전트 패키지가 있는 hello Linux 에이전트를 업데이트 합니다.

Wget (Redhat, CentOS 및 Oracle Linux 버전 6.4 및 6.5 같이 기본적으로 설치 하지 않는 일부 배포판은) 입력 하 여 설치 `sudo yum install wget` hello 명령줄에서.

### <a name="1-download-hello-latest-version"></a>1. Hello 최신 버전 다운로드
열기 [GitHub의 Azure Linux 에이전트의 릴리스 hello](https://github.com/Azure/WALinuxAgent/releases) 웹 페이지 및 hello 최신 버전 번호에 대해 알아봅니다. `waagent --version`을 입력하면 현재 버전을 찾을 수 있습니다.

#### <a name="for-version-22x-or-later-type"></a>2.2.x 이상 버전의 경우 다음을 입력합니다.
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

hello에 다음 줄에서는 2.2.0 버전을 예로:

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Hello Azure Linux 에이전트를 설치 합니다.

#### <a name="for-version-22x-use"></a>버전 2.2.x의 경우 다음을 사용합니다.
Tooinstall hello 패키지 해야 `setuptools` 처음- [여기](https://pypi.python.org/pypi/setuptools)합니다. 그런 후 다음을 실행합니다.

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>자동 업데이트가 활성화되었는지 확인

사용 하는 경우 먼저 toosee를 확인 합니다.

```bash
cat /etc/waagent.conf
```

'AutoUpdate.Enabled'를 찾습니다. 이 출력이 표시되는 경우 활성화되었습니다.

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable 실행:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Hello waagent 서비스를 다시 시작
대부분의 Linux 배포판:

```bash
sudo service waagent restart
```

Ubuntu의 경우 다음을 사용합니다.

```bash
sudo service walinuxagent restart
```

CoreOS의 경우 다음을 사용합니다.

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Hello Azure Linux 에이전트 버전 확인
    
```bash
waagent -version
```

CoreOS, 명령 위에 hello 작동 하지 않을 수 있습니다.

해당 hello Azure Linux 에이전트 버전 되었습니다 toohello 새 버전을 업데이트 하는 것이 나타납니다.

Hello Azure Linux 에이전트에 대 한 자세한 내용은 참조 [Azure Linux 에이전트 README](https://github.com/Azure/WALinuxAgent)합니다.
