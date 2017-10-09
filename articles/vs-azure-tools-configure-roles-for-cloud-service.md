---
title: "Azure에 대 한 aaaConfigure hello 역할 클라우드 Visual Studio와 함께 서비스 | Microsoft Docs"
description: "자세한 내용은 방법 tooset 및 Visual Studio를 사용 하 여 Azure 클라우드 서비스에 대 한 역할을 구성 합니다."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Visual Studio를 사용하여 Azure 클라우드 서비스 역할 구성
Azure 클라우드 서비스에는 하나 이상의 작업자 또는 웹 역할이 포함될 수 있습니다. 각 역할에 대해 해당 역할 설정 방법 toodefine 필요한 고도 실행 방식을 구성 합니다. 클라우드 서비스의 역할에 대해 자세히 toolearn hello 비디오를 참조 하세요. [소개 tooAzure 클라우드 서비스](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services)합니다. 

클라우드 서비스에 대 한 hello 정보는 다음 파일이 hello에 저장 됩니다.

- **ServiceDefinition.csdef** -hello 서비스 정의 파일은 필요한 역할을 포함 하 여 클라우드 서비스, 끝점 및 가상 컴퓨터 크기에 대 한 hello 런타임 설정을 정의 합니다. 에 저장 된 hello 데이터 없음 `ServiceDefinition.csdef` 역할이 실행 되는 경우에 변경할 수 있습니다.
- **ServiceConfiguration.cscfg** -hello 서비스 구성 파일 실행 되는 역할의 인스턴스 수를 구성 하 고 역할에 대해 정의 된 hello 설정의 hello 값입니다. 에 저장 된 데이터를 hello `ServiceConfiguration.cscfg` 역할이 실행 되는 동안에 변경할 수 있습니다.

역할 실행 되는 방식을 제어 하는 hello 설정에 대 한 다른 toostore 값, 여러 서비스 구성을 정의할 수 있습니다. 각 배포 환경에 대해 서로 다른 서비스 구성을 사용할 수 있습니다. 예를 들어, 로컬 서비스 구성에서 저장소 계정 연결 문자열 toouse hello 로컬 Azure 저장소 에뮬레이터를 설정할 수 있으며 hello 클라우드에서 다른 서비스 구성 toouse Azure 저장소를 만듭니다.

