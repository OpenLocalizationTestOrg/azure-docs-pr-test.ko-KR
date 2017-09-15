### <a name="azure-storage-linked-service"></a><span data-ttu-id="c033e-101">Azure Storage 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="c033e-101">Azure Storage Linked Service</span></span>
<span data-ttu-id="c033e-102">**Azure Storage 연결된 서비스**에서 **계정 키**를 사용하여 Azure Storage 계정을 Azure Data Factory에 연결할 수 있으며, 이렇게 하면 데이터 팩터리에 Azure Storage에 대한 전역 액세스가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-102">The **Azure Storage linked service** allows you to link an Azure storage account to an Azure data factory by using the **account key**, which provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="c033e-103">다음 테이블은 Azure Storage 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-103">The following table provides description for JSON elements specific to Azure Storage linked service.</span></span>

| <span data-ttu-id="c033e-104">속성</span><span class="sxs-lookup"><span data-stu-id="c033e-104">Property</span></span> | <span data-ttu-id="c033e-105">설명</span><span class="sxs-lookup"><span data-stu-id="c033e-105">Description</span></span> | <span data-ttu-id="c033e-106">필수</span><span class="sxs-lookup"><span data-stu-id="c033e-106">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c033e-107">type</span><span class="sxs-lookup"><span data-stu-id="c033e-107">type</span></span> |<span data-ttu-id="c033e-108">형식 속성은 **AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="c033e-108">The type property must be set to: **AzureStorage**</span></span> |<span data-ttu-id="c033e-109">예</span><span class="sxs-lookup"><span data-stu-id="c033e-109">Yes</span></span> |
| <span data-ttu-id="c033e-110">connectionString</span><span class="sxs-lookup"><span data-stu-id="c033e-110">connectionString</span></span> |<span data-ttu-id="c033e-111">connectionString 속성에 대한 Azure 저장소에 연결하는 데 필요한 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-111">Specify information needed to connect to Azure storage for the connectionString property.</span></span> |<span data-ttu-id="c033e-112">예</span><span class="sxs-lookup"><span data-stu-id="c033e-112">Yes</span></span> |

<span data-ttu-id="c033e-113">Azure Storage에 대한 계정 키를 보거나 복사하는 단계는 [저장소 액세스 키 보기, 복사 및 다시 생성](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account)문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c033e-113">See the following article for steps to view/copy the account key for an Azure Storage: [View, copy, and regenerate storage access keys](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

<span data-ttu-id="c033e-114">**예제:**</span><span class="sxs-lookup"><span data-stu-id="c033e-114">**Example:**</span></span>  

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

