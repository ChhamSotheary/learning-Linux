# មេរៀនទី ៥៖ Memory Pressure, Page Cache និង OOM

## Memory មិនមានតែ RAM ដែលកម្មវិធីកាន់កាប់

Linux ប្រើ RAM សម្រាប់ process និង cache ទិន្នន័យ file ដែលអាចយកមកប្រើឡើងវិញបាន។ ដូច្នេះ “used memory” មួយលេខមិនគ្រប់គ្រាន់សម្រាប់សន្និដ្ឋានថា RAM អស់ទេ។ ពិនិត្យ available, swap, page cache, pressure និងសារក្នុង kernel log ជាមួយគ្នា។

## ពិនិត្យដោយ read-only command

~~~bash
free -h
grep -E 'MemAvailable|Cached|SwapTotal|SwapFree|Dirty|Writeback' /proc/meminfo
vmstat 1 5
cat /proc/pressure/memory
dmesg --level=err,warn | tail -n 40
~~~

សិទ្ធិអាន dmesg អាចត្រូវបានកំណត់ដោយ distro។ កុំបង្ហោះ log ដោយមិនពិនិត្យព័ត៌មានឯកជនជាមុន។

Kernel អាចសម្លាប់ process ក្នុងស្ថានភាព memory ខ្វះខាតធ្ងន់ ដើម្បីសង្គ្រោះប្រព័ន្ធ។ នៅក្នុង cgroup ក៏អាចមាន memory limit និង local OOM behavior ផងដែរ។ សញ្ញា OOM ត្រូវអានជាមួយ cgroup និង system log មិនមែនគិតថាជា “Linux bug” ភ្លាមៗទេ។

## ចំណុចដែលងាយយល់ច្រឡំ

- Cache អាចបង្កើនការប្រើ RAM ប៉ុន្តែជាច្រើនអាចយកមកប្រើឡើងវិញបាន។
- Swap activity ខ្លាំងជាបន្តបន្ទាប់អាចធ្វើឱ្យប្រព័ន្ធយឺត ប៉ុន្តែការមាន swap មិនមែនជាបញ្ហាដោយខ្លួនឯងទេ។
- OOM kill មិនបញ្ជាក់ថា process ដែលត្រូវ kill ជាមូលហេតុដើមជានិច្ចទេ។
- កុំប្រើ drop_caches ឬប្តូរ swap/kernel settings ជា “ដំណោះស្រាយរហ័ស” លើម៉ាស៊ីនផលិតកម្ម។

## លំហាត់

1. ប្រៀបធៀប MemFree និង MemAvailable ក្នុង /proc/meminfo។
2. ពិនិត្យ memory PSI និង vmstat ហើយពន្យល់ថាតើមានសម្ពាធ memory ឬអត់។
3. ស្វែងរកសារដែលមានពាក្យ OOM ក្នុង log lab ឬរៀបរាប់ព័ត៌មានដែលត្រូវប្រមូល ប្រសិនបើវាកើតឡើង។

## ឯកសារយោង

- [Kernel memory management documentation](https://docs.kernel.org/admin-guide/mm/)
- [Kernel cgroup v2 documentation](https://docs.kernel.org/admin-guide/cgroup-v2.html)
