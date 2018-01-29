---
title: "Azure 스택 저장소 계정을 관리 | Microsoft Docs"
description: "찾기, 관리, 복구 및 저장소 계정은 Azure 스택 회수 하는 방법을 알아봅니다"
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 6e14bd6312135b45984a82099e68a934ec2a4a70
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a>Azure 스택에서 저장소 계정을 관리합니다
찾아를 복구 하 고 비즈니스 요구에 따라 저장소 용량을 회수 스택 Azure에서에서 저장소 계정을 관리 하는 방법을 알아봅니다.

## <a name="find"></a>저장소 계정 찾기
하 여 Azure 스택의 지역에서 저장소 계정 목록을 볼 수 있습니다.

1. 인터넷 브라우저에서 https://adminportal.local.azurestack.external로 이동 합니다.
2. (배포 중에 제공한 자격 증명을 사용 하 여) 클라우드 연산자로 스택 Azure 관리 포털에 로그인
3. 기본 대시보드-찾습니다는 **지역 관리** 나열 하 고 탐색 영역을 클릭 합니다. 예를 들어 **(로컬**).
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. 선택 **저장소** 에서 **리소스 공급자** 목록입니다.
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. 이제 저장소 리소스 공급자 관리자 블레이드의 –으로 아래로 스크롤하여는 **저장소 계정** 탭을 클릭 합니다.
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   결과 페이지에는 해당 지역에서 저장소 계정의 목록입니다.
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

기본적으로 처음 10 개의 계정이 표시 됩니다. 더 인출 하도록 선택할 수 있습니다를 클릭 하 여는 **자세히 알아보려면** 목록의 맨 아래에 링크 합니다.

또는

특정 저장소 계정-에 관심이 있는 경우 다음을 할 수 있습니다 **필터링 하 고 관련 계정 인출** 만 합니다.


**계정에 대 한 필터링:**

1. 클릭 **필터** 블레이드 맨 위에 있는 합니다.
2. 필터 블레이드에서 것 지정할 수 있습니다 **계정 이름**, **구독 ID** 또는 **상태** 표시할 저장소 계정 목록을 세밀 하 게 조정 합니다. 적절 한으로 사용 합니다.
3. **업데이트**를 클릭합니다. 목록에 따라 새로 고쳐야 합니다.
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. 필터를 다시 설정 하려면: 클릭 **필터**, 선택 항목을 제거 하 고 업데이트 합니다.

검색 텍스트 상자 (상단에 있는 저장소 계정 목록 블레이드) 계정 목록에서 선택한 텍스트를 강조 표시할 수 있습니다. 이 전체 이름 또는 id가 쉽게 사용할 수 있는 경우에 유용 합니다.

에 관심이 있는 계정을 찾을 수 있도록 여기에서 무료 텍스트를 사용할 수 있습니다.

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a>계정 세부 정보를 확인
보기에 관심이 있는 계정을 찾은 후에 특정 세부 정보를 보려면 특정 계정을 클릭 수 있습니다. 와 같은 계정 세부 정보로는 새 블레이드가 열립니다: 계정, 만든 시간, 위치 등의 형식입니다.

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a>삭제 된 계정 복구
삭제 된 계정 복구 해야 하는 경우에는 수도 있습니다.

Azure 스택에서 작업을 수행 하는 매우 간단 하 게가 있습니다.

