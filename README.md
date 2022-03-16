# openwrt_rtl8821cu_no80211

WiFi dongle: rtl8811cu 0bda:c811

Openwrt Linux : 21.02.1
Linux Version : 5.4.154

Openwrt platform : mt7688 LinkIt Smart 7688

Driver version : v5.4.1_28754.20180921_COEX20180712-3232

Change from : https://github.com/ProKn1fe/RTL8811CU_OpenWRT

Caution:
	This package doesn't support cfg80211. The station mode only.

//---make 8821cu.ko 
//---pacakge build 
untar 
copy rtl8821cu/ to openrt/package/kernel 

select M at 
	Kernel modules
	Wireless Drivers
	kmod-rtl8821cu

make openrt/package/kernel/rtl8821cu/compile V=s

rtl8812au.ko at openwrt/staging_dir/target-mipsel_musl/root-ramips/lib/modules/5.4.154/

//---verify
[openwrt v5.4.154]+[rtl8811cu] --- [AP : greatcat5G : 192.168.2.1]

//off debug message
echo 0 > /proc/net/rtl8821cu/log_level

// as a station, link to AP

iwinfo wlan1 scan
iwconfig wlan0 essid greatcat5G
udhcpc -i wlan1

// iwconfig comes from
// https://downloads.openwrt.org/releases/21.02.1/packages/mipsel_24kc/base/
// wireless-tools_29-6_mipsel_24kc.ipk 

// test
ping 192.168.2.1
