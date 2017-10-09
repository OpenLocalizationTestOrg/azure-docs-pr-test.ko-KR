### <a name="app-service-plan"></a><span data-ttu-id="2ce27-101">앱 서비스 계획</span><span class="sxs-lookup"><span data-stu-id="2ce27-101">App Service plan</span></span>
<span data-ttu-id="2ce27-102">Hello 웹 응용 프로그램을 호스팅하기 위한 hello 서비스 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ce27-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="2ce27-103">Hello 통해 hello 계획의 hello 이름을 제공 하면 **hostingPlanName** 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="2ce27-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="2ce27-104">hello 계획의 hello 위치는 hello hello 리소스 그룹에 사용 된 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="2ce27-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="2ce27-105">hello 가격 책정 계층 및 작업자 크기 hello에 지정 된 **sku** 및 **workerSize** 매개 변수</span><span class="sxs-lookup"><span data-stu-id="2ce27-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

