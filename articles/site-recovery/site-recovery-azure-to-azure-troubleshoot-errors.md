---
title: "aaaAzure Azure-Azure 복제 문제 및 오류에 대 한 사이트 복구 문제 해결 | Microsoft Docs"
description: "재해 복구를 위해 Azure 가상 컴퓨터를 복제할 때 오류 및 문제 해결"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Azure 간 VM 복제 문제 해결

이 문서를 복제 하 고 하나의 영역 tooanother 지역에서 Azure 가상 컴퓨터를 복구 하는 경우 Azure 사이트 복구에서 hello 일반적인 문제를 설명 하 고 설명 어떻게 tootroubleshoot 해당 합니다. 지원 되는 구성에 대 한 자세한 내용은 참조 hello [Azure Vm을 복제 하기 위한 지원 매트릭스](site-recovery-support-matrix-azure-to-azure.md)합니다.

## <a name="azure-resource-quota-issues-error-code-150097"></a>Azure 리소스 할당량 문제(오류 코드 150097)
구독 활성화 toocreate Azure Vm 재해 복구 지역으로 toouse를 계획 하는 hello 대상 지역에 있어야 합니다. 또한 구독을 보유 해야 충분 한 사용 할당량 toocreate 특정 크기의 Vm입니다. 기본적으로 사이트 복구 선택 hello 대상 VM으로 원본 VM hello에 대 한 동일한 크기를 hello 합니다. Hello 일치 하는 크기를 사용할 수 없는 경우 hello 가장 가까운 가능한 크기는 자동으로 선택 됩니다. 원본 VM 구성을 지원하는 일치하는 크기가 없는 경우 다음 오류 메시지가 나타납니다.

