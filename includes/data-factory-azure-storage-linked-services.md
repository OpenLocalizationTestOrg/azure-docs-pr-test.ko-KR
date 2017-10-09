### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스
hello **Azure 저장소 연결 된 서비스** hello를 사용 하 여 Azure 저장소 계정 tooan Azure 데이터 팩터리에 toolink 사용 하면 **계정 키**, 전역 액세스 toohello Azure와 hello 데이터 팩터리를 제공 하는 저장소입니다. 다음 표에서 hello JSON 요소 특정 tooAzure 저장소 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type |hello type 속성 설정 해야 합니다: **AzureStorage** |예 |
| connectionString |Hello connectionString 속성에 대 한 tooconnect tooAzure 저장소는 데 필요한 정보를 지정 합니다. |예 |

Hello Azure 저장소에 대 한 다음 단계 tooview/복사 hello 계정 키에 대 한 문서를 참조 하십시오: [보기, 복사 및 액세스 키 다시 생성 저장소](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.

**예제:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Azure Storage SAS 연결된 서비스
공유 액세스 서명 (SAS) 저장소 계정에 tooresources 위임 된 액세스를 제공합니다. 클라이언트 toogrant tooshare 계정 액세스 키 필요 없이 저장소 계정에 사용 권한을 tooobjects 시간 및 지정한 사용 권한 집합이 지정된 된 기간에 대 한 제한 수 있습니다. hello SAS 쿼리 매개 변수에서 인증 된 액세스 tooa 저장소 리소스에 대해 필요한 모든 hello 정보를 포함 하는 URI입니다. tooaccess hello SAS로 저장소 리소스를 hello 클라이언트 hello SAS toohello 적절 한 생성자 또는 메서드에 toopass를 해야합니다. SAS에 대 한 자세한 내용은 참조 [공유 액세스 서명: SAS 모델 이해 hello](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Azure Data Factory는 이제 **서비스 SAS**만 지원하며 계정 SAS는 지원하지 않습니다. 참조 [종류의 공유 액세스 서명](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) 이 두 종류에 대 한 세부 정보에 대 한 방법과 tooconstruct 합니다. Azure 포털에서 generable SAS URL 또는 저장소 탐색기 참고 hello는 지원 되지 않는 한 계정 SAS입니다.
> 

hello Azure 저장소 SAS 연결 된 서비스는 공유 액세스 서명 (SAS)를 사용 하 여 Azure 저장소 계정 tooan Azure 데이터 팩터리에 toolink를 허용 합니다. Hello 저장소의 tooall/관련 리소스 (blob/컨테이너) hello 데이터 팩터리 시간 제한/범위 액세스를 제공합니다. 다음 표에서 hello JSON 요소 특정 tooAzure 저장소 SAS 연결 된 서비스에 대 한 설명을 제공 합니다. 

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type |hello type 속성 설정 해야 합니다: **AzureStorageSas** |예 |
| sasUri |Blob, 컨테이너, 테이블 등 공유 액세스 서명 URI toohello Azure 저장소 리소스를 지정 합니다.  |예 |

**예제:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

만들 때는 **SAS URI**, hello 다음을 고려 합니다.  

* 적절 한 읽기/쓰기를 설정 **권한을** 기반으로 하는 개체에 hello (읽기, 쓰기, 읽기/쓰기) 서비스를 연결 하는 방법을 data factory에 사용 됩니다.
* **만료 시간**을 적절하게 설정합니다. Hello hello 파이프라인의 활성 기간 내에서 저장소 개체에 hello 액세스 tooAzure 만료 되지 않는 있는지 확인 합니다.
* Uri hello 오른쪽 컨테이너/blob에 만들지 아니면 hello에 따라 테이블 수준에서 필요 합니다. SAS Uri tooan Azure blob hello Data Factory 서비스 tooaccess 해당 특정 blob를 수 있습니다. SAS Uri tooan Azure blob 컨테이너에는 해당 컨테이너의에서 blob 통해 데이터 팩터리 서비스 tooiterate를 hello 수 있습니다. Tooprovide 액세스를 더 이상 필요/적은 나중에 개체 또는 업데이트 hello SAS URI를 tooupdate hello 연결 된 서비스를 기억 하는 경우 새 URI를 hello 합니다.   

