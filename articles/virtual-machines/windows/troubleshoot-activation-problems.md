---
title: "Azure에서 Windows 가상 컴퓨터 정품 인증 문제 aaaTroubleshoot | Microsoft Docs"
description: "Hello 제공 Azure에서 Windows 가상 컴퓨터 정품 인증 문제를 해결 하기 위한 문제 해결"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 4ebdac66166e80dcd68cd9e2931b30a29ac01eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Windows Azure 가상 컴퓨터 정품 인증 문제 해결

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

사용자 지정 이미지에서 만든 Azure Windows 가상 컴퓨터 (VM)를 활성화할 때 데 문제가 있으면이 문서 tootroubleshoot hello 문제에 제공 된 hello 정보를 사용할 수 있습니다. 

## <a name="symptom"></a>증상

Tooactivate Azure Windows VM을 시도할 때 오류가 발생 메시지는 다음 예제는 hello 유사 합니다.

**오류: 0xC004F074 hello 소프트웨어 LicensingService 보고 해당 hello 컴퓨터를 활성화할 수 없습니다. KMS(Key Management Service)를 연결할 수 없습니다. 추가 정보에 대 한 hello 응용 프로그램 이벤트 로그를 참조 하십시오.**

## <a name="cause"></a>원인
일반적으로 Azure VM 정품 인증 문제 hello Windows VM으로 구성 되지 않은 경우 적절 한 KMS 클라이언트 설정 키 hello를 사용 하 여 또는 hello Windows VM에 연결 문제가 toohello Azure KMS 서비스 (kms.core.windows.net, 1668 포트)에 발생 합니다. 

## <a name="solution"></a>해결 방법

