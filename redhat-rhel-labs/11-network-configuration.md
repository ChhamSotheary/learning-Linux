# Lab ១១៖ គ្រប់គ្រង Network Configuration (Manage Network Configuration)

## គោលបំណង
ពិនិត្យ network interfaces, IP addresses, routes និង DNS ដោយប្រើ tools ដែលមាននៅ RHEL។

## ១. ពិនិត្យ interfaces និង IP
```bash
ip link
ip address
```
រក interface ដែលស្ថិតក្នុងស្ថានភាព UP និង IP address ដែលបានកំណត់។ ឈ្មោះ interface អាចជា `ens160`, `enp0s3` ឬផ្សេងទៀត។

## ២. ពិនិត្យ Routing
```bash
ip route
```
Default route ជាផ្លូវចេញទៅ network ផ្សេងៗ។ កុំកែ route ក្នុង VM ដែលអ្នកកំពុងភ្ជាប់ពីចម្ងាយ ប្រសិនបើគ្មាន console access។

## ៣. ពិនិត្យ DNS
```bash
cat /etc/resolv.conf
getent hosts redhat.com
```
លទ្ធផល DNS អាស្រ័យលើ network និងការកំណត់របស់អ្នក។ `getent` ប្រើ name service configuration របស់ប្រព័ន្ធ។

## ៤. ពិនិត្យ NetworkManager
```bash
systemctl status NetworkManager
nmcli device status
nmcli connection show
```
`nmcli` ជា command-line client របស់ NetworkManager។ ប្រសិនបើ command មិនមាន សូមពិនិត្យថា package និង service ត្រូវបានដំឡើងឬអត់។

## ៥. Connectivity test
```bash
ping -c 4 1.1.1.1
ping -c 4 redhat.com
```
បើ ping IP បាន តែ hostname មិនបាន អាចពាក់ព័ន្ធនឹង DNS។ ប៉ុន្តែ host ឬ network ខ្លះ block ICMP ដូច្នេះ ping មិនមែនជាភស្តុតាងតែមួយនៃ connectivity ទេ។

## លំហាត់
1. កត់ឈ្មោះ interface និង IP address។
2. រក default route។
3. ពិនិត្យ DNS resolver។
4. សាកល្បង ping IP និង hostname ហើយប្រៀបធៀប។
5. ពន្យល់ភាពខុសគ្នារវាង IP address, route និង DNS។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចប្រើ `ip address` និង `ip route`។
- [ ] ខ្ញុំអាចពិនិត្យ NetworkManager ដោយ `nmcli`។
- [ ] ខ្ញុំយល់ថា ping អាចត្រូវបាន block។

**សុវត្ថិភាព:** Lab នេះផ្តោតលើការពិនិត្យប៉ុណ្ណោះ។ កុំប្ដូរ IP, gateway ឬ DNS លើ VM ដោយគ្មាន snapshot និងផែនការស្ដារវិញ។
