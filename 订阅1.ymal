mixed-port: 10801
redir-port: 7892
tproxy-port: 7893
allow-lan: true
bind-address: "*"
find-process-mode: strict
mode: rule
geox-url:
  geoip: "https://fastly.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geoip.dat"
  geosite: "https://fastly.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geosite.dat"
  mmdb: "https://fastly.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@release/geoip.metadb"
log-level: debug
ipv6: true
external-controller: 0.0.0.0:9093
secret: "9cmclFnWq8tAmohE"
tcp-concurrent: true
interface-name: en0
global-client-fingerprint: chrome
profile:
  store-selected: false
  store-fake-ip: true
tun:
  enable: true
  stack: system
  dns-hijack:
    - 0.0.0.0:53
  auto-detect-interface: true
  auto-route: false
  mtu: 9000
  strict-route: true
ebpf:
  auto-redir:
    - eth0
  redirect-to-tun:
    - eth0
sniffer:
  enable: true
  override-destination: false
  sniff:
    TLS:
      ports: [443, 8443]
    HTTP:
      ports: [80, 8080-8880]
      override-destination: true
  force-domain:
    - +.v2ex.com
tunnels:
  - tcp/udp,127.0.0.1:6553,114.114.114.114:53,Proxy
  - network: [tcp, udp]
    address: 127.0.0.1:7777
    target: target.com
    proxy: Proxy
dns:
  enable: true
  prefer-h3: true
  listen: 0.0.0.0:53
  ipv6: true
  ipv6-timeout: 300
  default-nameserver:
    - 114.114.114.114
    - 8.8.8.8
    - tls://1.12.12.12:853
    - tls://223.5.5.5:853
    - system
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  nameserver:
    - https://dns.alidns.com/dns-query
    - https://223.5.5.5/dns-query
    - https://doh.pub/dns-query
    - https://dns.alidns.com/dns-query#h3=true
    - quic://dns.adguard.com:784
  fallback:
    - tls://dns.google
    - https://1.1.1.1/dns-query
    - https://cloudflare-dns.com/dns-query
    - https://dns.google/dns-query
  fallback-filter:
    geoip: true
    geoip-code: CN
    geosite:
      - gfw
    ipcidr:
      - 240.0.0.0/4
    domain:
      - '+.google.com'
      - '+.facebook.com'
      - '+.youtube.com'
  nameserver-policy:
    "geosite:cn,private,apple":
      - https://doh.pub/dns-query
      - https://dns.alidns.com/dns-query
    "geosite:category-ads-all": rcode://success
    "www.baidu.com,+.google.cn": [223.5.5.5, https://dns.alidns.com/dns-query]
proxies:
  - name: vmess-ws-tls-kvm
    type: vmess
    server: 104.16.132.167
    port: 443
    uuid: cf5e36a8-c38f-4172-b8f1-b6ea78079145
    alterId: 0
    cipher: auto
    network: ws
    tls: true
    skip-cert-verify: false
    servername: kaol.styleed.top
    ws-opts:
      path: "/3I4ioyfB"
      headers: 
         host: kaol.styleed.top
      max-early-data: 2048
      early-data-header-name: Sec-WebSocket-Protocol
  - name: tuic-kvm
    server: kaol.styleed.top
    port: 25678
    type: tuic
    uuid: 684518e9-1cf9-4078-933f-cdb6f15462c2
    password: HRMo4L6cjUy3
    alpn: [h3]
    request-timeout: 8000
    udp-relay-mode: native
    congestion-controller: bbr
  - name: vless-reality-vision-kvm
    type: vless
    server: kaol.styleed.top
    port: 25677
    uuid: 6363b5d0-6f9f-4d70-af2a-042b1dbdb85d
    network: tcp
    udp: true
    tls: true
    flow: xtls-rprx-vision
    servername: kaol.styleed.top
    reality-opts:
      public-key: PC9x19rYplL_hc-37tTwx4P0GSSWXyvN5rEVIdNRU3Q
      short-id: 2c6772cbbe44b974
  - name: shadowtls-kvm
    type: ss
    server: kaol.styleed.top
    port: 25679
    cipher: 2022-blake3-chacha20-poly1305
    password: "s9qvvh2up/CFvzPzD5qxPrl0m+9qa4XcovauFRyPvHo="
    plugin: shadow-tls
    plugin-opts:
      host: "kaol.styleed.top"
      password: "bpoT+3ZPNRxSrONwCu5xq0n9jUL3C3qIlJxD9YkWpv8="
      version: 3
proxy-groups:
  - name: Proxy
    type: select
    proxies:
      - vmess-ws-tls-kvm
      - tuic-kvm
      - vless-reality-vision-kvm
      - shadowtls-kvm
      - auto
  - name: auto
    type: url-test
    proxies:
      - vmess-ws-tls-kvm
      - tuic-kvm
      - vless-reality-vision-kvm
      - shadowtls-kvm
    url: "https://cp.cloudflare.com/generate_204"
    interval: 300
rule-providers:
  reject:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/reject.txt"
    path: ./ruleset/reject.yaml
    interval: 86400
  icloud:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/icloud.txt"
    path: ./ruleset/icloud.yaml
    interval: 86400
  apple:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/apple.txt"
    path: ./ruleset/apple.yaml
    interval: 86400
  direct:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/direct.txt"
    path: ./ruleset/direct.yaml
    interval: 86400
  private:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/private.txt"
    path: ./ruleset/private.yaml
    interval: 86400
  gfw:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/gfw.txt"
    path: ./ruleset/gfw.yaml
    interval: 86400
  tld-not-cn:
    type: http
    behavior: domain
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/tld-not-cn.txt"
    path: ./ruleset/tld-not-cn.yaml
    interval: 86400
  cncidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/cncidr.txt"
    path: ./ruleset/cncidr.yaml
    interval: 86400
  lancidr:
    type: http
    behavior: ipcidr
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/lancidr.txt"
    path: ./ruleset/lancidr.yaml
    interval: 86400
  applications:
    type: http
    behavior: classical
    url: "https://cdn.jsdelivr.net/gh/Loyalsoldier/clash-rules@release/applications.txt"
    path: ./ruleset/applications.yaml
    interval: 86400
rules:
  - RULE-SET,applications,DIRECT
  - DOMAIN,clash.razord.top,DIRECT
  - DOMAIN,yacd.haishan.me,DIRECT
  - DOMAIN-SUFFIX,services.googleapis.cn,DIRECT
  - DOMAIN-SUFFIX,xn--ngstr-lra8j.com,DIRECT
  - RULE-SET,private,DIRECT
  - RULE-SET,reject,REJECT
  - RULE-SET,icloud,DIRECT
  - RULE-SET,apple,DIRECT
  - RULE-SET,direct,DIRECT
  - RULE-SET,lancidr,DIRECT
  - RULE-SET,cncidr,DIRECT
  - GEOIP,LAN,DIRECT
  - GEOIP,CN,DIRECT
  - MATCH,Proxy
