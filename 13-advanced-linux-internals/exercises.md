# លំហាត់ និង Lab សរុប — Linux Internals កម្រិតខ្ពស់

## ច្បាប់ Lab

ប្រើ VM ឬ lab ផ្ទាល់ខ្លួន។ ក្នុងផ្នែកនេះ command ទាំងអស់គឺសម្រាប់ការអាន/សង្កេត។ កុំបង្កើត namespace privileged, កុំសរសេរ cgroup control file, កុំបិទ security policy និងកុំបង្កើត memory pressure ដោយចេតនាលើម៉ាស៊ីនដែលប្រើប្រាស់ពិត។

## Lab ១៖ ផែនទី process មួយ

1. ជ្រើស process ផ្ទាល់ខ្លួនដែលមិនមានទិន្នន័យរសើប។
2. កត់ PID, parent PID, state និង thread count ពី ps និង /proc/PID/status។
3. ប្រសិនបើ strace មាន សង្កេត command សាមញ្ញរបស់ខ្លួនឯង ហើយរក file-related syscall។
4. ពន្យល់ថាតើអ្វីកើតនៅ user space និងអ្វីឆ្លងទៅ kernel។

## Lab ២៖ តើ container isolation មានអ្វីខ្លះ?

លើ host ឬ container ដែលអ្នកមានសិទ្ធិ inspect៖
1. ប្រៀបធៀប /proc/self/ns និង /proc/1/ns។
2. អាន /proc/self/cgroup។
3. កត់ថាតើ PID, mount និង network view ខុសគ្នាឬអត់។
4. សរសេរថាតើអ្វីដែលទិន្នន័យនេះមិនអាចបញ្ជាក់បានអំពី security។

## Lab ៣៖ ស្វែងរក service dependency

1. ជ្រើស service ដែលមិនសំខាន់។
2. ប្រើ systemctl cat/show/list-dependencies ដោយមិនកែ unit។
3. គូរខ្សែ dependency និង ordering។
4. ពិនិត្យ log boot ចុងក្រោយតាម journalctl ហើយកត់តែ error ដែលពាក់ព័ន្ធ។

## Lab ៤៖ Memory/Performance snapshot

ក្នុងពេលធម្មតា ប្រមូល uptime, free, vmstat និង PSI (ប្រសិនបើមាន) ពីរដង ដោយចន្លោះពេលថេរ។ កត់ workload និងម៉ោង។ សរសេរសម្មតិកម្មមួយ ហើយរាយការវាស់បន្ថែមដែលត្រូវការមុនសម្រេចចិត្ត optimize។

## Lab ៥៖ Threat model សម្រាប់ container

គូរទ្រព្យសម្បត្តិ (data/secrets), attacker, entry points, privilege និង resource limits។ បន្ទាប់មកកំណត់ mitigation ដែលអាចផ្ទៀងផ្ទាត់បាន៖ non-root, capabilities តិច, seccomp/LSM, read-only filesystem តាមសមស្រប, resource limits និង image provenance។

## សំណួរឆ្លើយពិនិត្យ

1. តើ namespace និង cgroup ខុសគ្នាត្រង់គោលបំណងអ្វី?
2. ហេតុអ្វី Requires= មិនមានន័យថា unit មួយចាប់ផ្តើមមុន unit មួយទៀត?
3. ហេតុអ្វី MemFree មួយលេខមិនគ្រប់គ្រាន់សម្រាប់វិនិច្ឆ័យ memory?
4. តើ capabilities, seccomp និង LSM កាត់បន្ថយហានិភ័យតាមរបៀបណាខុសគ្នា?
5. តើហានិភ័យពិសេសរបស់ container ដែលប្រើ privileged mode ឬ mount runtime socket ជាអ្វី?

## សញ្ញាថារៀនចេះ

អ្នកអាចបង្ហាញ command និងភស្តុតាងដែលអ្នកប្រមូលបាន, បែងចែក fact ពីសម្មតិកម្ម, ពន្យល់ហានិភ័យនៃការកែប្រែ និងប្រាប់ផ្លូវ rollback មុនធ្វើការផ្លាស់ប្តូរណាមួយ។