Visual Studio에서 Azure 클라우드 서비스를 만들 때 두 개의 서비스 구성이 자동으로 만들어집니다 및 tooyour Azure 프로젝트를 추가 합니다.

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Azure 클라우드 서비스 구성
단계를 수행 하는 hello와 같이 Visual Studio에서 솔루션 탐색기에서 Azure 클라우드 서비스를 구성할 수 있습니다.

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.
   
    ![솔루션 탐색기 프로젝트 - 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. Hello 프로젝트의 속성 페이지에서 선택 hello **개발** 탭 합니다. 

    ![프로젝트 속성 페이지 - 개발 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. Hello에 **서비스 구성** 목록, 선택 hello tooedit 원하는 hello 서비스 구성 이름입니다. (선택 toomake이이 역할에 대 한 tooall hello 서비스 구성을 변경 하려면 **모든 구성**.)
   
    > [!IMPORTANT]
    > 특정 서비스 구성을 선택하면 일부 속성은 모든 구성에 대해서만 설정 가능하므로 비활성화됩니다. tooedit 선택 해야 이러한 속성을 **모든 구성**합니다.
    > 
    > 
   
    ![Azure 클라우드 서비스에 대한 서비스 구성 목록](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Hello 역할 인스턴스 수 변경
클라우드 서비스의 tooimprove hello 성능을 hello, 사용자 또는 특정 역할에 대해 예상 되는 hello 로드 hello 수에 따라 실행 중인 역할의 인스턴스 수를 변경할 수 있습니다. Hello 클라우드 서비스가 Azure에서 실행 될 때 별도 가상 컴퓨터 역할의 각 인스턴스에 대해 생성 됩니다. 이 클라우드 서비스의 hello 배포에 대 한 hello 청구가 결정 됩니다. 대금 청구에 대한 자세한 내용은 [Microsoft Azure 청구서 이해](billing/billing-understand-your-bill.md)를 참조하세요.

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다. Hello에서 **역할** 노드, 마우스 오른쪽 단추로 클릭 hello 역할 tooupdate, 한, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.

    ![솔루션 탐색기 - Azure 역할의 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. 선택 hello **구성** 탭 합니다.

    ![구성 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. Hello에 **서비스 구성** 목록, tooupdate 않겠다고 선택 hello 서비스 구성 합니다.
   
    ![서비스 구성 목록](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. Hello에 **인스턴스 수를** 텍스트 상자에이 역할에 대 한 toostart 되도록 인스턴스의 hello 수를 입력 합니다. Hello 클라우드 서비스 tooAzure 게시할 때 각 인스턴스는 별도 가상 컴퓨터에서 실행 됩니다.

    ![Hello 인스턴스 수를 업데이트합니다.](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. Hello Visual Studio에서에서 도구 모음 선택 **저장**합니다.

## <a name="manage-connection-strings-for-storage-accounts"></a>저장소 계정에 대한 연결 문자열 관리
서비스 구성에 대한 연결 문자열을 추가, 제거 또는 수정할 수 있습니다. 예를 들어, `UseDevelopmentStorage=true`값이 있는 로컬 서비스 구성에 대해 로컬 연결 문자열이 필요할 수 있습니다. Azure에서 저장소 계정을 사용 하는 클라우드 서비스 구성을 tooconfigure를 수도 있습니다.

> [!WARNING]
> 저장소 계정 연결 문자열에 대 한 hello Azure 저장소 계정 키 정보를 입력 하면이 정보는 hello 서비스 구성 파일에 로컬로 저장 됩니다. 그러나 현재는 이 정보가 암호화된 텍스트로 저장되지 않습니다.
> 
> 

각 서비스 구성에 대 한 다른 값을 사용 하 여 클라우드 서비스에서 다른 연결 문자열은 toouse 개일 하 또는 클라우드 서비스 tooAzure 게시할 때 코드를 수정 하지 않는 합니다. Hello 코드와 hello 값에 hello 연결 문자열에 같은 이름을 클라우드 서비스를 빌드 또는 게시할 때 선택 하는 hello 서비스 구성에 따라 다를 사용할 수 있습니다.

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다. Hello에서 **역할** 노드, 마우스 오른쪽 단추로 클릭 hello 역할 tooupdate, 한, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.

    ![솔루션 탐색기 - Azure 역할의 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. 선택 hello **설정을** 탭 합니다.

    ![설정 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Hello에 **서비스 구성** 목록, tooupdate 않겠다고 선택 hello 서비스 구성 합니다.

    ![서비스 구성](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. 연결 문자열 tooadd 선택 **설정 추가**합니다.

    ![연결 문자열 추가](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Hello 새 설정이 toohello 목록 추가, hello 목록의 hello 행 hello 필요한 정보로 업데이트 합니다.

    ![새 연결 문자열](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **이름** -hello 연결 문자열에 대 한 toouse 되도록 hello 이름을 입력 합니다.
    - **형식** -선택 **연결 문자열** hello 드롭 다운 목록에서 합니다.
    - **값** -hello에 직접 hello 연결 문자열을 입력 하거나 **값** 셀 또는 hello에 줄임표 (...) toowork 선택 hello **저장소 연결 문자열 만들기** 대화 상자.  

1. Hello에 **저장소 연결 문자열 만들기** 대화 상자에서 옵션에 대 한 **사용 하 여 연결**합니다. 선택한 hello 옵션에 대 한 hello 지침을 따릅니다.

    - **Microsoft Azure 저장소 에뮬레이터** -이 옵션을 선택 하면 tooAzure만 적용 되므로 hello hello 대화 상자에서 나머지 설정이 비활성화 됩니다. **확인**을 선택합니다.
    - **구독** -Microsoft 계정으로이 옵션을 사용 하 여 hello 드롭다운 목록 tooeither select 및 기호를 선택 하거나 Microsoft 계정을 추가 하는 경우. Azure 구독 및 저장소 계정을 선택합니다. **확인**을 선택합니다.
    - **수동으로 입력 한 자격 증명** -hello 저장소 계정 이름을 입력 하 고 기본 키 또는 두 번째 키 hello 중 하나입니다. **연결** 옵션을 선택합니다(대부분의 시나리오에 대해 HTTPS 권장). **확인**을 선택합니다.

1. 연결 문자열 toodelete hello 연결 문자열을 선택한 다음 선택 **설정 제거**합니다.

1. Hello Visual Studio에서에서 도구 모음 선택 **저장**합니다.

## <a name="programmatically-access-a-connection-string"></a>프로그래밍 방식으로 연결 문자열 액세스

hello 다음 단계에서는 tooprogrammatically C#을 사용 하 여 연결 문자열을 액세스 하는 방법을

1. Hello 다음 추가 toouse hello 설정을 어디로 지시문 tooa C# 파일을 사용 하 여:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. hello 다음 코드에서는 방법의 예로 tooaccess 연결 문자열입니다. Hello 대체 &lt;ConnectionStringName > 자리 표시자 hello 적절 한 값으로. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Azure 클라우드 서비스에서 사용자 지정 설정을 toouse 추가
Hello 서비스 구성 파일에서 사용자 지정 설정 이름 및 특정 서비스 구성에 대 한 문자열에 대 한 값을 추가할 수 있습니다. 이 설정은 tooconfigure hello 값을 참조 하 여 클라우드 서비스의 기능을 설정 하 고 코드에서이 값 toocontrol hello 논리를 사용 하 여 hello toouse를 선택할 수 있습니다. 서비스 패키지 toorebuild 필요 없이 또는 클라우드 서비스가 실행 되 고 이러한 서비스 구성 값을 변경할 수 있습니다. 설정이 변경될 때 코드에서 알림을 확인할 수 있습니다. [RoleEnvironment.Changing 이벤트](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx)를 참조하세요.

서비스 구성에 대한 사용자 지정 설정을 추가, 제거 또는 수정할 수 있습니다. 다양한 서비스 구성에 대해 이러한 문자열에 서로 다른 값이 필요할 수 있습니다.

각 서비스 구성에 대 한 다른 값을 사용 하 여 클라우드 서비스에서 다른 문자열은 toouse 개일 하 또는 클라우드 서비스 tooAzure 게시할 때 코드를 수정 하지 않는 합니다. Hello 코드와 hello 값에 hello 문자열에 같은 이름을 클라우드 서비스를 빌드 또는 게시할 때 선택 하는 hello 서비스 구성에 따라 다를 사용할 수 있습니다.

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다. Hello에서 **역할** 노드, 마우스 오른쪽 단추로 클릭 hello 역할 tooupdate, 한, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.

    ![솔루션 탐색기 - Azure 역할의 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. 선택 hello **설정을** 탭 합니다.

    ![설정 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Hello에 **서비스 구성** 목록, tooupdate 않겠다고 선택 hello 서비스 구성 합니다.

    ![서비스 구성 목록](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. 사용자 지정 설정을 tooadd 선택 **설정 추가**합니다.

    ![사용자 지정 설정 추가](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Hello 새 설정이 toohello 목록 추가, hello 목록의 hello 행 hello 필요한 정보로 업데이트 합니다.

    ![새 사용자 지정 설정](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **이름** -hello 설정의 hello 이름을 입력 합니다.
    - **형식** -선택 **문자열** hello 드롭 다운 목록에서 합니다.
    - **값** -hello hello 설정 값을 입력 합니다. Hello에 직접 hello 값을 입력 하거나 **값** 셀 또는 hello에 줄임표 (...) tooenter hello 값 선택 hello **문자열 편집** 대화 상자.  

1. 사용자 지정 설정 toodelete hello 설정을 선택한 다음 선택 **설정 제거**합니다.

1. Hello Visual Studio에서에서 도구 모음 선택 **저장**합니다.

## <a name="programmatically-access-a-custom-settings-value"></a>프로그래밍 방식으로 사용자 지정 설정 값 액세스
 
hello 다음 단계에서는 tooprogrammatically C#을 사용 하 여 사용자 지정 설정을 액세스 하는 방법

1. Hello 다음 추가 toouse hello 설정을 어디로 지시문 tooa C# 파일을 사용 하 여:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. hello 다음 코드에서는 방법의 예로 사용자 지정 설정 tooaccess 합니다. Hello 대체 &lt;SettingName > 자리 표시자 hello 적절 한 값으로. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>각 역할 인스턴스에 대한 로컬 저장소 관리
각 역할 인스턴스에 대한 로컬 파일 시스템 저장소를 추가할 수 있습니다. hello 데이터 저장소는 액세스할 수 있다는 점에서 hello에 대 한 데이터가 저장 되는 hello 역할의 다른 인스턴스 또는 다른 역할을 저장 합니다.  

1. Visual Studio에서 Azure 클라우드 서비스 프로젝트를 만들거나 엽니다.

1. **솔루션 탐색기**, hello 프로젝트 노드를 확장 합니다. Hello에서 **역할** 노드, 마우스 오른쪽 단추로 클릭 hello 역할 tooupdate, 한, hello 상황에 맞는 메뉴에서 선택 **속성**합니다.

    ![솔루션 탐색기 - Azure 역할의 상황에 맞는 메뉴](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. 선택 hello **로컬 저장소** 탭 합니다.

    ![로컬 저장소 탭](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. Hello에 **서비스 구성** 나열 되어 있는지 확인 합니다. **모든 구성** hello 로컬 저장소 설정이 적용 tooall 서비스 구성을 선택 합니다. 사용할 수 없게 하는 hello 페이지의 모든 hello 입력된 필드에 다른 값이 발생 합니다. 

    ![서비스 구성 목록](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. 로컬 저장소 항목 tooadd 선택 **로컬 저장소 추가**합니다.

    ![로컬 저장소 추가](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Hello 새 로컬 저장소 항목에 toohello 목록 추가 되 면 hello 목록의 hello 행 hello 필요한 정보로 업데이트 합니다.

    ![새 로컬 저장소 항목](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **이름** -hello 새 로컬 저장소에 대 한 toouse 되도록 hello 이름을 입력 합니다.
    - **크기 (MB)** -hello 새 로컬 저장소에 필요한 mb hello 크기를 입력 합니다.
    - **역할 재생에서 정리** -hello 가상 컴퓨터 역할 hello에 대 한 재활용 될 때이 옵션 tooremove hello 데이터 hello 새 로컬 저장소에서 선택 합니다.

1. 로컬 저장소 항목 toodelete hello 항목을 선택한 다음 선택 **로컬 저장소 제거**합니다.

1. Hello Visual Studio에서에서 도구 모음 선택 **저장**합니다.

## <a name="programmatically-accessing-local-storage"></a>프로그래밍 방식으로 로컬 저장소 액세스

이 섹션에서는 tooprogrammatically 로컬 저장소를 사용 하 여 C# 테스트 텍스트 파일을 작성 하 여 액세스 하는 방법을 보여 줍니다. `MyLocalStorageTest.txt`합니다.  

### <a name="write-a-text-file-toolocal-storage"></a>텍스트 파일 toolocal 저장소 쓰기

hello 코드 다음에 어떻게 toowrite는 텍스트 파일 toolocal 저장소의 예가 나와 있습니다. Hello 대체 &lt;LocalStorageName > 자리 표시자 hello 적절 한 값으로. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Toolocal 저장소 기록 파일 찾기

다음이 단계를 수행 하는 hello 코드 hello 이전 섹션에서 만든 tooview hello 파일:
    
1.  Windows 알림 영역 hello hello Azure 아이콘을 마우스 오른쪽 단추로 클릭, hello 상황에 맞는 메뉴에서 선택 **계산 에뮬레이터 UI 표시**합니다. 

    ![Azure 계산 에뮬레이터 표시](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Hello 웹 역할을 선택 합니다.

    ![Azure 계산 에뮬레이터](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. Hello에 **Microsoft Azure 계산 에뮬레이터** 메뉴 선택 **도구** > **로컬 저장소 열기**합니다.

    ![로컬 저장소 메뉴 항목 열기](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Hello Windows 탐색기 창이 열리면 입력 ' MyLocalStorageTest.txt ' hello에 **검색** 텍스트 상자와 선택 **Enter** toostart hello 검색 합니다. 

## <a name="next-steps"></a>다음 단계
[Azure 프로젝트 구성](vs-azure-tools-configuring-an-azure-project.md)을 읽고 Visual Studio에서 Azure 프로젝트에 대해 자세히 알아봅니다. 에 대 한 자세한 hello 클라우드 서비스 스키마를 읽어서 [스키마 참조](https://msdn.microsoft.com/library/azure/dd179398)합니다.

