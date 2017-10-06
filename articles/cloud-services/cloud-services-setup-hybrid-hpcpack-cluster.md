---
title: "Azure에서 하이브리드 HPC Pack을 aaaSet 클러스터 | Microsoft Docs"
description: "어떻게 toouse Microsoft HPC Pack 및 Azure tooset 최대 크기가 작거나, 하이브리드 고성능 컴퓨팅 (HPC) 클러스터에 알아봅니다"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Microsoft HPC(고성능 컴퓨팅) Pack 및 주문형 Azure 계산 노드를 사용하여 하이브리드 HPC 클러스터 설정
Microsoft HPC Pack 2012 R2 및 Azure tooset는 작은 하이브리드 고성능 컴퓨팅 (HPC) 클러스터를 사용 합니다. 일부 계산 노드는 Azure에서 요청 시 배포할 클라우드 서비스와이 문서에 표시 된 hello 클러스터는 온-프레미스 HPC Pack 헤드 노드 구성 됩니다. 그런 다음 hello 하이브리드 클러스터에서 계산 작업을 실행할 수 있습니다.

![하이브리드 HPC 클러스터][Overview] 

이 자습서에서는 한 가지 방법은 클러스터 버스트 toohello "클라우드", 확장성, 주문형 Azure 리소스 toorun 계산 집약적인 응용 프로그램 toouse 라고도 합니다.

