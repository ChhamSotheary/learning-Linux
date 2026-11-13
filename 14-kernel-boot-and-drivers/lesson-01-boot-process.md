# មេរៀនទី ១៖ ដំណើរការ Boot និង initramfs

## លំដាប់ទូទៅ

ម៉ាស៊ីនបើក → firmware (UEFI/BIOS) ជ្រើស boot entry → bootloader ផ្ទុក kernel និង initramfs → kernel ចាប់ផ្តើម hardware និង mount root filesystem → init system (ជាទូទៅ systemd) ចាប់ផ្តើម units។

លំដាប់ពិតអាចខុសតាម architecture, distro និងការអ៊ិនគ្រីប/RAID។ initramfs ជាបរិស្ថានបណ្តោះអាសន្នដែលផ្ទុក driver ឬ tool ចាំបាច់ដើម្បីស្វែងរក និង mount root filesystem មុនប្ដូរទៅ root ពិត។

## សង្កេត

~~~bash
cat /proc/cmdline
findmnt /
systemd-analyze time
systemd-analyze critical-chain
journalctl -b -p warning --no-pager
~~~

systemd-analyze អាចមិនមានលើ distro មិនប្រើ systemd។ ពេលវេលា boot គួរបកស្រាយជាមួយ dependency និង hardware; មិនមែនគ្រប់ delay សុទ្ធតែអាចកាត់ចេញបានដោយសុវត្ថិភាពទេ។

## Recovery គំនិត

បើ root filesystem មិនអាច mount បាន មូលហេតុអាចជា UUID/parameter ខុស, driver បាត់, storage មិនទាន់រួច ឬ filesystem បញ្ហា។ កត់សារ error និងបញ្ជាក់ថាតើ kernel អាចរក block device បានមុនធ្វើ repair។ ការកែ bootloader ឬ filesystem ត្រូវធ្វើនៅ VM/lab និងមាន backup។

## លំហាត់

1. ពិនិត្យ /proc/cmdline និងស្វែងរក root= ប្រសិនបើមាន។
2. មើល critical-chain ហើយជ្រើស unit មួយដែលចំណាយពេលយូរ ដោយកុំបិទវា។
3. គូរខ្សែ boot ចាប់ពី firmware ដល់ login prompt។
