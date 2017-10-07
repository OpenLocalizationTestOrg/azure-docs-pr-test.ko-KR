---
title: "Hive 및 Hadoop-Azure HDInsight를 사용 하 여 aaaAnalyze 센서 데이터 | Microsoft Docs"
description: "Tooanalyze 센서 데이터를 사용 하 여 HDInsight (Hadoop)와 쿼리 콘솔 하이브 hello 하는 방법을 알아보려면 다음 PowerView 사용 하 여 Microsoft excel에서 hello 데이터를 시각화 합니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 70e595705c33d9835dc9809161f79c3ac5ece870
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-using-hello-hive-query-console-on-hadoop-in-hdinsight"></a>HDInsight에서 Hadoop에서 하이브 쿼리 콘솔 hello를 사용 하 여 센서 데이터 분석

Tooanalyze 센서 데이터를 사용 하 여 HDInsight (Hadoop)와 쿼리 콘솔 하이브 hello 하는 방법을 알아보려면 다음 Power View를 사용 하 여 Microsoft Excel에서 hello 데이터를 시각화 합니다.

> [!IMPORTANT]
> 이 문서 에서만 작동 하는 Windows 기반 HDInsight 클러스터의에서 hello 단계. HDInsight는 HDInsight 3.4 이하 버전의 경우 Windows에서만 사용 가능합니다. Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.


이 샘플에서 하이브 tooprocess 기록 데이터를 사용 하 여 한 난방 및 공기 조절 시스템과 문제를 식별 합니다. 시스템을 식별 하는 구체적으로 수 없습니다. tooreliably 유지 집합 온도 hello 다음 작업을 수행 하 여:

* 만들기 하이브 쉼표로 구분 된 값 (CSV) 파일에 저장 된 tooquery 데이터 테이블입니다.
* 하이브 쿼리 tooanalyze hello 데이터를 만듭니다.
* tooretrieve hello 분석 데이터를 Microsoft Excel tooconnect tooHDInsight를 사용 합니다.
* toovisualize hello 데이터는 Power View를 사용 합니다.

![Hello 솔루션 아키텍처 다이어그램](./media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a>필수 조건

* HDInsight(Hadoop) 클러스터: 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.
* Microsoft Excel 2013

  > [!NOTE]
  > Microsoft Excel은 [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US)를 통한 데이터 시각화에 사용됩니다.

* [Microsoft Hive ODBC 드라이버](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="toorun-hello-sample"></a>toorun hello 예제

1. 웹 브라우저에서 url toohello 이동: 

         https://<clustername>.azurehdinsight.net

    대체 `<clustername>` HDInsight 클러스터의 hello 이름의 합니다.

    메시지가 표시 되 면 hello 관리자 사용자 이름 및이 클러스터를 프로 비전 할 때 사용한 암호를 사용 하 여 인증 합니다.

2. Hello 열리면 hello 웹 페이지에서 클릭 하 **시작 갤러리** 탭을 선택한 다음 hello **샘플 데이터를 사용 하 여 솔루션** 범주를 hello 클릭 **센서 데이터 분석** 샘플입니다.

    ![갤러리 이미지 시작하기](./media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. Hello 웹 페이지 toofinish hello 샘플에서 제공 하는 hello 지침을 따릅니다.
