# មេរៀនទី ៣៖ Kernel Parameters និង sysctl

## Parameter ពេល boot និង sysctl

Kernel command line ផ្តល់ argument នៅពេល boot; អានបច្ចុប្បន្នតាម /proc/cmdline។ sysctl ផ្តល់ interface សម្រាប់ parameter ជាច្រើននៅ runtime តាម /proc/sys។ ទាំងពីរមាន scope និង persistence ខុសគ្នា។ ការកំណត់នៅ /etc/sysctl.d ជាធម្មតាមាននៅ reboot តែតម្រូវឱ្យ load តាម distro។

## អានប៉ុណ្ណោះ

~~~bash
cat /proc/cmdline
sysctl kernel.ostype
sysctl net.ipv4.ip_forward
sysctl -a 2>/dev/null | head
~~~

មេរៀននេះមិនស្នើឱ្យប្រើ sysctl -w ឬកែ bootloader ទេ។ Parameter មួយចំនួនប្ដូរ security, network reachability ឬស្ថិរភាព ហើយការប្តូរខុសអាចធ្វើឱ្យប្រព័ន្ធមិន boot ឬ service ដាច់។

## វិធីវាយតម្លៃការកំណត់

1. រកឯកសារ kernel/distro ដែលត្រឹម version។
2. កត់តម្លៃបច្ចុប្បន្ន និងម្ចាស់ configuration។
3. កំណត់ metric ដែលបញ្ជាក់ថាការប្តូរជួយ។
4. សាកល្បងមួយចំណុចក្នុង VM និងកត់ rollback។
5. ត្រួតពិនិត្យបន្ទាប់ពី reboot ប្រសិនបើមានការអនុញ្ញាត។

## លំហាត់

ជ្រើស sysctl ដែលអានបានមួយ ហើយសរសេរ៖ អត្ថន័យ, scope, តើ persistent ទេ, និងហានិភ័យបើប្តូរ។
