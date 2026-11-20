# Lab ៨៖ គ្រប់គ្រង Services និង Daemons (Control Services and Daemons)

## គោលបំណង
ស្គាល់ service និងប្រើ `systemctl` ដើម្បីពិនិត្យស្ថានភាព service នៅ RHEL ដែលប្រើ systemd។

## ១. ពិនិត្យ systemd
```bash
systemctl is-system-running
systemctl list-units --type=service --state=running
```
លទ្ធផលអាចខុសគ្នាតាម VM និង services ដែលបានដំឡើង។

## ២. ពិនិត្យ service ជាក់លាក់
```bash
systemctl status sshd
systemctl is-active sshd
systemctl is-enabled sshd
```
`status` បង្ហាញព័ត៌មានលម្អិត, `is-active` ពិនិត្យថាកំពុងដំណើរការឬអត់, `is-enabled` ពិនិត្យថាបានកំណត់ឱ្យចាប់ផ្ដើមនៅ boot ឬអត់។

## ៣. មើលព័ត៌មាន unit
```bash
systemctl cat sshd
systemctl list-unit-files --type=service
```
ប្រសិនបើ `sshd` មិនមាន សូមជ្រើស service ដែលមាននៅក្នុង VM របស់អ្នក ហើយពិនិត្យដោយ `systemctl status NAME`។

## ៤. ការចាប់ផ្ដើម/បញ្ឈប់ service (តែ Lab VM)
បញ្ជា start/stop/restart អាចប៉ះពាល់ការភ្ជាប់ និងសេវាកម្ម។ កុំបញ្ឈប់ SSH ប្រសិនបើអ្នកចូល VM តាម SSH។
```bash
sudo systemctl start sshd
sudo systemctl status sshd
```
អនុវត្តតែបើអ្នកមានសិទ្ធិ និងចង់ចាប់ផ្ដើម SSH server ក្នុង VM។ កុំបើក service ដោយស្វ័យប្រវត្តិដោយមិនចាំបាច់។

## លំហាត់
1. រាយ service ដែលកំពុងដំណើរការ។
2. ពិនិត្យ `sshd` ឬ service ផ្សេងដែលមាន។
3. កត់ស្ថានភាព active និង enabled។
4. ពន្យល់ភាពខុសគ្នារវាង service active និង enabled។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចប្រើ systemctl status។
- [ ] ខ្ញុំយល់ពី active និង enabled។
- [ ] ខ្ញុំមិនបញ្ឈប់ service ដោយមិនដឹងផលប៉ះពាល់។

**សុវត្ថិភាព:** ត្រូវមាន console access និង snapshot មុនកែ service សំខាន់។
