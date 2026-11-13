# មេរៀនទី ១៖ Routing Table និង Policy Routing

## Route ជ្រើសផ្លូវ

Kernel ប្រើ routing table ដើម្បីសម្រេចថា packet ចេញតាម interface/gateway ណា។ Route ជាក់លាក់ជាងអាចឈ្នះ route ទូទៅ ហើយ policy routing អាចជ្រើស table ផ្សេងតាម rule។ VPN, multiple NIC និង container អាចបន្ថែម route/rule ច្រើន។

## អានស្ថានភាព

~~~bash
ip -br address
ip route
ip rule
ip route get 1.1.1.1
~~~

ip route get បង្ហាញការសម្រេចចិត្ត route សម្រាប់ destination តាម context បច្ចុប្បន្ន។ វាមិនសាកល្បងថា remote host ឆ្លើយតបឬអត់ទេ។

## វិធី troubleshoot

ពិនិត្យ interface/link → address/prefix → route/rule → neighbor/ARP → firewall → DNS → application។ ប្រើ ping ឬ curl តែទៅគោលដៅដែលអ្នកមានសិទ្ធិ និងកុំសន្និដ្ឋានថា ping មិនឆ្លើយមានន័យថា host ដាច់ជានិច្ច។

## លំហាត់

1. រក default route និង interface របស់វា។
2. ប្រើ ip route get សម្រាប់ IP ដែលមានសុវត្ថិភាពក្នុង lab។
3. គូរផ្លូវ packet ពី local app ទៅ gateway និងបញ្ជាក់ថាតើ DNS ចូលនៅជំហានណា។
