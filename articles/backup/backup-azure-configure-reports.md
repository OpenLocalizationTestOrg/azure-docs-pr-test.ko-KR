---
title: "Azure 백업에 대 한 aaaConfigure 보고서"
description: "이 문서에서는 Recovery Services 자격 증명 모음을 사용하여 Azure Backup에 대한 Power BI 보고서를 구성하는 방법을 설명합니다."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>Azure Backup 보고서 구성
이 문서 발언 단계 tooconfigure 보고서에 대 한 복구 서비스 자격 증명 모음 및 tooaccess를 사용 하 여 Azure 백업에 대 한 Power BI를 사용 하 여 이러한 보고서. 다음이 단계를 수행한 후 있습니다 수 직접 tooPower BI tooview 모든 hello 보고서를 이동, 사용자 지정 보고서를 만듭니다. 

## <a name="supported-scenarios"></a>지원되는 시나리오
1. Azure 백업 보고서는 Azure 가상 컴퓨터 백업 및 파일/폴더 백업 toocloud Azure 복구 서비스 에이전트를 사용 하 여에 대 한 지원 됩니다.
2. Azure SQL, DPM 및 Azure Backup Server에 대한 보고서는 현재 지원되지 않습니다.
3. 볼 수 있습니다 보고서 및 구독, 자격 증명 모음에서 동일한 저장소 계정이 각 hello 자격 증명 모음에 대해 구성 된 경우. 선택한 저장소 계정 hello에 있어야 합니다. 동일한 지역 복구 서비스 자격 증명 모음입니다.
4. hello 보고서에 대 한 예정 된 새로 고침 빈도 hello에는 Power BI에서 24 시간입니다. Power bi에서 보고서를 렌더링 하기 위한 고객 저장소 계정에서 최신 데이터를 사례을 사용 하는 hello 보고서의 임시 새로 고침을 수행할 수도 있습니다. 

