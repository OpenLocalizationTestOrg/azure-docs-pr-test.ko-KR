## <a name="clean-up-deployment"></a><span data-ttu-id="30899-101">배포 정리</span><span class="sxs-lookup"><span data-stu-id="30899-101">Clean up deployment</span></span> 

<span data-ttu-id="30899-102">스크립트 샘플을 실행한 후에는 다음 명령을 사용하여 리소스 그룹, Azure Redis Cache 인스턴스 및 리소스 그룹에서 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30899-102">After the script sample has been run, the follow command can be used to remove the resource group, Azure Redis Cache instance, and any related resources in the resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```