#SA-MP Iptables Firewall
#Layer 7 Protection
#Rodriquez
#Additional Information; Attacks at a certain level are disabled,do not provide 100% protection, server features (cpu) must be high.

iptables -I INPUT  -s 68.45.155.112 -j ACCEPT
iptables -I INPUT  -s 68.45.160.0/24 -j ACCEPT
iptables -I INPUT  -s  45.46.170.13 -j ACCEPT
iptables -I INPUT  -s  45.46.160.0/24 -j ACCEPT		

iptables -t filter -A OUTPUT -p icmp -m icmp --icmp-type echo-reply -j DROP
iptables -t filter -A OUTPUT -p icmp -m icmp --icmp-type port-unreachable -j DROP

iptables -N Rodri
iptables -I INPUT -p udp \! -f -m udp --dport 7777 -m conntrack --ctstate NEW,ESTABLISHED -m u32 --u32 "0x0>>0x16&0x3c@0x8=0x53414d50" -j Rodri
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4500003e740700006a11|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|b91d79d220910100002a|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|3d269a18365500000000|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e49543100650000880d|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e495431006500008805|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e495431006500008802fd66|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e495431006588010100|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e49543100650000880c80d2|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|b91d79d214d4010001ee|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e49543100650000880edc3ae60060c6|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e495431006500008802fd66d3000000|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e49543100650000880edc3ae60060c6|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e495431006500008802fd66d3000000|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e49543100650000880edc3ae6049f8e|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|45000035d159000073114cf0134de331|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|b91d79d233c6010000210000ffffffff|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|54536f7572636520456e67696e652051|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e495431006500008805831b74000000|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e49543158442d5573645423534e6730|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|4e49543100000000000000000000|'" -j DROP
iptables -A INPUT -p udp --dport 7777 -m string --algo kmp --from 0x38 --hex-string "'|45000068d8310000f211fd6ab94c06ac|'" -j DROP
iptables -I INPUT -p udp -m udp -m string --hex-string "|ffffffff6765746368616c6c656e676520302022|" --algo kmp -j DROP
iptables -A INPUT -p udp -m u32 --u32 "6&0xFF=0,2:5,7:16,18:255" -j DROP

iptables -I INPUT -p udp --dport 7777 -m state --state NEW -m recent --update --seconds 120 --hitcount 300 -j

iptables -A Rodri -j REJECT --reject-with icmp-port-unreachable