이 자습서는 이전에 계산 클러스터나 HPC 팩을 사용한 경험이 없다고 가정합니다. 것이 의도 한 유일한 toohelp 예시 목적을 위한 신속 하 게 하이브리드 계산 클러스터를 배포 합니다. 고려 사항 및 단계 toodeploy 하이브리드 HPC Pack 클러스터를 프로덕션 환경 또는 toouse HPC 팩 2016에서 큰 규모로 참조 hello [세부 지침](http://go.microsoft.com/fwlink/p/?LinkID=200493)합니다. Azure Virtual Machine의 자동화된 클러스터 배포를 포함한 HPC Pack을 사용한 다른 시나리오의 경우 [Azure에서 Microsoft HPC Pack을 사용하는 HPC 클러스터 옵션](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.

## <a name="prerequisites"></a>필수 조건
* **Azure 구독** - Azure 구독이 없는 경우 몇 분 만에 [무료 계정](https://azure.microsoft.com/free/) 을 만들 수 있습니다.
* **Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 온-프레미스 컴퓨터** -hello HPC 클러스터의 헤드 노드와 hello이이 컴퓨터를 사용 합니다. Windows Server가 아직 실행되지 않는 경우 [평가판](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2)을 다운로드하고 설치할 수 있습니다.
  
  * hello 컴퓨터 tooan 조인 된 Active Directory 도메인 이어야 합니다. 테스트를 위해 hello 헤드 노드 컴퓨터를 도메인 컨트롤러로 구성할 수 있습니다. tooadd hello Active Directory 도메인 서비스 서버 역할 및 hello 헤드 노드 컴퓨터를 도메인 컨트롤러로 승격, Windows Server 용 hello 설명서를 참조 하십시오.
  * 이러한 언어 중 하나로 toosupport HPC Pack을 hello 운영 체제를 설치 해야 합니다: 영어 및 일본어, 중국어 (간체).
  * 중요 업데이트가 설치되었는지 확인합니다.
* **HPC Pack 2012 R2** - [다운로드](http://go.microsoft.com/fwlink/p/?linkid=328024) 요금 및 복사 hello 파일 toohello 헤드 노드 컴퓨터의 사용 가능한 최신 버전 hello에 대 한 hello 설치 패키지입니다. 선택 hello에 설치 파일이 동일한 언어의 Windows Server가 설치 합니다.

    >[!NOTE]
    > HPC Pack 2012 R2 대신 HPC 팩 2016 toouse 하려는 경우 추가 구성이 필요 합니다. Hello 참조 [세부 지침](http://go.microsoft.com/fwlink/p/?LinkID=200493)합니다.
    > 
* **도메인 계정** -hello 헤드 노드에 HPC Pack tooinstall에 로컬 관리자 권한으로이 계정을 구성 해야 합니다.
* **포트 443에서 TCP 연결** hello 헤드 노드 tooAzure에서 합니다.

## <a name="install-hpc-pack-on-hello-head-node"></a>Hello 헤드 노드에 HPC Pack 설치
먼저 Windows Server를 실행하는 온-프레미스 컴퓨터에 Microsoft HPC Pack을 설치합니다. 이 컴퓨터에는 hello hello 클러스터의 헤드 노드가 됩니다.

1. 로컬 관리자 권한이 있는 도메인 계정을 사용 하 여 toohello 헤드 노드에 로그온 합니다.

2. Hello HPC Pack 설치 파일에서 Setup.exe를 실행 하 여 hello HPC Pack 설치 마법사를 시작 합니다.

3. Hello에 **HPC Pack 2012 R2 설치** 화면에서 **새로 설치 하거나 새 기능 tooan 기존 설치를 추가할**합니다.

    ![HPC Pack 2012 설치][install_hpc1]

4. Hello에 **Microsoft 소프트웨어 사용자 계약 페이지**, 클릭 **다음**합니다.

5. Hello에 **설치 유형 선택** 페이지 **헤드 노드를 만들어 새 HPC 클러스터 만들기**, 클릭 하 고 **다음**합니다.

6. hello 마법사 여러 설치 하기 전에 테스트를 실행합니다. 클릭 **다음** hello에 **설치 규칙** 페이지에서 모든 테스트를 통과 하는 경우. 그렇지 않은 경우 제공 하는 hello 정보를 검토 하 고 사용자 환경에서 필요한 변경을 수행 합니다. 그런 다음 실행 하는 경우 필요한 시작 안녕 설치 마법사 또는 hello 테스트 다시입니다.
7. Hello에 **HPC DB 구성** 페이지에서 **헤드 노드** 모든 HPC 데이터베이스에 대해 선택한 다음 클릭 **다음**합니다. 

    ![DB 구성][install_hpc4]

8. Hello hello 마법사의 나머지 페이지에서 기본 선택 항목을 적용 합니다. Hello에 **필수 구성 요소 설치** 페이지 **설치**합니다.
   
    ![설치][install_hpc6]

9. Hello 설치가 완료 된 후의 선택을 취소 **HPC 클러스터 관리자를 시작** 클릭 하 고 **마침**합니다. (이후 단계에서 HPC 클러스터 관리자를 시작합니다.)
   
    ![Finish][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Hello Azure 구독 준비
Hello 단계를 수행 하는 hello 수행 [Azure 포털](https://portal.azure.com) Azure 구독. 다음이 단계를 완료 한 후 hello 온-프레미스 헤드 노드에서 Azure 노드를 배포할 수 있습니다. 
  
  > [!NOTE]
  > 또한 나중에 필요한 Azure 구독 ID를 기록해 둡니다. hello ID를 찾아볼 **구독** hello 포털에서입니다.
  > 

### <a name="upload-hello-default-management-certificate"></a>Hello 기본 관리 인증서 업로드
HPC Pack hello 헤드 노드를 hello 기본 Microsoft HPC Azure 관리 인증서를 Azure 관리 인증서로 업로드할 수 있는 호출에 자체 서명 된 인증서를 설치 합니다. 이 인증서가 테스트를 위해 제공 하 고 헤드 노드와 Azure 간의 개념 증명 배포 toosecure hello 연결 hello 합니다.

1. Toohello hello 헤드 노드 컴퓨터에서 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. **구독** > *your_subscription_name*을 클릭합니다.

3. **관리 인증서** > **업로드**.4를 클릭합니다. 파일이 C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer hello에 대 한 hello 헤드 노드에서 찾습니다. **업로드**를 클릭합니다.

   
hello **기본 HPC Azure 관리** hello 관리 인증서 목록에 인증서가 표시 됩니다.

### <a name="create-an-azure-cloud-service"></a>Azure 클라우드 서비스 만들기
> [!NOTE]
> 최상의 성능을 위해 hello 클라우드 서비스 및 hello 저장소 계정 만들기 (이후 단계)에서 hello에 동일한 지리적 지역입니다.
> 
> 

1. Hello 포털에서 클릭 **클라우드 서비스 (클래식)** > **+ 추가**합니다.

2.  Hello 서비스에 대 한 DNS 이름을 입력 한 리소스 그룹 및 위치를 선택한 후 클릭 **만들기**합니다.


### <a name="create-an-azure-storage-account"></a>Azure 저장소 계정 만들기
1. Hello 포털에서 클릭 **저장소 계정 (클래식)** > **+ 추가**합니다.

2. Hello 계정에 대 한 이름을 입력 하 고 hello 선택 **클래식** 배포 모델입니다.

3. 리소스 그룹 및 위치를 선택하고 다른 설정을 기본값 그대로 둡니다. 그런 다음 **Create**를 클릭합니다.

## <a name="configure-hello-head-node"></a>Hello 헤드 노드 구성
HPC 클러스터 관리자 toodeploy toouse Azure 노드 및 toosubmit 작업을 먼저 일부 필요한 클러스터 구성 단계를 수행 합니다.

1. Hello 헤드 노드에서 HPC 클러스터 관리자를 시작 합니다. 경우 hello **헤드 노드 선택** 대화 상자가 나타나면 클릭 **로컬 컴퓨터**합니다. hello **배포 할 일 목록** 나타납니다.

2. **Required deployment tasks**에서 **Configure your network**를 클릭합니다.
   
    ![네트워크 구성][config_hpc2]

3. Hello 네트워크 구성 마법사에서에서 선택 **엔터프라이즈 네트워크의 모든 노드만** (토폴로지 5). 이 네트워크 구성은 데모용으로 가장 간단한 hello 합니다.
   
    ![토폴로지 5][config_hpc3]
   
4. 클릭 **다음** hello 마법사의 페이지 남은 hello에서 tooaccept 기본값입니다. 그런 다음 hello **검토** 탭을 클릭 **구성** toocomplete hello 네트워크 구성 합니다.

5. Hello에 **배포 할 일 목록**, 클릭 **설치 자격 증명 제공**합니다.

6. Hello에 **설치 자격 증명** 대화 상자, tooinstall HPC Pack을 사용 하 여 hello 도메인 계정의 hello 자격 증명을 입력 합니다. 그런 후 **OK**를 클릭합니다. 
   
    ![Installation Credentials][config_hpc6]
   
7. Hello에 **배포 할 일 목록**, 클릭 **hello 새 노드의 명명 구성**합니다.

8. Hello에 **노드 명명 시리즈 지정** 대화 상자에서 기본값을 사용한 hello 명명 시리즈 및 클릭 **확인**합니다. Hello이 자습서에서는 추가 Azure 노드의 이름은 자동으로 하는 경우에이 단계를 완료 합니다.
   
    ![노드 이름 지정][config_hpc8]
   
9. Hello에 **배포 할 일 목록**, 클릭 **노드 템플릿 만들기**합니다. Hello 자습서의 뒷부분에 나오는 hello 노드 템플릿 tooadd Azure 노드 toohello 클러스터를 사용 합니다.

10. Hello 노드 템플릿 만들기 마법사에서 다음 hello를 실행 합니다.
    
    a. Hello에 **노드 템플릿 형식 선택** 페이지 **Windows Azure 노드 템플릿**, 클릭 하 고 **다음**합니다.
    
    ![노드 템플릿][config_hpc10]
    
    b. 클릭 **다음** tooaccept hello 기본 템플릿 이름입니다.
    
    c. Hello에 **구독 정보를 제공** 페이지 (Azure 계정 정보 사용 가능) Azure 구독 ID를 입력 합니다. 그런 후 **관리 인증서**에서 **기본 Microsoft HPC Azure 관리**를 찾습니다. 그런 후 **Next**를 클릭합니다.
    
    ![노드 템플릿][config_hpc12]
    
    d. Hello에 **서비스 정보를 제공** 페이지, 선택 hello 클라우드 서비스 및 이전 단계에서 만든 hello 저장소 계정입니다. 그런 후 **Next**를 클릭합니다.
    
    ![노드 템플릿][config_hpc13]
    
    e. 클릭 **다음** hello 마법사의 페이지 남은 hello에서 tooaccept 기본값입니다. 그런 다음 hello **검토** 탭을 클릭 **만들기** toocreate hello 노드 템플릿에 합니다.
    
    > [!NOTE]
    > 기본적으로 hello Azure 노드 템플릿 설정이 포함 됩니다 (프로 비전) toostart과 중지 hello 노드를 수동으로 HPC 클러스터 관리자를 사용 하 여. 필요에 따라 일정 toostart를 구성할 수 있습니다 및 Azure 노드를 자동으로 hello 중지 합니다.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Azure 노드 toohello 클러스터 추가
이제 hello 노드 템플릿 tooadd Azure 노드 toohello 클러스터를 사용 합니다. Hello 노드 toohello 클러스터 (프로 비전)를 시작할 수 있도록 구성 정보를 저장 추가 hello 클라우드 서비스에서 언제 든 지 게 됩니다. 구독을 가져옵니다 대해서만 요금이 청구 Azure 노드 hello 인스턴스가 hello 클라우드 서비스에서 실행 되 고 후 합니다.

두 작은 노드 tooadd 단계를 수행 합니다.

1. HPC 클러스터 관리자에서 **노드 관리**(최신 버전의 HPC Pack에서 **리소스 관리**) > **노드 추가**를 클릭합니다.
   
    ![노드 추가][add_node1]

2. Hello에 노드 추가 마법사 hello에 **배포 방법 선택** 페이지 **추가 Windows Azure 노드**, 클릭 하 고 **다음**합니다.
   
    ![Azure 노드 추가][add_node1_1]

3. Hello에 **새 노드를 지정** 페이지, 이전에 만든 선택 hello Azure 노드 템플릿 (기본적으로 호출 **기본 AzureNode 템플릿을**). 크기가 **Small**인 노드 **2**개를 지정하고 **Next**를 클릭합니다.
   
    ![노드 지정][add_node2]
   
4. Hello에 **완료 hello 노드 추가 마법사** 페이지 **마침**합니다.
    
     이제 **AzureCN-0001** 및 **AzureCN-0002**라는 Azure 노드 2개가 HPC Cluster Manager에 표시됩니다. 둘 다 hello에 **된** 상태입니다.
   
    ![추가된 노드][add_node3]

## <a name="start-hello-azure-nodes"></a>시작 hello Azure 노드
원하는 toouse hello 클러스터 리소스를 Azure에서 HPC 클러스터 관리자 toostart (프로 비전)를 사용 하 여 Azure 노드를 hello 하 고 온라인 상태로 합니다.

1. HPC 클러스터 관리자에서 클릭 **노드 관리** (호출 **리소스 관리** HPC Pack의 현재 버전에서), 선택 hello Azure 노드 및 합니다.

2. **시작**을 클릭한 다음 **확인**을 클릭합니다.
   
   ![노드 시작][add_node4]
   
    hello 노드 전환 toohello **프로 비전** 상태입니다. 보기 hello 프로비저닝 진행률 로그 tootrack hello를 프로 비전 합니다.
   
    ![노드 프로비전][add_node6]

3. 몇 분 후 hello Azure 노드 프로 비전을 완료 하 고 hello에 **오프 라인** 상태입니다. 이 상태 hello 역할 인스턴스가 실행 중인 있지만 클러스터 작업을 허용할 아직 없습니다.

4. hello Azure 포털에서에서 역할 인스턴스 hello tooconfirm를 실행 하는 클릭, **클라우드 서비스 (클래식)** > *your_cloud_service_name*합니다.
   
   두 개의 표시 되어야 **HpcWorkerRole** hello 서비스에서 실행 중인 인스턴스 (노드). HPC Pack에 두 항목을 자동으로 배포 **HpcProxy** 인스턴스 hello 헤드 노드와 Azure 간의 (보통 크기) toohandle 통신 합니다.

   ![실행 중인 인스턴스][view_instances1]

5. 작업 선택 hello 노드, 마우스 오른쪽 단추를 클릭 한 다음 toobring hello Azure 노드 온라인 toorun 클러스터 **온라인 상태로 만들기**합니다.
   
    ![오프라인 노드][add_node7]
   
    HPC 클러스터 관리자에에서 있음을 나타냅니다 hello 노드 hello **온라인** 상태입니다.

## <a name="run-a-command-across-hello-cluster"></a>Hello 클러스터 전체에서 명령 실행
toocheck hello 설치를 사용 하 여 hello HPC Pack **clusrun** 명령 toorun 명령 또는 하나 이상의 클러스터 노드에서 응용 프로그램입니다. 간단한 예로 사용 하 여 **clusrun** tooget hello IP 구성의 hello Azure 노드.

1. Hello 헤드 노드에서 관리자 권한으로 명령 프롬프트를 엽니다.

2. Hello 다음 명령을 입력 합니다.
   
    `clusrun /nodes:azurecn* ipconfig`

3. 메시지가 표시되면 클러스터 관리자 암호를 입력합니다. 명령 출력 비슷한 toohello 다음 표시 됩니다.
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a>테스트 작업 실행
이제 hello 하이브리드 클러스터에서 실행 되는 테스트 작업을 제출 합니다. 이 예제는 간단한 매개 변수 스윕 작업(본질적으로 병렬 계산 형식)입니다. 정수 tooitself hello를 사용 하 여 추가 하는 하위 작업을 실행 하는이 예제 **set /a** 명령입니다. Hello 클러스터의 모든 hello 노드 1 too100에서 정수에 대 한 toofinishing hello 하위 작업의 영향을 미칩니다.

1. HPC 클러스터 관리자에서 **작업 관리** > **New Parametric Sweep Job(새 매개 변수 스윕 작업)**을 클릭합니다.
   
    ![새 작업][test_job1]

2. Hello에 **새 파라메트릭 스윕 작업** 대화 상자의 **명령줄**, 형식 `set /a *+*` (나타나는 hello 기본 명령줄 덮어쓰기). 설정, 남은 hello에 대 한 기본값을 유지 하 고 클릭 **전송** toosubmit hello 작업 합니다.
   
    ![매개 변수 스윕][param_sweep1]

3. Hello 작업이 완료 되 면 hello를 두 번 클릭 **내 작업 된 스윕 작업** 작업 합니다.

4. 클릭 **작업 보기**를 클릭 한 다음 해당 하위 작업의 하위 작업 tooview 계산 hello 출력 하 고 있습니다.
   
    ![작업 결과][view_job361]

5. 노드는 해당 하위 작업에 대 한 hello 계산을 수행 하는 toosee 클릭 **노드 할당**합니다. 클러스터에서 다른 노드 이름이 표시할 수도 있습니다.
   
    ![작업 결과][view_job362]

## <a name="stop-hello-azure-nodes"></a>중지 hello Azure 노드
Hello 클러스터 아웃을 시도한 후 hello Azure 노드 tooavoid 불필요 한 요금 tooyour 계정을 중지 합니다. 이 단계는 hello 클라우드 서비스를 중지 하 고 hello Azure 역할 인스턴스를 제거 합니다.

1. HPC 클러스터 관리자의 **노드 관리**(이전 버전의 HPC Pack에서 **리소스 관리**)에서 두 Azure 노드를 모두 선택합니다. 그런 다음 **중지**를 클릭합니다.
   
    ![노드 중지][stop_node1]

2. Hello에 **중지 Windows Azure 노드** 대화 상자를 클릭 **중지**합니다. 
   
3. hello 노드 전환 toohello **중지** 상태입니다. 몇 분 후 HPC 클러스터 관리자는 hello 노드는 표시 **된**합니다.
   
    ![배포되지 않은 노드][stop_node4]

4. Azure에서 더 이상 hello 역할 인스턴스는 실행에서 tooconfirm hello Azure 포털에서 클릭 **클라우드 서비스 (클래식)** > *your_cloud_service_name*합니다. 인스턴스가는 hello 프로덕션 환경에 배포 됩니다. 
   
    Hello 자습서를 완료 했습니다.

## <a name="next-steps"></a>다음 단계
* 에 대 한 hello 설명서 탐색 [HPC Pack](https://technet.microsoft.com/library/cc514029)합니다.
* 하이브리드 큰 규모에 HPC Pack 클러스터 배포를 tooset 참조 [Microsoft HPC Pack을 사용한 tooAzure 작업자 역할 인스턴스에 버스트](http://go.microsoft.com/fwlink/p/?LinkID=200493)합니다.
* Azure의 HPC Pack 클러스터의 다른 방법으로 toocreate 포함 하 여 Azure 리소스 관리자 템플릿을 사용 하 여 참조 [Azure의 Microsoft HPC Pack을 사용한 HPC 클러스터 옵션](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
