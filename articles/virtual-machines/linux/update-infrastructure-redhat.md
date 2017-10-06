---
title: "aaaRed Hat 업데이트 인프라 (RHUI) | Microsoft Docs"
description: "Microsoft Azure의 주문형 Red Hat Enterprise Linux 인스턴스에 대한 RHUI(Red Hat Update Infrastructure)에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Azure의 주문형 Red Hat Enterprise Linux Vm에 대한 RHUI(Red Hat Update Infrastructure)
Hello 주문형 Red Hat Enterprise Linux (RHEL) 이미지에서 사용할 수 있는 Azure Marketplace에서 만든 가상 컴퓨터는 등록 된 tooaccess hello Red Hat 업데이트 인프라 (RHUI)이 Azure에 배포 합니다.  hello 주문형 RHEL 인스턴스 액세스 tooa 국가별 yum 리포지토리와 수 tooreceive 증분 업데이트를 가집니다.

RHUI 하 여 관리 되는 hello yum 리포지토리 목록 RHEL 인스턴스 프로 비전 하는 동안 구성 됩니다. Toodo 실행-추가 구성 필요 하지 않습니다 `yum update` RHEL 인스턴스 준비 tooget hello에 대 한 최신 업데이트 된 후입니다.

> [!NOTE]
> 2016 년 9 월 업데이트는 Azure RHUI 배포 및 hello의 단계적된 종료를 시작 했습니다. 2017 년 1 월에에서 Azure RHUI 이전 합니다. 사용 된 hello RHEL 이미지 (또는 해당 스냅숏) 2016 년 9 월에서에서 이상-가능성이 경우 동작은 필요 하지 않습니다. 그러나 오래 된 스냅숏을/Vm 있다면, 해당 구성을 toobe 중단 없이 액세스할 toohello Azure RHUI에 대해 업데이트 해야 합니다.
> 

## <a name="rhui-azure-infrastructure-update"></a>RHUI Azure 인프라 업데이트
2016년 9월을 기준으로 Azure는 새로운 RHUI(Red Hat 업데이트 인프라) 서버 모음을 포함합니다. 이러한 서버는 모든 VM에서 하위 지역에 관계없이 단일 끝점(rhui-1.micrsoft.com)을 사용할 수 있도록 [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/)를 통해 배포됩니다. hello Azure 마켓플레이스 (2016 년 9 월 이상 버전) 지점 toohello 새 Azure RHUI 서버에서 새 RHEL 종 량 제 (PAYG) 이미지 hello 하 고 추가 조치는 필요 하지 마십시오.

