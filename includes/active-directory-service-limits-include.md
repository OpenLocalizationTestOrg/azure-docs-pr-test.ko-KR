다음은 hello 사용 제약 조건 및 hello Azure Active Directory 서비스에 대 한 기타 서비스 제한입니다.

| Category | 제한 |
| --- | --- |
| 디렉터리 |사용자 한 명만 최대 20개의 Azure Active Directory 디렉터리에 연결될 수 있습니다.<br />가능한 조합의 예: <ul> <li>사용자 한 명이 20개의 디렉터리를 만드는 경우</li><li>한 명의 사용자를 멤버로 too20 디렉터리 추가 됩니다.</li><li>단일 사용자 10 디렉터리를 만들고 나중에 다른 사용자가 추가 too10 다른 디렉터리입니다.</li></ul> |
| 개체 |<ul><li>최대 500, 000 개체 hello Azure Active Directory의 무료 버전의 사용자가 단일 디렉터리에 사용할 수 있습니다.</li><li>관리자가 아닌 사용자는 250개 이하의 개체를 만들 수 있습니다.</li></ul> |
| 스키마 확장 |<ul><li>문자열 형식 확장은 최대 256자까지 가능합니다. </li><li>이진 형식 확장은 제한 된 too256 바이트입니다.</li><li>(모든 형식 및 모든 응용 프로그램)에서 확장 값을 100 tooany 단일 개체를 작성할 수 있습니다.</li><li>“User”, “Group”, “TenantDetail”, “Device”, “Application” 및 “ServicePrincipal” 엔터티만 “String” 형식 또는 “Binary” 형식의 단일 값 특성으로 확장할 수 있습니다.</li><li>스키마 확장은 Graph API 버전 1.21 미리 보기에서만 사용할 수 있습니다. hello 응용 프로그램에는 쓰기 권한을 부여한 tooregister 확장 해야 합니다.</li></ul> |
| 응용 프로그램 |최대 100명의 사용자가 단일 응용 프로그램의 소유자가 될 수 있습니다. |
| 그룹 |<ul><li>최대 100명의 사용자가 단일 그룹의 소유자가 될 수 있습니다.</li><li>Azure Active Directory에서 단일 그룹의 멤버가 될 수 있는 개체의 수는 제한이 없습니다.</li><li>온-프레미스 Active Directory tooAzure Active Directory에서에서 동기화 할 수 있습니다는 그룹의에서 구성원에 hello 수는 Azure Active Directory 디렉터리 동기화 (DirSync)를 사용 하 여 제한 된 too15K 멤버입니다.</li><li>온-프레미스 Active Directory tooAzure Active Directory에서에서 동기화 할 수 있습니다는 그룹의 멤버 수가 hello 제한 too50K 구성원은 Azure AD Connect를 사용 하 여 합니다.</li></ul> |
| 액세스 패널 |<ul><li>Azure AD Premium 또는 Enterprise Mobility Suite hello에 대 한 라이선스를 할당 된 사용자에 대 한 최종 사용자 당 액세스 패널 hello에서 볼 수 있는 응용 프로그램의 제한 toohello 수 없음입니다.</li><li>최대 10 개의 앱 타일의 (예: 상자나 Salesforce, Dropbox) 무료 라이선스를 할당 된 사용자 또는 Azure AD Basic 버전의 Azure Active Directory에 대 한 각 최종 사용자에 대 한 hello 액세스 패널에서에서 볼 수 있습니다. 이 제한은 tooAdministrator 계정을 적용 되지 않습니다.</li></ul> |
| 보고서 | 최대 1,000행을 표시하거나 보고서에 다운로드할 수 있습니다. 그 외의 데이터는 잘립니다. |
| 관리 단위 | 개체는 30개 이하 관리 단위의 멤버일 수 있습니다. |
