# Capstone Lab៖ ស៊ើបអង្កេតកម្មវិធីមួយពី command ដល់ kernel

## គោលដៅ

បង្កើតរបាយការណ៍តូចមួយបង្ហាញថាអ្នកអាចភ្ជាប់ file format, process, memory, file descriptors, syscalls និង network/log evidence ចូលជារូបភាពតែមួយ។

## ជំហាន

1. ជ្រើស binary ដែលជាផ្នែកប្រព័ន្ធស្តង់ដារ និងទុកចិត្តបាន ដូចជា /bin/echo ឬ /bin/sleep។
2. ប្រើ file/readelf ដើម្បីសង្កេត ELF type និង interpreter។ កត់ថា tool មួយណាមិនមាន។
3. រត់ process test ផ្ទាល់ខ្លួន ហើយកត់ PID/PPID/state។
4. អាន /proc/PID/maps និង /proc/PID/fd ដោយកុំអាន memory payload។
5. ប្រើ strace លើ command សាមញ្ញរបស់ខ្លួន ប្រសិនបើមានសិទ្ធិ។
6. ប្រសិនបើមាន local demo service សូមកត់ socket និង route ដោយមិន capture traffic អ្នកដទៃ។
7. សរសេរ timeline និងគំនូស៖ shell → execve → loader → process → syscall → kernel resource។
8. សរសេរផ្នែក limitation: អ្វីដែលអ្នកមិនអាចដឹងពី observation ទាំងនេះ។

## របាយការណ៍ដែលត្រូវដាក់

- OS/kernel version និង environment (លុប hostname/username ប្រសិនបើមិនចាំបាច់)
- Commands ដែលបានរត់ និង output សង្ខេប
- គំនូស process/memory/FD/syscall
- Observations និង hypothesis បំបែកដាច់គ្នា
- Privacy/security notes និងបញ្ហាដែលមិនទាន់ដោះស្រាយ

## វិធីវាយតម្លៃខ្លួនឯង

- មិនបង្ហោះ secret, token, personal path ឬ packet payload។
- មិន claim លើសពី evidence ដែលបានប្រមូល។
- អាចពន្យល់តួនាទី kernel និង user-space tool នីមួយៗ។
- អាចបញ្ជាក់ថា lab បានដំណើរការលើ environment ដែលអ្នកគ្រប់គ្រង។
