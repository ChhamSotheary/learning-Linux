# Final Project 01: Linux Workstation និង Backup

## គោលដៅ

រៀបចំ workstation Linux ឬ VM សម្រាប់ការងារប្រចាំថ្ងៃ ដោយមាន user-level workspace, package inventory, backup/restore test និងកំណត់ត្រា system health។

## Scope

- ប្រើ user account ធម្មតា និងរៀបចំ project directories។
- កត់ distro, kernel version, packages សំខាន់ៗ និង storage usage។
- បង្កើត backup archive នៃ directory សាកល្បង ឬ data ដែលអ្នកមានសិទ្ធិ។
- ផ្ទៀងផ្ទាត់ archive ហើយសាក restore ទៅទីតាំងថ្មី។
- បង្កើត Bash script របាយការណ៍ដែលសរសេរទៅ workspace ផ្ទាល់ខ្លួន។
- កត់ត្រា backup schedule, retention និង recovery steps។

កុំ backup ឬចែករំលែក files របស់អ្នកដទៃ ឬ data ដែលអ្នកមិនមានសិទ្ធិ។ កុំទុក backup តែមួយនៅលើ disk ដូចគ្នាជាប្រភព។

## Deliverables

- README/setup notes។
- System inventory ដែលលាក់ serial numbers, private paths ឬ sensitive details។
- Backup archive និង restore verification។
- Script/report output និងពន្យល់ exit status។
- Recovery checklist និងចំណុចដែលនៅត្រូវកែលម្អ។

## Rubric

- Workspace និង permissions មានរបៀប: 20%
- Script មាន input/error handling: 20%
- Backup archive អាច restore បាន: 25%
- Maintenance/security notes: 20%
- Documentation និង privacy: 15%

## Self-review

- តើ backup ត្រូវបាន restore សាកល្បងទេ?
- តើ data សម្ងាត់ត្រូវបានការពារ/encrypted តាមតម្រូវការទេ?
- តើ script អាចសរសេរទៅក្រៅ workspace ដោយចៃដន្យទេ?
- តើអ្នកអាចស្ដារការងារបន្ទាប់ពី disk failure ដោយជំហានណា?
