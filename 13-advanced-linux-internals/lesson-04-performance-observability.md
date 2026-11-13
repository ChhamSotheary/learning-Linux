# មេរៀនទី ៤៖ Performance Observability និង eBPF

## មុននឹង optimize

ចាប់ផ្តើមពីសំណួរថា “យឺតត្រង់ណា?” CPU, memory, disk I/O, network ឬ lock/contention? កត់ baseline, ពេលវេលា, workload និងការផ្លាស់ប្តូរដែលបានធ្វើ។ ការមើល CPU ខ្ពស់តែមួយមុខមិនប្រាប់ថា process ណាជាមូលហេតុ ឬថាវាជាបញ្ហាពិតទេ។

## ឧបករណ៍មូលដ្ឋាន

~~~bash
uptime
free -h
vmstat 1 5
ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head
cat /proc/pressure/cpu
cat /proc/pressure/memory
cat /proc/pressure/io
~~~

vmstat អាចមិនមានលើប្រព័ន្ធតូចៗ។ PSI (Pressure Stall Information) មានលើ kernel ដែលគាំទ្រ ហើយអាចប្រាប់ពេល task ត្រូវរង់ចាំធនធាន។ បកស្រាយជាមួយ workload និងពេលវេលា មិនមើលលេខតែឯង។

បើ perf ឬ eBPF tools ត្រូវបានដំឡើង សូមប្រើតែលើ VM/lab របស់អ្នក និងពិនិត្យ privilege និង overhead មុន។ កុំដំឡើង tool ឬបើក profiling លើម៉ាស៊ីនផលិតកម្មដោយគ្មានការអនុម័ត។ eBPF អនុញ្ញាតឱ្យកម្មវិធីតូចភ្ជាប់ទៅចំណុច kernel ដែលបានកំណត់ ហើយ kernel ផ្ទៀងផ្ទាត់កម្មវិធីមុនដំណើរការ; នេះមិនមានន័យថាអាចទុកចិត្តកម្មវិធីគ្រប់ប្រភេទដោយស្វ័យប្រវត្តិទេ។

## វិធីសាស្ត្រ troubleshoot

1. កំណត់រោគសញ្ញា និងចាប់ផ្តើម/បញ្ចប់ពេលវេលា។
2. ប្រមូល baseline ដោយមិនប្ដូរ configuration។
3. បំបែក workload តាម process, cgroup ឬ resource។
4. បង្កើតសម្មតិកម្មដែលអាចវាស់បាន។
5. ផ្លាស់ប្តូរមួយចំណុចនៅក្នុង lab ហើយប្រៀបធៀប។
6. រក្សាទុកលទ្ធផល និងរបៀបត្រឡប់ការផ្លាស់ប្តូរ។

## លំហាត់

1. ប្រមូល uptime, free, vmstat និង PSI នៅពេល idle និងពេលបើកកម្មវិធីធម្មតា។
2. សរសេរថា CPU load average ខុសពី CPU utilization ដូចម្តេច។
3. បង្កើតសម្មតិកម្មមួយពីទិន្នន័យដែលបានមើល និងបញ្ជាក់ថាតើត្រូវការវាស់អ្វីបន្ថែម មុន optimize។

## ឯកសារយោង

[Linux kernel BPF documentation](https://docs.kernel.org/bpf/)
