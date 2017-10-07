---
title: "Azure HDInsight 클러스터-aaaHow toodelete | Microsoft Docs"
description: "HDInsight 클러스터를 삭제할 수 있는 다양 한 방법으로 hello에 대 한 정보입니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>브라우저, PowerShell 또는 Azure CLI hello를 사용 하 여 HDInsight 클러스터 삭제

HDInsight 클러스터 결제 클러스터 만들어지고 hello 클러스터를 삭제할 때 중지 되 면 시작 합니다. 분 단위로 청구되므로 더 이상 사용하지 않으면 항상 클러스터를 삭제해야 합니다. 이 문서에서는 Azure 포털, Azure PowerShell 및 Azure CLI 1.0 hello 사용 하 여 클러스터 toodelete hello 하는 방법을 배웁니다.

> [!IMPORTANT]
> HDInsight 클러스터를 삭제 해도 hello Azure 저장소 계정 또는 hello 클러스터와 연결 된 데이터 레이크 저장소입니다. Hello 나중에 해당 서비스에 저장 된 데이터를 다시 사용할 수 있습니다.

## <a name="azure-portal"></a>Azure portal

1. Toohello 로그인 [Azure 포털](https://portal.azure.com) 고 HDInsight 클러스터를 선택 합니다. HDInsight 클러스터에 고정 된 toohello 대시보드 없으면 hello 검색 필드를 사용 하 여 이름별으로 검색할 수 있습니다.
   
    ![포털 검색](./media/hdinsight-delete-cluster/navbar.png)

2. Hello 블레이드 hello 클러스터에 대 한가 되 면 선택 hello **삭제** 아이콘입니다. 메시지가 나타나면 선택 **예** toodelete hello 클러스터입니다.
   
    ![삭제 아이콘](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

PowerShell 프롬프트에서 다음 명령을 toodelete hello 클러스터 hello를 사용 합니다.

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

대체 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의 합니다.

## <a name="azure-cli-10"></a>Azure CLI 1.0

프롬프트에서 다음 toodelete hello 클러스터 hello를 사용 합니다.

    azure hdinsight cluster delete CLUSTERNAME

대체 **CLUSTERNAME** HDInsight 클러스터의 hello 이름의 합니다.

> [!NOTE]
> Azure CLI 2.0은 현재(2017년 7월 31일) HDInsight 클러스터를 삭제하도록 지원하지 않습니다.