### <a name="app-service-plan"></a>앱 서비스 계획
Hello 웹 응용 프로그램을 호스팅하기 위한 hello 서비스 계획을 만듭니다. Hello 통해 hello 계획의 hello 이름을 제공 하면 **hostingPlanName** 매개 변수입니다. hello 계획의 hello 위치는 hello hello 리소스 그룹에 사용 된 동일한 위치입니다. hello 가격 책정 계층 및 작업자 크기 hello에 지정 된 **sku** 및 **workerSize** 매개 변수

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

