---
title: "Azure 기계 학습에서 온-프레미스 SQL Server는 aaaUse | Microsoft Docs"
description: "와 Azure 기계 학습 데이터는 온-프레미스 SQL Server 데이터베이스 tooperform advanced analytics에서 사용 합니다."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 08e4610d-02b6-4071-aad7-a2340ad8e2ea
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: garye;krishnan
ms.openlocfilehash: c0e9908e296b97b31611ef0192744a59073acd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-advanced-analytics-with-azure-machine-learning-using-data-from-an-on-premises-sql-server-database"></a>온-프레미스 SQL Server 데이터베이스의 데이터를 사용하여 Azure 기계 학습을 통해 고급 분석 수행

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

온-프레미스 데이터로 작업 하는 기업에서는 주로 작업 부하를 학습 하는 해당 컴퓨터에 대 한 hello 클라우드의 민첩성 및 hello 눈금의 tootake 활용 것인지 합니다. 하지만 되지 않도록 toodisrupt 자신의 현재 비즈니스 프로세스와 워크플로 온-프레미스 데이터 toohello 클라우드를 이동 하 여 합니다. 이제 Azure 기계 학습은 온-프레미스 SQL Server 데이터베이스의 데이터를 읽은 다음, 이 데이터를 사용하여 교육을 하고 모델 점수를 매길 수 있도록 지원합니다. 더 이상 hello 클라우드와 온-프레미스 서버 간에 toomanually 복사 및 동기화 hello 데이터 해야합니다. 대신, hello **데이터 가져오기** 교육 및 작업 점수 매기기에 대 한 온-프레미스 SQL Server 데이터베이스에서 직접 Azure 기계 학습 스튜디오의 모듈 읽을 이제 있습니다.

이 문서에서는 어떻게 tooingress 온-프레미스 SQL server 데이터 Azure 기계 학습에 대 한 개요를 제공 합니다. 여기서는 사용자가 작업 영역, 모듈, 데이터 집합, 실험 *등*의 Azure Machine Learning 개념에 익숙하다고 가정하겠습니다.

