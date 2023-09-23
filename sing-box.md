{
    "dns": {
        "servers": [
            {
                "tag": "remote",
                "address": "https://1.1.1.1/dns-query",
                "detour": "select"
            },
            {
                "tag": "local",
                "address": "https://223.5.5.5/dns-query",
                "detour": "direct"
            },
            {
                "address": "rcode://success",
                "tag": "block"
            }
        ],
        "rules": [
            {
                "outbound": [
                    "any"
                ],
                "server": "local"
            },
            {
                "disable_cache": true,
                "geosite": [
                    "category-ads-all"
                ],
                "server": "block"
            },
            {
                "clash_mode": "global",
                "server": "remote"
            },
            {
                "clash_mode": "direct",
                "server": "local"
            },
            {
                "geosite": "cn",
                "server": "local"
            }
        ],
        "strategy": "prefer_ipv4"
    },
    "inbounds": [
        {
            "type": "tun",
            "inet4_address": "172.19.0.1/30",
            "inet6_address": "2001:0470:f9da:fdfa::1/64",
            "sniff": true,
            "sniff_override_destination": true,
            "domain_strategy": "prefer_ipv4",
            "stack": "mixed",
            "strict_route": true,
            "mtu": 9000,
            "endpoint_independent_nat": true,
            "auto_route": true
        },
        {
            "type": "socks",
            "tag": "socks-in",
            "listen": "127.0.0.1",
            "sniff": true,
            "sniff_override_destination": true,
            "domain_strategy": "prefer_ipv4",
            "listen_port": 2333,
            "users": []
        },
        {
            "type": "mixed",
            "tag": "mixed-in",
            "sniff": true,
            "sniff_override_destination": true,
            "domain_strategy": "prefer_ipv4",
            "listen": "127.0.0.1",
            "listen_port": 2334,
            "users": []
        }
    ],
  "experimental": {
    "clash_api": {
      "external_controller": "127.0.0.1:9090",
      "secret": "",
      "store_selected": true
    }
  },
  "log": {
    "disabled": false,
    "level": "info",
    "timestamp": true
  },
  "outbounds": [
    {
      "tag": "select",
      "type": "selector",
      "default": "urltest",
      "outbounds": [
        "urltest",
        "sing-box-reality",
        "sing-box-hysteria2",
        "sing-box-vmess"
      ]
    },
    {
      "type": "vless",
      "tag": "sing-box-reality",
      "uuid": "232ff626-16ad-4d08-8586-b91618bbd828",
      "flow": "xtls-rprx-vision",
      "packet_encoding": "xudp",
      "server": "155.248.199.247",
      "server_port": 443,
      "tls": {
        "enabled": true,
        "server_name": "itunes.apple.com",
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        },
        "reality": {
          "enabled": true,
          "public_key": "r_zeVPXPzTZNl-MTVShrUY9JYMJOe1cZY3XykCU8jjA",
          "short_id": "a2f14f68808b4b12"
        }
      }
    },
    {
            "type": "hysteria2",
            "server": "155.248.199.247",
            "server_port": 8443,
            "tag": "sing-box-hysteria2",
            
            "up_mbps": 100,
            "down_mbps": 100,
            "password": "185d2d25ea1ef05a",
            "tls": {
                "enabled": true,
                "server_name": "bing.com",
                "insecure": true,
                "alpn": [
                    "h3"
                ]
            }
        },
        {
            "server": "speed.cloudflare.com",
            "server_port": 443,
            "tag": "sing-box-vmess",
            "tls": {
                "enabled": true,
                "server_name": "calendar-incentive-constitutes-pays.trycloudflare.com",
                "insecure": true,
                "utls": {
                    "enabled": true,
                    "fingerprint": "chrome"
                }
            },
            "transport": {
                "headers": {
                    "Host": [
                        "calendar-incentive-constitutes-pays.trycloudflare.com"
                    ]
                },
                "path": "0164358c2123",
                "type": "ws"
            },
            "type": "vmess",
            "security": "auto",
            "uuid": "772b201b-7582-4507-b33b-348e25b0a9f3"
        },
    {
      "tag": "direct",
      "type": "direct"
    },
    {
      "tag": "block",
      "type": "block"
    },
    {
      "tag": "dns-out",
      "type": "dns"
    },
    {
      "tag": "urltest",
      "type": "urltest",
      "outbounds": [
        "sing-box-reality",
        "sing-box-hysteria2",
        "sing-box-vmess"
      ]
    }
  ],
  "route": {
    "auto_detect_interface": true,
    "rules": [
      {
        "geosite": "category-ads-all",
        "outbound": "block"
      },
      {
        "outbound": "dns-out",
        "protocol": "dns"
      },
      {
        "clash_mode": "direct",
        "outbound": "direct"
      },
      {
        "clash_mode": "global",
        "outbound": "select"
      },
      {
        "geoip": [
          "cn",
          "private"
        ],
        "outbound": "direct"
      },
      {
        "geosite": "geolocation-!cn",
        "outbound": "select"
      },
      {
        "geosite": "cn",
        "outbound": "direct"
      }
    ],
    "geoip": {
            "download_detour": "select"
        },
    "geosite": {
            "download_detour": "select"
        }
  }
}