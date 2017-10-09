### <a name="prerequisites"></a>필수 조건
* Azure 계정의 경우 [무료 계정](https://azure.microsoft.com/free)
* [Azure Blob 저장소 계정](../articles/storage/common/storage-create-storage-account.md) hello 저장소 계정 이름 및 해당 액세스 키를 포함 합니다. 이 정보는 hello Azure 포털에서에서 저장소 계정 hello의 hello 속성에 나열 됩니다. [Azure Storage](../articles/storage/common/storage-introduction.md)에 대해 자세히 읽어봅니다.

Azure Blob 저장소 계정에서 논리 앱을 사용 하기 전에 tooyour Azure Blob 저장소 계정을 연결 하세요. Hello Azure 포털에서 논리 앱 내에서이 작업을 쉽게 수행할 수 있습니다.  

단계를 수행 하는 hello를 사용 하 여 tooyour Azure Blob 저장소 계정을 연결 합니다.  

1. 논리 앱을 만듭니다. Hello 논리 앱 디자이너에서 트리거를 추가 하 고 작업을 추가 합니다. 선택 **표시 Microsoft 관리 되는 Api** hello에 드롭다운 목록에서 선택한 다음 hello 검색 상자에 "blob"를 입력 합니다. Hello 작업 중 하나를 선택 합니다.  
   
    ![Azure Blob 저장소 연결 만들기 단계](./media/connectors-create-api-azureblobstorage/azureblobstorage-1.png)  
2. TooAzure 저장소 어떤 연결을 만들어 이전에 없는 경우 hello 연결 세부 정보에 대 한 표시 됩니다.   
   
    ![Azure Blob 저장소 연결 만들기 단계](./media/connectors-create-api-azureblobstorage/connection-details.png)  
3. Hello 저장소 계정 세부 정보를 입력 합니다. 별표가 있는 속성은 필수 사항입니다.
   
   | 속성 | 세부 정보 |
   | --- | --- |
   | 연결 이름 * |연결의 이름을 입력합니다. |
   | Azure 저장소 계정 이름 * |Hello 저장소 계정 이름을 입력 합니다. 저장소 계정 이름은 hello hello Azure 포털에서에서 hello 저장소 속성에 표시 됩니다. |
   | Azure 저장소 계정 액세스 키 * |Hello 저장소 계정 키를 입력 합니다. hello 선택 키 hello Azure 포털에서에서 hello 저장소 속성에 표시 됩니다. |
   
    이러한 자격 증명 사용 되는 tooauthorize 여 논리 앱 tooconnect 되며 데이터에 액세스. 
4. **만들기**를 선택합니다.
5. 공지 hello 연결이 만들어졌습니다. 이제 진행할 논리 앱의 단계를 다른 hello: 
   
    ![Azure Blob 저장소 연결 만들기 단계](./media/connectors-create-api-azureblobstorage/azureblobstorage-3.png)  