### <a name="azure-storage-sas-linked-service"></a><span data-ttu-id="c033e-115">Azure Storage SAS 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="c033e-115">Azure Storage Sas Linked Service</span></span>
<span data-ttu-id="c033e-116">SAS(공유 액세스 서명)는 저장소 계정의 리소스에 대한 위임된 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-116">A shared access signature (SAS) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="c033e-117">계정 액세스 키를 공유할 필요 없이 지정된 권한 집합을 사용하여 지정된 기간 동안 클라이언트에 저장소 계정의 개체에 대한 제한된 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-117">It allows you to grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span> <span data-ttu-id="c033e-118">SAS는 저장소 리소스에 인증된 액세스를 수행하는 데 필요한 모든 정보가 쿼리 매개 변수에 있는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-118">The SAS is a URI that encompasses in its query parameters all the information necessary for authenticated access to a storage resource.</span></span> <span data-ttu-id="c033e-119">SAS를 사용하여 저장소 리소스에 액세스하려는 클라이언트는 SAS를 적절한 생성자 또는 메서드에 전달하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-119">To access storage resources with the SAS, the client only needs to pass in the SAS to the appropriate constructor or method.</span></span> <span data-ttu-id="c033e-120">SAS에 대한 자세한 내용은 [공유 액세스 서명: SAS 모델 이해](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="c033e-120">For detailed information about SAS, see [Shared Access Signatures: Understanding the SAS Model](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c033e-121">Azure Data Factory는 이제 **서비스 SAS**만 지원하며 계정 SAS는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-121">Azure Data Factory now only supports **Service SAS** but not Account SAS.</span></span> <span data-ttu-id="c033e-122">이러한 두 가지 형식과 생성 방법에 대한 자세한 내용은 [공유 액세스 서명 형식](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c033e-122">See [Types of Shared Access Signatures](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) for details about these two types and how to construct.</span></span> <span data-ttu-id="c033e-123">Azure Portal 또는 Storage 탐색기에서 생성할 수 있는 SAS URL는 지원되지 않는 계정 SAS입니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-123">Note the SAS URL generable from Azure portal or Storage Explorer is an Account SAS, which is not supported.</span></span>
> 

<span data-ttu-id="c033e-124">Azure Storage SAS 연결된 서비스에서 SAS(공유 액세스 서명)을 사용하여 Azure Storage 계정을 Azure Data Factory에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-124">The Azure Storage SAS linked service allows you to link an Azure Storage Account to an Azure data factory by using a Shared Access Signature (SAS).</span></span> <span data-ttu-id="c033e-125">이 서비스는 저장소의 모든/특정 리소스(Blob/컨테이너)에 대해 제한된/시간 제한 액세스를 데이터 팩터리에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-125">It provides the data factory with restricted/time-bound access to all/specific resources (blob/container) in the storage.</span></span> <span data-ttu-id="c033e-126">다음 표는 Azure Storage SAS 연결된 서비스에 특정된 JSON 요소에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-126">The following table provides description for JSON elements specific to Azure Storage SAS linked service.</span></span> 

| <span data-ttu-id="c033e-127">속성</span><span class="sxs-lookup"><span data-stu-id="c033e-127">Property</span></span> | <span data-ttu-id="c033e-128">설명</span><span class="sxs-lookup"><span data-stu-id="c033e-128">Description</span></span> | <span data-ttu-id="c033e-129">필수</span><span class="sxs-lookup"><span data-stu-id="c033e-129">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c033e-130">type</span><span class="sxs-lookup"><span data-stu-id="c033e-130">type</span></span> |<span data-ttu-id="c033e-131">형식 속성은 **AzureStorageSas**</span><span class="sxs-lookup"><span data-stu-id="c033e-131">The type property must be set to: **AzureStorageSas**</span></span> |<span data-ttu-id="c033e-132">예</span><span class="sxs-lookup"><span data-stu-id="c033e-132">Yes</span></span> |
| <span data-ttu-id="c033e-133">sasUri</span><span class="sxs-lookup"><span data-stu-id="c033e-133">sasUri</span></span> |<span data-ttu-id="c033e-134">BLOB, 컨테이너, 테이블 등의 Azure 저장소 리소스에 공유 액세스 서명 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-134">Specify Shared Access Signature URI to the Azure Storage resources such as blob, container, or table.</span></span>  |<span data-ttu-id="c033e-135">예</span><span class="sxs-lookup"><span data-stu-id="c033e-135">Yes</span></span> |

<span data-ttu-id="c033e-136">**예제:**</span><span class="sxs-lookup"><span data-stu-id="c033e-136">**Example:**</span></span>

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of the Azure Storage resource>"   
        }  
    }  
}  
```

<span data-ttu-id="c033e-137">**SAS URI**를 만들 때 다음 사항을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="c033e-137">When creating an **SAS URI**, considering the following:</span></span>  

* <span data-ttu-id="c033e-138">데이터 팩터리에서 연결된 서비스(읽기, 쓰기, 읽기/쓰기)를 사용하는 방식에 따라 개체에 적절한 읽기/쓰기 **권한**을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-138">Set appropriate read/write **permissions** on objects based on how the linked service (read, write, read/write) is used in your data factory.</span></span>
* <span data-ttu-id="c033e-139">**만료 시간**을 적절하게 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-139">Set **Expiry time** appropriately.</span></span> <span data-ttu-id="c033e-140">Azure Storage 개체에 대한 액세스가 파이프라인의 활성 기간 내에 만료되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-140">Make sure that the access to Azure Storage objects does not expire within the active period of the pipeline.</span></span>
* <span data-ttu-id="c033e-141">필요에 따라 올바른 컨테이너/BLOB 또는 테이블 수준에서 URI가 만들어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-141">Uri should be created at the right container/blob or Table level based on the need.</span></span> <span data-ttu-id="c033e-142">Azure BLOB에 대한 SAS URI를 사용하면 Data Factory 서비스에서 특정 BLOB에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-142">A SAS Uri to an Azure blob allows the Data Factory service to access that particular blob.</span></span> <span data-ttu-id="c033e-143">Azure BLOB 컨테이너에 대한 SAS URI를 사용하면 Data Factory 서비스의 해당 컨테이너에서 BLOB을 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-143">A SAS Uri to an Azure blob container allows the Data Factory service to iterate through blobs in that container.</span></span> <span data-ttu-id="c033e-144">나중에 더 많은/더 적은 개체에 대한 액세스를 제공하거나 SAS URI를 업데이트해야 하는 경우 연결된 서비스를 새 URI로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c033e-144">If you need to provide access more/fewer objects later, or update the SAS URI, remember to update the linked service with the new URI.</span></span>   

