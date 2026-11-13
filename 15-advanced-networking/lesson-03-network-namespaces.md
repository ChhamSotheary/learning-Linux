# មេរៀនទី ៣៖ Network Namespace, veth និង Bridge

Network namespace អាចមាន interface, route, firewall rules និង socket view ផ្ទាល់ខ្លួន។ veth pair ជាគូ interface ដែល packet មួយចុងចេញទៅមួយចុង។ Linux bridge អាចភ្ជាប់ interface ដូចជា switch software។ Container runtime ជាច្រើនប្រើគំនិតទាំងនេះ។

## សង្កេតដោយមិនបង្កើត topology

~~~bash
ip -br link
ip -br address
ip route
ls -l /proc/self/ns/net
~~~

ការបង្កើត namespace, veth ឬ bridge ត្រូវការ privilege ហើយអាចប៉ះពាល់ network។ រៀន topology នៅក្នុង VM ដាច់ដោយឡែក; កុំប្រើ ip netns add ឬប្ដូរ route នៅលើម៉ាស៊ីនដែលអ្នកពឹងផ្អែកលើ network នោះ។

## លំហាត់លើក្រដាស

គូរ client namespace និង service namespace ភ្ជាប់ដោយ veth pair ទៅ bridge។ សម្គាល់ IP, route, gateway និងកន្លែងដែល firewall policy ត្រូវពិនិត្យ។ ពន្យល់ថា namespace ផ្តល់ isolation អ្វី ហើយមិនការពារអ្វី។
