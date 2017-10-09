<span data-ttu-id="81c90-101">배포 하는 동안 매개 변수 파일 toopass 매개 변수 값을 사용 하는 경우 필요한 toocreate JSON 파일을 다음 예제에서는 형식 비슷한 toohello 사용:</span><span class="sxs-lookup"><span data-stu-id="81c90-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

<span data-ttu-id="81c90-102">hello 매개 변수 파일의 hello 크기는 64KB 보다 큰 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="81c90-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="81c90-103">매개 변수 (예: 암호)에 대 한 tooprovide 중요 한 값을 필요한 경우 해당 값 tooa 주요 자격 증명 모음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c90-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="81c90-104">Hello 이전 예제에 나와 있는 것 처럼 배포 하는 동안 hello 주요 자격 증명 모음을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="81c90-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="81c90-105">자세한 내용은 [배포 중 보안 값 전달](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="81c90-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

