### <a name="azure-storage-linked-service"></a><span data-ttu-id="363d2-101">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="363d2-101">Azure Storage Linked Service</span></span>
<span data-ttu-id="363d2-102">hello **Azure 저장소 연결 된 서비스** hello를 사용 하 여 Azure 저장소 계정 tooan Azure 데이터 팩터리에 toolink 사용 하면 **계정 키**, 전역 액세스 toohello Azure와 hello 데이터 팩터리를 제공 하는 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-102">hello **Azure Storage linked service** allows you toolink an Azure storage account tooan Azure data factory by using hello **account key**, which provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="363d2-103">다음 표에서 hello JSON 요소 특정 tooAzure 저장소 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-103">hello following table provides description for JSON elements specific tooAzure Storage linked service.</span></span>

| <span data-ttu-id="363d2-104">속성</span><span class="sxs-lookup"><span data-stu-id="363d2-104">Property</span></span> | <span data-ttu-id="363d2-105">설명</span><span class="sxs-lookup"><span data-stu-id="363d2-105">Description</span></span> | <span data-ttu-id="363d2-106">필수</span><span class="sxs-lookup"><span data-stu-id="363d2-106">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="363d2-107">type</span><span class="sxs-lookup"><span data-stu-id="363d2-107">type</span></span> |<span data-ttu-id="363d2-108">hello type 속성 설정 해야 합니다: **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="363d2-108">hello type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="363d2-109">예</span><span class="sxs-lookup"><span data-stu-id="363d2-109">Yes</span></span> |
| <span data-ttu-id="363d2-110">connectionString</span><span class="sxs-lookup"><span data-stu-id="363d2-110">connectionString</span></span> |<span data-ttu-id="363d2-111">Hello connectionString 속성에 대 한 tooconnect tooAzure 저장소는 데 필요한 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-111">Specify information needed tooconnect tooAzure storage for hello connectionString property.</span></span> |<span data-ttu-id="363d2-112">예</span><span class="sxs-lookup"><span data-stu-id="363d2-112">Yes</span></span> |

