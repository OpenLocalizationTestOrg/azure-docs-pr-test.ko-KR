---
title: "Azure 리소스 그룹 프로젝트를 사용 하 여 VS Team Services에서 aaaContinuous 통합 | Microsoft Docs"
description: "Visual Studio에서 Azure 리소스 그룹 배포를 사용 하 여 Visual Studio Team Services에서 연속 통합을 tooset 프로젝션 하는 방법을 설명 합니다."
services: visual-studio-online
documentationcenter: na
author: mlearned
manager: erickson-doug
editor: 
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: 0fe4a4b8989ee323e8ef2206fa4ebed503025670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-integration-in-visual-studio-team-services-using-azure-resource-group-deployment-projects"></a>Azure 리소스 그룹 배포 프로젝트를 사용하여 Visual Studio Team Services에서 연속 통합
다양 한 단계에서 작업을 수행 Azure 템플릿 toodeploy: 빌드, 테스트, 복사 tooAzure ("준비" 라고도 함) 및 서식 파일을 배포 합니다. 두 가지 방법으로 toodeploy 템플릿 tooVisual Studio Team Services (VS Team Services) 있습니다. 두 방법 모두 hello 동일한 결과 제공 하므로 hello 워크플로 가장 잘 맞는 하나를 선택 합니다.

1. Hello Azure 리소스 그룹 배포 프로젝트 (deploy-azureresourcegroup.ps1 스크립트로)에 포함 된 hello PowerShell 스크립트를 실행 하는 단일 단계 tooyour 빌드 정의 추가 합니다. hello 스크립트 아티팩트를 복사한 다음 hello 서식 파일을 배포 합니다.
2. 각각 단계 작업을 수행하는 여러 VS Team Services 빌드 단계를 추가합니다.

이 문서에서는 두 옵션 모두를 보여 줍니다. hello 첫 번째 옵션 이점이 hello Visual Studio에서 개발자가 동일한 스크립트를 사용 하는 hello를 사용 하 고 hello 수명 주기 전체에서 일관성을 제공 합니다. hello 두 번째 옵션은 편리 하 게 대체 toohello 기본 제공 스크립트를 제공합니다. 두 절차에서는 이미 VS Team Services에 Visual Studio 배포 프로젝트를 체크인했다고 가정합니다.

## <a name="copy-artifacts-tooazure"></a>아티팩트 tooAzure 복사
템플릿 배포에 필요한 모든 아티팩트가 있으면 hello 시나리오에 관계 없이 Azure 리소스 관리자 액세스 toothem를 부여 해야 있습니다. 이러한 아티팩트에는 다음과 같은 파일이 포함될 수 있습니다.

* 중첩된 템플릿
* 구성 스크립트 및 DSC 스크립트 
* 응용 프로그램 이진 파일

