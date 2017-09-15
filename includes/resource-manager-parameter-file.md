<span data-ttu-id="1a0fd-101">배포 중에 매개 변수 값을 전달하는 데 매개 변수 파일을 사용하려면 다음 예와 유사한 형식의 JSON 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a0fd-101">If you use a parameter file to pass parameter values during deployment, you need to create a JSON file with a format similar to the following example:</span></span>

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

<span data-ttu-id="1a0fd-102">매개 변수 파일 크기는 64KB보다 클 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1a0fd-102">The size of the parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="1a0fd-103">매개 변수에 대해 중요한 값(예: 암호)을 제공해야 할 경우 해당 값을 주요 자격 증명 모음에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1a0fd-103">If you need to provide a sensitive value for a parameter (such as a password), add that value to a key vault.</span></span> <span data-ttu-id="1a0fd-104">앞의 예제에 표시된 대로 배포하는 동안 주요 자격 증명 모음을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1a0fd-104">Retrieve the key vault during deployment as shown in the previous example.</span></span> <span data-ttu-id="1a0fd-105">자세한 내용은 [배포 중 보안 값 전달](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1a0fd-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