1. 저장소 계정 목록을 찾습니다. 참조 [저장소 계정의 찾을](#find) 에 대 한 자세한 내용은이 항목의 합니다.
2. 목록에서 해당 특정 계정을 찾습니다. 필터링 할 수 있습니다.
3. 확인 된 *상태* 계정. 이 필드 **Deleted**합니다.
4. 계정 세부 정보 블레이드에서 열립니다 계정을 클릭 합니다.
5. 이 블레이드 맨 위에 찾을 **복구** 단추와 해당 연결을 클릭 합니다.
6. **예** 를 클릭하여 확인합니다.
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. 복구에는 이제 *처리... 대기* 성공 했는지 확인 합니다.
   진행률 표시를 보려면 포털 맨 위에 있는 "종 모양" 아이콘을 클릭할 수도 있습니다.
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   복구 된 계정을 성공적으로 동기화 되 면 다시 사용할 수 있습니다.

### <a name="some-gotchas"></a>몇 가지 주의 사항이
* 삭제 된 계정으로 상태를 보여 줍니다. **보존 부족**합니다.
  
  즉, 삭제 한 계정의 보존 기간을 초과 했습니다 고 복구할 수 있습니다.
* 삭제 한 계정의 계정 목록에 표시 되지 않습니다.
  
  삭제 한 계정의 가비지 수집 이미를 의미할 수 있습니다. 이 경우 복구할 수 없습니다. 참조 [용량을 회수](#reclaim) 이 항목의 합니다.

## <a name="set-the-retention-period"></a>보존 기간 설정
보존 기간 설정을 삭제 한 계정의 잠재적으로는 복구할 수 (0부터 9999 한 일에서 시간 기간을 지정 하는 클라우드 연산자 수 있습니다. 기본 보존 기간을 15 일로 설정 됩니다. 값을 삭제 한 계정의 즉시 보존 벗어났습니다 및 주기적 가비지 수집에 대 한 표시 "0"으로 설정 합니다.

**변경 하려면 보존 기간:**

1. 인터넷 브라우저에서 https://adminportal.local.azurestack.external로 이동 합니다.
2. (배포 중에 제공한 자격 증명을 사용 하 여) 클라우드 연산자로 스택 Azure 관리 포털에 로그인
3. 기본 대시보드-찾습니다는 **지역 관리** 나열 하 고 탐색-예를 들어 영역을 클릭 **(로컬**).
4. 선택 **저장소** 에서 **리소스 공급자** 목록입니다.
5. 클릭 **설정을** 위쪽으로 설정 블레이드를 엽니다.
6. 클릭 **구성** 다음 보존 기간 값을 편집 합니다.

   일 수를 설정 하 고 저장 합니다.
   
   이 값은 즉시 효과적 하 고 해당 전체 지역에 대해 설정 됩니다.

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <a name="reclaim"></a>용량을 회수 합니다.
보존 기간이 설정 된 것의 부작용 중 하나를 삭제 한 계정의 계속 보존 기간에 나올 때까지 용량을 소비입니다. 클라우드 운영자는 보존 기간을 아직 만료 되지 않은 경우에 삭제 한 계정의 공간을 회수 하는 방법을 할 수 있습니다.

포털 또는 PowerShell을 사용 하 여 용량을 회수할 수 있습니다.

**용량을 회수 하는 포털을 사용 하 여:**
1. 저장소 계정 블레이드로 이동 합니다. 참조 [저장소 계정의 찾을](#find)합니다.
2. 클릭 **공간을 회수** 블레이드 맨 위에 있는 합니다.
3. 메시지를 클릭 한 다음 **확인**합니다.

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. 성공 알림을 참조 포털에서 종 모양 아이콘 기다립니다.

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. 저장소 계정 페이지를 새로 고칩니다. 삭제 된 계정은 제거 되었기 때문에 더 이상 목록에 표시 됩니다.

또한 PowerShell을 사용 하 여 보존 기간을 명시적으로 재정의 수 있으며 즉시 용량을 회수할 수 있습니다.

**용량을 회수 하 PowerShell을 사용 하 여:**   

1. Azure PowerShell 설치 및 구성 되어 있는지 확인 합니다. 없다면 다음 지침을 따르십시오. 
   * 최신 Azure PowerShell 버전을 설치 하려면 Azure 구독과 연결 참조 [Azure PowerShell 설치 및 구성 하는 방법을](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)합니다.
   Azure 리소스 관리자 cmdlet에 대 한 자세한 내용은 참조 [Azure PowerShell 사용 하 여 Azure 리소스 관리자](http://go.microsoft.com/fwlink/?LinkId=394767)
2. 다음 cmdlet을 실행합니다.

> [!NOTE]
> 이 cmdlet을 실행 계정 및 해당 내용을 영구적으로 삭제 합니다. 복구할 수는 없습니다. 주의 하 여이 사용 합니다.


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


자세한 내용은 참조 [Azure 스택 powershell 설명서입니다.](https://msdn.microsoft.com/library/mt637964.aspx)
 

## <a name="migrate-a-container"></a>컨테이너 마이그레이션
테 넌 트를 균일 하지 않은 저장소 사용 인해 클라우드 운영자 하나를 찾을 수 또는 더 기본 테 넌 트 다른 항목 보다 더 많은 공간을 사용 하 여 공유 합니다. 이 경우 클라우드 운영자는 다른 공유를 일부 blob 컨테이너를 수동으로 마이그레이션하여 강세 공유에 공간을 확보 시도할 수 있습니다. 

PowerShell을 사용 하 여 컨테이너를 마이그레이션하려 합니다.
> [!NOTE]
>Blob 컨테이너 마이그레이션 실시간 마이그레이션을 지원 하지 않습니다 및 현재 사용 되는 오프 라인 작업. 마이그레이션 중 하며 완료 될 때까지 해당 컨테이너의 기본 blob에 사용할 수 없습니다 "오프 라인"입니다. 

**PowerShell을 사용 하 여 컨테이너를 마이그레이션:**

1. Azure PowerShell 설치 및 구성 되어 있는지 확인 합니다. 없다면 다음 지침을 따르십시오.
    * 최신 Azure PowerShell 버전을 설치 하려면 Azure 구독과 연결 참조 [Azure PowerShell 설치 및 구성 하는 방법을](http://azure.microsoft.com/documentation/articles/powershell-install-configure/)합니다. Azure 리소스 관리자 cmdlet에 대 한 자세한 내용은 참조 [Azure PowerShell 사용 하 여 Azure 리소스 관리자](http://go.microsoft.com/fwlink/?LinkId=394767)
2. 팜 이름 가져오기: 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. 공유를 가져옵니다. 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. 지정 된 공유에 대 한 컨테이너를 가져옵니다. 개수와 의도 선택적 매개 변수는 참고:
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   그런 다음 $containers 없는지 확인 합니다.

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. 컨테이너 마이그레이션에 대 한 최상의 대상 공유를 가져옵니다.

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    그런 다음 $destinationshares 없는지 확인 합니다.

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. 컨테이너에 대 한 마이그레이션 해제 퇴장 시킵니다, 그리고 하나는 공유의 모든 컨테이너를 반복 하 고 반환 된 작업 id를 사용 하 여 상태를 추적할 수 있으므로이 비동기 구현입니다.

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    그런 다음 $jobId 없는지 확인 합니다.

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. 해당 작업 id로 마이그레이션 작업의 상태를 확인 합니다. 컨테이너 마이그레이션 완료 되 면 MigrationStatus "Completed"로 설정 됩니다.

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. 진행 중인 마이그레이션 작업을 취소할 수 있습니다. 다시 비동기 작업 이므로 $jobid를 사용 하 여 추적할 수 있습니다.

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    다시 마이그레이션 취소의 상태를 확인할 수 있습니다.

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  