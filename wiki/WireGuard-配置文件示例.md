## Surge
  * 详细说明: https://manual.nssurge.com/policy/wireguard.html
  * `test-url`: WARP节点检测请使用`http://1.1.1.1/generate_204`
  * `private-key`: 客户端私钥，由Wireguard客户端生成（注：与下面的`节点公钥`不是同一对儿！）
  * `self-ip`: 客户端 IPv4 地址，隧道内使用 IPv4，默认值: 172.16.0.2
  * `self-ip-v6`: 客户端 IPv6 地址，隧道内使用 IPv6
    * 此配置需要`iOS 5.20.0 (2452)` 或 `macOS Version 4.8.1-1809` 及以上版本
    * x为配置下发的唯一ipv6地址，此地址与`客户端密钥`对应，随意填写则隧道内IPv6不可用！
  * `mtu`: 最大传输单元，默认值1280
    * ~~如需为隧道启用IPv6，此值应设为1400 （[来源](https://community.nssurge.com/d/1198-wireguard-ipv6warp-ipv6/2)）~~
    * 如您确认配置正确，但测试显示IPv4联通，IPv6不通，可尝试设置mtu为`1280`, `1380`, `1390`, `1400`, `1420`
    * 国内设置区间为`1280`-`1480`，在此区间，数值越大，性能越好
  * `peer`: 节点
    * `public-key`: 节点公钥，`Cloudflare WARP`的公钥始终为`bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=`
    * `allowed-ips`: 允许使用的IP或IP段, IPv4默认为`0.0.0.0/0`, IPv6默认为`::/0`
      * `allowed-ips`配置IPv6地址需要`iOS 5.20.0 (2452)` 或 `macOS Version 4.8.1-1809` 及以上版本
    * `endpoint`: 端点，即所要链接的服务器地址
      * ~~目前Surge仅支持单节点(peer)，所以需要选择一个可用IP，详见[可用IP](#可用IP)~~
      * 可以直接使用`engage.nanocat.me:2408`，此地址已配置解析为所有可用IP
      * 标准端口为`2408`，fallback端口为`500`, `1701`, `4500`
      * `162.159.195.0/24`与`2606:4700:d1::/48`除标准端口`2408`外，有额外端口`908`可用
```
[Proxy]
☁WARP = wireguard, section-name = Cloudflare, test-url=http://1.1.1.1/generate_204

[Group]
你的策略组 = 节点1, 节点2, 节点3, WARP

[WireGuard Cloudflare]
private-key = 客户端私钥
self-ip = 172.16.0.2
self-ip-v6 = 2606:4700:110:xxxx:xxxx:xxxx:xxxx:xxxx
dns-server = 162.159.36.1, 2606:4700:4700::1111
mtu = 1280
peer = (public-key = bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=, allowed-ips = "0.0.0.0/0, ::/0", endpoint = engage.nanocat.me:2408, keepalive = 45)
```
