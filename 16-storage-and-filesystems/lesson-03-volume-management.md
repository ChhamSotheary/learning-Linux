# មេរៀនទី ៣៖ LVM, RAID និង Encryption

LVM បង្កើត abstraction volume លើ physical volume និង volume group; logical volume អាចផ្លាស់ប្តូរទំហំតាមស្ថានភាព។ RAID គោលបំណង redundancy ឬ performance តាម level។ Encryption at rest ការពារទិន្នន័យលើ media ពេលបិទ/ដក drive ប៉ុន្តែមិនការពារ file ដែលបាន unlock ពេលប្រព័ន្ធដំណើរការទេ។

## អាន topology

~~~bash
lsblk -o NAME,TYPE,SIZE,FSTYPE,MOUNTPOINTS
cat /proc/mdstat
~~~

pvs/vgs/lvs និង mdadm status អាចប្រើសម្រាប់ប្រព័ន្ធដែលមាន tools ទាំងនេះ។ មេរៀននេះមិនបង្កើត ឬប្ដូរ volume ទេ។ RAID មិនមែនជា backup ហើយ encryption បាត់ key អាចធ្វើឱ្យ data មិនអាចស្ដារបាន។

## លំហាត់

គូរ topology របស់ lab ឬគូរឧទាហរណ៍ disk → LUKS → LVM → filesystem → mount។ សម្គាល់ failure ដែល RAID អាចទប់ទល់ និង failure ដែលត្រូវការ backup។
