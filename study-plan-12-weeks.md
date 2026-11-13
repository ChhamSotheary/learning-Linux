# ផែនការរៀន Linux រយៈពេល ១២ សប្ដាហ៍

ផែនការនេះរៀបចំមេរៀនទាំង ១៧ ម៉ូឌុលជាកាលវិភាគអនុវត្ត។ កំណត់ពេល ៥ ថ្ងៃក្នុងមួយសប្ដាហ៍ ប្រហែល ៤៥–៩០ នាទីក្នុងមួយថ្ងៃ។ បើរវល់ អ្នកអាចរៀនតិចជាងនេះ ហើយបន្តតាមល្បឿនខ្លួនឯង។

## របៀបរៀនរាល់សប្ដាហ៍

- ថ្ងៃទី ១–៣៖ អានមេរៀន និងសាក command ក្នុង VM/WSL2។
- ថ្ងៃទី ៤៖ ធ្វើលំហាត់ ហើយកត់ចម្លើយជាពាក្យខ្លួនឯង។
- ថ្ងៃទី ៥៖ ពិនិត្យឡើងវិញ និងធ្វើកំណត់ត្រា៖ អ្វីចេះ, អ្វីមិនទាន់ច្បាស់, ត្រូវសាកអ្វីបន្ថែម។
- សាកល្បងតែក្នុង VM ឬប្រព័ន្ធដែលអ្នកមានសិទ្ធិប្រើ។ សម្រាប់ command ដែលផ្លាស់ប្ដូរ disk, network, service, kernel ឬ security policy សូមអានឯកសារមុន និងមាន rollback។

## សប្ដាហ៍ទី ១៖ Linux និង Terminal

រៀន [មេរៀន ១](01-introduction/lesson.md) និង [មេរៀន ២](02-terminal-command-line/lesson.md)។

**អនុវត្ត៖** ស្គាល់ distribution, kernel version, shell, command history, help/manual, path និងការប្រើ command ជាមួយ option។

**លទ្ធផល៖** អ្នកអាចពន្យល់ថាកំពុងប្រើ Linux distro អ្វី និងប្រើ terminal ដើម្បីស្វែងរកជំនួយបាន។

## សប្ដាហ៍ទី ២៖ Filesystem និង Permissions

រៀន [Filesystem](03-filesystem-file-management/lesson.md) និង [Users, Groups, Permissions](04-users-groups-permissions/lesson.md)។

**អនុវត្ត៖** បង្កើត directory សាកល្បង, ចម្លង/ផ្លាស់ទី/ស្វែងរក file, ពិនិត្យ owner, group, mode និង umask។

**លទ្ធផល៖** អាចពន្យល់ថាហេតុអ្វី user ម្នាក់អាច ឬមិនអាចអាន/កែ file មួយ។

## សប្ដាហ៍ទី ៣៖ Packages, Processes និង Services

រៀន [Package Management](05-package-management/lesson.md) និង [Processes, Services, Logs](06-processes-services-logs/lesson.md)។

**អនុវត្ត៖** ស្វែងរក package, មើល process, ពិនិត្យ service status និង journal logs។ កុំបិទ service ដែលមិនស្គាល់។

**លទ្ធផល៖** អាចរកឃើញថា process/service កំពុងដំណើរការឬអត់ និងរក log ដែលពាក់ព័ន្ធ។

## សប្ដាហ៍ទី ៤៖ Networking និង Bash

រៀន [Networking Fundamentals](07-networking-fundamentals/lesson.md) និង [Bash Scripting](08-bash-scripting-automation/lesson.md)។

**អនុវត្ត៖** ពិនិត្យ IP, route, DNS និងសរសេរ script តូចមួយសម្រាប់រាយការណ៍ព័ត៌មានប្រព័ន្ធដោយមិនកែប្រែវា។

**លទ្ធផល៖** អាចបំបែកបញ្ហា DNS, route និង service តាមជំហានមូលដ្ឋាន។

## សប្ដាហ៍ទី ៥៖ Disk, Backup និង Security

រៀន [Disk, Filesystem, Backup](09-disk-filesystem-backup/lesson.md) និង [Security, Monitoring](10-security-monitoring/lesson.md)។

**អនុវត្ត៖** ប្រើ file សាកល្បងក្នុងការបង្កើត និងផ្ទៀងផ្ទាត់ backup; ពិនិត្យ permission និង resource usage។ កុំធ្វើ format disk ពិត។

**លទ្ធផល៖** មាន backup ដែលបានសាក restore ក្នុងទីតាំងសាកល្បង និងយល់ពីហេតុអ្វី backup មិនដូច RAID។

## សប្ដាហ៍ទី ៦៖ Troubleshooting និងគម្រោងមូលដ្ឋាន

រៀន [Troubleshooting និង System Administration](11-troubleshooting-system-administration/lesson.md) និងជ្រើសគម្រោងមួយពី [Final Projects](12-final-projects/README.md)។

**អនុវត្ត៖** ដោះស្រាយបញ្ហាសាកល្បងមួយដោយកត់ symptom, evidence, hypothesis, fix និង verification។

