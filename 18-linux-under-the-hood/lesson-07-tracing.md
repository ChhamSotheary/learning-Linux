# មេរៀនទី ៧៖ Tracing — strace, perf និង eBPF

strace សង្កេត system calls របស់ process។ perf ប្រមូល performance events ដែល kernel/hardware គាំទ្រ។ eBPF ផ្តល់របៀបភ្ជាប់កម្មវិធីតូចៗទៅ hook ដែលបានកំណត់ ដើម្បី observability ឬ networking/security use cases។ Tool ទាំងនេះខុសគ្នាតាម scope, overhead, privilege និងអ្វីដែលវាវាស់បាន។

## ច្បាប់មុន trace

- ចាប់ផ្តើមពីសំណួរដែលអាចវាស់បាន។
- Trace តែ process ផ្ទាល់ខ្លួន ឬដោយមានការអនុញ្ញាត។
- កុំបើកទិន្នន័យ payload ឬ argument ដែលអាចមាន secret។
- កត់ version, command, duration និង overhead។
- កុំដំឡើង BPF program មិនទុកចិត្ត ឬបើក privileged tracing លើ production ដោយខ្លួនឯង។

## strace សាមញ្ញ

~~~bash
strace -c -- sleep 1
~~~

បើ kernel policy ឬ environment មិនអនុញ្ញាត នោះវាអាច fail។ Failure នោះជាភស្តុតាងអំពី policy មិនមែនហេតុផលឱ្យបិទ protection ទេ។

## លំហាត់

1. សរសេរសំណួរមួយដែល strace អាចឆ្លើយ និងមួយដែលវាមិនអាចឆ្លើយ។
2. ពន្យល់ថាហេតុអ្វី profile មាន overhead ហើយ trace ខ្លីអាចមិនតំណាង workload ពេញ។
3. ប្រៀបធៀបប្រភេទទិន្នន័យដែល strace, perf និង eBPF អាចប្រមូលបាន។
