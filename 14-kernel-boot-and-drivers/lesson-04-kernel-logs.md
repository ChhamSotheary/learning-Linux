# មេរៀនទី ៤៖ Kernel Log និង Boot Errors

## ប្រមូលសារតាម boot

~~~bash
journalctl -k -b --no-pager
journalctl -k -b -p warning --no-pager
dmesg --level=err,warn | tail -n 80
~~~

កម្រិត dmesg អាចត្រូវបានកំណត់ដោយប្រព័ន្ធ។ Kernel log ជាព័ត៌មានមានតម្លៃ តែអាចបង្ហាញ hardware ID, path និងព័ត៌មានផ្ទៃក្នុង។ ពិនិត្យមុនចែករំលែក។

## អាន log មិនឱ្យច្រឡំ

- ស្វែងរកពេលកើតឡើង និងការកើតឡើងដដែលៗ។
- បែងចែក warning ដែលមិនទាក់ទងពី error ដែលកើតជាមួយរោគសញ្ញា។
- ស្វែងរក device/driver ឬ subsystem ដែលមានឈ្មោះ។
- ប្រៀបធៀប boot មុន និងក្រោយការផ្លាស់ប្តូរ។
- កុំចាត់ទុក log ចុងក្រោយជាមូលហេតុដោយស្វ័យប្រវត្តិ។

## លំហាត់

យក kernel log ក្នុង VM របស់អ្នក ហើយសង្ខេប ៣ សារ៖ ពេលវេលា, component, severity, និងតើវាពាក់ព័ន្ធនឹងរោគសញ្ញាឬទេ។ កុំបង្ហោះអត្តសញ្ញាណ hardware/host ប្រសិនបើមិនចាំបាច់។
