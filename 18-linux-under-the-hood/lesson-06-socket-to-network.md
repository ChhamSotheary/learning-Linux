# មេរៀនទី ៦៖ ពី Socket ទៅ Network Interface

កម្មវិធីសរសេរទៅ socket; kernel រៀបចំ transport/network headers និង route; packet ឆ្លង queue និង driver ទៅ NIC។ ពេលទទួល packet ដំណើរការទៅទិសផ្ទុយ តាម NIC queue, interrupt/NAPI និង protocol stack រហូតដល់ socket របស់កម្មវិធី។ Offload និង virtual networking អាចប្តូរផ្លូវលម្អិត។

## សង្កេត traffic ផ្ទាល់ខ្លួន

~~~bash
ss -tan
ip -s link
~~~

ប្រសិនបើ tcpdump ត្រូវបានដំឡើង និងមានសិទ្ធិ អ្នកអាចចាប់តែ loopback traffic របស់ខ្លួនឯងក្នុង VM។ កុំ capture traffic អ្នកដទៃ ឬ network ដែលគ្មានសិទ្ធិ។ Packet capture អាចមាន cookie, token និងទិន្នន័យផ្ទាល់ខ្លួន។

## Debug ជាស្រទាប់

1. តើ app កំពុង listen/connect ទេ? ពិនិត្យ ss។
2. តើ address និង route ត្រឹមត្រូវទេ? ពិនិត្យ ip address/route។
3. តើ DNS បកប្រែឈ្មោះបានទេ?
4. តើ firewall/policy រារាំងទេ?
5. តើ packet/error counters កើនឡើងទេ?
6. តើ server app ទទួល request ហើយឆ្លើយ error អ្វី?

## លំហាត់

គូរផ្លូវ request របស់ browser ទៅ local demo web server ដោយរាយ DNS (បើប្រើ hostname), socket, routing និង application layer។ បែងចែកអ្វីដែលបានពិនិត្យពីអ្វីដែលគ្រាន់តែសន្មត។
