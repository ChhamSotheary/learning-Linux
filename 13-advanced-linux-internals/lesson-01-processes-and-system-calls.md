# មេរៀនទី ១៖ ពី Process ទៅ System Call

## គោលបំណង

យល់ពីព្រំដែនរវាងកម្មវិធី និង kernel, របៀប process/thread ត្រូវបានតាមដាន និងរបៀបប្រើ strace ដើម្បីសង្កេតកម្មវិធីរបស់ខ្លួន។

## User space និង Kernel space

កម្មវិធីធម្មតាដំណើរការនៅ user space ហើយមិនអាចបញ្ជា hardware ឬចូល kernel memory ដោយផ្ទាល់បានទេ។ ពេលត្រូវការអាន file, បង្កើត process, ផ្ញើ network packet ឬស្នើ memory ពិសេស វាហៅ system call។ Kernel ពិនិត្យសំណើ និងសិទ្ធិ បន្ទាប់មកត្រឡប់លទ្ធផល ឬ error។

នេះជាខ្សែគំនិត មិនមែនជារូបភាពរាល់ system call ទាំងអស់ទេ៖

~~~text
កម្មវិធី → library wrapper → system call → kernel → លទ្ធផល/error → កម្មវិធី
~~~

ឧទាហរណ៍ ការហៅ fopen ក្នុង C ជាទូទៅឆ្លងកាត់ library; library អាចបង្កើត system call ដូចជា openat/read/close។ ឈ្មោះ syscall ពិតប្រាកដអាចខុសតាម library, architecture និង kernel។

## Process និង Thread

Process មាន address space និងធនធានដូចជា file descriptors។ Thread ជាខ្សែការងារមួយក្នុង process ហើយជាទូទៅចែករំលែក memory និងធនធានមួយចំនួនជាមួយ thread ផ្សេងៗក្នុង process ដដែល។ PID ដែលឃើញតាម tool អាចសំដៅ thread-group leader ឬ thread ID អាស្រ័យលើឯកសារ/command។

## សង្កេតប្រព័ន្ធ

~~~bash
ps -eo pid,ppid,stat,comm --sort=pid | head
cat /proc/self/status
ls -l /proc/self/ns
~~~

/proc ជា interface សម្រាប់ព័ត៌មាន runtime របស់ kernel និង process។ វាមិនមែនជា hard drive ធម្មតាដែលរក្សាទុកឯកសារអចិន្ត្រៃយ៍ទេ។

បើមាន strace សាកល្បងតែលើ command ធម្មតារបស់អ្នក៖

~~~bash
strace -f -e trace=file,process -o /tmp/my-command.trace -- sh -c 'printf "hello\n"'
less /tmp/my-command.trace
~~~

strace បង្ហាញ syscall និង argument មួយចំនួន។ វាអាចបន្ថយល្បឿនកម្មវិធី និង log អាចមាន path ឬទិន្នន័យរសើប។ កុំ trace process របស់អ្នកដទៃដោយគ្មានសិទ្ធិ។

## រក error

syscall ជាច្រើនត្រឡប់តម្លៃបរាជ័យ ហើយកំណត់ errno។ strace អាចបង្ហាញករណីដូចជា ENOENT (path មិនមាន) ឬ EACCES (គ្មានសិទ្ធិ)។ កុំសន្និដ្ឋានពីមួយបន្ទាត់តែឯង៖ ពិនិត្យ path, user, mount និង context ផង។

## លំហាត់

1. ពិនិត្យ /proc/self/status ហើយសរសេរពន្យល់ PID, PPid និង Threads។
2. ប្រើ strace លើ command ដែលអាន file សាកល្បងរបស់អ្នក ហើយរក syscall បើក/អាន/បិទ file។
3. ប្រៀបធៀប command ដដែលដោយមាន និងគ្មាន strace។ តើ output ដូចគ្នាទេ? តើ trace បន្ថែមអ្វី?

## ចំណុចសំខាន់

System call ជាព្រំដែនសំណើសេវា kernel; strace ជាឧបករណ៍សង្កេត មិនមែនជាឧបករណ៍សម្រាប់សន្និដ្ឋាន security ទាំងមូលទេ។