>[!NOTE]
>사이트 간 VPN을 사용 하는 참조를 강제 터널링 하는 경우 [사용자 지정 Azure 사용 강제 터널링 tooenable KMS 정품 인증 라우팅합니다](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx)합니다. 
>
>ExpressRoute를 사용 하 고 있는 경우 게시 된 기본 경로 참조 하십시오 [ExpressRoute를 통해 Azure VM tooactivate 못할](http://blogs.msdn.com/b/mast/archive/2015/12/01/azure-vm-may-fail-to-activate-over-expressroute.aspx)합니다.

### <a name="step-1-configure-hello-appropriate-kms-client-setup-key-for-windows-server-2016-and-windows-server-2012-r2"></a>1 단계 구성 hello 적절 한 KMS 클라이언트 설정 키 (예: Windows Server 2016 및 Windows Server 2012 R2)

Windows Server 2016 또는 Windows Server 2012 r 2의 사용자 지정 이미지에서 만들어진 VM hello에 대 한 hello 적절 한 KMS 클라이언트 설정 키 hello VM에 대 한 구성 해야 합니다.

TooWindows 2012 또는 Windows 2008 r 2에는이 단계가 적용 되지 않습니다. 에서만 지원 되며 Windows Server 2016 및 Windows Server 2012 r 2는 hello 자동화 활성화 AVMA (가상 컴퓨터) 기능을 사용 합니다.

1. 관리자 권한의 명령 프롬프트에서 **slmgr.vbs /dlv**를 실행합니다. Hello hello 출력에 대 한 설명 값을 확인 하 고 소매 (소매 채널) 또는 볼륨 (VOLUME_KMSCLIENT) 라이선스 미디어에서 만들어졌는지 여부를 확인 합니다.
  
    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. 경우 **slmgr.vbs /dlv** hello 명령을 tooset hello 다음을 실행 하는 소매 채널 표시 [KMS 클라이언트 설정 키](https://technet.microsoft.com/library/jj612867%28v=ws.11%29.aspx?f=255&MSPPError=-2147217396) hello 버전의 Windows Server에 사용 되 고 tooretry 정품 인증을 강제: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    예를 들어 Windows Server 2016 데이터 센터에 대 한 hello 다음 명령을 실행 합니다.

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-hello-connectivity-between-hello-vm-and-azure-kms-service"></a>2 단계 hello VM 및 Azure KMS 서비스 간의 hello 연결을 확인 하세요

1. 다운로드 하 고 hello 압축 [Psping](http:/technet.microsoft.com/en-us/sysinternals/jj729731.aspx) 도구 tooa hello 활성화 하지 않는 VM의에서 로컬 폴더입니다. 

2. TooStart 이동 Windows PowerShell에서 검색 Windows PowerShell을 마우스 오른쪽 단추로 클릭 한 다음 관리자 권한으로 실행을 선택 합니다.

3. VM이 해당 hello toouse hello 올바른 Azure KMS 서버를 구성 되어 있는지 확인 합니다. toodo이 다음 명령을 실행 합니다.
  
    ```
    iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms
    kms.core.windows.net:1688
    ```
    hello 명령이 반환 해야: 키 관리 서비스 컴퓨터 이름을 tookms.core.windows.net:1688를 성공적으로 설정 합니다.

4. 연결 toohello KMS 서버가 있는 Psping을 사용 하 여 확인 합니다. Hello Pstools.zip 다운로드, 추출 했던 toohello 폴더를 전환 하 고 hello 다음을 실행 하십시오.
  
    ```
    \psping.exe kms.core.windows.net:1688
    ```
  
  Hello hello 출력의 마지막 두 번째 줄에 표시 되는지 확인: 보낸 = 4, Received = 4, Lost = 0 (0% 손실).

  Lost 0 (영) 보다 큰 경우 hello VM 연결 toohello KMS 서버를 않아도 됩니다. 이 경우 hello VM 가상 네트워크 되었으며 경우에 사용자 지정 DNS 서버를 지정 해야 하며 해당 DNS 서버 수 tooresolve kms.core.windows.net이 됩니다. 또는 kms.core.windows.net 해결 않으면 hello DNS 서버 tooone 변경 합니다.

  모든 DNS 서버를 가상 네트워크에서 제거하면 VM은 Azure의 내부 DNS 서비스를 사용할 수 있습니다. 이 서비스는 kms.core.windows.net을 확인할 수 있습니다.
  
또한 해당 hello 게스트 방화벽 정품 인증 시도 차단 하는 방식으로 구성 되지 않은 확인 합니다.

5. 성공적인 연결 tookms.core.windows.net를 확인 한 후에 hello 다음 해당 관리자 권한 Windows PowerShell 프롬프트에서 명령을 실행 합니다. 이 명령은 여러 번 활성화되도록 시도합니다.

    ```
    1..12 | % { iex “$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato” ; start-sleep 5 }
    ```

성공적인 활성화 hello 다음과 비슷한 정보를 반환 합니다.

**Windows(R), ServerDatacenter 버전 활성화(12345678-1234-1234-1234-12345678) … 제품을 성공적으로 활성화했습니다.**

## <a name="faq"></a>FAQ 

### <a name="i-created-hello-windows-server-2016-from-azure-marketplace-do-i-need-tooconfigure-kms-key-for-activating-hello-windows-server-2016"></a>Windows Server 2016 hello Azure 마켓플레이스의 만들었습니다. Tooconfigure KMS 키는 Windows Server 2016 hello를 활성화 하는 데 필요 합니까? 
 
아니요. Azure 마켓플레이스에서 hello 이미지에 hello 적절 한 KMS 클라이언트 설정 키 이미 구성 되어 있습니다. 

### <a name="does-windows-activation-work-hello-same-way-regardless-if-hello-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>가 Windows 정품 인증 작업 hello 동일한 방식으로 상관 없이 여부 VM hello Azure 하이브리드 사용 혜택 (허브)를 사용 하는 경우? 
 
예. 
 
### <a name="what-happens-if-windows-activation-period-expires"></a>Windows 정품 인증 기간이 만료된 경우 어떻게 되나요? 
 
Hello 유예 기간이 만료 되었습니다. Windows가 여전히 활성화 되지 않았습니다를 Windows Server 2008 R2 및 이후 버전의 Windows 정품 인증 하는 방법에 대 한 추가 알림 없이 자동 표시 됩니다. hello 바탕 화면 배경 무늬 검은색으로 되어 있고 Windows 업데이트를 통해 보안 및 중요 업데이트만 되지만 필수 업데이트 설치. Hello 알림 참조의 hello hello 아래쪽 섹션 [라이선스 조건](http://technet.microsoft.com/en-us/library/ff793403.aspx) 페이지.   

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.
도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.
