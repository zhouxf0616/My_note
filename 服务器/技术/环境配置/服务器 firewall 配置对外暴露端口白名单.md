https://www.jianshu.com/p/169b3164336b

<zone>
  <short>Public</short>
  <description>For use in public areas. You do not trust the other computers on networks to not harm your computer. Only selected incoming connections are accepted.</description>
  <service name="dhcpv6-client"/>
  <service name="ssh"/>
  <port protocol="tcp" port="443"/>
  <port protocol="tcp" port="22"/>
  <port protocol="tcp" port="21"/>
  <port protocol="udp" port="53"/>
  <port protocol="tcp" port="8081"/>
  <port protocol="tcp" port="8080"/>
  <port protocol="tcp" port="80"/>
  <port protocol="tcp" port="9090"/>
  <port protocol="tcp" port="2222"/>
  <port protocol="tcp" port="3306"/>
</zone>

vim /etc/firewalld/zones/public.xml



firewall-cmd --reload