**លទ្ធផល៖** មិនសន្និដ្ឋានពី log ឬ metric តែមួយ ហើយអាចបង្ហាញភស្តុតាងនៃការដោះស្រាយ។

## សប្ដាហ៍ទី ៧៖ Process និង System Call Internals

រៀន [Linux Internals ១៖ Process ទៅ System Call](13-advanced-linux-internals/lesson-01-processes-and-system-calls.md) និង [២៖ Namespaces និង Cgroups](13-advanced-linux-internals/lesson-02-namespaces-and-cgroups.md)។

**អនុវត្ត៖** អាន /proc/self/status, សង្កេត namespace និង cgroup របស់ខ្លួន។ ប្រើ strace លើ command សាមញ្ញរបស់ខ្លួន ប្រសិនបើមាន។

**លទ្ធផល៖** អាចពន្យល់ system call, namespace និង cgroup ខុសគ្នាយ៉ាងណា។

## សប្ដាហ៍ទី ៨៖ systemd និង Performance

រៀន [systemd dependencies](13-advanced-linux-internals/lesson-03-systemd-dependencies.md), [performance observability](13-advanced-linux-internals/lesson-04-performance-observability.md) និង [memory pressure](13-advanced-linux-internals/lesson-05-memory-pressure.md)។

**អនុវត្ត៖** ប្រមូល snapshot uptime/free/vmstat/PSI និងពិនិត្យ dependency/log របស់ service ដោយមិនកែ config។

**លទ្ធផល៖** អាចបង្កើត hypothesis ពីទិន្នន័យ និងប្រាប់ថាត្រូវវាស់អ្វីបន្ថែម។

## សប្ដាហ៍ទី ៩៖ Security និង Containers

រៀន [Capabilities, Seccomp, LSM](13-advanced-linux-internals/lesson-06-linux-security-boundaries.md), [Container Security](13-advanced-linux-internals/lesson-07-container-security.md) និងលំហាត់ក្នុង [Advanced Internals](13-advanced-linux-internals/exercises.md)។

**អនុវត្ត៖** សរសេរ threat model សម្រាប់ app container និងកត់ privilege/secret/resource ដែលត្រូវការពារ។ កុំបិទ security controls ដើម្បីសាក។

**លទ្ធផល៖** អាចបែងចែក capabilities, seccomp, LSM និង resource limits បាន។

## សប្ដាហ៍ទី ១០៖ Boot និង Kernel

រៀនទាំង [មេរៀន Boot, Kernel និង Driver](14-kernel-boot-and-drivers/README.md)។

**អនុវត្ត៖** គូរ boot chain, អាន /proc/cmdline និង kernel log, សង្កេត driver ដែលភ្ជាប់ device។

**លទ្ធផល៖** អាចពន្យល់បញ្ហា boot មូលដ្ឋាន និងដឹងថាត្រូវប្រមូលភស្តុតាងអ្វី មុនកែ kernel/driver។

## សប្ដាហ៍ទី ១១៖ Networking កម្រិតខ្ពស់ និង Storage

រៀន [Advanced Networking](15-advanced-networking/README.md) និង [Storage Internals](16-storage-and-filesystems/README.md)។

**អនុវត្ត៖** ពិនិត្យ route, socket, interface counters, block device/mount និង inode usage។ គូរ packet path និង storage stack។

**លទ្ធផល៖** អាចបែងចែកបញ្ហា network layer និង storage layer តាមភស្តុតាង។

## សប្ដាហ៍ទី ១២៖ Reliability និង Capstone

រៀន [Linux Operations និង Reliability](17-linux-operations-and-reliability/README.md) ហើយបញ្ចប់ [Capstone](17-linux-operations-and-reliability/capstone.md)។

**អនុវត្ត៖** រៀបចំ service សាកល្បងក្នុង VM, runbook, backup/restore drill, security review និង incident timeline។

**លទ្ធផល៖** អ្នកអាចបង្ហាញ architecture, evidence, rollback និងការស្ដារសេវាដោយសុវត្ថិភាព។

## តារាងតាមដាន

ចម្លងតារាងនេះទៅកំណត់ត្រាផ្ទាល់ខ្លួន ហើយបំពេញវារៀងរាល់សប្ដាហ៍៖

| សប្ដាហ៍ | ស្ថានភាព | អ្វីដែលខ្ញុំចេះ | អ្វីដែលត្រូវសួរ/ហាត់បន្ថែម |
|---|---|---|---|
| ១ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ២ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ៣ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ៤ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ៥ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ៦ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ៧ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ៨ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ៩ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ១០ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ១១ | មិនទាន់ចាប់ផ្ដើម |  |  |
| ១២ | មិនទាន់ចាប់ផ្ដើម |  |  |

## បន្ទាប់ពី ១២ សប្ដាហ៍

បើអ្នកបានបញ្ចប់មេរៀន និង capstone ក្នុង repo នេះ នោះអ្នកបានបញ្ចប់កម្មវិធីសិក្សាដែលបានរៀបចំ។ ជំហានបន្ទាប់គឺជ្រើសឯកទេសមួយ ដូចជា Linux server administration, cloud, DevOps/SRE, cybersecurity ឬ kernel development ហើយបង្កើត lab/project ស្របតាមគោលដៅនោះ។
