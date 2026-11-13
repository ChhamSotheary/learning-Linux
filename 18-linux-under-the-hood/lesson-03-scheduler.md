# មេរៀនទី ៣៖ Scheduler និង Context Switch

Scheduler ជ្រើស task ដែលអាចរត់លើ CPU នៅពេលណា។ Process អាចមាន runnable, running, sleeping ឬ stopped state។ Context switch កើតឡើងពេល CPU ប្ដូរពី task មួយទៅមួយទៀត ហើយមាន cost ដូចជា register state, cache locality និង synchronization។ Scheduler policy និង implementation អាចប្ដូរតាម kernel version។

## សង្កេត

~~~bash
ps -eo pid,stat,ni,psr,comm --sort=pid | head -n 20
cat /proc/pressure/cpu
vmstat 1 5
~~~

STAT មានសញ្ញាសង្ខេបសម្រាប់ state; field PSR ជា CPU ដែលបានរត់ចុងក្រោយ មិនមែនការធានាថា task ចាក់សោរលើ CPU នោះទេ។ PSI CPU បង្ហាញសម្ពាធដែល task runnable ត្រូវរង់ចាំ CPU តាម semantics របស់ kernel។

កុំប្ដូរ nice, scheduler policy ឬ CPU affinity លើ service ផលិតកម្មដើម្បី “បង្កើនល្បឿន” ដោយគ្មានវាស់វែង និង rollback។

## លំហាត់

1. ពិនិត្យ process ធម្មតាពីរ ហើយប្រៀបធៀប STAT/NI។
2. មើល PSI CPU នៅពេល idle និង workload ធម្មតា។
3. ពន្យល់ភាពខុសគ្នារវាង CPU utilization ខ្ពស់ និង CPU pressure ខ្ពស់។