### <a name="determine-if-action-is-required"></a>작업이 필요한지 확인
TooAzure RHUI RHEL PAYG Azure VM에서 연결할 때 문제가 발생 하는 경우 다음이 단계를 수행
1. Azure RHUI 끝점에 대한 VM 구성 검사

    확인 `/etc/yum.repos.d/rh-cloud.repo` 파일 참조가 너무`rhui-[1-3].microsoft.com` 의 baseurl에 `[rhui-microsoft-azure-rhel*]` hello 파일의 섹션입니다. 사용 하는 경우 새 Azure RHUI hello 합니다.

    하는 경우 패턴을 따르는 hello로 tooa 위치를 가리키는 `mirrorlist.*cds[1-4].cloudapp.net` -hello 구성 업데이트 작업이 필요 합니다.

    Hello 새 구성을 사용 하는 경우 여전히 tooAzure RHUI-연결할 수 없는 Microsoft 소프트웨어 또는 Red Hat를 파일입니다.

    > [!NOTE]
    > TooAzure 호스팅되지 RHUI 액세스는 제한 된 toohello Vm 내에서 [Microsoft Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다.
    > 

2. Hello 이전 Azure RHUI 여전히 사용할 수 있는 경우이 검사를 수행 하 고 원하는 tooautomatically hello 구성 업데이트를 hello 다음 명령을 실행 합니다.

    `sudo yum update RHEL6`또는 `sudo yum update RHEL7` hello RHEL 패밀리 버전에 따라 합니다.

3. Toohello 더 이상 연결할 수 있는 경우 이전 Azure RHUI, hello 수동 단계 수행 hello 다음 섹션에서 설명 합니다.

4. VM을 영향을 받는 hello 원본 이미지/스냅숏 tooupdate hello 구성 되었는지 확인에서 프로 비전 합니다.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>단계적된 종료 hello 이전 Azure RHUI
Hello의 hello 종료 하는 동안 tooit는 다음과 같이 액세스를 제한할 이전 Azure RHUI:

1. 연결 하는 이미 tooit IP 주소의 액세스 (ACL) tooset을 제한 합니다. 가능한 부작용:를 사용 하 여 계속 진행 하면 기존 Azure RHUI hello-새 Vm 수 tooconnect tooit 되지 않을 수 있습니다. 동적 Ip와 RHEL Vm 종료/할당 취소/시작 순서를 통해 이동 하는 새 IP를 받을 수 있습니다 및 따라서도 시작할 수 tooconnect toohello 실패 이전 Azure RHUI

2. 미러 콘텐츠 배달 서버 종료 가능한 부작용: 자세한 CDSes 종료으로 표시 될 수 없습니다 더 이상 `yum update` toohello를 연결할 수 없을 때 hello까지 더 많은 시간 제한을 지점 시간을 제공 하는 이전 Azure RHUI 합니다.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>새 RHUI 콘텐츠 배달 서버 hello에 대 한 Ip hello는
네트워크 구성 toofurther를 사용 하는 경우 RHEL PAYG Vm에서 액세스를 제한, Ip 다음 hello에 사용할 수 있는지 확인 `yum update` 있는 hello 환경에 따라 toowork 합니다. 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>수동 업데이트 프로시저 toouse hello 새 Azure RHUI 서버
(Curl)를 통해 다운로드 hello 공개 키 서명

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

다운로드 한 hello 키 확인

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Hello 출력을 확인, 확인 `keyid` 및 `user ID packet`:

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

Hello 공개 키를 설치 합니다.

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

클라이언트 RPM 다운로드, 확인 및 설치

다운로드: RHEL 6의 경우

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

RHEL 7의 경우

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

다음 확인

```bash
rpm -Kv azureclient.rpm
```

출력에 해당 서명을 확인 hello의 패키지는 확인

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Hello RPM을 설치 합니다.

```bash
sudo rpm -U azureclient.rpm
```

완료 되 면 Azure RHUI 양식 hello VM에 액세스할 수 있는지 확인

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>Hello 앞에 태스크를 자동화 하기 위한 내부에서 올인원 스크립트
영향을 받는 Vm toohello 새 Azure RHUI 서버를 업데이트 하는 필요한 tooautomate hello 작업으로 스크립트를 다음 hello를 사용 합니다.

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a>RHUI 개요
[Red Hat 업데이트 인프라](https://access.redhat.com/products/red-hat-update-infrastructure) Red Hat 인증 클라우드 공급자에 의해 호스트 되는 Red Hat Enterprise Linux 클라우드 인스턴스에 대 한 확장성이 뛰어난 솔루션 toomanage yum 리포지토리 콘텐츠를 제공 합니다. Hello 업스트림 Pulp 프로젝트에 따라, RHUI 허용 클라우드 공급자 toolocally 미러 Red Hat 호스팅되지 리포지토리 콘텐츠, 사용자 지정 저장소도 콘텐츠를 만들고을 부하 분산을 통해 최종 사용자가 해당 저장소 사용 가능한 tooa 큰 그룹 콘텐츠 배달 시스템입니다.

## <a name="regions-where-rhui-is-available"></a>RHUI 사용 가능한 지역
RHUI는 RHEL 주문형 이미지를 사용할 수 있는 모든 지역에서 제공됩니다. Hello에 나열 된 모든 public 지역에서는 현재 [Azure 상태 대시보드](https://azure.microsoft.com/status/) 페이지, Azure 미국 정부 및 Azure 독일 영역입니다. RHEL 주문형 이미지에서 프로비전된 VM에 대한 RHUI 액세스 권한은 해당 가격에 포함되어 있습니다. Hello 나중에 요청 시 가용성 RHEL 확장 추가 지역/국가별 클라우드 가용성 업데이트 됩니다.

> [!NOTE]
> TooAzure 호스팅되지 RHUI 액세스는 제한 된 toohello Vm 내에서 [Microsoft Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653)합니다.
> 
> 

## <a name="get-updates-from-another-update-repository"></a>다른 업데이트 리파지토리에서 업데이트 받기
(Azure 호스팅 RHUI) 하는 대신 다른 업데이트 저장소에서 tooget 업데이트 해야 할 경우 먼저 toounregister RHUI에서 사용자 인스턴스가 있습니다. Toore 등록 해야 합니다 (예: Red Hat 위성 또는 Red Hat 고객 포털 CDN) hello 원하는 업데이트 인프라를 사용 하 여 합니다. 이러한 서비스에 대한 적합한 Red Hat 구독 및 [Azure에서 Red Hat 클라우드 액세스](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure)에 대한 등록이 필요합니다.

toounregister RHUI tooyour 업데이트 인프라를 다시 등록 하 고 다음이 단계를 따릅니다.

1. /Etc/yum.repos.d/rh-cloud.repo를 편집 하 고 모든 변경 `enabled=1` 너무`enabled=0`합니다. 예:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. /Etc/yum/pluginconf.d/rhnplugin.conf를 편집 하 고 변경 `enabled=0` 너무`enabled=1`합니다.
3. Red Hat 고객 포털 등 hello 원하는 인프라와를 등록 합니다. Red Hat 솔루션 가이드에 따라 [어떻게 tooregister 시스템 toohello Red Hat 고객 포털 구독할](https://access.redhat.com/solutions/253273)합니다.

> [!NOTE]
> Azure 호스팅 RHUI 액세스 toohello hello RHEL 종 량 제 (PAYG) 이미지 가격에 포함 됩니다. Azure 호스팅 RHUI hello에서 PAYG RHEL VM의 등록을 취소 해도 VM Bring Your-소유-라이선스 (BYOL) 형식으로 hello 가상 컴퓨터 변환 하지 않습니다. 등록 하는 경우 동일한 VM hello 업데이트의 다른 소스와 있습니다 수 수 비용이 발생 하지 이중: Red Hat 구독에 대 한 두 번째로 Azure RHEL 소프트웨어 요금 및 hello에 대 한 첫 번째입니다. 
> 
> Azure 호스팅 RHUI 이외의 업데이트 인프라를 만들고에 설명 된 대로 사용자 고유의 (BYOL 유형) 이미지를 배포 고려 toouse를 일관 되 게 해야 할 경우 [만들기 및 업로드 Red Hat 기반 가상 컴퓨터는 azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 문서.
> 

## <a name="next-steps"></a>다음 단계
Red Hat Enterprise Linux VM에서 Azure 마켓플레이스 종 량 제 이미지와 Azure 호스팅 RHUI 활용 toocreate 너무 이동[Azure 마켓플레이스](https://azure.microsoft.com/marketplace/partners/redhat/)합니다. 수 toouse 됩니다 `yum update` 추가 설정 없이 RHEL 인스턴스에 있습니다.

