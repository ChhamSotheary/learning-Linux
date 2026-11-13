# ចម្លើយណែនាំ៖ មេរៀនទី ៦

## ផ្នែក A

1. PID ជាលេខសម្គាល់ process មួយនៅក្នុងប្រព័ន្ធ។
2. ps បង្ហាញ process snapshot; top បង្ហាញ process/resources បន្តផ្ទាល់; pgrep ស្វែងរក PID តាមឈ្មោះ។
3. SIGTERM ស្នើឱ្យ process បញ្ចប់ដោយមានឱកាសសម្អាត។ SIGKILL បង្ខំបញ្ចប់ភ្លាមៗ ហើយមិនអាចចាប់ដោយ process បាន។
4. status អានស្ថានភាព និងព័ត៌មាន service។ restart បញ្ឈប់/ចាប់ផ្ដើម service ឡើងវិញ ហើយប្ដូរស្ថានភាពប្រព័ន្ធ។
5. Logs អាចបង្ហាញមូលហេតុដើម។ Restart មុនពិនិត្យអាចបាត់បង់ context ឬបង្ក downtime ដោយមិនដោះស្រាយមូលហេតុ។

## ផ្នែក B

sleep 60 & បង្កើត background process; $! សំដៅ PID របស់វា។ kill -TERM "$!" ស្នើឱ្យ process នោះបញ្ចប់។ ពេលវេលាពិតអាស្រ័យថាតើ process បានបញ្ចប់ដោយខ្លួនឯងមុនពេល command ឬអត់។

## ផ្នែក C

លទ្ធផលខុសគ្នាតាម system និង permissions។ ប្រសិនបើ journal មិនអនុញ្ញាតឱ្យអាន អ្នកអាចកត់ថា permission ត្រូវការបន្ថែម ហើយមិនចាំបាច់ប្រើ sudo ដើម្បីបំពេញលំហាត់ទេ។ កុំចម្លង logs ដែលមាន identifiers ឬ secrets ទៅទីសាធារណៈ។
