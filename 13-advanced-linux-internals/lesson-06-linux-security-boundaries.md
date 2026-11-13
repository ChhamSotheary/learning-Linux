# មេរៀនទី ៦៖ Capabilities, Seccomp និង LSM

## ពី root ទៅ capabilities

ការមាន UID 0 មិនមែនមានន័យថាដំណើរការមានសិទ្ធិគ្មានដែនកំណត់ក្នុងគ្រប់ context ទេ។ Linux បែងចែក privilege មួយចំនួនជាសមត្ថភាព (capabilities) ដូចជា CAP_NET_ADMIN ឬ CAP_SYS_ADMIN។ សិទ្ធិពិតប្រាកដនៅតែអាស្រ័យលើ namespace, capability sets, policy និង kernel។

មើល status របស់ shell ខ្លួនឯង៖

~~~bash
grep -E '^(Uid|Gid|CapInh|CapPrm|CapEff|CapBnd|NoNewPrivs|Seccomp):' /proc/self/status
~~~

លេខ Cap* ជា bitmask មិនមែនជាបញ្ជីឈ្មោះអានងាយទេ។ ប្រសិនបើ capsh មាន អាចអាន៖

~~~bash
capsh --print
~~~

## Seccomp និង LSM

Seccomp អាចកំណត់ system calls ដែល process អនុញ្ញាតឱ្យហៅ តាម filter។ វាមិនជំនួសការកំណត់ user, filesystem permission ឬ namespace ទេ។

LSM (Linux Security Modules) ជា framework សម្រាប់ policy បន្ថែម ដូចជា SELinux និង AppArmor។ វាអាចត្រូវបានកំណត់ឱ្យ enforce ឬ log/complain អាស្រ័យលើ distro និង policy។ ពិនិត្យ status ដោយ command ដែលមានលើ distro របស់អ្នក៖

~~~bash
getenforce
aa-status
~~~

command មួយអាចមិនមាន ប្រសិនបើ distro ប្រើ LSM ផ្សេង ឬមិនដំឡើង utility។

## គោលការណ៍អនុវត្ត

- កាត់បន្ថយ privilege ដែលកម្មវិធីមិនត្រូវការឱ្យនៅសល់តិចបំផុត។
- កុំដំណើរការកម្មវិធីមិនទុកចិត្តជា root។
- កុំបិទ SELinux/AppArmor ឬដក seccomp ដើម្បីឱ្យ error បាត់។
- វិភាគ audit/journal និង policy denial មុនកែ policy។
- សាកល្បង policy ក្នុង VM ហើយមានផ្លូវ rollback។

## លំហាត់

1. ពិនិត្យ CapEff និង NoNewPrivs របស់ shell របស់អ្នក។ តើតម្លៃទាំងនោះប្រាប់អ្វី?
2. ពន្យល់ភាពខុសគ្នារវាង capability, seccomp និង LSM។
3. រកឧទាហរណ៍មួយនៃសេវាដែលអាចដំណើរការដោយ privilege តិចជាង root ហើយរាយសិទ្ធិដែលវាត្រូវការ។

## ឯកសារយោង

- [Linux capabilities(7)](https://man7.org/linux/man-pages/man7/capabilities.7.html)
- [seccomp(2)](https://man7.org/linux/man-pages/man2/seccomp.2.html)
