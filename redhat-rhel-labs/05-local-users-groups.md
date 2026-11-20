# Lab ៥៖ គ្រប់គ្រង Local Users និង Groups (Manage Local Users and Groups)

## គោលបំណង
យល់ពី user, group, UID/GID និងពិនិត្យ local accounts។ ការបង្កើត ឬលុប account ត្រូវធ្វើតែក្នុង VM សាកល្បង និងមានការអនុញ្ញាត។

## ១. ពិនិត្យអ្នកប្រើបច្ចុប្បន្ន
```bash
whoami
id
id root
groups
getent passwd
getent group
```
`id` បង្ហាញ UID, primary GID និង supplementary groups។ `getent` ស្វែងរកទិន្នន័យតាមប្រព័ន្ធ NSS មិនមែនតែឯកសារ local ប៉ុណ្ណោះទេ។

## ២. ពិនិត្យ account មួយ
```bash
getent passwd nobody
getent group wheel
```
កុំសន្មតថា UID ឬ GID ជាក់លាក់ដូចគ្នានៅគ្រប់ប្រព័ន្ធ។

## ៣. បង្កើត user សាកល្បង (ជាជម្រើស)
ត្រូវការសិទ្ធិ administrator និង VM ដែលអ្នកគ្រប់គ្រង។ មុនអនុវត្ត សូមបង្កើត snapshot។
```bash
sudo useradd -m labuser
sudo passwd labuser
id labuser
```
កំណត់ password សាកល្បងដែលមិនប្រើនៅគណនីផ្សេង។ កុំដាក់ password ជាអក្សរធម្មតាក្នុង command ឬ script។

## ៤. Group សាកល្បង
```bash
sudo groupadd labteam
sudo usermod -aG labteam labuser
id labuser
```
Option `-aG` បន្ថែម supplementary group ដោយរក្សាក្រុមដែលមានស្រាប់។ បើភ្លេច `-a` អាចជំនួសបញ្ជី supplementary groups។

## ៥. លំហាត់
1. ប្រើ `id` ដើម្បីពិនិត្យ UID/GID របស់អ្នក។
2. ប្រើ `getent passwd` ដើម្បីស្វែងរក account។
3. ប្រសិនបើបានបង្កើត `labuser`, បង្ហាញ group របស់វា។
4. ពន្យល់ភាពខុសគ្នារវាង primary group និង supplementary group។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំយល់ពី UID និង GID។
- [ ] ខ្ញុំអាចពិនិត្យ groups របស់ user។
- [ ] ខ្ញុំយល់ពីផលប៉ះពាល់នៃ `usermod -aG`។

**សុវត្ថិភាព:** កុំកែ ឬលុប account ប្រព័ន្ធ។ កុំបន្ថែម user ទៅ `wheel` លុះត្រាតែមានហេតុផល និងការអនុញ្ញាតច្បាស់លាស់។
