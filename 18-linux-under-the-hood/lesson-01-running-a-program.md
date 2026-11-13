# មេរៀនទី ១៖ ពេលរត់កម្មវិធី — ELF និង Dynamic Linker

ពេលអ្នករត់ binary មួយ Shell ស្វែងរក executable តាម PATH ហើយស្នើ kernel បង្កើត process ថ្មី (ជាទូទៅតាម fork/clone ហើយ execve)។ Kernel អាន format របស់ executable ដូចជា ELF, រៀបចំ memory segments និងបញ្ជូនទៅ entry point។ បើកម្មវិធីត្រូវការ dynamic libraries នោះ interpreter/dynamic linker ផ្ទុក library និងរៀបចំ symbol references មុនកម្មវិធីដំណើរការធម្មតា។

## សង្កេត

~~~bash
command -v ls
file /bin/ls
readelf -h /bin/ls
readelf -l /bin/ls | grep interpreter
ldd /bin/ls
~~~

readelf មកពី binutils; file ឬ ldd អាចមិនមានលើប្រព័ន្ធតូចៗ។ ប្រើ ldd តែលើ binary ដែលទុកចិត្ត ព្រោះការវិភាគ executable មិនទុកចិត្តគួរធ្វើក្នុង sandbox។

ពិនិត្យ syscall ជាក់ស្តែងលើ command សាមញ្ញ៖

~~~bash
strace -f -e trace=process,file -o /tmp/ls.trace ls /tmp
less /tmp/ls.trace
~~~

## ចំណុចដែលងាយច្រឡំ

- Shell ខ្លួនឯងជ្រើស executable; kernel មិនស្វែងរក PATH ជំនួស shell ទេ។
- Dynamic linker មិនមែនជា kernel; វាជា user-space program ដែល kernel ចាប់ផ្តើមតាម ELF interpreter។
- library ដែលបង្ហាញដោយ ldd ជា dependency ក្នុង environment បច្ចុប្បន្ន ហើយអាចខុសនៅ host ផ្សេង។

## លំហាត់

1. រក ELF interpreter របស់ binary ដែលអ្នកស្គាល់។
2. ក្នុង strace រក execve និងការបើក shared library។
3. សរសេរលំដាប់ពី command ដែលអ្នកវាយ រហូតដល់ main() ចាប់ផ្តើម។
