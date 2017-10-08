---
title: "hello 팀 데이터 과학 프로세스에 대 한 aaaCustomize Hadoop 클러스터 | Microsoft Docs"
description: "일반적인 Python 모듈을 사용자 지정 Azure HDInsight Hadoop 클러스터에서 사용할 수 있습니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0c115dca-2565-4e7a-9536-6002af5c786a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: e192542dd39f71bccbb5163382b4050d0f12ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-azure-hdinsight-hadoop-clusters-for-hello-team-data-science-process"></a>Hello 팀 데이터 과학 프로세스에 대 한 Azure HDInsight Hadoop 클러스터를 사용자 지정
이 문서에서는 64 비트 Anaconda (Python 2.7)를 설치 하 여 toocustomize HDInsight Hadoop 클러스터 방법을 각 노드에서 hello 클러스터는 HDInsight 서비스로 프로 비전 될 때 또한 tooaccess toosubmit 사용자 지정 작업 toohello 클러스터 헤드 노드에 hello 하는 방법을 보여 줍니다. 이 사용자 지정 여러 인기 있는 Python 모듈, Anaconda에 포함 된으로 편리 하 게에 사용할 수 있는 사용자 정의 함수 (Udf)를 tooprocess hello 클러스터의 Hive 레코드 설계 합니다. 이 시나리오에서 사용 하는 hello 프로시저에 대 한 자세한 내용은 참조 하십시오. [어떻게 toosubmit 하이브 쿼리](machine-learning-data-science-move-hive-tables.md#submit)합니다.

hello 다음과 같은 메뉴가 링크 tooset hello 다양 한 데이터 과학 환경에서 어떻게 사용 hello를 설명 하는 tootopics [팀 데이터 과학 프로세스 (TDSP)](data-science-process-overview.md)합니다.

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

## <a name="customize"></a>Azure HDInsight Hadoop 클러스터 사용자 지정
사용자 지정 된 HDInsight Hadoop 클러스터 toocreate 너무 로그온 하 여 시작[**Azure 클래식 포털**](https://manage.windowsazure.com/), 클릭 **새로** hello 왼쪽에 아래 모퉁이 한 다음 데이터 서비스를 선택 HDINSIGHT->-> **사용자 지정 만들기** hello toobring **클러스터 세부 정보** 창. 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

1, 구성 페이지에서 만든 hello 클러스터 toobe의 hello 이름을 입력 하 고 다른 필드 hello에 대 한 기본값을 적용 합니다. Hello 화살표 toogo toohello 다음 구성 페이지를 클릭 합니다. 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img1.png)

구성 페이지 2의 hello 수를 입력 **데이터 노드**선택, hello **지역/가상 네트워크**의 hello hello 크기를 선택 하 고 **헤드 노드** 및 hello **데이터 노드**합니다. Hello 화살표 toogo toohello 다음 구성 페이지를 클릭 합니다.

> [!NOTE]
> hello **지역/가상 네트워크** toobe toobe hello HDInsight Hadoop 클러스터에 사용 되는 이동 하는 hello 저장소 계정의 hello 영역으로 hello 동일 했습니다. 그렇지 않으면 hello 네 번째 구성 페이지에서 hello 저장소 계정에 표시 되지 것입니다 hello 드롭다운 목록이 **계정 이름**합니다.
> 
> 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img3.png)

구성 페이지 3 hello HDInsight Hadoop 클러스터에 대 한 사용자 이름 및 암호를 제공 합니다. **없는** 선택 hello *Enter hello Hive/Oozie Metastore*합니다. 그런 다음 hello 화살표 toogo toohello 다음 구성 페이지를 클릭 합니다. 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img4.png)

구성 페이지 4 hello 저장소 계정 이름, hello HDInsight Hadoop 클러스터의 hello 기본 컨테이너를 지정 합니다. 선택 하는 경우 *기본 컨테이너 만들기* hello에 **기본 컨테이너** 드롭다운 목록, hello 사용 하 여 컨테이너 이름과 같은 이름을 hello 클러스터를 만들 때. Hello 화살표 toogo toohello 마지막 구성 페이지를 클릭 합니다.

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/customize-cluster-img5.png)

