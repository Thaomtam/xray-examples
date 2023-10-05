{
    "log": {
        "loglevel": "warning"
    },
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "type": "field",
                "port": "443",
                "network": "udp",
                "outboundTag": "block"
            },
            {
                "type": "field",
                "ip": [
                    "geoip:private"
                ],
                "outboundTag": "block"
            }
        ]
    },
    "inbounds": [
        {
            "listen": "0.0.0.0",
            "port": 443,
            "protocol": "vless",
            "settings": {
                "clients": [
                    {
                        "id": "thoi-tiet-openwrt",
                        "flow": "xtls-rprx-vision"
                    }
                ],
                "decryption": "none",
                "fallbacks": [
                    {
                        "dest": "8004",
                        "xver": 1
                    }
                ]
            },
            "streamSettings": {
                "network": "tcp",
                "security": "reality",
                "realitySettings": {
                    "dest": "itunes.apple.com:443",
                    "serverNames": [
                        "dl.kgvn.garenanow.com"
                    ],
                    "privateKey": "sELUHVtMZVXnBVNLOJYOR9NdpZbR7QVjS5b9X0F6iGU",
                    "shortIds": [
                        "e9455277471d0a78"
                    ]
                }
            },
            "sniffing": {
                "enabled": false,
                "destOverride": [
                    "http",
                    "tls",
                    "quic"
                ]
            }
        },
        {
            "listen": "127.0.0.1",
            "port": 8004,
            "protocol": "vless",
            "settings": {
                "clients": [
                    {
                        "id": "thoi-tiet-openwrt"
                    }
                ],
                "decryption": "none"
            },
            "streamSettings": {
                "network": "h2",
                "sockopt": {
                    "acceptProxyProtocol": true
                }
            },
            "sniffing": {
                "enabled": false,
                "destOverride": [
                    "http",
                    "tls",
                    "quic"
                ]
            }
        },
        {
			  "listen": "0.0.0.0",
			  "port": 16557,
			  "protocol": "socks",
			  "settings": {
					"auth": "password",
					"accounts": [
						{
							  "user": "admin",
							"pass": "admin123"
						}
					],
					"udp": true,
					"ip": "127.0.0.1"            
				},
			"streamSettings": {
				"network": "tcp",
				"security": "none"
			}
		}
    ],
    "outbounds": [
        {
            "protocol": "freedom",
            "tag": "direct"
        },
        {
            "protocol": "blackhole",
            "tag": "block"
        }
    ],
    "policy": {
        "levels": {
            "0": {
                "handshake": 2,
                "connIdle": 120
            }
        }
    }
}
