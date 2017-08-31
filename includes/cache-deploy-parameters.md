
### <a name="cacheskuname"></a>cacheSKUName
새 Azure Redis Cache의 가격 책정 계층입니다.

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "The pricing tier of the new Azure Redis Cache."
      }
    },

이 매개 변수에 허용되는 값(Basic 또는 Standard)을 정의하고, 값이 지정되지 않은 경우에는 기본값(Basic)을 할당하는 템플릿입니다. Basic은 최대 53GB를 사용할 수 있는 다양한 크기의 단일 노드를 제공합니다.
Standard는 최대 53GB를 사용할 수 있으며 99.9%의 SLA를 제공하는 다양한 크기의 2-노드 주/복제본을 제공합니다.

### <a name="cacheskufamily"></a>cacheSKUFamily
SKU 제품군입니다.

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "The family for the sku."
      }
    },


### <a name="cacheskucapacity"></a>cacheSKUCapacity
새 Azure Redis Cache 인스턴스의 크기입니다. 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "The size of the new Azure Redis Cache instance. "
      }
    }


이 매개 변수에 허용되는 값(0, 1, 2, 3, 4, 5 또는 6)을 정의하고, 값이 지정되지 않은 경우에는 기본값(1)을 할당하는 템플릿입니다. 이러한 숫자는 다음 캐시 크기에 해당합니다. 0 = 250MB, 1 = 1GB, 2 = 2.5GB, 3 = 6GB, 4 = 13GB, 5 = 26GB, 6 = 53GB