## <a name="prerequisites"></a>필수 조건
1. 만들기는 [Azure 저장소 계정](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure에 대해 보고 합니다. 이 저장소 계정은 보고서 관련 데이터를 저장하는 데 사용됩니다.
2. [Power BI 계정을 만듭니다](https://powerbi.microsoft.com/landing/signin/) tooview, 사용자 지정 하 고 Power BI 포털을 사용 하 여 보고서를 만듭니다.
3. Hello 리소스 공급자 등록이 **Microsoft.insights** 등록 되어 있지 이미 저장소 계정의 hello 구독 및 복구 서비스의 hello 구독과 자격 증명 모음에 tooenable tooflow toohello 데이터를 보고 합니다. 저장소 계정입니다. 동일한 toodo hello, tooAzure 포털 야 합니다. > 구독 > 리소스 공급자와 공급자 tooregister이에 대 한 확인 것입니다. 

## <a name="configure-storage-account-for-reports"></a>보고서에 대한 저장소 계정 구성
Azure 포털을 사용 하 여 복구 서비스 자격 증명 모음에 대 한 단계 tooconfigure hello 저장소 계정을 다음 hello를 사용 합니다. 이것은 일회성 구성 하 고 저장소 계정이 구성 되 면 보고서 tooview 콘텐츠 팩 및 활용 하 여 직접 tooPower BI 이동할 수 있습니다.
1. 복구 서비스 자격 증명 모음 열고 이미 있는 경우 toonext 단계를 진행 합니다. 복구 서비스 자격 증명 모음 열기를 갖지 않는 hello hello 허브 메뉴에서 Azure 포털에 있지만 클릭 **찾아보기**합니다.

   * Hello 리소스 목록에 입력 **복구 서비스**합니다.
   * 입력을 시작할 때 hello 사용자 입력에 따라 필터를 나열 합니다. **복구 서비스 자격 증명 모음**이 표시되면 클릭합니다.

      ![복구 서비스 자격 증명 모음 만들기 1단계](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     복구 서비스 자격 증명 모음 hello 목록이 표시 됩니다. 복구 서비스 자격 증명 모음 hello 목록에서 자격 증명 모음을 선택 합니다.

     hello 선택한 자격 증명 모음 대시보드를 엽니다.
2. Hello 목록에서 항목의 자격 증명 모음 아래에 나타나는 클릭 **백업 보고서** 모니터링 및 보고서 섹션 tooconfigure hello 저장소 계정에서 보고서에 대 한 합니다.

      ![백업 보고서 메뉴 항목 선택 2단계](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. Hello 백업 보고서 블레이드에서 클릭 **구성** 단추입니다. Toocustomer 저장소 계정의 데이터를 밀어 넣는 데 사용 되는 hello Azure Application Insights 블레이드가 열립니다.

      ![저장소 계정 구성 3단계](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. 너무 hello 상태 토글 단추가 설정**에** 선택 **보관 저장소 계정 tooa** 확인란을 선택 하 여 데이터 흐름 toohello 저장소 계정에 시작할 수를 보고 합니다.

      ![진단 사용 4단계](./media/backup-azure-configure-reports/set-status-on.png)
5. 저장소 계정 선택 및 보고 데이터와 클릭을 저장 하는 것에 대 한 hello 목록에서 선택 hello 저장소 계정을 클릭 **확인**합니다.

      ![저장소 계정 선택 5단계](./media/backup-azure-configure-reports/select-storage-account.png)
6. 선택 **AzureBackupReport** 확인란을 선택 하 고도 hello 슬라이더 tooselect 보존 기간이에 대 한 이동 데이터를 보고 합니다. Hello 저장소 계정의 데이터를에서 보고이 슬라이더를 사용 하 여 선택 하는 hello 기간 동안 보관 됩니다.

      ![저장소 계정 선택 6단계](./media/backup-azure-configure-reports/save-configuration.png)
7. 모든 hello 변경 내용을 검토 하 고 클릭 **저장** 위의 hello 그림에 나와 있는 것 처럼 위쪽에 단추입니다. 이 작업을 수행하면 모든 변경 내용이 저장되며, 이제 보고 데이터를 저장하는 데 사용할 저장소 계정이 구성되었습니다.

> [!NOTE]
> 저장소 계정을 저장 하 여 보고서를 구성 하 고 나면 해야 **24 시간 동안 대기** 푸시 toocomplete 초기 데이터에 대 한 합니다. 이 시간 이후에만 Power BI에서 Azure Backup 콘텐츠 팩을 가져와야 합니다. 자세한 내용은 [FAQ 섹션](#frequently-asked-questions)을 참조하세요. 
>
>

## <a name="view-reports-in-power-bi"></a>Power BI에서 보고서 보기 
복구 서비스 자격 증명 모음을 사용 하 여 보고서에 대 한 저장소 계정을 구성 하는 후에 약 24 시간 정도의 흐름에 데이터 toostart 보고용 걸립니다. 저장소 계정 설정의 24 시간 후 사용 하 여 hello 다음 Power BI의 보고서 tooview 단계:
1. [로그인](https://powerbi.microsoft.com/landing/signin/) tooPower BI 합니다.
2. **데이터 가져오기**를 클릭한 다음 콘텐츠 팩 라이브러리의 **서비스**에서 가져오기를 클릭합니다. 언급 한 단계를 사용 하 여 [설명서 tooaccess Power BI 콘텐츠 팩](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/)합니다.

     ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-import.png)
3. 검색 창에서 **Azure Backup**을 입력하고 **지금 가져오기**를 클릭합니다.

      ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-get.png)
4. 위의 5 단계에서 구성 된 hello 저장소 계정 이름을 입력 하 고 클릭 **다음** 단추입니다.

    ![저장소 계정 이름 입력](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. 이 저장소 계정에 대 한 hello 저장소 계정 키를 입력 합니다. 있습니다 수 [표시 및 저장소 액세스 키를 복사](../storage/common/storage-create-storage-account.md#manage-your-storage-account) Azure 포털에서 저장소 계정의 tooyour 이동 하 여 합니다. 

     ![저장소 계정 입력](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. **로그인** 단추를 클릭합니다. 로그인에 성공하면 **데이터를 가져오는 중** 알림이 표시됩니다.

    ![콘텐츠 팩 가져오기](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    가져올 일정 시간이 지난 후 **성공** hello 가져오기가 완료 된 후에 알림입니다. Hello 저장소 계정에는 데이터의 많은 있는 경우 거의 긴 tooimport hello 콘텐츠 팩을 걸릴 수 있습니다.
    
    ![콘텐츠 팩 가져오기 성공](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. 데이터를 성공적으로 가져온 후 **Azure 백업** 콘텐츠 팩을 볼 수 있으면 **앱** hello 탐색 창에서. hello 목록 새로 가져온된 보고서 나타내는 노란색 별이 있는 Azure 백업 대시보드, 보고서 및 데이터 집합을 이제 표시 됩니다. 

     ![Azure Backup 콘텐츠 팩](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. 대시보드에서 **Azure Backup**을 클릭합니다. 일련의 고정 키 보고서가 표시됩니다.

      ![Azure Backup 대시보드](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. tooview hello 전체 보고서를 집합 hello 대시보드에서 임의의 보고서를 클릭 합니다.

      ![Azure Backup 작업 상태](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. 해당 영역의 hello 보고서 tooview 보고서의 각 탭을 클릭 합니다.

      ![Azure Backup 보고서 탭](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>질문과 대답
1. **보고 데이터 흐름 toostorage 계정에 시작 된 경우 확인 방법**
    
    Toohello 저장소를 이동할 수 있습니다 계정 구성 및 선택 컨테이너입니다. Hello 컨테이너 insights-로그-azurebackupreport에 대 한 항목이 있으면, 보고 데이터가 시작 되었음을 흐름 나타냅니다.

2. **데이터 푸시 toostorage 계정 및 Azure 백업에서 Power BI 콘텐츠 팩의 hello 주파수 이란?**

   Day 0 사용자에 대 한 약 24 시간 동안 toopush 데이터 toostorage 계정을 걸립니다. 이 초기 푸시 compelete 되 면 아래 hello 그림에 표시 된 빈도 따라 hello로 데이터가 새로 고쳐집니다. 
      * 데이터가 너무 관련**작업, 경고, 백업 항목, 자격 증명 모음, 보호 된 서버 및 정책** 으로 toocustomer 저장소 계정 및 기록 되는 경우 푸시됩니다.
      * 데이터가 너무 관련**저장소** 24 시간 마다 toocustomer 저장소 계정 푸시됩니다.
   
    ![Azure Backup 보고서 데이터 푸시 빈도](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  Power BI에는 [하루에 한 번 예약된 새로 고침](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed)이 있습니다. Power BI에서 콘텐츠 팩 hello에 대 한 hello 데이터 수동 새로 고침을 수행할 수 있습니다.

3. **Hello 보고서를 유지할 수는 기간** 

   저장소 계정, 구성 하는 동안 hello 저장소 계정 (위의 보고서 섹션에 대 한 구성 저장소 계정에서 6 단계를 사용)에서 보고 데이터의 보존 기간을 선택할 수 있습니다. 뿐만 아니라 [Excel에서 보고서를 분석](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/)하고 요구에 따라 더 오랜 보존 기간 동안 저장할 수 있습니다. 

4. **Hello 저장소 계정을 구성한 후 보고서의 내 모든 데이터를 볼 수 있습니까?**

   모든 이후 생성 된 데이터를 hello **"저장소 계정 구성"** toohello 저장소 계정 밀어넣습니다 및 보고서에서 사용할 수 있습니다. 그러나 **진행 중인 작업은 보고를 위해 푸시되지 않습니다**. Hello 작업 완료 또는 실패를 일단 tooreports를 전송 됩니다.

5. **이미 hello 저장소 계정 tooview 보고서를 구성 하려면 경우 변경 hello 구성 toouse 다른 저장소 계정** 

   예, hello 구성 toopoint tooa 다른 저장소 계정을 변경할 수 있습니다. TooAzure 백업에 대 한 콘텐츠 팩을 연결 하는 동안 hello 새로 구성 된 저장소 계정을 사용 해야 합니다. 또한 다른 저장소 계정이 구성된 후 새 데이터는 이 저장소 계정으로 흐릅니다. 하지만 hello 구성 변경) (이전 오래 된 데이터는 여전히 hello 이전 저장소 계정에 유지 됩니다.

6. **여러 자격 증명 모음 및 구독의 보고서를 볼 수 있나요?** 

   예, hello를 구성할 수 있습니다 동일한 저장소 계정에서 다양 한 tooview 크로스-자격 증명 모음 보고서 자격 증명 모음입니다. 구성할 수는 또한 구독에서 동일한 저장소 계정 자격 증명 모음에 대 한 hello 합니다. 다음 백업 tooAzure tooview hello Power BI 보고서의 콘텐츠 팩을 연결 하는 동안이 저장소 계정을 사용할 수 있습니다. 하지만 Hello에 hello 저장소 계정을 선택 해야 동일한 지역 복구 서비스 자격 증명 모음입니다.
   
## <a name="next-steps"></a>다음 단계
이제 hello 저장소 계정 및 Azure 백업 콘텐츠 팩을 가져온된, hello 다음 단계를 사용 하도록 구성한입니다 toocustomize 이러한 보고서 및 데이터 모델 toocreate 보고서를 보고 사용 합니다. Hello 문서에 대 한 자세한 내용은 다음을 참조 하십시오.

* [Azure Backup 보고 데이터 모델 사용](backup-azure-reports-data-model.md)
* [Power BI에서 보고서 필터링](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [Power BI에서 보고서 만들기](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

