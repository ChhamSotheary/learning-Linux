# មេរៀនទី ២៖ Kernel Modules និង Driver

Module ជាកូដដែលអាចផ្ទុកចូល/ដកចេញពី kernel នៅ runtime។ Driver ជាច្រើនត្រូវបានផ្តល់ជា module ប៉ុន្តែមុខងារមួយចំនួនអាចបង្កើតជាប់ក្នុង kernel ផងដែរ។ Module មិនមែនជាកម្មវិធី user-space ធម្មតាទេ ហើយកំហុសអាចប៉ះពាល់ដល់ kernel ទាំងមូល។

## សង្កេតដោយសុវត្ថិភាព

~~~bash
lsmod | head
modinfo ext4
lspci -k
ls /sys/module | head
~~~

lspci អាចត្រូវការកញ្ចប់ pciutils។ កុំរត់ modprobe/rmmod ឬសាកល្បង module មិនទុកចិត្តលើម៉ាស៊ីនដែលប្រើប្រាស់ពិត។ ឈ្មោះ module និង driver អាចខុសតាម hardware/kernel។

## សំណួរពេល troubleshoot

- Device ត្រូវបាន firmware/PCI/USB រកឃើញទេ?
- Kernel ចង device ជាមួយ driver ណា?
- មាន error ក្នុង journalctl -k ឬ dmesg ទេ?
- Secure Boot ឬ module signing policy រារាំង module ទេ?
- តើបញ្ហាចាប់ផ្តើមក្រោយ kernel update ឬ firmware update?

## លំហាត់

1. ប្រើ lspci -k ឬ lsusb -t ដើម្បីរក driver សម្រាប់ device មួយ។
2. រក module ដែលពាក់ព័ន្ធ និងមើល description/version ដោយ modinfo។
3. សរសេរភស្តុតាងណាដែលត្រូវប្រមូល មុនផ្លាស់ប្ដូរ driver។
