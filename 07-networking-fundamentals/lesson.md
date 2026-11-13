# មេរៀនទី ៧៖ Networking Fundamentals ក្នុង Linux

## គោលបំណង

- ពន្យល់ IP address, subnet, gateway, DNS, port, TCP និង UDP។
- មើល network interfaces និង routing table។
- ពិនិត្យ DNS និង reachability ដោយ commands មូលដ្ឋាន។
- មើល listening sockets និងស្គាល់ ports ដែលសេវាកម្មប្រើ។
- អនុវត្តតែជាមួយម៉ាស៊ីន និងបណ្ដាញដែលអ្នកមានសិទ្ធិ។

## ១. ពាក្យគន្លឹះ

- Network interface: ច្រក logical/physical ដែលម៉ាស៊ីនប្រើទាក់ទងបណ្ដាញ ដូចជា Ethernet ឬ Wi-Fi។
- IP address: អាសយដ្ឋានរបស់ interface ក្នុង network។
- Subnet/prefix: បង្ហាញជួរ address ដែលជាផ្នែកនៃ network ដូចជា /24។
- Default gateway: router ដែលបញ្ជូន traffic ទៅ networks ផ្សេង។
- DNS: បកប្រែ hostname ដូចជា example.com ទៅ IP address។
- Port: លេខសម្គាល់ endpoint នៃ application/service ក្នុង host។
- TCP: transport protocol ដែលផ្ដោតលើ reliable ordered byte stream។
- UDP: transport protocol ដែលផ្ញើ datagrams ដោយគ្មានការធានា delivery/order ដូច TCP។

Port number តែមួយមិនប្រាប់ថាសេវាកម្មមានសុវត្ថិភាពឬអត់ទេ; ត្រូវពិនិត្យ process និង configuration ផងដែរ។

## ២. មើល Interfaces និង Address

~~~bash
ip link
ip addr
~~~

ip link រាយ interfaces និង state។ ip addr បង្ហាញ IP addresses និង prefix lengths។ Interface state DOWN មិនចាំបាច់ជាបញ្ហាទេ ប្រសិនបើវាមិនត្រូវប្រើ។

## ៣. Routing និង Gateway

~~~bash
ip route
~~~

Default route បង្ហាញផ្លូវចេញពី network បច្ចុប្បន្នទៅ gateway។ Routing table អាចមាន routes ជាច្រើនតាម VPN, container ឬ network configuration។

## ៤. DNS និង Reachability

ពិនិត្យការបកប្រែ hostname៖

~~~bash
getent hosts example.com
~~~

getent ប្រើ name service configuration របស់ប្រព័ន្ធ។ អាចពិនិត្យ reachability ទៅ host ដែលអ្នកមានសិទ្ធិប្រើ៖

~~~bash
ping -c 4 example.com
~~~

Ping អាចត្រូវបានបិទដោយ firewall ឬ network policy។ គ្មាន response មិនបញ្ជាក់ថា host មិនដំណើរការទេ។ កុំបញ្ជូន ping ឬ traffic ជាបរិមាណខ្ពស់ទៅប្រព័ន្ធអ្នកដទៃ។

## ៥. Listening Ports និង Connections

~~~bash
ss -tuln
ss -tpn
~~~

- -t TCP sockets។
- -u UDP sockets។
- -l listening sockets។
- -n បង្ហាញលេខ address/port ដោយមិន resolve names។
- -p បង្ហាញ process information ប្រសិនបើ permission អនុញ្ញាត។

Listening port មានន័យថា process កំពុងរង់ចាំ connection នៅ address/port មួយ។ វាមិនមានន័យថា port អាចចូលពី Internet បានទេ; firewall, routing និង bind address ក៏សំខាន់ដែរ។

## ៦. ពិនិត្យ HTTP Connection

សម្រាប់គេហទំព័រ ឬ server ដែលអ្នកគ្រប់គ្រង អាចប្រើ curl ដើម្បីមើល response headers៖

~~~bash
curl -I https://example.com
~~~

កុំផ្ញើ credentials ឬ private tokens ទៅ endpoint ដែលមិនទុកចិត្ត។ កុំប្រើ curl ដើម្បីទាញយក និងរត់ script ដោយមិនអានមាតិកា។

## ៧. Troubleshooting Checklist

ពេលមិនអាចភ្ជាប់បាន៖

1. ពិនិត្យ interface និង IP ដោយ ip addr។
2. ពិនិត្យ route ដោយ ip route។
3. ពិនិត្យ DNS ដោយ getent hosts។
4. សាកល្បង connection ជាមួយ service ដែលអ្នកមានសិទ្ធិប្រើ។
5. ពិនិត្យ proxy, VPN, firewall និង application logs។
6. កត់ error message និងពេលកើតបញ្ហា។

កុំបិទ firewall ទាំងស្រុងជាវិធីដោះស្រាយដំបូង។ កែតែ rule ដែលចាំបាច់ និងតាមគោលការណ៍របស់ប្រព័ន្ធ។

## ៨. កិច្ចការអនុវត្ត

1. ប្រើ ip link និង ip addr ដើម្បីកំណត់ interface និង IP របស់ម៉ាស៊ីន។
2. ប្រើ ip route ដើម្បីរក default route ប្រសិនបើមាន។
3. ប្រើ getent hosts example.com ដើម្បីពិនិត្យ DNS។
4. ប្រើ ss -tuln ដើម្បីមើល listening sockets។
5. បើគោលការណ៍ network អនុញ្ញាត សាក ping -c 4 ទៅ host ដែលអ្នកអាចប្រើបាន។
6. ពន្យល់ហេតុអ្វី ping មិនឆ្លើយតប មិនមែនជាភស្តុតាងថា server down។
7. កុំ scan ports ឬបង្កើត traffic ទៅប្រព័ន្ធដែលអ្នកមិនបានអនុញ្ញាត។

## សង្ខេប

ip បង្ហាញ interfaces, addresses និង routes។ getent ជួយពិនិត្យ DNS។ ping ពិនិត្យ reachability តាម ICMP ប្រសិនបើ network អនុញ្ញាត។ ss បង្ហាញ sockets/ports។ curl អាចពិនិត្យ HTTP response។ លទ្ធផលត្រូវបកស្រាយជាមួយ firewall, routing និង permissions។

## ឯកសារយោង

- [ip manual](https://man7.org/linux/man-pages/man8/ip.8.html)
- [ss manual](https://man7.org/linux/man-pages/man8/ss.8.html)
- [getent manual](https://man7.org/linux/man-pages/man1/getent.1.html)
- [curl documentation](https://curl.se/docs/)
