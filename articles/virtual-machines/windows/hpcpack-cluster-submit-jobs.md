---
title: "Azure에서 aaaSubmit 작업 tooan HPC 팩 클러스터 | Microsoft Docs"
description: "온-프레미스 컴퓨터 toosubmit tooset Azure의 HPC Pack 클러스터 tooan 작업 하는 방법에 대해 알아봅니다"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 78f6833c-4aa6-4b3e-be71-97201abb4721
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 2918cf633917d8730487152e6a5ddb863eb8bb5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="submit-hpc-jobs-from-an-on-premises-computer-tooan-hpc-pack-cluster-deployed-in-azure"></a>Azure에 배포 된 온-프레미스 컴퓨터 tooan HPC Pack 클러스터에서 HPC 작업 제출
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

온-프레미스 클라이언트 컴퓨터 toosubmit 작업 tooa 구성 [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) Azure 클러스터에에서 있습니다. 이 문서에서는 Azure toohello 클러스터를 HTTPS 통해 클라이언트와 함께 로컬 컴퓨터를 tooset toosubmit 작업 도구 방법을 보여 줍니다. 이러한 방식으로 여러 클러스터 사용자가 작업 tooa 클라우드 기반 HPC Pack 클러스터를 전송할 수 있지만 직접 toohello 헤드 노드 VM을 연결 하거나 Azure 구독에 액세스 하지 않고 있습니다.

![Azure에서 작업 tooa 클러스터 제출][jobsubmit]

