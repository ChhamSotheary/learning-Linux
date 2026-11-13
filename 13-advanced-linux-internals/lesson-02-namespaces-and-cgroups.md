# មេរៀនទី ២៖ Namespaces និង Cgroups — គ្រឹះរបស់ Container

## គំនិតស្នូល

Namespaces ធ្វើឱ្យ process មើលឃើញទិដ្ឋភាពដាច់ដោយឡែកនៃធនធានសកលមួយចំនួន។ ប្រភេទសំខាន់ៗរួមមាន mount, PID, network, IPC, UTS, user និង cgroup namespaces។ Cgroups រៀបចំ process ជាក្រុម ដើម្បីតាមដាន ឬគ្រប់គ្រងការប្រើ CPU, memory, I/O និងចំនួន process តាមការគាំទ្ររបស់ kernel។

Container ជាទូទៅផ្សំ isolation ទាំងនេះជាមួយ filesystem, capabilities, seccomp និង runtime។ វាមិនមែនជា virtual machine ពេញលេញទេ៖ container ចែករំលែក kernel របស់ host។

## សង្កេត namespaces របស់ខ្លួន

~~~bash
ls -l /proc/self/ns
readlink /proc/self/ns/pid
cat /proc/self/cgroup
~~~

បើមាន util-linux:

~~~bash
lsns
systemd-cgls
~~~

ឈ្មោះ namespace ដូចគ្នាបង្ហាញ handle/ID មួយ ប៉ុន្តែការបកស្រាយត្រូវពឹងលើ context និងសិទ្ធិ។ កុំសាកល្បង unshare ឬបង្កើត namespace ជាមួយ privilege លើម៉ាស៊ីនដែលអ្នកមិនគ្រប់គ្រង។

## Cgroup v2

លើប្រព័ន្ធដែលប្រើ cgroup v2 អាចអាន៖

~~~bash
cat /sys/fs/cgroup/cgroup.controllers
cat /sys/fs/cgroup/cgroup.stat
~~~

controller ដែលមានអាចខុសតាម kernel និងការកំណត់របស់ distro។ ការបើក controller ឬសរសេរទៅឯកសារ cgroup គឺជាការកែប្រែ state; មេរៀននេះប្រើតែការអាន។ សូមមើលឯកសារ kernel សម្រាប់ច្បាប់ hierarchy និង semantics លម្អិត។

## ការគិតដូចអ្នកគ្រប់គ្រងប្រព័ន្ធ

- Namespace ឆ្លើយសំណួរ៖ process មើលឃើញអ្វីខ្លះ?
- Cgroup ឆ្លើយសំណួរ៖ process ប្រើធនធានប៉ុន្មាន/ត្រូវបានកំណត់យ៉ាងណា?
- Isolation មិនស្មើនឹង security boundary ល្អឥតខ្ចោះទេ។ Configuration, kernel, capabilities និង attack surface សុទ្ធតែសំខាន់។

## លំហាត់

1. រក namespace links របស់ shell បច្ចុប្បន្ន និងសរសេរថាតើមានប្រភេទណាខ្លះ។
2. មើល cgroup membership របស់ process ខ្លួនឯង។ តើវាបង្ហាញ path អ្វី?
3. ពន្យល់ភាពខុសគ្នារវាង “ដាច់ដោយឡែកក្នុងការមើលឃើញ” និង “កំណត់ការប្រើធនធាន”។

## ឯកសារយោង

- [namespaces(7)](https://man7.org/linux/man-pages/man7/namespaces.7.html)
- [Kernel cgroup v2](https://docs.kernel.org/admin-guide/cgroup-v2.html)
