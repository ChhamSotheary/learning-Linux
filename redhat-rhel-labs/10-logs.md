# Lab ១០៖ វិភាគ និងរក្សាទុក Logs (Analyze and Store Logs)

## គោលបំណង
ស្វែងរក system logs, ពិនិត្យ journal និងត្រងសារដែលពាក់ព័ន្ធនឹង service ឬពេលវេលា។

## ១. មើល Journal
```bash
journalctl
journalctl -n 20
journalctl -p warning
```
ចុច `q` ដើម្បីចេញពី pager។ `-n 20` បង្ហាញ 20 entries ចុងក្រោយ។ Priority warning និងខ្ពស់ជាងនេះត្រូវបានបង្ហាញដោយ `-p warning`។

## ២. ពិនិត្យ Boot logs
```bash
journalctl -b
journalctl --list-boots
```
`-b` បង្ហាញ logs របស់ boot បច្ចុប្បន្ន។ ចំនួន boot ដែលរក្សាទុកអាស្រ័យលើ journal configuration។

## ៣. Logs របស់ service
```bash
journalctl -u sshd
journalctl -u sshd -n 30
```
ប្រសិនបើ service មិនមាន សូមប្រើ unit ដែលមានក្នុងប្រព័ន្ធ។

## ៤. ស្វែងរកតាមពេលវេលា
```bash
journalctl --since "1 hour ago"
journalctl --since today
```
ពាក្យពេលវេលាត្រូវបានបកស្រាយដោយ journalctl; តំបន់ម៉ោង និងនាឡិកាប្រព័ន្ធអាចប៉ះពាល់លទ្ធផល។

## ៥. រក្សាទុកលទ្ធផលសម្រាប់ Lab
```bash
mkdir -p "$HOME/rhel-labs/lab10"
journalctl -b -n 50 > "$HOME/rhel-labs/lab10/boot-log-sample.txt"
```
ឯកសារនេះអាចមាន hostname, usernames, IP ឬព័ត៌មានផ្ទៃក្នុង។ កុំបង្ហោះ logs ទៅទីសាធារណៈដោយមិនពិនិត្យ/លាក់ព័ត៌មានសម្ងាត់។

## លំហាត់
1. បង្ហាញ logs 20 entries ចុងក្រោយ។
2. ស្វែងរក warning និង error។
3. ពិនិត្យ logs របស់ sshd ប្រសិនបើមាន។
4. រក្សាទុក sample 50 entries ក្នុង workspace។
5. សរសេរពន្យល់ថា log មួយអាចជួយស្វែងរកមូលហេតុបញ្ហាយ៉ាងដូចម្តេច។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចប្រើ journalctl។
- [ ] ខ្ញុំអាចត្រងតាម service និងពេលវេលា។
- [ ] ខ្ញុំដឹងថា logs អាចមានព័ត៌មានរសើប។