최종 hello에 **스크립트 동작** 구성 페이지에서 클릭 **스크립트 동작 추가** 단추를 클릭 한 다음 값에는 hello로 hello 텍스트 필드를 입력 합니다.

* **이름** -hello 이름과이 스크립트 동작의 모든 문자열
* **노드 유형** - **모든 노드**를 선택합니다.
* **스크립트 URI** - *http://getgoing.blob.core.windows.net/publicscripts/Azure_HDI_Setup_Windows.ps1* 
  * *publicscripts* 은 hello 저장소 계정에서 공용 컨테이너 
  * *getgoing* tooshare PowerShell 스크립트 파일 toofacilitate 사용자 작업 사용 하 여 Azure에서
* **매개 변수** - 비어 있는 상태로 둡니다.

마지막으로, 사용자 지정 하는 hello HDInsight Hadoop 클러스터 hello 확인 표시가 toostart hello 만들기를 클릭 합니다. 

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/script-actions.png)

## <a name="headnode"></a>액세스 hello Hadoop 클러스터의 헤드 노드
RDP를 통해 hello Hadoop 클러스터의 헤드 노드 hello에 액세스 하려면 먼저 Azure에서 원격 액세스 toohello Hadoop 클러스터를 사용 하도록 설정 해야 합니다. 

1. Toohello 로그인 [ **Azure 클래식 포털**](https://manage.windowsazure.com/)선택, **HDInsight** hello 왼쪽에 클러스터의 hello 목록에서 Hadoop 클러스터를 선택, hello  **구성** 탭을 클릭 한 다음 hello **원격 사용** hello hello 페이지 맨 위에 있는 아이콘입니다.
   
    ![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-1.png)
2. Hello에 **원격 데스크톱 구성** 창 hello 사용자 이름 및 암호 필드를 입력 하 고 원격 액세스를 위한 hello 만료 날짜를 선택 합니다. Hello 확인 표시가 tooenable hello 원격 액세스 toohello 클러스터의 헤드 노드 hello Hadoop 클릭 합니다.
   
    ![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-2.png)

> [!NOTE]
> hello 사용자 이름 및 원격 액세스 hello에 대 한 암호 없는 hello 사용자 이름 및 암호를 hello Hadoop 클러스터를 만들 때 사용 합니다. 이는 별도의 자격 증명 집합입니다. 또한 hello 원격 액세스의 hello 만료 날짜는 현재 날짜 로부터 hello 7 일 이내 toobe 됩니다.
> 
> 

원격 액세스를 사용 하도록 설정한 후 클릭 **연결** hello 헤드 노드로 hello 페이지 tooremote hello 맨 아래에 있습니다. 이전에 지정한 hello 원격 액세스 사용자에 대 한 hello 자격 증명을 입력 하 여 hello Hadoop 클러스터의 헤드 노드 toohello에 로그온 합니다.

![작업 영역 만들기](./media/machine-learning-data-science-customize-hadoop-cluster/enable-remote-access-3.png)

hello hello 고급 분석 프로세스의에서 다음 단계에에서 매핑된 hello [팀 데이터 과학 프로세스 (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) 처리 하 고 hello 데이터 로부터 학습을 위한 준비 과정에서 샘플링 하는 것이 있으면 HDInsight에 테이블로 데이터를 이동 하는 단계를 포함할 수 있습니다 와 Azure 기계 학습 합니다.

참조 [어떻게 toosubmit 하이브 쿼리](machine-learning-data-science-move-hive-tables.md#submit) tooaccess hello 사용자 정의 함수 (Udf) 사용 하는 tooprocess 있는 클러스터의 헤드 노드에서 hello Anaconda에 포함 된 Python 모듈 hello 하는 방법에 대 한 지침은 하이브 저장 된 레코드 hello 클러스터에서.

