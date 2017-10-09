## <a name="clean-up-deployment"></a><span data-ttu-id="ac0e2-101">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ac0e2-101">Clean up deployment</span></span> 

<span data-ttu-id="ac0e2-102">Hello 스크립트 예제를 실행 한 후 사용 되는 tooremove hello 리소스 그룹, Azure Redis Cache 인스턴스와 hello 리소스 그룹에 관련 된 모든 리소스가 hello에 따라 명령 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac0e2-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```