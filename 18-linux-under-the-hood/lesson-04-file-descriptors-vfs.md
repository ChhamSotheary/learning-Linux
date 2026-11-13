# មេរៀនទី ៤៖ File Descriptor និង VFS

File descriptor (FD) គឺជាលេខតូចមួយក្នុង process ដែលយោងទៅ open file description ក្នុង kernel។ FD អាចតំណាងឱ្យ regular file, socket, pipe, terminal ឬ device។ VFS ផ្តល់ interface ទូទៅឱ្យ filesystem ផ្សេងៗអនុវត្តប្រតិបត្តិការស្រដៀងគ្នា។

## សង្កេត FD របស់ process test

~~~bash
sleep 60 &
pid=$!
ls -l /proc/$pid/fd
cat /proc/$pid/fdinfo/0
kill "$pid"
~~~

Shell អាចមាន FD 0/1/2 សម្រាប់ stdin/stdout/stderr។ FD ដែលមាន suffix ជា socket ឬ pipe មិនមែនជា file ធម្មតាទេ។ Hard link គឺឈ្មោះច្រើនចង្អុល inode ដូចគ្នា ខណៈ symlink ផ្ទុក path ទៅ target។

## ពេល file ត្រូវបានលុបតែ disk មិនទាន់ទំនេរ

បើ process នៅកាន់ open FD ទៅ inode មួយ បន្ទាប់ពីឈ្មោះ file ត្រូវបាន unlink នោះទំហំអាចនៅតែប្រើរហូតដល់ FD បិទ។ ក្នុង lab អ្នកអាចសង្កេត file test របស់ខ្លួនដោយ lsof ប្រសិនបើមាន។ កុំសម្លាប់ process ដែលកាន់ file ក្នុងប្រព័ន្ធមិនមែន lab។

## លំហាត់

1. បង្កើត process test ដែលបើក FD ហើយមើល /proc/PID/fd។
2. ពន្យល់ហេតុអ្វី FD ជា integer មិនបញ្ជាក់ប្រភេទ resource។
3. សរសេរជំហាន diagnose ករណី df បង្ហាញ disk ពេញ ប៉ុន្តែ du មើលទៅមិនពេញ។