**오류 코드** | **가능한 원인** | **권장 사항**
--- | --- | ---
150097<br></br>**메시지**: VmName hello 가상 컴퓨터에 대 한 복제를 사용할 수 없습니다. | -구독 ID 되지 않을 수 있습니다 toocreate hello 대상 지역 위치에서 Vm을 사용 합니다.</br></br>-구독 ID를 받아들일 수 없습니다 또는 hello 대상 지역 위치에 충분 한 할당량 toocreate 특정 VM 크기에 없는 합니다.</br></br>-Hello 소스 VM NIC 수 (2)와 일치 하는 적절 한 대상 VM 크기 A hello 구독 ID에 대 한 hello 대상 지역 위치에서 찾을 수 없습니다.| 연락처 [Azure 청구 지원](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable VM 만들기 hello에 대 한 구독에 대 한 VM 크기 hello 대상 위치에 필요 합니다. 활성화 된 후 다시 시도 hello 작업에 실패 했습니다.

### <a name="fix-hello-problem"></a>Hello 문제 해결
에 문의할 수 있습니다 [Azure 청구 지원](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable 프로그램 구독 toocreate hello 대상 위치에서 필요한 크기의 Vm입니다.

Hello 대상 위치 용량 제약 조건이 있으면 복제를 사용 하지 않도록 설정 하 고 구독 충분 한 할당량 toocreate hello 필요한 크기의 Vm에 있는 tooa 다른 위치를 사용 합니다.

## <a name="trusted-root-certificates-error-code-151066"></a>신뢰할 수 있는 루트 인증서(오류 코드 151066)

모든 hello 최신 신뢰할 수 있는 루트 인증서 hello VM에는 표시 되지, "복제 사용" 작업이 실패할 수 있습니다. Hello 인증서, 인증 hello 및 사이트 복구 서비스의 권한 부여 없이 hello VM에서에서 호출에 실패 합니다. hello 실패 "복제 사용" 사이트 복구 작업에 대 한 hello 오류 메시지가 나타납니다.

**오류 코드** | **가능한 원인** | **권장 사항**
--- | --- | ---
151066<br></br>**메시지**: Site Recovery 구성이 실패했습니다. | hello 필요한 권한 부여에 사용 되는 신뢰할 수 있는 루트 인증서 인증 hello 컴퓨터에는 표시 되지 않으며 | -Hello Windows 운영 체제를 실행 하는 VM을 장애 조치 해당 hello hello 컴퓨터에 있는 루트 인증서는 신뢰할 수 있는 합니다. 자세한 내용은 [신뢰할 수 있는 루트 및 허용되지 않는 인증서 구성](https://technet.microsoft.com/library/dn265983.aspx)을 참조하세요.<br></br>-Hello Linux 운영 체제를 실행 하는 VM에 대 한 hello Linux 운영 체제 버전 배포자가 게시 된 신뢰할 수 있는 루트 인증서에 대 한 hello 지침을 따릅니다.

### <a name="fix-hello-problem"></a>Hello 문제 해결
**Windows**

모든 hello 신뢰할 수 있는 루트 인증서는 hello 컴퓨터에 있는지를 hello VM에서 모든 hello 최신 Windows 업데이트를 설치 합니다. 연결이 끊어진된 환경에 있는 경우에 조직 tooget hello 인증서의 hello 표준 Windows 업데이트 프로세스를 따릅니다. Hello 인증서 hello VM에 존재 하지 않으면 필요한 경우 보안상의 이유로 hello 호출 toohello Site Recovery 서비스 실패 합니다.

Hello Vm에 hello 일반적인 Windows 업데이트 관리 또는 사용자 조직 tooget 모든 hello 최신 루트 인증서 및 업데이트 하는 hello 인증서 해지 목록에서 인증서 업데이트 관리 프로세스를 따릅니다.

문제 hello tooverify 해결 됨, VM에서 브라우저에서 toologin.microsoftonline.com를 이동 합니다.

**Linux**

Linux 배포자 tooget hello 최신 신뢰할 수 있는 루트 인증서 및 hello VM에 hello 최신 인증서 취소 목록을 제공한 hello 지침을 따릅니다.

SuSE Linux symlink toomaintain 인증서 목록에 사용 하므로 다음이 단계를 따르십시오.

1.  루트 사용자로 로그인합니다.

2.  다음 명령을 실행합니다.

      ``# cd /etc/ssl/certs``

3.  toosee는 hello Symantec 루트 CA 인증서가 있는지 또는 그렇지 않은 경우이 명령을 실행 합니다.

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Hello 파일을 찾을 수 없으면 이러한 명령을 실행 합니다.

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  toocreate b204d74a.0와 symlink VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem->,이 명령을 실행 합니다.

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  이 명령에는 다음 출력 hello 경우 toosee를 확인 합니다. 그렇지 않으면 toocreate symlink 했습니다.

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. 기호화 된 링크 653b494a.0 없으면이 명령은 toocreate symlink를 사용 합니다.

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Site Recovery URL 또는 IP 범위에 대한 아웃바운드 연결(오류 코드 151037 또는 151072)

사이트 복구 복제 toowork Url 또는 IP 범위는 아웃 바운드 연결 toospecific hello VM에서에서 필요 합니다. 뒤에 있는 VM은 방화벽이 나 사용 하 여 네트워크 보안 그룹 (NSG) 규칙 toocontrol 아웃 바운드 연결 이벤트를 이러한 오류 메시지 중 하나가 나타날 수 있습니다.

**오류 코드** | **가능한 원인** | **권장 사항**
--- | --- | ---
151037<br></br>**메시지**: tooregister Site Recovery와 Azure 가상 컴퓨터를 실패 했습니다. | Hello VM에서 NSG toocontrol 아웃 바운드 액세스를 사용 하 고-및 hello 필요한 IP 범위에 대 한 아웃 바운드 액세스 허용 되지 않습니다.</br></br>타사 방화벽 도구를 사용 하는-및 hello IP 범위/Url 허용 목록 없는 필요 합니다.</br>| -방화벽 프록시 toocontrol 아웃 바운드 네트워크 연결에 VM hello를 사용 하는 경우 해당 hello 필수 구성 요소 Url을 확인 또는 데이터 센터 IP 범위는 허용 목록입니다. 자세한 내용은 [방화벽 프록시 지침](https://aka.ms/a2a-firewall-proxy-guidance)을 참조하세요.</br></br>-Hello VM에 NSG 규칙 toocontrol 아웃 바운드 네트워크 연결을 사용 중인 경우에 hello 필수 구성 요소 데이터 센터 IP 범위 허용 되는지 확인 합니다. 자세한 내용은 [네트워크 보안 그룹 지침](https://aka.ms/a2a-nsg-guidance)을 참조하세요.
151072<br></br>**메시지**: Site Recovery 구성이 실패했습니다. | 연결에 설정 된 tooSite 복구 서비스 끝점 수 없습니다. | -방화벽 프록시 toocontrol 아웃 바운드 네트워크 연결에 VM hello를 사용 하는 경우 해당 hello 필수 구성 요소 Url을 확인 또는 데이터 센터 IP 범위는 허용 목록입니다. 자세한 내용은 [방화벽 프록시 지침](https://aka.ms/a2a-firewall-proxy-guidance)을 참조하세요.</br></br>-Hello VM에 NSG 규칙 toocontrol 아웃 바운드 네트워크 연결을 사용 중인 경우에 hello 필수 구성 요소 데이터 센터 IP 범위 허용 되는지 확인 합니다. 자세한 내용은 [네트워크 보안 그룹 지침](https://aka.ms/a2a-nsg-guidance)을 참조하세요.

### <a name="fix-hello-problem"></a>Hello 문제 해결
toowhitelist [hello 필요한 Url](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) 또는 hello [IP 범위 필요한](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), hello에 hello 단계를 따라 [네트워킹 지침 문서](site-recovery-azure-to-azure-networking-guidance.md)합니다.

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>디스크 hello 컴퓨터 (오류 코드 150039)에서 찾을 수 없습니다

새 디스크 연결 toohello VM 초기화 해야 합니다.

**오류 코드** | **가능한 원인** | **권장 사항**
--- | --- | ---
150039<br></br>**메시지**: 논리 단위 번호 (LUN) (LUNValue)와 Azure 데이터 디스크 (DiskName) (DiskURI) hello hello 있는 VM 내에서 보고 되 고 해당 디스크를 매핑된 tooa 없습니다. 동일한 LUN 값입니다. | -새 데이터 디스크 연결 된 toohello VM 했지만 초기화 되지 않았습니다.</br></br>-hello hello VM 데이터 디스크가 있는 hello에 디스크를 연결 된 toohello VM hello LUN 값을 올바르게 보고 하지 않는 합니다.| Hello 데이터 디스크가 초기화 됩니다 확인 hello 작업을 다시 시도 하십시오.</br></br>Windows의 경우: [새 디스크 연결 및 초기화](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk)를 수행합니다.</br></br>Linux의 경우: [Linux에서 새 데이터 디스크 초기화](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux)를 수행합니다.

### <a name="fix-hello-problem"></a>Hello 문제 해결
Hello 데이터 디스크가 초기화 된 후 hello 작업을 다시 시도 확인:

- Windows의 경우: [새 디스크 연결 및 초기화](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk)를 수행합니다.
- Linux의 경우: [Linux에서 새 데이터 디스크 초기화](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux)를 수행합니다.

Hello 문제가 계속 되 면 지원에 문의 합니다.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>"복제를 사용"에서 선택할 수 없습니다 toosee hello Azure VM

[복제를 사용하도록 설정: 2단계](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines)에서 선택할 Azure VM을 표시할 수 없습니다. 이 문제는 hello Azure VM에 남아 있는 toostale 사이트 복구 구성 원인일 수 있습니다. 비활성화 hello에 Azure VM에서 hello 구성이 오래 된 상태로 남겨둘 수 있습니다.:

- 사이트 복구를 사용 하 여 hello Azure VM에 대 한 복제를 활성화 하 고 후 명시적으로 hello VM에서 복제를 해제 하지 않고 hello 사이트 복구 자격 증명 모음을 삭제 합니다.
- Site Recovery를 사용 하 여 hello Azure VM에 대 한 복제를 활성화 하 고 명시적으로 hello VM에서 복제를 해제 하지 않고 hello 사이트 복구 자격 증명 모음을 포함 하는 hello 리소스 그룹을 삭제 합니다.

### <a name="fix-hello-problem"></a>Hello 문제 해결

사용할 수 있습니다 [부실 ASR 구성 스크립트를 제거](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) hello hello Azure VM에 부실 사이트 복구 구성을 제거 합니다. 표시 되어야 VM에 hello [복제 사용: 2 단계](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) 구성이 오래 된 상태로 hello를 제거한 후 합니다.


## <a name="next-steps"></a>다음 단계
[Azure 가상 컴퓨터 복제](site-recovery-replicate-azure-to-azure.md)
