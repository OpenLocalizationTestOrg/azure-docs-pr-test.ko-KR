### <a name="troubleshoot-azure-diagnostics"></a>Azure Diagnostics 문제 해결

Hello 다음과 같은 오류 메시지가 표시 되 면 hello Microsoft.insights 리소스 공급자가 등록 되지 않았습니다.

`Failed tooupdate diagnostics for 'resource'. {"code":"Forbidden","message":"Please register hello subscription 'subscription id' with Microsoft.Insights."}`

tooregister hello 리소스 공급자 hello hello Azure 포털의에서 단계를 수행 합니다.

1.  Hello hello 왼쪽의 탐색 창에서 클릭 *구독*
2.  Hello 오류 메시지에서 확인 하는 hello 구독 선택
3.  *리소스 공급자* 클릭
4.  Hello *Microsoft.insights* 공급자
5.  Hello 클릭 *등록* 링크

![Microsoft.insights 리소스 공급자 등록](./media/log-analytics-troubleshoot-azure-diagnostics/log-analytics-register-microsoft-diagnostics-resource-provider.png)

한 번 hello *Microsoft.insights* 리소스 공급자가 등록 진단 구성 프로그램을 다시 시도 하세요.


PowerShell을 hello 다음과 같은 오류 메시지가 표시 되 면 PowerShell 버전에서 tooupdate 필요 합니다.

`Set-AzureRmDiagnosticSetting : A parameter cannot be found that matches parameter name 'WorkspaceId'.`

2016 년 11 월 (v2.3.0) PowerShell toohello의 버전을 업데이트 또는 hello 지침을 사용 하 여 hello에를 릴리스 이상에서는 [Azure PowerShell cmdlet과 함께 시작](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 문서.