## <a name="prerequisites"></a>필수 조건
* **HPC Pack 헤드 노드는 Azure VM에 배포 된** -와 같은 자동화 된 도구를 사용 하는 것이 좋습니다는 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/) 또는 [Azure PowerShell 스크립트](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toodeploy hello 헤드 노드 및 클러스터입니다. Hello 헤드 노드의 hello DNS 이름 및 hello이이 문서의 단계를 완료 하려면 클러스터 관리자의 hello 자격 증명 필요.
* **클라이언트 컴퓨터** - HPC 팩 클라이언트 유틸리티를 실행할 수 있는 Windows 또는 Windows Server 클라이언트 컴퓨터가 필요합니다([시스템 요구 사항](https://technet.microsoft.com/library/dn535781.aspx) 참조). Toouse hello HPC Pack 웹 포털 또는 REST API toosubmit 작업을만 하려는 경우에 사용자가 선택한 모든 클라이언트 컴퓨터를 사용할 수 있습니다.
* **HPC Pack 설치 미디어** -HPC Pack (HPC Pack 2012 R2)의 최신 버전에서 사용할 수 없으면 tooinstall hello HPC Pack 클라이언트 유틸리티 hello 무료 설치 패키지는 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=328024)합니다. Hello을 다운로드 하는 동일한 버전의 hello 헤드 노드 VM에 설치 된 HPC 팩.

## <a name="step-1-install-and-configure-hello-web-components-on-hello-head-node"></a>1 단계: 설치 하 고 hello 헤드 노드에서 hello 웹 구성 요소 구성
HTTPS 통한 REST 인터페이스 toosubmit 작업 toohello 클러스터 tooenable hello HPC Pack 헤드 노드에 hello HPC Pack 웹 구성 요소가 구성 되어 있는지 확인 합니다. 이미 요소가 설치 되지 않았으면, 먼저 hello HpcWebComponents.msi 설치 파일을 실행 하 여 hello 웹 구성 요소를 설치 합니다. 그런 다음 구성 요소를 hello hello HPC PowerShell 스크립트를 실행 하 여 **집합 HPCWebComponents.ps1**합니다.

자세한 절차를 참조 하십시오. [hello Microsoft HPC Pack 웹 구성 요소 설치](http://technet.microsoft.com/library/hh314627.aspx)합니다.

> [!TIP]
> HPC Pack에 대 한 특정 Azure 빠른 시작 서식 파일 설치 하 고 hello 웹 구성 요소를 자동으로 구성 합니다. Hello를 사용 하는 경우 [HPC Pack IaaS 배포 스크립트](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toocreate hello 클러스터 필요에 따라 설치 하 고 hello 배포의 일부로 hello 웹 구성 요소를 구성할 수 있습니다.
> 
> 

**tooinstall hello 웹 구성 요소**

1. 클러스터 관리자의 hello 자격 증명을 사용 하 여 toohello 헤드 노드 VM을 연결 합니다.
2. Hello HPC 팩 설치 폴더에서 hello 헤드 노드의 HpcWebComponents.msi를 실행 합니다.
3. Hello 단계 hello 마법사 tooinstall hello 웹 구성 요소에 따라

**tooconfigure hello 웹 구성 요소**

1. Hello 헤드 노드에서 관리자 권한으로 HPC PowerShell을 시작 합니다.
2. 다음 명령을 형식 hello, hello 구성 스크립트의 toochange 디렉터리 toohello 위치:
   
    ```powershell
    cd $env:CCP_HOME\bin
    ```
3. tooconfigure는 REST 인터페이스 hello 하 고 다음 명령을 형식 hello hello HPC 웹 서비스를 시작 합니다.
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service REST –enable
    ```
4. 인증서를 증명된 tooselect hello 인증서를 선택 하는 경우 hello 헤드 노드의 toohello 공용 DNS 이름을 해당 하는 합니다. 예를 들어, CN 처럼 보이는 hello 인증서 이름을 hello 클래식 배포 모델을 사용 하 여 VM hello 헤드 노드를 배포 하는 경우 =&lt;*HeadNodeDnsName*&gt;. cloudapp.net에 합니다. Hello 인증서 이름 CN hello 리소스 관리자 배포 모델을 사용 하는 경우 같이 =&lt;*HeadNodeDnsName*&gt;.&lt; *지역*&gt;. cloudapp.azure.com 합니다.
   
   > [!NOTE]
   > 나중에이 인증서를 선택 하면 온-프레미스 컴퓨터에서 작업 toohello 헤드 노드를 제출 합니다. 선택 하지 않거나 hello Active Directory 도메인에 헤드 노드 hello의 toohello 컴퓨터 이름에 해당 하는 인증서 구성 (예: CN =*MyHPCHeadNode.HpcAzure.local*).
   > 
   > 
5. 작업 제출, 다음 명령을 형식 hello에 대 한 tooconfigure hello 웹 포털:
   
    ```powershell
    .\Set-HPCWebComponents.ps1 –Service Portal -enable
    ```
6. Hello 스크립트가 완료 되 면 후 중지 하 고 hello 다음 명령을 입력 하 여 hello HPC 작업 스케줄러 서비스를 다시 시작 합니다.
   
    ```powershell
    net stop hpcscheduler
    net start hpcscheduler
    ```

## <a name="step-2-install-hello-hpc-pack-client-utilities-on-an-on-premises-computer"></a>2 단계: 온-프레미스 컴퓨터에 hello HPC Pack 클라이언트 유틸리티를 설치 합니다.
컴퓨터에서 tooinstall hello HPC Pack 클라이언트 유틸리티를 원하는 경우 hello에서 HPC Pack 설치 파일 (전체 설치) 다운로드 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=328024)합니다. Hello 설치를 시작할 때 hello에 대 한 hello 설치 옵션을 선택 합니다. **HPC Pack 클라이언트 유틸리티**합니다.

toouse hello HPC Pack 클라이언트 도구 toosubmit 작업 toohello 헤드 노드 VM으로도 tooexport hello 헤드 노드에서 인증서 필요 하 고 hello 클라이언트 컴퓨터에 설치 합니다. hello 인증서에 있어야 합니다. CER 형식입니다.

**hello 헤드 노드에서 tooexport hello 인증서**

1. Hello 헤드 노드에서 hello 인증서 스냅인 tooa Microsoft Management Console hello 로컬 컴퓨터 계정에 대 한 추가 합니다. Tooadd hello 스냅인 단계를 참조 하십시오. [hello 인증서 스냅인 tooan MMC 추가](https://technet.microsoft.com/library/cc754431.aspx)합니다.
2. 콘솔 트리에서 hello **인증서 – 로컬 컴퓨터** > **개인**, 클릭 하 고 **인증서**합니다.
3. Hello HPC Pack 웹 구성 요소에 대해 구성 된 hello 인증서 찾기 [1 단계: 설치 hello 헤드 노드에서 hello 웹 구성 요소를 구성 하 고](#step-1:-install-and-configure-the-web-components-on-the-head-node) (예: CN =&lt;*HeadNodeDnsName* &gt;. cloudapp.net에).
4. Hello 인증서를 마우스 오른쪽 단추로 클릭 하 고 클릭 **모든 작업** > **내보내기**합니다.
5. Hello 인증서 내보내기 마법사, 클릭 **다음**, 되어 있는지 확인 하 고 **아니요, hello 개인 키는 내보내지 않습니다** 을 선택 합니다.
6. 남은 DER에 hello tooexport hello 인증서를 마법사의 단계에 따라 hello로 인코딩된 바이너리 X.509 (합니다. CER) 형식입니다.

**hello 클라이언트 컴퓨터에서 tooimport hello 인증서**

1. Hello 클라이언트 컴퓨터의 hello 헤드 노드 tooa 폴더에서 내보낸 hello 인증서를 복사 합니다.
2. Hello 클라이언트 컴퓨터에서 certmgr.msc를 실행 합니다.
3. 인증서 관리자에서 **인증서 - 현재 사용자** > **신뢰할 수 있는 루트 인증 기관**을 확장한 후 **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업** > **가져오기**를 클릭합니다.
4. Hello 인증서 가져오기 마법사, 클릭 **다음** 및 따라 hello 단계 tooimport hello 인증서를 신뢰할 수 있는 루트 인증 기관 저장소 hello 헤드 노드 toohello에서 내보낸 합니다.

> [!TIP]
> Hello 헤드 노드의 인증 기관이 hello hello 클라이언트 컴퓨터에서 인식 되지 않습니다 보안 경고가 표시 될 수 있습니다. 테스트를 위해가 경고와 전체 hello 인증서 가져오기를 무시할 수 있습니다.
> 
> 

## <a name="step-3-run-test-jobs-on-hello-cluster"></a>3 단계: hello 클러스터에서 테스트 작업을 실행
hello에서 Azure의 hello에서 실행 중인 작업을 시도 하면 구성을 클러스터 tooverify 온-프레미스 컴퓨터. 예를 들어 명령줄 명령 toosubmit 작업 toohello 클러스터 또는 HPC 팩 GUI 도구를 사용할 수 있습니다. 또한 웹 기반 포털 toosubmit 작업을 사용할 수 있습니다.

**hello 클라이언트 컴퓨터에서 작업 제출 명령을 toorun**

1. Hello HPC Pack 클라이언트 유틸리티 설치 되어 있는 클라이언트 컴퓨터에서 명령 프롬프트를 시작 합니다.
2. 샘플 명령을 입력합니다. 예를 들어 toolist hello 클러스터에서 모든 작업의 hello hello hello 헤드 노드의 전체 DNS 이름에 따라 다음 명령 비슷한 tooone를 입력 합니다.
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.cloudapp.net /all
    ```
   
    또는
   
    ```command
    job list /scheduler:https://<HeadNodeDnsName>.<region>.cloudapp.azure.com /all
    ```
   
   > [!TIP]
   > Hello 스케줄러 URL에 hello 헤드 노드를 hello IP 주소가 아닌의 전체 DNS 이름 hello를 사용 합니다. Hello IP 주소를 지정 하면 오류가 나타납니다 비슷한 너무 "tooeither를가 하는 hello 서버 인증서 신뢰 또는 toobe hello 신뢰할 수 있는 루트 저장소에 배치의 유효한 체인이."
   > 
   > 
3. 메시지가 표시 되 면 hello 사용자 이름을 입력 (hello 형태로 &lt;DomainName&gt;\\&lt;UserName&gt;) 및 hello HPC 클러스터 관리자 또는 구성한 다른 클러스터 사용자의 암호입니다. 추가 작업 운영에 대 한 로컬 자격 증명 hello toostore를 선택할 수 있습니다.
   
    작업 목록이 나타납니다.

**hello 클라이언트 컴퓨터에서 HPC 작업 관리자 toouse**

1. 이전에 작업을 제출 하는 경우에 클러스터 사용자에 대 한 도메인 자격 증명을 저장 하지 않은, hello 자격 증명을 자격 증명 관리자에 추가할 수 있습니다.
   
    a. Hello 클라이언트 컴퓨터에서 제어판에서 자격 증명 관리자를 시작 합니다.
   
    b. **Windows 자격 증명** > **일반 자격 증명 추가**를 클릭합니다.
   
    c. Hello 인터넷 주소 지정 (예를 들어 https://&lt;HeadNodeDnsName&gt;.cloudapp.net/HpcScheduler 또는 https://&lt;HeadNodeDnsName&gt;.&lt; 지역&gt;.cloudapp.azure.com/HpcScheduler), 및 hello 사용자 이름 (&lt;DomainName&gt;\\&lt;UserName&gt;) 및 hello 클러스터 관리자의 암호 구성 된 클러스터 사용자입니다.
2. Hello 클라이언트 컴퓨터에서 HPC 작업 관리자를 시작 합니다.
3. Hello에 **헤드 노드 선택** 대화 상자, 형식 hello URL toohello Azure에서 헤드 노드에 (예를 들어 https://&lt;HeadNodeDnsName&gt;. cloudapp.net에 또는 https://&lt;HeadNodeDnsName&gt;. &lt;지역&gt;. cloudapp.azure.com).
   
    HPC 작업 관리자가 열리고 hello 헤드 노드에서 작업 목록이 표시 됩니다.

**hello 헤드 노드에서 실행 중인 toouse hello 웹 포털**

1. Hello 클라이언트 컴퓨터에서 웹 브라우저를 시작 하 고 hello 주소 hello hello 헤드 노드의 전체 DNS 이름에 따라 다음 중 하나를 입력 합니다.
   
    ```
    https://<HeadNodeDnsName>.cloudapp.net/HpcPortal
    ```
   
    또는
   
    ```
    https://<HeadNodeDnsName>.<region>.cloudapp.azure.com/HpcPortal
    ```
2. Hello 보안 대화 상자가 나타나면 HPC 클러스터 관리자에 게의 hello 도메인 자격 증명을 입력 합니다. (다른 역할의 다른 클러스터 사용자를 추가할 수도 있습니다. [클러스터 사용자 관리](https://technet.microsoft.com/library/ff919335.aspx)를 참조하세요.)
   
    hello 웹 포털 toohello 작업 목록 보기를 엽니다.
3. hello 문자열 "Hello World" hello 클러스터에서 반환 하는 예제 작업 toosubmit 클릭 **새 작업** hello 왼쪽 탐색 창에서.
4. Hello에 **새 작업** 페이지의 **제출 페이지에서**, 클릭 **HelloWorld**합니다. hello 작업 제출 페이지가 나타납니다.
5. **제출**을 클릭합니다. 메시지가 표시 되 면 hello HPC 클러스터 관리자의 hello 도메인 자격 증명을 제공 합니다. hello 작업이 제출 되 및 hello 작업 ID hello에 **내 작업** 페이지.
6. 사용자가 제출한 hello 작업의 tooview hello 결과 hello 작업 ID를 클릭 한 다음 클릭 **작업 보기** tooview hello 명령 출력 (아래 **출력**).

## <a name="next-steps"></a>다음 단계
* 작업 toohello hello로 Azure 클러스터 제출할 수도 [HPC Pack REST API](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx)합니다.
* Linux 클라이언트에서 toosubmit 클러스터 작업을 하려는 경우 참조 hello Python hello 샘플 [HPC Pack 2012 R2 SDK와 샘플 코드가](https://www.microsoft.com/download/details.aspx?id=41633)합니다.

<!--Image references-->
[jobsubmit]: ./media/virtual-machines-windows-hpcpack-cluster-submit-jobs/jobsubmit.png
