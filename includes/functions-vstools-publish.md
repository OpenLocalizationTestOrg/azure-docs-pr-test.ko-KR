1. **솔루션 탐색기**hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **게시**합니다. **새로 만들기**를 선택한 다음 **게시**를 클릭합니다. 

    ![게시 - 새 함수 앱 만들기](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Visual Studio tooyour Azure 계정이 이미 연결 하지 않은 경우 클릭 **계정 추가...** .  

3. Hello에 **응용 프로그램 서비스 만들기** 대화 상자에서 사용 하 여 hello **호스팅** 표 다음에 지정 된 hello로 설정 합니다. 

    ![Azure 로컬 런타임](./media/functions-vstools-publish/functions-vstools-publish.png)

    | 설정      | 제안 값  | 설명                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **앱 이름** | 전역적으로 고유한 이름 | 새 함수 앱을 고유하게 식별하는 이름입니다. |
    | **구독** | 구독 선택 | hello Azure 구독 toouse 합니다. |
    | **[리소스 그룹](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  어떤 toocreate에 함수 앱을 그룹화 하는 hello 리소스의 이름입니다. |
    | **[App Service 계획](../articles/azure-functions/functions-scale.md)** | 소비 계획 | 있는지 toochoose hello 확인 **소비** 아래 **크기** 새 계획을 만들 때.  |
    | **[Storage 계정](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | 전역적으로 고유한 이름 | 기존 저장소 계정을 사용하거나 새 저장소 계정을 만듭니다.   |

4. 클릭 **만들기** toocreate 이러한 설정 사용 하 여 Azure에서 함수 응용 프로그램입니다. 완료 되 면 hello를 프로 비전 적어 hello **사이트 URL** 값 함수 이러한 앱에서 Azure의 hello 주소입니다. 

    ![Azure 로컬 런타임](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
