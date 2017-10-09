
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Toohello 로그인 [Azure 포털](https://portal.azure.com/) http://portal.azure.com/에 있습니다.
2. Hello 왼쪽된 배너에서 클릭 **모두 찾아보기**합니다. hello **찾아보기** 블레이드가 표시 됩니다.
3. 스크롤하여 **SQL Server**를 클릭합니다. hello **SQL server** 블레이드가 표시 됩니다.
   
    ![Hello 포털에서 Azure SQL 데이터베이스 서버를 찾아][b21-FindServerInPortal]
4. 편의 위해 hello 클릭 hello 이전 버전에서 컨트롤을 최소화 **찾아보기** 블레이드입니다.
5. Hello 필터 텍스트 상자에 서버 이름을 hello 입력을 시작 합니다. 해당 행이 표시됩니다.
6. 서버에 대 한 hello 행을 클릭 합니다. 서버 블레이드가 표시됩니다.
7. 서버 블레이드에서 **설정**을 클릭합니다. hello **설정을** 블레이드가 표시 됩니다.
8. **방화벽**을 클릭합니다. hello **방화벽 설정을** 블레이드가 표시 됩니다.
   
    ![설정 > 방화벽을 클릭합니다.][b31-SettingsFirewallNavig]
9. **클라이언트 IP 추가**를 클릭합니다. Hello 첫 번째 텍스트 상자에 새 규칙에 대 한 이름을 입력 합니다.
10. 낮은 임계값과 높은 hello 입력 IP 주소 원하는 hello 범위에 대 한 값 tooenable 합니다.
    
    * 것이 편리한 toohave hello 낮은 값 끝나야 **.0** 및 안전한 것으로 hello **.255**합니다.
    
    ![IP 주소 범위 tooallow 추가][b41-AddRange]
11. **Save**를 클릭합니다.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
