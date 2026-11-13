# មេរៀនទី ២៖ Socket, Port និង Connection State

Socket ជាចំណុចទំនាក់ទំនងក្នុង kernel រវាងកម្មវិធី និង network ឬ local IPC។ TCP connection ត្រូវបានសម្គាល់ដោយ endpoint ទាំងពីរ (IP/port) និង protocol; listening socket ខុសពី established connection។

~~~bash
ss -lntup
ss -tan state established
ss -s
~~~

Option -p អាចបង្ហាញ process និងត្រូវការសិទ្ធិបន្ថែម។ កុំបិទ port ដោយសារមើលឃើញតែវាបើក៖ កំណត់ម្ចាស់សេវា, bind address, firewall និង business need ជាមុន។

## Port ដែល bind

សេវា bind ទៅ 127.0.0.1 ជាទូទៅសម្រាប់ local access; 0.0.0.0 ស្តាប់ IPv4 interfaces ទាំងអស់; :: មានន័យ IPv6 wildcard តាមការកំណត់ប្រព័ន្ធ។ ការបកស្រាយ IPv4-mapped behavior អាចខុសតាម socket setting។

## លំហាត់

សម្រាប់ listening socket មួយ កត់ protocol, local address, port, process, និងថាតើវាអាចចូលពី network ផ្សេងឬទេ។ កុំផ្ញើលទ្ធផលដែលមាន process/user ឯកជនជាសាធារណៈ។