### <a name="nested-templates-and-configuration-scripts"></a>중첩된 템플릿 및 구성 스크립트
Visual Studio에서 제공 하는 hello 서식 파일을 사용 하는 경우 (또는 Visual Studio 코드 조각을 사용 하 여 빌드한) hello PowerShell 스크립트 뿐만 아니라 hello 아티팩트를 준비, 다양 한 배포에 대 한 hello 리소스에 대 한 hello URI에서 매개 변수화도 합니다. hello 스크립트 그런 다음 Azure의 hello 아티팩트 tooa 보안 컨테이너를 복사, 해당 컨테이너에 대 한 SaS 토큰을 만드는 데 및 toohello 템플릿 배포에 대 한 정보를 전달 합니다. 참조 [템플릿 배포를 만드는](https://msdn.microsoft.com/library/azure/dn790564.aspx) 중첩 템플릿에서 toolearn에 더 알아봅니다.  VS Team Services의 작업을 사용할 경우 템플릿 배포에 대 한 hello 적절 한 작업을 선택 하 고 필요한 경우 단계 toohello 템플릿 배포를 준비 하는 hello에서 매개 변수 값을 전달 해야 합니다.

## <a name="set-up-continuous-deployment-in-vs-team-services"></a>VS Team Services에서 연속 배포 설정
tooupdate 해야 toocall VS Team Services에서 PowerShell 스크립트를 hello, 빌드 정의 합니다. 간단히 말해서 hello 단계는 같습니다. 

1. Hello 빌드 정의 편집 합니다.
2. VS Team Services에서 Azure 권한을 설정합니다.
3. Hello Azure 리소스 그룹 배포 프로젝트에서 hello PowerShell 스크립트를 참조 하는 Azure PowerShell 빌드 단계를 추가 합니다.
4. Hello의 hello 값 설정 *-ArtifactsStagingDirectory* VS Team Services에서 빌드한 프로젝트와 toowork 매개 변수입니다.

### <a name="detailed-walkthrough-for-option-1"></a>옵션1에 대한 자세한 연습
hello 다음 절차에 관한 hello 단계 필요한 tooconfigure hello PowerShell 스크립트 프로젝트에서 실행 되는 단일 작업을 사용 하 여 VS Team Services에서 연속 배포입니다. 

1. VS Team Services 빌드 정의를 편집하고 Azure PowerShell 빌드 단계를 추가합니다. Hello에서 hello 빌드 정의 선택 **빌드 정의** 범주 hello 선택 **편집** 링크 합니다.
   
   ![빌드 정의 편집][0]
2. 새로 추가 **Azure PowerShell** 빌드 단계 toohello 빌드 정의 선택한 후 hello **빌드 단계 추가 중...** 단추를 선택합니다.
   
   ![빌드 단계 추가][1]
3. Hello 선택 **배포 작업** 범주, 선택 hello **Azure PowerShell** 의 작업을 선택한 후 해당 **추가** 단추입니다.
   
   ![작업 추가][2]
4. Hello 선택 **Azure PowerShell** 빌드 단계 및 해당 값을 입력 합니다.
   
   1. Azure 서비스 끝점 추가 tooVS Team Services 이미 있는 경우, hello에 hello 구독 선택 **Azure 구독** 드롭다운 목록 상자와 skip toohello 다음 섹션. 
      
      VS Team Services에서 Azure 서비스 끝점을 없다면 tooadd 하나 필요 합니다. 이 하위 섹션에서는 hello 과정을 안내합니다. Azure 계정에서 Microsoft 계정 (예: Hotmail)를 사용 하는 경우 서비스 사용자 인증 hello 단계 tooget 다음 수행 해야 합니다.
   2. Hello 선택 **관리** 다음 toohello 연결 **Azure 구독** 드롭다운 목록 상자입니다.
      
      ![Azure 구독 관리][3]
   3. 선택 **Azure** hello에 **새 서비스 끝점** 드롭다운 목록 상자입니다.
      
      ![새 서비스 끝점][4]
   4. Hello에 **Azure 구독 추가** 대화 상자, 선택 hello **서비스 사용자** 옵션입니다.
      
      ![서비스 주체 옵션][5]
   5. 추가 Azure 구독 정보 toohello **Azure 구독 추가** 대화 상자. 다음 항목 tooprovide hello가 필요 합니다.
      
      * 구독 ID
      * 구독 이름
      * 서비스 주체 ID
      * 서비스 주체 키
      * 테넌트 ID
   6. 선택한 toohello의 이름을 추가 **구독** 이름 상자입니다. 이 값 표시 hello의 뒷부분에 나오는 **Azure 구독** VS Team Services에서 드롭 다운 목록입니다. 
   7. Azure 구독 ID를 모르는 경우 다음 명령을 tooretrieve hello 중 하나를 사용할 수 있습니다 것입니다.
      
      PowerShell 스크립트의 경우 
      
      `Get-AzureRmSubscription`
      
      Azure CLI의 경우 
      
      `azure account show`
   8. 서비스 보안 주체 ID를 서비스 사용자 키 및 테 넌 트 ID tooget hello 절차에 따라 [만드는 Active Directory 응용 프로그램 및 서비스 사용자 포털을 사용 하 여](resource-group-create-service-principal-portal.md) 또는 [인 서비스 사용자를 인증 합니다. Azure 리소스 관리자](resource-group-authenticate-service-principal.md)합니다.
   9. 서비스 사용자 ID, 서비스 사용자 키 및 테 넌 트 ID 값 toohello 추가 hello **Azure 구독 추가** 대화 상자를 선택한 후 hello **확인** 단추입니다.
      
      Azure PowerShell 스크립트는 유효한 서비스 사용자 toouse toorun hello를 생깁니다.
5. Hello 빌드 정의 편집 하 고 hello 선택 **Azure PowerShell** 빌드 단계입니다. Hello에 hello 구독 선택 **Azure 구독** 드롭다운 목록 상자입니다. (Hello 구독 표시 되지 않으면 hello 선택 **새로 고침** 단추 다음 hello **관리** 링크 합니다.) 
   
   ![Azure PowerShell 빌드 작업 구성][8]
6. 경로 toohello deploy-azureresourcegroup.ps1 스크립트로 PowerShell 스크립트를 제공 합니다. toodo이 hello 줄임표 (...) 단추 다음 toohello 선택 **스크립트 경로** 상자에서 hello에서 deploy-azureresourcegroup.ps1 스크립트로 PowerShell 스크립트를 toohello 이동 **스크립트** 프로젝트의 폴더 선택 선택한 후 hello **확인** 단추입니다.    
   
   ![경로 선택 tooscript][9]
7. Hello 스크립트를 선택한 후 hello 경로 toohello 스크립트 hello Build.StagingDirectory에서에서 실행 될 수 있도록 업데이트 (동일한 디렉터리 hello 하 *ArtifactsLocation* 로 설정). "$(Build.StagingDirectory)/" toohello 경로의 시작 부분 hello 스크립트 추가 하 여 수행할 수 있습니다입니다.
   
    ![경로 tooscript 편집][10]
8. Hello에 **스크립트 인수** 상자 hello 매개 변수 (한 줄으로) 다음을 입력 합니다. Visual Studio에서 hello 스크립트를 실행할 때 VS 사용 하 여 hello에 대 한 매개 변수를 hello 하는 방법을 확인할 수 있습니다 **출력** 창. 빌드 단계에서 hello 매개 변수 값을 설정 하기 위한 시작 지점으로 사용할 수 있습니다.
   
   | 매개 변수 | 설명 |
   | --- | --- |
   | -ResourceGroupLocation |지리적 위치 값 hello 리소스 그룹은 같이 hello **eastus** 또는 **' 미국 동부 '**합니다. (Hello 이름에 공백이 있는 경우 작은따옴표로 추가 합니다.) 자세한 내용은 [Azure 지역](https://azure.microsoft.com/en-us/regions/)을 참조하세요. |
   | -ResourceGroupName |이 배포에 사용 되는 hello 리소스 그룹의 hello 이름입니다. |
   | -UploadArtifacts |이 매개 변수 있는 경우 toobe 해야 하는 아티팩트 업로드 지정 tooAzure hello 로컬 시스템에서입니다. 필요할 때만 tooset이이 스위치 템플릿 배포 추가 아티팩트 (예: 구성 스크립트 또는 중첩 된 템플릿도) hello PowerShell 스크립트를 사용 하 여 toostage 한다는 것을 요구 하는 경우. |
   | -StorageAccountName |이 배포에 대 한 toostage 아티팩트를 사용 하는 hello hello 저장소 계정의 이름입니다. 이 매개 변수는 배포에 대한 아티팩트를 준비하는 경우에만 사용됩니다. 이 매개 변수가 제공 되는 경우에 새 저장소 계정은 hello 스크립트는 이전 배포 하는 동안 생성 되지 않은 만들어집니다. Hello 매개 변수를 지정 하는 경우 hello 저장소 계정은 이미 있어야 합니다. |
   | -StorageAccountResourceGroupName |hello 저장소 계정과 연결 된 hello 리소스 그룹의 hello 이름입니다. 이 매개 변수는 hello StorageAccountName 매개 변수에 대 한 값을 제공 하는 경우에 필요 합니다. |
   | -TemplateFile |hello toohello 템플릿 파일 경로 hello Azure 리소스 그룹 배포 프로젝트. tooenhance 유연성을는 hello 절대 경로가 아닌 PowerShell 스크립트의 상대 toohello 위치는이 매개 변수에 대 한 경로 사용 합니다. |
   | -TemplateParametersFile |hello toohello 매개 변수 파일 경로 hello Azure 리소스 그룹 배포 프로젝트. tooenhance 유연성을는 hello 절대 경로가 아닌 PowerShell 스크립트의 상대 toohello 위치는이 매개 변수에 대 한 경로 사용 합니다. |
   | -ArtifactStagingDirectory |이 매개 변수는 hello PowerShell 스크립트를에서 hello 프로젝트의 이진 파일을 복사할 hello 폴더를 알고 있습니다. 이 값 hello PowerShell 스크립트에서 사용 하는 hello 기본값을 재정의 합니다. VS Team Services에 사용 하 여 hello 값으로 설정:-ArtifactStagingDirectory $(Build.StagingDirectory) |
   
   스크립트 인수 예는 다음과 같습니다(읽기 쉽도록 줄 구분).
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   완료 되 면 hello **스크립트 인수** 상자 목록 다음 hello와 유사 합니다.
   
   ![스크립트 인수][11]
9. Azure PowerShell 빌드 단계 항목을 필요한 대로 toohello hello 모두 추가한 후 선택 hello **큐** 단추 toobuild hello 프로젝트를 빌드합니다. hello **빌드** 화면 hello PowerShell 스크립트의에서 출력을 hello를 보여줍니다.

### <a name="detailed-walkthrough-for-option-2"></a>옵션2에 대한 자세한 연습
hello 다음 절차에 관한 hello 단계 필요한 tooconfigure hello 제공 되는 작업을 사용 하 여 VS Team Services에서 연속 배포입니다.

1. VS Team Services 빌드 정의 tooadd 두 개의 새 빌드 단계를 편집 합니다. Hello에서 hello 빌드 정의 선택 **빌드 정의** 범주 hello 선택 **편집** 링크 합니다.
   
   ![빌드 정의 편집][12]
2. 추가 hello 새 빌드 단계 hello를 사용 하 여 toohello 빌드 정의 **빌드 단계 추가 중...** 단추를 선택합니다.
   
   ![빌드 단계 추가][13]
3. Hello 선택 **배포** 작업 범주, 선택 hello **Azure 파일 복사** 의 작업을 선택한 후 해당 **추가** 단추입니다.
   
   ![Azure File Copy 작업 추가][14]
4. Hello 선택 **Azure 리소스 그룹 배포** 의 작업을 다음 선택 해당 **추가** 단추 차례로 **닫기** hello **작업 카탈로그**합니다.
   
   ![Azure 리소스 그룹 배포 작업 추가][15]
5. Hello 선택 **Azure 파일 복사** 작업 및 해당 값을 입력 합니다.
   
   Azure 서비스 끝점 추가 tooVS Team Services 이미 있는 경우, hello에 hello 구독 선택 **Azure 구독** 드롭다운 목록 상자입니다. 구독이 없는 경우 VS Team Services에서 구독을 설정하는 방법에 대한 지침은 [옵션 1](#detailed-walkthrough-for-option-1)을 참조하세요.
   
   * 원본 - **$(Build.StagingDirectory)** 입력
   * Azure 연결 형식 - **Azure Resource Manager** 선택
   * Azure RM 구독-toouse hello에 원하는 hello 저장소 계정에 대 한 선택 hello 구독 **Azure 구독** 드롭다운 목록 상자입니다. Hello 구독 표시 되지 않으면 hello 선택 **새로 고침** 단추 다음 hello **관리** 링크 합니다.
   * 대상 형식 - **Azure Blob** 선택
   * RM 저장소 계정-선택 hello 저장소 계정이 toouse 아티팩트를 준비 하 시겠습니까
   * 컨테이너 이름-hello 이름을 입력 hello 컨테이너의 원하는 toouse 준비;에 대 한 모든 올바른 컨테이너 이름이 될 수 있지만 하나의 전용된 toothis 빌드 정의 사용 하 여
   
   Hello 출력 값에 대 한 합니다.
   
   * 저장소 컨테이너 URI - **artifactsLocation** 입력
   * 저장소 컨테이너 SAS 토큰 - **artifactsLocationSasToken** 입력
   
   ![Azure File Copy 작업 구성][16]
6. Hello 선택 **Azure 리소스 그룹 배포** 빌드 단계 및 해당 값을 입력 합니다.
   
   * Azure 연결 형식 - **Azure Resource Manager** 선택
   * Azure RM 구독-hello에 대 한 배포에 대 한 선택 hello 구독 **Azure 구독** 드롭다운 목록 상자입니다. 동일한 구독에 사용 되는 hello hello 이전 단계에서 일반적으로 됩니다.
   * 작업 - **리소스 그룹 만들기 또는 업데이트** 선택
   * 리소스 그룹-리소스 그룹 이름 선택 또는 입력 hello 새 리소스 그룹의 hello 배포에 대 한
   * 위치-hello 리소스 그룹에 대 한 선택 hello 위치
   * 템플릿의 경우-hello 템플릿 배포 toobe 앞의 hello 경로 이름을 입력 **$(Build.StagingDirectory)**예를 들면: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * 템플릿 매개 변수-입력을 사용 하는 hello 매개 변수 toobe의 hello 경로 이름 앞에 추가 **$(Build.StagingDirectory)**예를 들면: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * 템플릿 매개 변수 재정의-입력 하거나 복사 하 코드 다음 hello를 붙여넣습니다.
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Azure 리소스 그룹 배포 작업 구성][17]
7. 모든 필요한 hello 항목을 추가한 후 hello 빌드 정의 저장 하 고 선택 **새 빌드 큐 대기** hello 위쪽에 있습니다.

## <a name="next-steps"></a>다음 단계
읽기 [Azure 리소스 관리자 개요](azure-resource-manager/resource-group-overview.md) toolearn Azure 리소스 관리자 및 Azure 리소스 그룹에 대 한 자세한 합니다.

[0]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: ./media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
