# មេរៀនទី ៤៖ Packet Path និង Network Performance

Packet receive អាចឆ្លង NIC queue, interrupt/NAPI, protocol stack, socket queue និង application។ កន្លែងណាមួយអាចក្លាយជា bottleneck។ Kernel docs ពិពណ៌នា RSS/RPS/RFS/XPS ជាវិធីចែកចាយការងារ ប៉ុន្តែមិនមាន setting ល្អសម្រាប់ hardware និង workload ទាំងអស់ទេ។

~~~bash
ip -s link
cat /proc/interrupts
ss -s
nstat -az 2>/dev/null | head
~~~

ប្រមូល counter មុន និងក្រោយពេលមានរោគសញ្ញា។ កុំប្ដូរ IRQ affinity, offload ឬ sysctl ដោយចៃដន្យ; វាអាចបន្ថែម latency ឬធ្វើឱ្យ throughput ធ្លាក់។

## លំហាត់

សម្រាប់ interface មួយ ប្រមូល RX/TX errors/drops ពីរពេលខុសគ្នា។ ពន្យល់ថា counter កើនឡើងអ្វី និងត្រូវប្រមូលភស្តុតាងណាបន្ថែម មុនសន្និដ្ឋានថាជា hardware fault។