> [!NOTE]
> 이 기능을 무료 작업 영역에서는 사용할 수 없습니다. 기계 학습 가격 책정 및 계층에 대한 자세한 내용은 [Azure 기계 학습 가격 책정](https://azure.microsoft.com/pricing/details/machine-learning/)을 참조하세요.
>
>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="install-hello-microsoft-data-management-gateway"></a>Hello Microsoft 데이터 관리 게이트웨이 설치 합니다.
Azure 기계 학습에서 온-프레미스 SQL Server 데이터베이스 tooaccess toodownload 및 설치 hello Microsoft 데이터 관리 게이트웨이 해야합니다. 기계 학습 스튜디오에서 hello 게이트웨이 연결을 구성 hello 기회를 다운로드 하 여 hello를 사용 하 여 hello 게이트웨이 설치 하 게 **다운로드 및 레지스터 데이터 게이트웨이** 대화 상자는 아래 설명 합니다.

또한 다운로드 하 고 hello에서 hello MSI 설치 패키지를 실행 하 여 미리 hello 데이터 관리 게이트웨이 설치할 수 [Microsoft 다운로드 센터](https://www.microsoft.com/download/details.aspx?id=39717)합니다.
32 비트 또는 64 비트 컴퓨터에 대 한 적절 하 게 선택 하는 hello 최신 버전을 선택 합니다. MSI hello 사용된 tooupgrade 기존 데이터 관리 게이트웨이 toohello 최신 버전을 유지 하는 모든 설정 될 수도 있습니다.

hello 게이트웨이 hello 다음 필수 구성 요소에 있습니다.

* Windows 운영 체제 버전 지원 hello Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012 및 Windows Server 2012 r 2는 합니다.
* hello는 hello 게이트웨이 컴퓨터에 대 한 구성은 2ghz 이상, 4 코어, 8GB RAM 및 80GB 디스크 하는 것이 좋습니다.
* Hello 호스트 컴퓨터 최대 절전 모드로 전환 hello 게이트웨이 toodata 요청 응답 하지 않습니다. 따라서 hello 게이트웨이 설치 하기 전에 hello 컴퓨터에 적절 한 전원 관리를 구성 합니다. Hello 컴퓨터가 구성 된 toohibernate 이면 hello 게이트웨이 설치는 메시지를 표시 합니다.
* 복사 활동 특정 빈도로 나타나므로 hello 리소스 사용 (CPU, 메모리) hello 컴퓨터에도 hello 유휴 시간 피크와 같은 패턴을 따릅니다. 리소스 사용률도에 따라 달라 집니다 hello 양의 데이터를 이동 합니다. 여러 복사 작업이 진행 중인 경우 사용량이 많은 시간 동안 리소스 사용량이 증가하는 것을 볼 수 있습니다. 위에 나열 된 hello 최소 구성으로 기술적으로 충분 하는 동안 데이터 이동은 특정 부하에 따라 toohave hello 최소 구성 보다 더 많은 리소스가 구성을 할 수 있습니다.

Hello 다음 설정 및 데이터 관리 게이트웨이 사용 하는 경우를 고려해 야 합니다.

* 단일 컴퓨터에 데이터 관리 게이트웨이 인스턴스를 하나만 설치할 수 있습니다.
* 여러 온-프레미스 데이터 원본에 대해 단일 게이트웨이를 사용할 수 있습니다.
* 여러 게이트웨이 toohello 서로 다른 컴퓨터에 연결할 수 있습니다 동일한 온-프레미스 데이터 원본입니다.
* 한 번에 하나의 작업 영역에 대해서만 게이트웨이를 구성합니다. 현재, 작업 영역 간에 게이트웨이를 공유할 수 없습니다.
* 단일 작업 영역에 대해 여러 게이트웨이를 구성할 수 있습니다. 예를 들어 준비 toooperationalize 했으면 toouse 개발 중 테스트 데이터 소스 연결된 tooyour 게이트웨이와 프로덕션 게이트웨이 원하는 수 있습니다.
* hello 게이트웨이 toobe hello hello 데이터 원본으로 동일한 컴퓨터에 필요 하지 않습니다. 하지만 데이터 원본을 더 가깝기 때문 toohello 유지 hello 게이트웨이 tooconnect toohello 데이터 원본에 대 한 hello 시간 줄어듭니다. 과에서 다른 해당 호스트 hello 온-프레미스 데이터 원본 하나 hello 하므로 hello 게이트웨이 및 데이터 원본 하지 경쟁 리소스에 대 한 컴퓨터에 hello 게이트웨이 설치 하는 것이 좋습니다.
* 컴퓨터에 Power BI 또는 Azure Data Factory 시나리오를 처리할 게이트웨이가 이미 설치된 경우 다른 컴퓨터에 Azure 기계 학습을 위한 별도의 게이트웨이를 설치하세요.

  > [!NOTE]
  > Hello에 데이터 관리 게이트웨이 및 Power BI 게이트웨이 실행할 수 없습니다 동일한 컴퓨터.
  >
  >
* 다른 데이터에 대 한 Azure ExpressRoute를 사용 하는 경우에 Azure 기계 학습 toouse hello 데이터 관리 게이트웨이가 필요 합니다. ExpressRoute를 사용하더라도 데이터 원본은 방화벽으로 보호되는 온-프레미스 데이터 원본으로 취급해야 합니다. 기계 학습 및 hello 데이터 원본 간의 hello 데이터 관리 게이트웨이 tooestablish 연결 기능을 사용 합니다.

Hello 문서에서 필수 구성 요소 설치, 설치 단계 및 문제 해결 팁에 대 한 자세한 정보를 찾을 수 있습니다 [데이터 관리 게이트웨이](../data-factory/data-factory-data-management-gateway.md)합니다.

## <a name="span-idusing-the-data-gateway-step-by-step-walk-classanchorspan-idtoc450838866-classanchorspanspaningress-data-from-your-on-premises-sql-server-database-into-azure-machine-learning"></a><span id="using-the-data-gateway-step-by-step-walk" class="anchor"><span id="_Toc450838866" class="anchor"></span></span>온-프레미스 SQL Server 데이터베이스의 데이터를 Azure 기계 학습으로 수신
이 연습에서는 Azure 기계 학습 작업 영역에서 데이터 관리 게이트웨이를 설정하고 구성한 후 온-프레미스 SQL Server 데이터베이스에서 데이터를 읽습니다.

> [!TIP]
> 시작하기 전에 `studio.azureml.net`에 대한 브라우저의 팝업 차단을 사용하지 않도록 설정합니다. Hello Google Chrome 브라우저를 사용 하는 경우 다운로드 하 여 여러 플러그 인에서 Google Chrome WebStore hello 중 하나를 설치 [앱 확장 두 번 클릭 하 여](https://chrome.google.com/webstore/search/clickonce?_category=extensions)합니다.
>
>

### <a name="step-1-create-a-gateway"></a>1단계: 게이트웨이 만들기
첫 번째 단계 hello toocreate 이며 hello 게이트웨이 tooaccess 온-프레미스 SQL 데이터베이스 설정 합니다.

1. 로그 너무[Azure 기계 학습 스튜디오](https://studio.azureml.net/Home/) 및 toowork에 원하는 선택 hello 작업 영역입니다.
2. Hello 클릭 **설정** hello에 블레이드 왼쪽과 hello 클릭 **데이터 게이트웨이** hello 위쪽 탭 합니다.
3. 클릭 **새 데이터 게이트웨이** hello hello 화면 맨 아래에 있습니다.

    ![새 데이터 게이트웨이](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-button.png)
4. Hello에 **새 데이터 게이트웨이** 대화 상자에서 입력 hello **게이트웨이 이름** 하 고 필요에 따라 추가 **설명**합니다. Hello 맨 아래 오른쪽 모서리 toogo toohello의 다음 단계인 hello 구성에서 hello 화살표를 클릭 합니다.

    ![게이트웨이 이름 및 설명 입력](media/machine-learning-use-data-from-an-on-premises-sql-server/new-data-gateway-dialog-enter-name.png)
5. Hello에 다운로드 하 여 등록 데이터 게이트웨이 대화 상자, hello 게이트웨이 등록 키 toohello 클립보드로 복사 합니다.

    ![다운로드 및 데이터 게이트웨이 등록](media/machine-learning-use-data-from-an-on-premises-sql-server/download-and-register-data-gateway.png)
6. <span id="note-1" class="anchor"></span>아직 다운로드 하 여 설치한 경우 Microsoft 데이터 관리 게이트웨이 hello 다음 클릭 **다운로드 데이터 관리 게이트웨이**합니다. Toothe Microsoft 다운로드 센터 hello 게이트웨이 버전을 선택할 수 있는 사용자이는이 필요 하 고 다운로드 한 설치 합니다. Hello 문서의 hello 시작 부분에서 필수 구성 요소 설치, 설치 단계 및 문제 해결 팁에 대 한 자세한 정보를 찾을 수 있습니다 [온-프레미스 원본 및 데이터 관리 게이트웨이와클라우드간데이터이동](../data-factory/data-factory-move-data-between-onprem-and-cloud.md).
7. Hello 데이터 관리 게이트웨이 구성 관리자가 열리고 hello hello 게이트웨이가 설치 된 후 **레지스터 게이트웨이** 대화 상자가 표시 됩니다. 붙여넣기 hello **게이트웨이 등록 키** 누른 toohello 클립보드에 복사한 **등록**합니다.
8. 설치 된 게이트웨이 이미 있는 경우 hello 데이터 관리 게이트웨이 구성 관리자를 실행 합니다. 클릭 **키 변경**, 붙여는 **게이트웨이 등록 키** toohello 클립보드 hello 이전 단계에서 복사한 **확인**합니다.
9. Hello 설치가 완료 되 면 hello **레지스터 게이트웨이** 에 대 한 Microsoft 데이터 관리 게이트웨이 구성 관리자 대화 상자가 표시 됩니다. Hello 이전 단계에서 hello 클립보드에 복사 하는 게이트웨이 등록 키를 붙여 넣고 클릭 **등록**합니다.

    ![게이트웨이 등록](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-register-gateway.png)
10. hello 게이트웨이 구성이 완료 된 다음 값에는 hello hello에 설정 된 경우 **홈** 탭에서 Microsoft 데이터 관리 게이트웨이 구성 관리자:

    * **게이트웨이 이름이** 및 **인스턴스 이름을** hello 게이트웨이의 toohello 이름을 설정 합니다.
    * **등록** 너무 설정**등록 된**합니다.
    * **상태** 너무 설정**Started**합니다.
    * hello 아래쪽 디스플레이에 hello 상태 표시줄 **tooData 관리 게이트웨이 클라우드 서비스에 연결 된** 녹색 확인 표시와 함께 합니다.

      ![데이터 관리 게이트웨이 관리자](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-registered.png)

      또한 azure 기계 학습 스튜디오 hello 등록이 완료 되 면 업데이트를 가져옵니다.

    ![게이트웨이 등록 성공](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-registered.png)
11. Hello에 **다운로드 하 고 데이터 게이트웨이 등록** 대화 상자에서 확인 표시 toocomplete hello 설정을 클릭 합니다. hello **설정을** 페이지 "Online"으로 게이트웨이 상태를 표시 합니다. Hello 오른쪽 창에서 상태 및 기타 유용한 정보를 찾을 수 있습니다.

    ![게이트웨이 설정](media/machine-learning-use-data-from-an-on-premises-sql-server/gateway-status.png)
12. Hello Microsoft 데이터 관리 게이트웨이 구성 관리자에서에서 toohello 전환 **인증서** 이 탭에 지정 된 탭 hello 인증서가 지정 하는 hello 온-프레미스 데이터 저장소에 대 한 자격 증명 사용 되는 tooencrypt/암호 해독 hello 포털입니다. 이 인증서는 hello 기본 인증서입니다. 인증서 관리 시스템에 백업 하는이 tooyour 자체 인증서를 변경 하는 것이 좋습니다. 클릭 **변경** toouse 고유의 인증서 대신 합니다.

    ![게이트웨이 인증서 변경](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-certificate.png)
13. (선택 사항) Hello 게이트웨이 통해 문제를 해결 하기 위한 자세한 정보 로깅 tooenable 원한다 면 hello Microsoft 데이터 관리 게이트웨이 구성 관리자에서에서 전환 toothe **진단** 탭 하 고 hello 확인 **사용 하도록 설정 자세한 문제 해결을 위해 로깅을** 옵션입니다. hello 로깅 정보에서에서 확인할 수 있습니다 hello에서 Windows 이벤트 뷰어 hello **Applications and Services Logs**  - &gt; **데이터 관리 게이트웨이** 노드. Hello를 사용할 수도 있습니다 **진단** 탭 tootest hello 연결 tooan 온-프레미스 데이터 원본 hello 게이트웨이 사용 하 여 합니다.

    ![자세한 로깅 정보 표시 사용](media/machine-learning-use-data-from-an-on-premises-sql-server/data-gateway-configuration-manager-verbose-logging.png)

Azure 기계 학습에서 hello 게이트웨이 설치 과정을 완료합니다.
사용자는 이제 준비 toouse 온-프레미스 데이터입니다.

각 작업 영역에 대한 스튜디오에서 여러 게이트웨이를 만들고 설정할 수 있습니다. 예를 들어 프로덕션 데이터 원본에 대 한 개발 및 다른 게이트웨이 중 tooconnect tooyour 테스트 데이터 소스를 사용할 게이트웨이 할 수 있습니다. Azure 기계 학습 유연성 tooset 기업 환경에 따라 여러 게이트웨이를 제공 합니다. 현재는 작업 영역 간에 게이트웨이를 공유할 수 없으며 단일 컴퓨터에 게이트웨이 하나만 설치할 수 있습니다. 자세한 내용은 [온-프레미스 원본과 클라우드 간에 데이터 관리 게이트웨이로 데이터 이동](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)을 참조하세요.

### <a name="step-2-use-hello-gateway-tooread-data-from-an-on-premises-data-source"></a>2 단계: hello 게이트웨이 tooread 데이터를 사용 하 여 온-프레미스 데이터 원본에서
Hello 게이트웨이 설정한 후에 추가할 수는 **데이터 가져오기** hello hello 온-프레미스 SQL Server 데이터베이스의에서 데이터를 입력 하는 실험에는 모듈입니다.

1. 기계 학습 스튜디오에서 선택 hello **실험** 탭을 클릭 **+ 새로 만들기** 왼쪽 아래 모서리 hello와 선택 **빈 실험** (또는 몇 가지 샘플 중 하나를 선택 실험을 사용할 수 있는)입니다.
2. 찾기 및 hello 끌어 **데이터 가져오기** 모듈 toohello 실험 캔버스입니다.
3. 클릭 **다른 이름으로 저장** hello 캔버스 아래 합니다. "Azure 컴퓨터 학습 온-프레미스 SQL Server 자습서" hello 실험 이름에 입력 작업 영역에서 선택한 hello 클릭 **확인** 확인 표시 합니다.

   ![실험을 새 이름으로 저장](media/machine-learning-use-data-from-an-on-premises-sql-server/experiment-save-as.png)
4. Hello 클릭 **데이터 가져오기** 모듈 tooselect, 그런 다음는 **속성** hello에서 "온-프레미스 SQL 데이터베이스"를 선택 하는 hello 캔버스의 오른쪽 창 toohello **데이터 원본** 드롭다운 목록입니다.
5. 선택 hello **데이터 게이트웨이** 설치 하 고 등록 합니다. "(새 데이터 게이트웨이 추가...)"를 선택하여 다른 게이트웨이를 설정할 수 있습니다.

   ![데이터 가져오기 모듈에 대해 데이터 게이트웨이 선택](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-select-on-premises-data-source.png)
6. Hello SQL 입력 **데이터베이스 서버 이름** 및 **데이터베이스 이름**, hello SQL 함께 **데이터베이스 쿼리** tooexecute 원하는 합니다.
7. **사용자 이름 및 암호** 아래에서 **값 입력**을 클릭하고 데이터베이스 자격 증명을 입력합니다. 온-프레미스 SQL Server가 구성된 방식에 따라 Windows 통합 인증 또는 SQL Server 인증을 사용할 수 있습니다.

   ![데이터베이스 자격 증명 입력](media/machine-learning-use-data-from-an-on-premises-sql-server/database-credentials.png)

   "값이 필요" 변경 내용이 너무 "값 집합" 녹색 확인 표시가 있는 hello 메시지입니다. 하기만 하면 tooenter hello 자격 증명 한 번 hello 데이터베이스 정보 또는 암호를 변경 하지 않는 됩니다. Azure 기계 학습 hello 클라우드에서 hello 게이트웨이 tooencrypt hello 자격 증명을 설치할 때 지정한 hello 인증서를 사용 합니다. Azure는 암호화되지 않은 온-프레미스 자격 증명을 절대 저장하지 않습니다.

   ![데이터 모듈 속성 가져오기](media/machine-learning-use-data-from-an-on-premises-sql-server/import-data-properties-entered.png)
8. 클릭 **실행** toorun hello 실험 합니다.

Hello 실험 실행이 종료 되 면 hello의 hello 출력 포트를 클릭 하 여 hello 데이터베이스에서 가져온 hello 데이터를 시각화할 수 있습니다 **데이터 가져오기** 모듈 선택 하 고 **시각화**합니다.

실험 개발이 끝나면 모델을 배포하고 운영할 수 있습니다. 일괄 처리 실행 서비스 hello에 구성 된 hello 온-프레미스 SQL Server 데이터베이스에서 데이터를 hello를 사용 하 여 **데이터 가져오기** 모듈에서 읽고 평가에 사용 합니다. 점수 매기기 온-프레미스 데이터에 대 한 hello 요청 응답 서비스를 사용할 수 있지만 좋습니다를 사용 하는 [Excel 추가 기능에](machine-learning-excel-add-in-for-web-services.md) 대신 합니다. 현재 tooan 작성 온-프레미스 SQL Server 데이터베이스를 통해 **데이터 내보내기** 지원 하거나 실험 또는 게시 된 웹 서비스 않습니다.