<span data-ttu-id="363d2-113">Hello Azure 저장소에 대 한 다음 단계 tooview/복사 hello 계정 키에 대 한 문서를 참조 하십시오: [보기, 복사 및 액세스 키 다시 생성 저장소](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-113">See hello following article for steps tooview/copy hello account key for an Azure Storage: [View, copy, and regenerate storage access keys](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

<span data-ttu-id="363d2-114">**예제:**</span><span class="sxs-lookup"><span data-stu-id="363d2-114">**Example:**</span></span>  

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

### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="363d2-115">Azure Storage SAS 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="363d2-115">Azure Storage Sas Linked Service</span></span>
<span data-ttu-id="363d2-116">공유 액세스 서명 (SAS) 저장소 계정에 tooresources 위임 된 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-116">A shared access signature (SAS) provides delegated access tooresources in your storage account.</span></span> <span data-ttu-id="363d2-117">클라이언트 toogrant tooshare 계정 액세스 키 필요 없이 저장소 계정에 사용 권한을 tooobjects 시간 및 지정한 사용 권한 집합이 지정된 된 기간에 대 한 제한 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-117">It allows you toogrant a client limited permissions tooobjects in your storage account for a specified period of time and with a specified set of permissions, without having tooshare your account access keys.</span></span> <span data-ttu-id="363d2-118">hello SAS 쿼리 매개 변수에서 인증 된 액세스 tooa 저장소 리소스에 대해 필요한 모든 hello 정보를 포함 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-118">hello SAS is a URI that encompasses in its query parameters all hello information necessary for authenticated access tooa storage resource.</span></span> <span data-ttu-id="363d2-119">tooaccess hello SAS로 저장소 리소스를 hello 클라이언트 hello SAS toohello 적절 한 생성자 또는 메서드에 toopass를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-119">tooaccess storage resources with hello SAS, hello client only needs toopass in hello SAS toohello appropriate constructor or method.</span></span> <span data-ttu-id="363d2-120">SAS에 대 한 자세한 내용은 참조 [공유 액세스 서명: SAS 모델 이해 hello](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="363d2-120">For detailed information about SAS, see [Shared Access Signatures: Understanding hello SAS Model](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="363d2-121">Azure Data Factory는 이제 **서비스 SAS**만 지원하며 계정 SAS는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-121">Azure Data Factory now only supports **Service SAS** but not Account SAS.</span></span> <span data-ttu-id="363d2-122">참조 [종류의 공유 액세스 서명](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) 이 두 종류에 대 한 세부 정보에 대 한 방법과 tooconstruct 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-122">See [Types of Shared Access Signatures](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) for details about these two types and how tooconstruct.</span></span> <span data-ttu-id="363d2-123">Azure 포털에서 generable SAS URL 또는 저장소 탐색기 참고 hello는 지원 되지 않는 한 계정 SAS입니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-123">Note hello SAS URL generable from Azure portal or Storage Explorer is an Account SAS, which is not supported.</span></span>
> 

<span data-ttu-id="363d2-124">hello Azure 저장소 SAS 연결 된 서비스는 공유 액세스 서명 (SAS)를 사용 하 여 Azure 저장소 계정 tooan Azure 데이터 팩터리에 toolink를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-124">hello Azure Storage SAS linked service allows you toolink an Azure Storage Account tooan Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="363d2-125">Hello 저장소의 tooall/관련 리소스 (blob/컨테이너) hello 데이터 팩터리 시간 제한/범위 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-125">It provides hello data factory with restricted/time-bound access tooall/specific resources (blob/container) in hello storage.</span></span> <span data-ttu-id="363d2-126">다음 표에서 hello JSON 요소 특정 tooAzure 저장소 SAS 연결 된 서비스에 대 한 설명을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-126">hello following table provides description for JSON elements specific tooAzure Storage SAS linked service.</span></span> 

| <span data-ttu-id="363d2-127">속성</span><span class="sxs-lookup"><span data-stu-id="363d2-127">Property</span></span> | <span data-ttu-id="363d2-128">설명</span><span class="sxs-lookup"><span data-stu-id="363d2-128">Description</span></span> | <span data-ttu-id="363d2-129">필수</span><span class="sxs-lookup"><span data-stu-id="363d2-129">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="363d2-130">type</span><span class="sxs-lookup"><span data-stu-id="363d2-130">type</span></span> |<span data-ttu-id="363d2-131">hello type 속성 설정 해야 합니다: **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="363d2-131">hello type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="363d2-132">예</span><span class="sxs-lookup"><span data-stu-id="363d2-132">Yes</span></span> |
| <span data-ttu-id="363d2-133">sasUri</span><span class="sxs-lookup"><span data-stu-id="363d2-133">sasUri</span></span> |<span data-ttu-id="363d2-134">Blob, 컨테이너, 테이블 등 공유 액세스 서명 URI toohello Azure 저장소 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-134">Specify Shared Access Signature URI toohello Azure Storage resources such as blob, container, or table.</span></span>  |<span data-ttu-id="363d2-135">예</span><span class="sxs-lookup"><span data-stu-id="363d2-135">Yes</span></span> |

<span data-ttu-id="363d2-136">**예제:**</span><span class="sxs-lookup"><span data-stu-id="363d2-136">**Example:**</span></span>

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

<span data-ttu-id="363d2-137">만들 때는 **SAS URI**, hello 다음을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-137">When creating an **SAS URI**, considering hello following:</span></span>  

* <span data-ttu-id="363d2-138">적절 한 읽기/쓰기를 설정 **권한을** 기반으로 하는 개체에 hello (읽기, 쓰기, 읽기/쓰기) 서비스를 연결 하는 방법을 data factory에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-138">Set appropriate read/write **permissions** on objects based on how hello linked service (read, write, read/write) is used in your data factory.</span></span>
* <span data-ttu-id="363d2-139">**만료 시간**을 적절하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-139">Set **Expiry time** appropriately.</span></span> <span data-ttu-id="363d2-140">Hello hello 파이프라인의 활성 기간 내에서 저장소 개체에 hello 액세스 tooAzure 만료 되지 않는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-140">Make sure that hello access tooAzure Storage objects does not expire within hello active period of hello pipeline.</span></span>
* <span data-ttu-id="363d2-141">Uri hello 오른쪽 컨테이너/blob에 만들지 아니면 hello에 따라 테이블 수준에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-141">Uri should be created at hello right container/blob or Table level based on hello need.</span></span> <span data-ttu-id="363d2-142">SAS Uri tooan Azure blob hello Data Factory 서비스 tooaccess 해당 특정 blob를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-142">A SAS Uri tooan Azure blob allows hello Data Factory service tooaccess that particular blob.</span></span> <span data-ttu-id="363d2-143">SAS Uri tooan Azure blob 컨테이너에는 해당 컨테이너의에서 blob 통해 데이터 팩터리 서비스 tooiterate를 hello 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-143">A SAS Uri tooan Azure blob container allows hello Data Factory service tooiterate through blobs in that container.</span></span> <span data-ttu-id="363d2-144">Tooprovide 액세스를 더 이상 필요/적은 나중에 개체 또는 업데이트 hello SAS URI를 tooupdate hello 연결 된 서비스를 기억 하는 경우 새 URI를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="363d2-144">If you need tooprovide access more/fewer objects later, or update hello SAS URI, remember tooupdate hello linked service with hello new URI.</span></span>   

